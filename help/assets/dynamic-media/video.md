---
title: Dynamic Media 中的視訊
description: 瞭解如何在Dynamic Media中使用影片。 檢閱編碼視訊、將視訊發佈至YouTube、檢視視訊報表，以及將隱藏式字幕或章節標籤新增至視訊的最佳作法。
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: e8aac0bef0383604f54c09e2902c23bb89efe8f1
workflow-type: tm+mt
source-wordcount: '9357'
ht-degree: 2%

---

# 影片 {#video}

本節說明如何在Dynamic Media中使用視訊。

## 快速入門：影片 {#quick-start-videos}

下列逐步工作流程說明可協助您快速上手並執行Dynamic Media中的最適化視訊集。 每個步驟之後，都有主題標題的互動參照，您可以在其中找到更多資訊。

>[!NOTE]
>
>在Dynamic Media中處理視訊之前，請確定Adobe Experience Manager管理員已啟用並設定Dynamic MediaCloud Service。
>
>* 請參閱「設定Dynamic Media」中的[設定Dynamic MediaCloud Service](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)和[疑難排解Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md)。
>

1. **執行下列動作，上傳您的Dynamic Media影片**：

   * 建立您自己的視訊編碼設定檔。 或者，您只需使用Dynamic Media隨附的預先定義&#x200B;_最適化視訊編碼_&#x200B;設定檔即可。

      * [建立視訊編碼設定檔](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 深入瞭解[視訊編碼的最佳實務](#best-practices-for-encoding-videos)。

   * 將視訊處理設定檔與您要上傳主要來源視訊的一或多個資料夾建立關聯。

      * [將視訊設定檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
      * 深入瞭解[組織數位資產](/help/assets/organize-assets.md)。

   * 將您的主要來源視訊上傳至資料夾。 將視訊新增至資料夾時，會根據您指派至資料夾的視訊處理設定檔進行編碼。

      * Dynamic Media主要支援長度上限為30分鐘，最小解析度大於25 x 25的短片影片。
      * 您可以上傳每個大小最多15 GB的視訊檔案。
      * [上傳您的視訊](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
      * 深入瞭解[支援的輸入檔案格式](/help/assets/file-format-support.md)。

   * 監視資產或工作流程檢視中[視訊編碼的進度](#monitoring-video-encoding-and-youtube-publishing-progress)。

1. **執行下列任一項作業，管理您的Dynamic Media影片**：

   * 組織、瀏覽和搜尋視訊資產

      * [組織數位資產](/help/assets/organize-assets.md)
      * [搜尋視訊資產](/help/assets/search-assets.md#custompredicates)或[搜尋資產](/help/assets/manage-digital-assets.md#search-assets)

   * 預覽和發佈視訊資產

      * 檢視視訊的來源視訊和編碼轉譯及其相關縮圖：
        [預覽視訊](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)或[預覽資產](/help/assets/dynamic-media/previewing-assets.md)
        [管理視訊轉譯](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * 使用視訊中繼資料

      * 編輯視訊的屬性，例如標題、說明和標籤、自訂中繼資料欄位：
        [正在編輯視訊內容](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理數位資產的中繼資料](/help/assets/manage-metadata.md)
      * [中繼資料結構描述](/help/assets/metadata-schemas.md)

   * 檢閱、核准和註釋視訊，並維持完整的版本控制

      * [為視訊加上註解](/help/assets/manage-video-assets.md#annotate-video-assets)或[為資產加上註解](/help/assets/manage-digital-assets.md#annotating)

      * [建立版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [在資產上啟動工作流程](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [檢閱資料夾資產](/help/assets/bulk-approval.md)
      * [專案](/help/sites-cloud/authoring/projects/overview.md)

1. **執行下列其中一項作業，以Publish您的Dynamic Media影片**：

   * 如果您使用Experience Manager做為WCM （Web內容管理）系統，可以直接將視訊新增至網頁。

      * [新增視訊至您的網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

   * 如果您使用協力廠商網站內容管理系統，您可以將影片連結或內嵌至網頁。

      * 使用URL整合視訊：
        [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。

      * 使用網頁上的內嵌程式碼整合影片：
        [將視訊檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)。

   * [產生視訊報告](#viewing-video-reports)。

   * [新增字幕至視訊](#adding-captions-to-video)。

## 在Dynamic Media中處理視訊 {#working-with-video-in-dynamic-media}

Dynamic Media中的視訊是端對端解決方案，可讓您輕鬆發佈高品質的最適化視訊，以跨多個熒幕（包括桌上型電腦、平板電腦和行動裝置）串流。 「最適化視訊集」會將使用不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 桌上型電腦或行動裝置會偵測可用的頻寬。

例如，在iOS行動裝置上，它會偵測3G、4G或Wi-Fi等頻寬。 之後，它會從「自我調整視訊集」中的各種視訊位元速率中，自動選取正確的編碼視訊。 影片會串流至桌上型電腦、行動裝置或平板電腦。

此外，如果桌上型電腦或行動裝置上的網路狀況改變，視訊品質會自動動態切換。 此外，如果客戶在桌上型電腦上進入全熒幕模式，Adaptive Video Set會使用更好的解析度來回應，進而改善客戶的觀看體驗。 使用自我調整視訊集可以為客戶在多個熒幕和裝置上播放Dynamic Media視訊提供最佳播放方式。

視訊播放器用來決定要播放或播放期間要選取已編碼視訊的邏輯，是根據下列演演算法：

1. 視訊播放器會根據位元速率（最接近在播放器本身中為「初始位元速率」設定的值）載入初始視訊片段。
1. 視訊播放器會根據使用下列條件的頻寬速度變更進行切換：

   1. 播放器會挑選低於或等於預估頻寬的最高頻寬資料流。
   1. 播放器只考慮80%的可用頻寬。 不過，如果調高了，則比較保守的是只有70%，以避免高估並立即調回。

如需演演算法的詳細技術資訊，請參閱[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

對於管理單一視訊和自我調整視訊集，支援下列專案：

* 以多種支援的視訊格式和音訊格式上傳視訊，並將視訊編碼為MP4 H.264格式，以便跨多個熒幕播放。 您可以使用預先定義的自我調整視訊預設集、單一視訊編碼預設集，或自訂自己的編碼來控制視訊的品質和大小。

   * 產生最適化視訊集時，其中會包含MP4視訊。
   * **注意**：主要/來源視訊未新增至最適化視訊集。

* 所有HTML5視訊檢視器中的視訊字幕。
* 使用完整中繼資料支援來組織、瀏覽和搜尋視訊，以有效管理視訊資產。
* 將最適化視訊集傳送至網頁版、桌上型電腦、平板電腦和行動裝置。

各種iOS平台均支援最適化視訊串流。 請參閱[Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html)。

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media視訊檢視器預設集播放視訊，包括下列專案：

   * 單一視訊檢視器。
   * 結合視訊和影像內容的混合媒體檢視器。

* 設定視訊播放器以符合您的品牌需求。
* 使用簡單的URL或內嵌程式碼將視訊整合至您的網站、行動網站或行動應用程式。

請參閱[動態視訊播放](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480)範例。

另請參閱[Experience Manager Assets檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)中的[Experience Manager Assets檢視器和Dynamic Media Classic ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc)以及[僅適用於Dynamic Media的檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only)。

## 最佳實務：使用HTML5視訊檢視器 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5視訊檢視器預設集是強大的視訊播放器。 您可以使用它們來避免許多與HTML5視訊播放相關的常見問題，以及與行動裝置相關的問題。 例如，缺乏最適化位元速率串流傳送，且桌上型電腦瀏覽器的觸及範圍有限。

在播放器的設計方面，您可以使用標準Web開發工具來設計視訊播放器的功能。 例如，您可以使用HTML5和CSS來設計按鈕、控制項和自訂海報影像背景，協助您以自訂外觀觸及客戶。

在檢視器的播放端，會自動偵測瀏覽器的視訊功能。 然後它會使用HLS或DASH （也稱為最適化視訊串流）提供視訊。 或者，如果這些傳送方法不存在，則改用HTML5 progressive。

>[!NOTE]
>
>若要在視訊中使用DASH，必須先由您帳戶上的Adobe技術支援啟用。 請參閱[在您的帳戶上啟用DASH](#enable-dash)。

您可以使用HTML5和CSS將設計播放元件的功能結合為單一播放器。 它可以內嵌播放，並根據瀏覽器的功能使用最適化和漸進式串流。 這項功能意味著，您可以將多媒體內容的觸角伸展至桌上型電腦和行動使用者，並確保簡化的視訊體驗。

另請參閱[Experience Manager Assets檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)中的[僅適用於Dynamic Media的檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only)。


### 使用HTML5視訊檢視器在桌上型電腦和行動裝置上播放視訊 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

就桌上型電腦和行動最適化視訊串流而言，用於位元速率切換的視訊均以最適化視訊集中的所有MP4視訊為基礎。

使用HLS或DASH或漸進式視訊下載進行視訊播放。 在舊版Experience Manager （例如6.0、6.1和6.2）中，影片會透過HTTP進行串流處理。

不過，在Experience Manager6.3及更新版本中，視訊現在會透過HTTPS （亦即HLS或DASH）進行串流，因為DM閘道服務URL也一律使用HTTPS。 此預設行為不會影響客戶。 也就是說，除非瀏覽器不支援視訊串流，否則一律會透過HTTPS進行視訊串流。 請參閱下表。

因此，

* 如果您的HTTPS網站採用HTTPS視訊串流，則串流沒有問題。
* 如果您的HTTP網站具有HTTPS視訊串流，串流就不會有問題，而且網頁瀏覽器也不會出現混合內容問題。

DASH是國際標準，HLS是Apple標準。 兩者都用於自我調整視訊串流。 而且，這兩種技術都會根據網路頻寬容量自動調整播放。 它也能讓客戶「搜尋」視訊中的任何位置，而不需要等候視訊的其餘部分下載。

漸進式視訊的傳送方式，是將視訊下載並儲存在使用者的案頭系統或行動裝置上。

下表說明使用[Dynamic Media HTML5視訊檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video)在桌上型電腦和行動裝置上播放視訊的裝置、瀏覽器和方法。

<table>
 <tbody>
  <tr>
   <td><strong>裝置</strong></td>
   <td><strong>瀏覽器</strong></td>
   <td><strong>視訊播放模式</strong></td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Internet Explorer 9和10</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows® 8和Windows® 10上 — 只要要求DASH或HLS，就強制使用HTTPS。 已知限制： DASH或HLS上的HTTP在此瀏覽器/作業系統組合中無法運作<br /> <br /> Windows® 7上的 — 漸進式下載。 使用標準邏輯來選取HTTP與HTTPS通訊協定。</td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Firefox 23-44</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Firefox 45或更新版本</td>
   <td>HLS或DASH*最適化位元速率串流</td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Chrome</td>
   <td>HLS或DASH*最適化位元速率串流</td>
  </tr>
  <tr>
   <td>桌上型電腦</td>
   <td>Safari (Mac)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Chrome (Android™ 6或更舊版本)</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Chrome (Android™ 7或更新版本)</td>
   <td>HLS或DASH*最適化位元速率串流/td&gt;
  </tr>
  <tr>
   <td>行動</td>
   <td>Android™ （預設瀏覽器）</td>
   <td>漸進式下載。</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Safari (iOS)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Chrome (iOS)</td>
   <td>HLS最適化位元速率串流</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*若要在視訊中使用DASH，必須先由帳戶上的Adobe技術支援啟用。 請參閱[在您的帳戶上啟用DASH](#enable-dash)。)

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media視訊解決方案的架構 {#architecture-of-dynamic-media-video-solution}

下圖顯示透過DMGateway (在Dynamic Media混合模式中)上傳及編碼，並可供公眾使用的視訊整體製作工作流程。

![chlimage_1-427](assets/chlimage_1-427.png)

## 視訊的混合式發佈架構 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 視訊編碼最佳作法 {#best-practices-for-encoding-videos}

如果您已啟用Dynamic Media並設定視訊Cloud Service，則&#x200B;**Dynamic Media編碼視訊**&#x200B;工作流程會對視訊進行編碼。 此工作流程會擷取工作流程處理歷程記錄和失敗資訊。如果您已啟用Dynamic Media並設定視訊Cloud Service，當您上傳視訊時，**[!UICONTROL Dynamic Media編碼視訊]**&#x200B;工作流程會自動生效。 (如果您未使用Dynamic Media，**[!UICONTROL DAM更新資產]**&#x200B;工作流程將會生效。)

以下是編碼來源視訊檔案的最佳實務提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### Source視訊檔案 {#source-video-files}

編碼視訊檔案時，請使用最高品質的來源視訊檔案。 避免使用先前編碼的視訊檔案，因為這些檔案已經過壓縮，進一步編碼會產生品質不佳的視訊。

* Dynamic Media主要支援長度上限為30分鐘，最小解析度大於25 x 25的短片影片。
* 您可以上傳每個大小最高達15 GB的主要來源視訊檔案。

下表說明編碼來源視訊檔案前，其建議的大小、外觀比例和最低位元速率等資訊：

| 大小 | 外觀比例 | 最小位元速率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 大部分的視訊為4500 kbps。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps （視視訊中的移動量而定）。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps （視視訊中的移動量而定）。 |

### 取得檔案的中繼資料 {#obtaining-a-file-s-metadata}

您可以使用視訊編輯工具檢視檔案的中繼資料，或使用專為取得中繼資料而設計的應用程式，來取得檔案的中繼資料。 以下是使用MediaInfo （協力廠商應用程式）來取得視訊檔案中繼資料的指示：

1. 移至[MediaInfo下載](https://mediaarea.net/en/MediaInfo/Download)。
1. 選取並下載GUI版本的安裝程式，然後依照安裝指示操作。
1. 安裝之後，請以滑鼠右鍵按一下視訊檔案(僅限Windows®)並選取MediaInfo，或開啟MediaInfo並將視訊檔案拖曳到應用程式中。 您會看到與視訊檔案相關的所有中繼資料，包括其寬度、高度和fps。

### 外觀比例 {#aspect-ratio}

當您選擇或建立主要來源視訊檔案的視訊編碼預設集時，請確定預設集具有與主要來源視訊檔案相同的外觀比例。 外觀比例是視訊的寬度與高度的比例。

若要判斷視訊檔案的外觀比例，請取得檔案的中繼資料，並注意檔案的寬度和高度（請參閱上述取得檔案的中繼資料）。 然後使用此公式來決定外觀比例：

寬度/高度=外觀比例

下表說明公式結果如何轉換成常見的外觀比例選擇：

| 公式結果 | 外觀比例 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，視訊的寬度為1440 x高度為1080，其外觀比例為1440/1080，即1.33。在這種情況下，您可以選擇外觀比例為4:3的視訊編碼預設集來編碼視訊檔案。

### 位元速率 {#bitrate}

Bitrate是經過編碼而構成視訊播放一秒的資料量。 位元速率是以每秒千位元(Kbps)來測量。

>[!NOTE]
>
>由於所有轉碼器都使用有失真壓縮，因此位元速率是視訊品質中最重要的因素。 使用有失真壓縮時，您壓縮視訊檔案的次數越多，品質就越會降低。 因此，其他所有特性相等（解析度、影格速率和轉碼器），位元速率越低，壓縮檔案的品質就越低。

選取位元速率編碼時，您可以選擇兩種型別：

* **[!UICONTROL 固定位元速率編碼]** (CBR) — 在CBR編碼期間，位元速率或每秒位元數在整個編碼過程中保持不變。 CBR編碼會在整個視訊中，將設定的資料速率儲存至您的設定。 此外，CBR編碼無法最佳化媒體檔案的品質，但會節省儲存空間。
如果您的視訊在整個視訊中包含類似的動作層級，請使用CBR。 CBR最常用於串流視訊內容。 另請參閱[使用自訂新增的視訊編碼引數](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters)。

* **[!UICONTROL 可變位元速率編碼]** (VBR) - VBR編碼會根據壓縮器所需的資料，將資料速率向下調整到您所設定的上限。 此功能表示在VBR編碼程式期間，媒體檔案的位元速率會根據媒體檔案位元速率需求動態增加或減少。
VBR需要更長的時間來編碼，但會產生最有利的結果；媒體檔案的品質優異。 VBR最常用於http漸進式傳送視訊內容。

何時使用VBR或CRB？
在選取VBR與CBR時，幾乎總是建議您將VBR用於媒體檔案。 VBR以具競爭力的位元速率提供更高品質的檔案。 使用VBR時，請務必使用兩階段編碼，並將最大位元速率設定為目標視訊位元速率的1.5倍。

當您選擇視訊編碼預設集時，請務必說明目標使用者的連線速度。 選擇資料速率為該速度80%的預設集。 例如，如果目標使用者的連線速度是1000 Kbps，則最佳預設集是視訊資料速率為800 Kbps的預設集。

此表格說明一般連線速度的資料速率。

| 速度(Kbps) | 連線型別 |
|--- |--- |
| 256 | 撥號連線。 |
| 800 | 一般行動連線。 針對此連線，針對3G體驗將資料速率目標定在400到最高800之間。 |
| 2000 | 典型的寬頻案頭連線。 針對此連線，將資料速率目標設定在800至2000 Kbps範圍內，大部分目標平均為1200至1500 Kbps。 |
| 5000 | 典型的高寬頻連線。 不建議在此上限範圍內進行編碼，因為大多數消費者無法使用此速度的視訊傳送。 |

### 解決方法 {#resolution}

**解析度**&#x200B;描述視訊檔案的高度和寬度（畫素）。 大部分的來源視訊都是以高解析度儲存（例如1920 x 1080）。 為了串流目的，來源視訊會壓縮成較小的解析度（640 x 480或更小）。

解析度和資料速率是決定視訊品質的兩個整合因素。 若要維持相同的視訊品質，視訊檔案中的畫素數越高（解析度越高），資料速率就必須越高。 例如，假設在320 x 240解析度和640 x 480解析度視訊檔案中，每個影格的畫素數：

| 解決方法 | 每個影格的畫素 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480檔案的每個影格畫素會增加4倍。 若要讓這兩個範例解析度達到相同的資料速率，您可以對640 x 480檔案套用四倍的壓縮，這會降低視訊的品質。 因此，250 Kbps的視訊資料速率可以以320 x 240的解析度提供高品質的觀賞效果，但無法以640 x 480的解析度提供。

一般而言，您使用的資料速率越高，視訊顯示效果就越好，而且您使用的解析度越高，您必須維持的檢視品質資料速率就越高（相較於解析度較低的情況）。

由於解析度和資料速率是相互關聯的，在編碼視訊時，您有兩個選項：

* 選擇資料速率，然後以最高解析度編碼，以您所選擇的資料速率顯示良好。
* 選擇解析度，然後以您選擇的解析度進行必要的資料速率編碼，以取得高品質的視訊。

當您選擇（或建立）主要來源視訊檔案的視訊編碼預設集時，請使用此表格來鎖定正確的解析度：

| 解決方法 | 高度 (像素) | 熒幕大小 |
|--- |--- |--- |
| 240p | 240 | 超小熒幕 |
| 300p | 300 | 通常適用於行動裝置的小熒幕 |
| 360p | 360 | 小熒幕 |
| 480p | 480 | Medium畫面 |
| 720p | 720 | 大熒幕 |
| 1080p | 1080 | 高解析度大熒幕 |

### Fps （每秒影格數） {#fps-frames-per-second}

在美國和日本，大部分的視訊是以每秒29.97幀(fps)的速率拍攝；在歐洲，大部分的視訊是以每秒25幀(fps)的速率拍攝。 電影的拍攝速度為24 fps。

選擇符合主要來源視訊檔案的fps速率的視訊編碼預設集。 例如，如果您的主要來源視訊是25 fps，請選擇具有25 fps的編碼預設集。 依預設，所有自訂編碼都會使用主要來源視訊檔案的fps。 因此，當您建立視訊編碼預設集時，不需要明確指定fps設定。

### 視訊編碼維度 {#video-encoding-dimensions}

為獲得最佳結果，請選取編碼維度，好讓來源視訊是所有已編碼視訊的整數倍。

若要計算此比率，請將來源寬度除以編碼寬度來得出寬度比率。 接著，將來源高度除以編碼後的高度，得出高度比率。

如果產生的比例是整數，表示影片會以最佳方式縮放。 如果產生的比率不是整數，則會影響視訊品質，在顯示區留下多餘的畫素不自然感。 當視訊中含有文字時，此效果最為明顯。

例如，假設您的來源視訊是1920 x 1080。 在下表中，三個已編碼的視訊提供要使用的最佳編碼設定。

| 視訊型別 | 寬x高 | 寬度比例 | 高度比例 |
|--- |--- |--- |--- |
| 來源 | 1920 x 1080 | 1 | 1 |
| 已編碼 | 960 x 540 | 2 | 2 |
| 已編碼 | 640 x 360 | 3 | 3 |
| 已編碼 | 480 x 270 | 4 | 4 |

### 已編碼的視訊檔案格式 {#encoded-video-file-format}

Dynamic Media建議使用MP4 H.264視訊編碼預設集。 由於MP4檔案使用H.264視訊轉碼器，因此可提供高品質的視訊，但檔案大小必須經過壓縮。

## 檢視視訊報表 {#viewing-video-reports}

>[!NOTE]
>
>視訊報表僅適用於執行Dynamic Media — 混合模式時。

視訊報表會顯示指定期間內的數個彙總量度，協助您監視&#x200B;*已發佈*&#x200B;個別和彙總視訊是否如預期般執行。 系統會針對您整個網站的所有已發佈影片，彙總下列排名在前的量度資料：

* 視訊開始
* 完成率
* 視訊平均逗留時間
* 影片花費的總時間
* 每次造訪的視訊數

也會列出所有&#x200B;*已發佈*&#x200B;影片的表格，如此一來，您就可以根據影片開始總數，追蹤網站上檢視次數最多的影片。

當您在清單中選取視訊名稱時，會以折線圖的形式顯示視訊的對象保留率（流失）報表。 此圖表顯示視訊播放期間任何指定時間的檢視次數。 當您播放視訊時，垂直列會與播放器中的時間指示器同步追蹤。 折線圖資料中的下降會指出您的對象從哪裡開始不感興趣。

如果影片是在Adobe Experience Manager Dynamic Media之外編碼，則無法使用表格中的對象保留率（流失）圖表和播放百分比資料。

>[!NOTE]
>
>追蹤和報表資料僅以Dynamic Media自己的視訊播放器及相關聯的視訊播放器預設集的使用為基礎。 因此，您無法追蹤和報告透過其他視訊播放器播放的視訊。

根據預設，您首次輸入「視訊報表」時，報表會顯示從當月第一個日期開始，到當月日期結束的視訊資料。 不過，您可以指定自己的日期範圍來覆寫預設日期範圍。 下次輸入視訊報表時，將會使用您指定的日期範圍。

為了讓視訊報表正常運作，設定Dynamic MediaCloud Service時會自動建立報表套裝ID。 同時，報表套裝ID會推送至Publish伺服器，以便您在預覽資產時可用於複製URL功能。 不過，若要使用此功能，必須先設定Publish伺服器。 如果Publish伺服器未設定，您仍可發佈以檢視視訊報表。 不過，您必須返回Dynamic Media雲端設定，並選取&#x200B;**[!UICONTROL 確定]**。

**若要檢視視訊報告：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側導軌中，導覽至&#x200B;**[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL Assets]** > **[!UICONTROL 視訊報表]**。
1. 在「視訊報表」頁面上，執行下列任一項作業：

   * 在右上角附近，選取&#x200B;**[!UICONTROL 重新整理視訊報告]**圖示。
只有在報表的結束日期為當天時，才可使用重新整理。 此功能可確保您看到自上次執行報表以來發生的視訊追蹤。

   * 在右上角附近，選取&#x200B;**[!UICONTROL 日期選擇器]**圖示。
指定您要視訊資料的開始和結束日期範圍，然後選取**[!UICONTROL 執行報表]**。

   「排名在前的量度」群組方塊可識別您網站上所有&#x200B;*已發佈*&#x200B;視訊的各種彙總測量。

1. 在列出最熱門發佈影片的表格中，選取影片名稱以播放影片，並參閱影片的「對象保留率（流失）」報表。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->





## 在您的Dynamic Media帳戶上啟用DASH、多字幕和多音訊曲目支援 {#enable-dash}

**關於啟用您帳戶的DASH支援**
DASH (Digital Adaptive Streaming over HTTP)是視訊串流的國際標準，被廣泛採用於不同的視訊檢視器中。 當您的帳戶啟用DASH時，您可以選擇使用DASH或HLS進行最適化視訊串流。 或者，當您在檢視器預設集中選取**[!UICONTROL auto]**&#x200B;作為播放型別時，可以選擇在播放器之間自動切換。

在您的帳戶上啟用DASH的一些主要優點包括：

* 封裝DASH串流視訊，以進行最適化位元速率串流。 此方法可提高傳遞效率。 最適化串流可確保為客戶提供最佳檢視體驗。
* 使用Dynamic Media播放器最佳化的瀏覽器串流可在HLS和DASH串流之間切換，以確保最佳服務品質。 使用Safari瀏覽器時，視訊播放器會自動切換至HLS。
* 您可以編輯視訊檢視器預設集，以設定您偏好的串流方法（HLS或DASH）。
* 最佳化的視訊編碼可確保啟用DASH功能時不會使用額外的儲存空間。 會針對HLS和DASH建立單一視訊編碼集，以最佳化視訊儲存成本。
* 協助讓客戶更容易存取視訊傳送。
* 也透過API取得串流URL。

在您的帳戶上啟用DASH支援，是透過您建立和提交的Adobe客戶支援案例來完成。

**關於在您的帳戶上啟用多重註解和音訊追蹤支援**

在您建立Adobe支援案例以在帳戶上啟用DASH的同時，您還可以從自動啟用多個註解和音訊追蹤支援中受益。 啟用後，您上傳的所有後續視訊都會透過新的後端架構進行處理，包括支援在視訊中新增多個註解和音訊曲目。

>[!IMPORTANT]
>
>在&#x200B;*之前，您已在您的Dynamic Media帳戶[上啟用多重註解和音訊追蹤支援，因此您上傳的任何視訊都必須重新處理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。*&#x200B;此視訊重新處理步驟是必要的，這樣使用者才能使用多個註解和音訊追蹤功能。 重新處理之後，視訊URL仍可繼續如常運作和播放。

**若要在您的Dynamic Media帳戶上啟用DASH、多字幕和多音訊曲目支援：**

1. [使用此Admin Console開始建立新的支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 若要建立支援案例，請遵循指示，同時確保您提供下列資訊：

   * 主要連絡人姓名、電子郵件、電話。
   * 您的Cloud Service環境（方案ID和環境ID）。
   * 您的Dynamic Media公司帳戶名稱。
   * 您的Dynamic Media地區：北美(NA)、亞太(APAC)或歐洲 — 中東 — 亞洲(EMEA)。
   * 指定您想在Dynamic Media帳戶上，於Experience Manager6.5啟用DASH、多註解和多音訊追蹤支援。

1. 「Adobe客戶支援」會根據提交請求的順序，將您新增至「客戶等候清單」。
1. 當Adobe準備好處理您的請求時，客戶支援聯絡您以協調並設定啟用的目標日期。
1. 客戶支援會在完成後通知您。
1. 現在您可以執行下列任一項作業：

   * 照常建立您的[視訊檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)。
   * [新增多個字幕和音軌](#add-msma)到您的視訊。


## 關於Dynamic Media中視訊的多重註解和音訊追蹤支援{#about-msma}

透過Dynamic Media中的多重字幕與音訊追蹤功能，您可以輕鬆將多重字幕與音訊追蹤新增至主要視訊。 此功能表示全球對象都可以存取您的影片。您可以以多種語言向全球對象自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。此外，作者還可以在使用者介面的單一標籤管理字幕和音軌。

![Dynamic Media中的註解與音訊曲目索引標籤，以及顯示已上傳的.VTT註解檔案和已上傳之視訊的.MP3音訊曲目檔案的表格。](/help/assets/dynamic-media/assets/msma-subtitle-audiotracks-tab2.png)

在主要視訊中新增多個字幕和音訊曲目時，需要考量的部分使用案例包括：

| 類型 | 使用案例 |
|--- |--- |
| **字幕** | 多語言支援 |
|  | 協助工具的描述性文字 |
| **曲目** | 多語言支援 |
|  | 註解追蹤 |
|  | 描述性音訊 |

Dynamic Media](/help/assets/file-format-support.md)和所有Dynamic Media視訊檢視器(除了Dynamic Media *Video_360*&#x200B;檢視器)支援的所有[視訊格式都支援搭配多個字幕和音軌使用。

您的Dynamic Media帳戶可使用多註解和多音訊追蹤功能，其方式為必須由Adobe客戶支援啟用（開啟）的功能切換。

### 在視訊中新增多個註解和音訊曲目 {#add-msma}

在將多個註解和音訊曲目加入視訊之前，請確定您已具備下列內容：

* Dynamic Media是在AEM環境中設定的。
* [Dynamic Media視訊設定檔已套用至您擷取視訊的資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
* [已在您的Dynamic Media帳戶上啟用多重註解和多音訊曲目](#enable-dash)。

新增的字幕和註解支援WebVTT和Adobe VTT格式。 此外，新增的音訊軌跡檔案也支援MP3格式。

>[!IMPORTANT]
>
>在&#x200B;*之前，您已在您的Dynamic Media帳戶[上啟用多重註解和音訊追蹤支援，因此您上傳的任何視訊都必須重新處理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。*&#x200B;此視訊重新處理步驟是必要的，這樣使用者才能使用多個註解和音訊追蹤功能。 重新處理之後，視訊URL仍可繼續如常運作和播放。

**若要在視訊中新增多個字幕與音軌：**

1. [將您的主要視訊上傳至已指派視訊設定檔的資料夾](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
1. 導覽至您要新增多個標題和音訊曲目的上傳視訊資產。
1. 在資產選取模式中，從「清單檢視」或「卡片檢視」中選取視訊資產。
1. 在工具列上，選取「屬性」圖示（內有「i」的圓形）。
   ![選取的視訊資產在視訊縮圖影像上加上核取記號，並在工具列上反白顯示「檢視屬性」。](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*在卡片檢視中選取的視訊資產。*
1. 在視訊的[內容]頁面上，選取&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤。

   >[!TIP]
   >如果您看不到&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤，表示有下列其中一種情況：
   >
   >* 選取的視訊所在的資料夾未指派視訊設定檔。 在這種情況下，請參閱[將視訊設定檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* 或者，影片必須由Dynamic Media重新處理。 在這種情況下，請參閱[重新處理資料夾](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)中的Dynamic Media資產。
   >
   >完成上述任一項工作後，請回到這些步驟。

   在[內容]頁面上的![註解和音軌索引標籤。在視訊的[內容]頁面上，](/help/assets/dynamic-media/assets/msma-audiotracks2.png)*註解與音訊曲目索引標籤。*

1. （可選）若要新增一或多個註解檔案至視訊，請執行下列動作：
   * 選取&#x200B;**[!UICONTROL 上傳字幕]**。
   * 導覽至一或多個.vtt （視訊文字軌）檔案，並加以開啟。
   * 若要在媒體播放器上顯示註解，您&#x200B;*必須*&#x200B;新增您上傳的每個&#x200B;*註解檔案的必要詳細資料（中繼資料）。*&#x200B;選取註解檔案名稱右側的鉛筆圖示。 在&#x200B;**編輯標題**&#x200B;對話方塊中，輸入下列檔案的必要詳細資訊，然後選取&#x200B;**[!UICONTROL 儲存]**。 對您上傳的每個註解檔案重複此程式：

     | 標題中繼資料 | 說明 |
     |--- |--- |
     | 檔案名稱 | 預設檔案名稱衍生自原始檔案名稱。 檔案名稱只能在上傳時變更，以後無法變更。 檔案名稱字元需求與AEM Assets相同。<br>其他註解檔和音訊曲目檔不能使用相同的檔名。 |
     | 語言 | 選取註解的語言。 |
     | 類型 | 選取您使用的註解型別。<br>**Subtitle** — 與視訊一起顯示的標題文字，該視訊會翻譯或轉譯對話方塊。<br>**註解** — 註解文字也包含背景噪音、說話者辨別與其他相關資訊，以及對話方塊的翻譯或轉錄，讓耳聾或聽力缺佳的人更容易存取內容。 |
     | 標籤 | 在媒體播放器的&#x200B;**[!UICONTROL 選取音訊或標題]**&#x200B;快顯清單中，為標題名稱顯示的文字。 客戶看到的標籤與副標題或標題追蹤相對應。 例如，`English (CC)`。 |

     如有需要，您可以稍後變更或編輯註解中繼資料。 發佈影片時，這些詳細資料會反映在已發佈影片中的公開URL上。

1. （選用）若要將一或多個音軌新增至視訊，請執行下列動作：
   * 選取&#x200B;**[!UICONTROL 上傳音軌]**。
   * 導覽至一或多個.mp3檔案並加以選取，然後開啟。
   * 為了在媒體播放器上的&#x200B;**[!UICONTROL 選取音訊或標題]**&#x200B;快顯清單中顯示音軌，您&#x200B;*必須*&#x200B;新增您新增的&#x200B;*每個*&#x200B;音軌檔案的必要詳細資料。 選取音軌檔案名稱右側的鉛筆圖示。 在&#x200B;**編輯音軌**&#x200B;對話方塊中，輸入下列必要的詳細資料，然後選取&#x200B;**[!UICONTROL 儲存]**。 為您上傳的每個音訊曲目檔案重複此程式。

     | 音訊曲目中繼資料 | 說明 |
     |--- |--- |
     | 檔案名稱 | 預設檔案名稱衍生自原始檔案名稱。 檔案名稱只能在上傳時變更，以後無法變更。 檔案名稱字元需求與AEM Assets相同。<br>其他音訊曲目檔或標題檔不能使用相同的檔名。 |
     | 語言 | 選取音訊曲目的語言。 |
     | 類型 | 選取您正在使用的音軌型別。<br>**原始** — 音訊曲目最初附加至視訊，並在預設選取語言為`English`的標籤中以`[Original]`表示。 雖然&#x200B;**[!UICONTROL 標籤]**&#x200B;和&#x200B;**[!UICONTROL 語言]**&#x200B;可以在&#x200B;**[!UICONTROL 編輯音軌]**&#x200B;對話方塊中變更，但如果重新處理主要視訊，預設值會為原始值。<br>**標準** — 原始語言以外的附加音軌。<br>**音訊描述** — 音訊曲目也包含視訊中非語言動作和手勢的描述性旁白，讓視障者更容易存取內容。 |
     | 標籤 | 在媒體播放器的&#x200B;**[!UICONTROL 選取音訊或標題]**&#x200B;快顯清單中顯示為音軌名稱的文字。 客戶看到的標籤與音訊軌相對應。 例如 `English [Original]`。附加至視訊的音訊標籤預設為`[Original]`。 |

     如有需要，您可以稍後變更或編輯此音訊曲目中繼資料。 發佈影片時，這些詳細資料會反映在已發佈影片中的公開URL上。

1. 在頁面的右上角，從&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 儲存]**。 檔案已上傳，且中繼資料處理已開始，如介面的&#x200B;**狀態**&#x200B;欄中所示。

   >[!NOTE]
   >
   >根據您執行個體的快取設定，中繼資料處理可能需要幾分鐘時間，才會反映在預覽和已發佈的URL中。

1. （選擇性）如果您在上一步選取了&#x200B;**[!UICONTROL 儲存並關閉]**，而不是選取&#x200B;**[!UICONTROL 儲存]**，您仍可檢視已上傳檔案的處理狀態。 請參閱[檢視上傳的標題和音訊曲目檔案的生命週期狀態](#lifecycle-status-video)。
1. （可選）在發佈之前預覽視訊，以確保字幕和音訊如預期般運作。 檢視[預覽含有多個字幕和音軌的視訊](#preview-video-audio-subtitle)
1. Publish影片。 檢視[Publish資產](publishing-dynamicmedia-assets.md)。

#### 關於新增標題和音訊曲目檔案至已發佈的視訊

當您上傳其他註解檔案或音訊曲目檔案到已發佈的視訊時，這表示這些檔案在上傳後準備就緒後將具有`Processed`狀態。 此時，您可以在Dynamic Media中預覽視訊，以檢視或聆聽新上傳的檔案。

不過，在預覽後，您必須&#x200B;*發佈*&#x200B;視訊，才能同時發佈新加入的註解或音訊曲目檔案。 發佈後，公開Dynamic Media URL即可使用註解或音訊。

>[!NOTE]
>
>根據您執行個體的快取設定，中繼資料更新可能需要幾分鐘的時間才會反映在預覽和已發佈的URL中。

在您設定立即發佈Dynamic Media的案例中，上傳其他註解或音訊檔案會立即觸發上傳註解或音訊檔案後的視訊發佈。

>[!CAUTION]
>
>當您上傳註解檔案或音訊檔案到已發佈或取消發佈的視訊時，如果您&#x200B;[*重新處理*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)&#x200B;視訊，檔案將會被刪除。 只有視訊的原始音訊會維持不變。 在這種情況下，您必須再次將註解檔案和音訊曲目檔案重新上傳到視訊。

#### 在具有現有URL和註解修飾元的視訊中新增多個註解

Dynamic Media支援透過URL修飾元在視訊中新增單一標題。 請參閱[將註解新增至視訊](#adding-captions-to-video)。

多個註解變更的優先順序高於透過已發佈視訊URL修飾元新增的註解。

**若要將多個註解新增至具有註解修飾元之現有URL的視訊：**

1. 上傳已新增為視訊修飾元的註解檔案，以便您明確管理檔案。
1. 視需要上傳任何其他註解檔案。
1. 照常使用Publish視訊。
具有註解修飾元的現有URL現在可以載入多個註解。

### 檢視上傳的標題和音訊曲目檔案的生命週期狀態{#lifecycle-status-video}

您可以觀察從&#x200B;**屬性**&#x200B;的&#x200B;**註解和音軌**&#x200B;索引標籤上傳到主要視訊的任何註解或音軌檔案的生命週期狀態。

**若要檢視視訊的生命週期狀態：**

1. 導覽至您要檢視其生命週期狀態的視訊資產。
1. 在資產選取模式中，從「清單檢視」或「卡片檢視」中選取視訊資產。
1. 在工具列上，選取「屬性」圖示（內有「i」的圓形）。
1. 在[內容]頁面上，選取&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤。 在「狀態」欄中，記下每個註解或音訊檔案的狀態。

| 註解或音訊曲目狀態 | 說明 |
| --- | --- |
| 處理中 | 新增並儲存新的註解或音訊曲目檔案時，檔案會進入「正在處理」狀態。 Dynamic Media會將串流資訊清單附加至主要視訊，以處理檔案。 |
| 已處理 | 處理完成後，註解或音訊曲目檔案，或與主要視訊相關的原始音訊曲目會以「已處理」狀態出現。 您可以預覽標題和音訊曲目檔案，這些檔案在您發佈視訊上線&#x200B;*之前*&#x200B;顯示為「已處理」。 |
| 已發佈 | 「已發佈」狀態代表與主要視訊「已發佈」類似的狀態。 Assets會在主要影片發佈時發佈，並可在公開Dynamic Media URL上使用。 |
| 已失敗 | 「失敗」狀態表示字幕或音訊曲目檔案的處理未完成。 請刪除註解或音訊曲目檔案，然後重新上傳。 |
| 已取消發佈 | 明確取消發佈已發佈的主要視訊時，您新增至視訊的任何註解或音訊追蹤檔案也會取消發佈。 |

![標題和音訊曲目欄位中反白顯示的狀態列。](/help/assets/dynamic-media/assets/msma-lifecycle-status2.png)*每個已上傳的註解和音訊曲目檔案的生命週期狀態。*

### 為具有多個音軌的視訊設定預設音訊

依預設，視訊的原始音訊會設定為要播放的預設音訊。

不過，任何上傳的音訊曲目檔案都可以設定為預設音訊，以便在視訊載入檢視器後播放。 在「屬性」使用者介面的&#x200B;**註解和音軌**&#x200B;標籤下方，`Default`標籤會套用至音軌檔案的右側，以播放視訊。

>[!NOTE]
>
>預設音訊的播放也取決於下列瀏覽器中的設定：
>
>* Chrome — 播放視訊中設定的預設音訊。
>* Safari — 如果在Safari中設定了預設語言，則會以設定的預設語言播放音訊（如果視訊資訊清單中有的話）。 否則，會播放設定為視訊屬性一部分的預設音訊。

**若要為具有多個音軌的視訊設定預設音訊：**

1. 導覽至您要設定其預設音訊曲目的視訊資產。
1. 在資產選取模式中，從「清單檢視」或「卡片檢視」中選取視訊資產。
1. 在工具列上，選取「屬性」圖示（內有「i」的圓形）。
1. 在[內容]頁面上，選取&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤。
1. 在&#x200B;**音軌**&#x200B;標題下，選取您要設定為視訊預設的音軌檔案。
1. 選取&#x200B;**[!UICONTROL 設定為預設值]**。
在**設定為預設值**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 取代]**。

   ![音訊曲目標題具有選取的音訊曲目檔案名稱，並反白顯示[設定為預設]按鈕。](/help/assets/dynamic-media/assets/msma-defaultaudiotrack2.png)*正在設定視訊的預設音軌。*

1. 在右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。
1. Publish影片。 檢視[Publish資產](publishing-dynamicmedia-assets.md)。

### 預覽含有多個字幕和音訊曲目的視訊{#preview-video-audio-subtitle}

將註解檔案和音訊曲目檔案上傳到視訊並進行處理後，您可以使用Dynamic Media視訊檢視器來預覽所有不同的曲目。 這麼做可協助您檢視客戶所看到的視訊外觀和聲音，並確保影片如預期般運作。

若您對視訊感到滿意，可以使用下列任一方法[發佈](publishing-dynamicmedia-assets.md)。

請參閱[將視訊或影像檢視器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。
檢視[將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
請參閱[將Dynamic Media Assets新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

>[!NOTE]
>
>預設的Experience Manager預覽索引標籤不會顯示多個標題和音訊曲目。 原因是這些曲目與Dynamic Media相關聯，而且只能使用Dynamic Media檢視器預覽來檢視。

**若要預覽含有多個字幕和音軌的視訊：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您已新增多個字幕和音軌的現有視訊。
1. 按一下視訊資產，以便您可以在預覽模式中將其開啟。
1. 在預覽頁面，在頁面的左上角附近，選取下拉式清單，然後選取&#x200B;**[!UICONTROL 檢視器]**。

   顯示[檢視器]選項的![下拉式清單。](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. 從「檢視器」清單中，選取您要用於視訊預覽的檢視器。 例如，下列熒幕擷圖顯示正在選取&#x200B;**[!UICONTROL 視訊]**&#x200B;檢視器。

   ![從[檢視器]下拉式清單選取視訊檢視器。](/help/assets/dynamic-media/assets/msma-dmviewerselected.png)

1. 在右下角附近，在音量圖示的左側，選取語音泡泡圖示，然後選取您要聽到的音訊或註解，或視見或兩者皆選。 如有需要，您可以在[註解]下選取&#x200B;**[!UICONTROL 關閉]**&#x200B;不顯示任何註解或註解。

   ![視訊檢視器中的音訊和註解快顯清單。](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*模擬使用者選取視訊播放的音訊和標題。*

1. 若要開始播放，請選取視訊的&#x200B;**[!UICONTROL 播放]**按鈕。
記下左下角的**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL Embed]**&#x200B;按鈕。 使用這些按鈕分別將視訊的URL[連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)或[將視訊內嵌至網頁](/help/assets/dynamic-media/embed-code.md)。
1. 在預覽頁面的右上角附近，選取&#x200B;**[!UICONTROL 關閉]**。

### 從視訊中刪除註解或音訊曲目檔案

您可以從視訊中刪除註解或音訊曲目檔案。 刪除已發佈的標題或音訊曲目檔案會自動反映在視訊的已發佈URL中。

無法刪除從主要視訊擷取的原始音軌。

**若要刪除視訊的標題或音訊曲目檔案：**

1. 導覽至您要設定其預設音訊曲目的視訊資產。
1. 在資產選取模式中，從「清單檢視」或「卡片檢視」中選取視訊資產。
1. 在工具列上，選取「屬性」圖示（內有「i」的圓形）。
1. 在[內容]頁面上，選取&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤。
1. 執行下列任一項作業：

   * 註解 — 在&#x200B;**註解**&#x200B;標題下，選取一或多個要從視訊中刪除的註解檔案，然後選取&#x200B;**[!UICONTROL 刪除]**。
   * 音訊曲目 — 在&#x200B;**音訊曲目**&#x200B;標題下，選取您要從視訊中刪除的一或多個音訊曲目檔案，然後選取&#x200B;**[!UICONTROL 刪除]**。

1. 在[刪除]對話方塊中，選取[確定]。****
1. Publish影片。

### 下載已上傳至視訊的註解或音訊曲目檔案

您可以下載一或多個您上傳以用於視訊的註解或音訊追蹤檔案。 您可以選擇以.zip格式下載所有選取的檔案，或為每個檔案建立個別的下載資料夾。

無法下載從主要檔案擷取的原始音軌。

**若要從視訊下載註解或音訊曲目檔案：**

1. 導覽至您要設定其預設音訊曲目的視訊資產。
1. 在資產選取模式中，從「清單檢視」或「卡片檢視」中選取視訊資產。
1. 在工具列上，選取「屬性」圖示（內有「i」的圓形）。
1. 在[內容]頁面上，選取&#x200B;**[!UICONTROL 註解與音軌]**&#x200B;標籤。
1. 執行下列任一項作業：

   * 註解 — 在&#x200B;**註解**&#x200B;標題下，選取您要從視訊下載的一或多個註解檔案，然後選取&#x200B;**[!UICONTROL 下載]**。
   * 音訊曲目 — 在&#x200B;**音訊曲目**&#x200B;標題下，選取您要從視訊下載的一或多個音訊曲目檔案，然後選取&#x200B;**[!UICONTROL 下載]**。

1. 在「下載」對話方塊中，設定下列選項：

   | 選項 | 說明 |
   |--- |--- |
   | 另存新檔 | 使用「另存新檔」文字欄位中指定的預設檔案名稱，或指定您自己的名稱。 |
   | 為每個資產建立個別的資料夾 | 為您選取要下載的每個註解檔或音訊追蹤檔建立一個資料夾。 |
   | 電子郵件 | 使用您的預設電子郵件程式，將.zip檔案傳送至指定的電子郵件地址。 |
   | Assets | 指定正在下載的檔案數以及所有選取檔案的組合總大小。 取消選取此選項會使&#x200B;**[!UICONTROL 下載]**&#x200B;按鈕變暗（關閉），使您無法下載任何檔案。 |
1. 選取&#x200B;**[!UICONTROL 下載]**。
1. Publish影片。 檢視[Publish資產](publishing-dynamicmedia-assets.md)。




## 新增隱藏式字幕至視訊 {#adding-captions-to-video}

>[!IMPORTANT]
>
>Adobe建議您在您的Dynamic Media帳戶上[啟用多重註解和音訊追蹤功能](#enable-dash)。 如此一來，您便可運用最新的Dynamic Media後端架構和簡化的工作流程，在視訊中新增註解、字幕和音訊曲目。

您可以將隱藏式字幕新增至單一視訊或最適化視訊集，以將視訊觸及全球市場。 透過新增隱藏式字幕，您就不需要對音訊進行配音，或是使用母語者重新錄製每種語言的音訊。 視訊會以錄製的語言播放。 出現外語註解時，不同語言的人仍可瞭解音訊部分。

隱藏式字幕還能讓耳聾或聽力缺佳的人有更出色的協助工具。

>[!NOTE]
>
>您使用的視訊播放器必須支援隱藏式字幕的顯示。

另請參閱[Dynamic Media中的協助工具](/help/assets/dynamic-media/accessibility-dm.md)。

Dynamic Media可以將註解檔案轉換為JSON (JavaScript物件標籤法)格式。 此轉換表示您可以將JSON文字內嵌至網頁，做為影片隱藏但完整的文字記錄。 搜尋引擎接著可以編目/索引內容，讓影片更容易找到，並為客戶提供更多有關影片內容的詳細資料。

如需在URL中使用JSON函式的詳細資訊，請參閱[提供靜態（非影像）內容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api)。

**若要新增註解至視訊：**

1. 使用協力廠商應用程式或服務來建立您的視訊註解檔案。

   確認您建立的檔案符合WebVTT （網頁視訊文字追蹤）標準。 字幕副檔名為.VTT。 您可以進一步瞭解WebVTT字幕標準。

   請參閱[WebVTT：網頁視訊文字追蹤格式](https://w3c.github.io/webvtt/)。

   有許多網站提供免費和優質的工具與服務，讓您在Dynamic Media外部用來製作WebVTT插圖示題檔案。<!-- THE FOLLOWING LINK IS NO LONGER LIVE. CHECKED DECEMBER 13, 2023 For example, to create a simple video caption file with no styling, you can use the following free online caption authoring and editing tool: -->

   <!-- [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   For best results, use the tool in Internet Explorer 9 or above, Google Chrome, or Safari.

   In the tool, in the **[!UICONTROL Enter URL of video file]** field, paste the copied URL of your video file and then select **[!UICONTROL Load]**. See [Obtain a URL for an Asset](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) to get the URL to the video file itself which you can then paste into the **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome, or Safari can then natively play back the video.-->

依照網站上的熒幕指示製作及儲存您的WebVTT檔案。 完成後，複製註解檔案內容並貼到純文字編輯器中，以VTT副檔名儲存。

>[!NOTE]
>
>為了在全球支援多種語言的視訊標題，WebVTT標準要求您建立個別的.vtt檔案，並針對您想要支援的每種語言呼叫。

一般來說，您會想要將註解VTT檔案的名稱與視訊檔案的名稱相同，並附加語言地區設定，例如 — EN、-FR或 — DE。 如此一來，即可協助您使用現有的網頁內容管理系統，自動化視訊URL的產生作業。

1. 在Experience Manager中，將您的WebVTT標題檔案上傳至DAM。
1. 導覽至&#x200B;*已發佈*&#x200B;視訊資產，您要將其與您上傳的註解檔案建立關聯。

   請記住，URL僅可在您首次發 *布資產* 後 *複製* 。

   檢視[Publish資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. 執行下列任一項作業：

   * 若要取得快顯視訊檢視器體驗，請選取&#x200B;**[!UICONTROL URL]**。 在URL對話方塊中，選取URL並複製到剪貼簿，然後將URL通過簡單文字編輯器。 請使用下列語法附加複製的視訊URL：

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     記下註解路徑結尾的`,1`。 路徑中的VTT副檔名後面緊接著可以選擇性啟用（開啟）或停用（關閉）視訊播放器列上的隱藏式字幕按鈕，方法是分別設定為`,1`或`,0`。

   * 若要內嵌視訊檢視器體驗，請選取&#x200B;**[!UICONTROL 內嵌程式碼]**。 在「內嵌程式碼」對話方塊中，選取「 」，並將內嵌程式碼複製到剪貼簿，然後將程式碼貼到簡單的文字編輯器中。 請使用下列語法附加複製的內嵌程式碼：

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     記下註解路徑結尾的`,1`。 路徑中的VTT副檔名後面緊接著可以選擇性啟用（開啟）或停用（關閉）視訊播放器列上的隱藏式字幕按鈕，方法是分別設定為`,1`或`,0`。

## 將章節標籤新增至視訊 {#adding-chapter-markers-to-video}

您可以新增章節標籤至單一視訊或自我調整視訊集，讓長格式視訊更易於觀看和導覽。 當使用者播放視訊時，他們可以在視訊時間軸上選取章節標籤（也稱為視訊筆畫壓感）。 他們可以輕鬆導覽至興趣點，或立即跳至新內容、培訓和示範。

>[!NOTE]
>
>使用的視訊播放器必須支援使用章節標籤。 Dynamic Media影片播放器不支援章節標籤，但使用協力廠商影片播放器可能不支援。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您可以使用與建立註解相同的方式來建立視訊的章節清單。 也就是說，您會建立WebVTT檔案。 但請注意，此檔案必須與任何WebVTT標題檔案分開。 您無法將字幕和章節合併到一個WebVTT檔案中。

您可以使用以下範例作為建立具有章節導覽的WebVTT檔案所使用的格式範例：

### 含有視訊章節導覽的WebVTT檔案 {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

在上述範例中，`Chapter 1`是提示識別碼，而且是選擇性的。 `00:00:000 --> 01:04:364`的提示時間指定章節的開始時間和結束時間，格式為`00:00:000`。 最後三位數為毫秒，可保留為`000` （若偏好設定）。 `The bicycle store behind it all`的章節標題是章節內容的實際描述。 當使用者將滑鼠指標停留在時間軸中的視覺提示點上時，提示識別碼、開始提示時間和章節標題都會顯示在視訊播放器的快顯視窗中。

由於您使用HTML5視訊檢視器，請確定您建立的章節檔案遵循WebVTT （Web視訊文字追蹤）標準。 章節副檔名為.VTT。 您可以進一步瞭解WebVTT字幕標準。

請參閱[WebVTT：網頁視訊文字追蹤格式](https://w3c.github.io/webvtt/)。

**若要將章節標籤新增至視訊：**

1. 請以UTF8編碼儲存VTT檔案，以避免章節標題文字中的字元轉譯發生問題。

   通常，您會想要將章節VTT檔案命名為與視訊檔案相同的名稱，並附加章節。 如此一來，即可協助您使用現有的網頁內容管理系統，自動化視訊URL的產生作業。
1. 在Experience Manager中，上傳您的WebVTT章節檔案。

   請參閱[上傳資產](/help/assets/manage-digital-assets.md#uploading-assets)。

1. 執行下列任一項作業：

   <table>
     <tbody>
      <tr>
       <td>適用於快顯視訊檢視器體驗</td>
       <td>
       <ol>
       <li>導覽至<i>已發佈的</i>視訊資產，您要將其與您上傳的章節檔案建立關聯。 請記住，URL僅可在您首次發 <i>布資產</i> 後 <i>複製</i> 。請參閱<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">發佈Assets。</a></li>
       <li>從下拉式功能表中，選取<strong>檢視器</strong>。</li>
       <li>在左側欄中，選取視訊檢視器預設集名稱。 視訊的預覽會在另一個頁面中開啟。</li>
       <li>在左側邊欄的底部，選取<strong>URL</strong>。</li>
       <li>在URL對話方塊中，選取URL並複製到剪貼簿，然後將URL通過簡單文字編輯器。</li>
       <li>使用下列語法附加複製的視訊URL，以便將其與複製的URL關聯至您的章節檔案： <br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>針對內嵌視訊檢視器體驗<br /> </td>
       <td>
       <ol>
       <li>導覽至<i>已發佈的</i>視訊資產，您要將其與您上傳的章節檔案建立關聯。 請記住，URL僅可在您首次發 <i>布資產</i> 後 <i>複製</i> 。請參閱<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">發佈Assets。</a></li>
       <li>從下拉式功能表中，選取<strong>檢視器</strong>。</li>
       <li>在左側欄中，選取視訊檢視器預設集名稱。 視訊的預覽會在另一個頁面中開啟。</li>
       <li>在左側邊欄的底部，選取<strong>內嵌</strong>。</li>
       <li>在「內嵌程式碼」對話方塊中，選取「 」，並將整個程式碼複製到剪貼簿，然後貼到簡單的文字編輯器中。</li>
       <li>使用下列語法附加視訊的內嵌程式碼，以便將其與複製的URL關聯至您的章節檔案：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>



## 關於視訊縮圖 {#about-video-thumbnails}

視訊縮圖是視訊影格的縮小版本，或是向客戶表示視訊的影像資產。 縮圖應該用於鼓勵客戶選擇影片。

Experience Manager中的所有視訊都必須有關聯的縮圖；您必須取代縮圖才能刪除縮圖。 根據預設，上傳視訊至Experience Manager時，會使用第一個影格作為縮圖。 不過，您可以自訂縮圖，以利品牌化或視覺化搜尋，例如。 自訂視訊縮圖時，您可以播放視訊並在要使用的影格上暫停。 或者，您可以選取已在數位資產管理器中上傳並&#x200B;*發佈*&#x200B;的影像資產。

當視訊的縮圖變更時，會略過重新處理視訊時透過Asset Compute服務產生縮圖。

只有在您將視訊設定檔套用至視訊所在的資料夾後，才能使用自訂視訊縮圖的功能。

### 新增自訂視訊縮圖 {#adding-a-custom-video-thumbnail}

1. 請確定您已完成下列操作：

   * 已建立視訊資產的資料夾。
   * [已將視訊設定檔套用至資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   * [已將視訊上傳至資料夾](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。

1. 導覽至您要變更其縮圖影像的上傳視訊資產。
1. 在資產選擇模式中，從&#x200B;**[!UICONTROL 清單檢視]**&#x200B;或&#x200B;**[!UICONTROL 卡片檢視]**，選取視訊資產。
1. 在工具列上，選取&#x200B;**[!UICONTROL 屬性]**&#x200B;圖示（內有「i」的圓形）。
1. 在視訊的「屬性」頁面上，選取&#x200B;**[!UICONTROL 變更縮圖]**。
1. 在「變更縮圖」頁面上，執行下列任一項作業：

   * 若要使用視訊中的影格做為新的縮圖：

      * 在工具列上，選取&#x200B;**[!UICONTROL 從視訊選取影格]**。
      * 選取「播放」按鈕，然後在您要擷取的影格上選取「暫停」按鈕，作為視訊的新縮圖。

   * 若要將影像資產作為新縮圖：

      * 在工具列上，選取&#x200B;**[!UICONTROL 從Assets中選取縮圖]**。
      * 選取&#x200B;**[!UICONTROL 選取縮圖]**。
      * 導覽至您想要使用的先前上傳和發佈影像資產。 資產會自動調整大小，以作為視訊的縮圖影像。
      * 選取影像資產，然後選取&#x200B;**[!UICONTROL 選取]**。

1. 在[變更縮圖]頁面上，選取[**[!UICONTROL 儲存變更]**]。
1. 在影片的「屬性」頁面右上角，選取「**[!UICONTROL 儲存並關閉]**」。



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## 變更Dynamic Media資產的Dynamic Media URL

在Dynamic Media中處理的視訊，可以透過開箱即用的檢視器使用，也可以直接存取資訊清單URL並透過您自己的自訂檢視器播放。 以下是為影片擷取資訊清單URL的API。

### 關於getVideoManifestURI API

`getVideoManifestURI`API透過c`q-scene7-api:com.day.cq.dam.scene7.api`公開，可用來產生下列資訊清單URL：

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API引數

此API會採用下列三個引數：

| 參數 | 說明 |
| --- | --- |
| `resource` | 與Dynamic Media已擷取的視訊對應的資源。 |
| `manifestType` | 可以是`ManifestType.DASH`或`ManifestType.HLS` |
| `onlyIfPublished` | 如果資訊清單URI只有在發佈後才能在傳遞層級上使用，則設為true。 |

若要使用上述方法擷取視訊的資訊清單URL，請將[視訊編碼設定檔](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)新增至「上傳視訊」資料夾。 Dynamic Media會根據指派給資料夾之視訊編碼檔案中的編碼，來處理這些視訊。 現在您可以叫用上述API，以擷取已上傳視訊的資訊清單URL。

### 錯誤案例

如果發生錯誤，API會傳回null。 例外狀況會記錄在Experience Manager錯誤記錄檔中。 所有這類記錄錯誤都以`Could not generate Video Manifest URI`開頭。 下列情況可能會導致此類錯誤：

* `IllegalArgumentException`會針對下列任一專案進行記錄：

   * 傳遞的`resource`引數為Null。
   * 傳遞的`resource`引數不是視訊。
   * 傳遞的`manifestType`引數為Null。
   * `onlyIfPublished`引數傳遞為true，但視訊未發佈。
   * 未使用Dynamic Media中的自我調整視訊集擷取視訊。

* 在連線到Dynamic Media時發生問題時，`IOException`會獲得記錄。
* 當傳遞的`manifestType`引數為`ManifestType.DASH`且未使用DASH格式處理視訊時，會記錄`UnsupportedOperationException`。

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->





