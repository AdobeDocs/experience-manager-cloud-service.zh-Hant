---
title: 如何根據核心元件為最適化表單新增當地語系化支援？
description: 瞭解如何為最適化表單新增地區設定。
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 3%

---

# 為以核心元件為主的最適化表單新增地區設定 {#supporting-new-locales-for-adaptive-forms-localization}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| 基礎元件 | [按一下這裡](supporting-new-language-localization.md) |
| 核心元件 | 本文章 |

<span class="preview">從右至左語言支援功能可在早期採用者程式下取得。 您可以使用官方電子郵件 ID 寫信至 aem-forms-ea@adobe.com，以加入早期採用者計劃並要求存取該功能。</span>

AEM Forms提供英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定的立即可用支援。 您也可以新增對更多地區設定的支援，例如印地語(hi_IN)。 您也可以新增這些地區設定，以從右至左(RTL)語言呈現最適化Forms，例如阿拉伯文、波斯文和烏爾都文。

>[!VIDEO](https://video.tv.adobe.com/v/3433132/adaptive-forms-rtl--arabic-hebrew-farsi)

## 適用性和使用案例

### 保險

## AEM Forms是否支援多語言保險使用案例？

可以。AEM Forms支援多語言表單體驗，這對於跨地區和語言運作的保險公司很重要。

## AEM Forms如何決定最適化表單的地區設定？

瞭解AEM Forms如何選取語言環境來呈現最適化表單，對正確的本地化至關重要。 以下是選取程式的劃分：

### 優先順序型地區設定選擇

AEM Forms會優先使用下列方法來判斷最適化表單的地區設定：

1. **URL地區設定選擇器（[地區設定]）**：

   系統會使用[locale]選取器來排定URL中所指定地區設定的優先順序。 此格式允許快取以獲得更好的效能。

   格式： URL遵循以下格式： http:/[AEM Forms伺服器URL]/content/forms/af/[afName]。[locale].html？wcmmode=disabled。

   範例： https://[server]/content/forms/af/contact-us.hi.html會以北印度文轉譯表單。


1. **afAcceptLang要求引數**：

   若要覆寫使用者的瀏覽器地區設定，您可以在URL中使用`afAcceptLang`引數。

   範例： https://[server]/forms/af/survey.ca-fr.html？afAcceptLang=ca-fr強制表單以加拿大法文轉譯。

1. **使用者的瀏覽器地區設定（Accept-Language標題）**：

   如果未指定其他地區設定，AEM Forms會考慮使用`Accept-Language`標頭傳送的使用者瀏覽器地區設定。


### 遞補機制：


* 如果無法取得所要求地區設定的使用者端資源庫（新增新地區設定的程式，稍後將在本文中說明），AEM Forms會根據地區設定中的語言代碼檢查資源庫。

  範例：如果要求en_ZA （南非英文），但沒有en_ZA資料庫，則會使用en （英文） （如果可用）。

  如果找不到合適的使用者端資料庫，則會使用表單編寫語言的預設字典（大部分`en`）。

  在沒有任何地區設定資訊的情況下，最適化表單會以開發期間使用的原始語言顯示。


## 新增地區設定的先決條件

開始為最適化Forms新增地區設定之前，請確保您具備下列條件：

**軟體：**

* 純文字編輯器(IDE)：雖然任何純文字編輯器都可以運作，但[Microsoft Visual Studio Code](https://code.visualstudio.com/download)之類的整合式開發環境(IDE)可提供進階功能，讓編輯更輕鬆。

* Git：管理程式碼變更需要此版本控制系統。 如果您尚未安裝，請從[https://git-scm.com](https://git-scm.com)下載。


**程式碼存放庫：**

複製Adaptive Forms核心元件存放庫：您需要此存放庫中的使用者端資料庫才能新增地區設定。 複製存放庫：

1. 開啟命令列或終端機視窗。

1. 導覽至您電腦上儲存存放庫所需的位置（例如/adaptive-forms-core-components）。

1. 執行以下命令以複製存放庫：

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   這個命令會下載存放庫並在您的電腦上建立名為`aem-core-forms-components`的資料夾。 在本指南中，我們將此資料夾稱為`[Adaptive Forms Core Components repository]`。


## 新增地區 {#add-localization-support-for-non-supported-locales}

若要根據核心元件為最適化表單新增地區設定的支援，請執行下列步驟：

### 複製您的AEM as a Cloud Service Git存放庫

1. 開啟命令列，並選擇要儲存AEM as a Cloud Service存放庫的目錄，例如`/cloud-service-repository/`。

1. 執行以下命令以複製存放庫：

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   若要複製Git存放庫，您需要一些資訊：

   * **組織名稱**：可在Adobe Experience Manager as a Cloud Service (AEM as a Cloud Service)中識別您的團隊或專案。

   * **程式識別碼**：這會指定與存放庫關聯的程式。

   * **認證**：您需要使用者名稱和密碼（或個人存取權杖），才能安全地存取存放庫。

   **在哪裡可以找到此資訊？**

   如需尋找這些詳細資訊的逐步指示，請參閱Adobe Experience League文章&quot;[存取Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git)&quot;。

   **您的專案已就緒！**

   當命令成功完成時，您會看到在本機目錄中建立的新資料夾。 此資料夾以您的程式命名（例如，program-id）。 此資料夾包含從AEM as a Cloud Service Git存放庫下載的所有檔案和程式碼。

   在本指南中，我們將此資料夾稱為`[AEMaaCS project directory]`。


### 新增語言環境至指南本地化服務

1. 在編輯器中開啟存放庫資料夾。

   在編輯器中的![存放庫資料夾](/help/forms/assets/repository-folder-in-an-editor.png)

1. 找到`Guide Localization Service.cfg.json`檔案。 此檔案可控制您的AEM Forms應用程式支援的地區設定。 您可以編輯此檔案以新增語言環境。

   * **現有的檔案**：如果檔案已經存在，請在您的AEM Forms專案目錄中尋找它。 典型位置為：

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     將`<appid>`取代為您的專案特定應用程式識別碼。 您可以在`<appid>`檔案中找到您AEM專案的`archetype.properties`。

     ![Archetype屬性](/help/forms/assets/archetype-properties.png)

   * **新檔案**：如果檔案不存在，您必須在上述相同位置建立檔案。 請勿從此檔案複製貼上檔案名稱，而是手動輸入名稱。 檔案名稱`Guide Localization Service.cfg.json`包含空格。 這是刻意的操作，不是檔案中的拼寫錯誤。

     包含OOTB支援地區設定清單的範例檔案為：

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. 將您所需語言的地區設定代碼新增到檔案中。
   1. 使用[ISO 639-1程式碼清單](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes)來尋找代表您所需語言的雙字母程式碼。

   1. 將地區設定代碼包含到`Guide Localization Service.cfg.json`檔案中。 以下是一些範例：

      * 由左至右語言：
         * 英文（美國）：en-US
         * 西班牙文（西班牙）： es-ES
         * 法文（法國）：fr-FR
      * 由右至左語言：
         * 阿拉伯文（阿拉伯聯合大公國）： ar-ae
         * 希伯來文： he （或iw以供歷史參考）
         * 波斯文： fa

1. 進行變更後，請確定`Guide Localization Service.cfg.json`檔案的格式正確為有效的JSON檔案。 JSON格式設定錯誤可能會使其無法正常運作。 儲存檔案。



### 利用範例使用者端資料庫輕鬆進行地區設定

AEM Forms提供有用的範例使用者端程式庫`clientlib-it-custom-locale`，以簡化新增地區設定的程式。 此程式庫屬於GitHub上提供的[最適化Forms核心元件存放庫](https://github.com/adobe/aem-core-forms-components)的一部分。


開始之前，請確定您有[最適化Forms核心元件存放庫]的本機副本。 如果不適用，您就可以使用Git透過以下命令輕鬆複製：

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

此命令會將整個存放庫（包括clientlib-it-custom-locale資料庫）下載到您電腦上名為aem-core-forms-components的目錄。

本機電腦上的![Adaptive Forms核心元件存放庫目錄](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### 整合範例使用者端程式庫

現在，讓我們將`clientlib-it-custom-locale`資料庫合併到您的AEM as a Cloud Service [AEMaaCS專案目錄]：

1. 找到範例使用者端程式庫：

   在[最適化Forms核心元件存放庫]的本機復本中，導覽至下列路徑：

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. 複製並貼上程式庫：

   1. 複製`clientlib-it-custom-locale`資料夾。

      ![正在複製clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. 導覽至[AEMaaCS專案目錄]中的下列目錄：

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **重要**：將`<app-id>`取代為您應用程式的實際ID。

   1. 將複製的`clientlib-it-custom-locale`資料夾貼到此目錄中。

      ![貼上clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)

1. 更新`aemLangUrl`中的`languageinit.js`路徑

   1. 導覽至[AEMaaCS專案目錄]中的下列目錄：

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib/clientlib-it-custom-locale/js
      ```

   1. 在編輯器中開啟`languageinit.js`檔案。
   1. 在`languageinit.js`檔案中找到下列行：

      `const aemLangUrl = /etc.clientlibs/forms-core-components-it/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json;`

   1. 將`forms-core-components-it`取代為上一行中您的`<app-id>` （應用程式的實際ID）。

      `const aemLangUrl = '/etc.clientlibs/<app-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json';`

      ![language-init-file](/help/forms/assets/language-init-name-change.png)

>[!NOTE]
>  
> 如果您沒有將`forms-core-components-it`取代為您的專案名稱或`<app-id>`，則日期選擇器元件將無法翻譯。

### 建立新地區設定的檔案：

1. 瀏覽到地區設定目錄：

   在您的`[AEMaaCS project directory]`內，瀏覽至下列路徑：

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **重要**：將`<program-id>`取代為您的實際應用程式識別碼。

1. 找到範例英文檔案：

   AEM Forms在GitHub[上提供](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json)範例英文地區設定檔(.json)。

   英文檔案包含預設的參考字串集。 您的地區設定特定檔案應模擬英文檔案的結構。

   對於阿拉伯文、希伯來文和波斯文等語言，文字會從右至左(RTL)閱讀，而非像英文那樣從左至右(LTR)閱讀。 為確保您的表單在這些語言中正確顯示，我們建議使用我們的範例地區設定檔案作為指南。 這些檔案提供如何設定RTL語言文字、日期和其他元素格式的參考。 您可以找到下列的範例地區設定檔案：

   * [阿拉伯文](/help/forms/assets/ar-ae.json)
   * [希伯來文](/help/forms/assets/he.json)
   * [波斯文](/help/forms/assets/fa.json)

   運用這些範例檔案，您可以確保表單為使用RTL語言的使用者提供順暢的體驗。


1. 建立您的地區設定檔：

   1. 在`i18n`目錄中建立新的.json檔案。
   1. 使用您所需語言的適當地區設定代碼為檔案命名（例如，法文為fr-FR.json，阿拉伯文為ar-ae.json）。 此檔案的結構應該會反映英文地區設定檔案。


1. 結構和翻譯：

   1. 在文字編輯器中開啟新建立的檔案。

   1. 將英文值取代為您目標語言的對應翻譯。

   1. 當您完成字串的翻譯後，請儲存檔案。




### 新增地區設定支援至字典

此步驟僅適用於下列常用支援的語言環境以外的語言環境：英文(en)、德文(de)、西班牙文(es)、法文(fr)、義大利文(it)、巴西葡萄牙文(pt-br)、中文（簡體 — zh_cn）、中文（繁體 — zh_tw）、日文(ja)和韓文(ko_kr)。

1. 找到設定資料夾：

   導覽至[AEMaaCS專案目錄]中的下列目錄：

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. 建立必要的資料夾（如果遺失）：

   如果`etc`資料夾不存在於`jcr_root`資料夾中，請建立它。 在`etc`內，建立另一個名為`languages`的資料夾（如果遺失）。

1. 建立地區設定檔：

   在`languages`資料夾中，建立名為`.content.xml`的新檔案。 請勿從此檔案複製貼上檔案名稱，而是手動輸入名稱。

   ![建立名為`.content.xml`](etc-content-xml.png)的新檔案

   開啟此檔案並貼上下列內容，將[LOCALE_CODE]取代為實際的地區設定代碼（例如，阿拉伯文的ar-ae）。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   警告：請勿取代現有清單。 請改為將新的地區設定代碼附加在方括弧內（以逗號分隔），如下所示（以ar-ae為例）：

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. 在filter.xml中包含新資料夾：

   導覽至`/ui.content/src/main/content/meta-inf/vault/filter.xml`AEMaaCS專案目錄[中的]檔案。

   開啟檔案，並在結尾新增下列行：

   ```
   <filter root="/etc/languages"/>
   ```

   ![在`filter.xml`下的`/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)中新增建立的資料夾

1. 儲存檔案。

### 將新建立的地區設定部署到您的AEM環境

您現在都已設定為可搭配最適化Forms使用新的地區設定。 您可以

* 將AEM as a Cloud Service [AEMaaCS專案目錄]部署至您的本機開發環境，以在本機電腦上嘗試新的地區設定組態。 若要部署到您的本機開發環境：

   1. 確認您的本機開發環境已啟動且執行中。 如果您尚未設定本機開發環境，請參閱[為AEM Forms設定本機開發環境](/help/forms/setup-local-development-environment.md)的指南。

   1. 開啟終端機視窗或命令提示。

   1. 導覽至[AEMaaCS專案目錄]

   1. 執行以下命令：

      ```
      mvn -PautoInstallPackage clean install
      ```

* 將AEM as a Cloud Service [AEMaaCS專案目錄]部署至您的Cloud Service環境。 若要部署至您的Cloud Service環境：

   1. 提交您的變更：

      新增新的地區設定組態之後，請以描述地區設定新增的清晰Git訊息來認可您的變更（例如「新增對[地區設定名稱]的支援」）。

   1. 部署更新的程式碼：

      透過[現有的完整棧疊管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)觸發程式碼的部署。 這會透過新的地區設定支援自動建置和部署更新的程式碼。

      如果您尚未設定管道，請參閱[上的指南以瞭解如何設定AEM Forms as a Cloud Service的管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)。


## 預覽具有新增地區設定的最適化表單

以下步驟將引導您預覽具有新新增地區設定的最適化表單：

1. 登入您的AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**Forms** > **Forms和檔案**。
1. 選取最適化表單，然後按一下&#x200B;**新增字典**&#x200B;和&#x200B;**新增字典至翻譯專案**&#x200B;精靈出現。
1. 指定&#x200B;**專案標題**，並從&#x200B;**新增字典至翻譯專案**&#x200B;精靈的下拉式功能表中選取&#x200B;**目標語言**。
1. 按一下&#x200B;**完成**&#x200B;並執行已建立的翻譯專案。
1. 移至&#x200B;**Forms** > **Forms和檔案**。
1. 選取最適化表單，然後選擇&#x200B;**以HTML預覽**&#x200B;選項。
1. 將`&afAcceptLang=<locale-name>`附加至預覽URL並按回車鍵。 將`<locale-name>`取代為您的實際地區設定代碼。 最適化表單會以指定的地區設定顯示。

## 支援新本地化的最佳實務 {#best-practices}

* Adobe建議您在建立最適化表單之後建立翻譯專案。 這能簡化本地化程式。
* 當數值方塊和日期選擇器元件轉換為特定地區設定時，可能會出現格式問題。 為了緩解此問題，**語言**&#x200B;選項已納入[日期選擇器元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab)和[數值方塊元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab)的「設定」對話方塊中。


* 處理新欄位：

   * **機器翻譯**：如果使用機器翻譯，您必須重新建立字典，並在將新欄位新增至現有的最適化表單後[執行翻譯專案](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)。 初始翻譯專案後新增的新欄位仍維持未翻譯狀態。

   * **人工翻譯**：對於人工翻譯工作流程，請使用`[AEM Forms Server]/libs/cq/i18n/gui/translator.html`的UI匯出字典。 更新新欄位的字典並上傳修訂版本。


## 另請參閱 {#see-also}

{{see-also}}

* [產生最適化Forms的記錄檔案](/help/forms/generate-document-of-record-core-components.md)
* [新增自適應表單至 AEM Sites 頁面或體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

