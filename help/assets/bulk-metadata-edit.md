---
title: 在Assets檢視中編輯大量中繼資料
description: 瞭解如何在Assets檢視上同時更新多個資產的預先定義標準中繼資料欄位集。
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 692ff4fbb5b7e703f727d6e20d87c4fc0abdb350
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 在Assets檢視中編輯大量中繼資料{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

Assets檢視中的&#x200B;**大量中繼資料編輯**&#x200B;功能可讓使用者同時編輯多個資產檔案的預定義標準中繼資料欄位集。 選取多個資產並一次大量更新其預先定義的標準中繼資料集，而非針對每個資產個別更新這些標準中繼資料。 此功能可提升大量資產標準中繼資料屬性的效率、一致性和準確性，進而改善資產搜尋能力及組織架構。

## 大量編輯資產中繼資料 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

執行這些步驟，一次大量編輯多個資產的中繼資料：

1. 在Assets檢視中，按一下&#x200B;**Assets**。
1. 瀏覽特定資產，或使用搜尋列中的關鍵字進行搜尋。
1. 選取資產，然後從頂端功能表按一下&#x200B;**大量中繼資料編輯**。
   ![大量中繼資料 — 編輯](/help/assets/assets/bulk-metadata-edit1.png)
1. 在「編輯中繼資料」頁面上，編輯&#x200B;**屬性**&#x200B;面板中的下列欄位：
   * **狀態：**&#x200B;選取所選資產的狀態。
   * **到期日：**&#x200B;設定資產不再有效或不再需要的日期。
   * **作者：**&#x200B;請指定作者名稱。
   * **關鍵字：**&#x200B;新增提供資產相關高階資訊的特定辭彙或文字字串，以增強其發現能力。 新增關鍵字，然後按Enter鍵或返回鍵以新增其他關鍵字至清單。
   * **標籤：**&#x200B;按一下![標籤圖示](/help/assets/assets/tags-icon.svg)從可用選項中選取標籤。 標籤提供有關資產的更具體資訊，並增強其可發現性。 已套用至所選資產的標籤會顯示在&#x200B;**屬性**&#x200B;面板中。 如果您找不到相關標籤，請建立這些標籤，並將其指派給選取的資產。 請參閱[在Assets檢視中管理標籤](/help/assets/tagging-management-assets-view.md)，以取得關於建立和指派標籤給資產的詳細資訊。
   * 按一下「儲存」****，將上述中繼資料更新套用至選取的資產。 儲存後，會附加關鍵字和標籤，而狀態、到期日和作者的更新詳細資訊會覆寫其現有詳細資訊。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >您可以一次編輯100個資產的中繼資料。

若要檢視已套用至資產的中繼資料更新內容，請瀏覽至資產詳細資料頁面（選取資產，然後按一下&#x200B;**詳細資料**），然後按一下![](/help/assets/assets/info-icon-solid-black.svg)，在&#x200B;**資訊**&#x200B;面板中檢視資產的中繼資料。

>[!NOTE]
>
>**狀態**、**到期日**、**作者**、**關鍵字**&#x200B;和&#x200B;**標籤**&#x200B;是可用於大量中繼資料編輯的標準中繼資料屬性，無論資料夾特定的中繼資料為何。 只有當這些中繼資料屬性包含在套用至資產資料夾的中繼資料表單中時，才會顯示在資產詳細資訊頁面上。 如果在資產詳細資訊頁面上找不到這些標準中繼資料屬性，請編輯資產資料夾的中繼資料表單以包含這些屬性。 請參閱Assets檢視中的[中繼資料](/help/assets/metadata-assets-view.md)，瞭解如何建立或編輯中繼資料表單，並將其套用至資料夾。
