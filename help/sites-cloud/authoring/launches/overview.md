---
title: 啟動
description: 啟動使您能夠高效地為未來版本開發內容。 它們允許您為將來的發佈做好更改準備，同時維護當前頁面
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 5%

---

# 啟動 {#launches}

啟動使您能夠高效地為未來版本開發內容。

將建立一個啟動，以便您為將來的發佈做好更改準備（同時維護當前頁面）。 編輯和更新啟動頁面後，您會將其升級回源頁面，然後激活源頁面（頂級）。 升級將啟動內容複製回源頁面，可以手動或自動完成（取決於建立和編輯啟動時設定的欄位）。

例如，您的線上商店的季節性產品頁面會按季度更新，以便特色產品與當前季度保持一致。 為準備下一個季度更新，您可以建立相應的網頁。 在整個季度中，以下更改會累計到發佈副本中：

* 對由於正常維護任務而發生的源頁所做的更改。 這些更改會在啟動頁中自動複製。
* 直接在發佈頁面上執行的編輯，以備下一季度。

您還可以：

* 在發佈分支中導航內容；根據需要添加或刪除頁面。
* 預覽已發佈內容將來如何查看特定日期/天。

下一季度到來時，您將升級啟動頁面，以便發佈源頁面（保存更新的內容）。 您可以升級所有頁面或僅升級已修改的頁面。

啟動還可以是：

* 為多個根分支建立。 雖然您可以為整個站點建立啟動（並在那裡進行更改），但是這可能不切實際，因為需要複製整個站點。 當涉及數百頁甚至數千頁時，複製操作以及以後升級任務所需的比較都會影響系統要求和效能。
* 嵌套（啟動中的啟動），使您能夠從現有啟動建立啟動，以便作者可以利用已做的更改，而不必對每次啟動多次進行相同的更改。

本節介紹如何建立、編輯和升級（如有必要） [刪除](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch))從站點控制台或 [啟動控制台](#the-launches-console):

* [建立啟動 ](/help/sites-cloud/authoring/launches/creating.md)
* [編輯啟動](/help/sites-cloud/authoring/launches/editing.md)
* [在啟動中管理頁面](/help/sites-cloud/authoring/launches/managing-pages.md)
* [使用Timewarp根據啟動預覽內容](/help/sites-cloud/authoring/launches/preview.md)
* [提升啟動](/help/sites-cloud/authoring/launches/promoting.md)

## 啟動 — 事件順序 {#launches-the-order-of-events}

啟動使您能夠有效地開發內容，以便將來發佈一個或多個激活的網頁。

啟動允許您：

* 建立來源頁面的復本：
   * 復本是您的啟動。
   * 頂層來源頁面稱為「生 **產」**。
      * 源頁可以從多個（獨立的）分支中提取。

   ![啟動操作順序](/help/sites-cloud/authoring/assets/launches-order.png)

* 編輯啟動設定：
   * 將頁面和/或分支添加到啟動或從啟動中刪除。
   * 編輯啟動屬性；例如 **Title**、Launch Date **、Production Ready****** 旗標。
* 您可以手動或自動升級和發佈內容：
   * 手動:
      * 將啟動內容提升回 **目標** （源頁面）。
      * 從源頁面發佈內容（在提升後）。
      * 升級所有頁面或僅升級已修改的頁面。
   * 自動 — 這涉及以下內容：
      * 的 **啟動**(**實況**) **日期** 欄位：可以在建立或編輯啟動時設定此設定。
      * 的 **生產就緒** 標誌：只有在編輯啟動時才可設定此值。
      * 如果 **生產就緒** 設定標誌，啟動將自動升級到指定頁面上的生產頁面 **啟動**(**實況**) **日期**。 促銷後，生產頁面會自動發佈。\
         如果尚未設定日期，則標誌將無效。
* 並行更新源和啟動頁面：
   * 對源頁面的更改在啟動副本中自動實現(如果設定為繼承；即作為即時拷貝)。
   * 您可以在不中斷這些自動更新或源頁面的情況下更改啟動副本。

   ![並行操作](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [建立嵌套啟動](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch)  — 在發射中啟動：
   * 源是現有的啟動。
   * 你可以 [提升嵌套啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) 任何目標；這可以是父啟動或頂層源頁（生產）。

   ![嵌套啟動](/help/sites-cloud/authoring/assets/launches-nested.png)

   >[!CAUTION]
   >
   >刪除啟動將刪除啟動本身和所有子體嵌套啟動。

>[!NOTE]
>
>建立和編輯啟動需要訪問權限 `/content/launches`  — 與預設組一樣 `content-authors`。
>
>如果遇到任何問題，請與系統管理員聯繫。

## 在引用（站點控制台）中啟動 {#launches-in-references-sites-console}

1. 在 **站點** 控制台，導航至啟動的源。
1. 開啟 **引用** 並選擇源頁面。
1. 選擇 **啟動**，將列出現有的產品發佈，並訪問 **啟動控制台**:

   ![站點控制台中啟動的引用](/help/sites-cloud/authoring/assets/launches-references.png)

1. 點擊/按一下相應的啟動，將顯示可能的操作清單：

   ![要在站點控制台中啟動的操作](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## 啟動控制台 {#the-launches-console}

「啟動」(Loacuss)控制台提供啟動的概述，並允許您對列出的操作執行操作。 可通過以下方式訪問控制台：

* 的 **工具** 控制台： **工具**。 **站點**。 **啟動**。

* **啟動控制台** 在 **啟動** 的下界 **引用** 在「站點」控制台中導航源內容時進行軌道。

   ![在Sites控制台中啟動的引用中啟動Console](/help/sites-cloud/authoring/assets/launches-references.png)

* 的 **啟動** 按鈕，在「站點」控制台中導航啟動內容時：

   ![在站點控制台中啟動選項](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* 或者直接；例如，與：
   `https://<host>:<port>/libs/launches/content/launches.html`
