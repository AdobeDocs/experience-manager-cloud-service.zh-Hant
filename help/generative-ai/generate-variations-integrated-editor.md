---
title: 產生變化版本
description: 瞭解如何從AEM as a Cloud Service中的各種編輯器存取產生變數
feature: Generate Variations
role: Admin, Architect, Developer, User
source-git-commit: 257fcd8df8bf216deec1fe96e64dd38e52f3ebe1
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 34%

---


# 產生變數 — 整合在AEM編輯器中 {#generate-variations-integrated-in-aem-editors}

如果您正在尋找最佳化數位頻道和加速內容建立的方法，您可以使用整合到AEM編輯器中的產生變數。

「產生變數」會使用產生式人工智慧(AI)，根據您的輸入建立內容變數。 建立變化版本後，您可以在網站上使用這些內容，也可以使用 [Edge Delivery Services](/help/edge/overview.md) 的「[實驗](https://www.aem.live/docs/experimentation)」功能來衡量其是否成功。

這可在數分鐘內快速建立品牌內容，加速內容速度。 這進而有助於改善新複製變體的轉換。

您可以從下列編輯器[存取產生變數](#access-generate-variations) （[設定變數後](#access-generate-variations)）：

* [在AEM Edge Delivery Services的Sidekick中；針對檔案式撰寫](#access-aem-sidekick)
* [在通用編輯器內](#access-aem-universal-editor)
* [在內容片段編輯器中](#access-aem-content-fragment-editor)

>[!IMPORTANT]
>
>本頁使用檔案式製作作為範例的基礎，但原則適用於其他編輯器。

>[!NOTE]
>
>在所有情況下，若要使用「產生變化版本」，您必須確保符合[存取權先決條件](#access-prerequisites)。

>[!NOTE]
>
>仍可直接存取[ Generate Variations的獨立版本](/help/generative-ai/generate-variations.md)。

然後，您可以：

* [從內容的現有區塊中選取您要使用的內容](#select-the-content)
   * 選取的區塊會指示顯示的內容和可用的動作
* [說明您想要的變更](#describe-the-changes-you-want)
* [產生您內容的變體](#generate-copy)，然後[如有需要，採取進一步的動作](#take-further-action-on-a-variation)
* [選取並使用變數](#use-a-generated-variation)
* 檢閱您的[歷程記錄](#history)
* 檢視您的[我的最愛](#favorites)

## 法律和使用備註 {#legal-usage-note}

<!--
Generative AI and Generate Variations for AEM are powerful tools – but **you** are responsible for use of the output.

Your inputs to the service should be tied to a context. This context can be your branding materials, website content, data, schemas for such data, templates, or other trusted documents.

You must evaluate the accuracy of any output as appropriate to your use case.

Before using Generate Variations you are recommended to read the [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).
-->

[「產生變化版本」的使用](#generative-action-usage)與生成動作的消耗緊密相關。

## 概觀 {#overview}

當您開啟整合至編輯器的「產生變數」時，您會看到擴充功能為一個包含三個索引標籤的浮動面板。

![產生變化 — 檔案式撰寫概述](assets/generate-variations-doc-based-overview.png)

* 編輯器：
   * 這會在編輯器中顯示內容流程。
   * 您可以在此處選取要用於&#x200B;**產生變化**&#x200B;的內容區塊。
* **產生變數**：
   * 是一個具有三個標籤的浮動面板，可以視需要重新定位
   * [產生](#get-started-with-generate-variations)：
      * 顯示您已選取的[內容](#select-the-content)。
      * 提供變更的範例&#x200B;**建議**。
      * 允許您[描述您想要的變更](#describe-the-changes-you-want)。
      * 可讓您[產生](#generate-copy)個新變數。
      * 顯示產生的變數。<!--, together with their [brand score](#the-brand-score).-->
      * [針對變數](#take-further-action-on-a-variation)採取進一步的動作。
      * [使用產生的變數](#use-a-generated-variation)。
   * [歷程記錄](#history)：
      * 顯示您最近的世代記錄。
   * [我的最愛](#favorites)：
      * 顯示您標籤為我的最愛的前一代結果。
   * **Adobe Generative AI辭彙**： [Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)的連結。

## 開始使用產生變數 {#get-started-with-generate-variations}

介面會引導您完成生成內容的過程。開啟介面後，第一步是選取您要使用的內容區塊。

### 選取內容 {#select-the-content}

從編輯器的主要內容流程中，選取您要產生變數的內容。 此&#x200B;**選取專案**&#x200B;將顯示在&#x200B;**產生**&#x200B;索引標籤中。

### 說明您想要的變更 {#describe-the-changes-you-want}

若要產生內容的變體，您需要說明您想要的變更。 您可以選取其中一個給定的&#x200B;**建議**，或提供您自己的說明。

您也可以指定&#x200B;**修飾元**&#x200B;以提供更多內容：

* **參考網頁**
提供一個URL以取得更多內容。
* **上傳內容簡介**
更新包含內容摘要（10MB或更少）詳細資料的`.docx`檔案。

### 產生副本 {#generate-copy}

說明您要的變更後，選取&#x200B;**產生**&#x200B;以檢視產生AI的回應。

![產生變化 — 以檔案為基礎產生復本](assets/generate-variations-doc-based-generate-copy.png)

<!--
### The Brand Score {#the-brand-score}

The brand score shows you how on-brand the generated variation is.
-->

### 對變數採取進一步動作 {#take-further-action-on-a-variation}

選取單一變數時，您可以使用下列動作：

* **編輯**
   * 您可以編輯產生之變數的文字。

      * 您可以在網頁中預覽您的更新。

   * 儲存變更以供稍後使用。
* **我的最愛**
   * 標幟此變數以供日後參考。
   * 標幟後，它將顯示在[我的最愛](#favorites)標籤下。
* **AI基本原則**
   * 為了增加透明度，這會簡要說明為何產生AI會產生該特定變數。

### 使用產生的變數 {#use-a-generated-variation}

若要使用產生AI所產生的內容，您必須先選取並&#x200B;**匯出至CSV**。

匯出後，您可以在其他位置使用內容；例如，為您的網站編寫內容時。 您也可以執行[實驗](https://www.aem.live/docs/experimentation)。

>[!NOTE]
>
>從[AEM通用編輯器](#access-aem-universal-editor)或[AEM內容片段編輯器](#access-aem-content-fragment-editor)存取產生變數時，系統會自動將選取的產生內容儲存至AEM。

## 記錄 {#history}

此索引標籤顯示您過去的活動，如同您選取&#x200B;**產生**&#x200B;之後。 已新增&#x200B;**History**&#x200B;專案。

如果您稍後在主要流程中選取相同的內容，並開啟&#x200B;**歷程記錄**&#x200B;標籤，則會看到該區塊產生的所有變數。

## 我的最愛 {#favorites}

檢閱內容後，您可以將選取的變化版本儲存為我的最愛。

儲存後，它們會顯示在&#x200B;**我的最愛**&#x200B;下。 我的最愛會持續存在（直到您&#x200B;**取消我的最愛**&#x200B;它們，或清除瀏覽器快取）。

* 您可以&#x200B;**編輯**，**取消收藏**，或顯示專案的&#x200B;**AI基本原則**。
* 選取變化後，您也可以&#x200B;**匯出至CSV**。

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

* [存取具有 Edge Delivery Services 的 Experience Manager as a Cloud Service](#access-to-aemaacs-with-edge-delivery-services)

#### 存取具有 Edge Delivery Services 的 Experience Manager as a Cloud Service{#access-to-aemaacs-with-edge-delivery-services}

需要存取「產生變化版本」的使用者，必須有權使用具有 Edge Delivery Services 的 Experience Manager as a Cloud Service 環境。

>[!NOTE]
>
>如果您的 AEM Sites as a Cloud Service 合約未包含 Edge Delivery Services，就需要簽署新合約才能獲得存取權。
>
>您應與客戶團隊聯絡，討論如何移轉至具有 Edge Delivery Services 的 AEM Sites as a Cloud Service。

若要授予存取權給特定使用者，請將他們的使用者帳戶指派至相應的產品設定檔。如需其他詳細資訊，請參閱[指派 AEM 產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md)。

### 從AEM Sidekick存取檔案式編寫 {#access-aem-sidekick}

來自AEM Sidekick的存取權用於[檔案式製作](/help/edge/wysiwyg-authoring/authoring.md)。

在您可以從 (Edge Delivery Services 的) Sidekick 存取「產生變化版本」之前，需要進行一些設定。

>[!NOTE]
>
>請參閱文件：[安裝 AEM Sidekick](https://www.aem.live/docs/sidekick-extension)，以了解如何安裝和設定 Sidekick。

若要在Edge Delivery Services的Sidekick中使用「產生變數」，請在您的Edge Delivery Services專案中包含下列設定。

1. 啟用應用程式於：

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

   您必須使用下列內容建立此檔案：

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

   必須更新此專案，才能在`loadLazy()`函式中包含下列陳述式：

   ```prompt
     import('../tools/sidekick/aem-genai-variations.js');
   ```

   這可確保`/tools/sidekick/aem-genai-variations.js`載入為延遲載入程式的一部分。

   ![產生變化 — 延遲載入器](assets/generate-variations-sidekick-lazyloader.png)

1. 然後，您可能需要確保使用者能夠[存取具有 Edge Delivery Services 的 Experience Manager as a Cloud Service](#access-to-aemaacs-with-edge-delivery-services)。

1. 然後，您可以存取該功能，方法是從Sidekick的工具列選取&#x200B;**使用AI產生**：

   ![產生變化版本 - 從 AEM Sidekick 存取](assets/generate-variations-doc-based-sidekick.png)

### 從AEM Universal Editor存取 {#access-aem-universal-editor}

從[AEM Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md)的存取已實作為擴充功能。 如需詳細資訊，請參閱AEM Experience Manager](https://developer.adobe.com/uix/docs/extension-manager/)中的[Extension Manager 。

### 從AEM內容片段編輯器的存取權 {#access-aem-content-fragment-editor}

從[AEM內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)的存取已實作為擴充功能。 如需詳細資訊，請參閱AEM Experience Manager](https://developer.adobe.com/uix/docs/extension-manager/)中的[Extension Manager 。

## 更多資訊 {#further-information}

如需詳細資訊，您也可以閱讀：

* [GitHub 上的 GenAI 產生變化版本](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Edge Delivery Services 實驗](https://www.aem.live/docs/experimentation)

## 發行歷史記錄 {#release-history}

有關目前和先前版本的詳細資訊，請參閱[產生變化版本的發行說明](/help/generative-ai/release-notes-generate-variations.md)
