---
title: 使用具OpenAPI功能的Dynamic Media建立虛名URL
description: 使用Dynamic Media OpenAPI功能，將您長時間的資產傳送URL轉換為簡短且具品牌的虛名URL。 虛名URL是您複雜傳送URL的簡短、乾淨、容易記住及可讀版本。 您可以在虛名URL中納入您的品牌名稱、產品名稱和相關關鍵字，以提高您的品牌曝光度和使用者參與度
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 73574b3358451dfe135b91011abb5cad372a783e
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---


# 使用虛名URL？{#vanity-urls}

使用[!DNL Dynamic Media OpenAPI capabilities]將您長長的資產傳遞URL轉換成短的、品牌化的虛名URL。 標準資產傳送URL包含系統產生的資產UUID，使傳送URL複雜、難以記憶和共用。 以簡單識別碼（虛名ID）取代這些資產UUID，以產生虛名URL。 虛名URL是複雜傳送URL的簡短、乾淨和可讀版本。

請參閱下列URL格式以瞭解其差異：
* [標準傳遞URL](#standard-urls)
* [虛名 URL](#vanity-url)

標準傳遞URL使用`aaid`，後接UUID，而虛名URL使用`avid`，後接自訂識別碼（虛名識別碼）。

使用簡短且簡單的虛名識別碼，讓您的傳送URL簡短易懂，容易記憶和分享。 使用您的品牌名稱、產品名稱和相關關鍵字作為虛名ID，以提高您的品牌曝光度和使用者參與度。

當您的使用者按一下您的虛名URL時，[!DNL Dynamic Media with OpenAPI]會在擷取時自動對應到原始資產位置，並在傳送時正確解析這些位置，以將資產伺服給使用者。

瞭解[建立虛名URL](#create-vanity-urls)。

## 標準傳送URL{#standard-urls}

標準[!DNL Dynamic Media with OpenAPI]資產傳遞URL包含系統產生的唯一識別碼，並遵循以下格式。

***格式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

標準傳遞URL包含`aaid`之後的&#x200B;*（*&#x200B;實際資產識別碼`urn:`）以及介於`urn:aaid:aem:`和`/as/<seoname>.<format>`之間的UUID。

***範例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

在上述範例中，`43341ab1-4086-44d2-b7ce-ee546c35613b`是UUID。

## 虛名 URL{#vanity-url}

虛名URL包含虛名識別碼以取代資產UUID，並遵循以下格式。

***格式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

虛名URL包含`avid`之後的&#x200B;*（*&#x200B;實際的虛名識別碼`urn:`）以及介於`urn:avid:aem:`到`/<seoname>.<format>`之間的虛名ID。

***範例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

在上述範例中，`VanityCheck`是取代UUID的虛名ID。

## 探索主要功能與優勢{#capabilities-and-benefits-of-vanity-urls}

使用有意義的虛名ID來自訂標準資產傳送URL，有幾項好處和可以測量的影響。 虛名URL的某些主要功能和優點包括。

### 主要功能{#key-capabilities}

* **URL自訂：**&#x200B;以較短且符合品牌規範的替代專案，取代傳遞URL中的長識別碼（資產UUID），以產生更乾淨的傳遞URL。
* **即時重新導向：**&#x200B;虛名URL會在執行階段重新導向至原始資產UUID，而不會中斷工作流程。 當系統處理技術路由時，使用者會在位址列中看到乾淨的URL。
* **輕鬆的連結管理：**&#x200B;隨時自訂您的虛名URL，而不會影響資產傳遞效能。

### 主要優點{#key-benefits}

* **增強使用者體驗：**&#x200B;清爽且較短的虛名URL可讀取、方便使用、容易記憶和分享。

* **改善使用者參與度：**&#x200B;品牌URL建立使用者信賴度和信任。 使用者更容易點選專業品牌連結，導致更高的點進率。

* **SEO最佳化：**&#x200B;包含相關關鍵字的URL可改善搜尋引擎排名和可發現性。

* **增強的品牌可見度：**品牌專屬URL可加強所有行銷管道（包括電子郵件、社群媒體和廣告行銷活動）中的品牌存在。
此外，在所有通訊中持續使用品牌URL可強化品牌識別與認可。

* **行銷活動追蹤和分析：**&#x200B;針對不同的行銷活動和管道使用唯一的虛名URL，以取得流量來源和轉換績效的詳細深入分析。

## 先決條件{#prerequisites-for-creating-vanity-id}

若要建立虛名URL，請確定您已[核准要公開傳遞的資產](/help/assets/manage-organize-assets-view.md#manage-asset-status)。

## 建立虛名URL{#create-vanity-urls}

執行以下步驟來建立虛名URL：
1. [設定資產中繼資料](#set-up-asset-metadata)
1. [建立和對應Cloud Manager環境變數](#map-cloud-manager-environment-variable)
1. [核准需要虛名URL以進行傳送的資產](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [產生虛名URL](#generate-vanity-urls)

### 設定資產中繼資料{#set-up-asset-metadata}

執行以下命令，在資產的中繼資料表單中設定虛名ID：
1. 導覽至含有[!DNL Dynamic Media with OpenAPI]傳遞之資產的資料夾的詳細資訊頁面。
1. [執行下列其中一項動作，編輯該中繼資料表單](/help/assets/metadata-assets-view.md#edit-metadata-forms)：
   * 新增中繼資料欄位，並將必要的虛名ID指定為該欄位的值。
   * 將現有中繼資料屬性的值取代為必要的虛名ID，以更新現有欄位。 瞭解建立虛名ID的[最佳做法](#best-practices)。
     ![虛名ID](/help/assets/assets/vanity-id-metadata.png)
深入瞭解[中繼資料結構](/help/assets/metadata-schemas.md)。

     >[!NOTE]
     >
     > * 對每個資產使用唯一的虛名ID。 一律確認共用相同中繼資料表單的資產具有唯一虛名ID，適用於DM搭配OpenAPI透過虛名URL傳送。 如果兩個資產共用相同的虛名ID，具有OpenAPI的DM會傳送最近收到該ID的資產，並覆寫該ID先前對另一個資產的權益。
     >
     > * 單一資產可以有多個虛名ID。 [連絡Adobe支援](https://helpx.adobe.com/in/contact.html)並提出產生所需虛名ID的請求。

在資產中繼資料表單中設定虛名ID後，[將此中繼資料欄位對應到系統的傳遞機制](#map-cloud-manager-environment-variable)。

### 建立和對應Cloud Manager環境變數{#map-cloud-manager-environment-variable}

執行以下步驟來建立環境變數，並將其對應至儲存虛名ID的中繼資料欄位：

1. [瀏覽至Cloud Manager環境的設定頁面](/help/implementing/cloud-manager/environment-variables.md)，並執行下列動作：
   1. 新增`ASSET_DELIVERY_VANITY_ID`變數。 這是索引鍵。
   1. 使用值欄位來對應到儲存虛名ID的中繼資料屬性。 對應遵循`dc:<your-metadata-property>`格式，其中中繼資料對應首碼（例如dc：）會根據您的中繼資料組態屬性而有所不同。
      ![ASSET_DELIVERY_VANITY_ID變數](/help/assets/assets/environment-config.png)
1. 儲存變更以重新啟動環境中的Pod。

### 核准要傳送的資產{#approve-assets-for-delivery}

將您Cloud Manager環境中的`ASSET_DELIVERY_VANITY_ID`變數對應到儲存虛名ID的資產中繼資料屬性後，[核准您需要虛名URL才能傳送的資產](/help/assets/manage-organize-assets-view.md#manage-asset-status)。

### 產生虛名URL{#generate-vanity-urls}

在您的標準傳送URL中進行下列取代操作，以將它轉換為虛名URL：

* 將&#x200B;**UUID**&#x200B;取代為您的&#x200B;**虛名ID**。
* 以`aaid`取代`avid`。

請參閱上述[URL從標準到虛名URL的轉換](#standard-urls)。
瞭解如何[複製您資產的Dynamic Media （含OpenAPI傳遞URL）](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets)。

當您的使用者按一下虛名URL時，[!DNL Dynamic Media with OpenAPI]會在擷取時將虛名ID自動對應到原始資產UUID，並在傳送時正確解析它們，以便毫不延遲地向使用者提供資產。 您可以即時自訂虛名URL，而不會影響資產傳送效能。

[使用AEM雲端服務的進階自訂功能，增強虛名URL的影響。](#scale-using-vanity-url)

## 使用虛名URL擴展{#scale-using-vanity-url}

AEM as a Cloud Service可讓您[自訂您網址內的DNS和CDN名稱](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction)。 使用這些AEMCS功能搭配您的虛名URL，將其轉換為簡潔的、描述性的、品牌化的、直覺式的唯一網址，並提供上述[優點](#key-benefits)。

請參閱下列虛名URL及其可自訂的元件：

**虛名URL格式：**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">自訂此DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">使用重寫規則自訂URL</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">建立虛名ID</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**具有自訂DNS和CDN名稱的虛名URL格式：**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/<seoname>.<format>`

**可自訂的URL元件**

* ***[DNS名稱（主機名稱）：](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com`是託管您資產的伺服器網域。 [自訂DNS以變更主機名稱](#customize-DNS)。
* ***[CDN重寫規則：](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:`是識別資產型別和傳遞方法的路徑結構。 [重寫CDN規則](#rewrite-cdn-rules)以修改網域路徑。

### 自訂DNS{#customize-dns}

[向Adobe支援提出要求](https://helpx.adobe.com/in/contact.html)，為您的傳遞層級產生所需的自訂DNS。 請依照這些[最佳實務](#best-practices)建立自訂DNS名稱。

### 重寫CDN規則{#rewrite-cdn-rules}

執行以下步驟來重寫要傳送的CDN規則：

1. 導覽至您的AEM存放庫以建立YAML設定檔。
2. 執行[設定](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup)區段中的步驟以設定CDN規則，並透過Cloud Manager設定管道部署設定。
按照這些[最佳實務](#best-practices)建立您的網域路徑。
   [進一步瞭解CDN重寫規則](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)。

以下是重寫規則的範例，這些規則用於以虛名URL附加副檔名的檔案名稱。 根據您的特定需求自訂這些重寫規則。 [聯絡Adobe支援](https://helpx.adobe.com/in/contact.html)以取得進一步協助：

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### 適用於SVG、GIF和PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### 視訊{#video}

視訊包括MP4、MOV、AVI和MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### 針對影像{#image}

適用於所有影像型別，不包括SVG。

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## 遵循建立乾淨虛名URL的最佳實務{#best-practices}

請遵循以下最佳實務來建立虛名ID、自訂DNS和網域名稱：

1. 請勿在虛名ID中使用特殊字元，例如空格、斜線、連字型大小等。 系統會使用預先定義的對應來取代虛名ID中的特殊字元。
1. 在虛名ID、自訂DNS和網域名稱中使用您的品牌名稱、產品名稱和相關關鍵字，以提高您的品牌曝光度和使用者參與度。
1. 使用簡短的描述性字詞或字串來傳達意義。
1. 使用邀請使用者點按的文字。
