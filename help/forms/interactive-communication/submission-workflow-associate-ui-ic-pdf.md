---
title: 關聯UI的提交工作流程 — IC產生PDF輸出
description: 瞭解提交和工作流程如何用於Associate UI，並遵循從互動式通訊(IC) JSON產生PDF的工作流程範例。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9d8a33e4-e206-48e6-9daf-b15feb9c67a3
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---

# 關聯使用者介面的提交工作流程

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

本文說明當您為「關聯UI」啟用工作流程時，提交和工作流程如何運作。 然後它會逐步說明如何設定提交工作流程。 逐步解說使用從互動式通訊(IC)裝載產生PDF作為範例；您可以針對其他工作流程型別調整步驟。

<!--
## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).
-->

## 設定提交工作流程

下列步驟說明如何建立工作流程，讓使用者從關聯UI提交時執行該工作流程。 在此我們使用&#x200B;**轉譯IC至PDF**&#x200B;作為範例，搭配現成可用的&#x200B;**IC轉譯PDF輸出**&#x200B;步驟。 當使用者從關聯UI提交時，裝載會傳送至工作流程；此步驟使用裝載中的&#x200B;**communicationDom** (IC-JSON)來產生PDF。

### 承載結構

工作流程會接收JSON裝載。 **communicationDom**&#x200B;欄位包含用於產生PDF的IC-JSON。 **IC轉譯PDF輸出**&#x200B;步驟使用它作為範本輸入。

| 欄位 | 說明 |
|-------|-------------|
| communicationDom | 適用於PDF世代的IC-JSON |
| auditMetadata | 稽核資訊 |
| submitdata | 提交的表單資料(JSON) |
| prefillData | 預填資料(JSON) |
| referer， cookie， queryString， clientIP， userAgent， formSubmitter | 請求中繼資料 |

### 建立工作流程模型

1. **基本：**&#x200B;建立工作流程模型（例如，將工作流程新增為&#x200B;**pdfrenderworkflow**）。

   ![工作流程模型基本索引標籤](/help/forms/assets/associate-ui-add-workflow.png)

1. **變數：**&#x200B;新增符合承載和步驟的變數： **communicationDom** (JSON)、**auditMetadata** (JSON)、**outputDocument** （檔案）。

   ![工作流程變數](/help/forms/assets/associate-ui-add-variables.png)

1. **步驟：**&#x200B;新增&#x200B;**IC轉譯PDF輸出**&#x200B;步驟。
   ![新增工作流程步驟](/help/forms/assets/associate-ui-add-step.png)

1. 在它的&#x200B;**Input**&#x200B;索引標籤中，將&#x200B;**Select範本(JsonObject)**&#x200B;設定為&#x200B;**變數** → **communicationDom**。 儲存步驟和模型。

   ![IC轉譯PDF輸出 — 輸入索引標籤](/help/forms/assets/associate-ui-input-variable.png)

1. 在其&#x200B;**輸出**&#x200B;索引標籤中，將&#x200B;**選取範本(JsonObject)**&#x200B;設定為&#x200B;**變數** → **communicationDom**。 儲存步驟和模型。

   ![工作流程變數和畫布](/help/forms/assets/assocaite-ui-output-variable.png)

### 將工作流程連線到關聯UI

在[啟用並設定關聯UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)中，啟用關聯檢視，並在&#x200B;**工作流程**&#x200B;中，將&#x200B;**設定更新的工作流程**&#x200B;設定為開啟，並選取此工作流程模型。 發佈IC並[整合關聯UI](/help/forms/interactive-communication/invoke-associate-ui.md)，所以提交會觸發此工作流程。

![互動式通訊設定 — 關聯UI的工作流程組態](/help/forms/assets/associate-ui-configure-workflow.png)

啟用&#x200B;**外部化工作流程資料儲存**&#x200B;時，請設定外部器，讓工作流程資料儲存在您的外部儲存空間（例如Azure）。 請參閱[外部化工作流程資料](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)。

## 另請參閱

- [在互動式通訊編輯器中建立UI關聯](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [啟用並設定互動式通訊的關聯UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [在您的應用程式中整合關聯UI](/help/forms/interactive-communication/invoke-associate-ui.md)
- [外部化工作流程資料](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)
