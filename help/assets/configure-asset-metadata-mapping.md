---
title: 設定Workfront和Experience Manager Assets之間的資產中繼資料對應
description: 在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您將資產從Workfront傳送至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 設定Adobe Workfront和Experience Manager Assets之間的資產中繼資料對應 {#asset-metadata-mapping-workfront-aem-assets}

您可以在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您將資產從Workfront傳送至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。

例如，如果您在將影像傳送至Experience Manager Assets時需要保留影像的中繼資料欄位，例如名稱、說明，以及影像在Workfront中屬於的專案，請設定這些欄位，並將這些欄位對應至Experience Manager Assets屬性。

**使用案例**

影像 `add-users-workfront.png` 存在於 `Metadata Syncs` 專案(在Adobe Workfront應用程式中)。 您必須使用下列中繼資料將該影像傳送至Experience Manager Assetsas a Cloud Service:

* 專案名稱

* 文檔名稱

* 文檔說明

## 必備條件 {#prerequisites}

* 管理員存取Workfront和Experience Manager Assetsas a Cloud Service應用程式。

* 整合 [Workfront和Experience Manager Assetsas a Cloud Service應用程式](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## 在Workfront中設定中繼資料對應 {#set-up-metadata-mapping}

要設定Workfront中「項目名稱」、「文檔名稱」和「文檔描述」欄位的元資料映射：

1. 按一下「主菜單」表徵圖 ![顯示菜單](assets/show-menu.svg) 位於Adobe Workfront應用程式的右上角，然後按一下 **[!UICONTROL 設定]**.

1. 選擇 **[!UICONTROL 檔案]** 在左側面板中，選取 **[!UICONTROL Experience Manager Assets]**.

1. 選取Experience Manager Assets整合，然後按一下 **[!UICONTROL 編輯]**.

1. 按一下 **[!UICONTROL 中繼資料]**. 在 **[!UICONTROL 資產]** 標籤 [!UICONTROL 專案] > [!UICONTROL 名稱] Workfront欄位至 `wm:projectName` Experience Manager Assets欄位。 如果您找不到完全相符的項目，Adobe建議尋找最佳相符項目，以對應Workfront和Experience Manager Assets欄位。 您可以避免對應不同資料類型的欄位。 例如，將日期Workfront欄位對應至說明資產欄位。
1. 對應 [!UICONTROL 檔案] > [!UICONTROL 名稱] Workfront欄位至 `wm:documentName` Experience Manager Assets欄位。

   ![Workfront中的對應](assets/workfront-metadata-mapping.png)

1. 對應 [!UICONTROL 檔案] > [!UICONTROL 說明] Workfront欄位至 `dc:description` Experience Manager Assets欄位。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 將影像從Workfront傳送至Experience Manager Assets {#send-image-workfront-assets}

若要將影像從Workfront傳送至Experience Manager Assets:

1. 按一下「主菜單」表徵圖 ![顯示菜單](assets/show-menu.svg) 位於Adobe Workfront應用程式的右上角，然後按一下 **[!UICONTROL 專案]**.

1. 按一下 **[!UICONTROL 新增專案]** 來建立新專案。

1. 按一下 **[!UICONTROL 檔案]** 選項，拖曳並選取您需要傳送至Experience Manager Assets的影像。

1. 按一下 **[!UICONTROL 傳送至]**，然後選擇Experience Manager Assets Essentials整合名稱。

   ![傳送至AEM](assets/send-to-aem.png)

1. 選擇資產的目標資料夾，然後按一下 **[!UICONTROL 選擇資料夾]**.

1. 按一下「**[!UICONTROL 儲存]**」。

## 在Experience Manageras a Cloud Service中設定資產中繼資料對應 {#metadata-mapping-aem}

之後 [在Adobe Workfront中設定資產中繼資料對應](#set-up-metadata-mapping)，您必須在Experience Manager Assetsas a Cloud Service應用程式中使用相同的對應，才能顯示影像的適當中繼資料結果。

中繼資料對應是使用Experience Manager Assets中的中繼資料結構來執行。 您可以編輯新增或現有的中繼資料結構表單。 中繼資料結構表單包含索引標籤和索引標籤內的表單項目。 您可以將這些表單項目對應/設定至CRX存放庫中中繼資料節點內的欄位。 您可以將索引標籤或表單項目新增至中繼資料結構表單。 如需詳細資訊，請參閱 [中繼資料結構](metadata-schemas.md).

若要在Experience Manager Assets as a Cloud Service中使用新的中繼資料表單來設定中繼資料對應：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.

1. 按一下 **[!UICONTROL 建立]** 的上界。 在對話方塊中，提供結構表單的標題，然後按一下 **[!UICONTROL 建立]** 以完成表單建立程式。

1. 選擇架構表單並按一下 **[!UICONTROL 編輯]**.

1. （選用）在中繼資料結構表單編輯器上，按一下 `+` 為Workfront欄位建立新索引標籤。

1. 按一下 **[!UICONTROL 建置表單]** 標籤並拖曳 **[!UICONTROL 單行文字]** 元件。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Project Name` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/wm:projectName` 在 **[!UICONTROL 對應至屬性]** 欄位。 建議您使用下列範本，以定義Experience Manager資產中的欄位對應：
      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront中設定對應時，您已對應 `wm:projectName` Experience Manager Assets欄位至專案>命名Workfront欄位。

      `wm` 指的名稱空間名稱和 `projectName` 是指屬性標題。 使用 `namespace:propertyTitle` 格式來定義中繼資料欄位對應。

      ![傳送至AEM](assets/metadata-schema-mapping.png)

1. 按一下 **[!UICONTROL 建置表單]** 標籤並拖曳 **[!UICONTROL 單行文字]** 元件。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Document Name` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/wm:documentName` 在 **[!UICONTROL 對應至屬性]** 欄位。
在Workfront中設定對應時，您已對應 `wm:documentName` Experience Manager Assets欄位至「檔案>命名Workfront」欄位。

1. 按一下 **[!UICONTROL 建置表單]** 標籤並拖曳 **[!UICONTROL 多行文本]** 元件。 按一下表單中的元件。 在 **[!UICONTROL 建置表單]** 標籤：

   1. 指定 `Document Description` 在 **[!UICONTROL 欄位標籤]** 欄位。

   1. 指定 `./jcr:content/metadata/dc:description` 在 **[!UICONTROL 對應至屬性]** 欄位。
在Workfront中設定對應時，您已對應 `dc:description` Experience Manager Assets欄位至「檔案>說明Workfront」欄位。

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 將中繼資料設定套用至影像資料夾 {#apply-metadata-settings-image-folder}

在Experience Manageras a Cloud Service應用程式中設定中繼資料設定後，將這些設定套用至 [包含從Workfront應用程式傳送之影像的資料夾](#send-image-workfront-assets).

要將元資料設定應用到影像資料夾：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.

1. 從可用清單中選取中繼資料結構，然後按一下 **[!UICONTROL 應用於資料夾]**.

1. 選擇要到的目標資料夾 [影像會從Adobe Workfront應用程式傳送](#send-image-workfront-assets) 按一下 **[!UICONTROL 套用]**.

您可以導覽至Experience Manager Assets中的影像，並檢視與影像相關聯的中繼資料。 選取影像，然後按一下 **[!UICONTROL 屬性]** 檢視影像中繼資料。
