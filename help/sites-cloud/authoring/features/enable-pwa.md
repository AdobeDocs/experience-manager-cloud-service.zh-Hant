---
title: 啟用漸進式網頁應用程式功能
description: AEM Sites可讓內容作者透過簡單的設定而非編碼，為任何網站啟用漸進式網頁應用程式功能。
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 0%

---

# 啟用漸進式網頁應用程式功能{#enabling-pwa}

透過簡單的設定，內容作者現在可以為AEM Sites中建立的體驗啟用漸進式網頁應用程式(PWA)功能。

>[!CAUTION]
>
>這是進階功能，需要：
>
>* PWA知識
>* 了解您的網站和內容結構
>* 了解快取策略
>* 來自您開發團隊的支援

>
>
建議您在使用此功能之前，先與開發團隊討論此問題，以定義將此功能用於專案的最佳方式。

>[!NOTE]
>
>本檔案所述的功能預計於2021年3月的[AEM版本中作為Cloud Service提供。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 簡介 {#introduction}

[漸進式網頁應用程式(PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) 可讓使用者將應用程式儲存在本機的電腦上，並可離線存取，為AEM網站提供沈浸式應用程式式體驗。即使遺失網際網路連線，使用者仍可在移動時瀏覽網站。 PWA即使網路遺失或不穩定，仍可提供順暢的體驗。

內容作者不必對網站進行任何重新編碼，而是可以將PWA屬性設定為網站[頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md)中的額外索引標籤。

* 儲存或發佈時，此設定會觸發事件處理常式，將[資訊清單檔案](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服務背景工作](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)寫出，以啟用網站上的PWA功能。
* 也會維護Sling對應，以確保從應用程式的根目錄提供服務背景工作，以啟用代理內容，允許應用程式內的離線功能。

透過PWA，使用者可取得網站的本機副本，即使沒有網際網路連線，也能提供類似應用程式的體驗。

>[!NOTE]
>
>漸進式Web應用程式是一項不斷發展的技術，支援本機應用程式安裝和其他功能[取決於您使用的瀏覽器。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 必備條件 {#prerequisites}

若要使用網站的PWA功能，您的專案環境有兩項需求：

1. [使用核](#adjust-components) 心元件來運用此功能
1. [調整您的](#adjust-dispatcher) Dispatcher規則以公開必要的檔案

這些是作者需要與開發團隊協調的技術步驟。 每個網站只需執行一次這些步驟。

### 使用核心元件{#adjust-components}

核心元件2.15.0版及更新版本完全支援AEM sites的PWA功能。 由於AEMaaCS一律包含最新版核心元件，因此您可以立即使用PWA功能。 您的AEMaaCS專案會自動符合此需求。

>[!NOTE]
>
>Adobe不建議在自訂元件或元件上使用PWA功能，而不是從核心元件[擴展。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer will need to add the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer will also need to add the following link to the `customfooterlibs.html` file of your page component.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```
-->

### 調整您的Dispatcher {#adjust-dispatcher}

PWA功能生成並使用`/content/<sitename>/manifest.webmanifest`檔案。 依預設，[Dispatcher](/help/implementing/dispatcher/overview.md)不會公開這類檔案。 若要公開這些檔案，開發人員必須將下列設定新增至您的網站專案。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

根據您的專案，您可能會想在重寫規則中加入不同類型的擴充功能。 當您導入可隱藏並重新導向`/content/<projectName>`請求的規則時，`webmanifest`擴充功能在重新寫入條件中很實用。

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## 啟用網站PWA{#enabling-pwa-for-your-site}

符合[必要條件](#prerequisites)後，內容作者便可輕鬆啟用網站的PWA功能。 以下是如何執行此作業的基本概述。 在[Detailed Options中詳細介紹了各個選項。](#detailed-options)

1. 登入AEM。
1. 從主菜單中，點選或按一下「**Navigation** -> **Sites**」。
1. 選取您的網站專案，然後點選或按一下「屬性」[**或使用快捷鍵`p`。**](/help/sites-cloud/authoring/fundamentals/page-properties.md)
1. 選取&#x200B;**漸進式Web應用程式**&#x200B;標籤並設定適用的屬性。 您至少會想：
   1. 選擇&#x200B;**啟用PWA**&#x200B;選項。
   1. 定義&#x200B;**啟動URL**。

      ![啟用 PWA](../assets/pwa-enable.png)

   1. 將512x512的png圖示上傳至DAM，並參照該圖示作為應用程式的圖示。

      ![定義PWA圖示](../assets/pwa-icon.png)

   1. 配置希望服務員離線的路徑。 典型路徑為：
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任何第三方字型參考
      * `/etc/clientlibs/<sitename>`

      ![定義PWA離線路徑](../assets/pwa-offline.png)


1. 點選或按一下「**儲存並關閉**」。

您的網站現在已設定完畢，您可以[以本機應用程式的形式安裝。](#using-pwa-enabled-site)

## 使用啟用PWA的站點{#using-pwa-enabled-site}

現在您已將[網站設定為支援PWA,](#enabling-pwa-for-your-site)您可以自己體驗它。

1. 在[支援的瀏覽器中訪問站點。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 您會在瀏覽器的位址列中看到新圖示，指出網站可安裝為本機應用程式。
   * 視瀏覽器而定，圖示可能會有所不同，而瀏覽器也可能顯示通知（例如橫幅或對話方塊），指出可以安裝為本機應用程式。
1. 安裝應用程式。
1. 應用程式會安裝在您裝置的主畫面上。
1. 開啟應用程式，瀏覽一下，然後查看頁面是否可離線使用。

## 詳細選項{#detailed-options}

下節提供[配置網站以進行PWA時可用選項的詳細資訊。](#enabling-pwa-for-your-site)

### 配置可安裝體驗{#configure-installable-experience}

這些設定可讓您的網站在訪客的主畫面上安裝，且離線可供使用，讓其行為與原生應用程式相同。

* **啟用PWA**  — 這是啟用網站PWA的主要切換按鈕。
* **啟動URL**  — 這是使用 [者載入本](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 機安裝的應用程式時，應用程式將會開啟的慣用啟動URL。
   * 這可以是內容結構中的任何路徑。
   * 此頁面不須為根目錄，且通常為應用程式的專用歡迎頁面。
   * 如果此URL為相對URL，則會以資訊清單URL作為解析此URL的基礎URL。
   * 若保留為空白，則功能會使用我們應用程式安裝來源網頁的位址。
   * 建議設定值。
* **顯示模式**  — 啟用PWA的應用程式仍為透過瀏覽器傳送的AEM網站。[這些顯](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 示選項可定義瀏覽器在本機裝置上如何隱藏或呈現給使用者。
   * **獨立**  — 瀏覽器完全隱藏於使用者面前，而且看起來像原生應用程式。這是預設值。
      * 透過此選項，您必須使用網站頁面上的連結和元件，完全透過您的內容進行應用程式導覽，而不需使用瀏覽器的導覽控制項。
   * **瀏覽器**  — 瀏覽器的顯示方式與瀏覽網站時的一般相同。
   * **最低的UI**  — 瀏覽器大多為隱藏狀態，例如原生應用程式，但基本導覽控制項會公開。
   * **全螢幕**  — 瀏覽器已完全隱藏，就像原生應用程式一樣，但會以全螢幕模式呈現。
      * 透過此選項，您必須使用網站頁面上的連結和元件，完全透過您的內容進行應用程式導覽，而不需使用瀏覽器的導覽控制項。
* **螢幕方向**  — 身為本機應用程式，PWA需知道如何處理裝 [置方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **任何**  — 應用程式會根據使用者裝置的方向進行調整。這是預設值。
   * **縱向**  — 這會強制應用程式以縱向版面開啟，而不論使用者裝置的方向為何。
   * **橫向**  — 這會強制應用程式以橫向版面配置開啟，而不論使用者裝置的方向為何。
* **主題顏色**  — 這會定 [義應用程](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 式的顏色，影響本機使用者作業系統顯示原生UI工具列和導覽控制項的方式。視瀏覽器而定，它可能會影響其他應用程式呈現元素。
   * 使用顏色井彈出式視窗來選取顏色。
   * 顏色也可以由十六進位或RGB值定義。
* **背景顏色**  — 這會定義應 [用程式的背景顏色，](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 當應用程式載入時便會顯示。
   * 使用顏色井彈出式視窗來選取顏色。
   * 顏色也可以由十六進位或RGB值定義。
   * 某些瀏覽器[會從應用程式名稱、背景顏色和圖示自動](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)建立開始畫面。
* **圖示**  — 這會定 [義](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 代表使用者裝置上應用程式的圖示。
   * 圖示必須是大小512x512像素的png檔案。
   * 圖示必須儲存在DAM中[。](/help/assets/overview.md)

### 快取管理（進階）{#offline-configuration}

這些設定可讓此網站的部分離線使用，並可在訪客的裝置上於本機使用。 這可控制Web應用程式的快取，以最佳化網路要求並支援離線體驗。

* **快取策略和內容重新整理的頻率**  — 此設定會定義您PWA的快取模型。
   * **適度**  - [此設](https://web.dev/stale-while-revalidate/) 定適用於大部分網站，且為預設值。
      * 使用此設定，將從快取載入使用者先前檢視的內容，而當使用者使用該內容時，將會重新驗證快取中其餘的內容。
   * **經常**  — 如果網站需要更新速度非常快，例如拍賣行，就是如此。
      * 透過此設定，應用程式會先透過網路尋找最新內容，如果無法使用，則會回復至本機快取。
   * **極少**  — 幾乎為靜態的網站（例如參考頁面）就是如此。
      * 透過此設定，應用程式會先在快取中尋找內容，如果無法使用，則會回復至網路加以擷取。
* **檔案預先快取**  — 當服務工作程式安裝時和使用前，AEM上托管的這些檔案會儲存至本機瀏覽器快取。這可確保離線時網頁應用程式可正常運作。
* **路徑包含**  — 會根據已設定的快取策略和內容重新整理頻率，截取已定義路徑的網 **路要求並傳回快取內容**。
* **快取排除**  — 無論檔案預先快取和路徑包含下的設定為何， **都不會快** 取這些 **檔案**。

>[!TIP]
>
>關於如何設定離線設定，開發人員團隊可能有寶貴的意見。

## 限制和Recommendations {#limitations-recommendations}

並非所有PWA功能都適用於AEM Sites。 以下是幾項顯著限制。

* 如果使用者未使用應用程式，則不會自動同步或更新頁面。

Adobe在您實作PWA時也會提出下列建議。

### 將要預快取的資源數減到最少。{#minimize-precache}

Adobe建議您限制預先快取的頁面數。

* 內嵌程式庫，以減少預先快取時要管理的項目數。
* 將影像變化數限制為預先快取。

### 在項目指令碼和樣式表穩定後啟用PWA。{#pwa-stabilized}

隨著快取選擇器的增加而傳送用戶端程式庫，且遵循下列模式`lc-<checksumHash>-lc`。 每次組成程式庫的其中一個檔案（和相依性）變更時，此選取器都會變更。 如果列出了要由服務員預先快取的客戶端庫，並且要引用新版本，則可以手動檢索和更新該條目。 因此，我們建議您在項目指令碼和樣式表穩定後，將站點配置為PWA。

### 將影像變化的數量減到最少。{#minimize-variations}

AEM核心元件的影像元件決定要擷取的最佳轉譯之前端。 此機制也包含與該資源上次修改時間對應的時間戳記。 此機制使PWA預快取的設定複雜化。

設定預先快取時，使用者需要列出所有可擷取的路徑變數。 這些變化由質量和寬度等參陣列成。 強烈建議將這些變數的數量減少至最多3個 — 小、中、大。 您可以透過[影像元件的content-policy對話方塊執行此操作。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

如果未仔細配置，記憶體和網路消耗將嚴重影響PWA的效能。 此外，如果您想要預快取（例如50個影像），並且每個影像有3個寬度，則維護網站的使用者必須在頁面屬性的「PWA預快取」區段中，維護最多150個項目的清單。

Adobe也建議您在影像的專案使用穩定後，將網站設為PWA。
