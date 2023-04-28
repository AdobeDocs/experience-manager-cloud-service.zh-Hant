---
title: 設定資產上傳限制
description: 設定Adobe Experience Manager Assets以根據MIME類型限制使用者可上傳的資產類型。 它有助於防止意外上傳不想要的格式和惡意檔案。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 8%

---

# 設定資產上傳限制 {#configure-asset-upload-restrictions}

您可以設定Adobe Experience Manager Assets，以根據MIME類型限制使用者可上傳的資產類型。

>[!IMPORTANT]
>
>依預設，Experience Manager Assets可讓使用者上傳所有MIME類型的資產。 不過，您可以配置設定，限制使用者僅上傳特定MIME類型的檔案。

## 必備條件 {#prerequisites-asset-upload-restrictions}

您必須擁有管理員權限才能設定資產上傳限制。

## 對資產上傳套用限制 {#apply-restrictions-asset-uploadsssssss}

配置 [!DNL Experience Manager] 要限制用戶上載特定MIME類型的檔案，請執行以下操作：

1. 導覽至 **[!UICONTROL 工具>資產>資產設定]**.

1. 按一下 **[!UICONTROL 上傳限制]**.

1. 按一下 **[!UICONTROL 新增]** 定義允許的MIME類型。

1. 在文本框中指定MIME類型。 您可以按一下 **[!UICONTROL 新增]** 再次指定更多允許的MIME類型。 您也可以按一下 ![刪除圖示](assets/delete-icon.svg) 從清單中刪除任何MIME類型。

1. 按一下「**[!UICONTROL 儲存]**」。

**範例1:允許將所有影像和PDF檔案上傳至Experience Manager Assets**

若要允許將所有格式的影像和PDF檔案上傳至Experience Manager Assets，請執行下列設定：

![資產上傳限制](assets/asset-upload-restrictions.png)

`image/*` 因為MIME類型允許以所有格式上傳影像。 `application/pdf` 因為MIME類型允許將PDF檔案上傳至Experience Manager Assets。

如果您嘗試上傳未包含在允許的MIME類型清單中的檔案，Experience Manager Assets會顯示下列錯誤訊息：

![受限檔案](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` 是指未包含在允許的MIME類型中的檔案名。

**範例2:允許將特定影像格式上傳至Experience Manager Assets**

若要將特定影像格式新增至允許的MIME類型，並限制上傳所有其他資產格式，請執行下列設定：

![資產限制](assets/asset-restrictions.png)

根據影像中所示的設定，您可以將。JPG、.PNG和。GIF格式的影像上傳至Experience Manager Assets。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [Assets支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連線資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
