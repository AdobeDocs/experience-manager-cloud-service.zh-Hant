---
title: 最適化表單區塊元件及其屬性
description: 本文件概述 AEM Forms 適用的 Edge Delivery Services 所提供表單元件及其屬性。
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: ht
source-wordcount: '1009'
ht-degree: 100%

---

# 最適化表單區塊元件及其屬性

AEM Forms 適用的 Edge Delivery Services 讓您可以使用各種元件建立容易使用的互動式表單。這些元件符合不同類型資料收集的需求，還可供您輕鬆自訂以滿足您的特定需求。


![含有部份元件和屬性的試算表範本](/help/edge/assets/sample-form-in-spreadsheet.png)

最適化 Forms 區塊可為所有欄位類型和容器 (面板) 產生[統一的 HTML 結構](/help/edge/docs/forms/style-theme-forms.md)以確保一致性。這種維持一致的結構可更易[設計表單樣式](/help/edge/docs/forms/style-theme-forms.md)。

## 可用元件

以下是可用元件的概觀：

### 輸入欄位

* 所有有效的 HTML5 [輸入類型](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)和 [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)。例如，按鈕、勾選方塊、顏色、日期、本地日期時間、電子郵件、檔案、隱藏、影像、月份、數字、密碼、單選、範圍、重設、提交、電話、文字、時間、url 和星期。

### 選取控制

* [勾選方塊群組](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)：選取多個選項。
* [單選按鈕群組](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)：在一組選項中進行一個單項選擇。
* [下拉式選單](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)：顯示選項選單。例如，下拉式方框。

### 容器

* 面板/容器：將相關的表單元素分組歸類以利整理安排。這是[欄位集](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)和[圖例](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend)的組合。


## 元件屬性

每個表單元件都有不同的屬性，可讓您控制表單的行為和外觀。這裡是最適化表單區塊元件支援的屬性：


| 屬性 | 適用元件 | 詳細資料 |
|--------------|------------------------------|----------------------------------------------------------------------|
| 類型 | 全部 | 指定元件的類型。此屬性決定輸入欄位的行為和外觀。例如，關於文字輸入，類型可以是「文字」、電子郵件輸入是「電子郵件」、密碼輸入是「密碼」。最適化表單區塊支援<a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">所有有效的 HTML5 輸入類型</a>、 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>、 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選取</a>和<a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">欄位集</a>作為類型。 |
| 名稱 | 全部 | 識別表單提交的元件。名稱屬性是將表單資料提交到伺服器時使用，主要是將使用者輸入與特定欄位建立關聯。 |
| 標籤 | 全部 | 向使用者提供內容資訊。標籤是顯示在元件旁邊的文件，主要是指引使用者輸入哪些資訊。 |
| 值 | 文字、密碼、電子郵件、數字、範圍、日期及其變體 (本地日期時間、月、週、時間)、核取方塊、單選、隱藏、提交、按鈕 | 指定元件的初始值。關於文字輸入、textarea 和選取元素，這是顯示的預設文字或選項。關於單選和核取方塊元件，這是選取這些元件時提交的值/資料。值屬性是選項，但核取塊方和單選輸入應被視為強制屬性。 |
| 預留位置 | 文字、電話、電子郵件、密碼、日期 (及其變體，如月、週、時間、本地日期時間)、數字、範圍 | 提供預期輸入的提示。預留位置屬性主要是提供簡短的提示，說明輸入欄位的預期值。用戶開始輸入資料後，此內容就會消失。 |
| 說明 | 全部 | 提供有關元件的更多資訊，並用作說明文字。說明欄位可供進一步說明填寫該元件的目的或指示。此欄位旨在幫助使用者了解輸入欄位的背景。 |
| 可見 | 全部 | 控制最初的可見度。可見度屬性是一種布林值屬性，用來確定表單載入時元件一開始是可看見或是隱藏的。如果設定為 true，則顯示該欄位；否則，欄位會隱藏。 |
| 必要 | 文字、電話、電子郵件、密碼、日期及其變體 (本地日期時間、月、週、時間)、數字、核取方塊、單選、文件、選取 (下拉式選單)、文字區域 | 指示提交前是否必須填寫該欄位。強制屬性是一個布林值屬性，用來指定使用者在提交表單之前是否必須為欄位輸入資料。 |
| 最小 | 日期 (及其變體，如月、週、時間、本地日期時間)、數字、範圍 | 指定允許的最小值。最小屬性設定使用者可以在欄位中輸入的最小值。例如，對於數字輸入，主要是定義可接受的最低數字。 |
| 最大 | 日期 (及其變體，如月、週、時間、本地日期時間)、數字、範圍 | 指定允許的最大值。最大屬性設定使用者可以在欄位中輸入的最大值。例如，對於日期輸入，主要是定義可接受的最高日期。 |
| 接受 | 檔案 | 定義允許的檔案類型。接受屬性是以逗號分隔的唯一檔案類型規範清單，主要是限制使用者可以在檔案輸入欄位中選取的檔案類型。 |
| 多個 | 檔案 | 允許多重選取。多重屬性是與檔案輸入欄位一起使用的布林值屬性。當設定為 true 時，使用者可以選取一個以上的檔案。 |
| 選項 | 下拉式清單 | 指定下拉式選單的選項。選項屬性是一個以逗號分隔的下拉式選單選項列表，主要是定義向使用者顯示的可選取選項。 |
| 已核取 | 核取方塊、單選按鈕 | 確定依預設是否選取該欄位。已勾選屬性是與核取方塊和單選輸入一起使用的布林值屬性。當設定為 true 時，表示表單載入時依預設選取的欄位。 |
| 欄位集 | 全部 | 將欄位分類以在表單中建立視覺效果不同的區段。欄位集元素是將表單中的相關欄位分類，主要是以視覺效果來區分欄位，以便改善組織和使用者的體驗。</br> 若要安排欄位集中的一組欄位，只需使用`fieldset`屬性並指定其名稱屬性。在下面的範例中，我們將示範如何將單選按鈕封裝在單一欄位集內，以更方便安排欄位。![欄位集範例](/help/edge/assets/fieldset-example.png) |
| 可重複 | 全部 | `fieldset` 的布林值屬性，表示特定欄位集可以重複，次數下限為 `Min`，上限為 `Max`。 `Min` 屬性應設為 1 或更大，請勿將 `Min` 屬性設為 0。 |
| 可見度運算式 | 全部 | 可見度運算式是指試算表公式，由 &#39;=&#39; 標記表示，用於控制欄位可見度。在此公式中，只能使用其他欄位的值屬性，以便可以直接管理系統內的欄位可見度。 |
| 值運算式 | 全部 | 值運算式是指試算表公式，由 &#39;=&#39; 標記表示，用於控制欄位的值。在此公式中，只能使用其他欄位的值屬性，以便可以直接管理系統內欄位的值。 |


## 另請參閱

{{see-more-forms-eds}}
