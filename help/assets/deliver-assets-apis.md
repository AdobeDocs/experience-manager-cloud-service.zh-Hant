---
title: 傳遞 API
description: 瞭解如何使用傳送API。
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 870f3f1826ea88cae0fc1fa31177bb9ffc8646f3
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 6%

---

# 傳送API {#delivery-apis}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media搭配OpenAPI功能指南現在提供PDF格式。 下載整份指南，並使用Adobe Acrobat AI Assistant回答您的疑問。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager資產存放庫中所有可用的[已核准資產](approve-assets.md)都可以進行[搜尋](search-assets-api.md)，然後使用傳遞URL傳遞至整合式下游應用程式。

對 DAM 中已核准資產所做的任何變更 (包括版本更新和中繼資料修改)，都會自動反映在傳遞 URL 中。由於透過CDN為資產傳送設定的短存留時間(TTL)值為10分鐘，因此在10分鐘內，所有編寫和發佈介面中都會顯示更新。

下圖說明可用的傳送URL：

![傳遞API](assets/delivery-url.png)

下表說明各種可用傳送API的使用情況：

| 傳送API | 說明 |
|---|---|
| 以要求的輸出格式呈現資產的[網頁最佳化的二進位表示](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | 根據請求中傳送的資產ID，傳回請求輸出格式之資產的Web最佳化二進位表示法。 此外，您可以定義各種影像修飾元，例如，寬度、高度、旋轉、翻轉、品質、裁切、格式和[智慧型裁切](/help/assets/dynamic-media/image-profiles.md)。 如需支援的格式和影像修飾元，請參閱[API詳細資料](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat)。<br>Adobe建議對所有影像格式型別使用此API。 |
| [資產](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset)的Web最佳化二進位表示 | 將預設套用至回應中傳回之資產的Web最佳化二進位表示的便利API。 預設值包括標準JPEG/WEBP格式、品質=> 65和寬度=> 1024。 |
| [資產的原始已上傳二進位檔](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | 傳回資產最初上傳的二進位檔案。 Adobe建議針對檔案格式型別和SVG影像使用此API。 |
| [預先產生的資產轉譯，可在AEM Assets製作環境中使用](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | 根據請求中傳送的資產ID和轉譯名稱，傳回AEM Assets製作環境中可用的資產轉譯位元串流。 |
| [資產中繼資料](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | 傳回與資產關聯的屬性，例如，標題、說明、CreateDate、ModifyDate等。 |
| 視訊資產的[播放器容器](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | 傳回視訊資產的播放器容器。 您可以將播放器內嵌至iframeHTML元素中，並播放視訊。 |
| [播放資料清單為選取的輸出格式](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | 以選取的輸出格式傳回指定視訊資產的播放資訊清單檔案。 您必須建置能夠透過HLS或DASH通訊協定進行自我調整資料流的自訂播放器，才能提取播放資訊清單檔案並播放視訊。 |


>[!NOTE]
>
* [影像預設集、智慧型影像以及其他影像修飾元](https://adobe-aem-assets-delivery-advancemodifiers.redoc.ly/)是您可用的有限功能。 若要取得存取權，請[建立並提交Adobe客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
* [Assets Prime](/help/assets/assets-ultimate-overview.md)無法使用智慧型裁切。

## 傳送API端點 {#delivery-apis-endpoint}

API端點因每個傳送API而異。 例如，`Web-optimized binary representation of the asset in the requested output format` API的API端點是：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

傳遞網域的結構類似於Experience Manager作者環境的網域。 唯一的差異是以`delivery`取代字詞`author`。

`pXXXX`參考方案識別碼

`eYYYY`參考環境識別碼

如需詳細資訊，請參閱[API詳細資料](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets)。

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

若要叫用傳遞API，`Authorization`詳細資料中需要IMS權杖才能傳遞受限制的資產。 IMS權杖是從技術帳戶中擷取。 請參閱[擷取AEM as a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials)以建立新的技術帳戶。 請參閱[產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)以產生IMS權杖，並在傳遞API要求標頭中正確使用它。


若要檢視要求範例、回應範例和回應代碼，請參閱[傳送API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat)。
