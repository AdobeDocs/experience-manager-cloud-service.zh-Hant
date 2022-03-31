---
title: 加水印
description: 將水印添加到數字資產。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: cf6cfb38a43004c8ac0c1d1e99153335a47860a8
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# 加水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 允許您向影像添加數字水印。 [!DNL Assets] 支援將影像作為水印應用於其他影像檔案。 水印可以幫助用戶驗證資產的真實性和版權所有權。 此外，水印可以用於表示文檔的狀態，如機密、草稿、有效性等。

配置 [!DNL Experience Manager] 到水印資產：

1. 將PNG檔案應用為水印。 將此檔案上載到DAM儲存庫。

1. 導航到 **[!UICONTROL 工具>資產>資產配置]**。

1. 按一下 **[!UICONTROL 系統水印配置檔案]**。

1. 在 [!UICONTROL 「系統水印配置檔案」頁]，在步驟1中指定上載到DAM儲存庫的映像路徑。

1. 在 **[!UICONTROL 縮放]** 的子菜單。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果已使用 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 配置檔案（OSGi配置），您可以繼續使用它，但是，Adobe建議使用新方法。


1. [建立處理配置檔案](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 利用資產微服務來應用水印。

   ![用於建立水印的資產處理配置檔案](assets/watermark-processing-profile.png)

   確保啟用 **[!UICONTROL 水印]** 建立處理配置檔案時切換。

1. [將處理配置檔案應用到資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 建立帶水印的資產。

## 提示和限制 {#tips-limitations-bestpractices}

* 可以使用單個配置來對所有資產進行水印。 只有一幅影像用於水印，其寬度固定。
* 可以將水印放在中心，而不進行平鋪。
* 不支援基於文本的水印。

>[!MORELIKETHIS]
>
>* [資產微服務概述](/help/assets/asset-microservices-overview.md)。
>* [將資產微服務與處理配置檔案一起使用](/help/assets/asset-microservices-configure-and-use.md)。

