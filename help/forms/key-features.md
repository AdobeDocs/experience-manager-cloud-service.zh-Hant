---
title: 'Adobe Experience Manager(AEMForms)as a Cloud Service '
description: '"[!DNL AEM Forms] as a Cloud Service是建立、管理、發佈企業級表單和業務流程的平台。」'
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->

# 關鍵特性和功能 {#key-features}

[!DNL AEM Forms] as a Cloud Service提供了多種雲本地功能，如雲本地體系結構、自動擴展、升級零停機、CDN（內容交付網路）、雲本地開發環境，以及通過雲管理器為環境自助服務的能力。 您可以使用該服務：

* [建立自適應Forms](creating-adaptive-form.md#strong-create-an-adaptive-form-strong) 自動呈現給用戶設備和瀏覽器。

   ![調適型表單](assets/rule-editor-example.gif)

* [建立像素完美PDF forms](use-forms-designer.md#create-an-adaptive-form) 看起來就像紙。

* 使用 [automated forms conversion服務](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html) 的子菜單。 它幫助您加快組織資料捕獲體驗的數字化和現代化。

   ![automated forms conversion服務](assets/pdf-to-adaptive-form-gitx50.gif)

* [建立業務流程](aem-forms-workflow-step-reference.md#create-form-centric-workflows)。 例如，您可以在提交自適應表單時建立和觸發審批和拒絕工作流。

除上文 [!DNL AEM Forms] as a Cloud Service提供以下功能和功能：

* 易於使用的圖形用戶介面，使業務用戶能夠輕鬆導入、管理、預覽和發佈表單
* 具有使用關鍵字、標籤和元資料的強大搜索功能的響應表單目錄
* 動態檢測用戶設備和位置以在網路和移動通道上適當地呈現表單
* [與Adobe Sign](adobe-sign-integration-adaptive-forms.md) 服務或Scribble以電子方式簽署包含機密資訊的文檔
* 能夠 [將服務連接到各種類型的資料源](data-integration.md#create-an-adaptive-form) 發送和檢索資料。 該服務支援從REST風格的Web服務、基於SOAP的Web服務和啟用OData的服務發送和檢索資料。
* 與AEM Sites整合。 它允許在AEM Sites頁面中嵌入自適應表單。 您還可以將自適應表單整合到任何網頁。
* 能夠建立記錄文檔(DoR)，以保留您提供的資訊的記錄並以自適應表單提交，以便您以後可以參考它。 DoR是表單的PDF版本。 它包括模板和資料。 該服務提供預設的DoR模板和工具來開發自定義模板。
* 能夠建立自適應Forms以生成符合模式的資料。 它幫助您將捕獲的資料提交到現有流程和資料源，而無需進行任何或最少的修改。
* 能夠建立預填服務以根據條件用現有客戶資料填寫表單。 該方法可加快成型過程，降低廢品率。


<!-- 

## Enterprise-class forms {#enterprise-class-forms}

You can create enterprise class forms (Adaptive Forms) and deliver beautiful, interactive, responsive, and personalized experiences to your customers. These forms change behavior and appearance based on the underlying device. You can also use themes and templates with Adaptive Forms to mandate a uniform structure and appearance for all the forms of an organization or a department.

![Creating custom patterns for fields in CrxDe](assets/adaptive-form.png)

## Automatic conversion of PDF forms to Adaptive Forms {#automatic-conversion-of-pdf-forms-to-adaptive-forms}

You can use Automated Forms Conversion service to convert a PDF Form to an Adaptive Form. It helps you accelerate digitization and modernization of data capture experiences of your organization.

![Creating custom patterns for fields in CrxDe](assets/pdf-to-adaptive-form-gitx50.gif)

## Data Integration {#data-integration}

You can connect the service to various types of data sources to send and retrieve data. The service supports sending and retrieving data from RESTful web services, SOAP-based web services, and OData enabled services.

![Build dynamism and interactivity to Adaptive Forms](assets/rule-editor-example.gif)

## Integration with [!DNL Adobe Sign] {#integration-with-adobe-sign}

 You can integrate the service with [!DNL Adobe Sign] and add [!DNL Adobe Sign] fields to an Adaptive Form. It allows your users to e-sign an Adaptive Form and use [!DNL Adobe Sign] with AEM Workflows. You can use AEM Workflows to develop a business logic and send forms and documents to recipients for signatures based on the business logic.

![Creating custom patterns for fields in CrxDe](assets/adobe-sign.png)


## Integration with [!DNL AEM Sites] {#integration-with-aem-sites}

You can embed an adaptive form in an AEM Sites or an external webpage. The service provides a component out of the box to integrate an adaptive forms to an AEM Sites page.

![integrate an adaptive forms to an AEM Sites page](assets/integrate.png)

## Business Processes Automation {#bpa}

You can use AEM Workflows to create business processes and automate operations. For example, You can create and trigger an approval and rejection workflow on submission of an Adaptive Form. 

![Create and trigger an approval and rejection workflow](assets/workflow.png)

## Document of Record {#dor}

You can create a Document of Record (DoR) to keep a record of the information that you provide and submit in an Adaptive Form so that you can refer to it later. A DoR is a PDF version of a form. It includes both a template and data. The service provides a default DoR template and tools to develop a custom template.

![Build dynamism and interactivity to Adaptive Forms](assets/designer.png)

## Rule editor {#rule-editor}

Rule editor empowers you to build dynamism and interactivity to Adaptive Forms. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps  streamline the form filling experience while ensuring accuracy and speed.
  
![Creating custom patterns for fields in CrxDe](assets/form-data-model.png)


## WYSIWYG editors {#wysiwyg-editor} 

The service provides several WYSIWYG editors: Adaptive Forms editor, Theme editor, and Template editor. These help you create and edit forms and related assets in WYSIWYG manner. The editors also provide out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations.

![Creating custom patterns for fields in CrxDe](assets/emulators.png)

## Schema-compliant data {#schema-complaint-data}

You can create Adaptive Forms to produce schema-compliant data. It helps you submit captured data to existing processes and data sources without any or minimal modifications.

![Build dynamism and interactivity to Adaptive Forms](assets/display-validation-error.gif)

## Prefill a form

You can create a prefill service to fill a form with existing customer data based on a criteria. It helps fasten the form filling process and reduce the abandon rate.

## Submit Actions

A Submit Action allows you to persist and process captured data. The service provides several Submit Actions out-of-the-box. You can use these Submit Actions to send submitted data to a REST endpoint, database, or an AEM Workflow. You can also email submitted data along with attachments and Document of Record(DoR). You can also develop a custom Submit Action to perform an action specific to your business.

* **Emulators:** You can view an Adaptive Form in an in-built emulator. It helps you simulate how an Adaptive Form appears on different devices to an end user. It provides out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations. 

In addition to standard [!DNL AEM Forms] features, [!DNL AEM Forms] as a Cloud Service provides several cloud-native capabilities such as a cloud-native architecture, auto-scaling, zero downtime for upgrades, a CDN (Content Delivery Network), cloud-native development environment, and ability to self-Service the environments via Cloud Manager. -->
