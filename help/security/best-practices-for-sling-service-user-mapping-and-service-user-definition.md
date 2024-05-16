---
title: Sling服務使用者對應和服務使用者定義的最佳實務
description: 瞭解Sling服務使用者對應和服務使用者定義的最佳實務
source-git-commit: b6f7b6996b377ecfa372742ce1ad22139547ebdd
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---


# Sling服務使用者對應和服務使用者定義的最佳實務 {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## 服務使用者對應 {#service-user-mapping}

若要將服務對應新增至對應的系統使用者，您需要為建立工廠組態 `ServiceUserMapper` 服務。 若要保持此模組化，可使用Sling「修改」機制提供此類設定(請參閱 [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) 以取得詳細資訊)。 建議使用您的套件安裝此類設定的方式是將其新增至Quickstart布建模型，如下列範例所述：

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### 對應格式 {#mapping-format}

自AEM 6.4起，對應格式的定義如下：

>[!NOTE]
>
>此 `userName` 已棄用，不應再使用。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` 和 `subserviceName` 識別服務， `userName/principalNames` 識別服務使用者並 `principalNames` 是以逗號分隔的清單。

另外請注意 `principalNames` 是與id相同的服務使用者主要名稱清單。


**最佳實務**

* 不同工作的子服務名稱 — 如果您的套裝服務執行不同的工作，建議識別 `subserviceNames` 依任務將他們分組
* 如果指定的服務執行不同的操作(例如，讀取資產內容並更新子樹狀結構下的資訊 `/var`)，建議彙總反映個別作業的不同服務主體(例如彙總通用 `dam-reader-service` 具有您專屬的功能 `assetreport-writer-service`
* 每個服務在理想情況下都會與非常特定且有限的作業集合繫結
* 的新格式與 `[one,or,multiple,principalNames]` 是定義自AEM 6.4起服務使用者對應的建議方式。

以下是變更格式的原因清單，以及Adobe建議您將其用於單一使用者ID，而非僅用於版本對應的原因：

* 結合客戶的特殊需求與一般工作，以重複使用服務使用者的能力
* 避免許可權設定的重複
* 更清楚瞭解指定服務實際執行的有效許可權（和工作）
* 不需要明確服務使用者的群組成員資格。 當群組許可權變更時，這可能會產生令人困擾的副作用
* 效能改善與擴充能力

## 對應解析和服務登入 {#mapping-resolution-and-service-login}

### 服務對應解析 {#service-mapping-resolution}

解決服務對應的呼叫順序，如下所述：

1. 搜尋作用中 `principalNames` 指定的對應 `bundleId` 和 `subserviceName`
1. `principalNames` 對應 `bundleId` 和null `subserviceName`
1. `userName` 對應 `bundleId` 和 `subserviceName`
1. `userName` 對應 `bundleId` 和null `subserviceName`
1. 預設對應
1. 預設使用者

### SlingRepository — 服務登入 {#slingrepository-servicelogin}

取得服務的順序 `Session/ResourceResolver` 其運作方式如下：

1. 從取得主體名稱 `ServiceUserMapper` =>預先驗證存放庫登入，如下所述
1. 從擷取使用者ID `ServiceUserMapper`
1. 檢查目前使用者ID中是否有過時的1ServiceUserConfiguration&#39;
1. 使用使用者ID登入的預設Sling服務(例如 `createAdministrativeSession` 並模擬服務使用者id)

具有主體名稱的新對應會產生以下簡化的存放庫登入：

* 主體名稱集被視為要用來填入 `Subject`
* 因此，存放庫登入可以預先驗證
* 無群組成員資格解析

  >[!NOTE]
  >
  >需要為服務使用者宣告所有必要的許可權。 &#39;everyone&#39;和其他群組許可權將不再繼承。

* 沒有額外的管理員登入可擁有此服務 — `Session/ResourceResolver` 都會建立。

### 已棄用的ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

請注意，在對應中指定單一使用者名稱等同於現有 `ServiceUserConfiguration.simpleSubjectPopulation`. 使用新格式時，由提供的因應措施 `ServiceUserConfiguration` 可直接反映為服務使用者對應。 此 `ServiceUserConfiguration` 因此，AEM已淘汰，所有現有用途已取代。

## 服務使用者 {#service-users}

### 重複使用現有的服務使用者 {#reusing-existing-service-users}

如果符合下列條件，建議重複使用現有的服務使用者：

* 您的需求符合現有服務使用者的目的
* 您的服務需要執行現有的一般服務使用者所涵蓋的一般工作。 在此情況下，建議重複使用服務使用者，而非引入重複
* 您的服務需要由現有服務使用者涵蓋的特定工作。 如果您對此有疑問，請洽詢擁有該計畫的功能團隊。

如果發生下列情況，請勿重複使用現有的服務使用者：

* 您需要以不相關的方式修改其許可權，才能使其運作
* 如果您只需要它提供的一小部分許可權，而您只需要重複使用它，因為它可讓您的功能運作，而不是因為它真的相符
* 如果它的名稱表示您需要的完全不同的意圖。 如果因為有效而選擇它，可能會導致以後發生問題，因為擁有特定服務的功能團隊可能會變更許可權並破壞您的功能。

### 建立服務使用者 {#creating-a-service-user}

在您驗證AEM中沒有任何現有的服務使用者適用於您的使用案例，且對應的RTC問題已核准後，您可以繼續並將新使用者新增至預設內容。 理想情況下，擴充的安全性團隊成員應該參與RTC投票，因此請確定您也涉及適當的利害關係人。

**命名慣例**

AEM安全性團隊為服務使用者定義了以下命名慣例，以便為新服務使用者增加一致性並改善其可讀性和可維護性。

服務使用者名稱包含3個以破折號分隔的元素 **&#39;-&#39;**：

1. 服務作業所定位的邏輯實體/功能（避免可能會變更的路徑元素）
1. 服務將執行的任務
1. Trailing **&#39;服務&#39;** 能夠輕易地從使用者身為服務使用者的id和主體名稱中辨識出來

**最佳實務**

* 請勿混合不同的圖元/特徵。 如果您的服務有不同的需求，請分割給個別服務使用者，並在對應中彙總他們
* 將您自己限製為每個服務使用者一個已妥善定義的任務。 如果您最終授予太多或不相關的許可權，請分割
* 請花時間找出您服務的實際需求
* 請花時間尋找良好、有意義且易於解釋的服務使用者名稱
* 要求意見反應和評論：不熟悉您的功能的開發人員應該能夠閱讀並瞭解您的意圖。 他們將來可能會接受修正或維護的任務。

最後，服務使用者名稱應該會顯示：

* 其使用方式以及可重複使用方式：

   * 非常一般： `content-writer-service`. 如果您的服務也需要能夠讀取所有內容，可在彙總中安全地重複使用
   * 非常明確： `asset-linkshare-service`. 重複使用並不安全，除非您的服務確實也連結分享資產。

* 功能集和許可權設定的預期外觀：

   * 邏輯實體必須符合許可權設定：

      * A `content-foo-service` 應該只與內容上的操作相關聯。 授與它在其他實體（例如設定或使用者）上操作的許可權是錯誤的
      * 特定服務，例如 `personalization-foo-service` 應該也會隨附特定許可權。 如果您最終獲得所有內容的許可權，就不再侷限於此了。 反映在名稱中或在彙總中重複使用一般使用者
      * 功能特定服務，例如 `msm-xyz-service` 應該只有msm相關的許可權。 請勿將許可權擴充至不相關的功能，例如管理社群設定或畫面使用者。

   * 任務必須符合許可權：

      * A `foo-reader-service` 應該只能讀取一般專案。 永不授予寫入許可權
      * A `foo-writer-service` 可以預期執行寫入作業。 但是，不應授予其讀取/修改存取控制內容的許可權
      * A `foo-replicator-service` 可以預期具有 `crx:replicate` 已授予。

**範例**

範例 `configuration-reader-service`：

* 該名稱表示它是指一般設定，而不是特定功能的設定，如DM整合的設定。 若是讀取這類整合設定的特定目標服務使用者，應命名為 `dmconfig-reader-service` 或 `s7config-reader-service`

  >[!NOTE]
  >
  >命名中未包含任何路徑資訊。 設定已從「 」移出「 」 `/etc` 至 `/conf`.

* task-element表示繫結至該使用者的服務只會執行讀取作業。

範例 `userproperties-copy-service`：

* 與此服務使用者繫結的服務將會對使用者/群組屬性（例如設定檔或偏好設定）進行操作
* 其目標鎖定為僅複製該資訊，而非像這樣的名稱 `userproperties-writer-service` 包括任何種類的寫入作業。 因此，這些複製工作的許可權設定可能僅允許在一個位置新增專案和在另一個位置移除專案。

**許可權設定的最佳實務**

* 一律對服務使用者使用以主體為基礎的存取控制設定。 如需詳細資訊，請參閱下列範例：

   * 允許在Skyline中將服務使用者及其許可權標籤為不可變的應用程式內容
   * 不需要建立路徑和樹狀結構

* 僅授予許可權，不拒絕
* 限制許可權

   * 僅授予所需的最小許可權集
   * 如需詳細資訊，請參閱 [將許可權對應至專案](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) 和 [將API呼叫對應至許可權](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) 檔案
   * 不授與許可權 `jcr:all`. 這很可能不是最小集合。

* 縮小範圍

   * 將存取控制原則放置在功能特定的子樹狀結構中
   * 分散式專案的情況下：使用限制來限制範圍(請參閱 [說明檔案](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) 以取得內建限制的清單)。

* 確保一致性

   * 使許可權與您在服務使用者名稱中使用的實體和任務一致
   * 避免新增不相關的許可權。 例如，如果有 `workflow-administration-service` 並授予it執行使用者管理操作的許可權： `/home/users/screens` 或讓其讀取s7-config。

* 完整性

   * 請確定您的服務擁有執行設計任務所需的所有許可權。 您的服務也需要在客戶環境中立即運作。
   * 切勿期望/要求客戶擴大許可權設定(例如，以下的 `/apps`)

* 避免許可權設定的重複

   * 重複使用一般服務使用者
   * 將它們與提供您另外需要的特定許可權的特定功能服務使用者彙總

* 請勿將許可權設定分割到不同的功能。 執行此動作的需求表示您的服務使用者未正確定義，或做了太多不同的事情
* 請勿將服務使用者放在群組中，因為：

   * 它會混合來自服務使用者與「公用」群組的實作詳細資料
   * 您缺乏許可權變更的控制權（容易回歸及許可權提升）
   * 登入與評估效能
   * 無法搭配以主體為基礎的AC設定使用

* 在repo init中，使用home(`userId`)。 檢視sling repo init [檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html) 以取得詳細資訊。
* RTC：如果您變更現有服務使用者的許可權，請建立專用的RTC問題，並確保由安全性團隊檢閱。

**使用存放庫初始化來建立**

永遠使用 `repo-init` 若要定義服務使用者及其許可權設定，並將兩者置於Quickstart功能模型的正確區段：

**最佳實務**

* 永遠使用 `repo-init` 建立服務使用者
* 一律指定服務使用者建立的中間路徑
* AEM的所有內建服務使用者必須位於下方 `system/cq:services/internal`
* 此外，附加至中介相對路徑，依功能將服務使用者分組： `system/cq:services/internal/<your-feature>`
* 客戶定義的服務使用者必須位於下方 `system/cq:services/<customer-intermediate-rel-path>` 而且絕不低於內部樹狀結構
* 使用 **使用強制路徑** 而非 **含路徑** 如果使用者已經存在，並且需要移動到支援主體式授權的新位置。

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

### 清理服務使用者和許可權 {#cleanup-service-users-and-permissions}

以下repo init命令可用於清除未使用的服務使用者及其許可權：

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

為服務使用者及其許可權設定編寫伺服器端測試很重要。 這不僅可驗證您的設定是否真的有效，也可協助您在變更存取控制內容或服務使用者時，找出回歸和意外的錯誤。

此 `com.adobe.granite.testing.clients` 程式庫提供許多公用程式，可讓服務使用者輕鬆撰寫SST。





