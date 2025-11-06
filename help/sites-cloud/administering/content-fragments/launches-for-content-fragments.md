---
title: 內容片段的啟動
description: 瞭解如何針對Adobe Experience Manager as a Cloud Service中的內容片段使用啟動。 啟動可讓您有效率地開發未來版本的內容，同時維護您目前的內容片段。
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: c0b9e571-3be5-42ab-8d56-d93e8ef4c2f7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 2%

---

# 內容片段的啟動 {#launches-for-content-fragments}

在Adobe Experience Manager (AEM) as a Cloud Service中，啟動可讓您有效率地開發未來版本的內容。

*Launch*&#x200B;已建立，可讓您在維護目前內容的同時，進行變更以準備未來出版物。 對於內容片段，這表示您同時有效地編輯兩個版本：目前發佈的內容以及未來要同時發佈的該內容的版本。 到時，您可以取代原始內容片段的內容並發佈新版本。

>[!NOTE]
>
>「頁面」也提供啟動項。 基本概念相同，但在AEM中管理概念的方式上有所差異。
>
>如需完整詳細資訊，請參閱[啟動頁面](/help/sites-cloud/authoring/launches/overview.md)。

您建立&#x200B;*啟動項*，然後在&#x200B;*啟動項*&#x200B;中編輯和更新您的內容片段。 如果在此階段期間變更&#x200B;*Source*&#x200B;片段，您可以透過&#x200B;*Rebase*&#x200B;作業將其複製到&#x200B;*Launch*。 準備就緒後，*Promote*&#x200B;會將啟動內容複製回來源。 然後，您可以手動或自動啟動來源片段（取決於建立和編輯啟動時設定的欄位）。 您也可以指定是否將參照的片段包含在此程式中。

例如，您線上商店的季節性產品片段會每季更新，以便精選產品與目前季節一致。 若要準備下一次每季更新，您可以建立適當片段的啟動。 在整個季度中，以下變更會累積在啟動副本中：

* 直接在啟動片段上執行的編輯，為下一季做準備。
* 變更您傳送至具有&#x200B;*Rebase*&#x200B;之啟動頁面的來源內容片段。
* 您也可以導覽啟動分支中的內容；視需要新增或移除片段。

當下一季到來時，您可以提升啟動頁面，以便發佈來源頁面（包含更新的內容）。 您可以升級所有片段，或僅升級您已修改的片段。

![啟動總覽 — 重新設定基數和提升](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

本節說明如何在[內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md)內建立、編輯、管理、重設、提升啟動，以及視需要刪除啟動：

* [在內容片段控制檯中存取和檢視啟動](#launches-in-the-content-fragment-console)
* [建立啟動項](#create-a-launch)
* [編輯啟動項內容](#edit-launch-content)
* [管理啟動項中的內容](#manage-content-within-a-launch)
* [比較啟動與來源](#compare-launch-to-source)
* [從Source重新建立Launch基礎](#rebase-a-launch-from-source)
* [將啟動項提升至Source](#promote-a-launch-to-source)
* [刪除啟動項](#delete-a-launch)

## 在內容片段主控台中啟動 {#launches-in-the-content-fragment-console}

內容片段主控台的&#x200B;**啟動項**&#x200B;標籤可讓您建立啟動項、列出所有現有啟動項、檢視關鍵屬性，以及對其採取動作。

未選取啟動項時，您可以[建立新的啟動項](#create-a-launch)。

主控台中的![啟動索引標籤](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

選取要顯示的啟動項：

* 工具列，其中包含可用的動作
* 右側面板，顯示屬性和進一步動作

主控台中的![啟動動作工具列](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

工具列可讓您：

* **[開啟啟動項](#edit-launch-content)**
* **[編輯來源](#manage-content-within-a-launch)**
* **[比較啟動項與Source](#compare-launch-to-source)**
* **[提升](#promote-a-launch-to-source)**
* **[重設](#promote-a-launch-to-source)**
* **[刪除啟動項](#delete-a-launch)**

而右側面板可讓您：

* 編輯啟動項&#x200B;**標題**
* 編輯啟動項&#x200B;**描述**
* 更新您[建立啟動項](#create-a-launch)時所設定的設定詳細資料：

   * **包含參考**：建立包含或不包含任何參考內容片段的啟動項。 依預設，會包含引用的片段。

      * 在稍後的階段，當您[從啟動項](#manage-content-within-a-launch)新增或移除片段時，參考的片段也會受到影響。

     >[!NOTE]
     >
     >檢視[包含參考的詳細資料](#details-concerning-included-references)

   * **發佈就緒**；啟用此切換功能會在啟動項提升至來源時自動發佈片段。

* 並且還定義：

   * **升級日期**&#x200B;和時間：如果[啟動項將自動升級](#promote-automatically)

## 建立啟動項 {#create-a-launch}

若要建立啟動項：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取&#x200B;**建立啟動項**。

1. 導覽至適當的資料夾，並選取要包含在啟動中的片段：

   ![選取新啟動的內容片段](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. 選取&#x200B;**「下一步」**。

1. 指定設定啟動項的詳細資料：

   * **標題**
   * **說明**
   * **包含參考**：建立包含或不包含任何參考內容片段的啟動項。 依預設，會包含引用的片段。

     >[!NOTE]
     >
     >檢視[包含參考的詳細資料](#details-concerning-included-references)

   * **發佈就緒**：啟用此切換功能會在啟動項提升至來源時自動發佈片段。

   新啟動項的![詳細資料](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **儲存**&#x200B;設定。

1. 您會回到內容片段主控台的&#x200B;**啟動**&#x200B;索引標籤，其中：

   * 您的新啟動項現已列出
   * 系統會顯示訊息，確認啟動項建立已開始：

      * **工作已開始建立新的啟動、監視AEM中的進度並在完成後重新載入頁面。**

1. 從訊息方塊中選取「**檢視**」，以在AEM主控台中檢視[背景作業](/help/operations/asynchronous-jobs.md)的詳細資料。

   ![在主控台中新增啟動項](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## 編輯啟動項內容 {#edit-launch-content}

若要編輯啟動項中的內容片段：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項以顯示工具列動作。

1. 選取&#x200B;**開啟啟動項**。

   畫面會顯示您的啟動項，以及其包含的片段。

   ![編輯啟動內容](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. 針對您要更新的片段選取&#x200B;**編輯**。 它將會照常在[片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中開啟。

## 管理啟動項中的內容 {#manage-content-within-a-launch}

若要管理啟動項中的內容片段，並編輯其內容：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項。

1. 選取&#x200B;**編輯來源**。

   將會顯示啟動項的來源片段。

   ![編輯Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. 您可以：

   1. **新增來源**&#x200B;以將更多片段新增至您的啟動項。

      * 如果啟動項的&#x200B;**包含參考**&#x200B;為True，所有參考的內容片段也會帶入啟動項（如果尚未存在）。

   1. 針對您要更新的來源片段選取&#x200B;**編輯**。 它將會照常在[片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中開啟。

   1. 選取片段，然後從工具列選取&#x200B;**刪除來源**&#x200B;動作，將該片段從啟動項中移除。

      * 如果啟動的&#x200B;**包含參考**&#x200B;為True，所有參考的內容片段也會從啟動中移除 — 除非它們也由仍在啟動中的其他內容片段參考。

   >[!NOTE]
   >
   >檢視[包含參考的詳細資料](#details-concerning-included-references)

## 比較啟動與來源 {#compare-launch-to-source}

在任何「重新布基」或「提升」動作之前，建議您一律比較來源和啟動以確認變更及其對您內容的影響（兩個動作都會覆寫目標內容）：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項。

1. 選取&#x200B;**比較啟動項與Source**。

   * 來源和啟動片段會並排顯示，以突顯差異。
      * Source片段會顯示在左側，Launch片段則會顯示在右側。
      * 更新會醒目提示：
         * Source：藍色
         * Launch：粉紅色
         * 衝突：黃色
   * [Promote](#promote-a-launch-to-source)和[Rebase](#rebase-a-launch-from-source)動作可從右上角使用。
   * **找到更新**：在左上角顯示所有更新的摘要。 以藍色顯示的來源更新數、以粉紅色顯示的啟動更新數，以及以黃色顯示的兩個（衝突）更新數。
      * 眼睛圖示可讓您顯示或隱藏實際內容更新，以更清楚概述。
   * **包含**&#x200B;滑桿可讓您定義要包含在後續Promote或Rebase作業中的內容片段：
      * 右上方的&#x200B;**包含全部**
      * 啟動項中每個片段上方的&#x200B;**包含**

     >[!NOTE]
     >
     >滑桿僅適用於從「比較」畫面中執行的「升級」和「重新定位」動作。

   * 片段內容會顯示在欄位層級（內容片段元素/資料型別層級）；反白顯示會指出變更。
   * 選取&#x200B;**檢視**&#x200B;以重新計算差異。

   ![比較Source和Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## 為Launch重新設定基礎(來自Source) {#rebase-a-launch-from-source}

來源片段已進行更新，而您想要將這些變更複製到啟動項時：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項和片段。

1. 選取&#x200B;**重設**。

>[!NOTE]
>
>您也可以從&#x200B;**比較啟動項與Source**&#x200B;來&#x200B;**[重新布建](#compare-launch-to-source)**&#x200B;啟動項。

## 提升啟動(至Source) {#promote-a-launch-to-source}

當您的啟動項準備好要發佈時，應將其複製到來源。 您可以在主控台中執行此作業，或設定在特定日期和時間自動執行此作業的設定。

### 手動提升 {#promote-manually}

當您的啟動項準備好要發佈時，可透過明確動作將其複製到來源：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項和片段。

1. 選取&#x200B;**升級**。

>[!NOTE]
>
>您也可以&#x200B;**將**&#x200B;啟動項從&#x200B;**比較啟動項與Source**&#x200B;提升。

### 自動提升 {#promote-automatically}

若要在指定的日期和時間自動提升啟動，您需要：

1. 定義&#x200B;**啟動標籤**&#x200B;右側面板的[提升日期](#launches-in-the-content-fragment-console)和時間。

1. 如果內容可以在提升時發佈，請在&#x200B;**建立啟動項**&#x200B;時設定[發佈就緒](#create-a-launch)，或從[啟動項索引標籤](#launches-in-the-content-fragment-console)的右側面板設定。

## 刪除啟動項 {#delete-a-launch}

提升您的啟動項，或決定不再需要它後，您可以將其刪除：

1. 導覽至內容片段主控台。

1. 開啟&#x200B;**啟動**&#x200B;標籤。

1. 選取您的啟動項。

1. 選取&#x200B;**刪除啟動項**。

   系統會在刪除啟動項前要求您確認動作。

## 關於包含參考的細節 {#details-concerning-included-references}

對於啟動，會考量下列內容片段參考，取決於[資料型別](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)：

* **片段參考**&#x200B;資料型別，適用於單一片段參考和多欄位片段參考。
* 使用&#x200B;**RTF文字**&#x200B;時，**多行文字**&#x200B;資料型別內參考的片段。

所有要點也適用於變數中參照的片段

不會考慮下列專案：

* 內容參考資料型別內參考的片段，包括&#x200B;**內容參考** （以路徑為基礎）和&#x200B;**內容參考(UUID)**。
* 在&#x200B;**片段參考(UUID)**&#x200B;資料型別中參考的片段。
