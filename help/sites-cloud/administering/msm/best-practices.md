---
title: MSM最佳實務
description: 瞭解由Adobe工程和諮詢團隊編譯的最佳實務，以協助您快速上手使用AEMMulti Site Manager。
feature: 多站點管理員
role: 管理員
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---


# MSM最佳實踐{#msm-best-practices}

## 一般 {#general}

MSM是可設定的架構，可自動化內容部署。 實作通常涉及網站的主要部分，而且涵蓋組織和地域。 因此，強烈建議您像規劃網站一樣，謹慎規劃MSM實作：

* 開始實施前，請仔細&#x200B;**規劃結構和內容流**。
* **視需要自訂，但盡可能少。** 雖然MSM支援高度自訂（例如展出組態），但是您網站的效能、可靠性和可升級性的最佳實務是將自訂降至最低。
* 盡早建立&#x200B;**governance**&#x200B;模型，並據此培訓使用者，以確保成功。 從治理角度來看，最佳做法是&#x200B;**將本機內容製作者擁有的授權(**)降至最低，以便將內容分配／連接至其他本機使用者及其各自的即時副本。 這是因為無管理、鏈式繼承可以顯著增加MSM結構的複雜性，並損害其效能和可靠性。
* 一旦您的結構、內容流程、自動化和治理有了計畫，**就會建立原型並徹底測試您的系統**，然後開始即時實作。
* 請記住，**Adobe咨詢和領先的系統整合商**&#x200B;具有與MSM一起進行內容自動化規劃和實施的豐富經驗，因此，他們可以幫助您開始使用MSM項目，並在整個實施過程中提供幫助。

## 即時副本來源和Blueprint組態{#live-copy-sources-and-blueprint-configurations}

請記住，即時副本可使用[一般頁面](creating-live-copies.md#creating-a-live-copy-of-a-page)或[藍圖設定](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)來建立。 這兩種都是有效的使用案例。

使用Blueprint設定的額外好處是：

* 允許作者在藍圖上使用&#x200B;**Rovolt**&#x200B;選項，以便明確將修改推送至繼承自此藍圖的即時副本。
* 允許作者使用&#x200B;**建立網站**，以輕鬆選擇語言並設定即時副本的結構。
* 定義與藍圖有關的即時副本的預設轉出設定。

如果未參考藍圖設定，則只能從即時副本本身啟動推播，實際上是從來源提取內容。

使用即時副本建立新網站時，建立藍圖組態是有利的，以確保完整MSM功能集的可用性。

## 元件和容器同步{#components-and-container-synchronization}

通常，MSM中關於元件同步的轉出規則是：

* 已推出元件，可同步藍圖中包含的任何資源。
* 容器僅同步目前的資源。

這表示元件會被視為總結，在推出時，元件本身及其所有子系會以藍圖中的元件取代。 這表示，如果資源在本機新增至此類元件，則在開始時會遺失在藍圖的內容中。

若要支援元件巢狀化，以便在轉出中維護本機新增的元件，元件必須宣告為容器。

>[!NOTE]
>
>將屬性`cq:isContainer`新增至元件，將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM建立即時副本的主要方法有兩種：

* 當[建立即時副本時](creating-live-copies.md#creating-a-live-copy-of-a-page) —— 這可視為更一般的方法，讓您從任何頁面建立即時副本。 即時副本的內容結構完全符合來源。

* 當[建立網站時——這是更專業的方法，主要用於建立具有多語言結構的網站。](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

在建立網站時，請注意以下幾點：

* 若要建立新網站，您需要[blueprint組態](creating-live-copies.md#managing-blueprint-configurations)。
* 若要允許選擇語言路徑以在新網站中建立，對應的語言根目錄必須存在於Blueprint（來源）中。
* 一旦將[新網站建立為即時副本](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)（使用&#x200B;**Create**，然後使用&#x200B;**Site**），此即時副本的前兩個層級為&#x200B;*淺層*。 頁面的子系不屬於即時關係，但如果找到符合觸發條件的即時關係，則推出仍會下降。

避免：

* 在Blueprint中手動新增語言（在第一層下）。
* 手動將內容直接新增至語言根目錄下方，因為這不會導致在推出時自動將此新內容傳送至即時副本。

## MSM和多語言網站{#msm-and-multilingual-websites}

MSM可協助建立多語言網站，方式有兩種：

建立語言主版時，請記住下列事項：

* 雖然MSM本身&#x200B;**不提供內容轉譯**，但可與提供內容轉譯的第三方轉譯連接器整合。 請注意：
   * MSM允許您在頁面和／或元件級別取消繼承。 這有助於防止在下次推出時覆寫已翻譯的內容（來自即時副本，而藍圖中尚未翻譯的內容）。
      * 某些協力廠商轉譯連接器會自動管理MSM繼承。
      * 請洽詢您的翻譯服務供應商以取得更多資訊。
      * 建立和翻譯語言主語的另一種方法是結合現成AEM的翻譯整合框架使用語言副本。

如需詳細資訊，請參閱[多語言網站翻譯內容](/help/sites-cloud/administering/translation/overview.md)和[翻譯最佳實務。](/help/sites-cloud/administering/translation/best-practices.md)

## 結構更改和推出{#structure-changes-and-rollouts}

藍圖／來源樹狀結構中的內容結構修改在即時副本中的反映不同。 這取決於修改類型：

* **在** Blueprint中建立新頁面，將會在使用標準轉出設定轉出後，在即時副本中建立對應的頁面。
* **使用** 標準轉出設定轉出後，Blueprint中的刪除頁面將導致從即時副本刪除對應頁面。
* **使用** 標準轉出設 **** 定後，在Blueprint中移動頁面時，不會導致在即時副本中移動對應頁面：
   * 此行為的原因是頁面移動隱含地包含頁面刪除。 這可能會導致發佈時發生非預期的行為，因為刪除作者上的頁面會自動停用發佈時的對應內容。 這也可對相關項目（例如連結、書籤等）產生額外的影響。
      * 會更新個別「即時副本」頁面中的內容繼承，以反映其來源在藍圖中的新位置。
      * 要完全實現頁面從藍圖移動到即時拷貝，請考慮[頁面移動最佳實踐。](#page-move)

### 頁面移動最佳實踐{#page-move}

當考慮在即時副本中移動頁面時，請考慮下列最佳實務。

>[!NOTE]
>
>以下僅適用於[On Rovolt觸發器](live-copy-sync-config.md#rollout-triggers)。

1. 建立自訂轉出設定。
   * 此新配置必須包含`PageMoveAction`操作。
   * 請勿將其他動作新增至此設定。
1. 定位新配置。
   * 若要在即時副本中刪除個別頁面的舊位置，同時完全展開頁面移動：
      * 在標準轉出設定之前，先定位新建立的設定。 標準的轉出設定將負責刪除其舊位置的頁面。
      * 若要展開頁面移動，同時將各頁面保留在即時副本的舊位置（實質上是複製內容）:
         * 在標準轉出設定後，放置新建立的設定。 如此可確保「即時副本」中不會刪除任何內容，也不會從發佈中停用。

## 自訂推出{#customizing-rollouts}

MSM首次展示配置具有高度可定製性。 您應該注意到，自動化推展可能產生深遠影響。 在進行下列活動之前，您應仔細規劃：

* 自動推出，例如使用[onModify triggers](#onmodify)
* 自定義[節點類型／屬性](#node-types-properties)
* 啟動後續工作流程
* 在推展中啟用內容

### onModify {#onmodify}

使用[轉出觸發器](live-copy-sync-config.md#rollout-triggers) `onModify`時，您應考慮：

* 使用`onModify`觸發器自動推出，可能會對製作效能造成負面影響，因為它們會在每次修改頁面後觸發推出。
* 首次推出的結果可能與預期的不同：
   * 您無法指定產生的修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理員的事件順序。
* 如果同一資源發生併發更新，使用這種轉出配置可能會導致提交衝突。

因此，建議您僅在自動開始使用`onModify`觸發器時，自動開始使用的好處超過任何潛在效能問題。

### 節點類型／屬性{#node-types-properties}

除了自訂轉出動作，MSM還可讓您自訂正在轉出的節點屬性。 [MSM OSGi配置允許您排除從源複製到即時拷貝的節點類型](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)。

## 更多資訊 {#further-information}

如需MSM和即時內容的詳細資訊，請參閱下列文章。

* [建立和同步即時副本](creating-live-copies.md)
* [即時副本概述主控台](live-copy-overview.md)
* [配置即時拷貝同步](live-copy-sync-config.md)
* [MSM推出衝突](rollout-conflicts.md)
