---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: AEM工作流程，整合最適化表單與AEM工作流程，叫用AEM工作流程提交動作
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 56%

---


# 整合AEM最適化表單與AEM Workflow：簡化業務流程

此 **[!UICONTROL 叫用AEM工作流程]** 提交動作會將最適化表單與AEM工作流程建立關聯。 提交表單後，相關聯的工作流程就會在作者執行個體上自動開始。您可以將資料檔案、附件和記錄檔案儲存至工作流程的裝載位置或變數。 如果工作流程標記為外部資料儲存空間，且設定為外部資料儲存空間，則只有變數選項可使用。您可以從可用於工作流程模型的變數清單中選取。如果工作流程是在後續階段標記為外部資料儲存空間，而不是在建立工作流程時標記，則請確保已經具備所需的變數設定。

>[!NOTE]
>
>  瞭解如何 [建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem) 定義使用者啟動工作流程時所執行的一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。

AEMas a Cloud Service提供多種現成的提交動作，用於處理表單提交。 如需這些選項的詳細資訊，請參閱 [最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)  文章。

## 優點

整合AEM工作流程與最適化Forms的一些優點包括：

* AEM Workflow整合可讓您自動化涉及表單提交的複雜業務流程。
* AEM Workflow支援條件式邏輯，因此可依據表單資料或外部因素進行動態決策。
* AEM Workflow會根據預先定義的規則和條件來路由任務，確保將任務指派給適當的個人或群組。

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## 將AEM工作流程與最適化Forms整合 {#steps-to-integrate-workflow-with-af}

若要設定自動化程式，請使用 [AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem) 針對最適化表單，執行以下步驟：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從 **[!UICONTROL 提交動作]** 下拉式清單，選取 **[!UICONTROL 叫用AEM工作流程]** .
   ![傳送電子郵件的動作設定](/help/forms/assets/configure-invoke-aem-workflow.png)

1. 從中選擇工作流程模型 **[!UICONTROL 工作流程模型]** 下拉式清單。
1. 從中選擇選項 **[!UICONTROL 使用以下專案儲存資料檔案：]** 下拉式清單。

   **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項並從工作流程模型可用的變數清單中選取變數。

1. 從中選擇選項 **[!UICONTROL 使用以下專案儲存附件：]** 下拉式清單。

   **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

1. 從中選擇選項 **[!UICONTROL 記錄檔案，使用]** 下拉式清單。

   **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!NOTE]
>
> 進一步瞭解 [以Forms為中心的AEM工作流程 — 自動化業務流程的步驟參考](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## 相關文章

{{af-submit-action}}