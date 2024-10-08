---
title: 智慧型影像
description: 瞭解智慧型影像與Adobe Sensei AI搭配如何套用每位使用者獨特的檢視特性，以自動提供針對其體驗最佳化的正確影像，進而提高效能和參與度。
contentOwner: Rick Brough
feature: Asset Management,Renditions,Best Practices
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 1b985a83fd58522ee485c02b96bfb6a697da6ce0
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 1%

---

# 智慧型影像 {#smart-imaging}

## 關於智慧型影像{#about-smart-imaging}

智慧型影像技術可套用Adobe Sensei AI功能，並與現有的「影像預設集」搭配使用。 它會根據使用者端瀏覽器功能自動最佳化影像格式、大小和品質，藉此增強影像傳送效能。

現在，LCP （最大內容繪製）的Google Core Web Vital分數更佳，智慧型影像處理功能更完善，現在同時提供AVIF和WebP支援。

>[!IMPORTANT]
>
>智慧型影像處理需要您使用Adobe Experience Manager - Dynamic Media隨附的現成可用CDN （內容傳遞網路）。 此功能不支援任何其他自訂CDN。

>[!TIP]
>
>嘗試使用Dynamic Media [_快照_](https://snapshot.scene7.com/)，探索Dynamic Media影像修飾元和智慧型影像的優點。
>
> Snapshot是視覺化展示工具，旨在說明Dynamic Media在最佳化及動態影像傳送方面的強大功能。 實驗測試影像或Dynamic Media URL，以視覺化方式觀察各種Dynamic Media影像修飾元的輸出，以及針對下列專案的智慧型影像最佳化：
>
>* 檔案大小（含WebP和AVIF傳送）
>* 網路頻寬
>* DPR （裝置畫素比率）
>
>若要瞭解使用快照的簡易程度，請播放[快照訓練影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) （3分17秒）。

智慧型影像可與Adobe同級最佳的高階CDN （內容傳遞網路）服務完全整合，進而提升效能。 此服務會尋找伺服器、網路和對等點之間的最佳網際網路路由。 它會找到延遲最低、封包遺失率最低的路由，而不使用網際網路上的預設路由。

下列影像資產範例說明新增的智慧型影像最佳化：

| 影像(URL) | 縮圖 | 大小(JPEG) | 使用智慧型影像處理調整大小(WebP) | 使用智慧型影像處理調整大小(AVIF) | 使用WebP減少% | 使用AVIF降低% |
|---|---|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

與上述類似，Adobe也使用較大的範例集執行測試。 與WebP相比，AVIF格式提供了20%的額外大小縮減，比JPEG提供了27%的縮減。 視覺品質完全相同。 與JPEG相比，AVIF的平均大小縮減率總計高達41%。

比較WebP和AVIF與PNG，您可以看到WebP的大小減少84%，AVIF的大小減少87%。 此外，由於WebP和AVIF格式都支援透明和多重影像動畫，因此非常適合取代透明的PNG和GIF檔案。

另請參閱[使用下一代影像格式（WebP和AVIF）的影像最佳化](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**智慧型影像的優點**

智慧型影像可根據使用者端使用的瀏覽器、裝置顯示和網路狀況，自動最佳化影像檔案大小，以提供更優異的影像傳送效能。 由於影像佔據了頁面的大部分載入時間，因此任何效能改善都會對業務KPI產生深遠影響，例如更高的轉換率、在網站上逗留的時間以及較低的網站跳出率。

最新智慧型影像處理的最新主要優點包括：

* 現在支援下一代AVIF格式。
* PNG至WebP和AVIF現在支援有損轉換。 由於PNG是無損格式，因此先前傳送的WebP和AVIF是無損的。
* [瀏覽器格式轉換](#bfc)
* [裝置畫素比例](#dpr)
* [網路頻寬](#bandwidth)

### 關於瀏覽器格式轉換 {#bfc}

透過將`bfc=on`附加至影像URL來開啟瀏覽器格式轉換，會自動將JPEG和PNG轉換成其他瀏覽器的有損AVIF、有損WebP、有損JPEGXR、有損JPEG2000。 對於不支援這些格式的瀏覽器，智慧型影像會繼續提供JPEG或PNG。 除了格式以外，新格式的品質也會由「智慧型影像」重新計算。

您也可以將`bfc=off`附加至影像的URL來關閉智慧型影像。

另請參閱Dynamic Media影像提供與轉譯API中的[bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en)。

### 關於裝置畫素比最佳化 {#dpr}

裝置畫素比率(DPR) — 也稱為CSS畫素比率 — 是裝置的實體畫素與邏輯畫素之間的關係。 特別是隨著Retina熒幕的出現，現代行動裝置的畫素解析度正以快速的速度增長。

啟用「裝置畫素比最佳化」 ，以熒幕的原生解析度呈現影像，使影像更清晰。

目前，顯示器的畫素密度來自Akamai CDN標題值。

| 影像URL中的允許值 | 說明 |
|---|---|
| `dpr=off` | 關閉個別影像URL層級的DPR最佳化。 |
| `dpr=on,dprValue` | 使用自訂值（任何使用者端邏輯或其他方式偵測到的值）覆寫智慧型影像偵測到的DPR值。 `dprValue`的允許值是大於0的任何數字。 |

>[!NOTE]
>
>* 即使公司層級DPR設定為off，您仍可使用`dpr=on,dprValue`。
>* 由於DPR最佳化，當產生的影像大於MaxPix Dynamic Media設定時，一律會透過維持影像的外觀比例來辨識MaxPix寬度。 —>

| 要求的影像大小 | 裝置畫素比率(dpr)值 | 傳遞的影像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另請參閱[處理影像時](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images)和[處理智慧型裁切](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)。

### 關於網路頻寬最佳化 {#bandwidth}

開啟網路頻寬會自動根據實際網路頻寬調整影像品質。 因為網路頻寬太低，DPR （裝置畫素比）最佳化功能即使已經開啟，也會自動關閉。

如有需要，貴公司可將`network=off`附加至影像的URL，選擇退出個別影像層級的網路頻寬最佳化。

| 影像URL中的允許值 | 說明 |
|---|---|
| `network=off` | 關閉個別影像URL層級的網路最佳化。 |

DPR和網路頻寬值是根據偵測到的套件式CDN使用者端值。 這些值有時不準確。 例如，DPR=2的iPhone5和`dpr=3`的iPhone12都顯示`dpr=2`。 不過，對於高解析度裝置，傳送`dpr=2`還是比傳送`dpr=1`好。 然而，克服這種不正確性的最佳方式是使用使用者端DPR，為您提供100%正確的值。 而且它適用於任何裝置，不論是Apple或任何其他已啟動的裝置。 請參閱[使用智慧型影像搭配使用者端裝置畫素比率](/help/assets/dynamic-media/client-side-dpr.md)。

**智慧型影像處理的其他主要優點**

* 改善使用最新智慧型影像處理之網頁的Google SEO排名。
* 立即提供最佳化內容（在執行階段）。
* 使用Adobe Sensei技術，根據影像要求中指定的品質(`qlt`)進行轉換。
* 不受TTL （存留時間）影響。 之前，智慧型影像處理至少必須有12小時的TTL才能運作。
* 先前，原始和衍生影像都會經過快取，而且是使快取失效的兩步驟程式。 在最新的智慧型影像處理中，只會快取衍生專案，進行單一步驟的快取失效程式。
* 在規則集中使用自訂標題的客戶可受益於最新的智慧型影像，因為這些標題不會遭到封鎖，不像舊版的智慧型影像。 例如，如[新增自訂標頭值至影像回應|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建議的「計時允許來源」、「X-Robot」。

## 智慧型影像的運作方式{#how-smart-imaging-works}

當消費者要求影像時，「智慧型影像處理」會檢查使用者特性，並根據使用中的瀏覽器將其轉換為適當的影像格式。 這些格式轉換的進行方式不會降低視覺的逼真度。 智慧型影像會根據瀏覽器功能，以下列方式自動將影像轉換為不同格式。

* 如果瀏覽器支援格式，則自動轉換為AVIF
* 如果AVIF轉換沒有好處或瀏覽器不支援AVIF，則自動轉換成WebP
* 如果Safari不支援WebP，則自動轉換為JPEG2000
* 自動轉換為IE 9+適用的JPEGXR，或如果Edge不支援WebP

  | 影像格式 | 支援的瀏覽器 |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* 對於不支援這些格式的瀏覽器，會提供最初請求的影像格式。

如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

## 智慧型影像處理支援影像格式{#image-format-support}

智慧型影像支援下列影像格式：

* JPEG
* PNG

對於JPEG影像檔案格式，新格式的品質會由「智慧型影像」重新計算。

對於支援PNG等透明度的影像檔案格式，您可以設定「智慧型影像」以傳送有損的AVIF和WebP。 針對有損格式轉換，「智慧型影像處理」會使用影像URL中所述的品質，或是使用Dynamic Media公司帳戶中設定的品質。

## 智慧型影像處理中的影像伺服命令支援{#imaging-serving-command-support}

不支援「影像伺服」命令`fmt`和`qlt`；支援所有剩餘的命令。

## 關於智慧型影像的常見問題{#smart-imaging-faq}

+++**是否有與智慧型影像相關的授權成本？**

否。智慧型影像包含於您現有的授權中。 此規則適用於Dynamic Media Classic或Experience Manager - Dynamic Media (內部部署、AMS和Experience Manageras a Cloud Service)。

>[!IMPORTANT]
>
>智慧型影像不適用於Dynamic Media — 混合型客戶。

+++

+++**智慧型影像處理是否可以針對任何要求關閉？**

可以。您可以新增下列任何修飾元來關閉智慧型影像：

* `bfc=off`以關閉瀏覽器格式轉換。 另請參閱[瀏覽器格式轉換](#bfc)。
* `dpr=off`以關閉裝置畫素比例。 另請參閱[裝置畫素比例](#dpr)。
* `network=off`以關閉網路頻寬。 另請參閱[網路頻寬](#network)。

+++

+++**是否可以「調整」智慧型影像？**

可以。智慧型影像有三個可啟用或停用的選項。

* [瀏覽器格式轉換](#bfc)
* [裝置畫素比例](#dpr)
* [網路頻寬](#network)

+++

+++**智慧型影像處理是否適用於我現有的影像預設集？**

可以。智慧型影像可搭配您現有的影像預設集使用，並觀察所有影像設定。 影像格式或品質設定（或兩者）會有何改變。 對於格式轉換，「智慧型影像處理」會維持影像預設集設定所定義的完整視覺逼真度，但檔案大小較小。

例如，假設影像預設集是以JPEG格式定義，大小為500 x 500，品質為85，遮色片銳利化調整為0.1,1，5。 當智慧型影像偵測到使用者在Chrome瀏覽器上時，影像會轉換為WebP格式，大小為500 x 500。 而且，不銳利化遮色片=0.1、1、5的WebP品質儘可能符合85的JPEG品質。 會將該WebP轉換的佔用空間與JPEG進行比較，並傳回兩者中較小者。

+++

+++**我是否必須在我的網站上變更任何URL、影像預設集或部署新程式碼？**

否。智慧型影像可以順暢地搭配您現有的影像URL和影像預設集。 此外，智慧型影像不需要您新增程式碼至網站以偵測使用者的瀏覽器。 所有此功能都會自動處理。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++

+++**智慧型影像處理是否適用於HTTPS？ HTTP/2呢？**

是，針對兩個問題。 智慧型影像處理透過HTTP或HTTPS傳送的影像。 此外，它也適用於HTTP/2。

+++

+++**我是否符合使用智慧型影像處理的資格？**

視情況而定。 若要使用智慧型影像，貴公司的Dynamic Media Classic或Dynamic MediaExperience Manager帳戶必須符合下列要求：

* 使用Adobe隨附的CDN （內容傳遞網路）作為授權的一部分。
* 使用專用網域（例如`images.company.com`或`mycompany.scene7.com`），而不是通用網域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

移至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。 尋找標示為&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;的欄位。 如果您目前使用一般網域，您可以要求移至您自己的自訂網域。 當您提交支援案例時，提出此轉換請求。

使用Dynamic Media授權時，您的第一個自訂網域不需額外付費。

+++

+++**我可以為我的帳戶啟用智慧型影像處理嗎？**

否。您起始了使用智慧型影像的要求，但系統不會自動啟用此要求。

建立支援案例，如下所述。 在您的支援案例中，請務必提及要在帳戶上啟用的下列智慧影像功能（一或多個）：

* WebP
* AVIF
* DPR與網路頻寬最佳化
* PNG至有損AVIF或有損WebP

如果您已透過WebP啟用智慧型影像，但想要上述的其他新功能，則必須建立支援案例。

**若要建立支援案例，在您的帳戶上啟用智慧型影像處理：**

1. [使用此Admin Console開始建立新的支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支援案例中提供下列資訊：

   * 主要連絡人姓名、電子郵件、電話。

   * 列出您要在帳戶上啟用的下列智慧影像功能（一或多個）：
      * WebP
      * AVIF
      * DPR與網路頻寬最佳化
      * PNG至有損AVIF或有損WebP

   * 要啟用智慧型影像的所有網域（即`images.company.com`或`mycompany.scene7.com`）。

     若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

     移至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。

     尋找標示為&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;的欄位。

   * 確認您是透過Adobe使用CDN，且並非透過直接關係管理。

   * 請確認您使用的是專用網域（例如`images.company.com`或`mycompany.scene7.com`），而不是通用網域（例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`）。

     若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

     移至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。

     尋找標示為&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;的欄位。 如果您目前使用一般Dynamic Media Classic網域，您可以在此轉換中要求移至您自己的自訂網域。

   * 指出您是否希望它透過HTTP/2運作。

1. Adobe客戶支援會根據提交請求的順序，將您新增至智慧型影像處理客戶等候清單。
1. 當Adobe準備好處理您的請求時，客戶支援聯絡您以協調並設定目標日期。
1. **選擇性**：您可以選擇在Adobe將新功能推展到生產環境之前，先在「測試」中測試「智慧型影像」。
1. 客戶支援會在完成後通知您。
1. 為了最大化智慧型影像的效能改善，Adobe建議將存留時間(TTL)設定為24小時或更長。 TTL會定義CDN快取資產的時間長度。 若要變更此設定：

   1. 若您使用Dynamic Media Classic，請移至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL Publish設定]** > **[!UICONTROL 影像伺服器]**。 將&#x200B;**[!UICONTROL 預設使用者端快取存留時間]**&#x200B;值設為24或更長。
   1. 如果您使用Dynamic Media，請遵循[這些指示](config-dm.md)。 將&#x200B;**[!UICONTROL Expiration]**&#x200B;值設定為24小時或更久。

+++

+++**我的帳戶何時啟用智慧型影像處理？**

根據「等待清單」，客戶支援收到的請求會依順序處理。

>[!NOTE]
>
>因為啟用智慧型影像處理需要Adobe清除快取，所以前置時間可能會很長。 因此，在任何指定時間只能處理少數客戶轉換。

+++

+++**使用智慧型影像處理是否有風險？**

客戶網頁沒有風險。 不過，轉換至智慧型影像處理會清除CDN快取。 此作業涉及在Experience Manager上移至Dynamic Media Classic或Dynamic Media的新設定。

在初始轉換期間，非快取影像會直接點選Adobe的原始伺服器，直到再次重建快取為止。 因此，Adobe計劃一次處理幾個客戶轉換，以便在從來源提取請求時維持可接受的效能。 對於大多數客戶而言，快取會在1至2天內在CDN再次完全建置。

+++

+++**我可以驗證智慧型影像處理是否正常運作嗎？**

可以。您可以執行下列動作：

1. 帳戶設定智慧影像後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager - Dynamic Media影像URL。
1. 在瀏覽器中前往&#x200B;**[!UICONTROL 檢視]** > **[!UICONTROL 開發人員]** > **[!UICONTROL 開發人員工具]**，開啟Chrome開發人員窗格。 或者，選擇您選擇的任何瀏覽器開發人員工具。

1. 請確保在開發人員工具開啟時停用快取。

   * 在Windows®上，瀏覽至開發人員工具窗格中的設定，然後選取&#x200B;**[!UICONTROL 停用快取（當devtools開啟時）]**&#x200B;核取方塊。
   * 在macOS上，在開發人員窗格的&#x200B;**[!UICONTROL 網路]**&#x200B;標籤下，選取&#x200B;**[!UICONTROL 停用快取]**。

1. 請注意，內容型別已轉換為適當的格式。 下列熒幕擷圖顯示的PNG影像正動態轉換為Chrome上的WebP。 如果您的網域已啟用AVIF，內容型別中也可能看到AVIF。
1. 在不同的瀏覽器和使用者條件下重複此測試。

>[!NOTE]
>
>並非所有影像都會轉換。 智慧型影像處理會決定轉換是否能改善效能。 有時，如果沒有預期的效能提升，或格式不是JPEG或PNG，影像就不會轉換。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

+++

+++**是否有辦法瞭解智慧型影像的優點？**

可以。智慧型影像標題決定智慧型影像的優點。 啟用智慧型影像時，當您要求影像之後，在&#x200B;**[!UICONTROL 回應標題]**&#x200B;標題下，您可以看到`-X-Adobe-Smart-Imaging`，如下列醒目提示的範例所示：

![智慧型影像標題](/help/assets/dynamic-media/assets/smartimagingheader.png)

此標題會告訴您下列內容：

* 智慧型影像處理功能適用於本公司。
* 正值表示轉換成功。 在這種情況下，會傳回新的WebP影像。
* 負值表示轉換不成功。 在這種情況下，會傳回原始要求的影像(如果未指定，預設為JPEG)。
* 正值會顯示要求的影像與新影像之間的位元組差異。 在上述範例中，儲存的位元組為`75048`或一個影像約75 KB。
* 負值表示要求的影像小於新影像。 會顯示負數大小差異，但提供的影像僅為原始要求的影像。

>[!NOTE]
>
>**XAdobe智慧型影像= -1，正在傳遞WebP**
>
>如果`X-Adobe-Smart-Imaging`的值為–1，而且WebP仍在傳遞，則表示智慧型影像正在運作，但由於快取記憶體太舊，因此並未計算大小優勢。 您可以在影像的URL中使用`cache=update` （僅一次）來修正此問題。
>使用修飾元的範例：
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>若要讓整個快取失效，您必須建立支援案例。

+++

+++**我可以在智慧型影像中停用AVIF最佳化嗎？**

可以。如果您想要依預設切換回提供WebP，請為相同專案建立支援案例。 如同往常，您可以新增引數`bfc=off`至影像的URL來關閉智慧型影像。 不過，您無法在智慧型影像的URL修飾元中選取WebP或AVIF。 此能力在您的公司帳戶層級進行維護。

+++

+++**為什麼我的要求在Chrome網頁瀏覽器上有fmt=tif的URL時失敗？**

如果您的帳戶未啟用智慧型影像處理，就不會發生這個錯誤。 智慧型影像僅適用於JPEG或PNG格式。

若要避免此錯誤，您可以：

* 指定JPEG或PNG，或
* 完全不使用`fmt`修飾元，或
* 使用智慧型影像定義的瀏覽器偏好格式。 例如，您可以使用Chrome網頁瀏覽器的WebP。

+++

+++**我可以從影像的URL下載TIFF影像嗎？**

可以。將`fmt=tif`和`bfc=off`新增至影像的URL路徑。

+++

+++**智慧型影像處理是否管理影像格式和影像品質設定？**

可以。智慧型影像使用格式和品質。 其餘的引數則維持不變（如果影像的URL中有要求）。

+++

+++**我可以設定最小和最大品質設定嗎？**

否。目前沒有這類布建。

+++

+++**智慧型影像處理是否調整百分比品質輸出設定？**

可以。智慧型影像會自動調整品質百分比。 此品質百分比是由Adobe開發的機器學習演演算法所決定。 此百分比不限範圍。

+++

+++**只有JPEG和PNG會由智慧型影像取代？**

可以。此功能僅適用於JPEG和PNG。

+++

+++**為何JPEG有時會回到Chrome而非WebP？**

智慧型影像可判斷轉換是否有效。 它只會傳迴轉換有利的新影像。

+++

+++**為什麼裝置畫素比(dpr)不適用於複合影像？**

如果複合影像涉及太多圖層，則使用position修飾元時，dpr功能可能會受到影響。 此問題已知，並將在未來版本的智慧型影像中修正。 如果其他智慧型影像功能無法如預期運作，您可以建立支援案例來報告問題。

+++

+++**為什麼智慧型影像處理PNG會轉換成不失真WebP/AVIF？**

由於PNG為無損格式，因此先前傳送的WebP和AVIF為無損結果，因此大小比預期大。 智慧型影像處理現在支援有損轉換。 您可以在影像要求中使用修飾元`cache=update` （僅限一次）來修正此問題。 使用此修飾元的範例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

若要讓整個快取失效，您必須建立要求此類努力的支援案例。

+++

+++**我可以在智慧型影像中繼續使用PNG進行無損轉換嗎？**

可以。智慧型影像處理現在支援根據品質等級進行有損轉換。 若要繼續使用無損轉換，您可以使用透過您公司的設定所設定的100品質，或是透過影像的URL，在路徑中使用`qlt=100`。

+++



























<!-- ## If Smart Imaging manages the quality settings, are there minimums and maximums I can set? For example, is it possible to set "no lower than 60" and "no greater than 80 quality"? {#minimum-maximum}

There is no such provisioning ability in the current Smart Imaging. -->

<!-- ## Sometimes a JPEG image is returned to Chrome instead of a WebP image. Why does that change happen? {#jpeg-webp}

Smart Imaging determines if the conversion is beneficial or not. It returns the new image only if the conversion results in a smaller file size with comparable quality.

How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) 
-->
