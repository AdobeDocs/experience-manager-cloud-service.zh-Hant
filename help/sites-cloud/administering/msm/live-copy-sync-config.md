---
title: 設定 Live Copy 同步
description: 瞭解可用的強大Live Copy同步選項，以及如何根據專案需求進行設定和自訂。
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 2%

---


# 設定 Live Copy 同步 {#configuring-live-copy-synchronization}

Adobe Experience Manager提供數種立即可用的同步設定。 在使用即時副本之前，您應該考慮以下事項，以定義即時副本與其來源內容同步化的方式和時間。

1. 決定現有的轉出設定是否符合您的需求
1. 如果現有轉出設定無法達成，請決定是否需要建立您自己的轉出設定。
1. 指定用於即時副本的轉出設定。

## 已安裝及自訂轉出設定 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝轉出設定及其使用的同步化動作，以及如何在必要時建立自訂設定的資訊。

>[!CAUTION]
>
>更新或變更立即可用的轉出設定是&#x200B;**不建議**。 如果需要自訂即時動作，則應將其新增到自訂轉出設定中。

### 轉出觸發器 {#rollout-triggers}

每個轉出設定都會使用轉出觸發程式，導致轉出發生。 轉出設定可以使用以下其中一個觸發器：

* **轉出**：在Blue Print頁面上使用&#x200B;**轉出**&#x200B;命令，或在即時副本頁面上使用&#x200B;**同步**&#x200B;命令。
* **修改**：來源頁面已修改。
* **啟動時**：來源頁面已啟動。
* **停用**&#x200B;時：來源頁面已停用。

>[!NOTE]
>
>使用&#x200B;**修改**&#x200B;觸發程式可能會影響效能。 如需詳細資訊，請參閱[MSM最佳實務](best-practices.md#onmodify)。

### 推出設定 {#rollout-configurations}

下表列出隨AEM一起提供的現成轉出設定。 此表格包含每個轉出設定的觸發器和同步動作。

如果安裝的轉出組態動作不符合您的需求，您可以[建立轉出組態](#creating-a-rollout-configuration)。

| 名稱 | 說明 | 觸發程序 | [同步處理動作](#synchronization-actions) |
|---|---|---|---|
| 標準轉出設定 | 標準轉出設定，允許在轉出觸發時開始轉出程式，並執行下列動作：建立、更新、刪除內容以及排序子節點 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| 在 Blueprint 啟動時啟動 | 在發佈來源時發佈即時副本 | 啟動時 | `targetActivate` |
| 在 Blueprint 停用時停用 | 停用來源時停用即時副本 | 停用 | `targetDeactivate` |
| 在發生修改時推送 | 在修改來源時將內容推送至即時副本<br>請謹慎使用此轉出設定，因為它使用「修改」觸發程式。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| 在發生修改時推送 (淺層) | 修改Blueprint頁面時將內容推送至即時副本，而不更新參考（例如，淺層副本）<br>謹慎使用此轉出設定，因為它使用「修改」觸發器。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| 提升啟動 | 提升啟動頁面的標準轉出設定。 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### 同步化動作 {#synchronization-actions}

下表列出隨AEM一起提供的現成同步動作。

如果安裝的動作不符合您的需求，您可以[建立新的同步化動作](/help/implementing/developing/extending/msm.md#creating-a-new-synchronization-action)。

| 動作名稱 | 說明 | 屬性 |
|---|---|---|
| `contentCopy` | 當即時副本上不存在來源的節點時，此動作會將節點複製到即時副本。 [設定&#x200B;**CQ MSM內容複製動作**&#x200B;服務](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的節點型別、段落專案及頁面屬性。 |  |
| `contentDelete` | 此動作會刪除不在來源上的即時副本節點。 [設定&#x200B;**CQ MSM內容刪除動作**&#x200B;服務](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的節點型別、段落專案及頁面屬性。 |  |
| `contentUpdate` | 此動作會使用來源中的變更來更新即時副本內容。 [設定&#x200B;**CQ MSM內容更新動作**&#x200B;服務](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的節點型別、段落專案及頁面屬性。 |  |
| `editProperties` | 此動作會編輯即時副本的屬性。 `editMap`屬性決定要編輯哪些屬性及其值。 `editMap`屬性的值必須使用下列格式： <br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value`和`new_value`是規則運算式，`n`是遞增整數。<br>例如，請考慮下列`editMap`的值：<br>`sling:resourceType#/(contentpage`‖`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>此值編輯即時副本節點的屬性，如下所示：<br>設定為`contentpage`或`homepage`的`sling:resourceType`屬性設定為`mobilecontentpage`。<br>設定為`contentpage`的`cq:template`屬性設定為`mobilecontentpage`。 | `editMap: (String)`會識別屬性、目前值和新值。 如需詳細資訊，請參閱說明。 |
| `notify` | 此動作會傳送頁面已轉出的頁面事件。 若要接收通知，必須先訂閱轉出事件。 |  |
| `orderChildren` | 此動作會根據Blueprint上的順序來排序子節點。 |  |
| `referencesUpdate` | 此同步動作會更新即時副本上的參考。<br>它會搜尋即時副本頁面中指向Blueprint內資源的路徑。 找到後，它會更新路徑以指向即時副本內的相關資源。 具有Blueprint外部目標的參考不會變更。 <br>[設定&#x200B;**CQ MSM參考更新動作**&#x200B;服務](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的節點型別、段落專案和頁面屬性。 |  |
| `targetVersion` | 此動作會建立即時副本的版本。<br>此動作必須是轉出設定中包含的唯一同步化動作。 |  |
| `targetActivate` | 此動作會啟動即時副本。<br>此動作必須是轉出設定中包含的唯一同步化動作。 |  |
| `targetDeactivate` | 此動作會停用即時副本。<br>此動作必須是轉出設定中包含的唯一同步化動作。 |  |
| `workflow` | 此動作會啟動目標屬性定義的工作流程（僅適用於頁面），並將即時副本視為裝載。<br>目標路徑是模型節點的路徑。 | `target: (String)`是工作流程模型的路徑。 |
| `mandatory` | 此動作會將Live Copy頁面上多個ACL的許可權，設定為特定使用者群組的唯讀。 已設定下列ACL：<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁面使用此動作。 | `target: (String)`是您為其設定許可權的群組識別碼。 |
| `mandatoryContent` | 此動作會將Live Copy頁面上多個ACL的許可權，設定為特定使用者群組的唯讀。 已設定下列ACL：<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁面使用此動作。 | `target: (String)`是您為其設定許可權的群組識別碼。 |
| `mandatoryStructure` | 此動作將即時副本頁面上`ActionSet.ACTION_NAME_REMOVE` ACL的許可權設定為特定使用者群組的唯讀。<br>僅對頁面使用此動作。 | `target: (String)`是您為其設定許可權的群組識別碼。 |
| `VersionCopyAction` | 如果Blueprint/來源頁面已發佈至少一次，此動作會使用已發佈的版本建立即時副本頁面。 注意：此動作僅適用於根據已發佈的來源頁面建立即時副本頁面，不適用於更新現有的即時副本頁面。 |  |
| `PageMoveAction` | 當頁面在Blueprint中移動時會套用`PageMoveAction`。<br>動作會將（相關的）即時副本頁面從移動前的位置複製到移動後的位置，而不是移動頁面。<br>`PageMoveAction`未變更移動前所在位置的即時副本頁面。 因此，對於連續轉出設定，它具有不含Blueprint的即時關係狀態。<br>[設定&#x200B;**CQ MSM頁面移動動作**&#x200B;服務](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的節點型別、段落專案和頁面屬性。<br>此動作必須是轉出設定中包含的唯一同步化動作。 | 將`prop_referenceUpdate: (Boolean)`設定為true （預設）以更新參考。 |
| `markLiveRelationship` | 此動作表示啟動項建立的內容存在即時關係。 |  |

### 建立轉出設定 {#creating-a-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，您可以[建立轉出設定](/help/implementing/developing/extending/msm.md#creating-a-new-rollout-configuration)，方法是執行下列步驟。

1. [建立轉出設定 — &#x200B;](/help/implementing/developing/extending/msm.md#create-the-rollout-configuration)
1. [將同步處理動作新增至轉出設定](/help/implementing/developing/extending/msm.md#add-synchronization-actions-to-the-rollout-configuration)。

然後，當您在Blueprint或即時副本頁面上設定轉出設定時，便可使用新的轉出設定。

### 從同步化中排除屬性和節點型別 {#excluding-properties-and-node-types-from-synchronization}

您可以設定數個支援相應同步化動作的OSGi服務，使其不會影響特定節點型別和屬性。 例如，許多與AEM內部功能相關的屬性和子節點不應包含在即時副本中。 只應複製與頁面使用者相關的內容。

使用AEM時，有數種方法可管理此類服務的組態設定。 請參閱[設定OSGi](/help/implementing/deploying/configuring-osgi.md)，以取得詳細資訊和建議的作法。

下表列出您可以指定要排除的節點的同步化動作。 此表格提供要使用「Web主控台」設定的服務名稱，以及使用存放庫節點進行設定的PID。

| 同步化動作 | Web主控台中的服務名稱 | 服務PID |
|---|---|---|
| `contentCopy` | CQ MSM內容複製動作 | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM內容刪除動作 | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM內容更新動作 | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM頁面移動動作 | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM參考更新動作 | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

下表說明您可以設定的特性：

| Web主控台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 排除的節點型別 | `cq.wcm.msm.action.excludednodetypes` | 符合要從同步化動作中排除的節點型別的規則運算式 |
| 排除的段落專案 | `cq.wcm.msm.action.excludedparagraphitems` | 符合要從同步化動作中排除的段落專案的規則運算式 |
| 排除的頁面屬性 | `cq.wcm.msm.action.excludedprops` | 符合要從同步動作中排除之頁面屬性的規則運算式 |
| 忽略的Mixin節點型別 | `cq.wcm.msm.action.ignoredMixin` | 符合要從同步化動作中排除之mixin節點型別名稱的規則運算式（僅適用於`contentUpdate`動作） |

#### CQ MSM內容更新動作 — 排除專案 {#cq-msm-content-update-action-exclusions}

預設會排除數個屬性和節點型別，這些屬性和節點型別定義於&#x200B;**CQ MSM內容更新動作**&#x200B;的OSGi組態中，**排除的頁面屬性**&#x200B;下。

依預設，轉出時會排除符合下列規則運算式的屬性（也就是說，不會更新）：

![即時副本排除規則運算式](../assets/live-copy-exclude.png)

您可以視需要變更定義排除清單的運算式。

例如，如果您希望頁面&#x200B;**Title**&#x200B;包含在考慮轉出的變更中，請從排除中移除`jcr:title`。 例如，使用規則運算式：

`jcr:(?!(title)$).*`

### 配置同步以更新參照 {#configuring-synchronization-for-updating-references}

您可以設定數個OSGi服務，以支援與更新參考相關的對應同步化動作。

使用AEM時，有數種方法可管理此類服務的組態設定。 請參閱[設定OSGi](/help/implementing/deploying/configuring-osgi.md)，以取得詳細資訊和建議的作法。

下表列出您可以為其指定參照更新的同步化動作。 此表格提供要使用「Web主控台」設定的服務名稱，以及使用存放庫節點進行設定的PID。

| Web主控台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 更新巢狀即時副本間的參考 | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | 在Web主控台中選取此選項，或使用存放庫設定將此布林值屬性設為`true`，以取代以位於最上層即時副本分支內的任何資源為目標的參考。 僅適用於`referencesUpdate`動作。 |
| 更新引用頁面 | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | 在Web主控台中選取此選項，或使用存放庫設定將此布林值屬性設定為`true`，以更新任何參照來使用原始頁面來參照即時副本頁面。 僅適用於`PageMoveAction`。 |

## 指定要使用的轉出設定 {#specifying-the-rollout-configurations-to-use}

MSM可讓您指定一般使用的轉出設定集，並視需要覆寫特定即時副本的轉出設定。 MSM提供數個位置來指定要使用的轉出設定。 位置會決定是否將設定套用至特定的即時副本。

以下列出您可指定要使用的轉出設定的位置，說明MSM如何決定要用於Live Copy的轉出設定：

* **[即時副本頁面屬性](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page)：**&#x200B;當即時副本頁面設定為使用一個或多個轉出設定時，MSM會使用這些轉出設定。
* **[Blueprint頁面屬性](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page)：**&#x200B;當即時副本以Blueprint為基礎時，且即時副本頁面未設定轉出設定，則會使用與Blueprint來源頁面關聯的轉出設定。
* **即時副本父頁面屬性：**&#x200B;當即時副本頁面和Blueprint來源頁面均未設定轉出設定時，將會使用套用至即時副本頁面父頁面的轉出設定。
* **[系統預設值](live-copy-sync-config.md#setting-the-system-default-rollout-configuration)：**&#x200B;當無法判斷即時副本上層頁面的轉出設定時，將會使用系統預設轉出設定。

例如，Blueprint使用[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)網站作為來源內容。 從Blueprint建立網站。 下列清單中的每個專案都說明有關轉出設定的使用不同情境：

* 所有Blueprint頁面或即時副本頁面都未設定為使用轉出設定。 MSM會針對所有即時副本頁面使用系統預設轉出設定。
* WKND網站的根頁面已設定數個轉出設定。 MSM會對所有即時副本頁面使用這些轉出設定。
* WKND網站的根頁面設定了數個轉出設定，而即時副本網站的根頁面則設定了不同的轉出設定。 MSM會使用在即時副本網站的根頁面上設定的轉出設定。

### 設定即時副本頁面的轉出設定 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用要在來源頁面轉出時使用的轉出設定來設定即時副本頁面。 子頁面預設會繼承設定。 當您設定要使用的轉出設定時，將會覆寫即時副本頁面從其父項繼承的設定。

您也可以在您[建立即時副本時](creating-live-copies.md#creating-a-live-copy-of-a-page)為即時副本頁面設定轉出設定。

1. 使用&#x200B;**網站**&#x200B;主控台來選取即時副本頁面。
1. 從工具列選取&#x200B;**屬性**。
1. 開啟&#x200B;**即時副本**&#x200B;標籤。

   **設定**&#x200B;區段會顯示頁面繼承的轉出設定。

   ![來自父頁面的即時副本繼承](../assets/live-copy-inherit.png)

1. 如有必要，請調整&#x200B;**即時副本繼承**&#x200B;旗標。 如果勾選，即時副本設定將在所有子項上都有效。

1. 清除&#x200B;**從父項繼承轉出設定**&#x200B;屬性，然後從清單中選取一或多個轉出設定。

   選取的轉出設定會顯示在下拉式清單下方。

   ![正在覆寫即時副本設定繼承](../assets/live-copy-inherit-override.png)

1. 選取「**儲存並關閉**」。

### 設定Blueprint頁面的轉出設定 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用轉出設定來設定Blueprint頁面，以便在轉出Blueprint頁面時使用。

Blueprint頁面的子頁面會繼承設定。 當您設定要使用的轉出設定時，可能會覆寫頁面從其父項繼承的設定。

1. 使用&#x200B;**Sites**&#x200B;主控台來選取Blueprint的根頁面。
1. 從工具列選取&#x200B;**屬性**。
1. 開啟&#x200B;**Blueprint**&#x200B;標籤。
1. 使用下拉式選取器選取一或多個&#x200B;**轉出設定**。
1. 透過&#x200B;**儲存**&#x200B;保留您的更新。

### 設定系統預設轉出設定 {#setting-the-system-default-rollout-configuration}

若要指定轉出設定做為系統預設值，請設定下列OSGi服務。

* **Day CQ WCM Live Relationship Manager**，服務PID為`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用[網頁主控台](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[存放庫節點](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository)設定服務。

* 在Web主控台中，要設定的屬性名稱是&#x200B;**預設轉出設定**。
* 使用存放庫節點，要設定的屬性名稱是`liverelationshipmgr.relationsconfig.default`。

將此屬性值設為轉出設定的路徑，以作為系統預設值。 預設值為`/libs/msm/wcm/rolloutconfigs/default`，這是&#x200B;**標準轉出設定**。
