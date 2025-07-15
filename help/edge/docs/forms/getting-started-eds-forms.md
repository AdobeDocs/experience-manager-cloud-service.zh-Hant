---
title: 開始使用 AEM Edge Delivery Services 上的 Forms
description: 瞭解如何在Adobe Experience Manager Edge Delivery Services上建立和傳遞高績效表單，並強調Universal Editor編寫方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 5%

---


# 開始使用 AEM Edge Delivery Services 上的 Forms

<span class="preview">這是透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hant#new-features">發行前通道</a>提供的發行前功能。</span>

Adobe Experience Manager (AEM) Edge Delivery Services (EDS)可讓您從邊緣提供極快速、高度擴充的Web體驗。 本指南說明&#x200B;**如何建置和發佈這些體驗的表單** — 具有明確的建議階層：

1. **Universal Editor (UE) — 大多數團隊的最佳選擇**
2. **檔案式製作（檔案/工作表） — 適用於快速、簡單的表單**
3. **Document Authoring (DA) — 使用將表單內嵌至DA編寫的頁面**

到最後，您將能夠選擇正確的撰寫方法、瞭解提交選項，並遵循後續步驟以建立生產就緒的表單。



## 選擇編寫方法

| 團隊與需求 | 建議的方法 | 原因 |
|--------------------|--------------------|-----|
| 行銷人員/設計人員需要視覺控制、條件邏輯或AEM整合 | **通用編輯器** | 拖放、進階規則、提交至FSS或AEM Publish |
| 內容作者已在Word/Google Docs/工作表中工作；將簡單資料擷取至試算表/電子郵件 | **檔案式製作** | 熟悉的工具，最快速的基本表單路徑 |
| 內建於&#x200B;**檔案製作(DA)**&#x200B;中的網站頁面 | **將UE或檔案型表單內嵌**&#x200B;至DA頁面 | DA不會建置表單本身 |


## 詳細編寫方法

### 通用編輯器

Universal Editor是行銷人員和設計人員適用的視覺化拖放式撰寫工具，結合速度與企業級效能：

* 即時WYSIWYG編輯和裝置預覽。
* 進階規則和驗證UI — 不需要程式碼。
* 與AEM資產、工作流程和表單資料模型(FDM)直接整合。
* 原始版JS/CSS中自訂元件的無縫交接給開發人員。
* 彈性的提交目標：使用&#x200B;**Forms提交服務(FSS)**&#x200B;開始簡單作業，或隨著您的需求成長切換至&#x200B;**AEM發佈提交動作**。

> **建議**：除非您的團隊是100%以檔案為中心且表單非常基本，否則請使用通用編輯器開始每個新表單專案。


### 檔案式製作（檔案/工作表）

檔案式製作最適合使用熟悉的工具(例如Microsoft Word、Google Docs或Google Sheets)來建立簡單、低複雜度的表單。 此方法適用於需要快速且簡單方式建立表單的內容團隊。

* 定義表格（檔案）內的表單欄位或列數（頁面）。
* 支援基本欄位驗證和Google reCAPTCHA的垃圾郵件保護。
* 表單提交僅透過Forms提交服務處理。
* 即時發佈 — 在來原始檔中所做的任何變更都會立即反映在網站上，而無需部署管道。


### 將Forms內嵌於檔案製作(DA)

檔案製作(DA)是專為建立結構化頁面內容而設計，不支援原生表單建立。 若要將表單新增至DA編寫的頁面，請執行下列步驟：

1. 使用&#x200B;**通用編輯器** （建議使用）或檔案式撰寫來建立表單。
2. 發佈表單以產生唯一URL （例如，`/forms/contact-us`）。
3. 在您的DA頁面中，插入&#x200B;**內嵌表單**&#x200B;區塊，並指定已發佈表單的URL。

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## 後續步驟

1. **從通用編輯器開始：**&#x200B;請參閱[通用編輯器快速入門手冊](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)以開始編寫表單。
2. **設定表單提交：**&#x200B;選取並設定您偏好的提交方法。 如需設定指示，請參閱[Forms提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)或AEM發佈提交動作。
3. **套用最佳實務：**&#x200B;檢閱[表單設計最佳實務](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md)，以確保協助工具與效能。
4. **使用檔案式製作：**&#x200B;若要使用Microsoft Excel或Google工作表建立表單，請遵循[檔案式製作教學課程](/help/edge/docs/forms/tutorial.md)。
5. **在檔案製作中內嵌Forms：**&#x200B;如果您在檔案製作中建置頁面，請參閱[DA教學課程](https://www.aem.live/developer/da-tutorial)以取得內嵌已發佈表單的說明。

> **您現在已準備好使用AEM Edge Delivery Services建立您的第一個高效能表單。**