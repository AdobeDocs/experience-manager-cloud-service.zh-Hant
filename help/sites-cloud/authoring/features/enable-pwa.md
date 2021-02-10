---
title: 啟用漸進式網頁應用程式功能
description: AEM Sites可讓內容作者透過簡單的設定，而非編碼，將漸進式網頁應用程式功能啟用至任何網站。
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 071eefa3b6f5e9636ace612e968b6a9627c98550
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# 啟用漸進式網頁應用程式功能{#enabling-pwa}

透過簡單的設定，內容作者現在可以為在AEM Sites中建立的體驗啟用漸進式網頁應用程式(PWA)功能。

>[!CAUTION]
>
>這項進階功能需要：
>
>* PWA的知識
>* 瞭解您的網站和內容結構
>* 瞭解快取策略
>* 您開發團隊的支援

>
>
建議您在使用此功能之前先與開發團隊討論此功能，以定義最適合您專案的運用方式。

## 簡介 {#introduction}

[漸進式網頁應用程式(PWAs)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) 可讓AEM網站在本機儲存並離線存取，提供身歷其境的應用程式樣式體驗。即使遺失網際網路連線，使用者仍可在外出時瀏覽網站。 PWA即使網路丟失或不穩定，也能提供無縫體驗。

內容作者不必對網站進行任何重新編碼，而可將PWA屬性設定為網站[頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md)中的其他標籤。

* 儲存或發佈時，此設定會觸發事件處理常式，將[manifest檔案](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服務工作者](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)寫出，以啟用網站上的PWA功能。
* 清單和服務工作器儲存在適用於站點的[上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html)中。 Sling映射也會保留，以確保服務工作者可從應用程式的根目錄取得，以啟用代理內容，允許應用程式內的離線功能。

使用PWA，使用者就擁有網站的本機副本，即使沒有網際網路連線，也能提供類似應用程式的體驗。

>[!NOTE]
>
>漸進式網頁應用程式是一項新興的技術，支援本端應用程式安裝和其他功能[取決於您使用的瀏覽器。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 必備條件 {#prerequisites}

為了能夠為您的網站使用PWA功能，您的專案環境有兩項需求：

1. [調整元](#adjust-components) 件以啟用此功能
1. [調整調度程](#adjust-dispatcher) 序規則以公開所需的檔案

這些是作者需要與開發團隊協調的技術步驟。 每個網站只需執行這些步驟一次。

### 調整元件{#adjust-components}

您的元件需要包含[manifest檔案](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服務員](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)，它們支援PWA功能。

若要這麼做，開發人員必須將下列連結新增至頁面元件的`customheaderlibs.html`檔案。

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

開發人員也需要將下列連結新增至頁面元件的`customfooterlibs.html`檔案。

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

>[!NOTE]
>
>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)的未來版本將自動包含這些功能。 不過，如果您使用自訂元件而非核心元件，則一律需要進行這些調整。

### 調整您的Dispatcher {#adjust-dispatcher}

PWA功能生成並使用`/content/<sitename>/manifest.webmanifest`檔案。 預設情況下，[dispatcher](/help/implementing/dispatcher/overview.md)不公開此類檔案。 若要公開這些檔案，開發人員必須將下列組態新增至您的網站專案。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>[AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing)的未來版本將包含此組態。

## 為您的站點啟用PWA {#enabling-pwa-for-your-site}

當[符合先決條件](#prerequisites)時，內容作者很容易將PWA功能啟用至網站。 以下是如何進行此操作的基本概述。 [「詳細選項」一節中詳細介紹了各個選項。](#detailed-options)

1. 登入AEM。
1. 從主菜單中，按一下或按一下&#x200B;**Navigation** -> **Sites**。
1. 選擇您的網站專案，點選或按一下「屬性&#x200B;[****](/help/sites-cloud/authoring/fundamentals/page-properties.md)」或使用熱鍵`p`。
1. 選擇&#x200B;**漸進式Web應用程式**&#x200B;標籤並設定適用的屬性。 您至少要：
   1. 選擇「Enable PWA **（啟用PWA**）」選項。
   1. 定義&#x200B;**啟動URL**。

      ![啟用 PWA](../assets/pwa-enable.png)

   1. 將512x512 png圖示上傳至DAM，並參照該圖示作為應用程式的圖示。

      ![定義PWA圖示](../assets/pwa-icon.png)

   1. 配置您希望服務員離線的路徑。 典型路徑為：
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任何第三方字型參考
      * `/etc/clientlibs/<sitename>`

      ![定義PWA離線路徑](../assets/pwa-offline.png)


1. 點選或按一下「儲存並關閉」**。**

您的網站現在已設定好，您可以[將其安裝為本機應用程式。](#using-pwa-enabled-site)

## 使用您啟用PWA的網站{#using-pwa-enabled-site}

現在您已將[網站設定為支援PWA，您可以親身體驗。](#enabling-pwa-for-your-site)

1. 在[支援的瀏覽器中存取網站。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 您會在瀏覽器的位址列中看到`+`圖示，指出該網站可以安裝為本機應用程式。
   * 視瀏覽器而定，它也會顯示通知（例如橫幅或對話方塊），指出可以以本機應用程式的形式安裝。
1. 安裝應用程式。
1. 應用程式將會安裝在您裝置的首頁畫面上。
1. 開啟應用程式、瀏覽一下，然後看到頁面是離線可用的。

## 詳細選項{#detailed-options}

以下章節提供了[為PWA配置站點時可用選項的詳細資訊。](#enabling-pwa-for-your-site)

### 配置可安裝體驗{#configure-installable-experience}

這些設定可讓您的網站在訪客的首頁畫面上安裝，並離線使用，讓其行為與原生應用程式相同。

* **啟用PWA**  —— 這是為網站啟用PWA的主要切換。
* **啟動URL** -這是使用者 [載入本機安](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 裝的應用程式時，應用程式會開啟的偏好啟動URL。
   * 這可以是內容結構中的任何路徑。
   * 這不必是根目錄，通常是應用程式的專屬歡迎頁面。
   * 如果此URL為相對URL，則資訊清單URL會當做基本URL來解析它。
   * 若保留空白，則功能會使用我們應用程式從中安裝的網頁位址。
   * 建議您設定值。
* **顯示模式** -啟用PWA的應用程式仍是透過瀏覽器傳送的AEM網站。[這些顯](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 示選項定義瀏覽器在本機裝置上的隱藏方式或呈現給使用者的方式。
   * **獨立** -瀏覽器完全隱藏於使用者之外，看起來就像原生應用程式。這是預設值。
      * 使用這個選項，應用程式導覽必須完全透過您的內容進行，而不需使用瀏覽器的導覽控制項，即可使用網站頁面上的連結和元件。
   * **瀏覽器** -瀏覽器的顯示與瀏覽網站時的正常顯示相同。
   * **最低UI**  —— 瀏覽器大部分都是隱藏的，就像原生應用程式，但基本的導覽控制項是公開的。
   * **全螢幕** -瀏覽器完全隱藏，就像原生應用程式，但會以全螢幕模式呈現。
      * 使用這個選項，應用程式導覽必須完全透過您的內容進行，而不需使用瀏覽器的導覽控制項，即可使用網站頁面上的連結和元件。
* **螢幕方向** - PWA是本機應用程式，需要知道如何處理裝 [置方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Any**  —— 應用程式會依使用者裝置的方向調整。這是預設值。
   * **縱向** -這會強制應用程式以縱向版面開啟，不論使用者裝置的方向為何。
   * **橫向** -這會強制應用程式在橫向版面中開啟，不論使用者裝置的方向為何。
* **主題色彩** -這會定 [義應用程](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 式的色彩，這會影響本機使用者作業系統顯示原生UI工具列和導覽控制項的方式。視瀏覽器而定，可能會影響其他應用程式簡報元素。
   * 使用顏色井快顯視窗來選取顏色。
   * 色彩也可以由十六進位或RGB值來定義。
* **背景顏色** -這會定義應 [用程式的背景顏色，](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 當應用程式載入時會顯示。
   * 使用顏色井快顯視窗來選取顏色。
   * 色彩也可以由十六進位或RGB值來定義。
   * 某些瀏覽器[會從應用程式名稱、背景色彩和圖示自動建立啟動顯示畫面](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)。
* **圖示** -這會定 [義](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 代表使用者裝置上應用程式的圖示。
   * 圖示必須是大小為512x512像素的png檔案。
   * 圖示必須儲存在DAM中。](/help/assets/overview.md)[

### 快取管理（高級）{#offline-configuration}

這些設定可讓此網站的部分內容離線使用，並可在訪客的裝置上在本機使用。 這可讓您控制網頁應用程式的快取，以最佳化網路要求並支援離線體驗。

* **快取策略和內容重新整理的頻率** -此設定會定義PWA的快取模型。
   * **適中** - [此](https://web.dev/stale-while-revalidate/) 設定適用於大部分網站，且為預設值。
      * 使用此設定時，使用者先檢視的內容會從快取載入，而當使用者使用該內容時，快取中的其餘內容將會重新驗證。
   * **經常** -對於需要快速更新的網站，例如拍賣行，就是如此。
      * 透過此設定，應用程式會先透過網路尋找最新的內容，如果不可用，則會返回本機快取。
   * **很少** -對於幾乎為靜態的網站（例如參考頁面），這是個情況。
      * 使用此設定時，應用程式會先在快取中尋找內容，如果無法使用，則會返回網路擷取內容。
* **檔案預先快取** -當服務工作者安裝或使用之前，AEM上裝載的這些檔案將儲存至本機瀏覽器快取。這可確保網頁應用程式在離線時能完整運作。
* **路徑包含** -根據配置的快取策略和內容刷新頻率，截取對已定義路徑的網路請求並返回 **快取內容**。
* **快取排除** -不論檔案前置快取和路徑內含項目下的設定，這些檔 **案都不會** 被快 **取**。

>[!TIP]
>
>您的開發人員團隊可能會在設定離線組態時，有寶貴的意見。

## 限制 {#limitations}

AEM Sites並非所有PWA功能都提供。 這些是一些顯著的限制。

* 使用者必須至少瀏覽一次頁面，才能離線快取頁面。
* 如果使用者未使用應用程式，則不會自動同步或更新頁面。
