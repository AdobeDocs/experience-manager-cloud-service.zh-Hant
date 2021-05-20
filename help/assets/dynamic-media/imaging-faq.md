---
title: 智慧型影像
description: 「了解智慧影像如何運用每位使用者的獨特檢視特性，自動提供針對其體驗最佳化的適當影像，進而提升效能和參與度。」
feature: 資產管理，轉譯
role: Business Practitioner
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 2%

---

# 智慧型影像 {#smart-imaging}

## 什麼是「智慧影像處理」？{#what-is-smart-imaging}

智慧型影像處理技術運用Adobe Sensei AI功能，並可與現有的「影像預設集」搭配使用。 它能根據用戶端瀏覽器功能自動最佳化影像格式、大小和品質，進而提升影像傳送效能。

>[!NOTE]
>
>若要使用此功能，您必須使用隨附於Adobe Experience Manager Dynamic Media的現成可用CDN（內容傳遞網路）。 此功能不支援任何其他自訂CDN。

智慧型影像處理還能與Adobe同級最佳的CDN（內容傳遞網路）服務充分整合，進而提升效能。 此服務可在伺服器、網路和互連點之間找到最佳的Internet路由。 它找到的路由延遲最低，丟包率最低，而不是使用網際網路上的預設路由。

下列影像資產範例將說明新增的智慧型影像處理最佳化：

| 影像<br>(URL) | 縮圖 | 大小<br>(JPEG) | 大小(WebP)<br>（帶智慧影像） | 減少 |
|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

與上述內容類似，Adobe也透過來自即時客戶網站的7009個URL執行測試。 他們能夠平均將JPEG的檔案大小進一步優化38%。 對於使用WebP格式的PNG，檔案大小最佳化平均可提高31%。 這種優化是可能的，因為智慧成像技術具有強大的功能。

## 最新智慧映像有哪些主要優勢？{#what-are-the-key-benefits-of-smart-imaging}

影像是頁面載入時間的大部分。 因此，任何效能改善都可能對較高的轉換率、網站逗留時間以及較低的網站跳出率產生深遠影響。

最新版智慧影像處理的增強功能：

* 使用最新智慧型影像處理改善網頁的Google SEO排名。
* 立即提供最佳化內容（在執行階段）。
* 使用Adobe Sensei技術根據影像要求中指定的品質(`qlt`)進行轉換。
* 可使用`bfc` URL參數關閉智慧影像。
* 獨立於TTL（存留時間）。 過去，智慧型影像處理必須具備至少12小時的TTL才能運作。
* 之前，原始和衍生影像都會進行快取，而使快取失效需要兩步驟。 在最新的智慧型影像處理中，只會快取衍生產品，進而允許執行單步快取失效程式。
* 在規則集中使用自訂標頭的客戶將受益於最新的智慧型影像處理，因為這些標頭不會遭到封鎖，這與舊版的智慧型影像處理不同。 例如，[新增自訂標頭值至影像回應|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建議的「計時允許來源」、「X-Robot」。

## 是否存在與智慧映像相關的許可成本？{#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智慧影像處理隨附於您現有的授權。 Dynamic Media Classic或Experience ManagerDynamic Media(內部部署、AMS和Experience Manager作為Cloud Service)的此規則皆為true。

>[!NOTE]
>
>Dynamic Media — 混合客戶無法使用智慧影像處理。

## 智慧型影像處理如何運作？{#how-does-smart-imaging-work}

當消費者請求影像時，智慧影像處理會檢查使用者特性，並根據使用中的瀏覽器轉換為適當的影像格式。 這些格式轉換的執行方式不會降低視覺逼真度。 智慧型影像會以下列方式根據瀏覽器功能自動將影像轉換為不同格式。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 針對下列瀏覽器自動轉換為WebP :
   * 鉻黃
   * Firefox
   * Microsoft® Edge
   * Safari（跨iOS、macOS、iPadOS）提供瀏覽器和作業系統版本支援WebP
   * Android™
   * Opera
* 舊版瀏覽器支援下列項目：

   | 瀏覽器 | 瀏覽器/作業系統版本 | 格式 |
   | --- | --- | --- |
   | Safari | 早於iOS/iPad 14.0或macOS BigSur | JPEG2000 |
   | Edge | 早於18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 若瀏覽器不支援這些格式，則會提供原始要求的影像格式。

如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

## 支援哪些影像格式？{#what-image-formats-are-supported}

智慧影像處理支援下列影像格式：

* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 智慧型影像處理如何處理已使用的現有影像預設集？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

智慧型影像處理可與您現有的「影像預設集」搭配使用。 如果請求的檔案格式為JPEG或PNG，則它會觀察除質量(`qlt`)和格式(`fmt`)之外的所有影像設定。 對於格式轉換，智慧影像處理會根據影像預設集設定所定義的完整視覺逼真度，但檔案大小較小。 如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 是否必須變更任何URL、影像預設集，或在我的網站上部署任何智慧型影像處理的新程式碼？{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在現有自訂網域上設定智慧型影像處理，智慧型影像處理可順暢地與您現有的影像URL和影像預設集搭配運作。 此外，智慧影像處理不要求您在網站上新增任何程式碼以偵測使用者的瀏覽器。 這些都會自動處理。

如果您必須設定新的自訂網域以使用智慧型影像，則必須更新URL以反映此自訂網域。

若要了解智慧型影像處理的先決條件，請參閱[我是否符合使用智慧型影像處理的資格？](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智慧型影像處理是否可搭配HTTPS運作？ HTTP/2如何？{#does-smart-imaging-working-with-https-how-about-http}

智慧型影像處理可透過HTTP或HTTPS傳送的影像。 此外，它也可透過HTTP/2運作。

## 我是否有資格使用智慧映像？{#am-i-eligible-to-use-smart-imaging}

若要使用智慧影像處理，您公司的Dynamic Media Classic或Dynamic MediaExperience Manager帳戶必須符合下列需求：

* 將Adobe隨附的CDN（內容傳遞網路）用於授權。
* 使用專用域（例如`images.company.com`或`mycompany.scene7.com`），而不是通用域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

點選「 **[!UICONTROL 設定>應用程式設定>一般設定]**」。 查找標籤為&#x200B;**[!UICONTROL 已發佈伺服器名稱]**&#x200B;的欄位。 如果您目前使用一般網域，可以要求移至您自己的自訂網域。 提交技術支援票證時，提出此轉換請求。

使用Dynamic Media授權，您的第一個自訂網域不需額外付費。

## 為我的帳戶啟用智慧影像處理的程式為何？{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您啟動使用智慧影像處理的請求；不會自動啟用。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。
1. 在您的支援案例中提供下列資訊：

   1. 主要聯繫人姓名、電子郵件、電話。
   1. 要啟用智慧映像的所有域（即`images.company.com`或`mycompany.scene7.com`）。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。

      查找標籤為&#x200B;**[!UICONTROL 已發佈伺服器名稱]**&#x200B;的欄位。
   1. 確認您是透過Adobe使用CDN，而非以直接關係進行管理。
   1. 確認您使用的是專用網域，如`images.company.com`或`mycompany.scene7.com`，而非通用網域，例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。

      查找標籤為&#x200B;**[!UICONTROL 已發佈伺服器名稱]**&#x200B;的欄位。 如果您目前使用一般Dynamic Media Classic網域，可以請求移轉至您自己的自訂網域，作為此轉變的一部分。
   1. 指出是否希望它透過HTTP/2運作。

1. Adobe客戶服務會根據提交請求的順序，將您新增至智慧型影像處理客戶等候清單。
1. 當Adobe準備好處理您的請求時，客戶服務會聯絡您以協調並設定目標日期。
1. **可選**:您可以選擇在測試環境中測試智慧型影像，然後Adobe將新功能推送至生產環境。
1. 客戶服務完成後，會通知您。
1. 為最大程度提升智慧型影像處理的效能，Adobe建議將存留時間(TTL)設為24小時或更長。 TTL會定義CDN快取資產的時間長度。 要更改此設定：

   1. 如果您使用Dynamic Media Classic，請按一下「**[!UICONTROL 設定>應用程式設定>發佈設定>影像伺服器]**」。 將&#x200B;**[!UICONTROL 預設客戶端快取時間設定為「Live]** 」值24或更長。
   1. 如果您使用Dynamic Media，請依照[這些指示](config-dm.md)操作。 將&#x200B;**[!UICONTROL 過期]**&#x200B;值設定24小時或更久。

## 何時可以使用智慧影像處理啟用帳戶？{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

系統會根據等待清單，依客戶服務接收請求的順序處理請求。

>[!NOTE]
>
>啟用智慧影像處理需要Adobe清除快取，因此可能需要較長的前置時間。 因此，在任何指定時間都只能處理少數客戶轉變。

## 切換到使用智慧映像有什麼風險？{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客戶網頁沒有風險。 不過，轉換至智慧型影像處理確實會清除CDN快取。 此操作涉及在Experience Manager上移至Dynamic Media Classic或Dynamic Media的新設定。

在初始轉變期間，非快取的影像會直接點擊Adobe的原始伺服器，直到重新建置快取為止。 因此，Adobe計劃一次處理一些客戶轉變，以在從來源提取請求時維持可接受的效能。 對於大部分的客戶，快取會在約1至2天內，於CDN中重新完全建立。

## 如何驗證智慧型影像是否如預期般運作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 使用智慧型影像設定帳戶後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager - Dynamic Media影像URL。
1. 在瀏覽器中，按一下「**[!UICONTROL 檢視>開發人員>開發人員工具]**」，開啟Chrome開發人員窗格。 或者，選擇您選擇的任何瀏覽器開發人員工具。

1. 開啟開發人員工具時，請確定已停用快取。

   * 在Windows®上，導覽至開發人員工具窗格中的設定，然後選取&#x200B;**[!UICONTROL 停用快取（當開啟裝置時）]**&#x200B;核取方塊。
   * 在macOS上，在開發人員窗格的&#x200B;**[!UICONTROL Network]**&#x200B;標籤下，選擇&#x200B;**[!UICONTROL disable cache]**。

1. 觀察「內容類型」已轉換為適當的格式。 下列螢幕擷圖顯示在Chrome上動態轉換為WebP的PNG影像。
1. 在不同的瀏覽器和使用者條件上重複此測試。

>[!NOTE]
>
>並非所有影像都經過轉換。 智慧型影像處理決定轉換是否能改善效能。 有時，如果沒有預期的效能增益，或格式不是JPEG或PNG，則不會轉換影像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以對任何請求關閉智慧映像？{#turning-off-smart-imaging}

是. 您可以將修飾詞`bfc=off`新增至URL，以關閉智慧型影像。

## 可以使用什麼「調整」？ 是否有任何可定義的設定或行為？ (#tuning-settings)

目前，您可以選擇啟用或禁用智慧映像。 沒有其他調整可用。

## 如果智慧影像處理管理質量設定，是否有可設定的最小值和最大值？ 例如，是否可設定「不低於60」和「不大於80品質」？ (#minimum-maximum)

當前智慧映像中沒有此類配置功能。

## 有時，JPEG影像會傳回至Chrome，而非WebP影像。 為什麼會發生這種變化？ (#jpeg-webp)

智慧型影像處理會判斷轉換是否有益。 只有在轉換導致檔案大小較小且品質相當時，才會傳回新影像。
