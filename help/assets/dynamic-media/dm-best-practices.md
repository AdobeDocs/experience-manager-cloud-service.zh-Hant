---
title: Dynamic Media 最佳實務
description: 瞭解使用影像和影片的Dynamic Media最佳實務。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: de1116ee39024d30e14838f8b36f9ab087a45f85
workflow-type: tm+mt
source-wordcount: '3571'
ht-degree: 0%

---

# Dynamic Media 最佳實務{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

組織在與使用者互動時，面臨著頻道和裝置的爆炸式增長。 客戶歷程橫跨實體商店、網路、行動裝置、社群媒體、電子郵件和商務。 為滿足此需求，Adobe Experience Manager (AEM)上的Dynamic Media提供全方位的解決方案。 它會最佳化資產傳送、處理個人化，並確保跨頻道和裝置的一致性、效能表現和品牌一致性體驗。

Dynamic Media的部分主要原則包括：

* **單一檔案方法：** 透過Dynamic Media，您可以儲存一個主要來源檔案，並在傳送時動態建立並最佳化所有大小變化和視覺效果。 此方法可節省儲存成本並免除工作流程的複雜性。
* **真正的全球化：** 智慧型影像在內容傳遞期間套用，可大幅減少影像大小和頁面寬度，而不會影響視覺品質。 針對網路頻寬和裝置畫素比例進行最佳化。
* **AI支援：** 智慧型裁切是AI驅動的功能，可自動裁切影像和視訊地標。 它省去了手動操作，並有效率地擴充以供企業使用。
* **簡易影片：** 將主要來源影片上傳到Dynamic Media，並使用描述性音訊以自適應的方式在多種語言間串流。
* **體驗檢視器資料庫：** 自訂影像和影片的品牌體驗檢視器。 這些檢視器可順暢地整合至您的數位體驗。
* **新興格式支援：** Dynamic Media可提供3D與全景體驗。

當您探索 [Dynamic Media歷程](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1)，檢閱下方最佳實務的彙總清單可協助您充分運用其功能。 調整這些Dynamic Media最佳實務，以符合您的特定內容和專案需求，這樣您就可以跨管道和裝置最佳化您的體驗。

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>本文中的Dynamic Media最佳實務可能會隨著Dynamic Media中新技術的出現而逐漸演變。 最新版Dynamic Media的最新資訊如下。


## 將資產內嵌至Dynamic Media

**業務案例：** *有效管理大量資產，並確保只將相關、經核准的內容提供給一般使用者。*

有效簡化您對大量資產的管理。 使用Dynamic Media的 **選擇性同步** 和 **選擇性發佈** 功能。

* **選擇性同步：**
主動式功能，可讓您選擇要與Dynamic Media同步的資產。 例如，您可能決定只同步處理包含已獲得最終核准之資產的資料夾。 此工作流程可協助您持續控制正在準備傳送給客戶的資產。

* **選擇性發佈：**
同步您的資產後，選擇性發佈可讓您控制哪些資產可向客戶顯示。 此功能表示您可以控管哪些已核准資產是實際透過您的管道傳送，確保您的客戶只會看到最佳且最相關的內容。

這兩個最佳實務可協助您對多媒體內容進行更好的控制、控管和生產力。

想要進一步瞭解嗎？ 前往 [在Dynamic Media中設定資料夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md).


## 準備資產以進行傳送

### 組織您的資產

**業務案例：** *有效率地組織資產以簡化工作流程。*

為有效率地組織資產並簡化工作流程，請使用下列一或多個最佳實務：

* **組織資料夾中的資產：**
有效地組織資產包括將資產分類到資料夾中，類似於電腦上的檔案組織。 正確的命名、建構子資料夾以及這些資料夾內的檔案管理，對有效率地處理資產而言至關重要。 實作系統化的命名慣例和中繼資料作法可讓您的數位資產存放庫發揮最大效用。
想要進一步瞭解嗎？ 前往 [組織資料夾中的資產](/help/assets/organize-assets.md#organize-using-folders).
* **使用標籤來組織資產：**
為資產加上標籤可增強搜尋能力、集合建立和搜尋排名。 Adobe Sensei的AI採用自我學習演演算法來進行精確標籤，進而實現快速資產擷取。 Adobe Sensei也會辨識並指派相關標籤（包括自訂標籤）給資產，以使用自動的描述性標籤來簡化資產管理。
想要進一步瞭解嗎？ 前往 [使用標籤組織資產](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **將資產組織為集合：**
Dynamic Media搭配Experience Manager Assets可讓使用者之間有效率地建立、編輯和共用資產集合。 您可以建立各種集合型別，包括靜態清單和以搜尋為基礎的動態編譯。 這些集合型別可以透過可自訂的存取及編輯許可權在多種位置共用。
想要進一步瞭解嗎？ 前往 [將資產組織為集合](/help/assets/manage-collections.md).
* **使用設定檔組織資產：**
處理設定檔可自動處理指定資料夾中的資產，精簡組織。 隨著數位資產集合的擴展，標準化中繼資料、檔案名稱和檔案夾結構可讓您一致且精確地應用這些設定檔。
想要進一步瞭解嗎？ 前往 [使用設定檔組織資產](/help/assets/organize-assets.md#organize-to-use-profiles).



### 最佳化影像品質

**業務案例：** *從Dynamic Media取得高品質影像。*

提升影像品質需要仔細考量各種因素。 此過程需要大量時間。 不過，有一些經過實踐檢驗的實務可以協助您取得理想的結果。 其中一些最佳實務包括如何取得最佳影像大小、影像銳利化及要使用的最佳影像格式。

想要進一步瞭解嗎？ 前往 [影像品質最佳化的最佳作法](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

由於對影像品質的感知會因人而異，有時候，系統性的實驗方法對於取得理想的結果至關重要。 Adobe Experience Manager使用100多個Dynamic Media命令來協助此程式，以進行影像增強。

想要進一步瞭解嗎？ 觀看 [Dynamic Media快照](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) （3分17秒）。

若要評估這些不同命令對影像品質的影響，您可以將影像上傳到Dynamic Media、在指定的URL使用工具的介面，然後套用您要嘗試的命令。

要試試嗎？ Launch [Dynamic Media快照](https://snapshot.scene7.com/)

### 標準化套用至影像的樣式

**業務案例：** *以高效率標準化套用至影像資產的樣式和轉換。*

在Dynamic Media中定期使用影像預設集，以便您可以一致且動態地調整影像大小、格式和屬性。 將影像預設集想像成一個巨集：這是一組已命名的指令，用於調整大小和格式設定。 例如，如果您的網站需要各種大小和格式的產品影像，並針對桌上型電腦和行動裝置進行特定壓縮，則影像預設集可有效自動化此程式。

要試試嗎？ 前往 [建立影像預設集以轉譯資產的基礎知識](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### 調整影像和影片的焦點與框架

**業務案例：** *確保影像或影片的主要興趣點在裝置間保持焦點。*

智慧型裁切是Dynamic Media中的一項功能，可利用Adobe的AI和機器學習架構Adobe Sensei來自動裁切影像和視訊。 它會聰明地偵測並聚焦於影像或視訊中的主要主題或興趣點。 這項智慧可確保焦點在桌上型電腦和行動裝置上的各種熒幕大小之間維持不變。

最佳實務是使用智慧型裁切建立影像設定檔。 在設定檔中，您可以定義各種熒幕大小並讓Adobe Sensei執行其餘工作，以確保您的影像和視訊一律為檢視者的裝置最佳化。

想要進一步瞭解嗎？ 觀看 [搭配AEM Assets Dynamic Media使用智慧型裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) （6分35秒）和 [針對視訊使用Dynamic Media智慧型裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) （6分22秒）。

### 改善SEO排名

**業務案例：** *設定Dynamic Media以改善SEO排名。*

請定期使用下列建議，以確保您的影像可有效地對您的整體SEO策略作出貢獻。

* **有意義的影像檔案名稱：**
使用可反映影像內容的描述性檔案名稱。 例如，
   * 使用 `myCompany-Silver-Wrist-Watch`
   * *避免* `myCompany_Silver_Wrist_Watch` 或 `myCompanySilverWristWatch`

  這麼做有助於搜尋引擎瞭解影像內容並改善SEO。 在檔案名稱中，Google偏好使用連字型大小而非底線或空格。 此外，請避免在檔案名稱中串連字詞。
* **自訂網域：**
實作包含您公司或品牌名稱的自訂網域，以強化品牌認知度和信任。 例如，
   * 使用 `http://images.mycompany.com/is/image/companyname/`
   * *避免* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`
* **SEO友善的資料夾結構：**
以包含公司名稱或品牌的資料夾結構來組織您的影像，以獲得更好的索引，例如 `http://images.mycompany.com/is/image/companyname/`.
* **Dynamic Media規則集：**
瞭解如何根據各種因素有條件地轉換URL，以增強SEO和使用者體驗。
想要進一步瞭解嗎？ 前往 [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **智慧型影像與智慧型裁切：**
使用Dynamic Media中的智慧型影像和智慧型裁切功能，提供最佳化和回應式影像。 這麼做不僅可改善頁面載入時間，也會對SEO排名產生正面影響。
想要進一步瞭解嗎？ 前往 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md)，或觀看 [搭配AEM Assets Dynamic Media使用智慧型裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) （6分35秒）。

請記住，這些最佳作法與Google的影像SEO最佳作法高度一致。 這些做法強調透過適當的命名慣例、結構化資料和最佳化的影像傳送，為搜尋引擎提供內容和清晰度的重要性。

想要進一步瞭解嗎？ 前往 [Google的URL結構最佳實務](https://developers.google.com/search/docs/crawling-indexing/url-structure) 和 [Google影像SEO最佳作法](https://developers.google.com/search/docs/appearance/google-images)


### 使用命令動態增強影像並建立視覺效果

**業務案例：** *將豐富的視覺效果套用至影像。*

Dynamic Media提供一套命令，用於增強影像以及動態建立視覺效果，而不需要多個靜態資產。 以下簡要說明其中一些流程，並提供一些範例來指導您：

#### 來源影像內的效果

| 任務 | 該做什麼 |
| --- | --- |
| **上傳並發佈原始影像** | ·首先，將原始影像上傳至Dynamic Media。<br>·請確定已發佈並可透過URL存取。<br>·在此範例中，具有白色背景的手錶的庫存影像（我們將其稱為「影像X」）會上傳至Dynamic Media。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer) |
| **建立遮色片** | ·開發定義主旨（要套用效果的區域）和背景（要變更的區域）的遮色片。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)<br>·遮色片通常是灰階影像，其中白色代表主題，黑色代表背景。 您可以使用Adobe Photoshop等工具建立遮色片。<br>想要進一步瞭解嗎？ 前往 [在Photoshop中建立和編輯快速遮色片](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).<br>·對於「影像X」，請建立精確勾勒出您要增強之主題的遮色片。 例如，人員、物件等。 |
| **套用Dynamic Media URL命令以取得效果** | 在您擁有遮色片之後，請使用URL命令套用陰影等效果，或將背景顏色變更為「影像X」。 以下是兩個範例：<br><br> · **投影效果：**<br>&#x200B;若要沿著主體邊界加入陰影效果，請編輯URL，如下所示：<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25)<br>在此URL中， `$shadow$` 引數會建立陰影效果，並且 `color=0,0,0` 將陰影顏色設定為黑色。<br>· **背景色彩變更：**<br>&#x200B;若要變更背景顏色，請使用具有不同背景顏色值的URL：<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0)<br> 在此範例中， `color=255,255,0` 將背景顏色設定為黃色。 將背景編輯成特定顏色，以符合視覺效果。 |

#### 新增影像邊框

Dynamic Media可讓您直接透過URL操作影像，使其成為建立動態數位體驗的強大工具。 以下是一些範例。 我們從下列原始影像URL開始： [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| 任務 | 該做什麼 |
| --- | --- |
| **白色邊框** | 若要新增白邊框，請使用下列URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10)<br>在此URL中， `extend=10,10,10,10` parameter指定四面十個畫素的邊框大小。 |
| **沿著白色邊框模糊** | 若要沿著白色邊框新增模糊效果，您可以依照以下步驟編輯URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0)<br>在此URL中， `effect=-1` 引數會套用模糊效果，並且 `op_blur=60` 控制模糊強度。 |
| **沿著外部邊界的投影效果** | 若要沿著外部邊界加入陰影效果，請使用此URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0)<br>此 `$shadow$` 引數會建立陰影效果，並且 `color=0,0,0` 將陰影顏色設定為黑色。 |

您可以嘗試使用這些URL來取得想要的視覺效果。

#### 建立影像覆蓋圖

如果您想在現有影像上疊加標誌或圖示，Dynamic Media會提供簡單明瞭的方法，讓您使用URL命令來達成此目的。 讓我們來劃分這些步驟。

| 步驟 | 該做什麼 |
| --- | --- |
| **上傳並發佈基本影像** | 首先，上傳並發佈您要重疊標誌或圖示的基本影像。 您可以使用任何影像作為基礎。<br>例如，以下是基本影像：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **上傳並發佈標誌或圖示影像** | 接著，上傳並發佈您要重疊在基本影像上的影像。 此影像應是透明的PNG，並應包含您要覆蓋的標誌或圖示。<br>以下是即將重疊的具有透明度效果的星形物件透明PNG影像：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **套用Dynamic Media URL** | 現在，請建立結合基本影像與標誌或圖示影像的Dynamic Media URL。 您可以使用URL命令來達到此效果。<br>URL結構看起來像這樣：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png)<br>位置<br>· `hotspotRetailBaseImage` 是基本影像。<br>· `starxp` 是標誌/圖示影像。<br>· `layer=1` 指定標誌或圖示應分層在基本影像上。<br>· `scale=1.25` 會調整標誌/圖示的大小。<br>· `posN=0.33,-.25` 決定相對於基本影像的標誌/圖示位置。<br>· `fmt=png` 確保輸出為PNG格式。 |

要進一步瞭解什麼？ 前往 [src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) 以取得更多關於 `src` 命令和其他Dynamic Media URL命令。


#### 重疊促銷文字

以下是使用HTML和CSS在影像上覆蓋促銷文字訊息的步驟。

| 步驟 | 該做什麼 |
| --- | --- |
| **上傳並發佈基本影像** | 首先，上傳並發佈您要附加文字的基本影像。 您可以使用任何您喜歡的影像。 例如，以下是範例基本影像：<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **套用Dynamic Media文字運運算元** | 使用Dynamic Media時，您可以套用文字運運算元，將動態文字直接覆蓋至影像上。 以下範例URL示範此功能：<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial；%7d%7d%7b\colortbl+\red255\green255\blue255；%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial；%7d%7d%7b\colortbl+\red255\green255\blue255；%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600) |

#### 調整大小及裁切各種使用案例

##### 影像調整大小基本需知

調整影像大小涉及變更影像的尺寸、解析度和檔案大小。 以下是一些要考慮的關鍵點：

* **畫素構成：**
數位影像是由稱為畫素的小點所組成。 建立影像時，它具有特定數目的畫素。 調整大小包括增加或減少畫素，以變更影像的尺寸、解析度和檔案大小。
* **外觀比例：**
維持外觀比例（寬度和高度之間的關係）對於防止扭曲至關重要。 不論您是要讓影像變大（放大）還是變小（縮小），保留外觀比例可確保視覺的一致性。
* **品質考量事項：**
調整大小可能會影響影像品質。 避免大幅放大，因為這可能會導致畫素化。 請考慮以較大的大小和解析度重新產生影像。 對於較小的影像，請使用適當的工具來維持解析度。

##### 裁切與調整大小

裁切和調整大小是Dynamic Media中的技術，可讓您變形影像以符合各種使用案例，無論是建立縮圖、產品顯示影像或橫幅。

* **裁切：**
涉及移除影像的一部分以改變其構成和框架。 它不會變更整體維度，但會聚焦於特定區域。
* **調整大小：**
調整整個影像的尺寸、解析度和檔案大小，同時維持外觀比例。

讓我們探索涉及下列客廳影像的使用案例：

* **原始客廳影像：**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **縮圖(200 px x 200 px)：**
適合快速載入或顯示的較小版本。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop)
* **裁切的縮圖（200畫素x 200畫素）：**
已裁剪以聚焦於沙發區域。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **產品顯示影像（800畫素x 600畫素）：**
為了展示沙發而裁切和調整大小。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **橫幅(1720 px x 820 px)：**
從原始影像衍生，強調空間。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop)

您可以根據特定需求，隨時探索這些變數。
想要進一步瞭解URL中可用的命令？ 前往 [命令參考](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### 為我的網站發佈影片

**業務案例：** *快速發佈行銷網站的視訊。*

* **選取視訊設定檔：**
首先，在Dynamic Media中，您應該選取合適的視訊設定檔。 您可以選擇使用 *自我調整視訊編碼* AEM Assets中的「視訊設定檔」底下可用的設定檔。 這些預先定義的編碼設定可確保您的視訊在各種裝置和頻寬條件下都能最佳化播放。 或者，您也可以建立自己的最適化視訊設定檔。
* **指派設定檔：**
將所選的視訊設定檔指派給要上傳視訊的資料夾。 此步驟可確保在上傳流程中套用正確的編碼設定。
* **上傳原始視訊：**
上傳原始視訊檔案。 請確定這是高解析度且品質良好的視訊。 來源視訊愈好，最終結果愈好。
* **預覽和發佈：**
預覽視訊，確保所有專案如預期般顯示。 一旦滿意，請繼續並發佈。 此步驟可讓您的對象存取影片。
* **連結或內嵌：**
發佈後，您有兩個選項。
   * **直接連結：**
使用提供的URL直接連結至影片。 在您的行銷網站上以適當方式建立超連結。
   * **內嵌視訊：**
複製提供的內嵌程式碼，並將其貼到您要顯示視訊的網頁HTML中。 如此一來，影片就能直接在您的網站上播放。

想要進一步瞭解嗎？ 前往 [視訊](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### 設定影片以獲得最佳品質和參與

**業務案例：** *設定影片以獲得最佳品質和參與度。*

為確保影片的最佳品質和參與度，請考慮實作下列最佳實務策略的組合：

* **使用內建的HTML5視訊檢視器：**
Dynamic Media HTML5視訊檢視器預設集是強大的視訊播放器。 使用它們可避免HTML5視訊播放和行動裝置相關的常見問題。
這些預設集可解決適應性位元速率串流傳送及有限的案頭瀏覽器觸及範圍等挑戰。
想要進一步瞭解嗎？ 前往 [最佳實務：使用HTML 5視訊檢視器](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **使用Dynamic Media影片設定檔：**
Dynamic Media中的視訊設定檔有助於有效率的視訊管理、一致的品質和調適型串流。
想要進一步瞭解嗎？ 前往 [Dynamic Media影片設定檔](/help/assets/dynamic-media/video-profiles.md).

* **請遵循視訊編碼最佳實務：**
套用視訊編碼設定檔，以維持原始視訊品質，並在編碼期間不會過度縮放。
想要進一步瞭解嗎？ 前往 [視訊編碼最佳作法](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **採用最適化串流而非漸進式串流：**
最適化串流會根據檢視者的網際網路連線速度和裝置功能來調整視訊品質。
它使用HLS （HTTP即時資料流）或DASH (`Dynamic Adaptive Streaming over HTTP`)以確保最佳播放品質。
與以線性方式提供視訊的漸進式串流不同，適應性串流可儘量減少緩衝，並提供順暢的觀看體驗。

* **在您的帳戶上啟用DASH （透過HTTP的數位最適化串流）：**
DASH會透過最適化串流的方式動態提供視訊內容。
若要啟用DASH，請為您的環境建立支援票證。
想要進一步瞭解嗎？ 前往 [在您的Dynamic Media帳戶上啟用DASH](/help/assets/dynamic-media/video.md#enable-dash).

### 將影片國際化，以使用多語言

**業務案例：** *讓視訊為使用多語言做好準備。*

將多語言使用量視訊國際化，是觸及全球受眾的必要條件。 Dynamic Media提供的功能可協助您達成此目標。

* **上傳您的視訊：**
   * 首先，建立視訊編碼設定檔。 您可以使用Dynamic Media隨附的預先定義最適化視訊編碼設定檔，或建立您自己的自訂設定檔。
   * 將視訊處理設定檔與您上傳主要來源視訊的一或多個資料夾建立關聯。
   * 將您的主要來源視訊上傳至這些資料夾。 Dynamic Media會根據指派的視訊處理設定檔進行編碼。
   * Dynamic Media主要支援短視訊（最長30分鐘），最低解析度大於25×25。 最多可上傳15 GB的視訊檔案1.

* **管理您的影片：**
   * 在AEM中整理、瀏覽及搜尋視訊資產。
   * 預覽和發佈視訊資產。
   * 檢視來源視訊及其編碼的轉譯，以及相關的縮圖。
   * 編輯視訊屬性，例如，標題、說明和標籤2。

* **本地化：**
   * 針對每個目標地理/語言，建立音訊曲目和字幕。
   * 從AEM介面將這些音訊和字幕曲目新增到您的視訊中。
   * 使用者播放視訊時，可以選擇自己偏好的音訊和字幕語言。

* **發佈：**
   * 如果您使用AEM作為網頁內容管理(WCM)系統，您可以直接將視訊新增至網頁。
   * 如果您使用協力廠商WCM系統，可以使用URL或內嵌程式碼來連結或內嵌網頁上的影片。

想要進一步瞭解嗎？ 前往 [關於Dynamic Media中視訊的多重註解和音訊追蹤支援](/help/assets/dynamic-media/video.md#about-msma) 或觀看 [在視訊中新增多個註解和音訊曲目](https://delivery-p106302-e1008131.adobeaemcloud.com/adobe/assets/urn:aaid:aem:daf9a222-9f7f-4333-b167-98cb4c63a1f8/play) （1分41秒）。


## 將資產遞送給客戶

### 最佳化影像大小並縮短頁面載入時間

**業務案例：** *針對任何瀏覽器或熒幕最佳化影像大小，並縮短頁面載入時間。*

Dynamic Media智慧型影像處理是一項功能強大的工具，可依據使用者端的瀏覽器功能，自動最佳化影像的格式、大小和品質，進而增強影像傳送效能。

Adobe建議您使用智慧型影像的功能，而非手動將影像格式設為 `webp` 或 `avif`. 原因如下：

* **瀏覽器相容性：**
智慧型影像可確保提供的影像格式與使用者的瀏覽器相容。
* **最佳壓縮：**
它會根據特定瀏覽器、網路狀況和熒幕解析度，選取最佳壓縮格式。
* **新式格式：**
當 `avif` 是一種較新的格式，提供較佳的壓縮，尚未普遍支援所有瀏覽器。
* **最佳實務：**
為了確保最佳化網頁格式，您可以信任智慧型影像進行格式選取，而不需手動使用指令 `fmt=webp` 或 `fmt=avif`.

仰賴智慧型影像處理，您可以確保影像以最有效率的方式傳送，並因應每位使用者的瀏覽環境量身打造。 此方法可簡化程式，並可改善影像載入時間和整體使用者體驗方面的效能。

想要進一步瞭解嗎？ 前往 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md).
