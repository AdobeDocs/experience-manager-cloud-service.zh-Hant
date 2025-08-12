---
title: 如何設定最適化表單的提交動作？
description: 最適化表單提供多個提交動作。提交動作會定義提交之後處理最適化表單的方式。您可以使用內建的提交動作或建立自己的動作。
keywords: 如何選取最適化表單的提交動作、將最適化表單連線至sharepoint清單、將最適化表單連線至sharepoint檔案庫、將最適化表單連線到表單資料模型(FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 47%

---

# 最適化表單提交動作

| 版本 | 文章連結 |
|---------|-----------------------------|
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service （基礎元件） | [按一下這裡](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service （核心元件） | [按一下這裡](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | 本文章 |


表單提交是使用者歷程中關鍵的最後步驟，就是在這時候處理所收集的資料並採取行動。此文件提供在通用編輯器中設定和管理自適應表單提交動作的綜合指南。

## 學習內容

本文件閱讀完畢後，您將了解如何進行以下事項：

- 為表單設定不同類型的提交動作
- 設定 REST 端點提交以便與外部系統整合
- 設定電子郵件提交以獲得表單回覆
- 實施自訂提交動作以滿足特定業務需求
- 處理提交期間的表單驗證和錯誤情況

## 目標讀者

本指南適用於以下人員：

- 實施提交邏輯的&#x200B;**表單開發人員**
- 將表單連接到後端系統的&#x200B;**系統整合商**
- 定義表單工作流程的&#x200B;**業務分析人員**
- 設計表單提交流程的&#x200B;**技術架構者**

## 針對在通用編輯器中建立的Forms提交動作

下列提交動作受到在Universal Editor[中編寫的](/help/edge/docs/forms/universal-editor/create-forms.md)最適化Forms支援：

- [寄送電子郵件](/help/forms/configure-submit-action-send-email.md)
- [叫用Power Automate流程](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [叫用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [使用表單資料模型 (FDM) 提交](/help/forms/integrate-adaptive-form-with-fdm.md)
- [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交至REST端點](/help/forms/configure-submit-action-restpoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [叫用 AEM 工作流程](/help/forms/configure-submit-action-workflow.md)
- [提交至 Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [提交至Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [提交至試算表](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

您可以使用&#x200B;**編輯表單屬性**&#x200B;擴充功能的&#x200B;**提交**&#x200B;索引標籤，為在Universal Editor中建立的表單設定提交動作。

**如何設定在Universal Editor中編寫之Forms的提交動作？**
您可以使用**編輯表單屬性**&#x200B;擴充功能的&#x200B;**提交**&#x200B;索引標籤，為在Universal Editor中建立的表單設定提交動作。

![表單屬性圖示](/help/forms/assets/ue-form-properties-icon.png)

![通用編輯器表單屬性](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
> - 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。
