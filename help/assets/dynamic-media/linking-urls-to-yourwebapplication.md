---
title: 將 URL 連結至您的網頁應用程式
description: 瞭解如何將URL連結至Dynamic Media中的網頁應用程式。
contentOwner: Rick Brough
feature: Publishing,Upload,Viewer Presets,Image Presets,Video
role: User
exl-id: 3cd3f4d5-ebf0-4318-9a0d-1ea69453d57b
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 6%

---

# 將 URL 連結至您的網頁應用程式 {#linking-urls-to-your-web-application}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

您的網站和應用程式會透過URL呼叫來存取Dynamic Media服務。 發佈資產後，Dynamic Media會啟用參考該資產的URL字串。 您可以將這些URL貼到網頁瀏覽器以進行測試。

只有在您&#x200B;*不是*&#x200B;使用Adobe Experience Manager做為WCM時，您才會連結至URL。 當您想要以快顯視窗或模型視窗形式傳送視訊播放器時，會使用連結（而非內嵌）。 如果您使用Experience Manager做為WCM，[請直接在頁面上新增資產](adding-dynamic-media-assets-to-pages.md)。

若要將這些URL字串置入網頁和應用程式中，請從Dynamic Media複製它們。

>[!NOTE]
>
>URL字串僅可用於資產的動態轉譯。 它們目前無法用於位於DAM中的靜態資產，也無法用於動態媒體伺服器。 靜態的轉譯不會出現URL按鈕。

另請參閱[將視訊或影像檢視器內嵌在網頁上](embed-code.md)。

另請參閱[將YouTube URL連結至您的網頁應用程式](video.md)。

另請參閱[傳送回應式網站的最佳化影像](responsive-site.md)。

另請參閱[上傳Assets](/help/assets/manage-digital-assets.md#uploading-assets)。

## 取得資產的URL {#obtaining-a-url-for-an-asset}

您可以取得影像預設集或檢視器預設集產生的URL字串。 複製URL後，它會貼到「剪貼簿」，以便您視需要將其貼到網站或應用程式中的頁面。

>[!NOTE]
>
>在您發佈選取的資產之前，無法複製URL。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>請參閱[發佈Assets](publishing-dynamicmedia-assets.md)。
>
>請參閱[發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

有幾種不同的方法可以取得URL字串。 不過，下列步驟只顯示一個您可以使用的方法。

**若要取得資產的URL：**

1. 導覽至您要複製其影像預設集URL或檢視器預設集URL的&#x200B;*已發佈*&#x200B;資產，然後選取要開啟的資產。

   請記住，URL僅可在您首次發 *布資產* 後 *複製* 。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱[發佈Assets](publishing-dynamicmedia-assets.md)。

   請參閱[發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

1. 根據您選取的資產，執行下列任一項作業：

   * 如果您已選取影像，請在下拉式功能表中選取&#x200B;**[!UICONTROL 轉譯]**。

     在&#x200B;**[!UICONTROL 動態]**&#x200B;標題下，選取預設集名稱，以在右方框架中檢視其轉譯。 如有必要，請捲動「轉譯」清單以檢視動態標題。

     在左側邊欄底部，選取&#x200B;**[!UICONTROL URL]**。

     ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉式選單中選取迴轉集、影像集、轉盤集或視訊，請選取&#x200B;**[!UICONTROL 檢視器]**。

     在左側欄中，選取檢視器預設集名稱。 集合或視訊的預覽會在個別頁面中開啟。

     在左側邊欄的底部，選取&#x200B;**[!UICONTROL URL]**。

     ![chlimage_1-271](assets/chlimage_1-271.png)

1. 若要預覽資產或新增至您的網頁內容頁面，請選取文字並複製到網頁瀏覽器。

   若要結束URL視窗，請選取&#x200B;**[!UICONTROL X]**&#x200B;或選取&#x200B;**[!UICONTROL 關閉]**。

## 取得靜態資產的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支援靜態資產的傳送，這是影像和視訊以外的其他資產。 支援的靜態資產傳送格式包括：

* 3D檔案
* GIF動畫
* 音訊檔案
* CSS
* JavaScript （當貴公司設定自己的網域時）
* PDF
* SVG
* XML
* ZIP

**若要取得靜態資產的URL：**

1. 導覽至您要複製其URL的&#x200B;*已發佈*&#x200B;靜態資產，然後選取要開啟的資產。

   請記住，URL僅可在您首次&#x200B;*發佈*&#x200B;靜態資產&#x200B;*後複製*。

   請參閱[發佈Assets](publishing-dynamicmedia-assets.md)。

1. 使用下列任一方法取得已發佈靜態資產的URL：

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

        例如，`https://aem.com/is/content/adobe/image.gif`。

   * 選取&#x200B;**[!UICONTROL 資產]** > **[!UICONTROL 動態轉譯]**，然後選取靜態資產的動態轉譯並複製URL。

     變更複製的URL以在路徑中使用`is/content`而非`is/image/`。

## 取得已發佈影片轉譯的影片URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲端]** > **[!UICONTROL 雲端服務]**。
1. 在&#x200B;**[!UICONTROL 雲端服務]**&#x200B;頁面上，向下捲動至&#x200B;**[!UICONTROL Dynamic Media雲端服務]**&#x200B;標題，然後選取&#x200B;**[!UICONTROL 顯示設定]**。
1. 在&#x200B;**[!UICONTROL 可用的組態]**&#x200B;下，選取您想要的組態名稱。

1. 在&#x200B;**[!UICONTROL Dynamic Media雲端設定]**&#x200B;頁面的&#x200B;**[!UICONTROL 視訊服務URL]**&#x200B;下，複製整個URL路徑。 您稍後需要在步驟中複製URL路徑。

   例如，URL路徑可能如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   （上述路徑僅供解釋；並非您複製的實際路徑。）

1. 在「 **[!UICONTROL 註冊ID]**」下方，複製ID最後一部分中找到的客戶名稱。

   例如，如果註冊ID為`87654321|MyCompany`，則客戶名稱將是`MyCompany`。

1. 在頁面的左上角附近，選取&#x200B;**[!UICONTROL 雲端服務]**，然後選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**。
1. 從JCR (Java™內容存放庫)向下複製整個視訊轉譯路徑。

   例如，視訊的轉譯路徑可能如下所示：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   （上述路徑僅供解釋；並非您複製的實際路徑。）

1. 若要形成完整的URL路徑，請依照下列順序排列複製的資訊：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步驟中的範例路徑和範例客戶名稱，完整路徑如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此路徑是已發佈視訊轉譯的完整視訊URL。

## 取得最適化位元速率串流(HLS)的視訊URL {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲端]** > **[!UICONTROL 雲端服務]**。
1. 在&#x200B;**[!UICONTROL 雲端服務]**&#x200B;頁面上，向下捲動至&#x200B;**[!UICONTROL Dynamic Media雲端服務]**&#x200B;標題，然後選取&#x200B;**[!UICONTROL 顯示設定]**。
1. 在&#x200B;**[!UICONTROL 可用的組態]**&#x200B;下，選取您想要的組態名稱。
1. 在&#x200B;**[!UICONTROL Dynamic Media雲端服務設定]**&#x200B;頁面上，執行下列動作：

   * 在&#x200B;**[!UICONTROL 視訊服務URL]**&#x200B;下，複製整個URL路徑。 您稍後需要這些步驟中複製的URL路徑。 例如，URL路徑可能如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   （上述路徑僅供解釋；並非您複製的實際路徑。）

   * 在&#x200B;**[!UICONTROL 註冊ID]**&#x200B;底下，複製ID最後一部分中找到的客戶名稱。 您稍後需要這些步驟中複製的客戶名稱。

     例如，如果註冊ID為`87654321|demoCo`，則您複製的客戶名稱將是`demoCo`。

1. 根據您使用的視訊傳送通訊協定，複製各自的通訊協定選擇器。 您稍後需要在這些步驟中複製通訊協定選擇器。

   <table>
    <tbody>
      <tr>
      <td><strong>您正在使用的視訊傳送通訊協定</strong></td>
      <td><strong>要使用的通訊協定選擇器</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>如果您使用HTTP （不安全的視訊傳送），請務必在先前複製的視訊服務URL值中將<code>https</code>變更為<code>http</code>。</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. 複製Experience Manager中的完整視訊資產路徑，並由Dynamic Media處理。 您稍後在這些步驟中需要此複製的視訊資產路徑。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 合併您先前複製的所有片段，依下列順序建立字串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用這些步驟中範例的複製資訊，字串會顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 將`.m3u8`附加至字串的結尾以完成URL。 例如，將`.m3u8`附加至上一步驟的字串，完整的URL路徑會顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2傳送您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並減少所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2進行，以提供更理想的回應和載入時間。

請參閱[HTTP2內容傳送](http2faq.md)，以取得有關透過您的Dynamic Media帳戶開始使用HTTP/2的完整詳細資料。
