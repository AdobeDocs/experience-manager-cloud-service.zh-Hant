---
title: 偵測 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]的重複資產
description: 瞭解如何偵測重複的資產
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 14%

---


# 偵測重複資產 {#detect-duplicate-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

如果DAM使用者上傳一個或多個已存在於存放庫中的資產，[!DNL Experience Manager]會偵測重複並通知使用者。 根據預設，重複資料偵測會停用，因為這會根據存放庫的大小和上傳的資產數量產生效能影響。

若要啟用功能：

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets > Assets設定]**。

1. 按一下&#x200B;**[!UICONTROL 資產重複偵測器]**。

1. 在[!UICONTROL 資產重複偵測器頁面]上，按一下&#x200B;**[!UICONTROL 已啟用]**。

   「偵測中繼資料」欄位的`dam:sha1`值可確保即使檔案名稱不同，仍會偵測到重複的資產。

1. 按一下「**[!UICONTROL 儲存]**」。

   ![資產重複偵測器](assets/asset-duplication-detector.png)

>[!NOTE]
>
>如果您已使用`/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json`組態檔（OSGi組態）設定複製偵測器，則可以繼續使用，不過Adobe建議使用新的方法。


啟用後，Experience Manager會將重複資產的通知傳送到Experience Manager收件匣。 這是多個重複專案的彙總結果。 使用者可以選擇根據結果移除資產。

![重複資產的收件匣通知](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>當您將資產上傳到存放庫時，Experience Manager會偵測重複並通知您前100個重複資產的相關資訊。
