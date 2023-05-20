---
title: 建立和管理嵌入或在「站點」頁中建立的AdaptiveForms的審閱
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: 審閱是一種機制，允許審閱者使用「分配任務」步驟為自適應表單執行不同任務
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# 在網站頁面中查看Forms的步驟 {#review-step-forms-aem-sites-page}

使用 [分配步驟](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) 審閱AEM者審閱已提交的表單並對其執行操作。 要使用「分配」任務步驟複查已提交的表單，請執行以下步驟：

1. [建立工AEM作流](#create-an-aem-workflow)
1. [配置Adaptive Form容器的提交操作](#configure-submit-action)
1. [在審核後提交自適應表單](#submit-af-after-review)

## 建立工AEM作流 {#create-an-aem-workflow}

1. 在編輯模式下開啟作者實例。
1. 轉到 **[!UICONTROL 工具]** >  **[!UICONTROL 工作流]** >  **[!UICONTROL 模型]** > **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**
1. 指定工作流的標題並添加 **[分配任務]** 步
1. 點擊 ![設定表徵圖](assets/settings_icon.png) 按鈕。 的 **[!UICONTROL 分配任務]** 對話框。
1. 開啟 [!UICONTROL 窗體和文檔] 頁籤 [!UICONTROL 預填充] 下拉並指定：

   * 選擇輸入資料檔案，使用
   * 選擇輸入附件，使用

   ![審閱步驟](/help/forms/assets/assigntask-review1.gif)

1. 開啟 **[!UICONTROL 受分配人]** 頁籤 [!UICONTROL 預填充] 下拉並指定 **[!UICONTROL 分配選項]**:

   ![審閱步驟](/help/forms/assets/review-assignstep.png)

1. 按一下「**[!UICONTROL 完成]**」以儲存變更。

## 配置提交操作 {#configure-submit-action}

現在，在站點的頁面上配置Adaptive Form Container元件的「提交」操作：

1. 轉到網站頁。
1. 點擊 ![設定表徵圖](assets/settings_icon.png) 的子菜單。 的 **[!UICONTROL 自適應窗體容器]** 對話框。
1. 開啟 **[!UICONTROL 提交]** 頁籤 **[!UICONTROL 提交操作]** 至 [調用工AEM作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. 按一下 [完成] 按鈕。

![子任務頁籤查看步驟](/help/forms/assets/submissiontab-reviewstep.gif)

## 在審核後提交自適應表單 {#submit-af-after-review}

要查看和確認已提交的自適應表單，請執行以下操作：

1. 轉到 [!UICONTROL 工具] >  [!UICONTROL 工作流] >  [!UICONTROL 實例]
1. 在「收件箱」中，您可以看到正在建立實例。
1. 選擇實例並按一下 [!UICONTROL 開啟]。
1. 現在，您可以看到已提交的表單。

審閱者執行的操作不同：

* **提交**:審核者完成表單並提交它以供進一步處理。
* **保存**:審閱者將表單保存為其當前狀態，而不提交它。
* **重置**:審閱者將清除對表單所做的任何更改，並將其恢復到原始狀態。
* **委託**:審查員將表格的所有權轉給其他人，以便採取進一步行動或審查。
