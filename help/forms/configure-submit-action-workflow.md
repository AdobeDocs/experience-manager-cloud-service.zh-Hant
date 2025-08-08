---
title: 如何將AEM工作流程與最適化表單整合？
description: 探索使用AEM Forms提交動作自動化工作流程初始化的程式。
keywords: AEM工作流程，整合最適化表單與AEM工作流程，叫用AEM工作流程提交動作
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 60%

---

# 整合AEM最適化表單與AEM工作流程：簡化業務流程

**[!UICONTROL 叫用AEM工作流程]**&#x200B;提交動作會將最適化表單與AEM工作流程建立關聯。 提交表單後，相關聯的工作流程就會在作者執行個體上自動開始。您可以將資料檔案、附件和記錄檔案儲存至工作流程的裝載位置或變數。 如果工作流程標記為外部資料儲存空間，且設定為外部資料儲存空間，則只有變數選項可使用。您可以從可用於工作流程模型的變數清單中選取。如果工作流程是在後續階段標記為外部資料儲存空間，而不是在建立工作流程時標記，則請確保已經具備所需的變數設定。

>[!NOTE]
>
>  瞭解如何[建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)，以定義使用者啟動工作流程時所執行的一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

## 優點

整合AEM工作流程與最適化Forms的一些優點包括：

* AEM工作流程整合可讓您自動化涉及表單提交的複雜業務流程。
* AEM工作流程支援條件式邏輯，因此可依據表單資料或外部因素進行動態決策。
* AEM工作流程會根據預先定義的規則和條件路由任務，確保任務指派給適當的個人或群組。

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## 將AEM工作流程與最適化Forms整合 {#steps-to-integrate-workflow-with-af}

>[!BEGINTABS]

>[!TAB 基礎元件]

若要針對以Foundation元件為基礎的最適化表單設定使用[AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)的自動化程式，請執行下列步驟：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**提交動作**&#x200B;作為&#x200B;**[!UICONTROL 叫用AEM工作流程]**。
1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;下拉式清單中選取工作流程模型。
1. 使用&#x200B;**[!UICONTROL 下拉式清單，從]**&#x200B;儲存資料檔中選取選項。

   **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項並從工作流程模型可用的變數清單中選取變數。

   ![invoke-workflow-fc](/help/forms/assets/invoke-workflow-fc.png)

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;儲存附件下拉式清單中選取選項。

   **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;的記錄檔案下拉式清單中選取選項。

   **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

   >[!NOTE]
   >
   > 深入瞭解[以Forms為中心的AEM工作流程 — 自動化業務流程的步驟參考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!TAB 核心元件]

若要針對以核心元件為基礎的最適化表單設定具有[AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)的自動化程式，請執行下列步驟：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 叫用AEM工作流程]** 。

   傳送電子郵件的![動作設定](/help/forms/assets/configure-invoke-aem-workflow.png)

1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;下拉式清單中選取工作流程模型。
1. 使用&#x200B;**[!UICONTROL 下拉式清單，從]**&#x200B;儲存資料檔中選取選項。

   **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項並從工作流程模型可用的變數清單中選取變數。

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;儲存附件下拉式清單中選取選項。

   **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;的記錄檔案下拉式清單中選取選項。

   **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

   >[!NOTE]
   >
   > 深入瞭解[以Forms為中心的AEM工作流程 — 自動化業務流程的步驟參考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!TAB 通用編輯器]

若要針對在Universal Editor中編寫的最適化表單設定具有[AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)的自動化程式，請執行下列步驟：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**&#x200B;擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

1. 按一下「**提交**」標籤，然後選取「**[!UICONTROL 叫用AEM工作流程]**」提交動作。


   傳送電子郵件的![動作設定](/help/forms/assets/invoke-service-ue.png)

1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;下拉式清單中選取工作流程模型。
1. 使用&#x200B;**[!UICONTROL 下拉式清單，從]**&#x200B;儲存資料檔中選取選項。

   **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項並從工作流程模型可用的變數清單中選取變數。

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;儲存附件下拉式清單中選取選項。

   **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

1. 從&#x200B;**[!UICONTROL 使用]**&#x200B;的記錄檔案下拉式清單中選取選項。

   **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

   >[!NOTE]
   >
   > 深入瞭解[以Forms為中心的AEM工作流程 — 自動化業務流程的步驟參考](/help/forms/aem-forms-workflow-step-reference.md)。

>[!ENDTABS]

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## 相關文章

{{af-submit-action}}
