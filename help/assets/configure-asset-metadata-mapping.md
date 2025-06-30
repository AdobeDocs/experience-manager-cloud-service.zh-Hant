---
title: 設定Workfront和Experience Manager Assets之間的資產中繼資料對應
description: 在Adobe Workfront和Experience Manager as a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您從Workfront傳送資產至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
feature: Metadata, Workfront Integrations and Apps
role: User, Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# 設定Adobe Workfront和Experience Manager Assets之間的資產中繼資料對應 {#asset-metadata-mapping-workfront-aem-assets}

您可以在Adobe Workfront和Experience Manager as a Cloud Service應用程式之間對應資產中繼資料欄位。 對應中繼資料欄位後，當您從Workfront傳送資產至Experience Manager Assets時，可以在Experience Manager Assets中檢視對應的資產中繼資料。

例如，如果您需要保留影像的中繼資料欄位，例如名稱、說明，以及影像在Workfront中屬於的專案，則請在將影像傳送至Experience Manager Assets時設定這些欄位，並將其對應至Experience Manager Assets屬性。

**使用案例**

在Adobe Workfront應用程式的`Metadata Syncs`專案中存在影像`add-users-workfront.png`。 您必須將該影像傳送至Experience Manager Assets as a Cloud Service，並具備下列中繼資料：

* 專案名稱

* 檔名稱

* 檔案說明

## 先決條件 {#prerequisites}

* Workfront和Experience Manager Assets as a Cloud Service應用程式的管理員存取權。

* [Workfront與Experience Manager Assets as a Cloud Service應用程式](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&_LANG=enus)之間的整合。

## 在Workfront中設定中繼資料對應 {#set-up-metadata-mapping}

若要為Workfront中的「專案名稱」、「檔名稱」和「檔案描述」欄位設定中繼資料對應：

1. 按一下Adobe Workfront應用程式右上角可用的主要功能表圖示![顯示功能表](assets/show-menu.svg)，然後按一下&#x200B;**[!UICONTROL 設定]**。

1. 在左側面板中選取&#x200B;**[!UICONTROL 檔案]**，然後選取&#x200B;**[!UICONTROL Experience Manager Assets]**。

1. 選取Experience Manager Assets整合，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 按一下&#x200B;**[!UICONTROL 中繼資料]**。 在&#x200B;**[!UICONTROL Assets]**&#x200B;索引標籤中，將[!UICONTROL 專案] > [!UICONTROL 名稱] Workfront欄位對應到`wm:projectName` Experience Manager Assets欄位。 如果您找不到完全相符的專案，Adobe建議您尋找能對應至Workfront和Experience Manager Assets欄位的最佳相符專案。 您可以避免對應不同資料型別的欄位。 例如，將日期Workfront欄位對應至說明Assets欄位。
1. 將[!UICONTROL 檔案] > [!UICONTROL 名稱] Workfront欄位對應到`wm:documentName` Experience Manager Assets欄位。

   在Workfront中進行![對應](assets/workfront-metadata-mapping.png)

1. 將[!UICONTROL Document] > [!UICONTROL Description] Workfront欄位對應至`dc:description` Experience Manager Assets欄位。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 將影像從Workfront傳送至Experience Manager Assets {#send-image-workfront-assets}

若要將影像從Workfront傳送至Experience Manager Assets：

1. 按一下Adobe Workfront應用程式右上角可用的主功能表圖示![顯示功能表](assets/show-menu.svg)，然後按一下&#x200B;**[!UICONTROL 專案]**。

1. 按一下&#x200B;**[!UICONTROL 新增專案]**&#x200B;以建立專案。

1. 按一下左側窗格中可用的&#x200B;**[!UICONTROL 檔案]**&#x200B;選項，拖曳，然後選取您需要傳送至Experience Manager Assets的影像。

1. 按一下&#x200B;**[!UICONTROL 傳送至]**，然後選擇Experience Manager Assets Essentials整合名稱。

   ![傳送至AEM](assets/send-to-aem.png)

1. 選擇資產的目的地資料夾，然後按一下&#x200B;**[!UICONTROL 選取資料夾]**。

1. 按一下「**[!UICONTROL 儲存]**」。

## 在Experience Manager as a Cloud Service中設定資產中繼資料對應 {#metadata-mapping-aem}

在[在Adobe Workfront](#set-up-metadata-mapping)中設定資產中繼資料對應後，您必須在Experience Manager Assets as a Cloud Service應用程式中使用相同的對應，以顯示影像的適當中繼資料結果。

在Experience Manager Assets中使用中繼資料結構描述來執行中繼資料對應。 您可以編輯新新增或現有的中繼資料結構表單。 中繼資料結構表單包含索引標籤以及索引標籤內的表單專案。 您可以將這些表單專案對應/設定至CRX存放庫中繼資料節點內的欄位。 您可以將索引標籤或表單專案新增到中繼資料結構表單。 如需詳細資訊，請參閱[中繼資料結構](metadata-schemas.md)。

若要在Experience Manager Assets as a Cloud Service中使用新的中繼資料表單來設定中繼資料對應：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。

1. 從工具列按一下&#x200B;**[!UICONTROL 「建立]**」。 在對話方塊中，提供結構表單的標題，然後按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以完成表單建立程式。

1. 選取結構表單並按一下&#x200B;**[!UICONTROL 編輯]**。

1. （選擇性）在中繼資料結構表單編輯器上，按一下「`+`」以建立Workfront欄位的索引標籤。

1. 按一下&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 單行文字]**&#x200B;元件拖曳至表單。 按一下表單中的元件。 在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中：

   1. 在&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;欄位中指定`Project Name`。

   1. 在&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;欄位中指定`./jcr:content/metadata/wm:projectName`。 建議先使用以下範本，在Experience Manger Assets中定義欄位對應：

      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront中設定對應時，您將`wm:projectName`個Experience Manager Assets欄位對應至專案>命名Workfront欄位。

      `wm`參考名稱空間名稱，`projectName`參考屬性標題。 使用`namespace:propertyTitle`格式來定義中繼資料欄位對應。

      ![傳送至AEM](assets/metadata-schema-mapping.png)

1. 按一下&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 單行文字]**&#x200B;元件拖曳至表單。 按一下表單中的元件。 在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中：

   1. 在&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;欄位中指定`Document Name`。

   1. 在&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;欄位中指定`./jcr:content/metadata/wm:documentName`。
在Workfront中設定對應時，您將`wm:documentName`個Experience Manager Assets欄位對應至檔案>命名Workfront欄位。

1. 按一下&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤，然後將&#x200B;**[!UICONTROL 多行文字]**&#x200B;元件拖曳至表單。 按一下表單中的元件。 在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中：

   1. 在&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;欄位中指定`Document Description`。

   1. 在&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;欄位中指定`./jcr:content/metadata/dc:description`。
在Workfront中設定對應時，您將`dc:description`個Experience Manager Assets欄位對應至檔案>說明Workfront欄位。

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 套用中繼資料設定至影像資料夾 {#apply-metadata-settings-image-folder}

在Experience Manager as a Cloud Service應用程式中設定中繼資料設定後，將這些設定套用至包含從Workfront應用程式[&#128279;](#send-image-workfront-assets)傳送之影像的資料夾。

若要將中繼資料設定套用至影像資料夾：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。

1. 從可用清單中選取中繼資料結構描述，然後按一下&#x200B;**[!UICONTROL 套用至資料夾]**。

1. 選取從Adobe Workfront應用程式[&#128279;](#send-image-workfront-assets)傳送影像的目標資料夾，然後按一下&#x200B;**[!UICONTROL 套用]**。

您可以導覽至Experience Manager Assets中的影像，並檢視與影像相關聯的中繼資料。 選取影像並按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;以檢視影像中繼資料。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
