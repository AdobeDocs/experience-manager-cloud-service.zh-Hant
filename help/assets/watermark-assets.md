---
title: 為資產加上浮水印
description: 為您的數位資產加上浮水印。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: cf6cfb38a43004c8ac0c1d1e99153335a47860a8
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# 為您的資產加上浮水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 可讓您為影像新增數位浮水印。 [!DNL Assets] 支援將影像作為浮水印套用至其他影像檔案。 水印可以幫助用戶驗證資產的真實性和版權所有權。 此外，水印可用於指示文檔的狀態，如機密、草稿、有效性等。

配置 [!DNL Experience Manager] 為資產加上浮水印：

1. PNG檔案會套用為浮水印。 將此檔案上傳至您的DAM存放庫。

1. 導覽至 **[!UICONTROL 工具>資產>資產設定]**.

1. 按一下 **[!UICONTROL 系統水印配置檔案]**.

1. 在 [!UICONTROL 系統水印配置檔案頁]，請在步驟1中指定上傳至DAM存放庫的影像路徑。

1. 在 **[!UICONTROL 規模]** 欄位。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果已配置系統水印配置檔案，則使用 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 設定檔案（OSGi設定），您可以繼續使用，但Adobe建議使用新方法。


1. [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 利用資產微服務來套用浮水印。

   ![資產處理設定檔以建立浮水印](assets/watermark-processing-profile.png)

   請確定您啟用 **[!UICONTROL 浮水印]** 在建立處理設定檔時切換。

1. [將處理設定檔套用至資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 建立加水印的資產。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用單一設定為所有資產加上浮水印。 水印僅使用一幅影像，其寬度是固定的。
* 您可以將浮水印置於中心，而不需進行拼貼。
* 不支援基於文本的水印。

>[!MORELIKETHIS]
>
>* [資產微服務概述](/help/assets/asset-microservices-overview.md).
>* [使用資產微服務和處理設定檔](/help/assets/asset-microservices-configure-and-use.md).

