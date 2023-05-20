---
title: 將對新語言環境的支援新增至最適化表單
seo-title: Learn to add support for new locales to your adaptive forms
description: AEM Forms允許您為本地化自適應表單添加新區域設定。 英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)語言環境。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 支援適應性Forms本地化的新語言環境 {#supporting-new-locales-for-adaptive-forms-localization}

AEM Forms為英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)語言環境提供現成支援。 您還可以添加對更多語言環境的支援，如Hindi(hi_IN)。

## 瞭解區域設定詞典 {#about-locale-dictionaries}

自適應表單的本地化依賴於兩種語言環境詞典：

* **表單特定詞典** 包含自適應表單中使用的字串。 例如，標籤、欄位名稱、錯誤消息、幫助說明。 它作為一組XLIFF檔案管理，用於每個區域設定，您可以在 `[author-instance]/libs/cq/i18n/gui/translator.html`。

* **全局詞典** 客戶端庫中有兩個全局字典，作為JSON對象AEM管理。 這些詞典包含預設錯誤消息、月名、貨幣符號、日期和時間模式等。 您可以在 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`。 這些位置包含每個區域設定的單獨資料夾。 由於全局詞典不會經常更新，因此為每個區域設定保留單獨的JavaScript檔案使瀏覽器能夠在訪問同一伺服器上的不同自適應表單時快取它們並減少網路頻寬使用。

## 添加對新語言環境的支援 {#add-support-for-new-locales}

執行以下步驟，添加對新區域設定的支援：

1. [添加對不支援的語言環境的本地化支援](#add-localization-support-for-non-supported-locales)
1. [在自適應Forms中使用添加的語言環境](#use-added-locale-in-af)

### 添加對不支援的語言環境的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)語言環境中的自適應Forms內容本地化。

要在Adaptive Forms運行時添加對新區域設定的支援，請：

1. [克隆儲存庫](#clone-the-repository)
1. [將區域設定添加到GuideLocalizationService服務](#add-a-locale-to-the-guide-localization-service)
1. [添加區域設定名稱特定的資料夾](#add-locale-name-specific-folder)
1. [為字典添加區域設定支援](#add-locale-support-for-the-dictionary)
1. [提交儲存庫中的更改並部署管道](#commit-changes-in-repo-deploy-pipeline)

#### 1。克隆儲存庫 {#clone-the-repository}

1. 從命令行導航到要克隆FormsCloud Service儲存庫的位置。
1. 執行命令 [從雲管理器中檢索到。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 類似 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`。
1. 使用git用戶名和密碼克隆儲存庫。
1. 在首選編輯器中開啟克隆的FormsCloud Service儲存庫資料夾。

#### 2.將區域設定添加到指南本地化服務 {#add-a-locale-to-the-guide-localization-service}

1. 查找 `Guide Localization Service.cfg.json` 檔案，並將要添加到支援的語言環境清單的語言環境添加。

   >[!NOTE]
   >
   > 建立名為的檔案 `Guide Localization Service.cfg.json` 的子菜單。

#### 3.添加區域設定名稱特定的資料夾客戶端庫 {#add-locale-name-specific-folder}

1. 在UI.content資料夾中，建立 `etc/clientlibs` 的子菜單。
1. 進一步建立名為 `locale-name` 在 `etc/clientlibs` 作為xfa和af客戶端的容器。

##### 3.1在locale-name資料夾中為區域設定添加XFA客戶端庫

建立名為的節點 `[locale-name]_xfa` 和 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，與類別 `xfaforms.I18N.<locale>`，並添加以下檔案：

* **I18N.js** 定義 `xfalib.locale.Strings` 為 `<locale>` 定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。
* **js.txt** 包含以下內容：
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2為區域設定語言環境名稱資料夾添加Adaptive Form客戶端庫

1. 建立名為的節點 `[locale-name]_af` 和 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，在類別中 `guides.I18N.<locale>` 和依賴項 `xfaforms.3rdparty`。 `xfaforms.I18N.<locale>` 和 `guide.common`。
1. 建立名為的資料夾 `javascript` 並添加以下檔案：

   * **i18n.js** 定義 `guidelib.i18n`，具有&quot;calendarSymbols&quot;的圖案， `datePatterns`。 `timePatterns`。 `dateTimeSymbols`。 `numberPatterns`。 `numberSymbols`。 `currencySymbols`。 `typefaces` 為 `<locale>` 按照中所述的XFA規範 [區域設定規範](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)。
   * **LogMessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 為 `<locale>` 定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。

1. 添加 **js.txt** 包含以下內容：

   ```
     i18n.js
     LogMessages.js
   ```

#### 4.為字典添加區域設定支援 {#add-locale-support-for-the-dictionary}

僅在 `<locale>` 您正在添加的 `en`。 `de`。 `es`。 `fr`。 `it`。 `pt-br`。 `zh-cn`。 `zh-tw`。 `ja`。 `ko-kr`。

1. 建立資料夾 `languages` 在 `etc`的子菜單。

1. 添加多值字串屬性 `languages` 到節點（如果尚未出現）。
1. 添加 `<locale-name>` 預設區域設定 `de`。 `es`。 `fr`。 `it`。 `pt-br`。 `zh-cn`。 `zh-tw`。 `ja`。 `ko-kr`的子菜單。

1. 添加 `<locale>` 到 `languages` 物業 `/etc/languages`。
1. 在 `filter.xml` 在etc/META-INF下[資料夾層次結構] 為：

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

在將更改提交到AEMGit儲存庫之前，您需要訪問 [Git儲存庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git)。

#### 5.提交儲存庫中的更改並部署管道 {#commit-changes-in-repo-deploy-pipeline}

添加新區域設定支援後，將更改提交到GIT儲存庫。 使用完整堆棧管道部署代碼。 學習 [如何設定管線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 添加新的區域設定支援。
管道完成後，新添加的區域設定將出現在環AEM境中。

### 在自適應Forms中使用添加的區域設定 {#use-added-locale-in-af}

執行以下步驟，使用新添加的區域設定來使用和呈現自適應表單：

1. 登錄到您的作AEM者實例。
1. 轉到 **Forms** >  **Forms和文檔**。
1. 選擇一個自適應表單，然後按一下 **添加詞典** 和 **將詞典添加到翻譯項目** 的子菜單。
1. 指定 **項目標題** 的 **目標語言** 的下拉菜單 **將詞典添加到翻譯項目** 的子菜單。
1. 按一下 **完成** 並執行建立的翻譯項目。
1. 選擇一個自適應表單，然後按一下 **預覽為HTML**。
1. 添加 `&afAcceptLang=<locale-name>` 的子菜單。
1. 刷新頁面，並在指定的區域設定中呈現「自適應表單」。

有兩種方法可標識「自適應表單」的區域設定。 在呈現自適應表單時，它通過以下方式標識所請求的區域設定：

* 檢索 `[local]` 的子菜單。 URL的格式為 `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`。 使用 `[local]` 選擇器允許快取自適應表單。

* 按所列順序檢索以下參數：

   * 請求參數 `afAcceptLang`
要覆蓋用戶的瀏覽器區域設定，可以通過 
`afAcceptLang` 請求參數以強制區域設定。 例如，以下URL強制以加拿大 — 法語語言環境呈現表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 用戶的瀏覽器區域設定，該設定在請求中使用 `Accept-Language` 標題。

如果請求的區域設定的客戶端庫不存在，則它會檢查客戶端庫中是否存在語言代碼。 例如，如果請求的區域設定為 `en_ZA` （南非英語）和 `en_ZA` 不存在，自適應表單使用的客戶端庫 `en` （英語）語言（如果存在）。 但是，如果它們都不存在，則「自適應表單」將字典用於 `en` 區域設定。


一旦確定了區域設定，「自適應表單」就會挑選特定於表單的字典。 如果找不到所請求區域設定的表單特定詞典，則它將該詞典用於編寫自適應表單的語言。

如果沒有區域設定資訊，則以表單的原始語言傳遞自適應表單。 原始語言是開發自適應表單時使用的語言。

獲取 [示例客戶端庫](/help/forms/assets/locale-support-sample.zip) 添加對新區域設定的支援。 您需要在所需區域設定中更改資料夾的內容。

## 支援新本地化的最佳實踐 {#best-practices}

* Adobe建議在建立「自適應表單」後建立翻譯項目。

* 在現有自適應表單中添加新欄位時：
   * **用於機器翻譯**:重新建立字典並運行翻譯項目。 在建立轉換項目後添加到自適應表單的欄位將保持未翻譯狀態。
   * **人文翻譯**:通過 `[server:port]/libs/cq/i18n/gui/translator.html`。 更新新添加欄位的字典並上載它。
