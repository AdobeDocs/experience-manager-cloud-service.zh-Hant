---
title: 建立及管理內嵌或在Sites中建立的適用性Forms審核
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: 審核是一種機制，可讓審核者使用「指派任務」步驟，針對最適化表單執行不同工作
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# 檢閱網站頁面中Forms的步驟 {#review-step-forms-aem-sites-page}

使用 [指派步驟](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) 審核者在AEM工作流程中審核提交的表單，並對其執行操作。 要使用「分配任務」步驟來複查已提交的表單，請執行以下步驟：

1. [建立AEM工作流程](#create-an-aem-workflow)
1. [設定適用性表單容器的提交動作](#configure-submit-action)
1. [審核後提交最適化表單](#submit-af-after-review)

## 建立AEM工作流程 {#create-an-aem-workflow}

1. 在編輯模式中開啟您的製作執行個體。
1. 前往 **[!UICONTROL 工具]** >  **[!UICONTROL 工作流程]** >  **[!UICONTROL 模型]** > **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**
1. 指定工作流程的標題並新增 **[分配任務]** 步驟
1. 點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **[!UICONTROL 分配任務]** 對話框開啟。
1. 開啟 [!UICONTROL 表單與檔案] 標籤和開啟 [!UICONTROL 預先填入] 下拉式清單並指定：

* 選擇輸入資料檔案，使用
* 選擇輸入附件，使用

   ![審核步驟](/help/forms/assets/assigntask-review1.gif)

1. 開啟 **[!UICONTROL 受託人]** 標籤和開啟 [!UICONTROL 預先填入] 下拉式清單並指定 **[!UICONTROL 指派選項]**:

   ![審核步驟](/help/forms/assets/review-assignstep.png)

1. 按一下「**[!UICONTROL 完成]**」以儲存變更。

## 配置提交操作 {#configure-submit-action}

現在，在網站的頁面上設定適用性表單容器元件的「提交」動作：

1. 前往網站的頁面。
1. 點選 ![settings_icon](assets/settings_icon.png) 最適化表單容器。 此 **[!UICONTROL 適用性表單容器]** 對話框開啟。
1. 開啟 **[!UICONTROL 提交]** 索引標籤 **[!UICONTROL 提交動作]** to [叫用AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 按一下 [完成] 以儲存設定。

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## 審核後提交最適化表單 {#submit-af-after-review}

若要檢閱並確認已提交的最適化表單：

1. 前往 [!UICONTROL 工具] >  [!UICONTROL 工作流程] >  [!UICONTROL 例項]
1. 在「收件匣」中，您會看到已建立例項。
1. 選取例項，然後按一下 [!UICONTROL 開啟].
1. 現在，您可以看到已提交的表單。

審核者執行以下不同操作：

* **提交**:審核者填寫表格並提交以供進一步處理。
* **儲存**:審核者將表單保存為當前狀態，而不提交。
* **重設**:審核者會清除對表單所做的任何變更，並將其還原為原始狀態。
* **委派**:審核者將表單的所有權轉移給他人，以便採取進一步行動或進行審核。
