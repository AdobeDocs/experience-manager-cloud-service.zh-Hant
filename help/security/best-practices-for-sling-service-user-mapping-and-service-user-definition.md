---
title: Sling Service 使用者對應和服務使用者定義的最佳實務
description: 了解 Sling Service 使用者對應和服務使用者定義的最佳實務
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '1883'
ht-degree: 100%

---

# Sling Service 使用者對應和服務使用者定義的最佳實務 {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## 服務使用者對應 {#service-user-mapping}

若要新增從服務到相應系統使用者的對應，您需要為 `ServiceUserMapper` 服務建立工廠設定。為了保持此模組化，可以使用 Sling「修改」機制提供此類設定 (有關更多詳細資訊，請參閱 [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578))。透過搭售方案安裝此類設定的建議方法是將其新增至快速入門設定模型中，如下列範例中所述：

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### 對應格式 {#mapping-format}

從 AEM 6.4 開始，對應格式定義如下：

>[!NOTE]
>
>`userName` 已棄用，不應再使用。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` 和 `subserviceName` 識別服務，`userName/principalNames` 識別服務使用者，`principalNames` 是逗號分隔的清單。

另外，請注意，`principalNames`  是服務使用者主體名稱清單，其開箱即用，與 ID 相同。


**最佳實務**

* 不同任務的子服務名稱 - 如果您的搭售方案的服務執行不同的任務，建議識別 `subserviceNames` 以按任務加以群組
* 如果給定服務執行不同作業 (例如，讀取資產內容和更新 `/var` 子樹狀結構下的資訊)，則建議透過彙總反映個別作業的不同服務主體來反映這一點，例如將一般 `dam-reader-service` 與功能特定 `assetreport-writer-service` 彙總。
* 理想情況下，每個服務都與一組非常特定且有限的作業綁定
*  `[one,or,multiple,principalNames]` 的新格式是自 AEM 6.4 起定義服務使用者對應的建議方法。

以下列出變更格式的原因，以及為什麼 Adobe 建議您使用它，而不是使用僅針對單一使用者 ID 的版本對應：

* 可以透過將客戶的特殊需求與常見任務結合來重複使用服務使用者
* 避免重複設定權限
* 更了解給定服務實際執行的有效權限 (和任務)
* 不需要服務使用者的明確群組會籍。當群組權限變更時，這可能會產生麻煩的副作用
* 效能改進和擴充性

## 對應解析和服務登入 {#mapping-resolution-and-service-login}

### 服務對應解析 {#service-mapping-resolution}

解析服務對應的呼叫順序如下所述：

1. 搜尋給定 `bundleId` 和 `subserviceName` 的作用中 `principalNames` 對應
1. `bundleId` 和 null `subserviceName` 的 `principalNames` 對應
1. `bundleId` 和 `subserviceName` 的 `userName` 對應
1. `bundleId` 和 null `subserviceName` 的 `userName` 對應
1. 預設對應
1. 預設使用者

### SlingRepository - 服務登入 {#slingrepository-servicelogin}

取得服務 `Session/ResourceResolver` 的順序如下：

1. 從 `ServiceUserMapper` 取得主體名稱 => 預先驗證存放庫登入，如下所述
1. 從 `ServiceUserMapper` 擷取使用者 ID
1. 檢查目前使用者 ID 是否已棄用 `1ServiceUserConfiguration`
1. 透過使用者 ID 的預設 Sling Service 登入 (例如 `createAdministrativeSession` 順序並模擬服務使用者 ID)

與主體名稱的新對應產生以下簡化的存放庫登入：

* 主體名稱集被視為用於填入 `Subject` 的有效主體
* 因此可以預先驗證存放庫登入
* 無群組會籍解析

  >[!NOTE]
  >
  >所有需要宣告的服務使用者必要權限。「所有人」和其他群組權限將不再被繼承。

* 無需額外的管理員登入即可建立服務 -`Session/ResourceResolver`。

### 已棄用的 ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

請注意，在對應中指定單一使用者名稱相當於現有的 `ServiceUserConfiguration.simpleSubjectPopulation`。有了新格式，`ServiceUserConfiguration` 提供的解決方法可以使用服務使用者對應直接反映。因此，AEM 已棄用  `ServiceUserConfiguration`，並且所有現有用法均已被替換。

## 服務使用者 {#service-users}

### 重複使用現有服務使用者 {#reusing-existing-service-users}

若符合以下條件，建議重複使用現有服務使用者：

* 您的需求符合現有服務使用者的意圖
* 您的服務需要執行現有一般服務使用者負責的一般任務。在這種情況下，建議重複使用服務使用者，而不是引入重複
* 您的服務需要現有服務使用者所負責的特定任務。如果您對此不確定，請詢問擁有它的功能團隊。

若出現以下情況，請勿重複使用現有服務使用者：

* 您需要以不相關的方式修改其權限才能使其正常運作
* 如果您只需要它提供的權限的一小部分，並且您只需重複使用它，因為它使您的功能正常運作，而不是因為它真正相符
* 如果其名稱表明的意圖與您所需的完全不同。因為它有效而選擇它可能會導致問題，因為擁有特定服務的功能團隊可能會變更權限並破壞您的功能。

### 建立服務使用者 {#creating-a-service-user}

在確認 AEM 中沒有現有服務使用者適用於您的使用案例，並且相應的 RTC 問題已獲得核准後，您可以繼續將新使用者新增至預設內容。理想情況下，擴充的安全團隊的成員參與 RTC 投票，因此請確保適當的利害關係人也參與其中。

**命名慣例**

AEM 安全團隊為服務使用者定義了以下命名慣例，以增加新服務使用者的一致性並提高其可讀性和可維護性。

服務使用者名稱由 3 個元素組成，以破折號 **&#39;-&#39;** 分隔：

1. 服務作業所針對的邏輯實體/功能 (避免可能變更的路徑元素)
1. 服務要執行的任務
1. 尾端加上 **&#39;service&#39;** 以便能夠從 ID 和主體名稱輕鬆發現該使用者是服務使用者

**最佳實務**

* 不要混合不同的實體/功能。如果您的服務有不同的需求，則分割到各個服務使用者並將其彙總在對應中
* 將自己限制為每個服務使用者一個明確定義的任務。如果您最終授予太多或不相關的權限，則分割
* 花時間確定服務的真正需求
* 花時間尋找一個好的、有意義的、簡單易懂的服務使用者名稱
* 尋求回饋和檢閱：不熟悉您的功能的開發人員應該能夠閱讀並理解您的意圖。他們將來可能會承擔修復或維護它的任務。

最後，服務使用者名稱應顯示：

* 它的用法以及是否可以重複使用：

   * 非常一般：`content-writer-service`。如果您的服務還需要能夠讀取所有內容，則可以安全地在彙總中重複使用
   * 非常特定：`asset-linkshare-service`。除非您的服務確實也進行資產連結共享，否則重複使用就沒那麼安全。

* 功能集和權限設定預計會是什麼樣子：

   * 邏輯實體必須符合權限設定：

      * `content-foo-service` 應該只與內容作業相關聯。授予其對其他實體 (例如設定或使用者) 進行作業的權限是錯誤的
      * 特定的服務 (例如 `personalization-foo-service`) 也應該具有特定的權限。如果您最終授予所有內容的權限，則它不再是特定的。在名稱中反映這一點，或在彙總中重複使用一般使用者
      * 功能特定服務，例如 `msm-xyz-service` 應該只具有與 msm 相關的權限。不要將權限擴充到不相關的功能，例如管理社群設定或螢幕使用者。

   * 任務需要符合權限：

      * `foo-reader-service` 應該只能讀取一般項目。永不授予寫入權限
      * `foo-writer-service` 預計會執行寫入作業。但是，不應授予其讀取/修改存取控制內容的權限
      * `foo-replicator-service` 預計會授予 `crx:replicate`。

**範例**

`configuration-reader-service` 範例：

* 名稱表示它是一般設定，而不是特定功能的設定，例如 DM 整合的設定。專門用於讀取此類整合之設定的服務使用者則可命名為 `dmconfig-reader-service` 或 `s7config-reader-service`

  >[!NOTE]
  >
  >命名不包含路徑資訊。設定已從 `/etc` 移到 `/conf`。

* 任務元素表示綁定到該使用者的服務將僅執行讀取作業。

`userproperties-copy-service` 範例：

* 綁定到此服務使用者的服務將在使用者/群組屬性 (例如設定檔或偏好設定)上執行
* 它的專門用於僅複製該資訊，而非像是 `userproperties-writer-service` 的名稱，其中包括任何類型的寫入作業。因此，這些複製任務的權限設定可能僅允許在一個位置新增項目並在另一個位置刪除項目。

**權限設定最佳實務**

* 一律對服務使用者使用基於主體的存取控制設定。如需詳細資訊，請參閱下列範例：

   * 允許將服務使用者及其權限標記為 skyline 中的不可變應用程式內容
   * 無需建立路徑和樹狀結構

* 只授予權限，永不拒絕
* 限制權限

   * 僅授予所需的最低權限集
   * 如需詳細資訊，請參閱[將權限對應到項目](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html)和[將 API 呼叫對應到權限](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html)文件
   * 不授予 `jcr:all` 權限。這很可能不是最低權限集。

* 縮小範圍

   * 將存取控制原則放置在功能特定的子樹狀結構中
   * 如果是分散式項目：使用限制來限制範圍 (如需內建限制的清單，請參閱[文件](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html))。

* 確保一致性

   * 使權限與您在服務使用者名稱中使用的實體和任務一致
   * 避免新增不相關的權限。例如，擁有 `workflow-administration-service` 並授予其權限可在 `/home/users/screens` 執行使用者管理作業，或讓它讀取 s7-config，這樣很奇怪。

* 完整性

   * 確保您的服務擁有執行其負責之任務所需的所有權限。您的服務也需要在客戶環境中開箱即用。
   * 切勿期望/要求客戶擴充權限設定 (例如下面的 `/apps`)

* 避免重複設定權限

   * 重複使用一般服務使用者
   * 將它們與您的功能特定服務使用者彙總，這些使用者還提供您需要的特定權限

* 不要將權限設定分割到不同功能。這樣做的必要性表示您的服務使用者未明確定義或執行太多不同作業
* 不要將服務使用者分組，因為：

   * 它將服務使用者的實施細節與「公共」群組混合在一起
   * 您無法控制權限變更 (容易出現迴歸和權限升級)
   * 登入及評估效能
   * 不適用於基於主體的 ac-setup

* 存取使用者主節點 (或其中包含的任何子樹狀結構)，該節點沒有可預測的路徑，是透過使用 home (`userId`) 在 repo init 中實現的。如需詳細資訊，請參閱 sling repo init [文件](https://sling.apache.org/documentation/bundles/repository-initialization.html)。
* RTC：如果您變更現有服務使用者的權限，請建立專屬 RTC 問題，並確定交由安全團隊審核。

**透過存放庫初始化建立**

一律使用 `repo-init` 定義服務使用者及其權限設定，並將兩者放在快速入門功能模型的正確部分：

**最佳實務**

* 一律使用 `repo-init` 建立服務使用者
* 一律為服務使用者建立作業指定中間路徑
* AEM 所有內建服務使用者必須位於 `system/cq:services/internal` 下方
* 另外附加到中間相對路徑以依功能將服務使用者分組：`system/cq:services/internal/<your-feature>`
* 客戶定義的服務使用者必須位於 `system/cq:services/<customer-intermediate-rel-path>` 下方且絕對不能位於內部樹狀結構下方
* 如果使用者已存在並且需要移動到新位置 (其支援基於主體的授權)，則搭配使用&#x200B;**強制路徑**&#x200B;而非&#x200B;**路徑**。

**範例**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### 清理服務使用者和權限 {#cleanup-service-users-and-permissions}

以下 repo init 命令可用於清理未使用的服務使用者及其權限：

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### 測試服務使用者 {#testing-service-users}

為服務使用者及其權限設定編寫伺服器端測試，這一點很重要。這不僅可以驗證您的設定是否確實有效，還可以幫助您在變更存取控制內容或服務使用者時發現迴歸和非預期的錯誤。

`com.adobe.granite.testing.clients` 程式庫提供了許多公用程式，讓您可以輕鬆編寫服務使用者的 SST。
