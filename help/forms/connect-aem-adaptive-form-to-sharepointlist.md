---
title: 如何將AEM最適化表單連結至Microsoft&reg； SharePoint清單？
description: 將最適化表單連線至Microsoft&reg； SharePoint清單。 瞭解如何設定Microsoft&reg； SharePoint清單，並使用設定建立表單資料模型。 此外，您也會瞭解如何將FDM與最適化表單整合。
role: User, Developer
keywords: 將AEM最適化表單連線至Microsoft SharePoint清單、將最適化表單連線至Microsoft SharePoint清單、將AEM最適化表單整合至Microsoft SharePoint清單、將最適化表單整合至Microsoft SharePoint清單、將最適化表單的資料提交至SharePoint清單、將AEM工作流程提交至SharePoint清單。
hide: true
hidefromToC: true
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 5%

---


# 將最適化表單連線至Microsoft® SharePoint清單

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)存取。</span>

**Microsoft® SharePoint**：Microsoft® SharePoint提供動態且有效的團隊網站給所有團隊、部門及部門，藉此促進共同作業。 它可用來儲存、組織、共用及存取使用任何網頁瀏覽器(例如Microsoft、Edge®Internet Explorer、Chrome或Firefox)之任何裝置的資訊。 的兩個主要元件 **Microsoft® SharePoint** 為：

* **Microsoft® SharePoint檔案庫**： Microsoft® SharePoint檔案庫會顯示檔案和資料夾清單及其關鍵資訊，例如上次修改日期和檔案所有者。 此功能可讓您輕鬆組織和導覽檔案。
如需如何整合的指示 **Microsoft® SharePoint檔案庫** 若使用最適化表單，請參閱 [最適化表單提交動作](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) 文章。

* **Microsoft® SharePoint清單**： Microsoft® SharePoint清單是資料集合。 您可以為不同型別的資料新增欄，並建立檢視以有效地顯示資料。 您可以輕鬆對清單進行分組、篩選、排序和格式化。

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## 將最適化表單連線至Microsoft® SharePoint清單的先決條件 {#prerequisites}

將最適化表單連線至Microsoft® SharePoint清單之前，請執行以下步驟：

1. [設定Microsoft](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [使用Microsoft建立表單資料模型](/help/forms/create-form-data-models.md)
1. [設定表單資料模型以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)

現在，您可以：

* [連線Microsoft](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [連線Microsoft](#connect-sharepoint-list-workflow)

## 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

若要將Microsoft® SharePoint清單整合至最適化表單 [設定最適化表單以使用表單資料模型](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

設定最適化表單以使用表單資料模型後，您可以：

* [使用表單資料模型設定提交動作](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [設定規則編輯器以叫用表單資料模型](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## 將Microsoft® SharePoint清單連線至AEM工作流程 {#connect-sharepoint-list-workflow}

若要將Microsoft® SharePoint清單整合至AEM工作流程：

1. [建立工作流程以叫用表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)

   <!--
    To create a new workflow with the editor, perform the following steps:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [設定提交動作以叫用AEM工作流程](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


瞭解如何 [使用AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) 在最適化表單中進行共同作業、管理和處理內容。

## 最佳做法 {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft&reg; SharePoint List rather than Microsoft&reg; SharePoint Document Library. -->
* Microsoft® SharePoint清單不支援下列欄型別：
   * 影像欄
   * 中繼資料欄
   * 人員欄
   * 外部資料欄

## 另請參閱 {#see-also}

* [建立以核心元件為基礎的最適化表單](/help/forms/creating-adaptive-form-core-components.md)
* [設定資料來源](/help/forms/configuring-submit-actions.md)
* [建立表單資料模型](/help/forms/create-form-data-models.md)
* [使用以Forms為中心的AEM Workflows — 步驟參考來自動化業務流程](/help/forms/aem-forms-workflow-step-reference.md)
* [建立最適化Forms的自訂提交動作](/help/forms/custom-submit-action-form.md)
* [建立最適化表單或新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [將最適化表單內嵌至AEM Sites頁面](/help/forms/embed-adaptive-form-aem-sites.md)
* [在最適化表單中建立、使用及自訂主題](/help/forms/using-themes-in-core-components.md)







