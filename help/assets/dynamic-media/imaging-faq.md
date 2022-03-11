---
title: 智慧映像
description: 瞭解Adobe SenseiAI的智慧成像如何應用每個用戶的獨特觀看特性來自動提供針對其體驗而優化的正確影像，從而獲得更好的效能和參與。
feature: Asset Management,Renditions
role: User
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2624'
ht-degree: 1%

---

# 智慧型影像 {#smart-imaging}

## 什麼是「智慧映像」？ {#what-is-smart-imaging}

智慧成像技術應用了Adobe SenseiAI功能，並與現有的&quot;影像預設&quot;配合使用。 它致力於通過基於客戶端瀏覽器功能自動優化影像格式、大小和質量來增強影像傳送效能。

>[!IMPORTANT]
>
>智慧映像要求您使用與Adobe Experience Manager-Dynamic Media捆綁的現成CDN（內容交付網路）。 此功能不支援任何其他自定義CDN。

智慧映像還得益於與Adobe同類最佳的高級CDN（內容交付網路）服務完全整合而帶來的效能提升。 此服務可在伺服器、網路和對等點之間找到最佳Internet路由。 它會找到延遲最小和丟包率最低的路由，而不是使用Internet上的預設路由。

以下映像資產示例說明了添加的智慧映像優化：

| 影像<br>(URL) | 縮圖 | 大小<br> (JPEG) | 大小(WebP)<br> （使用智慧映像） | %減少 |
|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 3成8 |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 6成3 |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 5成9 |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 4成4 |
|  |  |  |  | 平均= 51% |

與上述內容類似，Adobe還運行了一個test，其中包含來自現場客戶站點的7009個URL。 他們能夠實現平均38%的進一步檔案大小優化，以便進行JPEG。 對於WebP格式的PNG，他們能夠實現平均31%的檔案大小進一步優化。 由於智慧成像的功能，這種優化是可能的。

在移動網路上，挑戰還有兩個因素：

* 各種不同外形規格的設備和高解析度顯示器。
* 網路頻寬受限。

在影像方面，目標是盡可能高效地提供最優質的影像。

### 關於設備像素比優化 {#dpr}

設備像素比(DPR)也稱為CSS像素比，是設備的物理像素與邏輯像素之間的關係。 特別是隨著視網膜螢幕的出現，現代移動設備的像素解析度正在以快速的速度增長。

啟用設備像素比率優化將以螢幕的本機解析度呈現影像，使影像看起來清晰。

開啟智慧成像DPR配置會根據從中提供請求的顯示器的像素密度自動調整請求的影像。 目前，顯示器的像素密度來自Akamai CDN報頭值。

| 影像URL中允許的值 | 說明 |
|---|---|
| `dpr=off` | 在單個影像URL級別關閉DPR優化。 |
| `dpr=on,dprValue` | 使用自定義值（由任何客戶端邏輯或其他方法檢測）覆蓋智慧映像檢測到的DPR值。 允許的值 `dprValue` 是大於0的任何數字。 1.5、2或3的指定值是典型值。 |

>[!NOTE]
>
>* 您可以使用 `dpr=on,dprValue` 即使公司級DPR設定為「關閉」。
>* 由於DPR優化，當結果影像大於MaxPixDynamic Media設定時，通過保持影像的長寬比始終識別MaxPix寬度。


| 請求的映像大小 | DPR值 | 已傳送的影像大小 |
|---|---|---|
| 816x500 | 1 | 816x500 |
| 816x500 | 2 | 1632x1000 |

另請參閱 [使用影像時](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用Smart Crop時](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)。

### 關於網路頻寬優化 {#network-bandwidth-optimization}

啟用網路頻寬可根據實際網路頻寬自動調整提供的影像質量。 對於網路頻寬較差的情況，即使DPR優化已開啟，也會自動關閉。

如果需要，您的公司可以通過添加 `network=off` 的子菜單。

| 影像URL中允許的值 | 說明 |
|---|---|
| `network=off` | 在單個影像URL級別關閉網路優化。 |

>[!NOTE]
>
>DPR和網路頻寬值基於所綁定CDN的檢測到的客戶端值。 這些價值有時是不準確的。 例如，DPR=2的iPhone5和DPR=3的iPhone12都顯示DPR=2。 但是，對於高解析度設備，發送DPR=2比發送DPR=1要好。 即將推出：Adobe正在處理客戶端代碼以準確確定最終用戶的DPR。

## 最新智慧映像的主要優勢是什麼？ {#what-are-the-key-benefits-of-smart-imaging}

影像構成了頁面的大部分載入時間。 因此，任何效能改進都可能對提高轉換率、在站點上花費的時間以及降低站點彈跳率產生深遠的影響。

最新版智慧映像中的增強功能：

* 改進了使用最新智慧映像的網頁的GoogleSEO排名。
* 立即（在運行時）提供優化內容。
* 使用Adobe Sensei技術根據質量進行轉換(`qlt`)。
* 可以使用 `bfc` URL參數。
* TTL（生存時間）獨立。 以前，智慧映像的最低TTL為12小時是必需的。
* 以前，原始和衍生影像都被快取，而使快取失效的過程是兩步。 在最新的智慧映像中，只有衍生產品被快取，從而允許單步快取失效過程。
* 在規則集中使用自定義標頭的客戶可以從最新的智慧映像中獲益，因為這些標頭不會被阻止，這與以前版本的智慧映像不同。 例如，「計時允許原點」、「X-Robot」（如中所建議） [向映像響應添加自定義標頭值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)。

## 是否存在與智慧映像相關的許可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智慧映像隨您現有許可證一起提供。 此規則適用於Dynamic Media Classic或Experience Manager-Dynamic Media(On-prem、AMS和Experience Manageras a Cloud Service)。

>[!NOTE]
>
>Smart Imaging不適用於Dynamic Media — 混合型客戶。

## Smart Imaging是如何工作的？ {#how-does-smart-imaging-work}

當用戶請求影像時，智慧映像會檢查用戶特徵並根據使用中的瀏覽器轉換為適當的影像格式。 這些格式轉換以不降低視覺保真度的方式進行。 智慧成像按照以下方式根據瀏覽器功能自動將影像轉換為不同格式。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 自動轉換為以下瀏覽器的WebP:
   * 鉻
   * 火狐
   * Microsoft®邊緣
   * Safari(跨iOS、macOS、iPadOS)，提供瀏覽器和作業系統版本支援WebP
   * Android™
   * 歌劇
* 舊式瀏覽器支援：

   | 瀏覽器 | 瀏覽器/作業系統版本 | 格式 |
   | --- | --- | --- |
   | 薩法里 | 早於iOS/iPad14.0或macOS大蘇爾 | JPEG2000 |
   | 邊緣 | 早於18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 對於不支援這些格式的瀏覽器，將提供最初請求的影像格式。

如果原始影像大小小於智慧成像生成的影像大小，則提供原始影像。

## 支援哪些影像格式？ {#what-image-formats-are-supported}

智慧映像支援以下影像格式：

* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Smart Imaging如何處理已使用的現有影像預設？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging可與現有「影像預設」配合使用。 它會觀察除質量以外的所有影像設定(`qlt`)和格式(`fmt`)。 對於格式轉換，Smart Imaging會按照影像預設設定的定義保持完全的視覺保真度，但檔案大小較小。 如果原始影像大小小於智慧成像生成的影像大小，則提供原始影像。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 是否必須更改任何URL、影像預設，或在我的網站上部署任何新代碼以用於智慧成像？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在現有自定義域上配置Smart Imaging，則Smart Imaging可與現有影像URL和影像預設無縫協作。 此外，智慧映像不需要您在網站上添加任何代碼來檢測用戶的瀏覽器。 它都是自動處理的。

如果必須配置新的自定義域以使用智慧映像，則必須更新URL以反映此自定義域。

要瞭解智慧映像的先決條件，請參見 [我是否有資格使用智慧映像？](#am-i-eligible-to-use-smart-imaging)

<!-- OLD No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智慧映像是否與HTTPS配合使用？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智慧映像可與通過HTTP或HTTPS傳送的映像配合使用。 此外，它還通過HTTP/2工作。

## 我是否有資格使用智慧映像？ {#am-i-eligible-to-use-smart-imaging}

要使用Smart Imaging，您公司的Dynamic Media Classic或Dynamic MediaExperience Manager客戶必須滿足以下要求：

* 將Adobe捆綁的CDN（內容分發網路）用作許可證的一部分。
* 使用專用域(例如， `images.company.com` 或 `mycompany.scene7.com`)，而不是泛型域(例如， `s7d1.scene7.com`。 `s7d2.scene7.com`或 `s7d13.scene7.com`)。

要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。 查找標有 **[!UICONTROL 已發佈伺服器名稱]**。 如果您當前使用通用域，則可以請求移至您自己的自定義域。 在提交技術支援票證時發出此過渡請求。

您的第一個自定義域不需要額外的Dynamic Media許可證費用。

## 為我的帳戶啟用智慧映像的過程是什麼？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

啟動使用智慧映像的請求；未自動啟用。

預設情況下，Smart Imaging DPR和網路優化會為Dynamic Media公司帳戶禁用（關閉）。 如果要啟用（開啟）這些現成功能中的一項或兩項，請建立支援案例，如下所述。

<!-- NOW AVAILABLE IN ALL THREE REGIONS AS OF AUGUST 2. 2021. SEE CQDOC- 17915 The release schedule for Smart Imaging DPR and network optimization is available in North as follows:

| Region | Target date |
|---|---|
| North America | Live | 
| Europe, Middle East, Africa | 13 August 2021 | 
| Asia-Pacific | 22 July 2021 | -->

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在支援案例中提供以下資訊：

   1. 主要聯繫人姓名，電子郵件，電話。
   1. 要啟用智慧映像的所有域(即 `images.company.com` 或 `mycompany.scene7.com`)。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

      轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。

      查找標有 **[!UICONTROL 已發佈伺服器名稱]**。
   1. 驗證您是否正通過Adobe使用CDN，而不是使用直接關係進行管理。
   1. 驗證您是否使用專用域，如 `images.company.com` 或 `mycompany.scene7.com`，而不是泛型域，如 `s7d1.scene7.com`。 `s7d2.scene7.com`。 `s7d13.scene7.com`。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

      轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。

      查找標有 **[!UICONTROL 已發佈伺服器名稱]**。 如果您當前使用的是通用的Dynamic Media Classic域，則可以請求將此過渡過程的一部分移到您自己的自定義域。
   1. 指示是否希望它通過HTTP/2工作。

1. Adobe客戶支援根據請求的提交順序將您添加到智慧映像客戶等待清單。
1. 當Adobe準備好處理您的請求時，客戶支援會聯繫您以協調和設定目標日期。
1. **可選**:在將新功能推送到生產之前，您可以選擇在轉移中test智慧映像。
1. 完成後，客戶支援會通知您。
1. 為最大限度地提高智慧映像的效能，Adobe建議將「生存時間」(TTL)設定為24小時或更長。 TTL定義CDN快取資產的時間。 要更改此設定：

   1. 如果你用Dynamic Media Classic **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 映像伺服器]**。 設定 **[!UICONTROL 預設客戶端快取生存時間]** 值為24或更高。
   1. 如果你用Dynamic Media，跟上 [這些說明](config-dm.md)。 設定 **[!UICONTROL 到期]** 值24小時或更長。

## 我何時可以期望使用智慧映像啟用我的帳戶？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

請求按客戶支援根據等待清單接收的順序進行處理。

>[!NOTE]
>
>可能需要較長的提前期，因為啟用智慧映像涉及Adobe清除快取。 因此，在任何給定時間都只能處理少數客戶過渡。

## 切換到使用智慧映像有何風險？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客戶網頁沒有風險。 但是，向智慧映像的過渡確實會清除您的CDN快取。 這項行動涉及轉向Dynamic Media Classic或Dynamic Media的Experience Manager新配置。

在初始過渡期間，非快取映像直接命中Adobe的源伺服器，直到重新生成快取。 因此，Adobe計劃一次處理幾個客戶過渡，以便在從原點拉回請求時保持可接受的效能。 對於大多數客戶，在大約1到2天內在CDN上再次完全建立快取。

## 如何驗證智慧映像是否按預期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 配置了智慧映像後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager-Dynamic Media映像URL。
1. 通過轉到 **[!UICONTROL 視圖]** > **[!UICONTROL 開發人員]** > **[!UICONTROL 開發人員工具]** 的雙曲餘切值。 或者，選擇您選擇的任何瀏覽器開發工具。

1. 確保在開發人員工具開啟時禁用快取。

   * 在Windows®上，導航到開發人員工具窗格中的設定，然後選擇 **[!UICONTROL 禁用快取（當devtools處於開啟狀態時）]** 的子菜單。
   * 在macOS，在開發人員的窗格下 **[!UICONTROL 網路]** 頁籤 **[!UICONTROL 禁用快取]**。

1. 觀察內容類型已轉換為相應格式。 以下螢幕快照顯示了動態轉換為Chrome上WebP的PNG影像。
1. 在不同的瀏覽器和用戶條件上重複此test。

>[!NOTE]
>
>並非所有影像都已轉換。 Smart Imaging決定轉換是否可以提高效能。 有時，如果沒有預期的效能增益或格式不是JPEG或PNG，則不轉換影像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以關閉智慧映像以滿足任何請求？{#turning-off-smart-imaging}

是. 通過添加修飾符，可以關閉智慧成像 `bfc=off` 的子菜單。

## 是否可以請求在公司級別關閉DPR和網路優化？ {#dpr-companylevel-turnoff}

是. 要在您的公司禁用DPR和網路優化，請建立支援案例，如本主題前面所述。

## 有哪些「調諧」可用？ 是否可以定義任何設定或行為？ {#tuning-settings}

當前，您可以選擇啟用或禁用智慧映像。 沒有其他優化。

## 如果智慧映像管理質量設定，我是否可以設定最小值和最大值？ 例如，是否可以設定&quot;不低於60&quot;和&quot;不大於80質量&quot;? {#minimum-maximum}

當前智慧映像中沒有這種配置功能。

## 有時，JPEG影像會返回到Chrome而不是WebP影像。 為什麼會發生這種變化？ {#jpeg-webp}

Smart Imaging確定轉換是否有益。 僅當轉換導致檔案大小較小且質量相當時，才會返回新影像。

Smart Imaging DPR優化如何與Adobe Experience Manager Sites元件和Dynamic Media觀看者一起工作？

* Experience Manager Sites核心元件預設配置為DPR優化。 為避免因伺服器端智慧成像DPR優化而導致影像過大， `dpr=off` 始終添加到Experience Manager Sites核心元件Dynamic Media映像中。
* 預設情況下，為DPR優化配置了Dynamic Media基金會元件，以避免因伺服器端智慧成像DPR優化而導致影像過大， `dpr=off` 始終添加到Dynamic Media基金會元件映像。 即使客戶在DM Foundation Component中取消選擇DPR優化，伺服器端Smart Imaging DPR也不會啟動。 總之，在DM Foundation Component中，DPR優化僅基於DM Foundation Component級別設定生效。
* 任何查看器端DPR優化都與伺服器端Smart Imaging DPR優化配合工作，不會導致影像過大。 換句話說，無論DPR由查看器處理，如僅在啟用縮放的查看器中的主視圖，伺服器端智慧成像DPR值都不會觸發。 同樣，無論查看器元素（如色板和縮略圖）沒有DPR處理，都會觸發伺服器端的Smart Imaging DPR值。

另請參閱 [使用影像時](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用Smart Crop時](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)。

>[!MORELIKETHIS]
>
>* [採用WebP和AVIF格式的下一代影像優化。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
>

