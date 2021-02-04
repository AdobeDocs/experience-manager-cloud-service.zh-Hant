---
title: 啟用漸進式網頁應用程式功能
description: AEM Sites可讓內容作者透過簡單的設定，而非編碼，將漸進式網頁應用程式功能啟用至任何網站。
translation-type: tm+mt
source-git-commit: ba014bb90b1cb08630455b3ac72895272ae8ed5b
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

這些是作者需要與開發團隊協調的技術步驟。 每個站點只需執行一次這些步驟。

### 調整元件{#adjust-components}

您的元件需要包括支援PWA功能的[清單檔案](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服務工作程式](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)。

為此，開發人員需要將以下連結添加到頁面元件的`customheaderlibs.html`檔案。

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

開發人員還需要將以下連結添加到頁面元件的`customfooterlibs.html`檔案。

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
>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)的未來版本將自動包含這些功能。 但是，如果使用定制元件而不是核心元件，則始終需要這些調整。

### 調整調度程式{#adjust-dispatcher}

PWA功能生成並使用`/content/<sitename>/manifest.webmanifest`檔案。 預設情況下，調度程式](/help/implementing/dispatcher/overview.md)不公開此類檔案。 [要公開這些檔案，開發人員必須將以下配置添加到您的站點項目。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>[AEM項目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing)的未來版本將包括此配置。

## 為站點{#enabling-pwa-for-your-site}啟用PWA

滿足[先決條件](#prerequisites)後，內容作者很容易將PWA功能啟用到站點。 以下是如何執行此操作的基本概要。 各個選項在[詳細選項一節中詳細介紹。](#detailed-options)

1. 登錄AEM。
1. 在主菜單中，點擊或按一下&#x200B;**導航** -> **站點**。
1. 選擇您的站點項目，點擊或按一下「屬性&#x200B;**](/help/sites-cloud/authoring/fundamentals/page-properties.md)」或使用熱鍵`p`。[**
1. 選擇&#x200B;**漸進式Web應用**&#x200B;頁籤並配置適用的屬性。 您至少要：
   1. 選擇「啟用PWA **」選項。**
   1. 定義&#x200B;**啟動URL**。

      ![啟用 PWA](../assets/pwa-enable.png)

   1. 將512x512 png表徵圖上載到DAM，並將其作為應用的表徵圖引用。

      ![定義PWA表徵圖](../assets/pwa-icon.png)

   1. 配置希望服務工作人員離線的路徑。 典型路徑為：
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任何第三方字型引用
      * `/etc/clientlibs/<sitename>`

      ![定義PWA離線路徑](../assets/pwa-offline.png)


1. 點擊或按一下「保存並關閉&#x200B;**」。**

您的站點現在已配置，您可以[將其作為本地應用安裝。](#using-pwa-enabled-site)

## 使用啟用PWA的站點{#using-pwa-enabled-site}

現在，您已將您的站點配置為支援PWA，您可以自己體驗它。[](#enabling-pwa-for-your-site)

1. 在[支援的瀏覽器中訪問站點。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 您將在瀏覽器的地址欄中看到一個`+`表徵圖，表明該站點可以作為本地應用安裝。
   * 根據瀏覽器的不同，它還可能顯示一條通知（如橫幅或對話框），指示它可以作為本地應用進行安裝。
1. 安裝應用。
1. 應用將安裝在設備的主螢幕上。
1. 開啟應用，瀏覽一下，然後看到頁面離線可用。

## 詳細選項{#detailed-options}

以下部分提供了有關[為PWA配置站點時可用選項的詳細資訊。](#enabling-pwa-for-your-site)

### 配置可安裝體驗{#configure-installable-experience}

這些設定可讓您的網站在訪客的首頁畫面上安裝，並離線使用，讓其行為與原生應用程式相同。

* **啟用PWA**  — 這是為站點啟用PWA的主切換。
* **啟動URL**  — 這是用戶 [載入本](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 地安裝的應用時將開啟的首選啟動URL。
   * 這可以是內容結構中的任何路徑。
   * 這不必是根目錄，通常是應用程式的專用歡迎頁。
   * 如果此URL是相對的，則清單URL將用作解析該URL的基URL。
   * 如果為空，則該功能將使用我們應用從中安裝的網頁地址。
   * 建議設定值。
* **顯示模式**  — 啟用PWA的應用仍是通過瀏覽器提供的AEM站點。[這些顯](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 示選項定義瀏覽器應如何隱藏或以其他方式呈現給本地設備上的用戶。
   * **獨立**  — 瀏覽器完全隱藏在用戶面前，它看起來像本地應用。這是預設值。
      * 使用此選項，應用程式導航必須完全通過您的內容進行，而無需使用瀏覽器的導航控制項，即可使用站點頁面上的連結和元件。
   * **瀏覽器**  — 瀏覽器在訪問站點時會像通常一樣顯示。
   * **最小UI**  — 瀏覽器大多隱藏，就像本機應用程式一樣，但基本的導航控制項會暴露。
   * **全屏**  — 瀏覽器完全隱藏，就像本機應用一樣，但以全屏模式呈現。
      * 使用此選項，應用程式導航必須完全通過您的內容進行，而無需使用瀏覽器的導航控制項，即可使用站點頁面上的連結和元件。
* **螢幕方向**  — 作為本地應用，PWA需要知道如何處理設 [備方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Any**  — 應用根據用戶設備的方向進行調整。這是預設值。
   * **縱向**  — 這會強制應用以縱向佈局開啟，而不管用戶設備的方向如何。
   * **橫向**  — 這會強制應用程式以橫向佈局開啟，而不管用戶設備的方向如何。
* **主題顏色**  — 這定義 [了應用的](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 顏色，它影響本地用戶的作業系統顯示本機UI工具欄和導航控制項的方式。根據瀏覽器的不同，它可能會影響其他應用程式演示文稿元素。
   * 使用顏色井彈出窗口選擇顏色。
   * 顏色也可以由十六進位或RGB值定義。
* **背景顏色**  — 這定義 [了應用的背景顏](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 色，該顏色顯示為應用載入。
   * 使用顏色井彈出窗口選擇顏色。
   * 顏色也可以由十六進位或RGB值定義。
   * 某些瀏覽器[自動從應用名稱、背景顏色和表徵圖生成閃屏](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)。
* **表徵圖**  — 這 [定](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 義了表示用戶設備上應用的表徵圖。
   * 該表徵圖必須是大小為512x512像素的png檔案。
   * 表徵圖必須儲存在DAM中。](/help/assets/overview.md)[

### 快取管理（高級）{#offline-configuration}

這些設定使此站點的部分部分離線可用，並可在訪問者設備上本地使用。 這可讓您控制網頁應用程式的快取，以最佳化網路要求並支援離線體驗。

* **快取策略和內容刷新頻率**  — 此設定定義PWA的快取模型。
   * **適當** - [此](https://web.dev/stale-while-revalidate/) 設定對於大多數站點來說是情況，並且是預設值。
      * 通過此設定，用戶首先查看的內容將從快取中載入，當用戶使用該內容時，將重新驗證快取中的其餘內容。
   * **頻繁**  — 對於像拍賣行這樣需要快速更新的網站來說，情況就是如此。
      * 使用此設定，應用將首先通過網路查找最新內容，如果不可用，則返回本地快取。
   * **很少**  — 對於幾乎是靜態的站點（如參考頁），情況是這樣。
      * 使用此設定，應用程式將首先查找快取中的內容，如果不可用，將返回網路以檢索內容。
* **檔案預快取**  — 在安裝服務工作程式時和使用服務工作程式之前，AEM上承載的這些檔案將保存到本地瀏覽器快取中。這確保Web應用在離線時可以完全正常工作。
* **路徑包含**  — 根據配置的快取策略和內容刷新頻率，截取對已定義路徑的網路請求並返回快取內容 ****。
* **快取排除**  — 無論檔案預快取和路徑包含項下的設定如何，這些文 **件都不** 會被 **快取**。

>[!TIP]
>
>您的開發人員團隊可能在如何設定離線配置方面有寶貴的資訊。

## 限制 {#limitations}

並非所有PWA功能都可用於AEM站點。 這些是一些顯著的局限。

* 用戶必須至少瀏覽一次頁面，才能離線快取該頁面。
* 如果用戶未使用該應用，則不會自動同步或更新頁面。
