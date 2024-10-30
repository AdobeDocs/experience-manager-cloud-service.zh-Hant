---
title: 在Content Hub上管理授權的Assets
description: 瞭解各種中繼資料管理和編輯方法
source-git-commit: 541d5819e19c67eb3f961e41000106178bff66de
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 1%

---


# 在Content Hub上管理授權的Assets {#manage-licensed-assets-on-content-hub}

以管理員身分，編輯中繼資料表單以包含資產授權欄位，使其顯示在AEM作者環境的資產屬性中。 接著，您可以核准資產及其授權，讓資產獲得授權並可在Content Hub上使用。

執行以下步驟：

1. 編輯中繼資料表單以包含新文字欄位以包含授權詳細資料。 將文字欄位對應至`dc:license`屬性。 如需有關如何將欄位新增至中繼資料表單及定義屬性的詳細資訊，請參閱[設定中繼資料Forms](/help/assets/metadata-assets-view.md#metadata-forms)。
   ![zip解壓縮](/help/assets/assets/metadata-form-edit.png)
1. 將中繼資料表單套用至資產資料夾，以套用步驟1整合的設定。 有關如何將中繼資料表單指派至資產資料夾的資訊，請參閱[將中繼資料表單指派至資料夾](/help/assets/metadata-assets-view.md#metadata-forms)。
1. [核准授權PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. 選取該資產，然後按一下&#x200B;**詳細資料**&#x200B;以檢視其屬性。 在步驟1中新增的授權欄位中，為已在步驟3中核准或先前已核准的資產授權定義絕對路徑。 Content Hub絕對路徑遵循此標準模式： `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`。 例如， /content/dam/teamA/projects/documents/file1.pdf
   ![絕對路徑](/help/assets/assets/absolute-path.png)


