---
title: 配置即時拷貝同步
description: 瞭解可用的功能強大的Live Copy同步選項以及如何根據項目需要配置和自定義這些同步選項。
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2336'
ht-degree: 1%

---

# 配置即時拷貝同步 {#configuring-live-copy-synchronization}

Adobe Experience Manager提供了許多開箱即用的同步配置。 在使用即時拷貝之前，您應考慮以下內容來定義即時拷貝與其源內容的同步方式和同步時間。

1. 確定現有部署配置是否滿足您的要求
1. 如果現有的推廣配置不能，請決定是否需要建立自己的。
1. 指定要用於即時副本的推廣配置。

## 已安裝和自定義部署配置 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝的部署配置及其使用的同步操作的資訊，以及如何根據需要建立自定義配置。

>[!CAUTION]
>
>更新或更改現成部署配置 **不** 推薦。 如果需要自定義即時操作，則應在自定義部署配置中添加該操作。

### 推廣觸發器 {#rollout-triggers}

每個推廣配置都使用一種引發推廣的觸發器。 推廣配置可以使用以下觸發器之一：

* **推出時**:的 **推廣** 命令用於藍色打印頁面，或 **同步** 命令用於「即時複製」頁。
* **論修改**:源頁面已修改。
* **激活時**:源頁面已激活。
* **停用時**:源頁面已停用。

>[!NOTE]
>
>使用 **論修改** 觸發器會影響效能。 請參閱 [MSM最佳做法](best-practices.md#onmodify) 的子菜單。

### 轉出設定 {#rollout-configurations}

下表列出了隨附提供的預置配置AEM。 該表包括每個轉出配置的觸發器和同步操作。

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| 名稱 | 說明 | 觸發器 | [同步操作](#synchronization-actions) |
|---|---|---|---|
| 標準轉出設定 | 標準的展示配置，允許在展示觸發器上啟動展示過程並運行操作：建立、更新、刪除內容和訂購子節點 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| 在 Blueprint 啟動時啟動 | 發佈源時發佈即時拷貝 | 啟動時 | `targetActivate` |
| 在 Blueprint 停用時停用 | 禁用源時停用Live Copy | 停用時 | `targetDeactivate` |
| 在發生修改時推送 | 修改源時將內容推送到即時拷貝<br>在使用「修改時」觸發器時，請節省使用此部署配置。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| 在發生修改時推送 (淺層) | 在修改藍圖頁面時將內容推送到即時拷貝，而不更新引用（如淺拷貝）<br>在使用「修改時」觸發器時，請節省使用此部署配置。 | 於修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| 提升啟動 | 提升啟動頁面的標準轉出設定。 | 於轉出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### 同步操作 {#synchronization-actions}

下表列出了隨附提供的現成同步操作AEM。

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| 操作名稱 | 說明 | 屬性 |
|---|---|---|
| `contentCopy` | 如果源節點在即時拷貝上不存在，此操作會將節點複製到即時拷貝。 [配置 **CQ MSM內容複製操作** 服務](#excluding-properties-and-node-types-from-synchronization) 指定要排除的節點類型、段落項和頁面屬性。 |  |
| `contentDelete` | 此操作將刪除源上不存在的即時副本節點。 [配置 **CQ MSM內容刪除操作** 服務](#excluding-properties-and-node-types-from-synchronization) 指定要排除的節點類型、段落項和頁面屬性。 |  |
| `contentUpdate` | 此操作將使用來自源的更改更新Live Copy內容。 [配置 **CQ MSM內容更新操作** 服務](#excluding-properties-and-node-types-from-synchronization) 指定要排除的節點類型、段落項和頁面屬性。 |  |
| `editProperties` | 此操作編輯Live Copy的屬性。 的 `editMap` 屬性確定要編輯的屬性及其值。 的值 `editMap` 屬性必須使用以下格式：<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` 和 `new_value` 是規則運算式 `n` 是遞增的整數。<br>例如，請考慮以下值 `editMap`:<br>`sling:resourceType#/(contentpage`圖`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>此值編輯Live Copy節點的屬性，如下所示：<br>的 `sling:resourceType` 屬性設定為 `contentpage` 或 `homepage` 設定為 `mobilecontentpage`。<br>的 `cq:template` 設定為的屬性 `contentpage` 設定為 `mobilecontentpage`。 | `editMap: (String)` 標識屬性、當前值和新值。 有關詳細資訊，請參閱說明。 |
| `notify` | 此操作將發送已滾出頁面的頁面事件。 要得到通知，首先需要訂閱推廣活動。 |  |
| `orderChildren` | 此操作根據藍圖上的順序對子節點排序。 |  |
| `referencesUpdate` | 此同步操作將更新Live Copy上的引用。<br>它在「即時複製」頁中搜索指向藍圖中資源的路徑。 找到後，它會更新路徑以指向即時拷貝中的相關資源。 在藍圖之外具有目標的參照不會更改。 <br>[配置 **CQ MSM引用更新操作** 服務](#excluding-properties-and-node-types-from-synchronization) 指定要排除的節點類型、段落項和頁面屬性。 |  |
| `targetVersion` | 此操作將建立Live Copy的版本。<br>此操作必須是部署配置中包含的唯一同步操作。 |  |
| `targetActivate` | 此操作將激活即時拷貝。<br>此操作必須是部署配置中包含的唯一同步操作。 |  |
| `targetDeactivate` | 此操作將停用即時拷貝。<br>此操作必須是部署配置中包含的唯一同步操作。 |  |
| `workflow` | 此操作將啟動由目標屬性定義的工作流（僅適用於頁面），並將Live Copy作為負載。<br>目標路徑是模型節點的路徑。 | `target: (String)` 是工作流模型的路徑。 |
| `mandatory` | 此操作將「即時複製」頁上的幾個ACL的權限設定為特定用戶組的只讀。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁面使用此操作。 | `target: (String)` 是要為其設定權限的組的ID。 |
| `mandatoryContent` | 此操作將「即時複製」頁上的幾個ACL的權限設定為特定用戶組的只讀。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>僅對頁面使用此操作。 | `target: (String)` 是要為其設定權限的組的ID。 |
| `mandatoryStructure` | 此操作設定 `ActionSet.ACTION_NAME_REMOVE` Live Copy頁上的ACL，用於特定用戶組的只讀。<br>僅對頁面使用此操作。 | `target: (String)` 是要為其設定權限的組的ID。 |
| `VersionCopyAction` | 如果藍圖/源頁至少已發佈一次，則此操作將使用已發佈的版本建立「即時複製」頁。 注：此操作僅可用於基於已發佈的源頁建立Live Copy頁，而不可用於更新現有Live Copy頁。 |  |
| `PageMoveAction` | 的 `PageMoveAction` 在藍圖中移動頁面時應用。<br>操作將複製（相關）「即時複製」頁面，而不是將其從移動之前的位置移動到之後的位置。<br>的 `PageMoveAction` 不會更改移動前位置的「即時複製」頁面。 因此，對於連續的部署配置，它具有無藍圖的即時關係狀態。<br>[配置 **CQ MSM頁移動操作** 服務](#excluding-properties-and-node-types-from-synchronization) 指定要排除的節點類型、段落項和頁面屬性。<br>此操作必須是部署配置中包含的唯一同步操作。 | 設定 `prop_referenceUpdate: (Boolean)` 為true（預設）以更新引用。 |
| `markLiveRelationship` | 此操作表示啟動建立的內容存在即時關係。 |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### 從同步中排除屬性和節點類型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置幾個支援相應同步操作的OSGi服務，以便它們不會影響特定的節點類型和屬性。 例如，與內部功能相關的許多屬性和子節AEM點不應包含在即時拷貝中。 只應複製與頁面用戶相關的內容。

使用時，AEM有多種方法管理此類服務的配置設定。 請參閱 [配置OSGi](/help/implementing/deploying/configuring-osgi.md) 的子菜單。

下表列出了可以指定要排除的節點的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱和使用儲存庫節點進行配置的PID。

| 同步操作 | Web控制台中的服務名稱 | 服務PID |
|---|---|---|
| `contentCopy` | CQ MSM內容複製操作 | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM內容刪除操作 | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM內容更新操作 | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM頁移動操作 | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM引用更新操作 | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

下表介紹了可以配置的屬性：

| Web控制台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 排除的節點類型 | `cq.wcm.msm.action.excludednodetypes` | 與要從同步操作中排除的節點類型匹配的規則運算式 |
| 排除的段落項 | `cq.wcm.msm.action.excludedparagraphitems` | 與要從同步操作中排除的段落項匹配的規則運算式 |
| 排除的頁面屬性 | `cq.wcm.msm.action.excludedprops` | 與要從同步操作中排除的頁屬性匹配的規則運算式 |
| 忽略的混合節點類型 | `cq.wcm.msm.action.ignoredMixin` | 與要從同步操作中排除的混合節點類型的名稱相匹配的規則運算式(僅適用於 `contentUpdate` 動作) |

#### CQ MSM內容更新操作 — 排除 {#cq-msm-content-update-action-exclusions}

預設情況下，會排除一些屬性和節點類型，這些屬性和節點類型在OSGi配置中定義 **CQ MSM內容更新操作**&#x200B;下 **排除的頁面屬性**。

預設情況下，與以下規則運算式匹配的屬性在部署時被排除（即未更新）:

![即時複製排除規則](../assets/live-copy-exclude.png)

您可以根據需要更改定義排除清單的表達式。

例如，如果您希望 **標題** 要包括在考慮部署的更改中，請刪除 `jcr:title` 排除項。 例如，使用regex:

`jcr:(?!(title)$).*`

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置多個OSGi服務，這些服務支援與更新引用相關的相應同步操作。

使用時，AEM有多種方法管理此類服務的配置設定。 請參閱 [配置OSGi](/help/implementing/deploying/configuring-osgi.md) 的子菜單。

下表列出了可為其指定引用更新的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱和使用儲存庫節點進行配置的PID。

| Web控制台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 跨嵌套LiveCopys更新引用 | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | 在Web控制台中選擇此選項，或將此布爾屬性設定為 `true` 使用儲存庫配置替換針對位於最頂層Live Copy分支中的任何資源的引用。 僅可用於 `referencesUpdate` 操作。 |
| 更新引用頁 | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | 在Web控制台中選擇此選項，或將此布爾屬性設定為 `true` 使用儲存庫配置更新任何引用，以使用原始頁引用「即時複製」頁。 僅可用於 `PageMoveAction`。 |

## 指定要使用的展示配置 {#specifying-the-rollout-configurations-to-use}

MSM使您能夠指定一些通常使用的推廣配置集，並且如果需要，您可以為特定即時副本覆蓋這些配置集。 MSM提供了多個位置，用於指定要使用的推廣配置。 該位置確定該配置是否適用於特定即時副本。

以下位置清單可指定要使用的部署配置，說明MSM如何確定用於即時拷貝的部署配置：

* **[Live Copy頁屬性](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** 當Live Copy頁面配置為使用一個或多個部署配置時，MSM使用這些部署配置。
* **[藍圖頁屬性](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** 當即時拷貝基於藍圖，且「即時拷貝」頁面未配置部署配置時，將使用與藍圖源頁面關聯的部署配置。
* **即時複製父頁屬性：** 如果「即時拷貝」頁和藍圖源頁都未配置部署配置，則將使用應用於「即時拷貝」頁的父頁的部署配置。
* **[系統預設值](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** 當無法確定Live Copy的父頁的部署配置時，將使用系統預設的部署配置。

例如，藍圖使用 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 站點作為源內容。 根據藍圖建立站點。 以下清單中的每個項目都描述了有關部署配置使用的不同方案：

* 未將藍圖頁或Live Copy頁配置為使用部署配置。 MSM對所有Live Copy頁使用系統預設部署配置。
* WKND站點的根頁配置了多種部署配置。 MSM將這些部署配置用於所有Live Copy頁。
* WKND站點的根頁配置了多個部署配置，而Live Copy站點的根頁配置了一組不同的部署配置。 MSM使用在Live Copy站點的根頁上配置的部署配置。

### 設定即時複製頁的部署配置 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用展開配置配置配置「即時複製」頁，以便在展開源頁時使用。 預設情況下，子頁繼承配置。 將部署配置配置為使用時，將覆蓋「即時複製」頁從其父級繼承的配置。

您還可以在以下情況下為Live Copy頁面配置部署配置： [建立即時拷貝](creating-live-copies.md#creating-a-live-copy-of-a-page)。

1. 使用 **站點** 控制台，以選擇「即時複製」頁。
1. 選擇 **屬性** 的子菜單。
1. 開啟 **即時拷貝** 頁籤。

   的 **配置** 部分顯示頁面繼承的展開配置。

   ![從父頁即時複製繼承](../assets/live-copy-inherit.png)

1. 如果需要，請調整 **即時複製繼承** 。 如果選中，則Live Copy配置對所有子項都有效。

1. 清除 **從父代繼承展示配置** 屬性，然後從清單中選擇一個或多個部署配置。

   選定的部署配置顯示在下拉清單下方。

   ![覆蓋即時複製配置繼承](../assets/live-copy-inherit-override.png)

1. 按一下或點擊 **保存並關閉**。

### 設定藍圖頁的部署配置 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用展開配置配置配置藍圖頁，以在展開藍圖頁時使用。

請注意，藍圖頁的子頁繼承配置。 配置要使用的展示配置時，可以覆蓋頁面從其父級繼承的配置。

1. 使用 **站點** 控制台，以選擇藍圖的根頁。
1. 選擇 **屬性** 的子菜單。
1. 開啟 **藍圖** 頁籤。
1. 選擇一個或多個 **推廣配置** 使用下拉選擇器。
1. 保留更新 **保存**。

### 設定系統預設部署配置 {#setting-the-system-default-rollout-configuration}

要指定要用作系統預設值的部署配置，請配置以下OSGi服務。

* **第CQ WCM Live關係管理器** 服務PID `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [儲存庫節點](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。

* 在Web控制台中，要配置的屬性的名稱為 **預設部署配置**。
* 使用儲存庫節點，要配置的屬性的名稱為 `liverelationshipmgr.relationsconfig.default`。

將此屬性值設定為要用作系統預設值的推廣配置路徑。 預設值為 `/libs/msm/wcm/rolloutconfigs/default`，即 **標準部署配置**。
