---
title: 高級URL配置
description: 瞭解如何自定義產品和類別頁的URL。 這允許實現優化搜索引擎的URL並促進發現。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 3%

---

# 高級URL配置 {#url}

>[!NOTE]
>
> 搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，在許多 Adobe Experience Manager (AEM) as a Cloud Service 專案中，SEO 考量都是需要解決的問題。請閱讀 [SEO和URL管理最佳實踐](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) 的雙曲餘切值。

[AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 提供高級配置，以自定義產品和類別頁的URL。 許多實現將自定義這些URL以用於搜索引擎優化(SEO)。 以下視頻詳細資訊如何配置 `UrlProvider` 服務和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定義產品和類別頁的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

配置 `UrlProvider` 服務時，項目必須提供OSGI配置 _CIF URL提供程式配置_。

>[!NOTE]
>
> 自CIF核心元件2.0.0版以來，URL提供程式配置僅提供預定義的URL格式，而不提供1.x版中已知的自由文本配置格式。 此外，使用選擇器傳遞URL中的資料已被尾碼取代。

### 產品頁URL格式 {#product}

這將配置產品頁的URL，並支援以下選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

對於 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 將被產品的sku替換，例如 `VP09`
* `{{url_key}}` 將被產品的 `url_key` 屬性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 將被產品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將替換為當前選定的變型，例如 `VP09-KH-S`

自 `url_path` 已棄用，預定義的產品URL格式使用產品 `url_rewrites` 選擇路徑段最多的路徑段， `url_path` 不可用。

使用上面的示例資料，使用預設URL格式格式化的產品變型URL將看起來類似 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 類別頁URL格式 {#product-list}

這將配置類別或產品清單頁的URL，並支援以下選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

對於 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將被類別的 `url_key` 屬性
* `{{url_path}}` 將被類別的 `url_path`

使用上面的示例資料，使用預設URL格式設定的類別頁URL將看起來類似 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
> 的 `url_path` 是 `url_keys` 產品或類別的祖先和產品或類別的 `url_key` 分隔 `/` 斜線。 每個 `url_key` 在給定商店中被認為是唯一的。

### 儲存特定配置 {#store-specific-urlformats}

系統範圍的類別和產品頁面URL格式由 _CIF URL提供程式配置_ 可以為每個商店更改。

在CIF配置中，編輯器可以選擇替代產品或類別頁URL格式。 如果未選擇任何內容，則實施將回退到系統範圍的配置。

更改即時網站的URL格式可能會對站點的有機通信產生負面影響。 請參閱 [最佳做法](#best-practices) 並事先仔細規劃URL格式的更改。

![CIF配置中的URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> URL格式的儲存特定配置需要 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以及Adobe Experience Manager內容與商業附加軟體的最新版本。

## 類別感知產品頁URL {#context-aware-pdps}

由於可以對產品URL中的類別資訊進行編碼，因此可以用多個產品URL對處於多個類別的產品進行定址。

預設URL格式將使用以下方案選擇一個可能的替代方案：

* 的 `url_path` 由電子商務後端使用它（不建議使用）定義
* 從 `url_rewrites` 使用以產品結尾的URL `url_key` 作為替代
* 形成這些替代方案時使用路徑段最多的
* 如果有多個，請按電子商務後端給定的順序選擇第一個

此方案將選擇 `url_path` 基於子類別比其父類別更具體的假設。 所選 `url_path` 考慮 _正則_ 並且將始終用作產品頁面或產品站點地圖中的規範連結。

但是，當購物者從類別頁導航到產品頁，或從一個產品頁導航到同一類別中的另一個相關產品頁時，保留當前類別上下文是值得的。 在本例中， `url_path` 選擇應選擇在當前類別上下文內而不是 _正則_ 中。

必須在 _CIF URL提供程式配置_。 如果啟用，則選擇的備選項分數將更高

* 它們匹配給定類別的部分 `url_path` 從開頭（模糊前置詞匹配）
* 或者它們與給定類別匹配 `url_key` 任意位置（完全部匹配）

例如，請考慮 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下。 如果用戶位於「2022年夏季的新產品/新產品」類別頁面，且儲存區使用預設類別頁URL格式，則替代「new-products/new-in-summer-2022/gold-cirque-earrings.html」將從頭開始匹配上下文的2個路徑段：「新產品」和「2022年夏季新產品」。 如果儲存使用僅包含該類別的類別頁URL格式 `url_key`，當與上下文匹配時，仍將選擇相同的替代 `url_key` 任何地方。 在這兩種情況下，都將為「new-products/new-in-summer-2022/gold-cirque-earrings.html」建立產品頁URL `url_path`。

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
> 類別感知產品URL需要 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新。

## 特定類別和產品頁 {#specific-pages}

可以建立 [多類別和產品頁](../authoring/multi-template-usage.md) 僅用於目錄的特定類別或產品子集。

### 選擇條件 {#specific-pages-selection}

根據類別，選擇特定類別頁面是直接向前的 `url_path` 或 `url_key`。 僅對包含完整類別的URL格式支援匹配子類別 `url_path`。 否則，僅與 `url_key` 可能。

特定產品頁面按產品的sku或類別進行選擇。 後者要求在產品URL中編碼某些類別資訊。 這僅適用於某些預設URL格式。 有關URL格式支援按sku或類別選擇特定頁面的比較，請參閱下表。


| URL格式 | 按sku | 按類別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 完全匹配 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 完全匹配 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> 按類別選擇特定產品頁面需要 [CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新。

### 深度連結 {#specific-pages-deep-linking}

的 `UrlProvider` 預配置為在作者層實例上生成指向特定類別和產品頁的深層連結。 這對編輯器非常有用，編輯器使用「預覽」模式瀏覽網站，導航到特定產品或類別頁面並切換回「編輯」模式以編輯該頁面。

另一方面，在發佈層實例上，目錄頁URL應保持穩定，以避免在搜索引擎排名上失利。 由於該發佈層實例將不會在預設情況下呈現指向特定目錄頁的深度連結。 要更改此行為， _CIF URL提供程式特定頁面策略_ 可以配置為始終生成特定頁URL。

## 自定義 {#customization}

### 自定義URL格式 {#custom-url-format}

要提供自定義URL格式，項目可以 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，將實現註冊為OSGI服務。 如果可用，這些實現將替換已配置的預定義格式。 如果註冊了多個實現，則具有較高服務等級的實現用較低服務等級代替所述一個或多個實現。

自定義URL格式實現必須實現一對方法，以從給定參數構建URL，並分析URL以分別返回相同的參數。

### 與Sling映射組合 {#sling-mapping}

除 `UrlProvider`，也可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫和處理URL。 Archetype項AEM目還提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為埠4503（發佈）和80（調度程式）配置某些Sling映射。

### 與Dispatcher結AEM合 {#dispatcher}

還可以使用Dispatcher HTTP伺服器AEM和 `mod_rewrite` 中。 的 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 提供已包AEM含基本功能的引用Dispatcher配置 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 生成大小。

## 最佳作法 {#best-practices}

### 選擇最佳URL格式 {#choose-url-format}

正如在選擇可用預設格式之一或甚至實施自定義格式之前所提到的，這高度取決於儲存的需要和要求。 以下建議可能有助於作出明智的決定。

_**使用包含sku的產品頁面URL格式。**_

CIF核心元件將sku用作所有元件中的主標識符。 如果產品頁面URL格式不包含sku，則需要GraphQL查詢來解析它。 這可能會影響時間到第一位元組。 此外，消費者可以通過使用搜索引擎的sku來查找產品。

_**使用包含類別上下文的產品頁URL格式。**_

CIF URL提供程式的某些功能僅在使用產品URL格式（對類別上下文進行編碼）時可用，如類別 `url_key` 或類別 `url_path`。 即使新商店可能不需要這些功能，但在開始時使用這些URL格式有助於減少將來的遷移工作。

_**在URL長度和編碼資訊之間平衡。**_

根據目錄大小，特別是類別樹的大小和深度，對完整目錄進行編碼可能不合理 `url_path` 的子菜單。 在這種情況下，只包括類別的URL長度 `url_key` 的雙曲餘切值。 這將支援使用類別時可用的大多數功能 `url_path`。

此外， [Sling映射](#sling-mapping) 以便把sku和產品 `url_key`。 在大多數電子商務系統中，sku遵循特定格式，並將sku與 `url_key` 對於傳入的請求，應該很容易。 考慮到這一點，應將產品頁面URL重寫為 `/p/{{category}}/{{sku}}-{{url_key}}.html`和類別URL `/c/{{url_key}}.html` 分別來。 的 `/p` 和 `/c` 為了將產品和類別頁面與其他內容頁面區分開來，前置詞仍然是必要的。

### 遷移到新URL格式 {#migrate-url-formats}

許多預設URL格式在某種程度上彼此相容，這意味著由一個格式形成的URL可能由另一個格式解析。 這有助於在URL格式之間遷移。

另一方面，搜索引擎需要一些時間來使用新的URL格式重新搜索所有目錄頁。 為支援此過程並改善最終用戶體驗，建議提供將用戶從舊URL轉發到新URL的重定向。

一種方法是將階段環境連接到生產電子商務後端，並將其配置為使用新的URL格式。 隨後獲取 [由CIF產品站點地圖生成器生成的產品站點地圖](../../overview/seo-and-url-management.md) 為階段和生產環境建立 [Apache httpd重寫映射](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html)。 此重寫映射可以與新URL格式的推廣一起部署到調度程式。

## 範例 {#example}

的 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia) 項目包括示例配置，以演示產品和類別頁的自定義URL的使用。 這允許每個項目根據其SEO需求為產品和類別頁面設定單個URL模式。 CIF的組合 `UrlProvider` 和Sling映射（如上所述）。

>[!NOTE]
>
>此配置必須與項目使用的外部域一起調整。 Sling映射基於主機名和域工作。 因此，預設情況下禁用此配置，並且必須在部署之前啟用此配置。 要執行此操作，請更名Sling映射 `hostname.adobeaemcloud.com` 資料夾 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的域名，通過添加 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 項目的配置。

## 其他資源 {#additional}

* [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia)
* [資AEM源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
