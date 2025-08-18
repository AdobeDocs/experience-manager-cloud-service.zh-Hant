---
title: 搜尋Assets API
description: 瞭解如何使用Search Assets API。
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: 8b596c6e82d9beaeb922cc6635717f151bb390e7
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 搜尋Assets API {#search-assets-api}

可以搜尋Experience Manager資產存放庫中所有可用的[已核准資產](approve-assets.md)，然後使用傳送URL傳送給整合的下游應用程式。

從Experience Manager存放庫搜尋正確的已核准資產，是使用傳送URL傳送資產的第一步。 對搜尋請求的回應包括對應於符合搜尋條件的資產的一系列JSON檔案。 每個JSON檔案都使用`id`欄位識別，該欄位用於構成資產傳遞請求。

![直接二進位上傳通訊協定概觀](assets/search-assets-api-overview.png)

您可以在Search Assets API請求中定義屬性，以啟用下列功能：

* **全文檢索搜尋**：使用`match`查詢定義要搜尋的文字。  您也可以使用`match`查詢中的運運算元來篩選結果。

* **套用篩選器**：使用`term`查詢，定義一個`key`和一個或多個值，以進一步篩選結果。 `key`會識別其值必須相符的欄位，`value`代表要相符的欄位。 同樣地，您可以使用`range`查詢來定義欄位的範圍，其使用大於(gt)、大於或等於(gte)、小於(lt)以及小於或等於(lte)屬性。

* **排序結果**：使用`OrderBy`屬性，根據一或多個欄位來排序搜尋結果。 您可以依遞增或遞減順序來排序結果。

* **分頁**：使用`limit`和`cursor`屬性，在Search API要求中定義分頁屬性。 `limit`屬性會定義API回應中要擷取的最大專案數。 `cursor`屬性有助於擷取`limit`屬性中定義之下一組資產的起點。 例如，如果您在API要求中將`50`定義為限制，您可以使用`cursor`屬性來開始，並使用下一個API要求擷取接下來的50個專案。

## 搜尋資產API端點 {#search-assets-api-endpoint}

搜尋資產API請求中的端點必須採用以下格式：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

傳遞網域的結構類似於Experience Manager作者環境的網域。 唯一的差異是以`author`取代字詞`delivery`。

`pXXXX`參考方案識別碼

`eYYYY`參考環境識別碼

## 搜尋資產API要求方法 {#search-assets-api-request-method}

POST

## 搜尋Assets API標頭 {#search-assets-api-header}

在「搜尋資產API」中定義標題時，您必須提供下列詳細資料：

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

若要叫用搜尋API，必須在`Authorization`詳細資料中定義IMS權杖。 IMS權杖是從技術帳戶中擷取。 請參閱[擷取AEM as a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=zh-Hant#fetch-the-aem-as-a-cloud-service-credentials)以建立新的技術帳戶。 請參閱[產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=zh-Hant#generating-the-access-token)以產生IMS權杖，並在搜尋資產API要求標頭中正確使用它。

若要檢視要求範例、回應範例和回應代碼，請參閱[搜尋Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/search)。
