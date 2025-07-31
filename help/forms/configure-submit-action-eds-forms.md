---
title: 如何設定最適化表單的提交動作？
description: 最適化表單提供多個提交動作。提交動作會定義提交之後處理最適化表單的方式。您可以使用內建的提交動作或建立自己的動作。
keywords: 如何選取最適化表單的提交動作、將最適化表單連線至sharepoint清單、將最適化表單連線至sharepoint檔案庫、將最適化表單連線到表單資料模型(FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 19%

---


# 提交適用於Edge Delivery Services Forms的動作

| 版本 | 文章連結 |
|---------|-----------------------------|
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service （基礎元件） | [按一下這裡](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service （核心元件） | [按一下這裡](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | 本文章 |

提交動作可定義使用者提交表單時所發生的情況，例如儲存資料、觸發工作流程或與協力廠商系統整合。 您可以設定的提交動作型別取決於用來建立Edge Delivery Services Forms的編寫方法。

您可以使用[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)或使用[Document Based Forms](/help/edge/docs/forms/overview.md)編寫來建立Edge Delivery Services Forms，並相應地使用不同的提交動作來設定表單。

## 針對在通用編輯器中建立的Forms提交動作

下列提交動作受到在Universal Editor[中編寫的](/help/edge/docs/forms/universal-editor/create-forms.md)最適化Forms支援：

* [寄送電子郵件](/help/forms/configure-submit-action-send-email.md)
* [叫用Power Automate流程](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [叫用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [使用表單資料模型 (FDM) 提交](/help/forms/using-form-data-model.md)
* [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交至REST端點](/help/forms/configure-submit-action-restpoint.md)
* [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [叫用 AEM 工作流程](/help/forms/configure-submit-action-workflow.md)
* [提交至 Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [提交至Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [提交至試算表](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

您可以使用&#x200B;**編輯表單屬性**&#x200B;擴充功能的&#x200B;**提交**&#x200B;索引標籤，為在Universal Editor中建立的表單設定提交動作。

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
> * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

## 提交檔案型Forms的動作

檔案型Forms僅支援提交至試算表。 若要瞭解如何設定試算表以接收提交的資料，請參閱[設定Google工作表或Microsoft Excel檔案以開始接受資料](/help/edge/docs/forms/submit-forms.md)文章中的指示。

## 另請參閱 {#see-also}

{{af-submit-action}}

