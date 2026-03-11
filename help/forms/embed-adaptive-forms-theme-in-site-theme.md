---
title: 將最適化Forms主題內嵌於AEM Sites主題
description: 瞭解如何將最適化Forms主題（例如畫布）整合到AEM Sites主題中，讓Sites頁面和內嵌的最適化Forms共用一個統一的主題和部署。
keywords: 最適化表單主題，網站主題， AEM Sites主題，表單主題整合，前端管道，主題內嵌
feature: Adaptive Forms, Core Components
role: Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="適用於AEM Forms)。"
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# 將最適化Forms主題內嵌於AEM Sites主題

您可以將最適化Forms主題(例如[AEM Forms畫布主題](https://github.com/adobe/aem-forms-theme-canvas))內嵌到您的AEM Sites主題中。 如此一來，單一主題會驅動您的網站頁面，以及這些頁面上內嵌的任何最適化Forms，透過[AEM前端管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=zh-Hant)使用一個組建和一個部署。

本文適用於維護或自訂標準（或自訂） AEM Sites佈景主題，且想加入最適化表單樣式而不需管理個別Forms佈景主題部署的開發人員。

## 先決條件 {#prerequisites}

開始之前，請確定您已：

* **AEM as a Cloud Service**&#x200B;已針對您的網站主題設定[前端管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=zh-Hant)。
* **網站主題來源** — 例如[標準網站範本主題](https://github.com/adobe/aem-site-template-standard) （包含具有`theme/`、`src/theme.scss`等`src/components/`的存放庫）。
* **Forms主題來源** - [AEM Forms畫布主題](https://github.com/adobe/aem-forms-theme-canvas) (或其他相容的Adaptive Forms主題)在本機複製或下載。
* **Node.js和npm** — 建立網站主題（請參閱主題README以取得支援的版本）。
* **Maven** — 如果您建置完整的網站範本套件（僅限佈景主題工作的選用專案）。

## 步驟1：建立最適化表單元件資料夾 {#step-1-create-folder}

在您的網站主題存放庫中，建立Forms主題將顯示的資料夾：

```text
theme/src/components/adaptiveform/
```

所有Forms主題資產將位於此資料夾下方，因此與現有網站元件分開。

## 步驟2：複製Forms主題元件和影像 {#step-2-copy-components-and-images}

使用您的&#x200B;**Forms主題** （例如`aem-forms-theme-canvas`）和您的&#x200B;**網站主題**&#x200B;路徑：

1. **複製元件資料夾**\
   從Forms佈景主題，將`src/components/`的整個內容複製到網站佈景主題，如下所示：

   ```text
   theme/src/components/adaptiveform/
   ```

   因此您會獲得類似以下的路徑：

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![新增最適化表單元件](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **複製影像**\
   將Forms主題影像複製到網站主題：

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   建立`theme/src/components/adaptiveform/resources/images/` （若不存在），然後複製所有影像資產（例如`question.svg`、`Chevron-Left.svg`、`busy-state.gif`等）。

   ![新增影像](/help/forms/assets/theme-add-images.png)

## 步驟3：複製變數和mixin {#step-3-copy-variables-and-mixins}

Forms主題在`src/site/`下使用共用變數和mixin。 僅將這兩個檔案複製到&#x200B;**的**&#x200B;根`adaptiveform/` （不在`site`子資料夾內）：

| Source (Forms主題) | 目的地（網站主題） |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

請&#x200B;**不**&#x200B;複製Forms佈景主題的`src/site/`資料夾的其餘部分；內嵌的表單樣式只需要這兩個檔案。

![新增變數和mixin](/help/forms/assets/theme-add-mixin-variable.png)

## 步驟4：在SCSS中修正影像路徑 {#step-4-fix-image-paths}

在Forms佈景主題中，元件SCSS檔案通常會參照路徑如`./resources/`或`url(resources/`的影像。 複製到網站主題後，這些路徑必須指向`theme/src/components/adaptiveform/resources/images/`。

**標準網站範本主題**&#x200B;使用從`url()`解析`theme/src/`個路徑的Parcel。 因此，當影像位於`theme/src/components/adaptiveform/resources/images/`時，請使用路徑&#x200B;**`components/adaptiveform/resources/images/`** （相對於`theme/src/`）。

在&#x200B;**下每**&#x200B;的`.scss`尋找並取代`theme/src/components/adaptiveform/`：

| 尋找 | 取代為 |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**範例** — 之前(Forms佈景主題)：

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**在**&#x200B;之後（網站主題，`adaptiveform/resources/images/`中的影像）：

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![變更影像URL](/help/forms/assets/theme-change-url.png)

對`adaptiveform/`下參考影像（按鈕、摺疊式功能表、精靈、容器、塗鴉等）的每個SCSS檔案重複此步驟。 建議在IDE中尋找/取代`theme/src/components/adaptiveform/`以上的專案。

## 步驟5：建立最適化表單入口點SCSS {#step-5-create-adaptiveform-scss}

在網站主題中建立&#x200B;**`theme/src/components/adaptiveform/_adaptiveform.scss`**。 此檔案必須：

1. 匯入共用的變數和mixin。
2. 匯入每個最適化表單元件的主要SCSS檔案。

使用以下專案作為完整進入點（符合與所有核心元件型表單元件的標準整合）：

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![最適化表單scss](/help/forms/assets/theme-adaptive-form-scss.png)

如果您的Forms主題遺漏了某些元件（例如沒有塗鴉或驗證碼），請移除或註解相對應的`@import`行以避免建置錯誤。 以上清單符合[畫布主題](https://github.com/adobe/aem-forms-theme-canvas)結構。

## 步驟6：匯入網站主題中的最適化表單主題 {#step-6-import-in-theme-scss}

在&#x200B;**`theme/src/theme.scss`**&#x200B;中，在檔案的&#x200B;**端**&#x200B;新增單一匯入（在其他元件匯入之後）：

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**範例** - `theme.scss`結尾：

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![新增最適化表單scss](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

這是現有網站主題結構中唯一需要的變更；所有表單特定程式碼都會保留在`src/components/adaptiveform/`之下。

## 步驟7：建置和部署 {#step-7-build-and-deploy}

1. 從主題根目錄建置網站主題：

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![執行組建](/help/forms/assets/theme-mpm-run-build.png)

2. 透過您現有的[前端管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=zh-Hant)部署。 部署後，相同主題CSS將套用至網站頁面和內嵌的最適化Forms。

## 疑難排解 {#troubleshooting}

| 問題 | 檢查內容 |
|-------|-------------------------------|
| 建置失敗：影像的「找不到檔案」 | 確定所有表單影像都在`theme/src/components/adaptiveform/resources/images/`中。 在`.scss`下的每個`adaptiveform/`中，使用`url(components/adaptiveform/resources/images/...)`，這樣路徑會從`theme/src/`中解析（使用Parcel標準網站主題組建的必要專案）。 請勿單獨使用`../resources/`或`resources/`，除非您的套件組合器解析每個檔案的路徑；然後使用符合您影像資料夾的路徑。 |
| 建置失敗： `_variables.scss`或`_mixin.scss`的「找不到檔案」 | 將兩個檔案從Forms主題`src/site/`複製到`theme/src/components/adaptiveform/` （最適化表單根），而不是複製到`site`子資料夾內。 |
| 建置失敗：元件（例如`_scribble.scss`）的「找不到檔案」 | 您的Forms主題可能不包括該元件。 在`theme/src/components/adaptiveform/_adaptiveform.scss`中，移除或註解該元件的`@import`行。 |
| 表單會轉譯，但沒有樣式 | 確認頁面使用包含已建置主題CSS的使用者端資料庫，且`theme.scss`包含`@import './components/adaptiveform/_adaptiveform.scss';`行，且主題已重建並部署。 |
| 網站與表單元件之間的樣式衝突 | 表單元件類別已設定名稱空間（例如`cmp-adaptiveform-button`）。 如果您看到衝突，請檢查自訂網站CSS是否覆寫這些類別，並調整特殊性或順序。 |

## 另請參閱 {#see-also}

* [使用主題來設定核心元件型最適化Forms的樣式](/help/forms/using-themes-in-core-components.md)
* [使用前端管道開發](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=zh-Hant)
