---
title: 傳遞 API
description: 瞭解如何使用傳送API。
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 9f7164e99abb6fce3b1bbc6401234996bcd43889
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 5%

---

# 傳送API {#delivery-apis}

Experience Manager資產存放庫中所有可用的[已核准資產](approve-assets.md)都可以進行[搜尋](search-assets-api.md)，然後使用傳遞URL傳遞至整合式下游應用程式。

對 DAM 中已核准資產所做的任何變更 (包括版本更新和中繼資料修改)，都會自動反映在傳遞 URL 中。由於透過CDN為資產傳送設定的短存留時間(TTL)值為10分鐘，因此在10分鐘內，所有編寫和發佈介面中都會顯示更新。

下圖說明可用的傳送URL：

![傳遞API](assets/delivery-url.png)

下表說明各種可用傳送API的使用情況：

| 傳送API | 說明 |
|---|---|
| 以要求的輸出格式呈現資產的[網頁最佳化的二進位表示](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat) | 根據請求中傳送的資產ID，傳回請求輸出格式之資產的Web最佳化二進位表示法。 此外，您可以定義各種影像修飾元，例如寬度、高度、旋轉、翻轉、品質、裁切、格式和[智慧型裁切](/help/assets/dynamic-media/image-profiles.md)。 如需支援的格式和影像修飾元，請參閱[API詳細資料](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat)。<br>Adobe建議對所有影像格式型別使用此API。 |
| [資產](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAsset)的Web最佳化二進位表示 | 套用預設到回應中傳回之資產的網頁最佳化二進位表示的便利API。 預設值包括標準JPEG/WEBP格式、品質=> 65和寬度=> 1024。 |
| [資產的原始已上傳二進位檔](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetOriginal) | 傳回資產最初上傳的二進位檔案。 Adobe建議針對檔案格式型別和SVG影像使用此API。 |
| [預先產生的資產轉譯，可在AEM Assets製作環境中使用](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetRendition) | 根據請求中傳送的資產ID和轉譯名稱，傳回AEM Assets製作環境中可用的資產轉譯位元串流。 |
| [資產中繼資料](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetMetadata) | 傳回與資產關聯的屬性，例如，標題、說明、CreateDate、ModifyDate等。 |
| 視訊資產的[播放器容器](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoPlayerDelivery) | 傳回視訊資產的播放器容器。 您可以將播放器內嵌至iframe HTML元素中，並播放影片。 |
| [播放資料清單為選取的輸出格式](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoManifestDelivery) | 以選取的輸出格式傳回指定視訊資產的播放資訊清單檔案。 您必須建置可透過HLS或DASH通訊協定自我調整資料流的自訂播放器，才能提取播放資訊清單檔案並播放視訊。 |

>[!IMPORTANT]
>
>您可以測試任何修飾元，但這通常無法透過實驗API取得。 例如 `</adobe/experimental/advancemodifiers-expires-YYYYMMDD/assets>`
>&#x200B;>按一下這裡以進一步瞭解如何使用[實驗API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis)和[修飾元完整清單](https://developer.adobe.com/experience-cloud/experience-manager-apis/)。

具備OpenAPI功能的Dynamic Media也支援長格式視訊。 影片可支援高達 50 GB 和 2 小時。

如需有關可用的Dynamic Media產品專案及其功能的資訊，請參閱[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。

>[!NOTE]
>
>DM Prime客戶可以使用基本影像修飾元，包括旋轉、裁切、翻轉、高度、寬度和品質。 智慧型影像不支援DM Prime客戶的AVIF。

## 傳送API端點 {#delivery-apis-endpoint}

API端點因每個傳送API而異。 例如，`Web-optimized binary representation of the asset in the requested output format` API的API端點是：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

傳遞網域的結構類似於Experience Manager作者環境的網域。 唯一的差異是以`author`取代字詞`delivery`。

`pXXXX`參考方案識別碼

`eYYYY`參考環境識別碼

如需詳細資訊，請參閱[API詳細資料](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#tag/Assets)。

## 傳送API要求方法 {#delivery-api-request-method}

GET

## 傳送API標頭 {#deliver-assets-api-header}

在傳送API標題中定義標題時，您必須提供下列詳細資料：

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

若要叫用傳遞API，`Authorization`詳細資料中需要IMS權杖才能傳遞受限制的資產。 IMS權杖是從技術帳戶中擷取。 請參閱[擷取AEM as a Cloud Service認證](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis)以建立新的技術帳戶。 請參閱[產生存取權杖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis)以產生IMS權杖，並在傳遞API要求標頭中正確使用它。


若要檢視要求範例、回應範例和回應代碼，請參閱[傳送API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat)。
