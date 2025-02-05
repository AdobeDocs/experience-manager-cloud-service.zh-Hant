---
title: 如何根據基礎元件為最適化表單新增對新區域設定的支援？
description: 對於最適化Forms，除了現成可用的語言之外，您還可以新增更多語言的區域設定。
feature: Adaptive Forms, Foundation Components
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 3%

---

# 支援最適化Forms本地化的新地區設定 {#supporting-new-locales-for-adaptive-forms-localization}

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)，使用現代且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html) |
| 核心元件 | [按一下這裡](supporting-new-language-localization-core-components.md) |
| 基礎元件 | 本文章 |

AEM Forms提供英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定的立即可用支援。 您也可以新增對更多地區設定的支援，例如印地語(hi_IN)。

## 瞭解地區設定字典 {#about-locale-dictionaries}

最適化表單本地化依賴兩種型別的地區詞典：

* **表單特定字典**&#x200B;包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明。 它被管理為每個地區設定的一組XLIFF檔案，您可以在`[author-instance]/libs/cq/i18n/gui/translator.html`存取它。

* **全域字典** AEM使用者端程式庫中有兩個全域字典，管理為JSON物件。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在`[author-instance]/libs/fd/xfaforms/clientlibs/I18N`找到這些字典。 這些位置包含每個地區設定的個別資料夾。 由於全域字典不經常更新，因此針對每個地區設定保留個別的JavaScript檔案，可讓瀏覽器在存取相同伺服器上的不同最適化表單時，快取檔案並降低網路頻寬使用量。

## 新增新地區設定的支援 {#add-support-for-new-locales}

執行以下步驟來新增新地區設定的支援：

1. [新增不支援地區設定的本地化支援](#add-localization-support-for-non-supported-locales)
1. [在最適化Forms中使用新增的地區設定](#use-added-locale-in-af)

### 新增不支援地區設定的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM FormsForms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、巴西葡萄牙文(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)本地化內容。

若要在Adaptive Forms執行階段新增對新地區設定的支援：

1. [複製您的存放庫](#clone-the-repository)
1. [新增語言環境至GuideLocalizationService服務](#add-a-locale-to-the-guide-localization-service)
1. [新增地區名稱特定資料夾](#add-locale-name-specific-folder)
1. [新增字典的地區設定支援](#add-locale-support-for-the-dictionary)
1. [提交存放庫中的變更並部署管道](#commit-changes-in-repo-deploy-pipeline)

#### 1.複製存放庫 {#clone-the-repository}

1. 從命令列，導覽至您要複製FormsCloud Service存放庫的位置。
1. 執行您[從Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)擷取的命令。 它類似於`git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`。
1. 使用Git使用者名稱和密碼來複製存放庫。
1. 在您偏好的編輯器中，開啟複製的FormsCloud Service存放庫資料夾。

#### 2.新增語言環境至「本地化指南」服務 {#add-a-locale-to-the-guide-localization-service}

1. 找到`Guide Localization Service.cfg.json`檔案，並將您要新增的區域設定新增至支援的區域設定清單。

   >[!NOTE]
   >
   > 建立名為`Guide Localization Service.cfg.json`檔案的檔案（如果尚未存在）。

#### 3.新增地區名稱特定的資料夾使用者端資源庫 {#add-locale-name-specific-folder}

1. 在UI.content資料夾中，建立`etc/clientlibs`資料夾。
1. 進一步在`etc/clientlibs`下建立名為`locale-name`的資料夾，用作xfa和af clientlibs的容器。

##### 3.1在locale-name資料夾中新增地區設定的XFA使用者端資料庫

使用類別`xfaforms.I18N.<locale>`在`etc/clientlibs/locale_name`下建立名稱為`[locale-name]_xfa`且型別為`cq:ClientLibraryFolder`的節點，並新增下列檔案：

* **I18N.js**&#x200B;定義了`/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`中定義的`<locale>`的`xfalib.locale.Strings`。
* **js.txt**包含下列專案：
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2.為地區設定名稱資料夾新增最適化表單使用者端資料庫

1. 在`etc/clientlibs/locale_name`下建立名稱為`[locale-name]_af`且型別為`cq:ClientLibraryFolder`的節點，類別為`guides.I18N.<locale>`，相依性為`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。
1. 建立名為`javascript`的資料夾並新增下列檔案：

   * **i18n.js**&#x200B;定義了`guidelib.i18n`，並根據[地區設定集規格](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)中描述的XFA規格，為`<locale>`具有「calendarSymbols」、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces`的模式。
   * **LogMessages.js**&#x200B;定義了`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`中定義的`<locale>`的`guidelib.i18n.strings`和`guidelib.i18n.LogMessages`。

1. 新增包含下列專案的&#x200B;**js.txt**：

   ```
     i18n.js
     LogMessages.js
   ```

#### 4.為字典新增地區設定支援 {#add-locale-support-for-the-dictionary}

只有在您新增的`<locale>`不屬於`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`時，才執行此步驟。

1. 在`etc`下建立資料夾`languages` （如果尚未存在）。

1. 將多值字串屬性`languages`新增至節點（如果尚未存在）。
1. 新增`<locale-name>`預設地區設定值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` （如果尚未存在）。

1. 將`<locale>`新增至`/etc/languages`的`languages`屬性值。
1. 在etc/META-INF/[資料夾階層]下的`filter.xml`中新增建立的資料夾，如下所示：

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

在將變更提交至AEM Git存放庫之前，您需要存取您的[Git存放庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git)。

#### 5.認可存放庫中的變更並部署管道 {#commit-changes-in-repo-deploy-pipeline}

新增地區設定支援後，將變更提交到GIT存放庫。 使用完整棧疊管道部署您的計畫碼。 瞭解[如何設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)以新增地區設定支援。
管道完成後，新新增的地區設定會顯示在AEM環境中。

### 在最適化Forms中使用新增的地區設定 {#use-added-locale-in-af}

執行以下步驟，使用新新增的地區設定來使用和轉譯調適型表單：

1. 登入您的AEM作者執行個體。
1. 移至&#x200B;**Forms** > **Forms和檔案**。
1. 選取最適化表單，然後按一下&#x200B;**新增字典**&#x200B;和&#x200B;**新增字典至翻譯專案**&#x200B;精靈出現。
1. 指定&#x200B;**專案標題**，並從&#x200B;**新增字典至翻譯專案**&#x200B;精靈的下拉式功能表中選取&#x200B;**目標語言**。
1. 按一下&#x200B;**完成**&#x200B;並執行已建立的翻譯專案。
1. 選取最適化表單，然後按一下&#x200B;**以HTML預覽**。
1. 在最適化表單的URL中新增`&afAcceptLang=<locale-name>`。
1. 重新整理頁面，最適化表單會以指定的地區設定呈現。

有兩種方法可識別調適型表單的地區設定。 轉譯適用性表單時，會透過以下方式識別請求的地區設定：

* 正在擷取最適化表單URL中的`[local]`選取器。 URL 的格式是：`http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`。使用`[local]`選擇器可允許快取最適化表單。

* 正在以列出的順序擷取下列引數：

   * 要求引數`afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞`afAcceptLang`要求引數以強制地區設定。 例如，下列URL會強制以加拿大法文地區設定來轉譯表單：
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 使用`Accept-Language`標頭在請求中指定之使用者的瀏覽器地區設定。

如果要求的地區設定的使用者端程式庫不存在，它會檢查地區設定中存在的語言代碼的使用者端程式庫。 例如，如果要求的地區設定為`en_ZA` （南非英文），且`en_ZA`的使用者端資料庫不存在，則最適化表單會使用`en` （英文）語言的使用者端資料庫（如果存在）。 但是，如果兩者都不存在，則最適化表單會針對`en`地區設定使用字典。


地區設定一經識別，「最適化表單」就會挑選表單專屬的字典。 如果找不到所要求地區設定的表單特定字典，則會使用用於編寫最適化表單的語言的字典。

如果沒有地區設定資訊出現，最適化表單會以表單的原始語言傳送。 原始語言是開發最適化表單時使用的語言。

取得[範例使用者端程式庫](/help/forms/assets/locale-support-sample.zip)以新增新地區設定的支援。 您需要以所需的地區設定變更資料夾的內容。

## 支援新本地化的最佳實務 {#best-practices}

* Adobe建議您在建立最適化表單之後建立翻譯專案。

* 在現有的最適化表單中新增欄位時：
   * **對於機器翻譯**：重新建立字典並執行翻譯專案。 建立翻譯專案後新增至最適化表單的欄位仍維持未翻譯狀態。
   * **針對人工翻譯**：透過`[server:port]/libs/cq/i18n/gui/translator.html`匯出字典。 更新新新增欄位的字典並上傳。


## 另請參閱 {#see-also}

{{see-also}}