---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Azure Blob儲存與AEM Forms整合、提交資料至Azure儲存體、在AEM Forms中建立Azure儲存體設定、在調適性Forms提交動作中使用Azure Blob儲存體
feature: Adaptive Forms, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: 「如何設定最適化表單的提交動作？」
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 66%

---

# 將最適化表單提交至 Azure Blob 儲存體

「**[!UICONTROL 提交到 Azure Blob 儲存體]**」提交動作會將最適化表單連結到 Microsoft® Azure 入口網站。您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Azure儲存體容器。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

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

您可以在最適化表單中使用建立的 Azure 儲存體器設定，將資料或產生的記錄文件儲存在 Azure 儲存體容器中。執行以下步驟，即可在最適化表單中使用 Azure 儲存體容器設定：
1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 將「**提交動作**」選取作為「**[!UICONTROL 提交到 Azure Blob 儲存體]**」。
   ![Azure Blob 儲存體 GIF](/help/forms/assets/azure-submit-video.gif)

1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

提交表單時，資料會儲存在指定的 Azure 儲存體容器設定中。
儲存資料的資料夾結構是 `/configuration_container/form_name/year/month/date/submission_id/data`。

## 相關文章

{{af-submit-action}}
