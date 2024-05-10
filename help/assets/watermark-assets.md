---
title: 如何在AEM中為資產加上浮水印？
description: 瞭解如何在AEM中為資產新增數位浮水印。 浮水印可協助使用者驗證資產的真實性和版權所有權。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 16%

---

# 為您的資產加上浮水印 {#watermark-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets] 可讓您新增數位浮水印至影像。 [!DNL Assets] 支援將影像作為浮水印套用至其他影像檔案。 浮水印可協助使用者驗證資產的真實性和版權所有權。 此外，浮水印可用於表示檔案的狀態，如機密、草稿、有效性等。

進行設定 [!DNL Experience Manager] 若要為資產加上浮水印：

1. PNG檔案會套用為浮水印。 將此檔案上傳到您的DAM存放庫。

1. 瀏覽至 **[!UICONTROL 「工具>資產>資產設定」]**.

1. 按一下 **[!UICONTROL 系統浮水印設定檔]**.

1. 在 [!UICONTROL 系統浮水印設定檔頁面]，請指定在步驟1上傳至DAM存放庫的影像路徑。

1. 在「 」中指定相對於轉譯寬度的浮水印比例，範圍從0.0到1.0 **[!UICONTROL 縮放]** 欄位。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果您已使用設定系統浮水印設定檔 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 設定檔案（OSGi設定），您可繼續使用，但Adobe建議使用新方法。


1. [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 以使用資產微服務來套用浮水印。

   ![用於建立浮水印的資產處理設定檔](assets/watermark-processing-profile.png)

   請確定您已啟用 **[!UICONTROL 浮水印]** 在建立處理設定檔時切換。

1. [將處理設定檔套用至資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 以建立含浮水印的資產。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用單一設定來浮水印顯示所有資產。 只有一個影像用於浮水印，其寬度是固定的。
* 您可以將浮水印放在中央而不需要拼貼。
* 不支援文字式浮水印。

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

>[!MORELIKETHIS]
>
>* [資產微服務概覽](/help/assets/asset-microservices-overview.md).
>* [搭配處理設定檔使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).
