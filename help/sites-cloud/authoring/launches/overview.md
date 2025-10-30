---
title: 頁面啟動
description: 瞭解如何在Adobe Experience Manager as a Cloud Service中使用頁面啟動項。 啟動可讓您有效率地開發未來版本的內容，同時維護您目前的頁面。
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 20ad1d468ac0d8ec3933477f954120debe4e9240
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 72%

---

# 頁面啟動 {#launches-for-pages}

在Adobe Experience Manager (AEM) as a Cloud Service中，啟動可讓您有效率地開發未來版本的內容。

*Launch*&#x200B;已建立，可讓您在維護目前內容的同時，進行變更以準備未來出版物。 針對AEM頁面，這表示您同時有效編輯兩個版本：目前發佈的頁面，以及未來將同時發佈的這些頁面版本。 到了那一天後，您就可以取代原始頁面並發佈新版本。

>[!NOTE]
>
>內容片段也提供啟動項。 基本概念相同，但在AEM中管理概念的方式上有所差異。
>
>如需完整詳細資訊，請參閱[內容片段啟動](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)。

您建立&#x200B;*Launch*，然後在編輯和更新您的&#x200B;*Launch*&#x200B;頁面後，將其&#x200B;*提升*&#x200B;回&#x200B;*Source*。 然後您可以啟用這些&#x200B;*Source*&#x200B;頁面（頂層）。 提升功能會將啟動內容複製回來源頁面，可以手動或自動完成 (視建立和編輯啟動時設定的欄位)。

例如，您的線上商店的季節性產品頁面每季更新一次，以便特色產品符合目前季節。為準備下一季的更新，您可以建立一個相應網頁的啟動。在整個季度中，以下變更會累積在啟動副本中：

* 因正常維護工作而產生的來源頁面變更。這些變更會自動複製到啟動頁面中。
* 直接在啟動頁面上執行的編輯，為下一季做準備。

您也可以：

* 導覽啟動分支中的內容，視需要新增或移除頁面。
* 預覽已發佈內容未來特定日期的外觀。

下一季到來時，您提升啟動頁面，以便您可以發佈來源頁面 (包含更新的內容)。您可以提升所有頁面，也可僅提升您修改過的頁面。

啟動也可以：

* 為多個根分支建立。雖然您可以建立整個網站的啟動（並在那裡進行變更），但這並不實際，因為必須複製整個網站。 當涉及數百甚至數千頁時，複製動作和之後提升工作所需的比較作業，會影響系統要求和效能。
* 巢狀 (啟動中有啟動) 可讓您在現有啟動中建立啟動，如此作者可以利用已完成的變更，而不用對每個啟動重複進行相同的變更。

此章節描述如何從 Sites 主控台或[啟動](#the-launches-console)主控台，建立、編輯和提升 (如有需要可[刪除](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) 啟動頁面。

* [建立啟動](/help/sites-cloud/authoring/launches/creating.md)
* [編輯啟動](/help/sites-cloud/authoring/launches/editing.md)
* [管理啟動中的頁面](/help/sites-cloud/authoring/launches/managing-pages.md)
* [使用 Timewarp 根據啟動預覽您的內容](/help/sites-cloud/authoring/launches/preview.md)
* [提升啟動](/help/sites-cloud/authoring/launches/promoting.md)

## 啟動 - 事件順序 {#launches-the-order-of-events}

啟動可讓您有效率地為一或多個已啟動網頁的未來版本開發內容。

啟動可讓您：

* 建立來源頁面的副本：
   * 副本是您的啟動。
   * 頂層來源頁面稱為&#x200B;**生產**。
      * 來源頁面可以取自多個 (獨立的) 分支。

  ![啟動操作順序](/help/sites-cloud/authoring/assets/launches-order.png)

* 編輯啟動設定：
   * 在啟動中新增或移除頁面和/或分支。
   * 編輯啟動屬性；例如&#x200B;**標題**、**啟動日期**、**生產就緒**&#x200B;標幟。
* 您可以手動或自動提升和發佈內容：
   * 手動：
      * 當準備好發佈時，將啟動內容推回 **Target** (來源頁面)。
      * 從來源頁面 (推回後) 發佈內容。
      * 提升所有頁面，或僅提升修改後的頁面。
   * 自動 - 這涉及以下項目：
      * **啟動** (**上線**) **日期**&#x200B;欄位：這可在建立或編輯啟動時設定。
      * **生產就緒**&#x200B;標幟：這只能在編輯啟動時設定。
      * 如果&#x200B;**生產就緒**&#x200B;標幟已設定，啟動會於 **啟動** (**上線**) **日期**&#x200B;自動提升至生產頁面。提升後，生產頁面會自動發佈。\
        如果未設定日期，則該標幟將無效。
* 並行更新來源頁面和啟動頁面：
   * 對來源頁面的變更會自動實作在啟動副本 (如果設定為繼承，即為 Live Copy)。
   * 可以在不中斷這些自動更新或來源頁面的情況下，對啟動副本進行變更。

  ![並行動作](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [建立巢狀啟動](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - 啟動中的啟動：
   * 來源是現有的啟動。
   * 您可以[將巢狀啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)提升到任何目標，這可以是父啟動或頂層來源頁面 (生產)。

  ![巢狀啟動](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >刪除啟動將移除啟動本身和所有子系巢狀啟動。

>[!NOTE]
>
>建立和編輯啟動需要 `/content/launches` 的存取權 - 與預設群組 `content-authors` 相同。
>
>如果您遇到任何問題，請聯絡您的系統管理員。

## 啟動在在參考內 (Sites 主控台) {#launches-in-references-sites-console}

1. 在 **Sites** 主控台中，導覽至啟動來源。
1. 開啟&#x200B;**參考**&#x200B;邊欄並選取來源頁面。
1. 選取&#x200B;**啟動**，會列出現有的啟動，以及&#x200B;**啟動主控台**&#x200B;的存取權：

   ![網站主控台中的啟動參考](/help/sites-cloud/authoring/assets/launches-references.png)

1. 選取適當的啟動，便會顯示可能的動作清單：

   ![網站主控台中對啟動執行的動作](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## 啟動主控台 {#the-launches-console}

>[!NOTE]
>
>此主控台僅供頁面啟動使用。
>
>若要管理您的內容片段，請參閱內容片段的[啟動](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)。

「啟動」主控台提供啟動的總覽，並可讓您對列出的啟動執行動作。

![啟動主控台 — 管理內容](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

主控台可透過以下方式存取：

* **工具**&#x200B;主控台： **工具**，**一般**，**啟動**。

* 在 Sites 主控台瀏覽來源內容時，**啟動主控台**&#x200B;位於&#x200B;**參考**&#x200B;邊欄&#x200B;**啟動**&#x200B;區段的底部。

  ![啟動主控台位於 Sites 主控台的啟動參考中](/help/sites-cloud/authoring/assets/launches-references.png)

* 在 Sites 主控台導覽啟動內容時，**啟動** 按鈕位於右上角：

  ![Sites 主控台中的啟動選項](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
