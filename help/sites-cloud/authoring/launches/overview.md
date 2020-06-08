---
title: 啟動
description: 啟動可讓您有效率地開發未來版本的內容。 它們可讓您做好變更，以備日後出版，同時仍能維持目前的頁面
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 6%

---


# 啟動 {#launches}

啟動可讓您有效率地開發未來版本的內容。

會建立啟動，讓您做好變更，以備日後出版（同時維持目前的頁面）。 在編輯和更新啟動頁面後，您會將其提升回來源頁面，然後啟動來源頁面（頂層）。 升級會將啟動內容複製回來源頁面，並可手動或自動執行（取決於建立和編輯啟動時設定的欄位）。

例如，您線上商店的季節性產品頁面會每季更新一次，因此精選產品會與目前的季節一致。 為準備下一季度更新，您可以建立適當網頁的啟動。 在整個季度中，產品發佈副本中會累計下列變更：

* 對因正常維護任務而發生的源頁面進行更改。 這些變更會自動在啟動頁面中複製。
* 直接在啟動頁面上執行的編輯，以備下一季度使用。

下一季到來時，您會促銷啟動頁面，以便發佈來源頁面（保有更新的內容）。 您可以升級所有頁面，或僅升級已修改的頁面。

啟動也可以是：

* 為多個根分支建立。 雖然您可以建立整個網站的啟動（並在此進行變更），但是這可能不切實際，因為整個網站需要複製。 當涉及數百頁甚至數千頁時，複製動作以及升級工作所需的比較都會影響系統需求和效能。
* 巢狀內嵌（啟動中的啟動），可讓您從現有的啟動建立啟動，讓作者可以利用已做的變更，而不需針對每次啟動進行多次相同的變更。

本節說明如何從Sites主控台或啟動主控台中建立、編輯 [和提升](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)(以及視需要 [刪除)啟動頁面](#the-launches-console):

* [建立啟動 ](/help/sites-cloud/authoring/launches/creating.md)
* [編輯啟動](/help/sites-cloud/authoring/launches/editing.md)
* [提升啟動](/help/sites-cloud/authoring/launches/promoting.md)

## 啟動——事件順序 {#launches-the-order-of-events}

啟動可讓您有效率地開發內容，以供日後發行的一或多個已啟動網頁使用。

啟動可讓您：

* 建立來源頁面的復本：
   * 復本是您的啟動。
   * 頂層來源頁面稱為「生 **產」**。
      * 來源頁面可從多個（個別）分支取用。

   ![啟動操作順序](/help/sites-cloud/authoring/assets/launches-order.png)

* 編輯啟動設定：
   * 在啟動中新增或移除頁面和／或分支。
   * 編輯啟動屬性；例如 **Title**、Launch Date **、Production Ready****** 旗標。
* 您可以手動或自動促銷和發佈內容：
   * 手動:
      * 當您的啟動內容準備好發佈 **時，將其推回** Target（來源頁面）。
      * 從來源（在向後促銷後）頁面發佈內容。
      * 升級所有頁面，或僅升級修改的頁面。
   * 自動——這涉及下列事項：
      * The **Launch**(**Live**) **date** field: this can be set when creating or editing a launch.
      * 「生 **產就緒** 」標幟： 這只能在編輯啟動時設定。
      * If the **Production Ready** flag is set, the launch will be automatically promoted to the production pages on the specified **Launch**(**Live**) **date**. 促銷後，生產頁面會自動發佈。\
         如果尚未設定日期，則旗標將無效。
* 同時更新來源和啟動頁面：
   * 對源頁面的更改會自動在啟動副本中實現(如果設定為繼承； 即即即即時副本)。
   * 您可以變更啟動副本，而不中斷這些自動更新或來源頁面。

   ![並行動作](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [建立巢狀啟動](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) -啟動中的啟動：
   * 來源是現有的啟動。
   * 您可以將 [巢狀啟動提升至](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) 任何目標； 這可以是父級啟動或頂層來源頁面（生產）。

   ![巢狀啟動](/help/sites-cloud/authoring/assets/launches-nested.png)

   >[!CAUTION]
   >
   >刪除啟動會移除啟動本身和所有子系巢狀啟動。

>[!NOTE]
>
>建立和編輯啟動需要存取權 `/content/launches` 限——與預設群組一樣 `content-authors`。
>
>如果您遇到任何問題，請聯絡您的系統管理員。

### 啟動控制台 {#the-launches-console}

「啟動」控制台提供啟動的概述，並可讓您對所列的動作採取動作。 可通過以下方式訪問控制台：

* 工 **具控制** 台： **工具**、 **網站**、 **啟動**。

* 或直接使用 `https://<host>:<port>/libs/launches/content/launches.html`

## 參考中的啟動(Sites Console) {#launches-in-references-sites-console}

1. 在 **Sites** Console中，導覽至啟動的來源。
1. 開啟「參 **考** 」邊欄，並選取來源頁面。
1. 選取 **啟動**，現有啟動將會列出：

   ![網站主控台中啟動的參考](/help/sites-cloud/authoring/assets/launches-references.png)

1. 點選／按一下適當的啟動，將會顯示可能動作的清單：

   ![在網站主控台中啟動的動作](/help/sites-cloud/authoring/assets/launches-references-actions.png)
