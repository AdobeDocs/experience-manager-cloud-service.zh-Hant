---
title: 開始使用 AEM Edge Delivery Services 上的 Forms
description: 了解如何在 Adobe Experience Manager Edge Delivery Services 上建立和傳遞高效能表單，並強調通用編輯器的製作方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 100%

---


# 開始使用 AEM Edge Delivery Services 上的 Forms

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>
-->

透過 Adobe Experience Manager (AEM) Edge Delivery Services (EDS)，您可以從邊緣提供極快速且高度可擴充的網頁體驗。本指南說明&#x200B;**如何建置和發佈符合這些體驗的表單**，並具備明確的建議階層：

1. **通用編輯器 (UE) – 大多數團隊的最佳選擇**
2. **文件型製作 (文件/試算表)－非常適合快速、簡單的表單**
3. **文件製作 (DA) – 可以將表單嵌入至 DA 製作的頁面中**

最後，您將能選擇正確的製作方法、了解提交選項，並按照後續步驟製作立即可用的表單。



## 選擇製作方法

| 團隊和要求 | 建議方法 | 原因 |
|--------------------|--------------------|-----|
| 行銷人員/設計師需要視覺化控制、條件邏輯或 AEM 整合 | **通用編輯器** | 拖放功能、進階規則、提交至 FSS 或 AEM Publish |
| 內容作者原本已在使用 Word/Google Docs/試算表；簡單地將資料擷取至試算表/電子郵件 | **文件型製作** | 熟悉的工具，製作基本表單的最快途徑 |
| 以&#x200B;**文件製作 (DA)**&#x200B;建置的網站頁面 | 將 UE 或文件型表單&#x200B;**嵌入**&#x200B;至 DA 頁面 | DA 無法自行建置表單 |


## 製作方法詳細資訊

### 通用編輯器

通用編輯器是一款適用於行銷人員和設計師的視覺化拖放式製作工具，兼具速度與企業級效能：

- 即時的所見即所得編輯和裝置預覽。
- 進階規則和驗證 UI—無需程式碼。
- 與 AEM 資產、工作流程及表單資料模型 (FDM) 直接整合。
- 將普通 JS/CSS 中的自訂元件順利移交給開發人員。
- 彈性提交目標：從簡單的 **表單提交服務 (FSS)** 開始，或隨著需求增加切換至 **AEM Publish 提交動作**。

> **建議**：使用通用編輯器開啟每個新表單專案，除非您的團隊完全以文件為中心且表單設計非常樸素。


### 文件型製作 (文件/試算表)

使用如 Microsoft Word、Google Docs 或 Google Sheets 等熟悉的工具來建立簡單、低複雜度的表單者，最適合使用文件型製作。此方法非常適合需要用快速、直接的方式建置表單的內容團隊。

- 使用表格 (文件) 或列 (試算表) 來定義表單欄位。
- 支援基本欄位驗證和 Google reCAPTCHA，以提供垃圾資訊防護。
- 表單提交由表單提交服務專門處理。
- 即時發佈—在來源文件中所做的任何變更，不需要部署管道即會立即反映在網站上。


### 在文件製作 (DA) 中嵌入表單

文件製作 (DA) 旨在建立結構化頁面內容，並不支援原生的表單建立功能。若要將表單新增至以 DA 製作的頁面，請依照下列步驟進行：

1. 使用&#x200B;**通用編輯器** (建議) 或文件型製作建立表單。
2. 發佈表單以產生唯一的 URL (例如 `/forms/contact-us`)。
3. 在您的 DA 頁面中，插入&#x200B;**嵌入表單**&#x200B;區塊並指定已發佈表單的 URL。

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

1. **從通用編輯器開始使用：**&#x200B;請參閱[通用編輯器快速入門指南](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)來開始製作表單。
2. **設定表單提交：**&#x200B;選取並設定您偏好的提交方法。請參閱[表單提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)或 AEM Publish 提交動作，以取得設定說明。
3. **套用最佳做法：**&#x200B;審閱[表單設計最佳做法](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md)，以確保無障礙功能和效能。
4. **使用文件型製作：**&#x200B;若要使用 Microsoft Excel 或 Google Sheets 建立表單，請依照[文件型製作教學課程](/help/edge/docs/forms/tutorial.md)進行。
5. **在文件製作中嵌入表單：** 如果您正在文件製作中建置頁面，請查閱 [DA 教學課程](https://www.aem.live/developer/da-tutorial)以了解有關嵌入已發佈表單的說明。

> **現在，您已準備好使用 AEM Edge Delivery Services 建立第一個高效能表單。**