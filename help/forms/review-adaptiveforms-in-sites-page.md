---
title: 如何傳送最適化表單以供檢閱？ 如何管理aem最適化表單的稽核？
description: 稽核是一種機制，可讓稽核者使用「指派工作」步驟為最適化表單執行不同工作。
feature: Adaptive Forms
hide: true
hidefromtoc: true
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# 建立和管理最適化表單的稽核 {#review-step-forms-aem-sites-page}

稽核者使用AEM工作流程的[指派步驟](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step)，稽核提交的表單並對其執行動作。 若要使用「指派工作」步驟來複查已提交的表單，請遵循下列步驟：

1. [建立AEM工作流程](#create-an-aem-workflow)
1. [設定最適化表單容器的提交動作](#configure-submit-action)
1. [檢閱後提交最適化表單](#submit-af-after-review)

## 建立AEM工作流程 {#create-an-aem-workflow}

1. 在編輯模式下開啟您的作者執行個體。
1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**
1. 指定工作流程的標題並新增&#x200B;**[指派任務]**&#x200B;步驟
1. 在動作列上選取![settings_icon](assets/settings_icon.png)。 **[!UICONTROL 指派任務]**&#x200B;對話方塊開啟。
1. 開啟[!UICONTROL 表單和檔案]標籤，然後開啟[!UICONTROL 預先填入]下拉式清單，並指定：

   * 選擇輸入資料檔案，使用
   * 選擇輸入附件，使用

   ![檢閱步驟](/help/forms/assets/assigntask-review1.gif)

1. 開啟&#x200B;**[!UICONTROL 受指派人]**&#x200B;索引標籤並開啟[!UICONTROL 預先填入]下拉式清單並指定&#x200B;**[!UICONTROL 指派選項]**：

   ![檢閱步驟](/help/forms/assets/review-assignstep.png)

1. 按一下「**[!UICONTROL 完成]**」以儲存變更。

## 設定提交動作 {#configure-submit-action}

現在，請在網站的頁面上設定最適化表單容器元件的提交動作：

1. 移至網站的頁面。
1. 選取最適化表單容器的![settings_icon](assets/settings_icon.png)。 **[!UICONTROL 最適化表單容器]**&#x200B;對話方塊開啟。
1. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;索引標籤並指定&#x200B;**[!UICONTROL 提交動作]**&#x200B;至[叫用AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 按一下[完成]以儲存設定。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## 稽核後提交最適化表單 {#submit-af-after-review}

若要檢閱並確認已提交的最適化表單：

1. 移至[!UICONTROL 工具] > [!UICONTROL 工作流程] > [!UICONTROL 執行個體]
1. 在收件匣中，您可以看到正在建立執行個體。
1. 選取執行個體並按一下[!UICONTROL 開啟]。
1. 現在，您可以檢視提交的表單。

稽核者會執行不同的動作，如：

* **提交**：稽核者完成表單並提交以進行進一步處理。
* **儲存**：檢閱者將表單儲存為目前狀態而不提交。
* **重設**：檢閱者會清除對表單所做的任何變更，並將其還原為原始狀態。
* **委派**：檢閱者將表單的所有權轉移給其他人員，以進一步動作或檢閱。
