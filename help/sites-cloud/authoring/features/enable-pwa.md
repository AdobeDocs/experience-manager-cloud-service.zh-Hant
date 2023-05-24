---
title: 啟用漸進式網頁應用程式功能
description: AEM Sites可讓內容作者透過簡易設定（而非編碼）為任何網站啟用漸進式網頁應用程式功能。
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: 3910b47c5d25679d03409380d91afaa6ff5ab265
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 1%

---

# 啟用漸進式網頁應用程式功能 {#enabling-pwa}

透過簡單的設定，內容作者現在可以為在AEM Sites中建立的體驗啟用漸進式網頁應用程式(PWA)功能。

>[!CAUTION]
>
>這是進階功能，需要：
>
>* PWA知識
>* 您的網站和內容結構知識
>* 瞭解快取策略
>* 來自開發團隊的支援
>
>使用此功能之前，建議您先與開發團隊討論，以定義將它用於專案的最佳方式。

## 簡介 {#introduction}

[漸進式網頁應用程式(PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) 允許AEM sites本機儲存在使用者的電腦上，並可離線存取，藉此為Sites啟用類似應用程式的沈浸式體驗。 即使失去網際網路連線，使用者也可以在行動中瀏覽網站。 即使網路遺失或不穩定，PWA仍可提供順暢的體驗。

內容作者無需對網站進行任何重新編碼，而是可以將PWA屬性設定為中的額外索引標籤 [頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 網站的。

* 儲存或發佈後，此設定會觸發一個事件處理常式，此處理常式會寫出 [資訊清單檔案](https://developer.mozilla.org/en-US/docs/Web/Manifest) 和 [服務背景工作](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) 可啟用網站上的PWA功能。
* 也會維護Sling對應，以確保從應用程式的根提供Service Worker，以啟用代理內容，允許應用程式內的離線功能。

透過PWA，使用者擁有網站的本機副本，即使沒有網際網路連線，也能提供類似應用程式的體驗。

>[!NOTE]
>
>漸進式網頁應用程式是一項不斷發展的技術，可支援本機應用程式安裝和其他功能 [視您使用的瀏覽器而定。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 必備條件 {#prerequisites}

若要能夠針對您的網站使用PWA功能，您的專案環境有兩個要求：

1. [使用核心元件](#adjust-components) 以善用此功能
1. [調整您的Dispatcher](#adjust-dispatcher) 公開所需檔案的規則

這些是作者將需要與開發團隊協調的技術步驟。 每個網站只需執行這些步驟一次。

### 使用核心元件 {#adjust-components}

核心元件2.15.0版及更新版本完全支援AEM網站的PWA功能。 由於AEMaaCS一律包含最新版本的核心元件，因此您可以運用現成的PWA功能。 您的AEMaaCS專案會自動滿足此要求。

>[!NOTE]
>
>Adobe不建議在自訂元件上使用PWA功能，或是不建議使用 [從核心元件擴充。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
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

PWA功能會產生並使用 `/content/<sitename>/manifest.webmanifest` 檔案。 依預設， [Dispatcher](/help/implementing/dispatcher/overview.md) 不會公開此類檔案。 若要公開這些檔案，開發人員必須將下列設定新增至您的網站專案。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

根據您的專案，您可能想要在重寫規則中包含不同型別的擴充功能。 此 `webmanifest` 當您匯入隱藏和重新導向請求的規則時，將擴充功能加入重寫條件會很有用 `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## 為您的網站啟用PWA {#enabling-pwa-for-your-site}

替換為 [必備條件](#prerequisites) 符合，內容作者很容易就能對網站啟用PWA功能。 以下是如何執行此操作的基本概述。 個別選項將於一節中詳細說明 [詳細選項。](#detailed-options)

1. 登入AEM。
1. 從主功能表，點選或按一下 **導覽** -> **網站**.
1. 選取您的網站專案，然後點選或按一下 [**屬性**](/help/sites-cloud/authoring/fundamentals/page-properties.md) 或使用快速鍵 `p`.
1. 選取 **漸進式網頁應用程式** 標籤並設定適用的屬性。 您至少需要：
   1. 選取選項 **啟用PWA**.
   1. 定義 **啟動URL**.

      ![啟用 PWA](../assets/pwa-enable.png)

   1. 將512x512 png圖示上傳至DAM，並參照該圖示作為應用程式的圖示。

      ![定義PWA圖示](../assets/pwa-icon.png)

   1. 設定您希望Service Worker離線使用的路徑。 典型路徑包括：
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任何協力廠商字型參照
      * `/etc/clientlibs/<sitename>`

      ![定義PWA離線路徑](../assets/pwa-offline.png)


1. 點選或按一下&#x200B;**儲存並關閉**。

您的網站現已設定完成，您可以 [將其安裝為本機應用程式。](#using-pwa-enabled-site)

## 使用已啟用PWA的網站 {#using-pwa-enabled-site}

現在您已擁有 [已設定您的網站以支援PWA，](#enabling-pwa-for-your-site) 您可以親身體驗。

1. 在中存取網站 [支援的瀏覽器。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 您會在瀏覽器的位址列看到新圖示，表示網站可作為本機應用程式安裝。
   * 視瀏覽器而定，圖示可能會有所不同，且瀏覽器也可能會顯示通知（例如橫幅或對話方塊），指出可作為本機應用程式安裝。
1. 安裝應用程式。
1. 應用程式將安裝在裝置的主畫面上。
1. 開啟應用程式、瀏覽一點，然後檢視頁面是否可離線使用。

## 詳細選項 {#detailed-options}

下節提供以下情況下可用選項的更多詳細資料： [設定您的網站以進行PWA。](#enabling-pwa-for-your-site)

### 設定安裝體驗 {#configure-installable-experience}

這些設定可讓您的網站安裝在訪客的主畫面上並離線使用，讓網站的行為與原生應用程式類似。

* **啟用PWA**  — 這是啟用網站PWA功能的主要切換按鈕。
* **啟動URL**  — 這是 [偏好的起始URL](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 當使用者載入本機安裝的應用程式時，應用程式會開啟。
   * 這可以是內容結構中的任何路徑。
   * 這不一定是根目錄，且通常是應用程式的專屬歡迎頁面。
   * 如果此URL是相對的，則資訊清單URL會作為基礎URL來解析。
   * 留空時，功能會使用安裝應用程式的網頁位址。
   * 建議設定值。
* **顯示模式**  — 啟用PWA的應用程式仍為透過瀏覽器傳送的AEM網站。 [這些顯示選項](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 定義瀏覽器應該如何隱藏，或如何以其他方式顯示給本機裝置上的使用者。
   * **獨立**  — 使用者看不到瀏覽器，且看起來像原生應用程式。 這是預設值。
      * 透過此選項，應用程式導覽必須能夠完全透過您的內容進行，使用網站頁面上的連結和元件，而不使用瀏覽器的導覽控制項。
   * **瀏覽器**  — 瀏覽器在造訪網站時如常顯示。
   * **最小UI**  — 瀏覽器大多隱藏，就像原生應用程式，但會顯示基本導覽控制項。
   * **全熒幕**  — 瀏覽器會完全隱藏（像原生應用程式），但在全熒幕模式下呈現。
      * 透過此選項，應用程式導覽必須能夠完全透過您的內容進行，使用網站頁面上的連結和元件，而不使用瀏覽器的導覽控制項。
* **熒幕方向**  — 作為本機應用程式，PWA需要瞭解如何處理 [裝置方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **任何**  — 應用程式會根據使用者裝置的方向進行調整。 這是預設值。
   * **縱向**  — 這強制應用程式以縱向配置開啟，無論使用者裝置的方向為何。
   * **橫向**  — 這強制應用程式以橫向配置開啟，無論使用者裝置的方向為何。
* **佈景主題顏色**  — 這會定義 [應用程式的色彩](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 這會影響本機使用者的作業系統顯示原生UI工具列和導覽控制項的方式。 視瀏覽器而定，它可能會影響其他應用程式簡報元素。
   * 使用顏色井彈出式視窗來選取顏色。
   * 顏色也可以由十六進位或RGB值定義。
* **背景顏色**  — 這會定義 [應用程式的背景顏色，](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 會在應用程式載入時顯示。
   * 使用顏色井彈出式視窗來選取顏色。
   * 顏色也可以由十六進位或RGB值定義。
   * 特定瀏覽器 [自動建立啟動畫面](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) 從應用程式名稱、背景顏色和圖示。
* **圖示**  — 這定義 [圖示](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 代表使用者裝置上的應用程式。
   * 圖示必須是大小為512x512畫素的png檔案。
   * 圖示必須是 [儲存在DAM中。](/help/assets/overview.md)

### 快取管理（進階） {#offline-configuration}

這些設定可讓此網站的部分內容可離線使用，並可在訪客的裝置上在本機使用。 這可控制網頁應用程式的快取，以最佳化網路請求並支援離線體驗。

* **快取策略和內容重新整理頻率**  — 此設定會定義PWA的快取模型。
   * **適度** - [此設定](https://web.dev/stale-while-revalidate/) 適用於大部分網站，且為預設值。
      * 透過此設定，使用者首先檢視的內容將從快取載入，當使用者使用該內容時，快取中的其餘內容將會重新驗證。
   * **經常**  — 拍賣行等需要快速更新的網站就是這種情況。
      * 透過此設定，應用程式會先透過網路尋找最新內容，如果無法使用，則會回溯至本機快取。
   * **極少**  — 這適用於參考頁面等幾乎靜態的網站。
      * 透過此設定，應用程式會先在快取中尋找內容，如果沒有，則會回傳至網路來擷取內容。
* **檔案預先快取**  — 這些在AEM上託管的檔案將在安裝Service Worker時和使用它之前儲存到本機瀏覽器快取。 這可確保網頁應用程式在離線時可完全正常運作。
* **路徑包含**  — 攔截定義路徑的網路請求，並根據設定的傳回快取內容 **快取策略和內容重新整理頻率**.
* **快取排除專案**  — 無論下的設定為何，系統都不會快取這些檔案 **檔案預先快取** 和 **路徑包含**.

>[!TIP]
>
>您的開發人員團隊很可能對如何設定離線設定有寶貴意見。

## 限制和建議 {#limitations-recommendations}

並非所有PWA功能都可用於AEM Sites。 以下是幾項值得注意的限制。

* 如果使用者未使用應用程式，頁面不會自動同步或更新。

實作Adobe時，PWA也會提出下列建議。

### 最小化要預先快取的資源數量。 {#minimize-precache}

Adobe建議您限制要預先快取的頁數。

* 內嵌程式庫，減少預先快取時要管理的專案數量。
* 限制要預先快取的影像變化數量。

### 在專案指令碼和樣式表穩定後啟用PWA。 {#pwa-stabilized}

使用者端程式庫在傳送時已新增快取選擇器，並遵循以下模式 `lc-<checksumHash>-lc`. 每當構成程式庫的其中一個檔案（和相依性）變更時，此選取器就會變更。 如果您列出要由service-worker預先快取的使用者端程式庫，且想要參照新版本，請手動擷取並更新專案。 因此，我們建議您在穩定專案指令碼和樣式表後，將您的網站設定為PWA。

### 將影像變化數減到最少。 {#minimize-variations}

AEM核心元件的影像元件會決定要擷取的前端最佳轉譯。 此機制也包含與該資源上次修改時間對應的時間戳記。 此機制會使PWA預先快取的設定複雜化。

設定預先快取時，使用者需要列出所有可擷取的路徑變數。 這些變化是由品質和寬度等引數所組成。 強烈建議將這些變數的數量減少到最多三個 — 小、中、大。 您可以透過以下對話方塊的內容原則來執行此操作： [影像元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

若未謹慎設定，記憶體與網路耗用量可能會嚴重影響PWA效能。 此外，如果您打算預先快取50個影像，且每個影像有3個寬度，維護網站的使用者必須在頁面屬性的PWA預先快取區段中維護最多150個專案的清單。

Adobe也建議您在使用影像的專案穩定後，將網站設定為PWA。
