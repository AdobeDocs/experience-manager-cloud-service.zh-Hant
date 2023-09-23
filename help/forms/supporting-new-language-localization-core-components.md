---
title: 如何根據核心元件為最適化表單新增地區設定的支援？
description: 瞭解如何為最適化表單新增地區設定。
source-git-commit: 0d2e353208e4e59296d551ca5270be06e574f7df
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 4%

---


# 根據核心元件為最適化Forms新增地區設定 {#supporting-new-locales-for-adaptive-forms-localization}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| Foundation 元件 | [按一下這裡](supporting-new-language-localization.md) |
| 核心元件 | 本文章 |

AEM Forms提供英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定的立即可用支援。 您也可以新增對更多地區設定的支援，例如印地語(hi_IN)。

## 如何為最適化表單選取地區設定？

開始為最適化Forms新增地區設定之前，請先瞭解如何為最適化表單選取地區設定。 有兩種方法可以在最適化表單呈現時識別及選取其地區設定：

* **使用 `locale` URL中的選取器**：呈現最適化表單時，系統會透過檢查 [地區設定] 最適化表單URL中的選取器。 URL格式如下： http:/[AEM Forms伺服器URL]/content/forms/af/[afName].[地區設定].html？wcmmode=disabled. 使用 [地區設定] 選擇器允許快取最適化表單。 例如，URL `www.example.com/content/forms/af/contact-us.hi.html?wcmmmode=disabled` 以印地語呈現表單。

* 正在以下列順序擷取引數：

   * **使用 `afAcceptLang`請求引數**：若要覆寫使用者的瀏覽器地區設定，您可以傳遞afAcceptLang請求引數。 例如， `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr` URL強制AEM Forms伺服器以加拿大法文地區設定轉譯表單。

   * **使用瀏覽器地區設定（Accept-Language標頭）**：系統也會考量使用者的瀏覽器地區設定，該設定是使用於請求中指定的 `Accept-Language` 標頭。

  如果無法取得所要求地區設定的使用者端程式庫（本文稍後會介紹建立及使用程式庫的程式），則系統會檢查地區設定內是否有語言程式碼的使用者端程式庫。 例如，如果要求的地區設定為 `en_ZA` （南非英文），而且沒有客戶資料庫 `en_ZA`，則最適化表單會使用en （英文）的使用者端資料庫（如有）。 如果兩者都找不到，則最適化表單會為以下專案訴諸字典： `en` 地區設定。

  地區設定一經識別，最適化表單就會選取對應的表單特定字典。 如果找不到所要求地區設定的字典，則預設為使用製作最適化表單時所用語言的字典。

  如果沒有可用的地區設定資訊，最適化表單會以其原始語言顯示，原始語言是表單開發期間使用的語言


## 先決條件 {#prerequistes}

開始新增地區設定之前：

* 安裝純文字編輯器(IDE)以更輕鬆進行編輯。 本檔案中的範例是根據 [Microsoft® Visual Studio Code](https://code.visualstudio.com/download).
* 安裝版本 [Git](https://git-scm.com)，若您的電腦沒有提供。
* 原地複製 [最適化Forms核心元件](https://github.com/adobe/aem-core-forms-components) 存放庫。 複製存放庫：
   1. 開啟命令列或終端機視窗，並導覽至存放庫的位置。 例如 `/adaptive-forms-core-components`
   1. 執行以下命令以複製存放庫：

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  存放庫包含新增地區設定所需的使用者端資料庫。

  成功執行命令時，存放庫會複製到 `aem-core-forms-components` 資料夾。 在文章的其餘部分，資料夾將改名為， [最適化Forms核心元件存放庫].


## 新增地區 {#add-localization-support-for-non-supported-locales}

若要新增新地區設定的支援，請遵循下列步驟：

![新增地區設定至存放庫](add-a-locale-adaptive-form-core-components.png)

### 1.複製您的AEMas a Cloud ServiceGit存放庫 {#clone-the-repository}

1. 開啟命令列，然後選擇用來儲存AEM Formsas a Cloud Service存放庫的目錄，例如 `/cloud-service-repository/`.

1. 執行以下命令以複製存放庫：

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   取代 `<my-org>` 和 `<my-program>` 以上的URL中，加入您的組織名稱和方案名稱。 如需詳細指示，以取得組織名稱、計畫名稱或Git存放庫的完整路徑以及複製存放庫所需的認證，請參閱 [存取Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 文章。

   成功完成命令後，資料夾 `<my-program>` 「 」已建立。 其中包含從Git存放庫複製的內容。 在文章的其餘部分，資料夾將改稱為 `[AEM Forms as a Cloud Service Git repository]`.


### 2.新增語言環境至「本地化指南」服務 {#add-a-locale-to-the-guide-localization-service}

1. 以純文字編輯器開啟上一節複製的存放庫資料夾。
1. 導覽至 `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` 檔案夾。您可找到 `<appid>` 在 `archetype.properties` 專案的檔案。
1. 開啟 `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` 檔案進行編輯。 如果檔案不存在，請建立檔案。 具有支援地區設定的範例檔案如下所示：

   ![範例指南Localization Service.cfg.json](locales.png)

1. 新增 [語言的區域設定代碼](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 例如，您想要新增的北印度語新增「hi」。
1. 儲存並關閉檔案。

### 3.建立使用者端資料庫以新增地區設定

AEM Forms提供範例使用者端資料庫，協助您輕鬆新增地區設定。 您可以下載並新增 `clientlib-it-custom-locale` 來自的使用者端資源庫 [最適化Forms核心元件存放庫] 在GitHub上前往您的Formsas a Cloud Service存放庫。 若要新增使用者端程式庫，請執行下列步驟：

1. 開啟您的 [最適化Forms核心元件存放庫] 在純文字編輯器中。 如果您沒有複製存放庫，請參閱 [必要條件](#prerequistes) 以取得複製存放庫的指示。
1. 導覽至 `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` 目錄。
1. 複製 `clientlib-it-custom-locale` 目錄。
1. 瀏覽至 `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` 並貼上 `clientlib-it-custom-locale` 目錄。


### 4.建立特定地區設定的檔案 {#locale-specific-file}

1. 瀏覽到 `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. 找到 [GitHub上的英文地區設定.json檔案](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json)，其中包含產品所包含的最新預設字串集。
1. 為您的特定地區設定建立.json檔案。
1. 在新建立的.json檔案中，映象英文地區設定檔案的結構。
1. 將.json檔案中的英文字串取代為您的語言對應的當地語系化字串。
1. 儲存並關閉檔案。


### 5.新增地區設定支援至字典 {#add-locale-support-for-the-dictionary}

只有在 `<locale>` 您新增的內容不屬於 `en`， `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`.

1. 導覽至 `[AEM Forms as a Cloud Service Git repository]/ui.content/src/main/content/jcr_root/etc/` 檔案夾。

1. 建立 `etc` 下的資料夾 `jcr_root` 資料夾（如果尚未存在）。

1. 建立資料夾 `languages` 在 `etc` 資料夾（如果尚未存在）。

   ![替代文字](etc-content-xml.png)

1. 建立 `.content.xml` 下的檔案 `languages` 資料夾。 將下列內容新增至檔案：

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr]"/>
   ```

1. 將地區設定代碼新增至 `languages` 屬性。 例如，在下列範常式式碼中新增了印地語的hi。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

1. 將新建立的資料夾新增至 `filter.xml` 在 `/ui.content/src/main/content/meta-inf/vault/filter.xml` 作為：

   ```
   <filter root="/etc/languages"/>
   ```

   ![將新建立的資料夾新增至 `filter.xml` 在 `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

### 6.提交變更並部署管道 {#commit-changes-in-repo-deploy-pipeline}

在新增地區設定後，將變更提交到GIT存放庫。 使用完整棧疊管道部署您的計畫碼。 瞭解 [如何設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 以新增地區設定支援。

管道執行成功後，新新增的地區設定即可使用。

## 預覽具有新增地區設定的最適化表單 {#use-added-locale-in-af}

執行以下步驟，以預覽具有新新增地區設定的最適化：

1. 登入您的AEM Formsas a Cloud Service執行個體。
1. 前往 **Forms** >  **Forms與檔案**.
1. 選取最適化表單並按一下 **新增字典** 和 **新增字典至翻譯專案** 精靈出現。
1. 指定 **專案標題** 並選取 **目標語言** 從「 」的下拉式功能表 **新增字典至翻譯專案** 精靈。
1. 按一下 **完成** 並執行已建立的翻譯專案。
1. 選取最適化表單並按一下 **以HTML預覽**.
1. 新增 `&afAcceptLang=<locale-name>` 在最適化表單的URL中。
1. 重新整理頁面，最適化表單會以指定的地區設定呈現。

## 支援新本地化的最佳實務 {#best-practices}

* Adobe建議您在建立最適化表單之後建立翻譯專案。

* 在現有的最適化表單中新增欄位時：
   * **針對機器翻譯**：重新建立字典及 [執行翻譯專案](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md). 建立翻譯專案後新增至最適化表單的欄位仍維持未翻譯狀態。
   * **針對人工翻譯**：使用位於的UI匯出字典 `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. 更新新新增欄位的字典並上傳。

## 檢視更多

* [使用機器翻譯或人工翻譯來翻譯以核心元件為基礎的最適化表單](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)
* [產生最適化Forms的記錄檔案](/help/forms/generate-document-of-record-core-components.md)
* [新增調適型表單至 AEM Sites 頁面或體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)


