---
title: 在Assets檢視中編輯大量中繼資料
description: 瞭解如何在Assets檢視上同時編輯多個可用資產的中繼資料。
source-git-commit: 5778d0dac141174c1b950625057f920af0301a8b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在Assets檢視中編輯大量中繼資料{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

在Assets檢視UI中使用&#x200B;**大量中繼資料編輯**，您可以同時修改多個資產檔案的中繼資料。 您一次不會個別編輯每個資產的中繼資料，而是將變更套用至大量資產。 此功能可提升大量資產的中繼資料屬性的效率、一致性和準確性，進而改善資產搜尋能力和組織能力。

## 大量編輯資產中繼資料 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

執行這些步驟，一次大量編輯多個資產的中繼資料：

1. 在Assets檢視中，按一下&#x200B;**Assets**。
1. 瀏覽資產或在搜尋列中輸入相關關鍵字，以找出特定資產。
1. 選取多個資產，然後從頂端功能表按一下&#x200B;**大量中繼資料編輯**。
   ![大量中繼資料 — 編輯](/help/assets/assets/bulk-metadata-edit.png)
1. 在「編輯中繼資料」頁面上，編輯&#x200B;**屬性**&#x200B;面板中的下列欄位：
   * **狀態：**&#x200B;選取狀態以定義所選資產的可用性。
   * **到期日：**&#x200B;設定資產不再有效或不再需要的日期。
   * **作者：**&#x200B;請指定作者名稱。
   * **關鍵字：**新增可提供有關資產的高階資訊的字詞或文字字串，以增強其發現能力。 新增關鍵字，然後按Enter鍵或返回鍵以新增其他關鍵字至清單。
     <!-- * **Tags:** Click ![tags icon](/help/assets/assets/tags-icon.svg) to select tags from the available options. Tags provide more specific information about the assets and enhances their discoverability. Tags already applied to the selected assets are only displayed in the **Properties** panel. If you cannot find the relevant tags, create the tags and assign them to the selected assets. See [Manage tags in Assets view](/help/assets/tagging-management-assets-view.md) for details.-->
   * 按一下&#x200B;**儲存**&#x200B;以附加關鍵字，並<!-- Tags while-->覆寫狀態、到期日和作者的現有詳細資料。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties1.png)

     >[!NOTE]
     >
     >您可以一次編輯100個資產的中繼資料。

若要檢視套用至資產的中繼資料變更，請瀏覽至資產詳細資料頁面（選取資產，然後按一下&#x200B;**詳細資料**），然後按一下![](/help/assets/assets/info-icon-solid-black.svg)，在&#x200B;**資訊**&#x200B;面板中檢視資產的中繼資料。

>[!NOTE]
>
>狀態、到期日、作者和關鍵字<!-- and Tags-->是可用於大量中繼資料編輯的標準中繼資料屬性，無論檔案夾特定的中繼資料為何。 只有當這些中繼資料屬性包含在套用至資產資料夾的中繼資料表單中時，才會顯示在資產詳細資訊頁面上。  如果您在資產詳細資訊頁面上看不到這些中繼資料屬性，請編輯資產資料夾的中繼資料表單以包含它們。 請參閱Assets檢視中的[中繼資料](/help/assets/metadata-assets-view.md)，瞭解如何建立或編輯中繼資料表單，並將其套用至資料夾。


