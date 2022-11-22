---
title: 進階URL設定
description: 了解如何自訂產品和類別頁面的URL。 這可讓實施最佳化搜尋引擎的URL，並促進探索。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: fbd2fdcb61bcbae49f07c3da26b14d56d50b1cab
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 3%

---

# 進階URL設定 {#url}

>[!NOTE]
>
> 搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，在許多 Adobe Experience Manager (AEM) as a Cloud Service 專案中，SEO 考量都是需要解決的問題。請閱讀 [SEO和URL管理最佳作法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) 以取得其他資訊。

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 提供進階設定，可自訂產品和類別頁面的URL。 許多實作會為了搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定 `UrlProvider` 服務與功能 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要設定 `UrlProvider` 服務（根據SEO需求和需求）必須提供 _CIF URL提供者設定_.

>[!NOTE]
>
> 自AEM CIF核心元件2.0.0版起，URL提供者設定僅提供預先定義的URL格式，而非1.x版已知的可自由文字設定的格式。 此外，在URL中使用選取器傳遞資料的做法已取代為尾碼。

### 產品頁面URL格式 {#product}

這可設定產品頁面的URL並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

若 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 會取代為產品的sku，例如 `VP09`
* `{{url_key}}` 將被產品的 `url_key` 屬性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 將被產品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將替換為目前選取的變體，例如 `VP09-KH-S`

由於 `url_path` 已遭取代，預先定義的產品URL格式會使用產品的 `url_rewrites` 並挑選路徑區段最多的區段，若 `url_path` 無法使用。

使用上述範例資料，使用預設URL格式格式化的產品變體URL看起來會像 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 類別頁面URL格式 {#product-list}

這可設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

若 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將替換為類別的 `url_key` 屬性
* `{{url_path}}` 將替換為類別的 `url_path`

使用上述範例資料，使用預設URL格式格式化的類別頁面URL看起來會像 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 此 `url_path` 是 `url_keys` 產品或類別的祖先和產品或類別的 `url_key` 分隔 `/` 斜線。 每個 `url_key` 在指定商店內被視為唯一。

### 儲存特定配置 {#store-specific-urlformats}

由 _CIF URL提供者設定_ 可針對每個商店進行變更。

在CIF設定中，編輯器可以選取替代產品或類別頁面URL格式。 若未選取任何項目，則實作會回退至系統範圍設定。

變更即時網站的URL格式可能會對網站的自然流量造成負面影響。 請參閱 [最佳實務](#best-practices) 並事先謹慎規劃URL格式的變更。

![CIF設定中的URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> 儲存URL格式的特定配置需要 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 和最新版Adobe Experience Manager Content and Commerce附加元件。

## 類別感知產品頁面URL {#context-aware-pdps}

由於可以將產品URL中的類別資訊編碼，因此多個類別中的產品也可以用多個產品URL來定址。

預設URL格式會使用下列配置來選取其中一個可能的替代方案：

* 若 `url_path` 由電子商務後端使用它來定義（已過時）
* 從 `url_rewrites` 使用以產品結尾的URL `url_key` 作為替代
* 形成這些替代項目時，會使用路徑區段最多的
* 如果有多個，請依電子商務後端提供的順序取用第一個

此配置將選取 `url_path` 以最祖先為基礎，假設子類別比父類別更具體。 所選 `url_path` 被視為 _正則_ 和一律會在產品頁面或產品Sitemap中當作標準連結。

不過，當購物者從類別頁面導覽至產品頁面，或從一個產品頁面導覽至相同類別中的另一個相關產品頁面時，應保留目前的類別內容。 在此案例中， `url_path` 選取項目應偏好替代項目，而這些替代項目位於目前類別內容，而非 _正則_ 選項。

此功能必須在 _CIF URL提供者設定_. 如果已啟用，則選取項目的評分會較高，當

* 它們與給定類別的部分匹配 `url_path` 從開頭開始（模糊前置詞匹配）
* 或者它們與指定類別的 `url_key` 隨處（完全部分比對）

例如，請考量 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下方。 由於使用者位於「2022年夏季的新產品/新產品」類別頁面，且商店使用預設類別頁面URL格式，因此替代的「new-products/new-in-summer-2022/gold-cirque-earrings.html」會從頭開始符合上下文的2個路徑區段：「新產品」和「2022年夏季新產品」。 如果商店使用的類別頁面URL格式僅包含類別 `url_key`，則仍會選取相同的替代，因為它符合上下文的 `url_key` 隨處皆可。 在這兩種情況下，都會為&quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot;建立產品頁面URL `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> 類別感知產品URL需要 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

## 特定類別和產品頁面 {#specific-pages}

您可以建立 [多類別和產品頁面](../authoring/multi-template-usage.md) 僅適用於目錄的特定類別或產品子集。

### 選擇標準 {#specific-pages-selection}

根據類別，直接選擇特定類別頁面 `url_path` 或 `url_key`. 只有包含完整類別的URL格式才支援相符的子類別 `url_path`. 否則，只有 `url_key` 是可能的。

特定產品頁面會依產品的SKU或類別來選取。 後者需要在產品URL中編碼某些類別資訊。 這僅適用於部分預設URL格式。 請參閱下表以取得比較，了解哪些URL格式支援依SKU或類別選取特定頁面。


| URL格式 | 按sku | 依類別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 僅完全匹配 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 僅完全匹配 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> 需要依類別選取特定產品頁面 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

### 深度連結 {#specific-pages-deep-linking}

此 `UrlProvider` 已預先設定，以在製作層級例項上產生特定類別和產品頁面的深層連結。 對於編輯者來說，這很實用，他們可以使用預覽模式瀏覽網站、導覽至特定產品或類別頁面，然後切換回編輯模式以編輯頁面。

另一方面，在發佈層級例項上，目錄頁面URL應保持穩定，以免在搜尋引擎排名上失去增益。 因為該發佈層級例項預設不會呈現特定目錄頁面的深層連結。 若要變更此行為， _CIF URL提供者特定頁面策略_ 可設定為一律產生特定頁面URL。

### 多個目錄頁面 {#multiple-product-pages}

當編輯者想要完全控制網站的頂層導覽時，可能不需要使用單一目錄頁面來呈現目錄的頂層類別。 編輯者可以建立多個目錄頁面，針對他們要包含在頂層導覽中的目錄類別各建立一個頁面。

對於該使用案例，每個目錄頁面可具有對針對目錄頁面配置的類別的特定產品和類別頁面的參考。 此 `UrlProvider` 將使用這些來建立已設定類別中頁面和類別的連結。 不過，基於效能考量，僅會考慮網站導覽根/登陸頁面的直接目錄頁面子項。

建議將目錄頁面的產品和類別頁面子系至該目錄頁面，否則導覽或階層連結等元件可能無法正常運作。

>[!NOTE]
>
> 需要完整支援多個目錄頁面 [CIF核心元件2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) 或更新版本。

## 自訂 {#customization}

### 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可在 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，並將實作註冊為OSGI服務。 這些實作（若有）將取代已設定的預先定義格式。 如果已註冊多個實施，則服務排名較高的實施會以較低的服務排名取代該實施。

自訂URL格式實施必須實作一對方法，以從指定參數建立URL，並剖析URL以分別傳回相同參數。

### 結合Sling對應 {#sling-mapping}

除了 `UrlProvider`，也可以設定 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫及處理URL。 AEM原型專案也提供 [範例設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為連接埠4503（發佈）和80（調度程式）設定某些Sling對應。

### 結合AEM Dispatcher {#dispatcher}

URL重新寫入也可透過使用AEM Dispatcher HTTP伺服器來達成，並搭配 `mod_rewrite` 模組。 此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 提供參考AEM Dispatcher設定，其中已包含基本 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) ，取代所產生的大小。

## 最佳作法 {#best-practices}

### 選擇最佳URL格式 {#choose-url-format}

如在選取可用的預設格式之一，或甚至實作自訂格式前所述，高度取決於商店的需求和需求。 下列建議有助於做出有根據的決定。

_**使用包含SKU的產品頁面URL格式。**_

CIF核心元件會以SKU作為所有元件的主要識別碼。 如果產品頁面URL格式不包含SKU，則需要GraphQL查詢才能加以解析。 這可能會影響到首位元組時間。 此外，購物者可使用搜尋引擎，依SKU尋找產品。

_**使用包含類別內容的產品頁面URL格式。**_

CIF URL提供者的某些功能只有在使用產品URL格式時才可使用，這些格式可編碼類別內容，例如類別 `url_key` 或類別 `url_path`. 即使新商店可能不需要這些功能，但一開始使用其中一種URL格式有助於減少日後的移轉工作。

_**平衡URL長度與編碼資訊。**_

根據目錄大小，特別是類別樹的大小和深度，對完整目錄進行編碼可能不合理 `url_path` 的類別。 在這種情況下，只要包含類別的 `url_key` 。 這將支援使用類別時可用的大部分功能 `url_path`.

此外，請使用 [Sling對應](#sling-mapping) 以便將sku與產品結合 `url_key`. 在大部分的電子商務系統中，SKU會遵循特定格式，並將SKU與 `url_key` 對於傳入的請求，應該很容易。 有鑑於此，將產品頁面URL重新寫入 `/p/{{category}}/{{sku}}-{{url_key}}.html`，以及類別URL `/c/{{url_key}}.html` 分別來說。 此 `/p` 和 `/c` 為了將產品和類別頁面與其他內容頁面區分開來，首碼仍然是必要的。

### 移轉至新URL格式 {#migrate-url-formats}

許多預設URL格式彼此不同程度地相容，這表示由某個格式設定的URL可能會由另一個格式設定的URL剖析。 這有助於在URL格式之間移轉。

另一方面，搜尋引擎需要一些時間，才能以新的URL格式重新編目所有目錄頁面。 若要支援此程式並改善一般使用者體驗，建議您提供重新導向，將使用者從舊的URL轉送至新的URL。

其中一個方法是將預備環境連結至生產電子商務後端，並設定為使用新的URL格式。 之後請取得 [由CIF產品Sitemap產生器產生的產品Sitemap](../../overview/seo-and-url-management.md) 針對預備和生產環境，並使用它們來建立 [Apache httpd重寫映射](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). 此重新寫入地圖可與新URL格式的轉出一併部署至Dispatcher。

## 範例 {#example}

此 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) 專案包含設定範例，以示範產品和類別頁面的自訂URL使用方式。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別的URL模式。 CIF的組合 `UrlProvider` 和Sling對應已使用，如上所述。

>[!NOTE]
>
>此設定必須與專案使用的外部網域一併調整。 Sling對應會根據主機名稱和網域運作。 因此，預設情況下會停用此設定，且必須在部署前啟用。 若要這麼做，請重新命名Sling對應 `hostname.adobeaemcloud.com` 資料夾 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的網域名稱，並借由新增 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 專案的設定。

## 其他資源 {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
