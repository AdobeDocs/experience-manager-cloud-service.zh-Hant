---
title: 如何設定最適化表單的提交動作？
description: 最適化表單提供多個提交動作。提交動作會定義提交之後處理最適化表單的方式。您可以使用內建的提交動作或建立自己的動作。
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 58%

---


# 提交最適化Forms支援的動作

最適化表單可讓您建立吸引人、回應式、動態且最適化的表單。這些模組提供直覺式使用者介面和一組現成可用的元件，讓您有效率地設計和管理表單。 您可以設定各種提交動作，將表單資料傳送至OneDrive、SharePoint、Workfront Fusion等服務。

當使用者按一下最適化表單上的&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕時，就會觸發提交動作。 Forms as a Cloud Service提供數種立即可用的提交動作。 內建的提交動作可讓您：

* 透過電子郵件輕鬆傳送表單資料
* 在傳輸資料時啟動Microsoft®Power Automate流程或AEM工作流程。
* 直接將表單資料傳輸至Microsoft®SharePoint Server、Microsoft®Azure Blob Storage或Microsoft® OneDrive。
* 使用表單資料模型(FDM)，順暢地將資料傳送至已設定的資料來源。
* 方便地將資料提交到 REST 端點。

## 提交最適化Forms支援的動作

AEM forms提供下列立即可用的提交動作：

* [寄送電子郵件](/help/forms/configure-submit-action-send-email.md)
* [叫用 Power Automate 流程](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [叫用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [使用表單資料模型 (FDM) 提交](/help/forms/using-form-data-model.md)
* [提交到 Azure Blob 儲存體](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交到 REST 端點](/help/forms/configure-submit-action-restpoint.md)
* [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [叫用 AEM 工作流程](/help/forms/configure-submit-action-workflow.md)
* [提交至Marketo enagage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [提交至Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [提交至試算表](/help/forms/forms-submission-service.md)

您也可以將最適化表單提交至其他儲存設定：

* [將最適化表單連結到 Salesforce 應用程式](/help/forms/aem-forms-salesforce-integration.md)
* [將最適化表單連結到 Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

## 跨撰寫型別提交動作支援

下表顯示根據AEM Forms中使用的表單製作方法支援哪些提交動作：

| 提交動作 | [Foundation 元件](/help/forms/configuring-submit-actions.md) | [核心元件](/help/forms/configure-submit-actions-core-components.md) | [通用編輯器](/help/forms/configure-submit-action-eds-forms.md#submit-actions-supported-by-adaptive-forms-created-in-universal-editor) | [以檔案為基礎的Forms](/help/forms/configure-submit-action-eds-forms.md#supported-submit-actions-for-document-based-forms) |
|----------------------------|------------------------|------------------|------------------|------------------------|
| 傳送電子郵件 | ✅支援 | ✅支援 | ✅支援 |                        |
| Power Automate流程 | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交到 SharePoint | ✅支援 | ✅支援 | ✅支援 |                        |
| Workfront Fusion | ✅支援 | ✅支援 | ✅支援 |                        |
| 使用FDM提交 | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交至AEP | ✅支援 | ✅支援 | ✅支援 |                        |
| Azure Blob儲存體 | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交至REST端點 | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交至 Marketo Engage | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交到 OneDrive | ✅支援 | ✅支援 | ✅支援 |                        |
| 呼叫 AEM 工作流程 | ✅支援 | ✅支援 | ✅支援 |                        |
| 提交至試算表 |                        |                  | ✅支援 | ✅支援 |


## 最適化表單中的伺服器端重新驗證

一般而言，在任何線上資料擷取系統中，開發人員都會在用戶端放置一些 JavaScript 驗證，以強制執行一些業務規則。但在現代的瀏覽器中，一般使用者可以略過那些驗證，並使用各種技巧 (例如 Web Browser DevTools Console) 手動進行提交。此類技術對於最適化表單也有效。表單開發人員可以建立各種驗證邏輯，但技術上而言，一般使用者可以略過那些驗證邏輯並提交無效的資料給伺服器。無效的資料會破壞表單作者強制執行的業務規則。

伺服器端重新驗證功能也能夠執行最適化表單作者在伺服器上設計最適化表單時提供的驗證能力。這樣可以避免對提交的資料造成任何可能的危害，以及在表單驗證方面違反業務規則。


### 伺服器上會進行哪些驗證？

會在伺服器上對最適化表單重新執行的所有立即可用 (OOTB) 欄位驗證包括：

* 必填
* 驗證圖片子句
* 驗證運算式

使用在側邊欄「最適化表單容器」下方的「**[!UICONTROL 在伺服器上重新驗證]**」，即可對目前表單啟用或停用伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

**啟用伺服器端驗證**

如果一般使用者略過那些驗證並提交表單，伺服器將再次執行驗證。如果伺服器端驗證失敗，就會停止提交交易。使用者會再次看到原始表單。 擷取的資料和提交的資料會做為錯誤呈現給使用者。

>[!NOTE]
>
>伺服器端驗證會驗證表單模型。建議您建立獨立的用戶端程式庫已進行驗證，並避免與相同用戶端程式庫中其他內容混淆，例如 HTML 樣式和 DOM 操作等。

<!--### Supporting Custom functions in Validation Expressions {#supporting-custom-functions-in-validation-expressions-br}

At times, if there are **complex validation rules**, the exact validation script reside in custom functions and author calls these custom functions from field validation expression. To make this custom function library known and available while performing server-side validations, the form author can configure the name of AEM client library under the **[!UICONTROL Basic]** tab of Adaptive Form Container properties as shown below.

![Supporting Custom functions in Validation Expressions](assets/clientlib-cat.png)

Supporting Custom functions in Validation Expressions

Author can configure customJavaScript library per Adaptive Form. In the library, only keep the reusable functions, which have dependency on jquery and underscore.js third-party libraries.

Refer to the following articles to learn how to create custom functions for:

* [Adaptive Forms based on Foundation Components](/help/forms/rule-editor.md#custom-functions-in-rule-editor)
* [Adaptive Forms based on Core Components](/help/forms/create-and-use-custom-functions.md)
* [Adaptive Forms authored using Document-Based Authoring](/help/edge/docs/forms/rules-forms.md#create-a-custom-function)
* [Adaptive Forms created using the Universal Editor](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#create-a-custom-function)

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.-->

## 另請參閱

{{af-submit-action}}

