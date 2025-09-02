---
title: 使用具備OpenAPI功能的Dynamic Media最佳化影像
description: 瞭解如何在公開傳送前使用Dynamic Media的影像最佳化功能搭配OpenAPI功能即時最佳化影像
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 5a01aff1d6c10d86e2faef22da2dbe724e24e673
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# 使用具備OpenAPI功能的Dynamic Media最佳化影像{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]提供影像最佳化功能，例如[!DNL Smart Crop]、[!DNL Image Presets]和[!DNL Smart Imaging]。 這些功能有助於提供高品質、回應式影像，並快速載入不同的裝置和網路。

## 智慧裁切{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[智慧型裁切](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)是[!DNL Dynamic Media with OpenAPI capabilities]的動態大小調整功能。 [!DNL Smart Crop]是進階的影像處理技術，它使用AI支援的內容感知裁切功能，以智慧方式裁切各種熒幕大小的影像，同時保留裁切版本中的視覺內容。 AI會分析影像以識別焦點或預期興趣點，然後自動裁切影像以保留所有裁切版本中的焦點。 [!DNL Smart Crop]是回應式設計的關鍵元素，提供符合成本效益且符合時間效率的方式裁切影像。

請參閱[Dynamic Media影像設定檔](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles)文章以瞭解如何在[中](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles)建立智慧型裁切轉譯[!DNL Admin View]、[將其套用至資料夾](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders)或[編輯轉譯](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image)已套用至影像或資料夾。 瞭解如何在此[!DNL Smart Crop]影片[中逐步建立](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)。

[!DNL Smart Crop]引數預期named-smartcrop-profiles存在且已套用至資產。 請參閱[智慧型裁切設定檔](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)以進一步瞭解[!DNL Smart Crop]引數以及名稱[!DNL Smart Crop]設定檔的套用方式。

>[!IMPORTANT]
>
> 您只能在管理員檢視中建立[!DNL Smart Crop]轉譯。

## 影像預設集{#image-presets-using-dynamic-media-with-openapi-capabilities}

在[中使用](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request)影像預設集[!DNL Dynamic Media with OpenAPI capabilities]功能即時轉換影像。 [!DNL image preset]是一組預先定義的輸出影像大小調整與格式設定規則。

[!DNL Dynamic Media with OpenAPI capabilities]會使用預設名稱即時轉換影像並立即產生其轉譯。 當您透過包含預設集引數的[!DNL Dynamic Media with OpenAPI]傳遞URL要求影像時，[!DNL DM with OpenAPI]會套用預設集的轉換、依需求建立轉譯，並將其傳遞給使用者。

您可以透過影像的[!DNL Dynamic Media with OpenAPI]傳遞URL，將單一預設集套用至多個影像。 這可確保跨資產的一致格式，無需手動編輯每個資產。

請參閱[管理影像預設集](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets)文章以瞭解[如何在管理員檢視中建立影像預設集](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets)，以及[如何建立可自動調整資產以符合不同熒幕大小的回應式影像預設集](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset)。

### 使用影像預設集的好處{#benefits-of-image-presets}

[!DNL Image Presets]在[!DNL Dynamic Media with OpenAPI]中管理和傳遞影像有幾項優點。 主要優點包括：

* 預設集會縮短影像傳送URL。 請使用單一預設集，而非新增多個影像修飾元來拉長傳送URL。 較短的URL更容易管理，並確保跨網站、行動應用程式、電子郵件和其他頻道的一致影像傳送。
* 影像預設集會從來源影像檔案中建立即時轉譯。 這種隨選轉譯產生功能消除了建立並儲存相同檔案的多個靜態轉譯的需求，同時節省了時間和儲存空間。
* 一次將單一預設集套用至大型資產集，避免個別手動編輯每個資產，確保一致的格式並啟用擴充性。
* 當您更新預設集的引數時，使用該預設集的所有影像都會自動重新格式化。 透過集中格式更新，這簡化了編輯，無需重新編輯個別資產或網頁程式碼。
* 透過CDN快取的動態轉譯來提升效率和效能，進而加快載入速度，並在裝置和網路間最佳化效能。

### 使用影像預設集{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

建立[!DNL Image Presets]後，您便可將它們用於下列工作流程：

* [在影像傳送URL中使用預設集來即時建立其轉譯，然後再傳送給一般使用者](#use-presets-in-delivery-urls)
* [在AEM Sites中製作時使用預設集](#use-presets-during-authoring-in-aem-sites)

#### 在影像傳送URL中使用預設集{#use-presets-in-delivery-urls}

預設集可讓您的傳送URL變得更短且易於使用。  每個預設集名稱都會當作傳遞URL中的唯一識別碼。 請參考預設集名稱，立即產生其轉譯，而不是將多個修飾元新增到資產的傳送URL。 [瞭解如何將Dynamic Media影像預設集套用至您的影像](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets)。
以下範例將具有預設集的URL與沒有預設集的URL進行比較。

**沒有預設集的URL （長URL）**：

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true
```

**具有預設集的URL （簡短URL）**：

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail
```

預設集縮圖會繫結相同的影像修飾元設定。

#### 在AEM Sites中製作時使用預設集{#use-presets-during-authoring-in-aem-sites}

啟用[!DNL Image Presets]支援時，作者可以在[!DNL AEM Sites]編寫頁面中選取[!DNL Dynamic Media]進行頁面編輯。

執行以下步驟，以在編寫頁面中使用影像預設集：

1. 導覽至您的「網站」撰寫頁面。
1. 執行[存取AEM頁面編輯器中的遠端資產](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor)區段中的步驟，以使用[!DNL Asset Selector]面板來選取資產。
1. 在[!DNL asset selector]面板中，向下捲動至&#x200B;**[!UICONTROL 預設集型別]**，並在`Preset=Preset Name`影像修飾元&#x200B;**[!UICONTROL 欄位中指定]**。

   ![預設集](/help/assets/assets/preset-in-asset-selector-panel.png)

## 智慧型影像處理{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

當您使用[!DNL Dynamic Media with OpenAPI capabilities]傳送影像時，影像會透過[智慧型影像](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/?lang=zh-Hant)自動最佳化。 最佳化的傳送方式可確保影像載入更快、視覺品質最佳，且檔案大小最少。 如此一來，各個裝置和網路的頁面載入速度最快，視覺品質也始終如一，同時耗用最少的頻寬，讓您的網站更快速、回應更迅速。

[!DNL Smart Imaging]包含下列功能：

* [自動格式轉換](#auto-format-conversion)
* [網路頻寬最佳化](#network-bandwidth-optimisation)

### 自動格式轉換{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [會自動將影像轉換為現代的、網頁最佳化的格式，例如AVIF或WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request)。 轉換取決於瀏覽器的功能和[授權權利](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)，無論請求的格式為何。

AVIF和WEBP格式提供更好的壓縮，讓影像變得更小、傳送和載入更快。 AVIF在處理所有瀏覽器功能時會用作預設格式。

[!DNL Dynamic Media with OpenAPI]使用`auto-format`查詢引數來控制將影像轉換為各種格式以進行最佳化傳遞的瀏覽器行為。 自動格式轉換包含&#x200B;**自動促銷**&#x200B;和&#x200B;**自動降級**。 當系統透過JPEG或PNG促銷網頁最佳化格式（AVIF或WEBP）以進行傳送時，這稱為自動促銷。

根據預設，`auto-format`查詢引數設定為`true`。 啟用`auto-format` (true)時，系統會忽略要求的格式，並根據影像特性、瀏覽器功能和[授權權利](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)自動選取網頁最佳化格式（AVIF或WEBP）。

當`auto-format`為true時，系統會依下列順序傳送影像格式：

* ***AVIF***：如果瀏覽器支援AVIF，而且授權允許，就會傳送AVIF。 這稱為自動促銷活動。
* ***WEBP***：如果AVIF不受支援或授權，則會傳送WEBP。 這也稱為自動促銷活動。
* ***JPEG***：只有在不支援AVIF和WEBP時，才會傳送JPEG，而且影像沒有Alpha色版（透明度）。 這稱為自動降級。
* ***PNG***：瀏覽器不支援新式格式，且影像有Alpha色版（透明度）時，會傳送PNG。 這也稱為自動降級。

將查詢引數設定為`auto-format`以停用`false`，然後指定所需的格式，以取得該格式傳送的影像。

### 網路頻寬最佳化{#network-bandwidth-optimisation}

影像會根據使用者端的網路狀況自動最佳化，以確保更快速的傳送和平順的載入。 [Quality](#quality-parameter)和[Max-quality](#max-quality-parameter)引數會藉由控制影像壓縮等級來自動調整品質，其值範圍介於1到100之間。

檢視`quality`和`max-quality `引數的下列主要行為：

* 如果同時指定[!DNL quality]和[!DNL max-quality]，則會以[!DNL quality]優先。
* 如果只指定[!DNL quality]，則不論載入時間為何，都會根據網路速度傳送品質。
* 如果只指定[!DNL max-quality]，則影像品質會根據網路狀況自動調整，提供最佳品質至指定[!DNL max-quality]值。
* 若兩者皆未指定，系統會套用預設值`max-quality`為`85`的動態最佳化。

#### 品質引數{#quality-parameter}

品質引數會將影像品質優先於載入速度。 它會將輸出影像品質修正為要求的值（介於1到100之間）並忽略網路條件。 深入瞭解[品質引數](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)。

#### Max-quality引數{#max-quality-parameter}

最大品質會根據使用者端的網路速度來平衡影像品質和載入時間。 它藉由降低較慢網路上的影像品質來排定較快的載入時間，同時仍提供特定網路狀況下的最高品質(1-100)。 深入瞭解[max-quality引數](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)。
