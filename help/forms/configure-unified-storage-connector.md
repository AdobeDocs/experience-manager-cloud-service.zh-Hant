---
title: 如何設定AEM Forms的統一儲存聯結器(USC)？
description: 瞭解如何管理AEM Forms的統一儲存聯結器(USC)。 使用統一儲存聯結器(USC)將AEM Forms連線至外部資料儲存。
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# 管理AEM Forms的統一儲存聯結器(USC) {#manage-unified-storage-connector}

您可以使用統一儲存聯結器(USC)將AEM Forms連線至外部資料儲存。

例如，您可以在最適化表單中填寫欄位值，並將其提交至AEM Workflow。 您可以進一步設定AEM Workflow將資料儲存在外部儲存空間，例如Microsoft Azure儲存伺服器。 使用統一儲存聯結器(USC)在AEM Workflow和外部儲存裝置之間建立連線。

## 將AEM工作流程與Microsoft Azure儲存伺服器連線 {#connect-workflows-with-azure}

建立Azure儲存體設定，並使用統一儲存聯結器(USC)參照該設定。 然後，您可以設定AEM工作流程模型以將資料儲存區外部化，以將其連線至Azure儲存體伺服器。

### 建立[!DNL Azure]儲存設定 {#create-azure-storage-configuration}

在執行這些步驟之前，請確定您有[!DNL Azure]儲存體帳戶和存取金鑰，以授權存取[!DNL Azure]儲存體帳戶。

執行以下步驟來建立[!DNL Azure]儲存設定：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure儲存體]**。
1. 選取資料夾以建立組態，並選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定組態的標題。
1. 在&#x200B;**[!UICONTROL Azure儲存體帳戶]**&#x200B;欄位中指定[!DNL Azure]儲存體帳戶的名稱。
1. 在&#x200B;**[!UICONTROL Azure存取金鑰]**&#x200B;欄位中指定存取Azure儲存體帳戶的金鑰，並選取&#x200B;**[!UICONTROL 儲存]**。

### 設定AEM Workflow的統一儲存聯結器(USC) {#configure-unified-storage-connector-workflows}

執行以下步驟，為AEM Workflow設定統一儲存聯結器(USC)：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 整合式儲存聯結器]**。

1. 在&#x200B;**[!UICONTROL 工作流程]**&#x200B;區段中，從「儲存」下拉式清單中選取&#x200B;**[!UICONTROL Azure]**。
1. 在&#x200B;**[!UICONTROL 儲存設定路徑]**&#x200B;欄位中指定Azure儲存體設定](#create-azure-storage-configuration)的[設定路徑。
1. 選取「**[!UICONTROL Publish]**」，然後選取「**[!UICONTROL 儲存]**」以儲存設定。

### 設定外部資料儲存的AEM Workflow模型 {#configure-workflow-external-data-storage}

執行以下步驟，為外部資料儲存設定AEM Workflow模型：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 選取模型名稱並選取&#x200B;**[!UICONTROL 編輯]**。
1. 選取[頁面資訊]圖示，然後選取&#x200B;**[!UICONTROL 開啟屬性]**。
1. 選取&#x200B;**[!UICONTROL 將工作流程資料儲存區外部化]**。
1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存屬性。

>[!NOTE]
>
>當您為外部資料儲存設定AEM工作流程模型時，會停用將「指派任務」步驟儲存為草稿以及擷取「指派任務」步驟記錄的選項。

### 外部資料儲存的AEM工作流程准則 {#guidelines-workflows-external-data-storage}

以下是使用AEM Workflow並將資料儲存至外部資料儲存區(例如Microsoft Azure儲存伺服器)時的准則：

* 在工作流程模型步驟中定義輸入和輸出資料檔案及附件時，使用變數來儲存資料。 請勿選取&#x200B;**[!UICONTROL 相對於承載]**&#x200B;以及&#x200B;**[!UICONTROL 絕對路徑可用的]**&#x200B;選項。 當您[設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage)後，**[!UICONTROL 相對於承載]**&#x200B;和&#x200B;**[!UICONTROL 在絕對路徑上可用的]**&#x200B;選項就不會自動顯示。

* 將最適化表單提交至AEM Workflow時，請使用變數來儲存資料檔案和附件。 將最適化表單提交至AEM工作流程時，請勿選取&#x200B;**[!UICONTROL 相對於承載]**&#x200B;選項。 當您[設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage)後，**[!UICONTROL 相對於承載]**&#x200B;選項就不會自動顯示。

* 請勿在工作流程模型中使用自訂AEM工作流程步驟，將資料儲存在CRX DE存放庫中。

* 當您[為外部資料儲存設定AEM Workflow模型](#configure-workflow-external-data-storage)時，請勿為AEM收件匣建立自訂欄，因為如果AEM收件匣中的工作專案屬於標籤為外部儲存的工作流程，則不會擷取自訂欄的值。

>[!MORELIKETHIS]
>
>* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
>* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
>* [整合Microsoft Dynamics 365和Salesforce與最適化Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
