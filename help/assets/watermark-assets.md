---
title: 浮水印資產
description: 將浮水印新增至您的數位資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: af27295b618fb3909d43ed94a74148f7c4f59c10
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 浮水印您的資產 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 可讓您在影像中新增數位浮水印。 [!DNL Assets] 支援將影像套用為浮水印至其他影像檔案。 浮水印可協助使用者驗證資產的真實性和版權所有權。 此外，水印可用來表示檔案的狀態，如機密、草稿、有效性等。

若要設定浮 [!DNL Experience Manager] 水印資產，請遵循下列步驟：

1. PNG檔案會套用為浮水印。 將此檔案上傳至DAM儲存庫。

1. 訪問與 [!DNL Cloud Manager] 您的環境關聯的Git儲存庫。 提交具有以下 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 內容的儲存庫中名為的檔案。 如需指示，請 [參閱如何將OSGi [!DNL Experience Manager] 組態設為雲端服務](/help/implementing/deploying/configuring-osgi.md)。

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) ，以運用資產微服務來套用浮水印。

   ![建立浮水印的資產處理設定檔](assets/watermark-processing-profile.png)

1. [將處理設定檔套用至資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles) ，以建立浮水印資產。

## 提示與限制 {#tips-limitations-bestpractices}

* 您可以使用單一設定來浮水印所有資產。 水印只使用一張影像，其寬度固定。
* 您可以將浮水印置於中央，而不需拼貼。
* 不支援文字水印。

>[!MORELIKETHIS]
>
>* [資產微服務概觀](/help/assets/asset-microservices-overview.md)。
>* [將資產微服務與處理設定檔搭配使用](/help/assets/asset-microservices-configure-and-use.md)。

