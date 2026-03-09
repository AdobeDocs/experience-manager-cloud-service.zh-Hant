---
title: 管理 Content Hub 上的已授權資產
description: 瞭解如何將授權欄位新增至資產中繼資料表單、將授權中繼資料屬性套用至資產資料夾，以及核准具有授權的資產以供使用。
badgeSaas: label="AEM Assets" type="Positive" tooltip="適用於AEM Assets)。"
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

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

## 常見問題 {#faqs-manage-licensed-assets-content-hub}

### 在AEM Assets Content Hub上管理授權資產的用途為何？

在Content Hub上管理授權資產可讓管理員確保只能使用具有有效授權的已核准資產，同時在AEM作者環境中維持合規性和正確的中繼資料追蹤。

### 如何在Experience Manager as a Cloud Service中將授權欄位新增至資產屬性？

您可以編輯中繼資料表單，加入對應至`dc:license`屬性的新文字欄位，藉此將授權欄位新增至資產屬性。 然後，此欄位會出現在AEM Assets製作環境的資產屬性中。

### 如何將中繼資料表單套用至資產資料夾，以在資產屬性中包含授權欄位？

編輯中繼資料表單以包含授權欄位。 將此中繼資料表單套用至所需的資產資料夾，以確保新設定已納入該資料夾中的所有資產。

### 如何指定資產的授權詳細資料？

若要指定授權詳細資訊，請選取資產，按一下&#x200B;**詳細資料**&#x200B;以檢視其屬性，並在新增至中繼資料表單的授權欄位中輸入已核准資產授權的絕對路徑。

### 資產授權的Content Hub絕對路徑需要什麼格式？

Content Hub絕對路徑應遵循以下模式：/content/dam/（DAM存放庫中的資產資料夾階層）/(asset_name)。（檔案副檔名）。 例如，`/content/dam/teamA/projects/documents/file1.pdf`。

### 為何同時核准資產及其授權很重要，才能在AEM Assets Content Hub上使用？

核准資產及其授權可確保在AEM Assets Content Hub上只能使用已適當授權和授權的資產，以協助維護合規性和正確的使用權利。

### 在核准資產授權後，如何在AEM Assets Content Hub中提供資產？

在資產屬性中定義授權路徑後，核准資產並按一下儲存。 此動作會讓授權資產可在AEM Assets Content Hub中使用。

### 誰負責管理Content Hub中的授權資產？

管理員負責編輯中繼資料表單、將表單指派給資產資料夾，以及在Content Hub中核准資產及其授權。
