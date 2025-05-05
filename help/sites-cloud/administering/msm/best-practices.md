---
title: MSM 最佳做法
description: 瞭解Adobe工程和諮詢團隊編譯的最佳實務，協助啟動和執行AEM Multi Site Manager。
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 3%

---

# MSM 最佳做法 {#msm-best-practices}

## 一般 {#general}

MSM是可設定的架構，用於自動化內容部署。 實作通常涉及網站的主要部分，且橫跨多個組織和地區。 因此，強烈建議您如同規劃網站一樣仔細規劃MSM實施：

* 開始實作前，請仔細&#x200B;**規劃結構和內容流程**。
* **請儘可能多地自訂，但儘可能少地自訂。**&#x200B;雖然MSM支援高度自訂（例如轉出設定），但通常網站效能、可靠性和可升級性的最佳實務是將自訂最小化。
* 及早建立&#x200B;**治理**&#x200B;模型，並據此訓練使用者以確保成功。 從治理的觀點來看，最佳實務是&#x200B;**將本機內容製作者擁有**&#x200B;的授權最小化，以配置/連線內容給其他本機使用者及其個別即時副本。 這是因為，不受控管的鏈式繼承會大幅增加MSM結構的複雜性，並損害其效能和可靠性。
* 在針對您的結構、內容流程、自動化和控管制定計畫後，**建立原型並徹底測試您的系統**，然後再開始即時實作。
* 請記住，**Adobe Consulting和領先的系統整合經銷商**&#x200B;擁有使用MSM規劃和實作內容自動化的豐富經驗，他們可以協助您開始使用MSM專案並完成整個實作。

## 即時副本來源和Blueprint設定 {#live-copy-sources-and-blueprint-configurations}

請記住，可使用[一般頁面](creating-live-copies.md#creating-a-live-copy-of-a-page)或[Blueprint設定](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)來建立即時副本。 兩者都是有效的使用案例。

使用Blueprint設定的其他優點包括：

* 允許作者在Blueprint上使用&#x200B;**轉出**&#x200B;選項，以明確推送修改至從此Blueprint繼承的即時副本。
* 允許作者使用&#x200B;**建立網站**&#x200B;以輕鬆選取語言並設定即時副本的結構。
* 為與藍圖具有關係的 Live Copy 定義預設推出設定。

如果未參考Blueprint設定，則轉出只能從即時副本本身啟動，基本上是從來源提取內容。

使用即時副本建立網站時，建立Blueprint設定以確保完整MSM功能集的可用性是有利的。

>[!NOTE]
>
>許可權索引標籤中的CUG無法從Blueprint轉出至即時副本。 設定即時副本時，請針對此規則制定計畫。

## 元件與容器同步 {#components-and-container-synchronization}

一般而言，MSM中有關元件同步的轉出規則是：

* 元件會與Blueprint中包含的任何資源同步推出。
* 容器僅同步目前資源。

這表示會將元件視為彙總，在轉出時，元件本身及其所有子項都會取代為Blueprint中的元件。 這表示如果在本機將資源新增至這類元件，轉出時就會遺失至Blueprint的內容中。

若要支援巢狀元件，以便在轉出中維護本機新增的元件，必須將元件宣告為容器。

>[!NOTE]
>
>將屬性`cq:isContainer`新增至元件，以將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM有兩個建立即時副本的主要方法：

* [建立即時副本時](creating-live-copies.md#creating-a-live-copy-of-a-page) — 這可以視為較一般的方法，可讓您從任何頁面建立即時副本。 即時副本的內容結構與來源完全相符。

* [建立網站](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)時 — 這是更專業的方法，主要用於建立具有多語言結構的網站。

以下是建立網站時請謹記的幾個考量事項：

* 若要建立網站，您需要[Blueprint設定](creating-live-copies.md#managing-blueprint-configurations)。
* 若要允許選取在新網站中建立的語言路徑，對應的語言根必須存在於Blueprint （來源）中。
* 一旦將[新網站建立為即時副本](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) （使用&#x200B;**Create**，然後使用&#x200B;**Site**），此即時副本的前兩個層級為&#x200B;*淺層*。 頁面的子系不屬於即時關係，但如果找到符合觸發器的即時關係，轉出仍會下降。

這有助於避免：

* 在Blueprint中手動新增語言（第一個層級下）。
* 直接在語言根底下手動新增內容，因為這不會導致在轉出時自動將此新內容傳送到即時副本。

## MSM和多語言網站 {#msm-and-multilingual-websites}

MSM可以透過兩種方式協助建立多語言網站：

建立語言主版時，請牢記以下事項：

* 雖然MSM本身&#x200B;**不提供內容翻譯**，但它可以與第三方翻譯聯結器整合。 請注意下列事項：
   * MSM可讓您取消頁面和/或元件層級的繼承。 這有助於防止在下一次轉出時覆寫已翻譯內容（來自即時副本，以及來自Blueprint的尚未翻譯內容）。
      * 有些協力廠商翻譯聯結器會將MSM繼承的管理作業自動化。
      * 請洽詢您的翻譯服務提供者，以取得詳細資訊。
      * 建立及翻譯語言主版的替代方法是將語言副本與AEM現成的翻譯整合架構搭配使用。

如需詳細資訊，請參閱[翻譯多語言網站的內容](/help/sites-cloud/administering/translation/overview.md)和[翻譯最佳實務](/help/sites-cloud/administering/translation/best-practices.md)。

## 結構變更和轉出 {#structure-changes-and-rollouts}

對Blueprint/來源樹狀結構中內容結構的修改，會以不同方式反映在即時副本中。 這取決於修改型別：

* **在Blueprint中建立**&#x200B;新頁面將導致在使用標準轉出設定轉出後，在即時副本中建立對應的頁面。
* 在Blueprint中刪除&#x200B;**1&rbrace;頁面將導致在使用標準轉出設定轉出後，對應的頁面從即時副本中刪除。**
* 在Blueprint中移動&#x200B;**頁面將**&#x200B;不會&#x200B;**導致在採用標準轉出設定的轉出後，在即時副本中移動對應的頁面：**
   * 此行為的原因是頁面移動隱含包含頁面刪除。 這可能會導致發佈時產生非預期的行為，因為刪除作者上的頁面會自動停用發佈上的對應內容。 這也可能對相關專案（例如連結、書籤等）產生其他影響。
      * 個別即時副本頁面中的內容繼承會更新，以反映其來源在Blueprint中的新位置。
      * 若要完全實現從Blueprint到即時副本的頁面移動，請考慮[頁面移動最佳實務]。(#page-move)

### 頁面移動最佳實務 {#page-move}

考慮在即時副本中移動頁面時，請考慮以下最佳實務。

>[!NOTE]
>
>下列僅適用於[轉出觸發程式](live-copy-sync-config.md#rollout-triggers)。

1. 建立自訂轉出設定。
   * 此新設定必須包含動作`PageMoveAction`。
   * 請勿將其他動作新增至此設定。
1. 定位新組態。
   * 若要完全轉出頁面移動，同時在即時副本中的舊位置刪除個別頁面：
      * 將建立的設定放置在標準轉出設定之前。 標準轉出設定會負責刪除舊位置的頁面。
      * 若要轉出頁面移動，同時將個別頁面保留在即時副本中的舊位置（基本上是重複的內容）：
         * 將建立的設定放置在標準轉出設定的後面。 這將確保即時副本中的內容不會被刪除或從發佈中停用。

## 自訂轉出 {#customizing-rollouts}

MSM轉出設定是高度可自訂的。 自動化轉出可能會產生深遠的影響。 最佳實務是，在從事下列活動之前，請務必仔細規劃：

* 使用[onModify觸發程式](#onmodify)自動化轉出
* 自訂[節點型別/屬性](#node-types-properties)
* 開始後續工作流程
* 在轉出中啟用內容

### onModify {#onmodify}

使用[轉出觸發程式](live-copy-sync-config.md#rollout-triggers) `onModify`時，您應考慮：

* 使用`onModify`觸發器自動化轉出可能會對編寫效能產生負面影響，因為它們會在每次修改頁面後觸發轉出。
* 轉出結果可能與預期結果不同：
   * 您無法指定產生之修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理器的事件順序。
* 如果同時更新相同資源，使用此轉出設定可能會導致提交衝突。

因此，如果自動轉出啟動的好處多於任何潛在的效能問題，建議您只使用`onModify`觸發器。

### 節點型別/屬性 {#node-types-properties}

除了自訂轉出動作之外，MSM也可讓您自訂正在轉出的節點屬性。 [MSM OSGi設定可讓您排除從來源複製到即時副本的節點型別](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)。

## 更多資訊 {#further-information}

請參閱下列文章以取得有關MSM和Live Copy的詳細資料。

* [建立和同步 Live Copies](creating-live-copies.md)
* [Live Copy 概觀主控台](live-copy-overview.md)
* [設定 Live Copy 同步](live-copy-sync-config.md)
* [MSM 推出衝突](rollout-conflicts.md)
