---
title: 產生變化版本
description: 了解「產生變化版本」，可透過 AEM as a Cloud Service 內的各種編輯器進行存取
feature: Generate Variations
role: Admin, Architect, Developer, User
exl-id: d380ddd6-43f9-4bbf-8167-a6a472b9fc01
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '1417'
ht-degree: 100%

---

# 產生變化版本：與 AEM 編輯器整合 {#generate-variations-integrated-in-aem-editors}

如果您正在尋找一種將數位管道最佳化並加速內容建立的方法，可以使用與 AEM 編輯器整合的「產生變化版本」。

產生變化版本使用生成式人工智慧 (AI)，根據您的輸入建立內容變化版本。建立變化版本後，您可以在網站上使用這些內容，也可以使用 [Edge Delivery Services](/help/edge/overview.md) 的「[實驗](https://www.aem.live/docs/experimentation)」功能來衡量其是否成功。

這有助於在數分鐘內快速建立品牌內容，進而加快內容速度。也會因此提高新副本變體的轉換率。

您可以利用下列編輯器[存取「產生變化版本」](#access-generate-variations)([當編輯器設定完成後](#access-generate-variations))：

* [在 AEM Edge Delivery Services 的 Sidekick 中；用於文件型編寫](#access-aem-sidekick)
* [在通用編輯器中](#access-aem-universal-editor)
* [在內容片段編輯器中](#access-aem-content-fragment-editor)

>[!IMPORTANT]
>
>此頁面使用文件型編寫當成範例的基礎，但其原則也適用於其他編輯器。

>[!NOTE]
>
>在所有情況下，若要使用「產生變化版本」，您必須確保符合[存取權先決條件](#access-prerequisites)。

>[!NOTE]
>
>建議使用此版本，因為目前雖然[仍可直接存取產生變化版本](/help/generative-ai/generate-variations.md)的獨立版本，但未來將會棄用。

然後，您可以：

* [選取您想要處理的內容](#select-the-content)：從您的內容現有的區塊中選取
   * 所選取的區塊會決定要呈現出的內容和可用的操作
* [描述您想要的變更](#describe-the-changes-you-want)
* [替您的內容產生變化版本](#generate-copy)，然後[需要時採取進一步動作](#take-further-action-on-a-variation)
* [選取並使用變化版本](#use-a-generated-variation)
* 檢閱您的[歷史記錄](#history)
* 檢視您的[我的最愛](#favorites)

## 法律和使用備註 {#legal-usage-note}

<!--
Generative AI and Generate Variations for AEM are powerful tools – but **you** are responsible for use of the output.

Your inputs to the service should be tied to a context. This context can be your branding materials, website content, data, schemas for such data, templates, or other trusted documents.

You must evaluate the accuracy of any output as appropriate to your use case.

Before using Generate Variations you are recommended to read the [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).
-->

[「產生變化版本」的使用](#generative-action-usage)與生成動作的消耗緊密相關。

>[!NOTE]
>
>關於在 AEM 中產生變化版本的詳細資訊，請參閱[安全性情況說明書](https://www.adobe.com/tw/content/dam/cc/en/trust-center/ungated/whitepapers/experience-cloud/aem-sites-generate-variations-security-fact-sheet.pdf)。

## 概觀 {#overview}

當您開啟與編輯器整合的「產生變化版本」時，會看到具有三個索引標籤的浮動面板擴充功能。

![產生變化版本：文件型編寫概觀](assets/generate-variations-doc-based-overview.png)

* 編輯器：
   * 呈現編輯器中的內容流程。
   * 您可於此處選取要在&#x200B;**產生變化版本**&#x200B;中使用的內容區塊。
* **產生變化版本**：
   * 為具有三個索引標籤的浮動面板，可以根據需要重新定位
   * [產生](#get-started-with-generate-variations)：
      * 呈現[您所選取的內容](#select-the-content)。
      * 提供變更的範例&#x200B;**建議**。
      * 讓您能夠[描述您想要的變更](#describe-the-changes-you-want)。
      * 讓您能夠[產生](#generate-copy)新的變化版本。
      * 呈現所產生的變化版本。<!--, together with their [brand score](#the-brand-score).-->
      * [對變化版本採取進一步動作](#take-further-action-on-a-variation)。
      * [使用所產生的變化版本](#use-a-generated-variation)。
   * [歷史記錄](#history)：
      * 顯示您最近產生變化版本的歷史記錄。
   * [我的最愛](#favorites)：
      * 呈現您標記為「我的最愛」的先前版本。
   * **Adobe 生成式 AI 詞彙**：連結至 [Adobe Experience Cloud 生成式 AI 使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## 開始使用「產生變化版本」 {#get-started-with-generate-variations}

介面會引導您完成生成內容的過程。開啟介面後，第一步是選取您要使用的內容區塊。

### 選取內容 {#select-the-content}

從編輯器的主要內容流程中，選取您想要產生變化版本的內容。這項&#x200B;**選取結果**&#x200B;會顯示在「**產生**」索引標籤中。

### 描述您想要的變更 {#describe-the-changes-you-want}

若要產生變化版本，您需要描述您想要的變更。您可以從指定的&#x200B;**建議**&#x200B;中選取一項，或提供您自己的描述。

您也可以指定&#x200B;**修飾詞**&#x200B;來提供更多內容：

* **參照網頁**
提供 URL 以獲取更多內容。
* **上傳內容簡介**
更新內含內容簡介詳細資訊的 `.docx` 檔案 (10MB 或更小)。

### 產生副本 {#generate-copy}

描述完想要的變更後，選取「**產生**」，查看生成式 AI 的回應。

![產生變化版本：文件型產生副本](assets/generate-variations-doc-based-generate-copy.png)

<!--
### The Brand Score {#the-brand-score}

The brand score shows you how on-brand the generated variation is.
-->

### 對變化版本採取進一步動作 {#take-further-action-on-a-variation}

選取單一變化版本時，您可以進行以下動作：

* **編輯**
   * 您可以編輯所產生變化版本的文字。

      * 您可以在網頁中預覽更新。

   * 儲存您的變更供日後使用。
* **我的最愛**
   * 標記此變化版本供將來參考。
   * 被標記後便會顯示在「[我的最愛](#favorites)」索引標籤下。
* **AI 原理**
   * 為了提高透明度，此動作提供簡短描述，說明為什麼生成式 AI 會產生該特定變化版本。

### 使用所產生的變化版本 {#use-a-generated-variation}

若要使用生成式 AI 所產生的內容，您必須先選取該內容，然後「**匯出為 CSV**」。

匯出後，您可以在其他地方使用該內容 (例如為您的網站編寫內容時)。您也可以執行[實驗](https://www.aem.live/docs/experimentation)。

>[!NOTE]
>
>當透過 [AEM 通用編輯器](#access-aem-universal-editor)或者 [AEM 內容片段編輯器](#access-aem-content-fragment-editor)存取「產生變化版本」時，所選的已產生的內容會自動儲存至 AEM。

## 歷史記錄 {#history}

此索引標籤會顯示您選取「**產生**」之後的歷史活動。已新增一項「**歷史記錄**」項目。

若您稍後在主要流程中選取相同的內容，並開啟「**歷史記錄**」索引標籤，您將會看到該區塊產生的所有變化版本。

## 我的最愛 {#favorites}

檢閱內容後，您可以將選取的變化版本儲存為我的最愛。

儲存後，變化版本會顯示在「**我的最愛**」之下。「我的最愛」會永久保留 (直到您將其&#x200B;**移除最愛**，或是清除瀏覽器快取)。

* 您可以針對項目進行&#x200B;**編輯**、**移除最愛**，或者顯示 **AI 原理**。
* 選取變化版本後，您亦可以「**匯出為 CSV**」。

## 生成式動作的使用 {#generative-action-usage}

使用量管理取決於所採取的動作：

* 產生變化版本

  產生一個副本變體就等於一次生成式動作。身為客戶，您的 AEM 授權已附帶一定數量的生成式動作。基本權益次數使用完畢後，您可以購買額外的動作次數。

  >[!NOTE]
  >
  >如需有關基本權益的其他詳細資訊，請參閱 [Adobe Experience Manager：Cloud Service | 產品說明](https://helpx.adobe.com/tw/legal/product-descriptions/aem-cloud-service.html)；如果您想購買更多生成式動作，請與您的客戶團隊聯絡。

## 存取產生變化版本 {#access-generate-variations}

滿足先決條件後，您可以從 AEM as a Cloud Service 或 Edge Delivery Services 的 Sidekick 存取「產生變化版本」。

### 存取的先決條件 {#access-prerequisites}

若要使用「產生變化版本」，必須確保符合先決條件：

* [存取包含 Edge Delivery Services 的 Experience Manager as a Cloud Service](#access-to-aemaacs-with-edge-delivery-services)

#### 存取包含 Edge Delivery Services 的 Experience Manager as a Cloud Service{#access-to-aemaacs-with-edge-delivery-services}

需要存取「產生變化版本」的使用者，必須有權使用包含 Edge Delivery Services 的 Experience Manager as a Cloud Service 環境。

>[!NOTE]
>
>如果您的 AEM Sites as a Cloud Service 合約未包含 Edge Delivery Services，就需要簽署新合約才能獲得存取權。
>
>您應與客戶團隊聯絡，討論如何移轉至包含 Edge Delivery Services 的 AEM Sites as a Cloud Service。

若要授予存取權給特定使用者，請將他們的使用者帳戶指派至相應的產品設定檔。如需其他詳細資訊，請參閱[指派 AEM 產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md)。

### 適用於文件型編寫的「從 AEM Sidekick 存取」 {#access-aem-sidekick}

「從 AEM Sidekick 存取」適用於[文件型編寫](https://www.aem.live/docs/aem-authoring)。

在您可以從 (Edge Delivery Services 的) Sidekick 存取「產生變化版本」之前，需要進行一些設定。

>[!NOTE]
>
>請參閱文件：[安裝 AEM Sidekick](https://www.aem.live/docs/sidekick-extension)，以了解如何安裝和設定 Sidekick。

若要在 (Edge Delivery Services 的) Sidekick 中使用「產生變化版本」，請在 Edge Delivery Services 專案中納入下列設定。

1. 於以下位址啟用我們的應用程式：

   * `tools/sidekick/config.json`

   必須將其合併到您現有的設定中，然後進行部署。

   例如：

   ```prompt
   {
     "plugins": [
       {
         "id": "aem-genai-variations",
         "titleI18n": {
           "en": "Generate with AI"
         },
         "environments": [
           "preview"
         ],
         "includePaths": [
           "**.docx**"
         ],
         "event": "aem-genai-variations-sidekick"
       }
     ]
   }
   ```

1. 建立：

   * `/tools/sidekick/aem-genai-variations.js`

   您必須使用以下內容建立這個檔案：

   ```prompt
   (function () {
     let isAEMGenAIVariationsAppLoaded = false;
     function loadAEMGenAIVariationsApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/aem-sites-genai-aem-genai-variations-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMGenAIVariationsAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMGenAIVariationsApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMGenAIVariationsAppLoaded) {
         loadAEMGenAIVariationsApp();
       }
     }
   
     // The code snippet for the Sidekick V1 extension, https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo?hl=en
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       // sidekick already loaded
       sidekick.addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
     } else {
       // wait for sidekick to be loaded
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
       }, { once: true });
     }
   
     // The code snippet for the Sidekick V2 extension, https://chromewebstore.google.com/detail/aem-sidekick/igkmdomcgoebiipaifhmpfjhbjccggml?hl=en
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       // sidekick already loaded
       sidekickV2.addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
     } else {
       // wait for sidekick to be loaded
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. 更新：

   * `/scripts/scripts.js`

   必須更新此內容，在 `loadLazy()` 函數中包含以下陳述式：

   ```prompt
     import('../tools/sidekick/aem-genai-variations.js');
   ```

   這能確保 `/tools/sidekick/aem-genai-variations.js` 是作為延遲載入過程的一部分載入。

   ![產生變化版本：延遲載入器](assets/generate-variations-sidekick-lazyloader.png)

1. 然後，您可能需要確保使用者能夠[存取包含 Edge Delivery Services 的 Experience Manager as a Cloud Service](#access-to-aemaacs-with-edge-delivery-services)。

1. 接著，您可以從 Sidekick 工具列中選取「**以 AI 產生**」來存取該功能：

   ![產生變化版本：從 AEM Sidekick 存取](assets/generate-variations-doc-based-sidekick.png)

### 從 AEM 通用編輯器存取 {#access-aem-universal-editor}

以擴充功能的形式，實施從 [AEM 通用編輯器](/help/sites-cloud/authoring/universal-editor/authoring.md)存取的功能。

* 如需有關如何從通用編輯器存取「產生變化版本」的詳細資訊，請參閱文件[使用通用編輯器編寫內容。](/help/sites-cloud/authoring/universal-editor/authoring.md#generate-variations)
* 有關如何啟用擴充功能的詳細資訊，請參閱文件 [AEM Experience Manager 中的 Extension Manager。](https://developer.adobe.com/uix/docs/extension-manager/)

### 從 AEM 內容片段編輯器存取 {#access-aem-content-fragment-editor}

「從 [AEM 內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)存取」需以擴充功能的形式實施。如需其他詳細資訊，請參閱「[AEM Experience Manager 中的 Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)」。

## 更多資訊 {#further-information}

如需詳細資訊，您也可以閱讀：

* [GitHub 上的 GenAI 產生變化版本](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Edge Delivery Services 實驗](https://www.aem.live/docs/experimentation)
* [Experience Cloud 產品中的生成式 AI](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/features/generative-ai)

   * [Experience Cloud 產品中的生成式 AI - Adobe Experience Manager](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/features/generative-ai#aem)

* [Experience Cloud 上的產生變化版本登陸頁面](https://experience.adobe.com/solutions/aem-sites-genai-aem-genai-variations-mfe/static-assets/resources/ga.html)

* [AEM as a Cloud Service 中的生成式服務](/help/generative-ai/generative-ai-in-aem.md)

## 發行歷史記錄 {#release-history}

有關目前和先前版本的詳細資訊，請參閱[產生變化版本的發行說明](/help/generative-ai/release-notes-generate-variations.md)
