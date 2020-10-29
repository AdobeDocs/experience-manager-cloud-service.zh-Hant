---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 這可讓實作最佳化搜尋引擎的URL，並促進搜尋。
sub-product: 商務
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---


# 進階URL設定 {#url}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) （AEM CIF核心元件）提供進階設定，可自訂產品和類別頁面的URL。 許多實作將自訂這些URL以用於搜尋引擎最佳化(SEO)。  以下視訊詳細資訊如何設定 `UrlProvider` Service和 [](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) Sling Mapping的功能，以自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要根據 `UrlProvider` SEO要求設定服務，而且需要專案必須針對「CIF URL提供者設定」設定提供OSGI設定，並依下列說明設定服務。

>[!NOTE]
>
> Venia Reference [store專案](https://github.com/adobe/aem-cif-guides-venia) （請參閱下文）包含範例組態，以示範產品和類別頁面的自訂URL使用情形。

### 產品頁面URL範本 {#product}

這會使用下列屬性來設定產品頁面的URL:

* **產品URL範本**:定義具有一組佔位符的URL格式。 預設值為 `{{page}}.{{url_key}}.html#{{variant_sku}}`，最後會產生URL，例如 `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`
   * `{{page}}` 替換為 `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 已由產品的 `url_key` 屬性取代，此處 `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 已由目前選取的變體取代，此處 `MH01-M-Orange`
* **產品識別碼位置**:定義用來擷取產品資料之識別碼的位置。 預設值為 `SELECTOR`，其它可能值為 `SUFFIX`。 在上一個範例URL中，這表示識 `chaz-kangeroo-hoodie` 別碼將用來擷取產品資料。
* **產品識別碼類型**:定義擷取產品資料時要使用的識別碼類型。 預設值為 `URL_KEY`，其它可能值為 `SKU`。 在上一個範例URL中，這表示產品資料將會以Magento GraphQL篩選器擷取，如 `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`下。

### 產品清單頁面URL範本 {#product-list}

這會使用下列屬性來設定類別或產品清單頁面的URL:

* **類別URL範本**:定義具有一組佔位符的URL格式。 預設值為 `{{page}}.{{id}}.html`，最後會產生URL，例如 `/content/venia/us/en/products/category-page.3.html`
   * `{{page}}` 替換為 `/content/venia/us/en/products/category-page`
   * `{{id}}` 已由類別的 `id` Magento屬性取代，此處 `3`
* **類別識別碼位置**:定義用來擷取產品資料之識別碼的位置。 預設值為 `SELECTOR`，其它可能值為 `SUFFIX`。 在上一個範例URL中，這表示識 `3` 別碼將用來擷取產品資料。
* **類別識別碼類型**:定義擷取產品資料時要使用的識別碼類型。 預設值和目前僅支援的值為 `ID`。 在上一個範例URL中，這表示類別資料將會以Magento GraphQL篩選器擷取，如 `category(id:3)`下。

只要使用的元件正在設定對應的資料，就可以為每個範本新增自訂屬性 `UrlProvider`。 檢查類的代碼示例， `ProductListItemImpl` 瞭解如何實現此類。

您也可以將服務取代 `UrlProvider` 為完全自訂的OSGi服務。 在這種情況下，必須實作介 `UrlProvider` 面，並以較高的服務排名來註冊它，以取代預設實作。

## 與Sling Mappings結合 {#sling-mapping}

除了此 `UrlProvider`外，您也可以設定 [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) ，以便重寫和處理URL。 AEM Archetype專案也提供 [範例設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) ，以設定埠4503(publish)和80(dispatcher)的某些Sling Mappings。

## 與AEM Dispatcher結合 {#dispatcher}

URL重寫也可以透過搭配使用AEM Dispatcher HTTP伺服器與模組來 `mod_rewrite` 完成。 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) provides a reference AEM Dispatcher config already includes [basic rewrite rules](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) for the generated size.

## 範例

Venia Reference [store專案包含範例設定](https://github.com/adobe/aem-cif-guides-venia) ，以示範產品和類別頁面的自訂URL使用情形。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別的URL模式。 使用CIF和Sling `UrlProvider` 映射的組合，如上所述。

>[!NOTE]
>
>此配置必須與項目使用的外部域一起調整。 Sling Mappings會根據主機名稱和網域運作。 因此，此配置預設為禁用，在部署之前必須啟用。 若要這麼做，請根據使用的網 `hostname.adobeaemcloud.com` 域名稱，在中重 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 新命名Sling Mapping資料夾，並新增至專案 `resource.resolver.map.location="/etc/map.publish"` 的 `JcrResourceResolver` 設定以啟用此設定。

## 其他資源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
