---
title: 整合Asset Selector與Dynamic Media Open API
description: 整合資產選擇器與各種Adobe、非Adobe及協力廠商應用程式。
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: 47afd8f95eee2815f82c429e9800e1e533210a47
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 9%

---

# 整合Dynamic Media與OpenAPI功能 {#integrate-asset-selector-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
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

Asset Selector可讓您整合使用各種Adobe應用程式，讓這些應用程式緊密合作。


## 先決條件 {#prereqs-polaris}

如果您整合Asset Selector與Dynamic Media以及OpenAPI功能，請使用下列先決條件：

* [通訊方法](/help/assets/overview-asset-selector.md#prereqs)
* 若要使用OpenAPI功能存取Dynamic Media，您必須擁有下列專案的授權：
   * Assets存放庫(例如Experience Manager Assets as a Cloud Service)。
   * AEM Dynamic Media。
* 只有[個核准的資產](/help/assets/approve-assets.md)可供使用，以確保品牌一致性。

## 整合Dynamic Media與OpenAPI功能 {#adobe-app-integration-polaris}

Asset Selector與Dynamic Media OpenAPI程式的整合涉及各種步驟，包括建立自訂的Dynamic Media URL或準備選取Dynamic Media URL等。

### 整合 Dynamic Media 的資產選擇器與 OpenAPI 功能 {#integrate-dynamic-media}

`rootPath`和`path`屬性不應該是具有OpenAPI功能的Dynamic Media的一部分。 您可以改為設定`aemTierType`屬性。 以下是設定的語法：

```
aemTierType:[1: "delivery"]
```

此設定可讓您檢視所有核准的資產，而不使用資料夾或以平面結構檢視。 如需詳細資訊，請導覽至[資產選擇器屬性](/help/assets/asset-selector-properties.md)下的`aemTierType`屬性。


### 從已核准的資產建立動態傳送URL {#create-dynamic-media-url}

設定「資產選擇器」後，系統會使用物件的結構描述，從選取的資產建立動態傳送URL。
例如，從選取資產時收到的物件陣列中的一個物件的結構描述：

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

所有選取的資產都由做為JSON物件的`handleSelection`函式執行。 例如 `JsonObj`。動態傳遞URL是透過結合以下電信業者來建立：

| 物件 | JSON |
|---|---|
| 主機 | `assetJsonObj["repo:repositoryId"]` |
| API根目錄 | `/adobe/dynamicmedia/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| 格式 | `.jpg` |

#### 核准的資產傳送API規格 {#approved-assets-delivery-api-specification}

URL格式：
`https://<delivery-api-host>/adobe/assets/<asset-id>/<seo-name>.<format>?<image-modification-query-parameters>`

其中，

* 主機為`https://delivery-pxxxxx-exxxxxx.adobe.com`
* API根目錄為`"/adobe/assets"`
* `<asset-id>`為資產識別碼
* `<seo-name>`為資產名稱
* `<format>`為輸出格式
* `<image modification query parameters>`為核准資產的傳遞API規格所支援

#### 核准的資產原始轉譯傳送API {#approved-assets-delivery-api}

動態傳送URL擁有下列語法：
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`，其中，

* 主機為`https://delivery-pxxxxx-exxxxxx.adobe.com`
* 原始轉譯傳遞的API根為`"/adobe/assets"`
* `<asset-id>`為資產識別碼
* `/original/as`是open API規格的常數部分，指出原始轉譯稱為
* `<seo-name>`為具有或不具有副檔名的資產名稱

### 準備挑選動態傳遞URL {#ready-to-pick-dynamic-delivery-url}

所有選取的資產都由做為JSON物件的`handleSelection`函式執行。 例如 `JsonObj`。動態傳遞URL是透過結合以下電信業者來建立：

| 物件 | JSON |
|---|---|
| 主機 | `assetJsonObj["repo:repositoryId"]` |
| API根目錄 | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

以下是遍歷JSON物件的兩種方式：

![動態傳遞URL](assets/dynamic-delivery-url.png)

* **縮圖：**&#x200B;縮圖可為影像，資產為PDF、影片、影像等。 不過，您可以使用資產縮圖的高度和寬度屬性作為動態傳送轉譯。
下列轉譯集可用於PDF型別資產：
在sidekick中選取PDF後，選取內容會提供以下資訊。 以下為遍歷JSON物件的方式：

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  您可以在上方熒幕擷圖中，參考`selection[0].....selection[4]`以取得一系列轉譯連結。 例如，其中一個縮圖轉譯的關鍵屬性包括：

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

在上述熒幕擷圖中，如果需要PDF，而非其縮圖，則需要將PDF原始轉譯的傳送URL合併至目標體驗。 例如 `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **影片：**&#x200B;您可以使用內嵌iFrame的影片型別資產，使用影片播放器URL。 您可以在目標體驗中使用下列陣列轉譯：
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  您可以在上方熒幕擷圖中，參考`selection[0].....selection[4]`以取得一系列轉譯連結。 例如，其中一個縮圖轉譯的關鍵屬性包括：

  上述熒幕擷取畫面中的程式碼片段為視訊資產的範例。 其中包含轉譯連結陣列。 摘錄中的`selection[5]`是影像縮圖的範例，可做為目標體驗中視訊縮圖的預留位置。 轉譯陣列中的`selection[5]`適用於視訊播放器。 此函式提供HTML，可設為iframe的`src`。 它支援自我調整位元速率串流，這是網頁最佳化的視訊傳送方式。

  在上述範例中，視訊播放器URL為`https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

### 設定自訂篩選器 {#configure-custom-filters-dynamic-media-open-api}

具有OpenAPI功能的Dynamic Media資產選擇器可讓您設定自訂屬性，以及基於自訂屬性的篩選器。 `filterSchema`屬性是用來設定這類屬性。 自訂可公開為`metadata.<metadata bucket>.<property name>.`，以便針對其設定篩選器，其中，

* `metadata`是資產的資訊
* `embedded`是用於設定的靜態引數，並且
* `<propertyname>`是您正在設定的篩選器名稱

對於設定，定義在`jcr:content/metadata/`層級的屬性會針對您要設定的篩選器，公開為`metadata.<metadata bucket>.<property name>.`。

例如，在具有OpenAPI功能的Dynamic Media資產選擇器中，`asset jcr:content/metadata/client_name:market`上的屬性會針對篩選器設定轉換為`metadata.embedded.client_name:market`。

若要取得名稱，必須完成一次性活動。 對資產發出搜尋API呼叫，並取得屬性名稱（基本上是貯體）。

### 具OpenAPI功能的Dynamic Media資產選擇器使用者介面 {#interface-dynamic-media-open-api}

與Adobe的微前端資產選擇器整合後，您只能看到Experience Manager資產存放庫中所有已核准資產的結構。

![具有OpenAPI功能UI的Dynamic Media](assets/polaris-ui.png)

* **A**：[隱藏/顯示面板](#hide-show-panel)
* **B**： [Assets](#repository)
* **C**： [排序](#sorting)
* **D**：[篩選器](#filters)
* **E**：[搜尋列](#search-bar)
* **F**： [依遞增或遞減順序排序](#sorting)
* **G**：取消選取
* **H**：選取單一或多個資產

>[!NOTE]
>
>只有在連線到作者存放庫時才支援資料夾，不支援具有OpenAPI存放庫的Dynamic Media。

>[!MORELIKETHIS]
>
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
