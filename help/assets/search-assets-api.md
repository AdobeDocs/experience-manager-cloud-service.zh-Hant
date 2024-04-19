---
title: 搜尋資產API
description: 瞭解如何使用搜尋資產API。
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 搜尋資產API {#search-assets-api}

全部 [核准的資產](approved-assets.md) Experience Manager資產存放庫中可用的專案，可以透過傳送URL搜尋並傳送至整合的下游應用程式。

從Experience Manager存放庫搜尋正確的已核准資產，是使用傳送URL傳送資產的第一步。 對搜尋請求的回應包括對應於符合搜尋條件的資產的一系列JSON檔案。 每個JSON檔案都使用 `id` 欄位，用於撰寫資產傳送請求。

![直接二進位上傳通訊協定概觀](assets/search-assets-api-overview.png)

您可以在Search Assets API請求中定義屬性，以啟用下列功能：

* **全文檢索搜尋**：使用 `match` 查詢以定義搜尋文字。  您也可以使用中的運運算元 `match` 查詢以篩選結果。

* **套用篩選器**：使用 `term` 查詢：透過定義 `key` 和一個或多個值。 `key` 會識別其值必須比對的欄位，並且 `value` 代表要比對的專案。 同樣地，您可以使用 `range` 查詢以使用「大於(gt)」、「大於或等於(gte)」、「小於(lt)」和「小於或等於(lte)」屬性來定義欄位範圍。

* **排序結果**：使用 `OrderBy` 根據一或多個欄位來排序搜尋結果的屬性。 您可以依遞增或遞減順序來排序結果。

* **分頁**：使用 `limit` 和 `cursor` 屬性來定義搜尋API請求中的分頁屬性。 `limit` 屬性會定義API回應中要擷取的最大專案數。 `cursor` 屬性有助於擷取中定義之下一組資產的起點 `limit` 屬性。 例如，如果您定義 `50` 作為API請求中的限制，您可以使用 `cursor` 屬性以開始使用下一個API請求來擷取接下來的50個專案。

## 搜尋資產API端點 {#search-assets-api-endpoint}

搜尋資產API請求中的端點必須採用以下格式：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

傳遞網域的結構類似於Experience Manager作者環境的網域。 唯一的區別是取代術語 `author` 替換為 `delivery`.

`pXXXX` 是指方案ID

`eYYYY` 指環境ID

## 搜尋資產API要求方法 {#search-assets-api-request-method}

POST

## 搜尋資產API標題 {#search-assets-api-header}

在「搜尋資產API」中定義標題時，您必須提供下列詳細資料：

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

若要叫用Search API，必須在中定義IMS權杖 `Authorization` 詳細資料。 IMS權杖是從技術帳戶中擷取。 另請參閱 [擷取AEMas a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) 以建立新的技術帳戶。 另請參閱 [產生存取權杖](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) 以產生IMS代號，並在搜尋資產API請求標頭中適當使用。

若要檢視要求範例、回應範例和回應代碼，請參閱 [搜尋資產API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).

