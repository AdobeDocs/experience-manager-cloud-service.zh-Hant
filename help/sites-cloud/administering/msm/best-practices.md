---
title: MSM最佳實務
description: 了解由Adobe工程和諮詢團隊編譯的最佳實務，以協助您快速上手並執行AEM Multi Site Manager。
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# MSM最佳實務 {#msm-best-practices}

## 一般 {#general}

MSM是可自動部署內容的可設定架構。 實作通常涉及網站的主要部分，並橫跨組織和地理區域。 因此，強烈建議您在規劃網站時，務必謹慎規劃MSM實作：

* 小心 **規劃結構和內容流程** 開始實作之前。
* **視需要自訂，但盡可能少。** 雖然MSM支援高度自訂（例如轉出設定），但針對網站效能、可靠性和可升級性，通常最佳實務是將自訂降至最低。
* 建立 **治理** 及早建模，並據此訓練使用者，以確保成功。 從治理角度來看，最佳實務是 **盡量減少本地內容製作者的權威** 來分配/連線內容給其他本機使用者及其各自的Live Copy。 這是因為不受管理、鏈式繼承可以顯著增加MSM結構的複雜性，並損害其效能和可靠性。
* 一旦您的結構、內容流、自動化和治理存在計畫， **原型和徹底測試您的系統** 開始即時實作之前。
* 請記住 **Adobe咨詢和領先的系統整合商** 擁有透過MSM進行內容自動化規劃與實作的豐富經驗，因此可協助您開始使用MSM專案，以及完成整個實作。

## 即時副本來源和Blueprint設定 {#live-copy-sources-and-blueprint-configurations}

請記住，您可以使用 [一般頁面](creating-live-copies.md#creating-a-live-copy-of-a-page) 或 [Blueprint設定](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 兩者皆為有效的使用案例。

使用Blueprint配置的額外好處是：

* 允許作者使用 **轉出** 選項，以便明確將修改推送至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站** 以便輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關係的Live Copy定義預設轉出設定。

如果未參考Blueprint設定，則只能從Live Copy本身啟動轉出，實際上是從來源提取內容。

使用Live Copy建立新網站時，建立Blueprint設定是有利的作法，以確保可使用完整的MSM功能集。

>[!NOTE]
>
> 請注意，「權限」頁簽中的CUG無法從Blueprint轉出到Live Copy。 設定Live Copy時，請針對此進行規劃。

## 元件和容器同步 {#components-and-container-synchronization}

一般而言，MSM中關於元件同步的轉出規則為：

* 系統會推出元件，同步Blueprint中包含的任何資源。
* 容器僅同步當前資源。

這表示元件被視為聚合，在轉出時，元件本身及其所有子代將被藍圖中的元件替換。 這表示如果資源在本機新增至此類元件，在轉出時將會遺失至Blueprint的內容。

若要支援元件巢狀，以便轉出時維護本機新增的元件，必須將元件宣告為容器。

>[!NOTE]
>
>新增屬性 `cq:isContainer` 元件來將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM有兩種建立Live Copy的主要方法：

* 當 [建立即時副本](creating-live-copies.md#creating-a-live-copy-of-a-page)  — 這可視為較通用的方法，可讓您從任何頁面建立Live Copy。 即時副本的內容結構完全符合來源。

* 當 [建立網站](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)  — 這是一種更專業的方法，主要用於建立具有多語言結構的網站。

建立網站時，請謹記以下幾點：

* 若要建立新網站，您需要 [Blueprint設定](creating-live-copies.md#managing-blueprint-configurations).
* 若要允許選取要在新網站中建立的語言路徑，對應的語言根必須存在於Blueprint（來源）中。
* 一次a [已將新網站建立為即時副本](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **建立**，然後 **網站**)，此Live Copy的前兩個層級為 *淺*. 頁面的子項不屬於即時關係，但如果找到符合觸發器的即時關係，則轉出仍會下降。

有助於避免：

* 在Blueprint中手動新增語言（在第一層下）。
* 手動在語言根目錄正下方新增內容，因為這不會導致在轉出時自動將此新內容傳送到Live Copy。

## MSM與多語言網站 {#msm-and-multilingual-websites}

MSM可以以兩種方式協助建立多語言網站：

建立語言主版時，請記住以下事項：

* 而MSM本身 **不提供內容翻譯**，則可與具備此功能的協力廠商翻譯連接器整合。 請注意：
   * MSM可讓您取消頁面和/或元件層級的繼承。 這有助於防止下次轉出時覆寫已轉譯的內容（來自即時副本，而來自Blueprint的尚未轉譯內容）。
      * 某些第三方翻譯連接器會自動管理MSM繼承內容。
      * 請洽詢您的翻譯服務提供商以了解更多資訊。
      * 建立和翻譯語言主版的替代方法是結合AEM現成的翻譯整合架構使用語言副本。

如需詳細資訊，請參閱 [轉譯多語言網站的內容](/help/sites-cloud/administering/translation/overview.md) 和 [翻譯最佳實務。](/help/sites-cloud/administering/translation/best-practices.md)

## 結構變更和轉出 {#structure-changes-and-rollouts}

Blueprint/來源樹狀結構中對內容結構的修改，在Live Copy中的反映方式不同。 這取決於修改類型：

* **建立** blueprint中的新頁面使用標準轉出設定轉出後，將導致在Live Copy中建立對應的頁面。
* **刪除** Blueprint中的頁面在透過標準轉出設定轉出後，將會導致從Live Copy刪除對應的頁面。
* **移動** 藍圖中的頁面 **not** 透過標準轉出設定，導致轉出後對應的頁面移至Live Copy中：
   * 此行為的原因是頁面移動隱含地包含頁面刪除。 這可能會在發佈時導致非預期的行為，因為刪除作者上的頁面會自動在發佈時停用對應的內容。 這也可能對相關項目（例如連結、書籤等）產生額外影響。
      * 會更新個別Live Copy頁面中的內容繼承，以反映其來源在Blueprint中的新位置。
      * 若要完全實現頁面從Blueprint移至Live Copy，請考慮 [頁面移動最佳實務。](#page-move)

### 頁面移動最佳作法 {#page-move}

考慮在Live Copy中移動頁面時，請考慮下列最佳實務。

>[!NOTE]
>
>下列項目僅能搭配 [轉出觸發時](live-copy-sync-config.md#rollout-triggers).

1. 建立自訂轉出設定。
   * 這個新設定必須包含動作 `PageMoveAction`.
   * 請勿將其他動作新增至此設定。
1. 定位新配置。
   * 若要在Live Copy中刪除個別頁面的舊位置時完全轉出頁面移動：
      * 在標準轉出設定之前放置新建立的設定。 標準轉出設定會處理刪除其舊位置中的頁面。
      * 若要展開頁面移動，同時將個別頁面保留在Live Copy的舊位置（基本上重複內容）:
         * 在標準轉出設定後，放置新建立的設定。 這可確保Live Copy中不會刪除任何內容，或從發佈中停用。

## 自訂轉出 {#customizing-rollouts}

MSM轉出設定可高度自訂。 請注意，自動轉出可能會產生深遠的後果。 在進行下列活動之前，您應謹慎規劃，此為最佳作法：

* 自動轉出，例如使用 [onModify觸發器](#onmodify)
* 自訂 [節點類型/屬性](#node-types-properties)
* 開始後續的工作流程
* 在轉出中啟用內容

### onModify {#onmodify}

使用 [轉出觸發](live-copy-sync-config.md#rollout-triggers) `onModify` 您應考慮：

* 使用自動轉出 `onModify` 觸發器可能會對製作效能造成負面影響，因為它們會在每次修改頁面後觸發轉出。
* 轉出結果可能與預期的不同，如下所示：
   * 您無法指定產生的修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理器的事件順序。
* 如果同一資源同時更新，使用此類轉出設定可能會導致提交衝突。

因此，建議您只使用 `onModify` 如果自動轉出啟動的好處超過任何潛在的效能問題，就會觸發。

### 節點類型/屬性 {#node-types-properties}

除了自訂轉出動作，MSM也可讓您自訂正在轉出的節點屬性。 此 [MSM OSGi設定可讓您排除節點類型](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) 從來源複製到Live Copy。

## 更多資訊 {#further-information}

如需MSM和Live Copy的詳細資訊，請參閱下列文章。

* [建立和同步Live Copy](creating-live-copies.md)
* [Live Copy概述主控台](live-copy-overview.md)
* [配置Live Copy同步](live-copy-sync-config.md)
* [MSM轉出衝突](rollout-conflicts.md)
