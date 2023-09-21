---
title: 如何根據核心元件將新語言環境的支援新增至最適化表單？
description: AEM Forms可讓您新增本地化最適化表單的地區設定。
source-git-commit: 23f915f0e2e33b9cf1313d15cb98a0a4f8243746
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 3%

---

# 根據核心元件為最適化Forms新增地區設定 {#supporting-new-locales-for-adaptive-forms-localization}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| Foundation 元件 | [按一下這裡](supporting-new-language-localization.md) |
| 核心元件 | 本文章 |

AEM Forms提供英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定的立即可用支援。 您也可以新增對更多地區設定的支援，例如印地語(hi_IN)。

## 瞭解地區設定字典 {#about-locale-dictionaries}

最適化表單本地化依賴兩種型別的地區詞典：

* **表單特定字典** 包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明。 它作為每個地區設定的一組XLIFF檔案進行管理，您可以在以下位置存取它： `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **全域字典** AEM使用者端資料庫中有兩個全域字典，以JSON物件形式管理。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 這些字典位於 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. 這些位置包含每個地區設定的個別資料夾。 由於全域字典不經常更新，因此針對每個地區設定保留個別的JavaScript檔案，可讓瀏覽器在存取相同伺服器上的不同最適化表單時，快取檔案並降低網路頻寬使用量。

## 先決條件 {#prerequistes}

在您開始新增新地區設定的支援之前，

* 安裝純文字編輯器(IDE)以更輕鬆進行編輯。 本檔案中的範例是根據Microsoft VS Code。
* 複製最適化Forms核心元件存放庫。 複製存放庫：
   1. 開啟命令列或終端視窗，並導覽至儲存庫的位置。 例如 `/adaptive-forms-core-components`
   1. 執行以下命令以複製存放庫：

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  存放庫包含新增地區設定所需的使用者端資料庫。


## 新增地區 {#add-localization-support-for-non-supported-locales}

AEM FormsForms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、巴西葡萄牙文(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)本地化內容。 若要在Adaptive Forms執行階段新增對新地區設定的支援，請遵循下列步驟：

![新增地區設定至存放庫](add-a-locale-adaptive-form-core-components.png)

### 1.複製您的AEMas a Cloud ServiceGit存放庫 {#clone-the-repository}

1. 開啟命令列，然後選擇要儲存存放庫的目錄，例如 `/cloud-service-repository/`.

1. 執行以下命令以複製存放庫：

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   取代 `<my-org>` 和 `<my-program>` 以上的URL中，加入您的組織名稱和方案名稱。 如需詳細指示，以取得組織名稱、計畫名稱或Git存放庫的完整路徑以及複製存放庫所需的認證，請參閱 [存取Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 文章。

   成功完成命令後，資料夾 `<my-program>` 「 」已建立。 其中包含從Git存放庫複製的內容。 在文章的其餘部分，資料夾將改稱為 `[AEM Forms as a Cloud Service Git repostory]`.


### 2.新增語言環境至「本地化指南」服務 {#add-a-locale-to-the-guide-localization-service}

1. 以純文字編輯器開啟上一節複製的存放庫資料夾。
1. 導覽至 `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` 檔案夾。您可找到 `<appid>` 在 `archetype.properties` 專案的檔案。
1. 開啟 `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` 檔案進行編輯。 如果檔案不存在，請建立檔案。 具有支援地區設定的範例檔案如下所示：

   ![範例指南Localization Service.cfg.json](locales.png)

1. 新增 [語言的區域設定代碼](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 例如，您想要新增北印度語的「hi」。
1. 儲存並關閉檔案。

### 3.建立使用者端資料庫以新增地區設定

AEM Forms提供範例使用者端資料庫，協助您輕鬆新增地區設定。 您可以下載並新增 `clientlib-it-custom-locale` 使用者端資料庫從GitHub上的最適化Forms核心元件存放庫移至您的Formsas a Cloud Service存放庫。 若要新增使用者端程式庫，請執行下列步驟：

1. 以純文字編輯器開啟Adaptive Forms核心元件存放庫。 如果您沒有複製存放庫，請參閱 [必要條件](#prerequistes) 以取得複製存放庫的指示。
1. 導覽至 `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` 目錄。
1. 複製 `clientlib-it-custom-locale` 目錄。
1. 瀏覽至 `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` 並貼上 `clientlib-it-custom-locale` 目錄。


### 4.建立特定地區設定的檔案 {#locale-specific-file}

1. 瀏覽到 `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. 找到 [GitHub上的英文地區設定.json檔案](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json)，其中包含產品所包含的最新預設字串集。
1. 為您的特定地區設定建立新的.json檔案。
1. 在新建立的.json檔案中，映象英文地區設定檔案的結構。
1. 將.json檔案中的英文字串取代為您的語言對應的當地語系化字串。
1. 儲存並關閉檔案。


### 4.新增地區設定支援至字典 {#add-locale-support-for-the-dictionary}

只有在 `<locale>` 您新增的內容不屬於 `en`， `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`.

1. 導覽至 `[AEM Forms as a Cloud Service Git repostory]/ui.content/src/main/content/jcr_root/etc/` 檔案夾。

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

### 5.提交變更並部署管道 {#commit-changes-in-repo-deploy-pipeline}

在新增地區設定支援後，將變更提交到GIT存放庫。 使用完整棧疊管道部署您的計畫碼。 瞭解 [如何設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 以新增地區設定支援。
管道完成後，新新增的地區設定會顯示在AEM環境中。

## 在最適化Forms中使用新增的地區設定 {#use-added-locale-in-af}

執行以下步驟，使用新新增的地區設定來使用和轉譯調適型表單：

1. 登入您的AEM作者執行個體。
1. 前往 **Forms** >  **Forms與檔案**.
1. 選取最適化表單並按一下 **新增字典** 和 **新增字典至翻譯專案** 精靈出現。
1. 指定 **專案標題** 並選取 **目標語言** 從「 」的下拉式功能表 **新增字典至翻譯專案** 精靈。
1. 按一下 **完成** 並執行已建立的翻譯專案。
1. 選取最適化表單並按一下 **以HTML預覽**.
1. 新增 `&afAcceptLang=<locale-name>` 在最適化表單的URL中。
1. 重新整理頁面，最適化表單會以指定的地區設定呈現。

有兩種方法可識別調適型表單的地區設定。 轉譯適用性表單時，會透過以下方式識別請求的地區設定：

* 正在擷取 `[local]` 最適化表單URL中的選取器。 URL 的格式是：`http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`。使用 `[local]` 選擇器允許快取最適化表單。

* 正在以列出的順序擷取下列引數：

   * 要求引數 `afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 `afAcceptLang` 要求引數以強制地區設定。 例如，下列URL會強制以加拿大法文地區設定來轉譯表單：
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 為使用者設定的瀏覽器地區設定，該設定是在使用 `Accept-Language` 標頭。

如果要求的地區設定的使用者端程式庫不存在，它會檢查地區設定中存在的語言代碼的使用者端程式庫。 例如，如果要求的地區設定為 `en_ZA` （南非英文）和的客戶資料庫 `en_ZA` 不存在，調適型表單會將使用者端程式庫用於 `en` （英文）語言（如果有的話）。 但是，如果兩者都不存在，則最適化表單會將該字典用於 `en` 地區設定。


地區設定一經識別，「最適化表單」就會挑選表單專屬的字典。 如果找不到所要求地區設定的表單特定字典，則會使用用於編寫最適化表單的語言的字典。

如果沒有可用的地區設定資訊，最適化表單將會以其原始語言顯示，原始語言是開發期間使用的語言。

Get [範例使用者端資源庫](/help/forms/assets/locale-support-sample.zip) 以新增新地區設定的支援。 您需要以所需的地區設定變更資料夾的內容。

## 支援新本地化的最佳實務 {#best-practices}

* Adobe建議您在建立最適化表單之後建立翻譯專案。

* 在現有的最適化表單中新增欄位時：
   * **針對機器翻譯**：重新建立字典並執行翻譯專案。 建立翻譯專案後新增至最適化表單的欄位仍維持未翻譯狀態。
   * **針對人工翻譯**：透過匯出字典 `[server:port]/libs/cq/i18n/gui/translator.html`. 更新新新增欄位的字典並上傳。
