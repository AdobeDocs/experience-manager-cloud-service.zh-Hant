---
title: 提升啟動
description: 您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: b5ded40d1cb8b8fab28583467b68c4586eecf1a0
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# 提升啟動 {#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，可使用下列選項：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是要升級完整啟動項，還是隻升級已變更的頁面。
* 升級後是否要刪除啟動。

>[!NOTE]
>
>將啟動頁面提升至目標（**生產**）後，您可以啟動&#x200B;**生產**&#x200B;頁面作為實體（讓程式更快）。 將頁面新增至Workflow封裝，並作為啟動頁面封裝的Workflow的裝載。 提升啟動項之前，必須先建立工作流程封裝。 請參閱[使用AEM工作流程](#processing-promoted-pages-using-aem-workflow)處理提升頁面。

>[!CAUTION]
>
>無法同時提升單一啟動。 這表示在同一個啟動上同時執行兩個提升動作可能會導致錯誤 — `Launch could not be promoted` （連同記錄中的衝突錯誤）。

>[!CAUTION]
>
>提升&#x200B;*已修改*&#x200B;頁面的啟動時，來源和啟動分支中的修改都會被考慮。

## 提升啟動頁面 {#promoting-launch-pages}

>[!NOTE]
>
>當只有一個啟動層級時，這會涵蓋提升啟動頁面的手動動作。 請參閱：
>
>* [當結構中有多個啟動項時，提升巢狀啟動項](#promoting-a-nested-launch)。
>* [啟動 — 活動順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)，以取得關於自動促銷活動和發佈的進一步詳細資訊。
>

您可以從&#x200B;**Sites**&#x200B;主控台或&#x200B;**Launches**&#x200B;主控台提升啟動：

1. 開啟：
   * 瀏覽來源頁面時的&#x200B;**網站**&#x200B;主控台：
      1. 開啟[參考邊欄](/help/sites-cloud/authoring/sites-console/console-side-panel.md#references)，然後使用[選取模式](/help/sites-cloud/authoring/basic-handling.md)來選取必要的來源頁面（或者選取並開啟參考邊欄，順序並不重要）。 所有參照都會顯示。
      1. 選取&#x200B;**啟動** (例如「啟動(1)」)以顯示特定啟動清單。
      1. 選取特定啟動項以顯示可用的動作。
      1. 選取&#x200B;**提升啟動**&#x200B;以開啟精靈。
   * 瀏覽啟動頁面時的&#x200B;**Sites**&#x200B;主控台：
      1. 使用[選取模式](/help/sites-cloud/authoring/basic-handling.md)選取必要的啟動頁面。
      1. **Promote**&#x200B;動作在工具列中可供使用。
   * **啟動**&#x200B;主控台：
      1. 選取您的啟動項（選取縮圖）。
      1. 選取&#x200B;**升級**。
1. 在第一個步驟中，您可以指定：
   * **目標**
      * **促銷活動後刪除啟動項**
   * **領域**
      * **提升完整啟動項**
      * **提升已修改的頁面**
      * **提升已核准的頁面** — 取決於啟動核准工作流程
      * **升級目前頁面**
      * **提升目前頁面和子頁面**

     例如，當選取僅提升已修改的頁面時：

     ![啟動項促銷活動](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >若您有巢狀啟動，請參閱提升巢狀啟動[，這會涵蓋單一啟動](#promoting-a-nested-launch)。

1. 選取&#x200B;**下一步**&#x200B;以繼續。

1. 您可以檢閱要提升的頁面，頁面視您選擇的頁面範圍而定：

   ![檢閱促銷活動](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. 選取&#x200B;**升級**。

## 編輯時提升啟動頁面 {#promoting-launch-pages-when-editing}

當您編輯啟動頁面時，**頁面資訊**&#x200B;中也提供&#x200B;**提升啟動**&#x200B;動作。 這會開啟精靈以收集所需的資訊。

![從網站資訊提升啟動](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>這適用於單一和[巢狀啟動](#promoting-a-nested-launch)。

## 提升巢狀啟動 {#promoting-a-nested-launch}

建立巢狀啟動後，您可以將其升級回任何來源，包括根來源（生產）。

![巢狀啟動](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. 如同建立巢狀啟動項一樣，在&#x200B;**啟動項**&#x200B;主控台或&#x200B;**參考**&#x200B;邊欄中，導覽並選取所需的啟動項。
1. 選取&#x200B;**提升啟動**&#x200B;以開啟精靈。
1. 輸入必要的明細：
   * **目標**
      * **促銷目標** — 您可以促銷至任何來源。
      * **促銷活動後刪除啟動項** — 促銷活動後，會刪除所選啟動項及其內巢狀啟動項。
   * **範圍** — 您可在此選取是要提升整個啟動，還是只提升已實際編輯的頁面。 如果是後者，您就可以選取包含/排除子頁面。 預設設定為僅提升目前頁面的頁面變更：
      * **提升完整啟動項**
      * **提升已修改的頁面**
      * **提升已核准的頁面** — 取決於啟動核准工作流程
      * **升級目前頁面**
      * **提升目前頁面和子頁面**

   ![提升啟動設定](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. 選取&#x200B;**「下一步」**。
1. 在選取&#x200B;**提升**&#x200B;之前，請先檢閱提升詳細資料：

   ![檢閱提升設定](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >列出的頁面將取決於定義的&#x200B;**範圍**，而且可能取決於實際編輯的頁面。

1. 您的變更會提升並反映在&#x200B;**啟動**&#x200B;主控台中：

   ![在啟動主控台](/help/sites-cloud/authoring/assets/launches-console.png)

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來對提升的「啟動」頁面執行大量處理：

1. 建立Workflow封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

若要在提升頁面時自動啟動工作流程，請為封裝節點設定工作流程啟動器。<!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![促銷工作流程](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
