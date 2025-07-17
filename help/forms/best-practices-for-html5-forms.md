---
title: HTML5 Forms的最佳作法
description: 調整您的XFA型HTML5 Forms以獲得最佳效能。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# HTML5 Forms的最佳作法{#best-practices-for-html-forms}

<span class="preview"> HTML5 Forms功能屬於Early Access方案的一部分。 若要要求存取權，請將您的正式（工作）電子郵件ID傳送電子郵件至aem-forms-ea@adobe.com。
</span>

## 概觀 {#overview}

AEM Forms有一個名為HTML5 forms的元件。 這有助於以HTML5格式呈現現有XFA型PDF forms （XDP檔案）。 本檔案提供減少載入時間及改善行動裝置上HTML5表單效能的准則和建議。

大部分的行動裝置處理能力和記憶體功能有限。 這有助於改善行動裝置的待命時間。 在行動裝置上執行的網頁瀏覽器可存取有限的資源（有限的記憶體與處理功能）。 達到限制後，瀏覽器行為會變得緩慢。 本檔案提供保持HTML5表單大小受限的建議。 較小的格式不會違反裝置的記憶體與處理能力限制，提供順暢的體驗。

雖然如此，本文章中討論的建議是針對的HTML5表單，但這些建議同樣適用於XFA型PDF forms。 這些最佳實務會共同促進HTML5表單的整體效能。 開發有效率且高生產力的表單時，需要謹慎的規劃。 讓我們開始吧：

## 節點是HTML5表單的貨幣，明智地使用它們 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表單有多個元素。 例如，表格、文字欄位和影像。 每個元素都有數個屬性可控制元素的行為和外觀。 以HTML5格式轉譯XFA表單時，所有XFA元素和對應的屬性都會轉換為模型或HTML DOM節點。 這些節點會增加DOM的大小和複雜性。 降低HTML5表單的呈現速度。

瀏覽器呈現較精簡的DOM會比較容易。 因此，您可以在XFA表單上執行下列最佳化，以減少節點數量。 因此，請產生精簡的DOM結構：

* 使用caption屬性將標籤新增到欄位。 請勿使用個別的文字元素來新增標籤。 這有助於減輕重量，進而提升效能。 它還有助於避免版面問題。
* 將表單上Draw文字元素的數量維持在最小值。 繪圖元素有助於改善可讀性和外觀，但沒有任何資訊儲存功能。 建議將多個Draw文字元素合併為一個Draw文字元素。 不要翻動石頭，讓表單更精簡。

## Lite表單效能更佳，可維持資源壓縮狀態 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表單可包含多個外部資源，例如影像、JavaScript和CSS檔案。 每次瀏覽器請求表單時，都會透過網路傳送外部資源。 在網路上傳輸所需的時間與檔案大小成正比。

因此，減少外部資源大小，只使用絕對必要的資源，是改善表單效能的偏好方法。 您可以對XFA表單執行下列最佳化，以減少表單的外部資源大小：

* 使用[壓縮影像](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)。 它可減少呈現表單所需的網路活動和記憶體量。 因此，表單載入時間會大幅減少。
* 使用AEM Configuration Manager (Day CQ HTML Library Manager)中的「縮制」選項來壓縮JavaScript和CSS檔案。 如需詳細資訊，請參閱[OSGi組態設定](/help/implementing/deploying/configuring-osgi.md)。
* 啟用Web壓縮。 這會減少源自表單的請求和回應大小。 如需詳細資訊，請參閱[AEM Forms伺服器的效能調整](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持興趣不變，僅顯示必要欄位  {#keep-the-interest-alive-show-only-required-fields}

HTML5表單可能會有數百頁。 含有大量欄位的表單在瀏覽器中載入緩慢。 您可以對XFA表單執行下列最佳化，以最佳化具有大量欄位和頁面的表單：

* 評估將大型表單分割為多個表單。 您也可以使用表單集將所有較小的表單分組，並將它們顯示為單一單位。 表單集只會載入必要的表單。 此外，在表單集中，您可以設定不同表單中的通用欄位以共用資料繫結。 資料繫結可協助使用者僅填入一次通用資訊；資訊會自動填入後續的表單，進而大幅改善效能。 如需有關表單集的詳細資訊，請參閱AEM表單中的[表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。
* 請考慮分割區段，並將每個區段移至不同頁面。 HTML5 forms會在頁面捲動要求時動態載入每個頁面。 記憶體中只會儲存捲動頁面（顯示的頁面及其之前的頁面），其餘頁面則會視需要載入。 因此，在其本身的頁面上分割和移動區段可縮短載入表單所需的時間。 您也可以使用表單的第一頁做為登入頁面。 它類似於書籍的目錄(TOC)。 表單的登入頁面僅包含表單其他區段的連結。 它大幅改善表單第一頁的載入時間，並導致改善使用者體驗。
* 依預設，隱藏條件區段。 讓這些區段只在符合特定條件時才可見。 這有助於將DOM的大小維持在最小。 您也可以使用標籤式導覽，一次只顯示一個截面。

## 越少越好，請減少頁數 {#less-is-more-reduce-the-number-of-pages}

HTML5表單可包含資料導向欄位（表格和子表單）。 這些欄位會展開執行階段表單的大小。 例如，HTML5表單中的資料驅動表格可跨越數千列。 這類表格可能會導致版面配置和效能降低。 以下建議的最佳化可協助您縮短資料導向欄位HTML5表單的載入時間：

* 使用XFA指令碼完成分頁導覽，以顯示資料導向欄位（表格和子表單）。 在分頁導覽中，頁面上只會顯示特定資料。 它限制瀏覽器上色作業為一次顯示的欄位，並使表單導覽更容易。 此外，行動裝置上的使用者只對資料子集感興趣。 它可幫助您提供絕佳的使用者體驗，並減少載入所需資料所需的時間。 您只需要一個的價格，就能獲得兩個解決方案。  另請注意，分頁導覽無法直接使用。 您可以使用XFA指令碼來開發分頁導覽。

* 評估將多個唯讀欄合併到單一欄中的情形。 它可減少顯示表單所需的記憶體。 同時，請避免顯示不需要使用者輸入任何內容的欄。
* 如果上述建議並未產生許多改善效果，請評估將資料導向表單分割為[表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果表格超過1000列，則每100列會移至不同的表單。 這有助於改善表單的載入時間和效能。  另請注意，表單集會產生所有表單的合併提交XML。 若要區分每個表單的資料，請使用不同的資料根。 如需詳細資訊，請參閱[AEM Forms中的表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。

## 記錄檔案(DOR)的二進位功能 {#power-of-two-for-document-of-record-dor}

XFA表單可以有大量的專用於記錄檔案(DOR)的區段。 為了減少節點數並改善這類表單的效能，您可以維護不同的表單副本 — 一個副本用於填寫表單，另一個副本用於在伺服器上產生記錄檔案。 在填入XFA表單的副本中，顯示僅擷取資料所需的欄位。 在從產生記錄檔案XFA中，僅在表單的列印輸出中保留必填欄位。 在選擇建議的方法之前，請評估效能增益和維護額外負荷。

## 建議閱讀  {#recommended-reads}

Adobe Experience Manager (AEM)表單可協助您將複雜的交易轉換為簡單、愉快的數位體驗。 然而，您需要共同努力開發有效率且高生產力的表單。 除了HTML5 Forms，以下是一般AEM最佳實務的建議閱讀：


<!--

* Best practices for Deploying and maintaining AEM
* Best practices for Authoring content
* [Best practices for Administering AEM](/help/sites-administering/administer-best-practices.md)
* [Best practices for Developing solutions](/help/sites-developing/best-practices.md)
* [Best practices for working with adaptive forms](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms server does not embed fonts to a Dynamic PDF form](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

-->

## 快速參考卡 {#quick-reference-card}

您可以列印下列卡片（按一下卡片可下載高解析度版本），並將其放在您的案頭上以供快速參考：
[![HTML5 Forms最佳作法快速參考卡](assets/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
