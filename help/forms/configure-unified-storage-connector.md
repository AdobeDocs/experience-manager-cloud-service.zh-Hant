---
title: 如何為AEM Forms配置統一儲存連接器？
description: 瞭解如何管理用於AEM Forms的統一儲存連接器。 使用統一儲存連接器將AEM Forms連接到外部資料儲存。
source-git-commit: da3cef0a0a28dd16e627a157f02bbe6a84f59da5
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---


# 管理用於AEM Forms的統一儲存連接器 {#manage-unified-storage-connector}

您可以使用統一儲存連接器將AEM Forms連接到外部資料儲存。

例如，您可以填充自適應表單中欄位的值，並將其提交到工AEM作流。 您可以進一步AEM配置工作流以將資料儲存在外部儲存中，如MicrosoftAzure儲存伺服器。 使用統一儲存連接器在工作流和外AEM部儲存之間建立連接。

## 將工AEM作流與MicrosoftAzure儲存伺服器連接 {#connect-workflows-with-azure}

使用統一儲存連接器建立Azure儲存配置並參考該配置。 然後，您可以配AEM置工作流模型以將資料儲存外部化，以將其連接到Azure儲存伺服器。

### 建立 [!DNL Azure] 儲存配置 {#create-azure-storage-configuration}

在執行這些步驟之前，請確保 [!DNL Azure] 儲存帳戶和訪問密鑰，以授權對 [!DNL Azure] 儲存帳戶。

執行以下步驟建立 [!DNL Azure] 儲存配置：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存]**。
1. 選擇要建立配置的資料夾並點擊 **[!UICONTROL 建立]**。
1. 在中為配置指定標題 **[!UICONTROL 標題]** 的子菜單。
1. 指定 [!DNL Azure] 儲存帳戶 **[!UICONTROL Azure儲存帳戶]** 的子菜單。
1. 指定在中訪問Azure儲存帳戶的密鑰 **[!UICONTROL Azure訪問密鑰]** 欄位和攻擊 **[!UICONTROL 保存]**。

### 為工作流配置統一儲存連AEM接器 {#configure-unified-storage-connector-workflows}

執行以下步驟以配置工作流的統一儲存連AEM接器：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一儲存連接器]**。

1. 在 **[!UICONTROL 工作流]** ，選擇 **[!UICONTROL Azure]** 從「儲存」下拉清單中。
1. 指定 [Azure儲存配置的配置路徑](#create-azure-storage-configuration) 的 **[!UICONTROL 儲存配置路徑]** 的子菜單。
1. 點擊 **[!UICONTROL 發佈]** 然後點擊 **[!UICONTROL 保存]** 的子菜單。

### 為外部AEM資料儲存配置工作流模型 {#configure-workflow-external-data-storage}

執行以下步驟為外部AEM資料儲存配置工作流模型：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 選擇模型名稱並點擊 **[!UICONTROL 編輯]**。
1. 點擊「頁面資訊」表徵圖，然後點擊 **[!UICONTROL 開啟屬性]**。
1. 選擇 **[!UICONTROL 將工作流資料儲存外部化]**。
1. 點擊 **[!UICONTROL 保存並關閉]** 的子菜單。

>[!NOTE]
>
>在為外部資料儲存配置工作流模型時，將「分配任務」步驟另存為草稿並檢索「分配任務」步驟歷史記錄的選項AEM將被禁用。

### 外部資料AEM儲存的工作流指南 {#guidelines-workflows-external-data-storage}

以下是使用工作流並將資料儲存AEM到外部資料儲存(如MicrosoftAzure儲存伺服器)時的指導原則：

* 在工作流模型步驟中定義輸入和輸出資料檔案和附件時，使用變數來儲存資料。 不選擇 **[!UICONTROL 相對於負載]** 和 **[!UICONTROL 在絕對路徑上可用]** 頁籤 的 **[!UICONTROL 相對於負載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項在您 [為外部AEM資料儲存配置工作流模型](#configure-workflow-external-data-storage)。

* 在向工作流提交自適應表單時，使用變數來儲存資料檔案和附AEM件。 不選擇 **[!UICONTROL 相對於負載]** 的子菜單。 的 **[!UICONTROL 相對於負載]** 選項在 [為外部AEM資料儲存配置工作流模型](#configure-workflow-external-data-storage)。

* 不要在工作流模AEM型中使用自定義工作流步驟將資料儲存在CRX DE儲存庫中。

* 當你 [為外部AEM資料儲存配置工作流模型](#configure-workflow-external-data-storage)，不要為收件箱建立自定義列AEM，因為如果收件箱中的工作項屬於標籤為外部儲存的工作流，則不會回遷自定義列的值AEM。