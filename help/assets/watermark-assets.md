---
title: 為資產加上浮水印
description: 為您的數位資產加上浮水印。
contentOwner: AG
feature: 資產管理，發佈
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 為您的資產加上浮水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 可讓您為影像新增數位浮水印。[!DNL Assets] 支援將影像作為浮水印套用至其他影像檔案。水印可以幫助用戶驗證資產的真實性和版權所有權。 此外，水印可用於指示文檔的狀態，如機密、草稿、有效性等。

若要設定[!DNL Experience Manager]為資產加上浮水印，請遵循下列步驟：

1. PNG檔案會套用為浮水印。 在您的DAM存放庫中上傳此檔案。

1. 存取與您環境相關聯的[!DNL Cloud Manager] Git存放庫。 提交儲存庫中名為`com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json`的檔案，其中包含以下內容。 有關說明，請參閱[如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)中配置OSGi。

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [建立處理設](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 定檔，以運用資產微服務套用浮水印。

   ![資產處理設定檔以建立浮水印](assets/watermark-processing-profile.png)

1. [將處理設定檔套用至資料夾，](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 以建立加上浮水印的資產。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用單一設定為所有資產加上浮水印。 水印僅使用一幅影像，其寬度是固定的。
* 您可以將浮水印置於中心，而不需進行拼貼。
* 不支援基於文本的水印。

>[!MORELIKETHIS]
>
>* [資產微服務概述](/help/assets/asset-microservices-overview.md)。
>* [搭配處理設定檔使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)。

