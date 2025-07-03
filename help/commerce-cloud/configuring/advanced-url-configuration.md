---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 自訂可讓實作將搜尋引擎的URL最佳化並提升探索能力。
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 2%

---

# 進階URL設定 {#url}

>[!NOTE]
>
> 搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，在Adobe Experience Manager (AEM) as a Cloud Service上的許多專案中，SEO考量都是必須解決的問題。 如需詳細資訊，請參閱[SEO和URL管理最佳實務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/seo-and-url-management.html?lang=zh-Hant)。

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)提供進階設定，可自訂產品和類別頁面的URL。 許多實施會針對搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定`UrlProvider`服務和[Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要根據SEO需求和需求設定`UrlProvider`服務，專案必須提供&#x200B;_CIF URL提供者組態_&#x200B;的OSGI組態。

>[!NOTE]
>
> 自AEM CIF核心元件2.0.0版以來，「URL提供者」設定僅提供預先定義的URL格式，而非1.x版已知的自由文字可設定格式。 此外，在URL中使用選取器傳遞資料的功能，已由尾碼取代。

### 產品頁面URL格式 {#product}

設定產品頁面的URL並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

如果存在[Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已由`/content/venia/us/en/products/product-page`取代
* `{{sku}}`已由產品的SKU取代，例如`VP09`
* `{{url_key}}`已由產品的`url_key`屬性取代，例如`lenora-crochet-shorts`
* `{{url_path}}`已由產品的`url_path`取代，例如`venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}`已由目前選取的變體取代，例如`VP09-KH-S`

由於`url_path`已過時，預先定義的產品URL格式會使用產品的`url_rewrites`，並在`url_path`無法使用時，挑選具有最多路徑區段的專案作為替代方案。

在上述範例資料中，使用預設URL格式格式的產品變體URL看起來像`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 類別頁面URL格式 {#product-list}

設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

如果存在[Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已由`/content/venia/us/en/products/category-page`取代
* `{{url_key}}`已由類別的`url_key`屬性取代
* `{{url_path}}`已由類別的`url_path`取代

在上述範例資料中，使用預設URL格式格式化的類別頁面URL看起來像`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
> `url_path`是產品或類別祖先的`url_keys`與產品或類別的`url_key`的串連，以`/`斜線分隔。 在指定的存放區中，每個`url_key`都視為唯一。

### 存放區專屬設定 {#store-specific-urlformats}

可針對每個商店變更&#x200B;_CIF URL提供者組態_&#x200B;所設定的全系統類別和產品頁面URL格式。

在CIF設定中，編輯器可以選取替代產品或類別頁面URL格式。 如果未在該處選取任何專案，則實施作業會退回至系統範圍設定。

變更已上線的網站URL格式可能會對您網站的自然流量產生負面影響。 請參閱下方的[最佳實務](#best-practices)，並提前謹慎規劃URL格式的變更。

CIF設定中的![URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> URL格式的商店專用設定需要[CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)以及最新版本的Adobe Experience Manager內容和Commerce附加元件。

## 類別感知產品頁面URL {#context-aware-pdps}

由於可在產品URL中編碼類別資訊，因此屬於多個類別的產品也可使用多個產品URL來定址。

預設URL格式會使用以下配置選取一個可能的替代方案：

* 如果`url_path`是由電子商務後端定義，請使用它（已棄用）
* 來自`url_rewrites`，請使用結尾為產品`url_key`的URL作為替代專案
* 這些替代方案會使用具有最多路徑區段的替代方案
* 如果有多個，則按照電子商務後端所給定的順序進行第一個

此配置會根據子類別比其父類別更具體的假設，選取具有最多祖項的`url_path`。 選取的`url_path`會視為&#x200B;_規範_，且一律會作為產品頁面或產品網站地圖中的規範連結使用。

不過，當購物者從類別頁面導覽至產品頁面，或從某個產品頁面導覽至相同類別中的另一個相關產品頁面時，最好保留目前的類別內容。 在此情況下，`url_path`選取範圍應該偏好目前類別內容中的替代專案，而非上述的&#x200B;_canonical_&#x200B;選取專案。

必須在&#x200B;_CIF URL提供者組態_&#x200B;中啟用此功能。 若啟用，選擇分數會高於替代專案，當

* 它們從頭開始比對指定類別的`url_path`部分（模糊首碼比對）
* 或者在任何地方都和指定類別的`url_key`相符（完全的部份相符）

例如，考慮以下[產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)的回應。 假設有下列情況：

* 使用者在「2022年夏季新產品/新增」類別頁面
* 商店使用預設類別頁面URL格式

替代「new-products/new-in-summer-2022/gold-cirque-earrings.html」從頭開始比對內容的兩個路徑區段。 即「new-products」和「new-in-summer-2022」。 如果存放區使用僅包含類別`url_key`的類別頁面URL格式，則仍會選取相同的替代方案，因為它在任何地方都符合內容的`url_key`。 在這兩種情況下，都會為&quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`建立產品頁面URL。

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
> 類別感知產品URL需要[CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)或更新版本。

## 特定類別和產品頁面 {#specific-pages}

只能針對目錄的特定類別或產品子集建立[多類別和產品頁面](../authoring/multi-template-usage.md)。

### 選取條件 {#specific-pages-selection}

根據類別的`url_path`或`url_key`，特定類別頁面的選取是直接進行的。 只有包含完整類別`url_path`的URL格式才支援相符的子類別。 否則，只能完全符合`url_key`。

特定產品頁面是由產品的SKU或類別所選取。 後者需要在產品URL中編碼某些類別資訊。 此功能僅適用於部分預設URL格式。 請參閱下表比較，瞭解哪種URL格式支援依SKU或類別的特定頁面選擇。


| URL格式 | 依SKU | 依類別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 僅完全相符 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 僅完全相符 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style="table-layout:auto"}

>[!NOTE]
>
> 依類別選取特定產品頁面需要[CIF核心元件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)或更新版本。

### 深度連結 {#specific-pages-deep-linking}

`UrlProvider`已預先設定為產生作者層執行個體上特定類別和產品頁面的深層連結。 對於使用「預覽」模式瀏覽網站、導覽至特定產品或類別頁面並切換回「編輯」模式以編輯頁面的編輯者而言，此功能非常有用。

另一方面，在發佈層級執行個體上，目錄頁面URL應維持穩定，以免失去搜尋引擎排名之類的評分。 因為該發佈層級，依預設，執行個體不會轉譯特定目錄頁面的深層連結。 若要變更此行為，_CIF URL提供者特定頁面策略_&#x200B;可以設定為永遠產生特定頁面URL。

### 多個目錄頁面 {#multiple-product-pages}

當編輯器想要完全控制網站的最上層導覽時，可能不需要使用單一目錄頁面來呈現目錄的最上層類別。 編輯器可以建立多個目錄頁面，每個類別各有一個要包含在頂層導覽中的目錄。

對於該使用案例，每個目錄頁面都可具有產品和類別頁面的參考，這些頁面是為目錄頁面設定的類別所專屬。 `UrlProvider`會使用這些連線，為設定類別中的頁面和類別建立連結。 然而，基於效能考量，只會考量網站導覽根目錄/登陸頁面的直接目錄頁面子項。

建議目錄頁面的產品和類別頁面為該目錄頁面的子代，否則導覽或階層連結等元件可能無法正常運作。

>[!NOTE]
>
> 需要[CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0)或更新版本，才能完整支援多個目錄頁面。

## 自訂 {#customization}

### 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可以實作[`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html)或[`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html)服務介面，並將實作註冊為OSGI服務。 這些實施（如果可用）會取代已設定的預先定義格式。 如果註冊了多個實作，則服務排名較高的實作會取代服務排名較低的實作。

自訂URL格式實作必須實作一對方法，用於從指定引數建置URL並剖析URL以分別傳回相同的引數。

### 與Sling對應結合 {#sling-mapping}

除了`UrlProvider`之外，也可以設定[Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)來重寫及處理URL。 AEM Archetype專案也提供[範例設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以為連線埠4503 （發佈）和80 (Dispatcher)設定一些Sling對應。

### 與AEM Dispatcher結合 {#dispatcher}

也可以使用具有`mod_rewrite`模組的AEM Dispatcher HTTP伺服器來完成URL重寫。 [AEM專案原型](https://github.com/adobe/aem-project-archetype)提供參考的AEM Dispatcher設定，其中已包含產生大小的基本[重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 最佳實務 {#best-practices}

### 選擇最佳的URL格式 {#choose-url-format}

如在選取其中一個可用的預設格式，或甚至實施自訂格式之前所述，這在很大程度上取決於商店的需求和要求。 下列建議可能有助於做出有教育意義的決定。

_&#x200B;**使用包含SKU的產品頁面URL格式。**&#x200B;_

CIF核心元件會使用SKU作為所有元件的主要識別碼。 如果產品頁面URL格式不包含SKU，則需要使用GraphQL查詢來解析。 此解析度可能會影響第一個位元組的時間。 此外，購物者可能希望能夠使用搜尋引擎透過SKU尋找產品。

_&#x200B;**使用包含類別內容的產品頁面URL格式。**&#x200B;_

CIF URL Provider的某些功能只有在使用產品URL格式時才能使用，這些格式會編碼類別內容，例如類別`url_key`或類別`url_path`。 即使新商店可能不需要這些功能，一開始便使用其中一種URL格式有助於減少未來的移轉工作。

_&#x200B;**在URL長度和編碼資訊之間取得平衡。**&#x200B;_

視目錄大小（尤其是類別樹狀目錄的大小和深度）而定，將完整的`url_path`個類別編碼到URL中可能不太合理。 在這種情況下，可以只包含類別的`url_key`來縮短URL長度。 此方法支援使用類別`url_path`時可用的大部分功能。

此外，請使用[Sling對應](#sling-mapping)將SKU與產品`url_key`結合。 在大多數電子商務系統中，SKU會遵循特定格式，因此很容易就能將傳入請求的SKU與`url_key`分開。 考慮到這一點，應該可以將產品頁面URL重寫為`/p/{{category}}/{{sku}}-{{url_key}}.html`，並將類別URL分別重寫為`/c/{{url_key}}.html`。 若要將產品和類別頁面與其他內容頁面區分開來，仍需使用`/p`和`/c`首碼。

### 移轉至新的URL格式 {#migrate-url-formats}

許多預設URL格式以某種方式彼此相容，這表示某一種格式的URL可能會被另一種格式剖析。 這有助於在URL格式之間移轉。

另一方面，搜尋引擎需要時間來重新耙梳所有具有新URL格式的目錄頁面。 為了支援此流程並改善一般使用者體驗，建議提供將使用者從舊URL轉送到新URL的重新導向。

其中一種方式可能是將預備環境連線到生產電子商務後端，並將其設定為使用新的URL格式。 然後取得由CIF產品Sitemap產生器[針對預備和生產環境產生的](../../overview/seo-and-url-management.md)產品Sitemap，並使用它們來建立[Apache httpd重寫對應](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html)。 然後，可將此重寫對應與新URL格式的推出一起部署到Dispatcher。

## 範例 {#example}

[Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)專案包含範例設定，以示範產品和類別頁面使用自訂URL的情況。 此設定可讓每個專案根據其SEO需求，為產品和類別頁面設定個別URL模式。 如上所述，已使用CIF `UrlProvider`和Sling對應的組合。

>[!NOTE]
>
>此設定必須使用專案使用的外部網域進行調整。 Sling對應是根據主機名稱和網域來運作。 因此，此設定預設為停用，必須在部署之前啟用。 若要這麼做，請根據使用的網域名稱重新命名`hostname.adobeaemcloud.com`中的Sling對應`ui.content/src/main/content/jcr_root/etc/map.publish/https`資料夾，並將`resource.resolver.map.location="/etc/map.publish"`新增到專案的`JcrResourceResolver`設定中來啟用此設定。

## 其他資源 {#additional}

* [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=zh-Hant)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
