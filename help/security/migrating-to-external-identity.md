---
title: 移轉至外部身分和動態群組成員資格
description: 在AEM as a Cloud Service中將本機使用者和群組移轉至具有動態群組成員資格的外部身分模型的技術指南
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: 1f8bd9eea249e0b2242f3fbe1490b3d51052f546
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 1%

---

# 移轉至外部身分和動態群組成員資格 {#migrating-to-external-identity}

## 概觀 {#overview}

在AEM as a Cloud Service中啟用[資料同步處理](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization)時，可以將SAML驗證處理常式設定為在管理使用者和群組建立時，自動移轉至具有動態群組成員資格的外部身分識別。 如果您的專案使用自訂程式碼來建立使用者或群組，您必須更新以建立外部使用者和群組，而不是本機使用者和群組。

### 為何需要外部使用者和群組 {#why-external-required}

出於幾個重要原因，從本機使用者和群組移轉至具有動態群組成員資格的外部身分至關重要：

**效能最佳化：**

* **減少的存放庫寫入**：傳統的本機群組成員資格要求將成員資格關係寫入群組節點的單一多值屬性中的存放庫。 使用動態群組成員資格時，使用者會擁有包含所有群組主參與者的單一`rep:externalPrincipalNames`屬性，不需要同步處理群組節點
* **更快速的同步處理**：在同步處理發佈層節點間的使用者時，具有動態群組成員資格的外部使用者所需的資料傳輸和寫入作業都比具有傳統群組成員資格的本機使用者少很多
* **擴充性**：擁有大量使用者和群組的系統，會大幅減少存放庫的開銷。 即使對於非常大的群組，動態群組成員資格也能有效擴展。

本檔案提供下列事項的技術指引：

* 瞭解外部身分模型
* 修改自訂程式碼以建立外部使用者和群組
* 將現有的本機使用者和群組移轉至外部身分模型

## 瞭解外部身分 {#understanding-external-identity}

### 外部使用者 {#external-users}

外部使用者由`rep:externalId`屬性識別，該屬性會將使用者連結至外部識別提供者。 格式為：

```
userId;idpName
```

例如：`john.doe;saml-idp`。

>[!NOTE]
>
> `idpName`參考驗證處理常式設定中定義的Oak身分識別提供者(Idp)名稱。 對於SAML整合，這是SAML驗證處理常式中為`idpIdentifier`屬性設定的值。

**金鑰屬性：**

* `rep:externalId`：將使用者標籤為外部的必要屬性（例如，`john.doe;saml-idp`）
* `rep:externalPrincipalNames`：包含動態成員資格之外部群組主體的多值屬性
* `rep:lastSynced`：上次同步的時間戳記
* `rep:lastDynamicSync`：上次動態群組成員資格同步的時間戳記

### 外部群組 {#external-groups}

外部群組也由`rep:externalId`屬性識別，並使用主體名稱格式：

```
groupId;idpName
```

例如：`content-authors;saml-idp`

### 動態群組成員資格 {#dynamic-group-membership}

動態群組成員資格不是儲存於存放庫中的直接使用者與群組關係，而是使用使用者節點上的`rep:externalPrincipalNames`屬性。 當使用者擁有符合外部群組ID的外部主體名稱時，他們會自動成為該群組的成員。 如需詳細資訊，請參閱[Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)。

**優點：**

* 減少存放庫寫入次數（新增/移除群組中的使用者時，不會修改任何群組成員資格節點）
* 更快速地跨發佈層節點進行同步
* 可擴充的群組成員資格管理
* 與資料同步需求相容

## 服務使用者組態 {#service-user-configuration}

所有建立或修改外部使用者和群組的作業，應該使用已正確設定為略過&#x200B;**和**&#x200B;屬性預設保護的`rep:externalId`服務使用者`rep:externalPrincipalNames`來執行。

### 為什麼需要服務使用者 {#why-is-a-service-user-required}

根據預設，Oak安全性會防止一般工作階段修改受保護的屬性，例如：

* `rep:externalId` — 將使用者/群組標籤為外部
* `rep:externalPrincipalNames` — 儲存動態群組成員資格主體

只有正確設定的服務使用者才能修改這些屬性。

### 服務使用者組態與對應 {#service-user-configuration-mapping}

設定服務使用者以管理外部身分需要三個協調的設定：

1. 透過`repoinit`建立服務使用者
2. 設定`ExternalPrincipal`保護
3. 將服務使用者對應至您的應用程式套件組合。

如需這些步驟的詳細說明，請參閱下文。

#### 步驟1：透過Repoinit建立服務使用者 {#create-the-serviice-user-via-repoinit}

此步驟詳細說明如何使用`repoinit`指令碼建立具有必要許可權的服務使用者。

**組態檔：** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**示範位置：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**許可權總覽**

* `jcr:read`：讀取使用者和群組
* `jcr:readAccessControl`：讀取ACL
* `jcr:modifyAccessControl`：修改ACL （設定屬性所需）
* `rep:userManagement`：建立和管理使用者/群組
* `rep:write`：寫入包含`rep:externalId`和`rep:externalPrincipalNames`的屬性

>[!NOTE]
>
>服務使用者是在`/home/users/system/yourproject`下建立，以便與其他系統使用者一起保持井然有序。

#### 步驟2：設定ExternalPrincipal保護 {#configure-externalprincipal-protection}

以下是將服務使用者列入白名單的設定範例，這樣就可以略過套用至外部身分屬性的保護。

**設定檔名稱：** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**位置範例：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**組態屬性：**

* `protectExternalIdentities`：控制外部識別屬性的保護等級：
   * `"Strict"`：只有白名單中的系統主體可以修改外部屬性。 這是生產環境建議的等級。
   * `"Warn"`：記錄警告，但允許修改。 對開發/測試非常有用。
   * `"None"`：沒有保護。 不建議使用。
* `systemPrincipalNames`：允許修改`rep:externalId`和`rep:externalPrincipalNames`的服務使用者名稱清單。 包含需要管理外部身分的所有服務使用者（例如，`group-provisioner`、`saml-migration-service`）。

>[!IMPORTANT]
>
>`systemPrincipalNames`中的服務使用者名稱必須與在repoinit指令碼中建立的服務使用者ID完全相符。

#### 步驟3：服務使用者對應 {#service-user-mapping}

將服務使用者對應至您的應用程式套件組合，讓您的程式碼可以使用它。

**組態檔：** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**位置：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**對應格式：**

* `yourproject.core`：符號套件組合名稱（在`pom.xml` `<Bundle-SymbolicName>`中找到）
* `group-provisioner` （在`=`之前）：您將在程式碼中使用的子服務名稱
* `[group-provisioner]` （在`=`之後）：在repoinit中建立的實際服務使用者識別碼

### 在程式碼中使用服務使用者 {#using-the-service-user-in-code}

開啟工作階段以執行移轉或使用者/群組建立作業時，您必須使用服務使用者：

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>如果沒有適當的服務使用者組態，嘗試設定`rep:externalId`或`rep:externalPrincipalNames`將會失敗，並出現許可權錯誤。 在嘗試移轉之前，請確認您的服務使用者已在`ExternalPrincipal`設定中正確設定。

## 完成設定範例 {#complete-configuration-example}

下方提供完整的工作範例，說明這三個設定組合：

### 檔案結構 {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### 修改自訂程式碼 {#modifying-custom-code}

#### 建立外部使用者 {#creating-external-users}

**之前（本機使用者）：**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**之後（外部使用者）：**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### 建立外部群組 {#creating-external-groups}

**之前（本機群組）：**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**之後（外部群組）：**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### 指派動態群組成員資格 {#assigning-dynamic-membership}

**之前（直接成員資格）：**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**之後（動態成員資格）：**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## 移轉程式 {#migration-process}

在啟用Data Synchronization Services之前更新自訂程式碼時，不需要將現有的本機使用者和群組移轉至外部身分。

如果存放庫已保留本機使用者和群組，並且已主動使用環境，我們建議您執行如下的多步驟移轉，以避免中斷或不一致。

>[!IMPORTANT]
>
>所有移轉步驟都必須使用正確設定的服務使用者（例如`group-provisioner`）執行，該使用者已被授與略過`rep:externalId`和`rep:externalPrincipalNames`屬性保護的許可權。 如需詳細資訊，請參閱[服務使用者組態](#service-user-configuration)。

### 步驟1：建立外部群組結構 {#step-1-create-external-group-structure}

對於需要移轉的每個本機群組：

1. 建立主要名稱對應的外部群組： `<localGroupId>;<idpName>`。 使用有助於將外部群組與本機群組連結的命名慣例
1. 在外部群組上設定`rep:externalId`屬性，值為： `<localGroupId>;<idpName>`
1. 將外部群組新增為原始本機群組的成員。

**驗證**

* 您可以檢查每個本機群組是否都有對應的外部群組，以驗證結果。 此外，每個外部群組都是對應本機群組的成員。

**範例Servlet端點：**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**使用狀況：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### 步驟2：轉換使用者並指派動態成員資格 {#step-2-convert-users-and-assign-dynamic-membership}

對於屬於本機群組成員的每個使用者：

1. 確定已設定`rep:externalId` （如有需要，可轉換為外部使用者）。
1. 對於每個群組成員資格，將對應的外部群組主體新增到`rep:externalPrincipalNames`
1. 更新同步時間戳記。

>[!IMPORTANT]
>
>在此過程中略過「所有人」等系統群組。

**範例Servlet端點：**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**使用狀況：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**驗證**

您可以透過檢查每個使用者是否具有每個外部群組的`rep:externalId`的`rep:externalPrincipalName`和`principalName`屬性來驗證此專案。 使用者是本機群組&#x200B;*和外部群組*&#x200B;的成員。

### 步驟3：移除直接使用者成員資格 {#step-3-remove-direct-user-memberships}

使用者設定動態群組成員資格後：

1. 從本機群組移除直接使用者成員資格
1. 保留群組對群組成員資格（包括外部群組成員資格）

**範例Servlet端點：**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**使用狀況：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**驗證**

* 您可以檢查每個本機群組都只有對應的外部群組或其他群組作為成員，以驗證此資訊。


## 移轉工作流程 {#migration-workflow}

### 移轉前檢查清單 {#pre-migration-checklist}

* **設定服務使用者**：建立並設定具有適當許可權的服務使用者（例如`group-provisioner`）
* **驗證ExternalPrincipal設定**：確定服務使用者已設定為略過`rep:externalId`和`rep:externalPrincipalNames`上的保護
* **測試服務使用者許可權**：驗證服務使用者是否可以在開發中設定外部身分屬性
* 識別建立使用者或群組的所有自訂程式碼
* 檢閱並更新自訂程式碼以使用外部身分模型
* 在開發環境中測試更新的程式碼
* 清查所有現有的本機使用者和群組以進行移轉
* 在較低的環境中測試移轉程式

### 執行步驟 {#execution-steps}

1. **部署更新的程式碼**：部署自訂程式碼變更以建立外部使用者/群組

1. **建立外部群組** （針對每個本機群組）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **移轉使用者** （每個使用者）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **清除** （針對每個移轉的群組）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **驗證**：檢查使用者群組成員資格並測試存取許可權

1. **啟用資料同步處理**：請連絡客戶支援以啟用此功能

### 移轉後驗證 {#post-migration-validation}

驗證移轉：

1. **檢查使用者屬性**：

   在使用者節點上驗證是否存在：

   * `rep:externalId`：格式應為`userId;idpName`
   * `rep:externalPrincipalNames`：格式為`groupId;idpName`的群組主體陣列
   * `rep:lastSynced`：時間戳記已設定為遙遠的未來（約自移轉日期起10年）
   * `rep:lastDynamicSync`：時間戳記已設定為遙遠的未來（約自移轉日期起10年）

   **注意**：作為OAK-12079的因應措施，時間戳記會刻意設定為更遠的未來日期。 這是預期的行為。

1. **檢查群組屬性**：

   在本機群組節點上，驗證是否存在：

   * 格式為`groupId;idpName`的外部群組成員
   * 沒有直接使用者成員（僅在步驟3之後）

1. **測試使用者登入**：確認使用者可以登入且擁有正確的許可權

1. **測試存取控制**：確認使用者可以存取受CUG/ACL保護的內容

## 疑難排解 {#troubleshooting}

### 常見問題 {#common-issues}

**問題：設定`rep:externalId`或`rep:externalPrincipalNames`**&#x200B;時出現許可權錯誤

**錯誤訊息：**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**解決方案**：必須使用正確設定的服務使用者開啟工作階段，該使用者已被授與略過外部識別屬性保護的許可權。

**要解析的步驟：**

1. **驗證服務使用者是否存在**：確定服務使用者（例如，`group-provisioner`）是透過repoinit建立的
1. **檢查服務使用者對應**：確認servlet或服務正在使用`repository.loginService("group-provisioner", null)`
1. **驗證ExternalPrincipal設定**：確定`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration`已正確設定
1. **檢查服務使用者許可權**：服務使用者需要`rep:write`和`rep:userManagement`的`/home/users`和`/home/groups`許可權

如需完整的安裝指示，請參閱[服務使用者組態](#service-user-configuration)。

**問題：`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**解決方案**：使用者必須先設定`rep:externalId`，才能設定`rep:externalPrincipalNames`。 請確認步驟2會先將使用者轉換為外部使用者。

**問題：使用者在移轉後失去群組成員資格**

**解決方案**：確認：

* 外部群組是以正確的主體名稱格式(`groupId;idpName`)建立
* 外部群組已新增為本機群組的成員（步驟1）
* 使用者在`rep:externalPrincipalNames`中有正確的外部主體名稱（步驟2）
* 步驟3的清除作業只會在步驟1與步驟2完成後才執行

**問題：外部群組成員資格在使用者登入後意外移除(OAK-12079)**

**問題**：由於Oak發生錯誤[OAK-12079](https://issues.apache.org/jira/browse/OAK-12079)，Oak同步處理機制可能會根據`rep:lastSynced`和`rep:lastDynamicSync`時間戳記提前清除外部群組成員資格。

**解決方案**：將`rep:lastSynced`和`rep:lastDynamicSync`時間戳記設定為遙遠的未來日期（從現在起的10年後），而非目前時間。 這會防止同步處理清理程式移除外部群組成員資格。

**實作：**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**為什麼這個方式會運作**：透過將時間戳記設定為遙遠的未來日期，Oak同步處理邏輯會將這些使用者視為「最近已同步」，不會觸發清除程式，移除外部主要使用者名稱和群組成員資格。

**注意**：這是暫時性的因應措施，直到未來Oak版本中解決OAK-12079為止。 本檔案中的所有程式碼範例已包含此因應措施。

**問題：系統群組「所有人」造成錯誤**

**解決方案**：使用者移轉期間一律略過「所有人」系統群組（步驟2）。 此群組由AEM自動管理。

### 反轉程式 {#rollback-procedure}

如果移轉遇到問題：

1. 停止移轉程式
1. 在關鍵資料受到影響時從備份還原
1. 復原程式碼上的變更，以建立具有動態群組成員資格的外部使用者和群組
1. 在重新嘗試移轉之前，請先檢閱並修正問題。

## 最佳做法 {#best-practices}

* **徹底測試**：在生產之前，一律先在開發和中繼環境中測試移轉
* **批次處理**：對於大型使用者群，請批次處理移轉以避免逾時問題
* **監視效能**：在移轉期間監視存放庫效能
* **維護稽核軌跡**：記錄所有移轉作業以進行疑難排解
* **服務使用者許可權**：確定移轉servlet使用具有必要許可權的適當服務使用者。 服務使用者必須在ExternalPrincipal設定中設定為略過`rep:externalId`和`rep:externalPrincipalNames`屬性的保護
* **等冪操作**：設計移轉程式碼以安全地重新執行
* **在每個步驟驗證**：在繼續之前，請先檢查每個移轉步驟之後的結果

## 保護移轉Servlet的安全 {#securing-migration-servlets}

移轉servlet擁有建立及修改使用者和群組的提升許可權。 限制存取這些端點以防止未經授權的存取至關重要。

### 建議方法： IMS技術帳戶驗證 {#recommended-approach-ims-technical-account}

建議使用Adobe IMS整合來保護這些servlet，只允許授權的技術帳戶存取它們。

#### 步驟1：在AEM Developer Console中建立技術帳戶 {#create-a-technical-account-in-aem-developer-console}

1. 依序導覽至[Experience Manager](https://experience.adobe.com/)和&#x200B;**Cloud Manager**
1. 選取您的方案，然後按一下您要建立技術帳戶的環境
1. 在環境的省略符號選單中，按一下&#x200B;**Developer Console**
1. 在AEM Developer Console中，前往&#x200B;**整合**&#x200B;標籤
1. 按一下&#x200B;**建立新的技術帳戶**
1. 提供整合的名稱（例如「移轉服務帳戶」）
1. 按一下「**建立**」
1. 請注意已建立整合中的下列值：
   * **使用者端識別碼**
   * **使用者端密碼**
   * **技術帳戶ID** （這將是存取您的servlet的使用者ID — 格式： `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`）

如需詳細指示，請參閱[產生伺服器端API的存取權杖檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

檢查呼叫者是否獲得授權的程式碼範例：

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### 深入防禦：IP型限制 {#defense-in-depth-ip-based-restrictions}

作為額外的安全層，您可以設定CDN規則，以依IP位址限制對移轉端點的存取。 從已知的基礎架構執行移轉時，這項功能相當實用。

>[!NOTE]
>
>光有IP限制是不夠的。 如上所述，一律結合驗證檢查。

### 安全性檢查清單 {#security-checklist}

將移轉servlet部署到生產環境之前：

* 在AEM Developer Console中建立IMS整合
* 設定servlet以驗證技術帳戶ID
* 在開發/中繼環境中測試驗證流程
* 考慮CDN層級的其他IP型限制
* 規劃在移轉完成後停用或移除移轉servlet
* 稽核並記錄移轉端點的所有存取權

>[!IMPORTANT]
>
>移轉完成後，請考慮從部署中停用或移除移轉servlet，以消除任何潛在的安全性風險。

## 其他資源 {#additional-resources}

* [發佈層的使用者和群組同步](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=zh-Hant)
* [外部識別提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html?lang=zh-Hant)
* [動態群組成員資格](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
