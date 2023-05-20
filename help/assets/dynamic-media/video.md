---
title: Dynamic Media 中的視訊
description: 瞭解如何在Dynamic Media使用視頻。 查看對視頻進行編碼、向YouTube發佈視頻、查看視頻報告以及向視頻添加隱藏字幕、字幕或章節標籤的最佳做法。
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 124b363fe341199fdc9b25d25bbf2a9bc8f87d87
workflow-type: tm+mt
source-wordcount: '5868'
ht-degree: 2%

---

# 影片 {#video}

本節介紹在Dynamic Media使用視頻。

## 快速啟動：視頻 {#quick-start-videos}

下面的逐步工作流描述旨在幫助您快速啟動並運行Dynamic Media的自適應視頻集。 在每個步驟之後，都會交叉引用主題標題，您可以在其中查找詳細資訊。

>[!NOTE]
>
>在Dynamic Media處理視頻之前，請確保您的Adobe Experience Manager管理員已啟用並配置了Dynamic MediaCloud Services。
>
>* 請參閱 [配置Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) 配置Dynamic Media和 [排除Dynamic Media故障](/help/assets/dynamic-media/troubleshoot-dm.md)。
>


1. **上傳你的Dynamic Media視頻** 執行以下操作：

   * 建立您自己的視頻編碼配置檔案。 或者，您只需使用預定義的 _自適應視頻編碼_ Dynamic Media的檔案。

      * [建立視頻編碼配置檔案](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 瞭解有關 [視頻編碼的最佳做法](#best-practices-for-encoding-videos)。
   * 將視頻處理配置檔案關聯到一個或多個資料夾，以上載主源視頻。

      * [將視頻配置檔案應用於資料夾](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
      * 瞭解有關 [組織數字資產](/help/assets/organize-assets.md)。
   * 將主源視頻上載到資料夾。 將視頻添加到資料夾時，會根據分配給資料夾的視頻處理配置檔案對它們進行編碼。

      * Dynamic Media主要支援長度最長為30分鐘、解析度最低大於25 x 25的短格式視頻。
      * 您可以上傳每個高達15 GB的視頻檔案。
      * [上傳視頻](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
      * 瞭解有關 [支援的輸入檔案格式](/help/assets/file-format-support.md)。
   * 監視方式 [視頻編碼正在進行](#monitoring-video-encoding-and-youtube-publishing-progress) 從資產或工作流視圖。




1. **管理您的Dynamic Media視頻** 執行下列任一操作：

   * 組織、瀏覽和搜索視頻資產

      * [組織數字資產](/help/assets/organize-assets.md)
      * [搜索視頻資產](/help/assets/search-assets.md#custompredicates) 或 [搜索資產](/help/assets/manage-digital-assets.md#search-assets)
   * 預覽和發佈視頻資產

      * 查看視頻的源視頻和編碼格式副本及其關聯的縮略圖：
         [預覽視頻](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) 或 [預覽資產](/help/assets/dynamic-media/previewing-assets.md)
         [管理視頻格式副本](/help/assets/manage-digital-assets.md#managing-renditions)

      * [管理查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * 使用視頻元資料

      * 編輯視頻的屬性，如標題、說明和標籤、自定義元資料欄位：
         [編輯視頻屬性](/help/assets/manage-digital-assets.md#editing-properties)

      * [管理數字資產的元資料](/help/assets/manage-metadata.md)
      * [中繼資料結構描述](/help/assets/metadata-schemas.md)
   * 查看、批准和注釋視頻，並維護完整的版本控制

      * [注釋視頻](/help/assets/manage-video-assets.md#annotate-video-assets) 或 [注釋資產](/help/assets/manage-digital-assets.md#annotating)

      * [建立版本](/help/assets/manage-digital-assets.md#asset-versioning)
      * [啟動資產的工作流](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [審閱資料夾資產](/help/assets/bulk-approval.md)
      * [專案](/help/sites-cloud/authoring/projects/overview.md)




1. **發佈你的Dynamic Media視頻** 執行下列操作之一：

   * 如果將Experience Manager用作WCM（Web內容管理）系統，則可以直接將視頻添加到網頁。

      * [將視頻添加到網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
   * 如果您使用第三方Web內容管理系統，則可以將視頻連結或嵌入到您的網頁。

      * 使用URL整合視頻：
         [將 URL 連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * 使用網頁上的嵌入代碼整合視頻：
         [將視頻查看器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。
   * [生成視頻報告](#viewing-video-reports)。

   * [將字幕添加到視頻](#adding-captions-to-video)。



## 在Dynamic Media使用視頻 {#working-with-video-in-dynamic-media}

Dynamic Media的視頻是一種端到端解決方案，它使發佈高質量自適應視頻在多個螢幕（包括台式機、平板電腦和移動設備）上流動變得輕鬆。 自適應視頻集將以不同比特率和格式（如400 kbps、800 kbps和1000 kbps）編碼的同一視頻的版本分組。 台式電腦或移動設備檢測可用頻寬。

例如，在iOS移動設備上，它檢測3G、4G或Wi-Fi等頻寬。 然後，自動從自適應視頻集內的各種視頻比特率中選擇正確編碼的視頻。 視頻被流式傳輸到台式機、移動設備或平板電腦。

此外，如果案頭或移動設備上的網路狀況發生變化，則自動切換視頻質量。 此外，如果客戶在案頭上進入全屏模式，自適應視頻集會通過使用更好的解析度來響應，從而改善客戶的觀看體驗。 使用自適應視頻集為客戶在多個螢幕和設備上播放Dynamic Media視頻提供了最佳的可回放。

視頻播放器用於確定在回放期間播放或選擇哪些編碼視頻的邏輯基於以下算法：

1. 視頻播放器基於與在播放器本身中為「初始比特率」設定的值最接近的比特率來載入初始視頻片段。
1. 視頻播放器根據頻寬速度的更改使用以下標準進行切換：

   1. 播放器選擇低於或等於估計頻寬的最高頻寬流。
   1. 玩家只考慮80%的可用頻寬。 但是，如果換了，就比較保守，只有70%，避免高估，立即換回。

有關算法的詳細技術資訊，請參見 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

對於管理單個視頻和自適應視頻集，支援以下操作：

* 從多種支援的視頻格式和音頻格式上傳視頻，並將視頻編碼為MP4 H.264格式，以便在多個螢幕上播放。 可以使用預定義的自適應視頻預設、單個視頻編碼預設或自定義自己的編碼來控制視頻的質量和大小。

   * 當生成自適應視頻集時，它包括MP4視頻。
   * **注釋**:主/源視頻未添加到自適應視頻集。

* 所有HTML5個視頻查看器中的視頻字幕。
* 利用完整的元資料支援組織、瀏覽和搜索視頻，以有效管理視頻資產。
* 向Web和台式機、平板電腦和移動設備提供自適應視頻集。

各種iOS平台支援自適應視頻流。 請參閱 [Dynamic Media觀眾參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html)。

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 使用Dynamic Media視頻查看器預設回放視頻，包括：

   * 單個視頻觀看器。
   * 將視頻和影像內容組合在一起的混合媒體查看器。

* 配置視頻播放器以滿足您的品牌推廣需求。
* 將視頻與您的網站、移動站點或移動應用程式整合，並使用簡單的URL或嵌入代碼。

請參閱 [動態視頻播放](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) 樣式。

另請參閱 [Experience Manager Assets和Dynamic Media Classic觀眾](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [僅Experience Manager Assets觀眾](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 的 [Dynamic Media觀眾參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)。

## 最佳做法：使用HTML5視頻查看器 {#best-practice-using-the-html-video-viewer}

Dynamic MediaHTML5視頻查看器預設是強大的視頻播放器。 您可以使用它們來避免許多與HTML5視頻播放相關的常見問題和與移動設備相關的問題。 例如，缺少自適應比特率流傳輸和案頭瀏覽器訪問限制。

在播放器的設計端，您可以使用標準Web開發工具設計視頻播放器的功能。 例如，您可以使用HTML5和CSS設計按鈕、控制項和自定義海報影像背景，以幫助您以自定義外觀接觸客戶。

在查看器的播放端，它自動檢測瀏覽器的視頻功能。 然後，它使用HLS或DASH（也稱自適應視頻流）為視頻服務。 或者，如果這些傳遞方法不存在，則改用HTML5累進。

>[!NOTE]
>
>要將DASH用於視頻，必須先通過帳戶上的Adobe技術支援來啟用它。 請參閱 [啟用帳戶上的DASH](#enable-dash)。

可以將使用HTML5和CSS設計回放元件的功能組合到單個播放器中。 它可以有嵌入式回放，並根據瀏覽器的功能使用自適應和漸進式流。 所有這些功能都意味著您可以將您的富媒體內容擴展到案頭用戶和移動用戶，並確保簡化的視頻體驗。

另請參閱 [僅Experience Manager Assets觀眾](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) 的 [Dynamic Media觀眾參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)。


### 使用HTML5視頻查看器在台式電腦和移動設備上回放視頻 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

對於案頭和移動自適應視頻流，用於比特率切換的視頻基於自適應視頻集中的所有MP4視頻。

使用HLS或DASH或漸進式視頻下載進行視頻回放。 在以前的Experience Manager版本中，如6.0、6.1和6.2，視頻通過HTTP流式傳輸。

但是，在Experience Manager6.3和ON中，視頻現在通過HTTPS（即HLS或DASH）流式傳輸，因為DM網關服務URL也始終使用HTTPS。 此預設行為不會對客戶產生影響。 即，除非瀏覽器不支援HTTPS，否則視頻流始終會通過HTTPS進行。 （見下表）。

所以，

* 如果您有一個HTTPS網站，其中包含HTTPS視頻流，則流處理是正常的。
* 如果HTTP網站具有HTTPS視頻流，則流處理是正常的，並且Web瀏覽器中不存在混合內容問題。

DASH是國際標準，HLS是Apple標準。 兩者都用於自適應視頻流。 而且，這兩種技術都可根據網路頻寬容量自動調整回放。 它還讓客戶可以「查找」到視頻中的任何點，而無需等待視頻的其餘部分下載。

通過在用戶的案頭系統或移動設備上本地下載和儲存視頻來傳送漸進視頻。

下表介紹了在台式電腦和移動設備上使用 [Dynamic MediaHTML5視頻查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video)。

<table>
 <tbody>
  <tr>
   <td><strong>裝置</strong></td>
   <td><strong>瀏覽器</strong></td>
   <td><strong>視頻播放模式</strong></td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 9和10</td>
   <td>逐步下載。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows® 8和Windows® 10上 — 只要請求DASH或HLS，就強制使用HTTPS。 已知限制：DASH或HLS上的HTTP在此瀏覽器/作業系統組合中不工作<br /> <br /> 在Windows® 7上 — 漸進式下載。 使用標準邏輯選擇HTTP與HTTPS協定。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>火狐23-44</td>
   <td>逐步下載。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 45或更高版本</td>
   <td>HLS或DASH*自適應比特率流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>鉻</td>
   <td>HLS或DASH*自適應比特率流</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>薩法里(Mac)</td>
   <td>HLS自適應比特率流</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Chrome（Android™ 6或更早版本）</td>
   <td>逐步下載。</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>Chrome（Android™ 7或更高版本）</td>
   <td>HLS或DASH*自適應比特率流/td&gt;
  </tr>
  <tr>
   <td>行動</td>
   <td>Android™（預設瀏覽器）</td>
   <td>逐步下載。</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>薩法里(iOS)</td>
   <td>HLS自適應比特率流</td>
  </tr>
  <tr>
   <td>行動</td>
   <td>克羅姆語(iOS)</td>
   <td>HLS自適應比特率流</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*要將DASH用於視頻，必須先通過帳戶上的Adobe技術支援來啟用它。 請參閱 [啟用帳戶上的DASH](#enable-dash)。)

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media視頻解決方案的體系結構 {#architecture-of-dynamic-media-video-solution}

下圖顯示了通過DMGateway(在Dynamic Media混合模式下)上傳和編碼並供公眾使用的視頻的總體創作工作流程。

![chlimage_1-427](assets/chlimage_1-427.png)

## 用於視頻的混合發佈體系結構 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 編碼視頻的最佳做法 {#best-practices-for-encoding-videos}

的 **Dynamic Media編碼視頻** 如果啟用了Dynamic Media並設定視頻Cloud Services，則工作流會對視頻進行編碼。 此工作流程會擷取工作流程處理歷程記錄和失敗資訊。如果您啟用了Dynamic Media並設定視頻Cloud Services, **[!UICONTROL Dynamic Media編碼視頻]** 當您上載視頻時，工作流將自動生效。 (如果你不用Dynamic Media, **[!UICONTROL DAM更新資產]** 工作流生效。)

以下是對源視頻檔案進行編碼的最佳做法提示。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### 源視頻檔案 {#source-video-files}

對視頻檔案進行編碼時，請使用盡可能高質量的源視頻檔案。 避免使用以前編碼的視頻檔案，因為這些檔案已經壓縮，而進一步編碼會造成質量欠佳的視頻。

* Dynamic Media主要支援長度最長為30分鐘、解析度最低大於25 x 25的短格式視頻。
* 您可以上載每個高達15 GB的主源視頻檔案。

下表介紹了在對源視頻檔案進行編碼之前必須具有的建議大小、長寬比和最小比特率：

| 大小 | 外觀比例 | 最小比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps，用於大多數視頻。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具體取決於視頻中的運動量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具體取決於視頻中的運動量。 |

### 獲取檔案的元資料 {#obtaining-a-file-s-metadata}

您可以通過使用視頻編輯工具查看檔案的元資料或使用旨在獲取元資料的應用程式來獲取檔案的元資料。 以下是使用第三方應用程式MediaInfo獲取視頻檔案元資料的說明：

1. 轉到 [MediaInfo下載](https://mediaarea.net/en/MediaInfo/Download)。
1. 選擇並下載GUI版本的安裝程式，並按照安裝說明進行操作。
1. 安裝後，按一下右鍵視頻檔案（僅限Windows®）並選擇「MediaInfo」，或開啟MediaInfo並將視頻檔案拖到應用程式中。 您可以看到與視頻檔案關聯的所有元資料，包括其寬度、高度和fps。

### 外觀比例 {#aspect-ratio}

選擇或為主源視頻檔案建立視頻編碼預設時，請確保預設具有與主源視頻檔案相同的長寬比。 縱橫比是視頻寬度與高度的比值。

要確定視頻檔案的長寬比，請獲取檔案的元資料並記錄檔案的寬度和高度（請參閱上面的獲取檔案的元資料）。 然後使用此公式確定縱橫比：

寬高=寬高比

下表說明公式結果如何轉換為通用縱橫比選擇：

| 公式結果 | 外觀比例 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，寬度為1440 x 1080的視頻的寬高比為1440/1080或1.33。在這種情況下，您選擇具有4:3長寬比的視頻編碼預設來編碼視頻檔案。

### 位元速率 {#bitrate}

比特率是編碼的資料量，它構成視頻回放的一秒鐘。 比特率以千位每秒(Kbps)為單位。

>[!NOTE]
>
>由於所有編解碼器都使用有損壓縮，因此比特率是視頻質量中最重要的因素。 在有損壓縮中，對視頻檔案的壓縮越多，質量就越降低。 因此，所有其它特性（解析度、幀速率和編解碼器）相等，比特率越低，壓縮檔案的質量越低。

選擇比特率編碼時，可以選擇兩種類型：

* **[!UICONTROL 恆定比特率編碼]** (CBR) — 在CBR編碼期間，比特率或每秒的比特數在整個編碼過程中保持相同。 CBR編碼在整個視頻上將設定的資料速率保留為您的設定。 此外，CBR編碼不會為質量優化媒體檔案，而會節省儲存空間。
如果視頻在整個視頻中包含類似的運動級別，則使用CBR。 CBR是流視頻內容最常用的算法。 另請參閱 [使用自定義添加的視頻編碼參數](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters)。

* **[!UICONTROL 可變比特率編碼]** (VBR)- VBR編碼根據壓縮器所需的資料，將資料速率調低並調整到您設定的上限。 此功能意味著在VBR編碼過程中，媒體檔案的比特率會根據媒體檔案的比特率需求動態地增加或減少。
VBR編碼時間較長，但效果最好；媒體檔案的質量優越。 VBR最常用於視頻內容的http漸進傳送。

您何時使用VBR與CRB?
選擇VBR與CBR時，幾乎總是建議您將VBR用於媒體檔案。 VBR以競爭比特率提供更高質量的檔案。 使用VBR時，請確保使用兩遍編碼，並將最大比特率設定為目標視頻比特率的1.5倍。

選擇視頻編碼預設時，請確保考慮目標最終用戶的連接速度。 選擇資料速率為該速度80%的預設。 例如，如果目標最終用戶的連接速度是1000 Kbps，則最佳預設值是視頻資料速率為800 Kbps。

此表介紹了典型連接速度的資料速率。

| 速度(Kbps) | 連接類型 |
|--- |--- |
| 256 | 撥號連接。 |
| 800 | 典型的移動連接。 對於此連接，針對3G體驗，將資料速率定為400到最大800。 |
| 2000 | 典型寬頻案頭連接。 對於此連接，以800-2000 Kbps範圍內的資料速率為目標，大多數目標的平均速率為1200-1500 Kbps。 |
| 5000 | 典型的高寬頻連接。 建議不要在此上限範圍內進行編碼，因為大多數消費者無法以此速度進行視頻傳輸。 |

### 解析度 {#resolution}

**解決** 描述視頻檔案的高度和寬度（以像素為單位）。 大多數源視頻都以高解析度儲存（例如，1920 x 1080）。 為了流式傳輸，源視頻被壓縮到更小的解析度（640 x 480或更小）。

解析度和資料速率是決定視頻質量的兩個整體聯繫的因素。 要保持相同的視頻質量，視頻檔案中的像素數越多（解析度越高），資料速率就越高。 例如，請考慮320 x 240解析度和640 x 480解析度視頻檔案中每幀的像素數：

| 解析度 | 每幀像素 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480檔案每幀的像素數是原來的四倍。 為了對這兩個示例解析度實現相同的資料速率，對640 x 480檔案應用四倍的壓縮，這會降低視頻質量。 因此，250 Kbps的視頻資料速率可以以320 x 240的解析度而不是以640 x 480的解析度來提供高質量的觀看。

通常，您使用的資料速率越高，視頻顯示越好，解析度越高，您必須保持查看質量的資料速率越高（解析度越低）。

由於解析度和資料速率是連結的，因此在編碼視頻時有兩個選項：

* 選擇資料速率，然後以最高解析度進行編碼，該解析度在您選擇的資料速率上看起來良好。
* 選擇解析度，然後按所需的資料速率進行編碼，以便以您選擇的解析度獲得高質量視頻。

為主源視頻檔案選擇（或建立）視頻編碼預設時，請使用此表以正確的解析度為目標：

| 解析度 | 高度 (像素) | 螢幕大小 |
|--- |--- |--- |
| 240p | 240 | 小螢幕 |
| 300p | 300 | 通常用於移動設備的小螢幕 |
| 360p | 360 | 小螢幕 |
| 480p | 480 | 中屏 |
| 720p | 720 | 大螢幕 |
| 1080p | 1080 | 高清大螢幕 |

### Fps（每秒幀數） {#fps-frames-per-second}

在美國和日本，大多數視頻的拍攝速度是每秒29.97幀(fps);在歐洲，大多數視頻的拍攝速度是25 fps。 影片以24幀/秒的速度拍攝。

選擇與主源視頻檔案的fps速率匹配的視頻編碼預設。 例如，如果主源視頻為25 fps，請選擇一個25 fps的編碼預設。 預設情況下，所有自定義編碼都使用主源視頻檔案的fps。 因此，建立視頻編碼預設時不需要顯式指定fps設定。

### 視頻編碼維度 {#video-encoding-dimensions}

為獲得最佳結果，請選擇編碼尺寸，使源視頻是所有編碼視頻的整倍。

要計算此比率，請將源寬度除以編碼寬度，以獲得寬度比。 然後，將源高度除以編碼高度，得到高度比。

如果得到的比率是整整數，則表示視頻被最優縮放。 如果結果比率不是整數，則它會通過將剩餘像素偽像留在顯示器上而影響視頻質量。 當視頻有文本時，此效果最為明顯。

例如，假設源視頻為1920 x 1080。 在下表中，三個編碼視頻提供了要使用的最佳編碼設定。

| 視頻類型 | 寬x高 | 寬度比例 | 高度比 |
|--- |--- |--- |--- |
| 來源 | 1920x1080 | 1 | 1 |
| 編碼 | 960 x 540 | 2 | 2 |
| 編碼 | 640 x 360 | 3 | 3 |
| 編碼 | 480 x 270 | 4 | 4 |

### 編碼視頻檔案格式 {#encoded-video-file-format}

Dynamic Media建議使用MP4 H.264視頻編碼預設。 由於MP4檔案使用H.264視頻編解碼器，因此它提供高質量的視頻，但檔案大小是壓縮的。

### 啟用帳戶上的DASH {#enable-dash}

DASH(Digital Adaptive Streaming over HTTP)是視頻流的國際標準，在不同的視頻觀看者中被廣泛採用。 在您的帳戶上啟用DASH後，您可以選擇從DASH或HLS中選擇自適應視頻流。 或者，您可以選擇兩者，在 **[!UICONTROL 自動]** 在「查看器」預設中選擇為播放類型。

在您的帳戶上啟用DASH的一些主要好處包括：

* 用於自適應比特率流的包DASH流視頻。 該方法提高了輸送效率。 自適應流式處理可確保您的客戶獲得最佳的觀看體驗。
* 瀏覽器優化了流式傳輸，Dynamic Media播放器在HLS和DASH流之間切換，以確保最佳服務質量。 當使用Safari瀏覽器時，視頻播放器自動切換到HLS。
* 可以通過編輯視頻查看器預設來配置首選流式處理方法（HLS或DASH）。
* 優化的視頻編碼可確保在啟用DASH功能時不使用其他儲存。 為HLS和DASH建立一組視頻編碼以優化視頻儲存成本。
* 幫助讓客戶更容易訪問視頻交付。
* 也通過API獲取流URL。

您啟動使用DASH的請求；不會在您的帳戶上自動啟用它。

要在您的帳戶上啟用DASH，請建立客戶支援案例，如下所述。 在支援案例中，指定要在Dynamic Media帳戶和Experience Manager上啟用DASH。

**要啟用帳戶上的DASH:**

1. [使用Admin Console開始建立新支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 要建立支援案例，請按照說明操作，同時確保提供以下資訊：

   * 主要聯繫人姓名，電子郵件，電話。
   * 你的Dynamic Media帳戶的名稱。
   * 指定希望在Dynamic Media帳戶和Experience Manager上啟用DASH。

1. Adobe客戶支援根據請求提交的順序將您添加到DASH客戶等待清單。
1. 當Adobe準備好處理您的請求時，客戶支援會聯繫您，以協調並設定啟用DASH的目標日期。
1. 完成後，客戶支援會通知您。
1. 建立 [視頻查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) 像往常一樣。

## 查看視頻報告 {#viewing-video-reports}

>[!NOTE]
>
>視頻報告僅在您運行Dynamic Media — 混合模式時可用。

視頻報告在指定的時段內顯示多個聚合度量，以幫助您監視 *出版* 單個視頻和聚合視頻正在按預期執行。 以下頂級度量資料將聚合到整個網站中所有已發佈的視頻：

* 視訊開始
* 完成率
* 視頻上的平均時間
* 視頻總時間
* 每次訪問的視頻

全部表 *出版* 還列出視頻，以便您可以根據總視頻開始時間跟蹤網站上最熱門的已查看視頻。

在清單中選擇視頻名稱時，它將以折線圖的形式顯示視頻的觀眾保留（下拉）報告。 該圖表顯示視頻回放期間任意給定時間刻度的視圖數。 播放視頻時，竪條與播放器中的時間指示器同步跟蹤。 在折線圖資料中出現，表示您的受眾從不感興趣的位置。

如果視頻是在Adobe Experience ManagerDynamic Media之外編碼的，則表中的觀眾保留（下拉）圖和播放百分比資料不可用。

>[!NOTE]
>
>跟蹤和報告資料完全基於使用動態媒體自己的視頻播放器和相關的視頻播放器預設。 因此，您無法跟蹤和報告通過其他視頻播放器播放的視頻。

預設情況下，在您首次輸入視頻報告時，該報告將顯示從當月的第一個開始到當月日期結束的視頻資料。 但是，您可以通過指定自己的日期範圍來覆蓋預設日期範圍。 下次輸入視頻報表時，將使用指定的日期範圍。

為使視頻報告正常工作，在配置Dynamic MediaCloud Services時會自動建立報表套件ID。 同時，將「報告套件ID」推送到「發佈」伺服器，以便在預覽資產時可以使用「複製URL」功能。 但是，此功能要求已設定發佈伺服器。 如果未設定「發佈」伺服器，您仍可以發佈以查看視頻報告。 但是，您必須返回Dynamic Media雲配置並選擇 **[!UICONTROL 確定]**。

**要查看視頻報告：**

1. 在Experience Manager的左上角，選擇Experience Manager徽標，然後在左滑軌中導航至 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 視頻報告]**。
1. 在「視頻報告」頁上，執行下列操作之一：

   * 在右上角處，選擇 **[!UICONTROL 刷新視頻報告]** 表徵圖
僅當報表的結束日期為當前日期時，才使用「刷新」。 此功能可確保您查看自上次運行報告以來發生的視頻跟蹤。

   * 在右上角處，選擇 **[!UICONTROL 日期選取器]** 表徵圖
指定要獲取視頻資料的開始和結束日期範圍，然後選擇 **[!UICONTROL 運行報告]**。

   「頂級度量」組框標識所有的各種聚合度量 *出版* 視頻。

1. 在列出頂級發佈視頻的表中，選擇視頻名稱來播放視頻，並查看視頻的觀眾保留（下拉）報告。

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

## 將隱藏字幕或字幕添加到視頻 {#adding-captions-to-video}

通過將隱藏字幕添加到單個視頻或自適應視頻集，您可以將視頻的觸角擴展到全球市場。 通過添加隱藏字幕，您不必對音頻進行調音，也不必使用母語人士為每種不同的語言重新錄制音頻。 視頻以錄制的語言播放。 外文字幕出現，使不同語言的人仍然能夠理解音頻部分。

閉式字幕還使聾啞或聽力障礙的人更容易獲得。

>[!NOTE]
>
>您使用的視頻播放器必須支援隱藏字幕的顯示。

另請參閱 [Dynamic Media無障礙](/help/assets/dynamic-media/accessibility-dm.md)。

Dynamic Media可以將字幕檔案轉換為JSON（JavaScript對象表示法）格式。 此轉換意味著您可以將JSON文本嵌入到網頁中，作為視頻的隱藏但完整的記錄。 然後，搜索引擎可以對內容進行爬網/索引，以使視頻更容易被發現，並為客戶提供有關視頻內容的更多詳細資訊。

請參閱 [服務靜態（非影像）內容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 的子菜單。

**向視頻添加字幕或字幕：**

1. 使用第三方應用程式或服務建立視頻字幕/副標題檔案。

   確保您建立的檔案遵循WebVTT（Web視頻文本軌道）標準。 字幕檔案名副檔名為.VTT。 您可以瞭解有關WebVTT字幕標準的更多資訊。

   請參閱 [WebVTT:Web視頻字幕資訊格式](https://w3c.github.io/webvtt/)。

   您可以使用免費和高級工具和服務來製作Dynamic Media以外的字幕/字幕檔案。 例如，要建立沒有樣式的簡單視頻標題檔案，可以使用以下免費聯機標題創作和編輯工具：

   [WebVTT字幕製作](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   為獲得最佳結果，請在Internet Explorer 9或更高版本、GoogleChrome或Safari中使用該工具。

   在工具中，在 **[!UICONTROL 輸入視頻檔案的URL]** 欄位，貼上視頻檔案的複製URL，然後選擇 **[!UICONTROL 載入]**。 請參閱 [獲取資產的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 獲取視頻檔案本身的URL，然後可以貼上到 **[!UICONTROL 輸入視頻檔案欄位的URL]**。 然後，Internet Explorer、Chrome或Safari就可以原生播放視訊。

   現在，請按照網站的螢幕說明編寫並保存WebVTT檔案。 完成後，複製標題檔案內容並將其貼上到純文字檔案編輯器中，並使用VTT檔案副檔名將其保存。

   >[!NOTE]
   >
   >為全局支援多語言視頻字幕，WebVTT標準要求您為要支援的每種語言建立單獨的.vtt檔案和調用。

   通常，您希望將標題VTT檔案命名為與視頻檔案同名，並使用語言區域設定（如 — EN、-FR或 — DE）附加它。 通過這樣做，它可以幫助您使用現有的Web內容管理系統自動生成視頻URL。

1. 在Experience Manager中，將WebVTT標題檔案上載到DAM。
1. 導航到 *出版* 要與上載的標題檔案關聯的視頻資產。

   請記住，URL僅可在您首次發 *布資產* 後 *複製* 。

   請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. 執行下列任一項作業：

   * 要獲得彈出式視頻查看器體驗，請選擇 **[!UICONTROL URL]**。 在「URL」對話框中，選擇URL並將其複製到剪貼簿，然後將URL傳到簡單文本編輯器中。 使用以下語法追加視頻的複製URL:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      注意 `,1` 標題路徑的末尾。 緊隨路徑中的VTT檔案副檔名後，您可以選擇啟用（開啟）或禁用（關閉）視頻播放器欄上的隱藏字幕按鈕，方法是將設定為 `,1` 或 `,0`的下界。

   * 對於嵌入式視頻查看器體驗，請選擇 **[!UICONTROL 嵌入代碼]**。 在「嵌入代碼」對話框中，選擇嵌入代碼並將其複製到剪貼簿，然後將代碼貼上到簡單的文本編輯器中。 使用以下語法追加複製的嵌入代碼：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      注意 `,1` 標題路徑的末尾。 緊隨路徑中的VTT檔案副檔名後，您可以選擇啟用（開啟）或禁用（關閉）視頻播放器欄上的隱藏字幕按鈕，方法是將設定為 `,1` 或 `,0`的下界。

## 將章節標籤添加到視頻 {#adding-chapter-markers-to-video}

通過向單個視頻或自適應視頻集添加章節標籤，您可以更輕鬆地觀看和導航長格式視頻。 當用戶播放視頻時，他們可以選擇視頻時間軸上的章節標籤（也稱為視頻掃描器）。 他們可以輕鬆找到自己的興趣點，或立即跳到新內容、培訓和演示中。

>[!NOTE]
>
>使用的視頻播放器必須支援使用章節標籤。 Dynamic Media視頻播放器確實支援章節標籤，但使用第三方視頻播放器可能不支援。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您為視頻建立章節清單的方式與建立字幕的方式大致相同。 即，建立WebVTT檔案。 但請注意，此檔案必須與任何WebVTT標題檔案分開。 不能將字幕和章節合併為一個WebVTT檔案。

您可以使用以下示例作為建立WebVTT檔案時使用章節導航的格式的示例：

### 具有視頻章節導航的WebVTT檔案 {#webvtt-file-with-video-chapter-navigation}

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

在上例中， `Chapter 1` 是提示標識符，是可選的。 的提示時間 `00:00:000 --> 01:04:364` 指定本章的開始時間和結束時間，在 `00:00:000` 的子菜單。 最後三位數是毫秒，可以保留為 `000`，也請參見Wiki頁。 章標題 `The bicycle store behind it all` 是本章內容的實際描述。 當用戶將滑鼠指針懸停在時間軸中的視覺提示點上時，提示標識符、開始提示時間和章節標題都顯示在視頻播放器的彈出窗口中。

由於您使用的是HTML5視頻查看器，因此請確保您建立的章節檔案遵循WebVTT（Web視頻文本軌道）標準。 章檔案名副檔名為.VTT。 您可以瞭解有關WebVTT字幕標準的更多資訊。

請參閱 [WebVTT:Web視頻字幕資訊格式](https://w3c.github.io/webvtt/)。

**要將章節標籤添加到視頻：**

1. 以UTF8編碼保存VTT檔案，以避免在章節標題文本中出現字元格式副本問題。

   通常，您希望將VTT章檔案命名為與視頻檔案同名，並在其後添加章節。 通過這樣做，它可以幫助您使用現有的Web內容管理系統自動生成視頻URL。
1. 在Experience Manager中，上載WebVTT章節檔案。

   請參閱 [上載資產](/help/assets/manage-digital-assets.md#uploading-assets)。

1. 執行下列任一項作業：

   <table>
     <tbody>
      <tr>
       <td>用於彈出式視頻查看器體驗</td>
       <td>
       <ol>
       <li>導航到 <i>出版 </i>要與上載的章節檔案關聯的視頻資產。 請記住，URL僅可在您首次發 <i>布資產</i> 後 <i>複製</i> 。請參閱 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">發佈資產。</a></li>
       <li>從下拉菜單中，選擇 <strong>查看者</strong>。</li>
       <li>在左滑軌中，選擇視頻查看器預設名稱。 視頻的預覽在單獨的頁面中開啟。</li>
       <li>在左滑軌底部，選擇 <strong>URL</strong>。</li>
       <li>在「URL」對話框中，選擇URL並將其複製到剪貼簿，然後將URL傳到簡單文本編輯器中。</li>
       <li>使用以下語法添加視頻的複製URL，以便您可以將其與複製的URL關聯到章節檔案：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>嵌入式視頻查看器體驗<br /> </td>
       <td>
       <ol>
       <li>導航到 <i>出版 </i>要與上載的章節檔案關聯的視頻資產。 請記住，URL僅可在您首次發 <i>布資產</i> 後 <i>複製</i> 。請參閱 <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">發佈資產。</a></li>
       <li>從下拉菜單中，選擇 <strong>查看者</strong>。</li>
       <li>在左滑軌中，選擇視頻查看器預設名稱。 視頻的預覽在單獨的頁面中開啟。</li>
       <li>在左滑軌底部，選擇 <strong>嵌入</strong>。</li>
       <li>在「嵌入代碼」對話框中，選擇整個代碼並將其複製到剪貼簿，然後將其貼上到簡單的文本編輯器中。</li>
       <li>使用以下語法添加視頻的嵌入代碼，以便您可以將其與複製的URL關聯到章節檔案：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to select the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, select the video asset.
1. On the toolbar, select the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Frame from video]**.
        * Select the Play button, then select the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Thumbnail from Assets]**.
        * Select **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then select **[!UICONTROL Select]**.

1. On the Change Thumbnail page, select **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, select **[!UICONTROL Save & Close]**.

-->

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

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

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

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
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

## 更改Dynamic Media資產的URL

在Dynamic Media處理的視頻可以通過現成觀看者使用，也可以通過直接訪問清單URL並通過您自己的自定義觀看者播放。 以下是用於獲取視頻的清單URL的API。

### 關於getVideoManifestURI API

的 `getVideoManifestURI`API通過c公開`q-scene7-api:com.day.cq.dam.scene7.api` 並可用於生成以下清單URL:

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

#### getVideoManifestURI API參數

此API採用以下三個參數：

| 參數 | 說明 |
| --- | --- |
| `resource` | 與Dynamic Media攝入的視頻相對應的資源。 |
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果僅當清單URI發佈且在交付層上可用時，才會將其設定為true。 |

要使用上述方法獲取視頻的清單URL，請添加 [視頻編碼配置檔案](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 到「上傳視頻」資料夾。 Dynamic Media根據在分配給資料夾的視頻編碼檔案中找到的編碼來處理這些視頻。 現在，您可以調用上述API來獲取上載視頻的清單URL。

### 錯誤方案

如果存在錯誤，API將返回空值。 異常記錄在Experience Manager錯誤日誌中。 所有此類記錄錯誤都以 `Could not generate Video Manifest URI`。 以下情形可能導致此類錯誤：

* 安 `IllegalArgumentException` 將記錄以下任一項：

   * 的 `resource` 傳遞的參數為null。
   * 的 `resource` 傳遞的參數不是視頻。
   * 的 `manifestType` 傳遞的參數為null。
   * 的 `onlyIfPublished` 參數傳遞為true，但視頻未發佈。
   * 該視頻沒有使用Dynamic Media的自適應視頻集攝取。

* `IOException` 連接到Dynamic Media時記錄。
* `UnsupportedOperationException` 在 `manifestType` 傳遞的參數 `ManifestType.DASH`，但視頻未使用DASH格式處理。

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





