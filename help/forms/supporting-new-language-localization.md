---
title: 支援最適化表單本地化的新地區設定
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms可讓您新增當地語系化適用性表單的地區設定。 英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)地區設定。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: eb722054f6a51320a7772bf666f656418f8392cd
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---

# 支援適用性Forms本地化的新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

## 關於語言環境字典 {#about-locale-dictionaries}

最適化表單的本地化需要兩種語言環境字典：

* **表單特定字典** 包含適用性表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明等。 它作為一組XLIFF檔案來管理，用於每個區域設定，您可以在 `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **全域字典** AEM用戶端程式庫中有兩本全域字典，以JSON物件管理。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. 這些位置包含每個區域設定的單獨資料夾。 由於全域字典不會經常更新，因此為每個區域設定保留個別的JavaScript檔案，可讓瀏覽器快取，並減少在同一伺服器上存取不同最適化表單時的網路頻寬使用量。

支援AEM Forms新本地化的步驟：

1. [添加對不支援的語言環境的本地化支援](#add-localization-support-for-non-supported-locales-add-localization-support-for-non-supported-locales)
1. [使用適用性Forms中新增的地區設定](#use-added-locale-in-adaptive-forms-use-added-locale-in-af)

## 添加對不支援的語言環境的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定來將最適化Forms內容本地化。

若要在適用性Forms執行階段新增對新地區設定的支援：

1. [複製存放庫](#1-clone-the-repository-clone-the-repository)
1. [向GuideLocalizationService服務添加區域設定](#1-add-a-locale-to-the-guide-localization-service-add-a-locale-to-the-guide-localization-service-br)
1. [添加特定於語言環境名稱的資料夾](#3-add-locale-name-specific-folder-add-locale-name-specific-folder)
3.1 [為地區設定新增XFA用戶端程式庫](#3-add-xfa-client-library-for-a-locale)
3.2 [為地區設定新增適用性表單用戶端程式庫](#4-add-adaptive-form-client-library-for-a-locale-add-adaptive-form-client-library-for-a-locale-br)
1. [為字典添加地區支援](#5-add-locale-support-for-the-dictionary-add-locale-support-for-the-dictionary-br)
1. [提交儲存庫中的更改並部署管道](#7-commit-the-changes-in-the-repository-and-deploy-the-pipeline-commit-changes-in-repo-deploy-pipeline)

### 1.克隆儲存庫 {#clone-the-repository}

1. 從命令列，導覽至您要複製FormsCloud Service存放庫的位置。
1. 執行您 [從Cloud Manager中擷取。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 類似 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. 使用Git使用者名稱和密碼來複製存放庫。
1. 在您偏好的編輯器中開啟複製的FormsCloud Service存放庫資料夾。

### 2.向指南本地化服務添加地區設定 {#add-a-locale-to-the-guide-localization-service-br}

1. 找出 `Guide Localization Service.cfg.json` 檔案並將要添加到支援區域設定的清單中的區域設定添加到。

   >[!NOTE]
   >
   >* 建立名稱為 `Guide Localization Service.cfg.json` 檔案（如果尚未存在）。


### 3.添加特定於語言環境名稱的資料夾客戶端庫 {#add-locale-name-specific-folder}

1. 在UI.content資料夾中，建立 `etc/clientlibs` 檔案夾。
1. 進一步建立名為的資料夾 `locale-name` 在 `etc/clientlibs` 做為xfa和af clientlib的容器。

#### 3.1為locale-name資料夾中的區域設定新增XFA用戶端程式庫

1. 建立名為的節點 `[locale-name]_xfa` 輸入為 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，包含類別 `xfaforms.I18N.<locale>`，並新增下列檔案：
* **I18N.js** 定義 `xfalib.locale.Strings` 針對 `<locale>` 定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** 包含下列項目：
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

#### 3.2.為語言環境地區名稱資料夾新增適用性表單用戶端程式庫 {#add-adaptive-form-client-library-for-a-locale-br}

1. 建立名為的節點 `[locale-name]_af` 輸入為 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，類別為 `guides.I18N.<locale>` 和依賴項 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 和 `guide.common`.
1. 建立名為的資料夾 `javascript` 並新增下列檔案：

   * **i18n.js** 定義 `guidelib.i18n`，具有「日曆符號」的模式， `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` 針對 `<locale>` 根據 [地區設定規範](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 針對 `<locale>` 定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. 新增 **js.txt** 包含下列項目：

   ```text
     i18n.js
       LogMessages.js
   ```

### 4.為字典添加地區支援 {#add-locale-support-for-the-dictionary-br}

只有在 `<locale>` 您添加的不在 `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. 建立資料夾 `languages` 在 `etc`，如果尚未存在。

1. 新增多值字串屬性 `languages` 至節點（如果尚未存在）。
1. 新增 `<locale-name>` 預設地區值 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`，如果尚未存在。

1. 新增 `<locale>` 的值 `languages` 屬性 `/etc/languages`.


```text
Add the newly created folders in the `filter.xml` under etc/META-INF/[folder hierarchy] as:
<filter root="/etc/clientlibs/[locale-name]"/>
<filter root="/etc/languages"/>
```

將變更提交至AEM Git存放庫前，您必須先存取 [Git存放庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

### 5.提交儲存庫中的更改並部署管道 {#commit-chnages-in-repo-deploy-pipeline}

新增地區設定支援後，將變更提交至GIT存放庫。 使用完整堆疊管道部署程式碼。 學習 [如何設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 添加新區域設定支援。

管道完成後，新新增的地區設定會顯示在AEM環境中。

### 在適用性Forms中使用新增的地區設定 {#use-added-locale-in-af}

使用新增的地區設定來使用和呈現適用性表單的步驟：

1. 登入您的AEM製作例項。
1. 前往 **Forms** >  **Forms與檔案**.
1. 選取適用性表單並按一下 **新增字典** 和 **將字典新增至翻譯專案** 嚮導。
1. 指定 **專案標題** ，然後選取 **目標語言** 從 **將字典新增至翻譯專案** 嚮導。
1. 按一下 **完成** 並執行建立的翻譯專案。
1. 選取適用性表單並按一下 **預覽為HTML**.
1. 新增 `&afAcceptLang=<locale-name>` 在適用性表單的URL中。
1. 重新整理頁面，並在指定的地區中轉譯適用性表單。

有兩種方法可識別適用性表單的地區設定。 呈現適用性表單時，會依以下項目識別要求的地區設定：

* 看 `[local]` 最適化表單URL中的選取器。 URL的格式為 `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. 使用 `[local]` 選取器允許快取最適化表單。

* 以指定順序查看下列參數：

   * 要求參數 `afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 
`afAcceptLang` 要求參數以強制地區設定。 例如，以下URL會強制以加拿大 — 法文地區設定轉譯表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 為使用者設定的瀏覽器地區設定，使用 `Accept-Language` 頁首。

如果所請求區域的客戶端庫不存在，則它檢查客戶端庫中是否存在語言代碼。 例如，如果請求的區域設定為 `en_ZA` （南非英語）和 `en_ZA` 不存在，適用性表單會使用用戶端程式庫 `en` （英語）語言（如果存在）。 不過，如果其中沒有任何表單，適用性表單會將字典用於 `en` 地區。


識別地區設定後，適用性表單會挑選表單特定字典。 如果找不到所請求地區的表單特定字典，則該字典會使用編寫適用性表單的語言的字典。

如果沒有地區設定資訊，適用性表單會以表單的原始語言傳送。 原始語言是開發最適化表單時使用的語言。

取得 [範例用戶端程式庫](/help/forms/assets/locale-support-sample.zip) 添加對新區域設定的支援。 您需要更改所需地區中的資料夾內容。

### 支援新本地化的最佳實踐 {#best-practices}

* Adobe建議在建立最適化表單後建立翻譯專案。

* 在現有適用性表單中新增欄位時：
   * **機器翻譯**:重新建立字典並執行翻譯專案。 建立翻譯專案後新增至適用性表單的欄位仍會保留未翻譯。
   * **人翻譯**:透過 `[server:port]/libs/cq/i18n/gui/translator.html`. 更新新欄位的字典並上傳它。
