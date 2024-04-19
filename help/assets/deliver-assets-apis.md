---
title: 傳送API
description: 瞭解如何使用傳送API。
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 傳送API {#delivery-apis}

全部 [核准的資產](approved-assets.md) Experience Manager資產存放庫中的可用資產可以是 [已搜尋](search-assets-api.md) 然後使用傳送URL傳送給整合的下游應用程式。

對DAM中已核准的資產所做的任何變更（包括版本更新和中繼資料修改）都會自動反映在傳送URL中。 由於透過CDN為資產傳送設定的短存留時間(TTL)值為10分鐘，因此在10分鐘內，所有編寫和發佈介面中都會顯示更新。

下圖說明可用的傳送URL：

![傳送API](assets/delivery-url.png)

下表說明各種可用傳送API的使用情況：

| 傳送API | 說明 |
|---|---|
| [以要求的輸出格式呈現資產的Web最佳化二進位表示法](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat) | 根據請求中傳送的資產ID，傳回請求輸出格式之資產的Web最佳化二進位表示法。 此外，您可以定義各種影像修飾元，例如，寬度、高度、旋轉、翻轉、品質等等。 請參閱 [API詳細資料](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat) 以取得支援的格式和影像修飾元。<br>Adobe建議針對所有影像格式型別使用此API。 |
| [資產的網頁最佳化二進位表示](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAsset) | 將預設套用至回應中傳回之資產的Web最佳化二進位表示的便利API。 預設值包括標準JPEG/WEBP格式、品質=> 65和寬度=> 1024。 |
| [資產的原始上傳二進位檔](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetOriginal) | 傳回資產最初上傳的二進位檔案。 Adobe建議針對檔案格式型別和SVG影像使用此API。 |
| [資產中繼資料](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetMetadata) | 傳回與資產關聯的屬性，例如，標題、說明、CreateDate、ModifyDate等。 |
| [視訊資產的播放器容器](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/videoPlayerDelivery) | 傳回視訊資產的播放器容器。 您可以將播放器內嵌至iframeHTML元素中，並播放視訊。 |
| [以選取的格式顯示播放](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/videoManifestDelivery) | 以選取的輸出格式傳回指定視訊資產的播放資訊清單檔案。 您必須建置能夠透過HLS或DASH通訊協定進行自我調整資料流的自訂播放器，才能提取播放資訊清單檔案並播放視訊。 |

## 傳送API端點 {#delivery-apis-endpoint}

API端點因每個傳送API而異。 例如，的API端點 `Web-optimized binary representation of the asset in the requested output format` API是：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

傳遞網域的結構類似於Experience Manager作者環境的網域。 唯一的區別是取代術語 `author` 替換為 `delivery`.

`pXXXX` 是指方案ID

`eYYYY` 指環境ID

另請參閱 [API詳細資料](https://adobe-aem-assets-delivery-experimental.redoc.ly/#tag/Assets) 以取得詳細資訊。

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

若要叫用傳送API，必須在以下專案中使用IMS代號： `Authorization` 傳遞受限制資產的詳細資訊。 IMS權杖是從技術帳戶中擷取。 另請參閱 [擷取AEMas a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) 以建立新的技術帳戶。 另請參閱 [產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) 以產生IMS代號，並在傳送API請求標頭中適當使用它。

若要檢視要求範例、回應範例和回應代碼，請參閱 [傳送API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat).

