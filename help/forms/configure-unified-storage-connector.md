---
title: 如何配置AEM Forms的Unified Storage Connector?
description: 了解如何管理AEM Forms的Unified Storage Connector。 使用Unified Storage Connector將AEM Forms連接到外部資料儲存。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# 管理AEM Forms的Unified Storage Connector {#manage-unified-storage-connector}

您可以使用Unified Storage Connector將AEM Forms連接到外部資料儲存。

例如，您可以填寫最適化表單中欄位的值，並提交至AEM工作流程。 您可以進一步設定AEM工作流程，將資料儲存在外部儲存中，例如Microsoft Azure儲存伺服器。 使用「統一儲存連接器」在AEM工作流程和外部儲存之間建立連線。

## 使用Microsoft Azure儲存伺服器連線AEM工作流程 {#connect-workflows-with-azure}

建立Azure儲存配置，並使用Unified Storage Connector引用該配置。 然後，您可以配置AEM工作流模型以將資料儲存外部化，以將其連接到Azure儲存伺服器。

### 建立 [!DNL Azure] 儲存配置 {#create-azure-storage-configuration}

執行這些步驟之前，請確定您有 [!DNL Azure] 儲存帳戶和存取金鑰，以授權存取 [!DNL Azure] 儲存帳戶。

執行下列步驟以建立 [!DNL Azure] 儲存配置：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存]**.
1. 選取要建立設定的資料夾，然後點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 儲存帳戶 **[!UICONTROL Azure儲存帳戶]** 欄位。
1. 指定要在 **[!UICONTROL Azure訪問密鑰]** 欄位和點選 **[!UICONTROL 儲存]**.

### 為AEM工作流程配置Unified Storage Connector {#configure-unified-storage-connector-workflows}

執行下列步驟為AEM工作流程配置Unified Storage Connector:

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一儲存連接器]**.

1. 在 **[!UICONTROL 工作流程]** 部分，選擇 **[!UICONTROL Azure]** 從「儲存」下拉式清單中。
1. 指定 [Azure儲存配置的配置路徑](#create-azure-storage-configuration) 在 **[!UICONTROL 儲存配置路徑]** 欄位。
1. 點選 **[!UICONTROL 發佈]** 然後點選 **[!UICONTROL 儲存]** 以儲存設定。

### 為外部資料儲存設定AEM工作流程模型 {#configure-workflow-external-data-storage}

執行下列步驟來設定外部資料儲存的AEM工作流程模型：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 選取模型名稱並點選 **[!UICONTROL 編輯]**.
1. 點選「頁面資訊」圖示，然後點選 **[!UICONTROL 開啟屬性]**.
1. 選擇 **[!UICONTROL 將工作流程資料儲存外部化]**.
1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存屬性。

>[!NOTE]
>
>為外部資料儲存配置AEM工作流模型時，將分配任務步驟另存為草稿和檢索分配任務步驟歷史記錄的選項不可用。

### 外部資料儲存的AEM工作流程手冊 {#guidelines-workflows-external-data-storage}

以下是使用AEM工作流程並將資料儲存至外部資料儲存時的准則，例如Microsoft Azure儲存伺服器：

* 在工作流模型步驟中定義輸入和輸出資料檔案和附件時，使用變數來儲存資料。 不選擇 **[!UICONTROL 相對於裝載]** 和 **[!UICONTROL 在絕對路徑中可用]** 選項。 此 **[!UICONTROL 相對於裝載]** 和 **在絕對路徑中可用** 選項一旦您 [為外部資料儲存設定AEM工作流程模型](#configure-workflow-external-data-storage).

* 將最適化表單提交至AEM工作流程時，使用變數來儲存資料檔案和附件。 不選擇 **[!UICONTROL 相對於裝載]** 選項。 此 **[!UICONTROL 相對於裝載]** 選項後不會自動顯示 [為外部資料儲存設定AEM工作流程模型](#configure-workflow-external-data-storage).

* 請勿在工作流程模型中使用自訂AEM工作流程步驟，將資料儲存在CRX DE存放庫中。

* 當您 [為外部資料儲存設定AEM工作流程模型](#configure-workflow-external-data-storage)，請勿根據工作流程的資料建立AEM收件匣的自訂欄。
