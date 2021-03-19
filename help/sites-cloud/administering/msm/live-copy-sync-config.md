---
title: 配置即時拷貝同步
description: 瞭解可用的強大即時副本同步選項，以及如何根據專案需求來設定和自訂這些選項。
feature: 多站點管理員
role: 管理員
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 2%

---


# 配置即時拷貝同步{#configuring-live-copy-synchronization}

Adobe Experience Manager提供了一些現成可用的同步配置。 在使用即時副本之前，您應考慮以下事項來定義即時副本與其來源內容同步的方式和時間。

1. 決定現有的轉出設定是否符合您的需求
1. 如果現有的轉出設定沒有，請決定您是否需要自行建立。
1. 指定要用於即時副本的轉出設定。

## 安裝和自訂轉出組態{#installed-and-custom-rollout-configurations}

本節提供有關已安裝的轉出配置及其使用的同步操作的資訊，以及如何根據需要建立自定義配置。

>[!CAUTION]
>
>建議更新或變更現成可用的轉出設定為&#x200B;**not**。 如果需要自訂即時動作，則應將它新增至自訂轉出設定。

### 轉出觸發器{#rollout-triggers}

每個轉出設定都使用轉出觸發器，導致轉出發生。 轉出設定可使用下列其中一個觸發器：

* **推出時**:Rollout **** 命令用於藍色打印頁，或者Synchronization命 **** 令用於即時副本頁。
* **修改時**:源頁面已修改。
* **啟動時**:源頁面被激活。
* **停用時**:來源頁面已停用。

>[!NOTE]
>
>使用&#x200B;**On Modification**&#x200B;觸發器可影響效能。 如需詳細資訊，請參閱[MSM最佳實務](best-practices.md#onmodify)。

### 轉出設定 {#rollout-configurations}

下表列出隨附提供的轉出設定AEM。 該表包括每個轉出配置的觸發器和同步操作。 如果安裝的轉出配置操作不符合您的要求，您可以[建立新的轉出配置](#creating-a-rollout-configuration)。

| 名稱 | 說明 | 觸發器 | [同步操作](#synchronization-actions) |
|---|---|---|---|
| 標準轉出設定 | 標準轉出設定，允許在轉出觸發器時開始轉出程式，並執行動作：建立、更新、刪除內容及訂購子節點 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| 在 Blueprint 啟動時啟動 | 發佈來源時發佈即時副本 | 啟動時 | `targetActivate` |
| 在 Blueprint 停用時停用 | 停用來源時停用即時副本 | 停用時 | `targetDeactivate` |
| 在發生修改時推送 | 在修改來源時將內容推送至即時副本<br>當使用「修改時」觸發器時，請謹慎使用此轉出設定。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| 在發生修改時推送 (淺層) | 修改藍圖頁面時將內容推送至即時副本，而不更新參考（例如淺層副本）<br>使用「修改時」觸發器時，請謹慎使用此轉出設定。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| 提升啟動 | 提升啟動頁面的標準轉出設定。 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### 同步操作{#synchronization-actions}

下表列出了隨附的現成同步操作AEM。

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| 動作名稱 | 說明 | 屬性 |
|---|---|---|
| `contentCopy` | 當源節點在即時副本上不存在時，此操作會將節點複製到即時副本。 [設定 **CQ MSM Content Copy** ](#excluding-properties-and-node-types-from-synchronization) Actionservice以指定要排除的節點類型、段落項目和頁面屬性。 |  |
| `contentDelete` | 此操作將刪除源上不存在的即時副本節點。 [設定 **CQ MSM內容刪除動作** ](#excluding-properties-and-node-types-from-synchronization) 服務，以指定要排除的節點類型、段落項目和頁面屬性。 |  |
| `contentUpdate` | 此動作會使用來源的變更來更新即時副本內容。 [設定 **CQ MSM內容更新** ](#excluding-properties-and-node-types-from-synchronization) Actionservice，以指定要排除的節點類型、段落項目和頁面屬性。 |  |
| `editProperties` | 此動作會編輯即時副本的屬性。 `editMap`屬性決定要編輯的屬性及其值。 `editMap`屬性的值必須使用下列格式：<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value`和`new_value`是規則運算式，而`n`是遞增的整數。<br>例如，請考慮以下值 `editMap`:<br>`sling:resourceType#/(contentpage`´`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>This value edits the properties of the Live Copy nodes as follows:<br> `sling:resourceType` the properties whiter set to  `contentpage` or  `homepage`  `mobilecontentpage`set to Jozze.<br>設 `cq:template` 置為的屬 `contentpage` 性設定為 `mobilecontentpage`。 | `editMap: (String)` 標識屬性、當前值和新值。如需詳細資訊，請參閱說明。 |
| `notify` | 此動作會傳送頁面事件，指出該頁面已經推出。 為了獲得通知，您必須先訂閱以推出事件。 |  |
| `orderChildren` | 此動作會根據Blueprint上的順序對子節點排序。 |  |
| `referencesUpdate` | 此同步動作會更新即時副本上的參考。<br>它會在「即時副本」頁面中搜尋指向藍圖中資源的路徑。當找到時，會更新路徑以指向即時副本中的相關資源。 在藍圖以外具有目標的參照不會變更。 <br>[設定 **CQ MSM參考更新** ](#excluding-properties-and-node-types-from-synchronization) Actionservice，以指定要排除的節點類型、段落項目和頁面屬性。 |  |
| `targetVersion` | 此動作會建立即時副本的版本。<br>此動作必須是轉出設定中包含的唯一同步動作。 |  |
| `targetActivate` | 此動作會啟動即時副本。<br>此動作必須是轉出設定中包含的唯一同步動作。 |  |
| `targetDeactivate` | 此動作會停用即時副本。<br>此動作必須是轉出設定中包含的唯一同步動作。 |  |
| `workflow` | 此動作會啟動目標屬性所定義的工作流程（僅限頁面），並將即時副本視為裝載。<br>目標路徑是模型節點的路徑。 | `target: (String)` 是工作流模型的路徑。 |
| `mandatory` | 此操作將「即時副本」頁上多個ACL的權限設定為特定用戶組的只讀。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁使用此操作。 | `target: (String)` 是您要設定權限之群組的ID。 |
| `mandatoryContent` | 此操作將「即時副本」頁上多個ACL的權限設定為特定用戶組的只讀。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁使用此操作。 | `target: (String)` 是您要設定權限之群組的ID。 |
| `mandatoryStructure` | 此操作將「即時複製」頁上的`ActionSet.ACTION_NAME_REMOVE` ACL的權限設定為特定用戶組的只讀。<br>此動作僅適用於頁面。 | `target: (String)` 是您要設定權限之群組的ID。 |
| `VersionCopyAction` | 如果藍圖／來源頁面至少已發佈一次，此動作會使用已發佈的版本建立即時副本頁面。 注意：此動作僅適用於根據已發佈的來源頁面建立即時副本頁面，而不適用於更新現有的即時副本頁面。 |  |
| `PageMoveAction` | `PageMoveAction`會在藍圖中移動頁面時套用。<br>動作會複製（相關）「即時副本」頁面，而非將「即時副本」頁面從移動前的位置移至之後的位置。<br>移 `PageMoveAction` 動前不會變更「即時副本」頁面。因此，對於連續的轉出設定，它的狀態為即時關係，而無藍圖。<br>[設定 **CQ MSM Page Move** ](#excluding-properties-and-node-types-from-synchronization) Actionservice以指定要排除的節點類型、段落項目和頁面屬性。<br>此動作必須是轉出設定中包含的唯一同步動作。 | 將`prop_referenceUpdate: (Boolean)`設為true（預設值）以更新參考。 |
| `markLiveRelationship` | 此動作表示啟動建立的內容存在即時關係。 |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### 從同步{#excluding-properties-and-node-types-from-synchronization}中排除屬性和節點類型

您可以配置支援相應同步操作的多個OSGi服務，以便它們不影響特定節點類型和屬性。 例如，與內部功能相關的許多屬性和子節點AEM不應包含在即時副本中。 僅複製與頁面使用者相關的內容。

使用時，有AEM幾種方法可管理此類服務的配置設定。 如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/implementing/deploying/configuring-osgi.md)。

下表列出了可以指定要排除的節點的同步操作。 該表提供了使用Web控制台配置的服務名和使用儲存庫節點配置的PID。

| 同步操作 | Web控制台中的服務名 | 服務PID |
|---|---|---|
| `contentCopy` | CQ MSM內容複製動作 | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM內容刪除動作 | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM內容更新動作 | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM Page Move Action | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM參考更新動作 | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

下表說明了您可以配置的屬性：

| Web控制台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 排除的節點類型 | `cq.wcm.msm.action.excludednodetypes` | 與要從同步操作中排除的節點類型相匹配的規則運算式 |
| 排除的段落項目 | `cq.wcm.msm.action.excludedparagraphitems` | 與要從同步操作中排除的段落項匹配的規則運算式 |
| 排除的頁面屬性 | `cq.wcm.msm.action.excludedprops` | 與要從同步操作中排除的頁面屬性相匹配的規則運算式 |
| 忽略Mixin NodeTypes | `cq.wcm.msm.action.ignoredMixin` | 與要從同步操作中排除的mixin節點類型名稱相匹配的規則運算式（僅適用於`contentUpdate`操作） |

#### CQ MSM內容更新動作——排除{#cq-msm-content-update-action-exclusions}

預設情況下，會排除一些屬性和節點類型，這些在&#x200B;**CQ MSM內容更新操作**&#x200B;的OSGi配置中定義，位於&#x200B;**排除的頁面屬性**&#x200B;下。

依預設，在轉出時會排除與下列規則運算式相符的屬性（亦即未更新）:

![即時副本排除規則](../assets/live-copy-exclude.png)

您可以視需要變更定義排除清單的運算式。

例如，如果您希望將頁面&#x200B;**Title**&#x200B;納入考慮轉出的變更中，請從排除項中移除`jcr:title`。 例如，使用regex:

`jcr:(?!(title)$).*`

### 配置同步以更新引用{#configuring-synchronization-for-updating-references}

您可以配置幾個支援與更新引用相關的相應同步操作的OSGi服務。

使用時，有AEM幾種方法可管理此類服務的配置設定。 如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/implementing/deploying/configuring-osgi.md)。

下表列出了可以為其指定引用更新的同步操作。 該表提供了使用Web控制台配置的服務名和使用儲存庫節點配置的PID。

| Web控制台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 跨巢狀LiveCopys更新參考 | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | 在Web控制台中選擇此選項，或使用儲存庫配置將此布爾屬性設定為`true` ，以替換指向位於最頂層即時副本分支中的任何資源的引用。 僅適用於`referencesUpdate`操作。 |
| 更新參考頁面 | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | 在Web控制台中選擇此選項，或使用儲存庫配置將此布爾屬性設定為`true`以更新任何引用，以使用原始頁來改為引用「即時複製」頁。 僅適用於`PageMoveAction`。 |

## 指定要使用{#specifying-the-rollout-configurations-to-use}的轉出配置

MSM可讓您指定一般使用的轉出組態集，並可視需要覆寫特定即時副本的組態。 MSM提供了幾個位置，用於指定要使用的轉出配置。 位置會決定設定是否套用至特定即時副本。

以下位置清單可指定使用的轉出組態，說明MSM如何決定用於即時副本的轉出組態：

* **[即時副本頁面屬性](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page)：當「即** 時副本」頁面設定為使用一或多個轉出設定時，MSM會使用這些轉出設定。
* **[Blueprint頁面屬性](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page)** ：當即時副本以藍圖為基礎，而「即時副本」頁面未設定轉出設定時，會使用與藍圖來源頁面相關聯的轉出設定。
* **即時副本父頁面屬性：** 當「即時副本」頁面和Blueprint來源頁面都未以轉出設定進行設定時，會使用套用至即時副本頁面父頁面的轉出設定。
* **[系統預設](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** 當無法判斷即時副本父頁面的轉出設定時，會使用系統預設的轉出設定。

例如，Blueprint使用[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)網站做為來源內容。 從Blueprint建立網站。 下列清單中的每個項目說明使用轉出組態的不同情形：

* 未將任何藍圖頁面或即時副本頁面設定為使用轉出設定。 MSM對所有即時副本頁面使用系統預設的轉出設定。
* WKND網站的根頁面已設定數個轉出設定。 MSM將這些展開設定用於所有即時副本頁面。
* WKND網站的根頁面已設定數個轉出設定，而即時副本網站的根頁面則設定了不同的轉出設定集。 MSM使用在即時副本網站的根頁面上設定的轉出設定。

### 設定即時副本頁面的轉出設定{#setting-the-rollout-configurations-for-a-live-copy-page}

使用轉出設定來設定「即時副本」頁面，以便在轉出來源頁面時使用。 預設情況下，子頁繼承配置。 當您設定轉出設定使用時，您會覆寫即時副本頁面繼承自其父項的設定。

您也可以在[建立即時副本](creating-live-copies.md#creating-a-live-copy-of-a-page)時，為即時副本頁面設定轉出設定。

1. 使用&#x200B;**Sites**&#x200B;控制台選擇「即時副本」頁面。
1. 從工具欄中選擇&#x200B;**屬性**。
1. 開啟&#x200B;**即時副本**&#x200B;標籤。

   **Configuration**&#x200B;區段顯示頁面繼承的轉出配置。

   ![從父頁面即時複製繼承](../assets/live-copy-inherit.png)

1. 如果需要，請調整&#x200B;**即時副本繼承**&#x200B;標幟。 如果勾選「即時副本」設定，則所有子系都會生效。

1. 清除&#x200B;**從父級繼承轉出配置**&#x200B;屬性，然後從清單中選擇一個或多個轉出配置。

   選取的轉出設定會顯示在下拉式清單下方。

   ![覆寫即時副本組態繼承](../assets/live-copy-inherit-override.png)

1. 按一下或點選&#x200B;**保存並關閉**。

### 設定Blueprint頁面{#setting-the-rollout-configuration-for-a-blueprint-page}的轉出設定

使用轉出設定設定來設定藍圖頁面，以便在展開藍圖頁面時使用。

請注意，Blueprint頁面的子頁面繼承配置。 當您設定使用轉出設定時，您可能會覆寫頁面繼承自其父項的設定。

1. 使用&#x200B;**Sites**&#x200B;控制台來選擇Blueprint的根頁面。
1. 從工具欄中選擇&#x200B;**屬性**。
1. 開啟&#x200B;**Blueprint**&#x200B;標籤。
1. 使用下拉式選擇器，選取一或多個&#x200B;**轉出組態**。
1. 使用&#x200B;**Save**&#x200B;保存更新。

### 設定系統預設轉出配置{#setting-the-system-default-rollout-configuration}

若要指定轉出組態以用作系統預設值，請設定下列OSGi服務。

* **Day CQ WCM Live Relationship** Manager與服務PID  `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用[Web控制台](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[儲存庫節點](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository)配置服務。

* 在Web控制台中，要配置的屬性的名稱為&#x200B;**預設轉出配置**。
* 使用儲存庫節點時，要配置的屬性的名稱為`liverelationshipmgr.relationsconfig.default`。

將此屬性值設定為轉出配置的路徑，以用作系統預設值。 預設值為`/libs/msm/wcm/rolloutconfigs/default`，即&#x200B;**標準轉出設定**。
