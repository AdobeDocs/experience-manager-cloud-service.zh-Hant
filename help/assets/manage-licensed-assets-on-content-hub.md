---
title: 管理 Content Hub 上的已授權資產
description: 瞭解如何將授權欄位新增至資產中繼資料表單、將授權中繼資料屬性套用至資產資料夾，以及核准具有授權的資產以供使用。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 6%

---

# 管理 Content Hub 上的已授權資產 {#manage-licensed-assets-on-content-hub}

以管理員身分，編輯中繼資料表單以包含資產授權欄位，使其顯示在AEM作者環境的資產屬性中。 接著，您可以核准資產及其授權，讓資產獲得授權並可在Content Hub上使用。

執行以下步驟：

1. 編輯中繼資料表單以包含新文字欄位以包含授權詳細資料。 將文字欄位對應至`dc:license`屬性。 如需有關如何將欄位新增至中繼資料表單及定義屬性的詳細資訊，請參閱[設定中繼資料Forms](/help/assets/metadata-assets-view.md#metadata-forms)。
   ![zip解壓縮](/help/assets/assets/metadata-form-edit.png)
1. 將中繼資料表單套用至資產資料夾，以套用步驟1整合的設定。 有關如何將中繼資料表單指派至資產資料夾的資訊，請參閱[將中繼資料表單指派至資料夾](/help/assets/metadata-assets-view.md#metadata-forms)。
1. [核准授權的PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. 選取該資產，然後按一下&#x200B;**詳細資料**&#x200B;以檢視其屬性。 在步驟1中新增的授權欄位中，為已在步驟3中核准或先前已核准的資產授權定義絕對路徑。 Content Hub絕對路徑遵循此標準模式： `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`。 例如， /content/dam/teamA/projects/documents/file1.pdf
   ![絕對路徑](/help/assets/assets/absolute-path.png)
1. 核准資產使其可在Content Hub中使用，然後按一下&#x200B;**儲存**。 如需如何核准資產的詳細資訊，請參閱[設定資產狀態](/help/assets/manage-organize-assets-view.md#set-asset-status)。
