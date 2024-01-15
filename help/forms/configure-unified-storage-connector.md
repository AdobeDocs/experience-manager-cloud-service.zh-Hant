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

### 建立 [!DNL Azure] 儲存設定 {#create-azure-storage-configuration}

在執行這些步驟之前，請確定您已 [!DNL Azure] 儲存帳戶與存取金鑰，用於授權存取 [!DNL Azure] 儲存體帳戶。

執行以下步驟來建立 [!DNL Azure] 儲存設定：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure儲存體]**.
1. 選取資料夾以建立設定，然後選取 **[!UICONTROL 建立]**.
1. 在中指定設定的標題 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 中的儲存體帳戶 **[!UICONTROL Azure儲存體帳戶]** 欄位。
1. 指定金鑰以存取 **[!UICONTROL Azure存取金鑰]** 欄位並選取 **[!UICONTROL 儲存]**.

### 設定AEM Workflow的統一儲存聯結器(USC) {#configure-unified-storage-connector-workflows}

執行以下步驟，為AEM Workflow設定統一儲存聯結器(USC)：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一的儲存聯結器]**.

1. 在 **[!UICONTROL 工作流程]** 區段，選取 **[!UICONTROL Azure]** 從「儲存」下拉式清單。
1. 指定 [Azure儲存體設定的設定路徑](#create-azure-storage-configuration) 在 **[!UICONTROL 儲存設定路徑]** 欄位。
1. 選取 **[!UICONTROL 發佈]** 然後選取 **[!UICONTROL 儲存]** 以儲存組態。

### 設定外部資料儲存的AEM Workflow模型 {#configure-workflow-external-data-storage}

執行以下步驟，為外部資料儲存設定AEM Workflow模型：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 選取模型名稱並選取 **[!UICONTROL 編輯]**.
1. 選取「頁面資訊」圖示，然後選取 **[!UICONTROL 開啟屬性]**.
1. 選取 **[!UICONTROL 將工作流程資料儲存區外部化]**.
1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存屬性。

>[!NOTE]
>
>當您為外部資料儲存設定AEM工作流程模型時，會停用將「指派任務」步驟儲存為草稿以及擷取「指派任務」步驟記錄的選項。

### 外部資料儲存的AEM工作流程准則 {#guidelines-workflows-external-data-storage}

以下是使用AEM Workflow並將資料儲存至外部資料儲存區(例如Microsoft Azure儲存伺服器)時的准則：

* 在工作流程模型步驟中定義輸入和輸出資料檔案及附件時，使用變數來儲存資料。 不要選取 **[!UICONTROL 相對於承載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項。 此 **[!UICONTROL 相對於承載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項不會在您之後自動顯示 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage).

* 將最適化表單提交至AEM Workflow時，請使用變數來儲存資料檔案和附件。 不要選取 **[!UICONTROL 相對於承載]** 選項時，將最適化表單提交至AEM Workflow。 此 **[!UICONTROL 相對於承載]** 選項不會在您之後自動顯示 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage).

* 請勿在工作流程模型中使用自訂AEM工作流程步驟來將資料儲存在CRX DE存放庫中。

* 當您 [設定外部資料儲存的AEM Workflow模型](#configure-workflow-external-data-storage)，請勿為AEM收件匣建立自訂欄，因為如果AEM收件匣中的工作專案屬於標籤為外部儲存的工作流程，則不會擷取自訂欄的值。

>[!MORELIKETHIS]
>
>* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
>* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
>* [將Microsoft Dynamics 365和Salesforce與最適化Forms整合](/help/forms/configure-msdynamics-salesforce.md)
>  [將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
