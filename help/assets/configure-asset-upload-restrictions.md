---
title: 設定資產上傳限制
description: 配置Adobe Experience Manager資產以限制用戶可以基於MIME類型上傳的資產類型。 它有助於防止意外上載不希望有的格式和惡意檔案。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 11%

---

# 設定資產上傳限制 {#configure-asset-upload-restrictions}

您可以配置Adobe Experience Manager資產，以限制用戶可以基於MIME類型上傳的資產類型。

>[!IMPORTANT]
>
>預設情況下，Experience Manager Assets允許用戶上載所有MIME類型的資產。 但是，您可以配置設定，以僅限於用戶上載特定MIME類型的檔案。

## 必備條件 {#prerequisites-asset-upload-restrictions}

您必須具有管理員權限才能配置資產上載限制。

## 對資產上載應用限制 {#apply-restrictions-asset-uploadsssssss}

配置 [!DNL Experience Manager] 要限制用戶上載特定MIME類型的檔案，請執行以下操作：

1. 導航到 **[!UICONTROL 工具>資產>資產配置]**。

1. 按一下 **[!UICONTROL 上載限制]**。

1. 按一下 **[!UICONTROL 添加]** 定義允許的MIME類型。

1. 在文本框中指定MIME類型。 您可以按一下 **[!UICONTROL 添加]** 再次指定更多允許的MIME類型。 也可以按一下 ![刪除表徵圖](assets/delete-icon.svg) 從清單中刪除任何MIME類型。

1. 按一下「**[!UICONTROL 儲存]**」。

**示例1:允許將所有映像和PDF檔案上載到Experience Manager Assets**

要允許將所有格式的影像和PDF檔案上載到Experience Manager Assets，請執行以下設定：

![資產上載限制](assets/asset-upload-restrictions.png)

`image/*` 因為MIME類型允許以所有格式上載影像。 `application/pdf` 因為MIME類型允許將PDF檔案上載到Experience Manager Assets。

如果嘗試上載未包含在允許的MIME類型清單中的檔案，Experience Manager Assets將顯示以下錯誤消息：

![受限檔案](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` 引用不包括在允許的MIME類型中的檔案名。

**示例2:允許將特定影像格式上載到Experience Manager Assets**

要將特定影像格式添加到允許的MIME類型並限制上載所有其他資產格式，請執行以下設定：

![資產限制](assets/asset-restrictions.png)

根據影像中描述的設定，可以將。JPG、.PNG和。GIF格式的影像上載到Experience Manager Assets。

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
