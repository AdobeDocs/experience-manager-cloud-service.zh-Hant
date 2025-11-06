---
title: 表單體驗建立工具
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 183e999c-9896-49a2-b29b-7c77da380df9
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 32%

---

# 概觀

AEM Forms Experience Builder運用Generative AI透過自然語言加速數位表單的建立。 這項功能強大的工具可讓技術和非技術使用者透過簡單的對話式介面，設計、修改和最佳化專業級表格。

Forms Experience Builder可透過對話式人工智慧快速建立表單，同時讓非技術使用者無需編碼知識即可建立複雜表單。 您可以設計複雜的版面、實作驗證規則，以及透過簡單的對話命令來設定提交動作。

## 核心功能

表單體驗建立工具提供兩種用於建立強大數位表單的主要工作流程：

### AI支援表單建立

**以自然語言產生表單**

使用簡單的英語描述，從頭開始建立完整的表單。只需描述您的需求，例如「建立包含評分量表和評論欄位的客戶回饋表單」，表單體驗建立工具就會產生適當的表單結構。您可以使用視覺編輯器的體驗建立工具新增更多欄位、驗證規則和提交邏輯。

**動態欄位管理**

透過對話式命令新增、修改或移除表單欄位。AI 會理解內容，並且可以根據您的需求智慧地建議欄位類型、驗證規則和使用者介面改善。

**版面最佳化**

透過自然語言更新表單版面和設定。請求變更，例如「將表單版面變更為精靈版面」，表單體驗建立工具便會套用適當的樣式和版面調整。

### 智慧型匯入和轉換

將現有檔案轉換為互動式數位體驗。 Forms Experience Builder支援各種格式，可分析上傳的內容以偵測欄位型別、保留版面，並透過回應式設計和進階邏輯增強表單。 支援的格式包括：

- **Acroforms**：具有現有欄位結構的互動式 PDF 表單
- **XFA PDF**：XML 型的複雜表單架構
- **平面 PDF**：靜態文件轉換為互動式表單
- **影像和熒幕擷取畫面**： JPG、PNG格式
- **手繪表單**：草圖與紙本表單照片


## Forms Experience Builder展示 {#forms-experience-builder-demo}

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

## 入門與必要條件

Forms Experience Builder目前可透過搶先使用程式取得。 若要要求存取權，請從您的正式電子郵件識別碼傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。

Experience Builder需要具有[最適化AEM Forms as a Cloud Service核心元件](/help/forms/enable-adaptive-forms-core-components.md)的Forms生產製作環境。

## 存取表單體驗建立工具


1. 導覽至&#x200B;**AEM > Forms > Forms與檔案**。
1. 按一下&#x200B;**建立**&#x200B;並選取&#x200B;**最適化表單**
1. 使用精靈，根據您的需求使用[核心元件範本](/help/forms/creating-adaptive-form-core-components.md)或[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)範本建立新表單，並開啟表單進行編輯。
1. 在編輯器工具列中選取&#x200B;**Forms Experience Builder**&#x200B;圖示，開啟Forms Experience Builder介面以使用自然語言建立表單。


| ![最適化Forms編輯器 — Forms Experience Builder](/help/edge/docs/forms/assets/adaptive-forms-editor.gif "最適化Forms編輯器 — Forms Experience Builder") | ![通用編輯器 — Forms Experience Builder](/help/forms/assets/ue-forms-experience-builder.gif "通用編輯器 — Forms Experience Builder") |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| *自適應表單編輯器* | *通用編輯器* |

<!-- >

## Learn more on key capabilities {#key-capabilities-forms-experience-builder}

<table>
<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
   <img alt="Getting started with Forms Experience Builder" src="./assets/getting-started.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-getting-started.md">
      <strong>Getting started with Forms Experience Builder</strong>
      </a>
   </div>
   <p>
      <em>Learn the basics of creating your first form using AI-powered capabilities.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
   <img alt="LLM-enhanced smart fields" src="./assets/llm-smart-fields.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-llm-smart-fields.md">
      <strong>LLM-enhanced smart fields</strong>
      </a>
   </div>
   <p>
      <em>Learn how to create fields with pre-populated options using AI knowledge base.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
   <img alt="AI-powered form creation" src="./assets/ai-form-creation.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md">
      <strong>AI-powered form creation</strong>
      </a>
   </div>
   <p>
      <em>Learn how to utilize natural language to create and modify forms.</em>
   </p>
</td>
</table>

<table>
<td>
   <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
   <img alt="Intelligent import and conversion" src="./assets/intelligent-import.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/intelligent-import-conversion.md">
      <strong>Intelligent import and conversion</strong>
      </a>
   </div>
   <p>
      <em>Learn how to transform existing documents into interactive digital forms</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/form-submission-integration.md">
   <img alt="Form submission and integration" src="./assets/form-submission.png" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/form-submission-integration.md">
      <strong>Form submission and integration</strong>
      </a>
   </div>
   <p>
      <em>Learn how to configure form submissions to integrate with your business systems.</em>
   </p>
</td>

<td>
   <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
   <img alt="Forms Experience Builder frequently asked questions" src="./assets/faq-banner.jpg" />
   </a>
   <div>
      <a href="/help/forms/experience-builder/forms-experience-builder-frequently-asked-questions.md">
      <strong>Frequently asked questions</strong>
      </a>
   </div>
   <p>
      <em>Get responses to common questions about Forms Experience Builder capabilities and usage.</em>
   </p>
</td>
</table> -->



<!--
**Comprehensive Submit Action Configuration**

Configure form submissions to integrate with your existing business systems:

- **Email Integration**: Set up automated email notifications and confirmations
- **REST API Endpoints**: Connect to custom applications and services
- **Cloud Storage**: Integrate with Azure Blob Storage, SharePoint, and OneDrive
- **Workflow Automation**: Connect to Power Automate and Workfront Fusion
- **Marketing Platforms**: Direct integration with Marketo for lead management
- **AEM Workflows**: Leverage existing AEM workflow capabilities
-->


## 開始探索

以下是您可以開始探索Forms Experience Builder的幾種方法：

- **逐步建置表單**：從簡單的表單開始，並逐步增加複雜性。 例如，建立基本連絡人表單，然後新增驗證規則、預留位置文字和條件式邏輯。 [了解更多](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#incremental-development-examples)。

- **建立智慧欄位**：利用AI的知識建立具有預先填入的內容感知選項的欄位，例如所有國家、主要機場或業界標準職銜的下拉式清單。 [了解更多](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#llm-enhanced-smart-fields)。

- **實作複雜的商業邏輯**：定義根據使用者輸入顯示或隱藏表單區段的條件式規則。 例如，建立只有在使用者的婚姻狀況為「已婚」時才顯示「配偶資訊」區段的規則。 [了解更多](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)。

- **與您的系統整合**：設定表單提交以與您現有的業務工作流程連結，不論是傳送資料至REST API、在您的CRM中建立新的銷售機會，還是將檔案儲存至雲端儲存空間。 [了解更多](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md#data-integration--submission)。

<!-- ## Onboarding

The Forms Experience Builder is currently available through an Early Access Program. To request access, follow these steps:

1. **Gather your information**: You will need the following details:
    - IMS Organization ID
    - Program ID
    - Project Details (timeline, scope, use cases)
    - Your Official Work Email

   If you need help finding your IMS Organization ID and Program ID, refer to the [Adobe Experience Cloud Organization Setup Guide](/help/onboarding/cloud-manager-introduction.md) and the [Program and Environment Management](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) documentation.

2. **Send an access request**: Email [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) with all the information gathered in the previous step. 

    Access to the Forms Experience Builder is limited and subject to approval based on program capacity and alignment with early access criteria. 

## Getting started

To get started with the Forms Experience Builder, visit the [Forms Experience Builder documentation](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

-->
