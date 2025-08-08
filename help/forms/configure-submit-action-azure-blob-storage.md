---
description: 瞭解如何在AEM Forms中建立Azure Blob儲存設定，並在最適化Forms中使用它來有效率地儲存資料。
keywords: Azure Blob儲存與AEM Forms整合、提交資料至Azure儲存體、在AEM Forms中建立Azure儲存體設定、在調適性Forms提交動作中使用Azure Blob儲存體
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: 如何設定最適化表單的提交動作？
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 43%

---

# 將自適應表單提交至 Azure Blob Storage

「**[!UICONTROL 提交到 Azure Blob 儲存體]**」提交動作會將最適化表單連結到 Microsoft® Azure 入口網站。您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Azure儲存體容器。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/aem-forms-submit-action.md)文章中進一步瞭解這些選項。

## 優點

Azure Blob儲存與AEM Forms整合的部分優點包括：

* 它有助於簡化將最適化表單資料、檔案、附件和記錄檔案提交至Azure儲存體容器的程式。
* 它使用Azure Blob儲存體來集中且有條理地儲存最適化表單提交內容。

## 將AEM Forms與Microsoft® Azure Blob儲存體連線

若要在最適化Forms提交動作中使用Azure Blob儲存體：

1. [建立 Azure Blob 儲存體容器](#create-a-azure-blob-storage-container-create-azure-configuration)：將 AEM Forms 連結到 Azure 儲存體容器。
2. [在最適化表單中使用 Azure 儲存體設定](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：將您的最適化表單連結到已設定的 Azure 儲存體容器。

### 建立 Azure Blob 儲存體容器 {#create-azure-configuration}

若要將 AEM Forms 連結到 Azure 儲存體容器：

1. 前往 **AEM Forms 作者**&#x200B;執行個體 >「**[!UICONTROL 工具]**」>「**[!UICONTROL 雲端服務]**」>「**[!UICONTROL Azure 儲存體]**」。
1. 一旦選取了「**[!UICONTROL Azure 儲存體]**」，系統就會將您重新導向至「**[!UICONTROL Azure 儲存體瀏覽器]**」。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下「**[!UICONTROL 建立]**」。此時會顯示「建立 Azure 儲存體設定」精靈。

   ![Azure 儲存體設定](/help/forms/assets/azure-storage-configuration.png)

1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL Azure 儲存體帳戶]**」和「**[!UICONTROL Azure 存取金鑰]**」。

   * 您可以從 Microsoft® Azure 入口網站的儲存體帳戶擷取 `Azure Storage Account` 名稱和 `Azure Access key`。
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=zh-Hant)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=zh-Hant)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. 按一下「**[!UICONTROL 儲存]**」。

現在，您可以使用此 Azure 儲存體容器設定，在最適化表單中使用該提交動作。

### 在最適化表單中使用 Azure 儲存體設定 {#use-azure-storage-configuartion-in-af}

您可以在調適型表單中使用已建立的Azure儲存體容器設定，以在Azure儲存體容器中儲存資料或產生的記錄檔案。

>[!NOTE]
>
> * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
> * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

>[!BEGINTABS]

>[!TAB 基礎元件]

執行以下步驟，根據基礎元件在最適化表單中使用Azure儲存體容器設定，如下所示：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至Azure Blob儲存體]**。

   ![Azure Blob儲存體GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%，height=50%}

   您也可以將記錄檔案(DoR)儲存在Azure Blob儲存體中。

1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

提交表單時，資料會儲存在指定的 Azure 儲存體容器設定中。
儲存資料的資料夾結構是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!TAB 核心元件]

執行以下步驟，根據核心元件在最適化表單中使用Azure儲存體容器設定，如下所示：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 提交至Azure Blob儲存體]**。

   ![Azure Blob 儲存體 GIF](/help/forms/assets/azure-submit-video.gif)

   您也可以將記錄檔案(DoR)儲存在Azure Blob儲存體中。

1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

提交表單時，資料會儲存在指定的 Azure 儲存體容器設定中。
儲存資料的資料夾結構是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!TAB 通用編輯器]

執行以下步驟，以在通用編輯器中編寫的最適化表單中使用Azure儲存體容器設定：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**&#x200B;擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 提交至Azure Blob儲存體]**&#x200B;提交動作。
   ![Azure Blob儲存體](/help/forms/assets/azure-blob-storage-ue.png)

   如果您選取&#x200B;**以原始名稱儲存附件**，則附件會使用其原始檔案名稱儲存在資料夾中。 您也可以將記錄檔案(DoR)儲存在Azure Blob儲存體中。

1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存送出設定。

提交表單時，資料會儲存在指定的 Azure 儲存體容器設定中。
儲存資料的資料夾結構是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!ENDTABS]

## 相關文章

{{af-submit-action}}
