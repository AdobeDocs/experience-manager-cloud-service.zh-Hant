---
title: 管理數位資產
description: 瞭解如何偵測重複的資產
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
source-git-commit: bd0981b262f645653723f1b35d871808506d47ba
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# 偵測重複的資產 {#detect-duplicate-assets}

如果DAM使用者上傳一個或多個已存在於存放庫中的資產， [!DNL Experience Manager] 會偵測重複並通知使用者。 根據預設，重複資料偵測會停用，因為這會根據存放庫的大小和上傳的資產數量產生效能影響。

若要啟用功能：

1. 瀏覽至 **[!UICONTROL 「工具>資產>資產設定」]**.

1. 按一下 **[!UICONTROL 資產重複偵測器]**.

1. 在 [!UICONTROL 資產重複偵測器頁面]，按一下 **[!UICONTROL 已啟用]**.

   `dam:sha1` 「偵測中繼資料」欄位的值可確保即使檔案名稱不同，仍會偵測到重複的資產。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/asset-duplication-detector.png)

>[!NOTE]
>
>如果您已使用設定重複偵測器 `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` 設定檔案（OSGi設定），您可繼續使用，但Adobe建議使用新方法。


啟用後，Experience Manager會將重複資產的通知傳送到Experience Manager收件匣。 這是多個重複專案的彙總結果。 使用者可以選擇根據結果移除資產。

![重複資產的收件匣通知](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>當您將資產上傳到存放庫時，Experience Manager會偵測重複並通知您前100個重複資產的情況。

