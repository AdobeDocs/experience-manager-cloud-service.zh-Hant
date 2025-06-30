---
title: 在 [!DNL Assets View]中大量中繼資料編輯
description: 瞭解如何為[DNL！提供的多個資產更新預先定義的標準中繼資料欄位集 同時Assets檢視]。
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 在[!DNL Assets View]中大量中繼資料編輯{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

[!DNL Assets View]的&#x200B;**[!DNL Bulk Metadata Edit]**&#x200B;功能可讓您同時編輯多個資產檔案的預定義標準中繼資料欄位集。 選取多個資產並一次大量更新其預先定義的標準中繼資料集，而非針對每個資產個別更新這些標準中繼資料。 此功能可跨大型資產集維持標準中繼資料屬性集的效率、一致性和準確性，並改善這些資產的可搜尋性和組織性。

## 大量編輯資產中繼資料 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

執行這些步驟，一次大量編輯多個資產的中繼資料：

1. 導覽至&#x200B;**[!DNL Assets View]**&#x200B;並按一下&#x200B;**[!UICONTROL Assets]**。
1. 瀏覽特定資產，或使用搜尋列中的關鍵字進行搜尋。
1. 選取資產，然後從頂端功能表按一下&#x200B;**[!UICONTROL 大量中繼資料編輯]**。
   ![大量中繼資料 — 編輯](/help/assets/assets/bulk-metadata-edit1.png)
1. 在[!UICONTROL 編輯中繼資料頁面]上，編輯&#x200B;**[!UICONTROL 屬性]**&#x200B;面板中的下列欄位：
   * **[!UICONTROL 狀態]：**&#x200B;選取所選資產的狀態。
   * **[!UICONTROL 到期日]：**&#x200B;設定資產不再有效或不再需要的日期。
   * **[!UICONTROL 作者]：**&#x200B;請指定作者名稱。
   * **[!UICONTROL 關鍵字]：**&#x200B;新增提供資產相關高階資訊的特定辭彙或文字字串，以提升其發現能力。 新增關鍵字，然後按&#x200B;**Enter**&#x200B;或&#x200B;**return**&#x200B;將另一個關鍵字新增到清單中。
   * **[!UICONTROL 標籤]：**&#x200B;按一下![大量中繼資料編輯](/help/assets/assets/tags-icon.svg)，從可用選項中選取標籤。 標籤提供有關資產的更具體資訊，並增強其可發現性。 已套用至所選資產的標籤會顯示在&#x200B;**[!UICONTROL 屬性]**&#x200B;面板中。 如果您找不到相關標籤，請建立這些標籤，並將其指派給選取的資產。 如需建立標籤並將標籤指派給資產的詳細資訊，請參閱[管理 [!DNL Assets view]](/help/assets/tagging-management-assets-view.md)中的標籤。
   * 按一下「儲存」****，將上述中繼資料更新套用至選取的資產。 儲存後，會附加&#x200B;**[!UICONTROL 關鍵字]**&#x200B;和&#x200B;**[!UICONTROL 標籤]**，而&#x200B;**[!UICONTROL 狀態]**、**[!UICONTROL 到期日]**&#x200B;和&#x200B;**[!UICONTROL 作者]**的更新詳細資料會覆寫其現有的詳細資料。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >您可以一次編輯100個資產的中繼資料。

若要檢視套用至資產的中繼資料更新，請瀏覽至[!DNL asset details page] （選取資產，然後按一下&#x200B;**[!UICONTROL 詳細資料]**），然後按一下![大量中繼資料編輯](/help/assets/assets/info-icon-solid-black.svg)，以在&#x200B;**[!UICONTROL 資訊]**&#x200B;面板中檢視資產的中繼資料。

>[!NOTE]
>
>**[!UICONTROL 狀態]**、**[!UICONTROL 到期日]**、**[!UICONTROL 作者]**、**[!UICONTROL 關鍵字]**&#x200B;和&#x200B;**[!UICONTROL 標籤]**&#x200B;是可用於大量中繼資料編輯的標準中繼資料屬性，無論資料夾特定的中繼資料為何。 只有當這些中繼資料屬性包含在套用至資產資料夾的中繼資料表單中時，它們才會顯示在[!UICONTROL 資產詳細資料頁面]上。 如果您在[!UICONTROL 資產詳細資料頁面]上找不到這些標準中繼資料屬性，請編輯資產資料夾的中繼資料表單以包含這些屬性。 請參閱 [!DNL Assets View]](/help/assets/metadata-assets-view.md)中的[中繼資料，瞭解如何建立或編輯中繼資料表單，並將其套用至資料夾。
