---
title: 如何在AEM中為資產加上浮水印？
description: 瞭解如何在AEM中為資產新增數位浮水印。 浮水印可協助使用者驗證資產的真實性和版權所有權。
contentOwner: AG
feature: Asset Management,Publishing
role: User, Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 16%

---

# 為您的資產加上浮水印 {#watermark-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets]可讓您新增數位浮水印至影像和視訊。 [!DNL Assets]支援將影像作為浮水印套用至其他影像檔案。 浮水印可協助使用者驗證資產的真實性和版權所有權。 此外，浮水印可用於表示檔案的狀態，如機密、草稿、有效性等。

若要設定[!DNL Experience Manager]為資產加上浮水印：

1. PNG檔案會套用為浮水印。 將此檔案上傳到您的DAM存放庫。

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets > Assets設定]**。

1. 按一下&#x200B;**[!UICONTROL 系統浮水印設定檔]**。

1. 在[!UICONTROL 系統浮水印設定檔頁面]上，指定在步驟1中上傳至DAM存放庫的影像路徑。

1. 在&#x200B;**[!UICONTROL 比例]**&#x200B;欄位中，指定相對於轉譯寬度的浮水印比例，範圍從0.0到1.0。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果您已使用`com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json`組態檔（OSGi組態）設定系統浮水印設定檔，則可以繼續使用，不過Adobe建議使用新的方法。


1. [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile)以使用資產微服務來套用浮水印。

   ![用來建立浮水印的資產處理設定檔](assets/watermark-processing-profile.png)

   在建立處理設定檔時，請確定您已啟用&#x200B;**[!UICONTROL 浮水印]**&#x200B;切換。

1. [將處理設定檔套用至資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles)以建立加注水印。

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
>* [資產微服務總覽](/help/assets/asset-microservices-overview.md)。
>* [使用資產微服務來處理設定檔](/help/assets/asset-microservices-configure-and-use.md)。
