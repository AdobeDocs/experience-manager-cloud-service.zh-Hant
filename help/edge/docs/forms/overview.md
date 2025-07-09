---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: 瞭解如何使用Edge Delivery Services透過AEM Forms建立及傳遞高效能表單，以實現快速開發及簡化資料收集。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 8%

---


# AEM Forms 適用的 Edge Delivery Services


AEM Forms 適用的 Edge Delivery Services 是一套可組合的服務，提供快速開發環境讓作者迅速更新、發佈並推出新表單。這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

* **更快的體驗：** Forms是由全域內容傳遞網路(CDN)提供，確保使用者能快速載入。
* **快速開發：**&#x200B;簡化的開發程式可加快更新速度。 變更可以發佈，而不需要等待漫長的管道建置。
* **彈性撰寫：**&#x200B;選擇多種工具來建立表單，包括檔案式撰寫(Microsoft Word、Google Docs/工作表)或視覺化WYSIWYG編輯器（通用編輯器）。

## 運作方式

透過Edge Delivery Services，您的表單結構和內容可位於AEM as a Cloud Service、Microsoft SharePoint或Google Drive等來源。 此內容會發佈至全域CDN。 當使用者造訪您的網站時，會直接從最近的CDN邊緣伺服器提供表單，以獲得最佳效能。

![顯示內容來源、CDN和使用者的簡化架構圖。](/help/forms/assets/eds-simplified-architecture.png)
**簡化的Edge Delivery Services架構搭配Forms**

使用者提交的資料可傳送至不同的目的地，從簡單的試算表到強大的AEM後端以供進一步處理。

## 選擇編寫方法

您有數種方式可為Edge Delivery Services網站建立表單。 最佳方法取決於您團隊的技能、表單的複雜度以及您的專案需求。

![協助選擇表單撰寫方法的決策樹。](/help/forms/assets/eds-authoring-selection.png)
**表單撰寫決策樹**

### 文件型編寫

此方法可讓您[使用Microsoft Word或Google Docs/工作表](/help/edge/docs/forms/create-forms.md)建立表單。 您可以使用特定的表格格式在檔案中定義表單欄位、標籤和型別。 Edge Delivery Services會將此檔案轉換為互動式HTML表單。

**功能：**

* 在熟悉的工具中撰寫：Word、Google Docs或Google Sheets。
* 定義文字輸入、電子郵件、下拉式清單、核取方塊和選項按鈕等欄位。
* 設定基本驗證規則，例如必填欄位。
* 整合Google reCAPTCHA以防護垃圾郵件。
* 支援檔案上傳。
* 將資料直接提交至試算表或電子郵件地址。
* 透過GitHub的自訂程式碼擴充以使用進階元件和樣式。

**最適合：**

* 主要使用檔案編輯器建立內容的團隊。
* 快速建立從簡單到中等複雜的表單。
* 將簡單的資料收集轉換為試算表或電子郵件。

來自檔案式表單的提交通常由[AEM Forms提交服務](/help/forms/forms-submission-service.md)處理，該服務會將資料路由到已設定的試算表或電子郵件地址。

### 通用編輯器製作

[Universal Editor提供現代的WYSIWYG介面](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)，用於建立具有拖放體驗的表單。

**功能：**

* 使用預先建立的元件庫以視覺化的拖放方式建立表單。
* 設定即時驗證和複雜的商業邏輯（例如，根據使用者選擇顯示/隱藏欄位）。
* 不同裝置的即時預覽。
* 與AEM as a Cloud Service功能(例如內容片段、AEM工作流程和使用者許可權)的深度整合。
* 透過「體驗產生器」由AI協助建立及編輯表單。

**最適合：**

* 使用條件式邏輯、多步驟面板或個人化來建置複雜表單。
* 偏好視覺工具的團隊（例如行銷人員、業務使用者）。
* 需要與AEM後端高度整合的專案，以進行資料處理和工作流程。

使用Universal Editor建置的Forms可以使用[Forms Submission Service](/help/forms/forms-submission-service.md)，或設定為使用由OOTB提供的[提交動作以進行進階資料處理](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)，例如傳送資料至AEM Workflow、REST端點或資料庫。

### 在檔案編寫頁面中內嵌Forms

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial)是Adobe代管服務，用於管理Edge Delivery Services的網站內容。 雖然DA本身並非表單建立工具，但您可以用它來製作網頁，然後內嵌以其他方法建立的表單。

**運作方式：**

1. **建立表單：**&#x200B;使用檔案式撰寫或通用編輯器建置您的表單。
2. **發佈表單：**&#x200B;請確定表單已發佈，且可從自己的URL存取。
3. **內嵌於DA：**&#x200B;在檔案編寫頁面上，新增參考表單URL的區塊以內嵌它。

這種方法適用於使用檔案製作作為Edge Delivery Services網站主要內容管理系統的團隊。

## 製作方法比較

| 條件 | 文件型編寫 | 通用編輯器(WYSIWYG) | 檔案製作(DA)中的Forms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要撰寫工具** | Word/Google Docs/工作表 | 瀏覽器(AEM通用編輯器) | 不適用(Forms為&#x200B;*內嵌*) |
| **團隊技能等級** | 熟悉檔案編輯器 | 熟悉視覺化網頁工具 | 使用DA處理頁面內容 |
| **一般表單複雜度** | 從簡單到中等 | 中等到複雜，企業級 | 取決於內嵌表單 |
| **提交選項** | Forms提交服務（至工作表/電子郵件） | Forms提交服務、AEM發佈（工作流程、表單資料模型、協力廠商整合） | 遵循內嵌表單的設定 |
| **AEM後端整合** | 最小 | 高(透過AEM發佈提交) | 透過內嵌式通用編輯器表單間接取得 |
| **最適合……** | 內容團隊快速建立簡單表單，快速資料擷取。 | 需要視覺控制、複雜表單或深入AEM整合的行銷人員和業務使用者。 | 在DA中管理主要內容的網站。 |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## 後續步驟

* [使用檔案式撰寫功能建立表單](/help/edge/docs/forms/tutorial.md)
* [瞭解Forms的Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [設定表單提交動作](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [瞭解檔案製作(DA)](https://www.aem.live/developer/da-tutorial)
