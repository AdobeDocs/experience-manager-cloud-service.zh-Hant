---
title: Experience Manager [!DNL Forms] as a Cloud Service通信批處理
description: 如何打造品牌導向和個性化的溝通？
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: f8f9aeb12d7a988deaf1ceed2cdf29519f8102dd
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Formsas a Cloud Service通信 — 批處理

通信允許您建立、匯編和提供面向品牌的個性化通信，如業務通信、文檔、報表、理賠信函、利益通知、理賠信函、每月帳單和歡迎套件。 您可以使用Communications API將模板(XFA或PDF)與客戶資料組合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

通信為按需和計畫文檔生成提供了API。 您可以將同步API用於按需API，而將批處理API（非同步API）用於計畫文檔生成：

* 同步API適用於按需、低延遲和單記錄文檔生成使用情形。 這些API更適合基於用戶操作的使用案例。 例如，在用戶填寫表單後生成文檔。

* 批處理API（非同步API）適用於計畫的高吞吐量多文檔生成使用情形。 這些API以批次形式生成文檔。 例如，每月生成電話單、信用卡對帳單和福利對帳單。

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## 批處理操作 {#batch-operations}

批處理操作是按預定間隔為一組記錄生成多個類似類型文檔的過程。 批處理操作包含兩個部分：配置（定義）和執行。

* **配置（定義）**:批配置儲存關於要為生成的文檔設定的各種資產和屬性的資訊。 例如，它提供了有關XDP或PDF模板以及要使用的客戶資料的位置的詳細資訊，並為輸出文檔指定了各種屬性。

* **執行**:要啟動批處理操作，請將批處理配置名稱傳遞給批處理執行API。

### 批操作的元件 {#components-of-a-batch-operations}

**雲配置**:體驗管理器雲配置可幫助您將Experience Manager實例連接到客戶擁有的MicrosoftAzure儲存。 它允許您指定客戶擁有的MicrosoftAzure帳戶的憑據以連接到它。

**批處理資料儲存配置(USC)**:批處理資料配置可幫助您為批處理API配置特定的Blob儲存實例。 它允許您指定客戶擁有的MicrosoftAzure Blob儲存中的輸入和輸出位置。

**批處理API**:允許您建立批配置並基於這些配置執行批運行，以將PDF或XDP模板與資料合併，並以PDF、PS、PCL、DPL、IPL和ZPL格式生成輸出。 通信為配置管理和批執行提供了批API。

![資料合併表](assets/communications-batch-structure.png)

**儲存**:通信API使用客戶擁有的MicrosoftAzure雲儲存來獲取客戶記錄並儲存生成的文檔。 你在「Microsoft配置」中配置Experience Manager Cloud ServiceAzure儲存。

**應用**:您的自定義應用程式使用批處理API生成和使用文檔。

## 使用批處理操作生成多個文檔 {#generate-multiple-documents-using-batch-operations}

您可以使用批處理操作按預定的間隔生成多個文檔。

>[!VIDEO](https://video.tv.adobe.com/v/338349)

您可以觀看視頻或執行以下說明，以瞭解如何使用批處理操作生成文檔。 視頻中使用的API參考文檔以.yaml格式提供。 您可以下載 [批處理API](assets/batch-api.yaml) 檔案並上傳給郵遞員，以檢查API的功能，並跟隨視頻。

### 先決條件 {#pre-requisites}

要使用批處理API，需要執行以下操作：

* [MicrosoftAzure儲存帳戶](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* PDF或XDP模板
* [要與模板合併的資料](#form-data)
* 具有Experience Manager管理員權限的用戶

### 設定環境 {#setup-your-environment}

使用批操作之前：

* 將客戶資料（XML檔案）上載到MicrosoftAzure Blob儲存
* 建立雲配置
* 建立批資料儲存配置
* 將模板和其他資產上載到您的Experience Manager FormsCloud Service實例

### 將客戶資料（XML檔案）上載到Azure儲存 {#upload-customer-data-to-Azure-Storage}

在你的MicrosoftAzure儲存上，建立 [容器](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) 和 [上載客戶資料(XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) 到 [資料夾](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) 裝箱裡。
>[!NOTE]
>
>您可以配置MicrosoftAzure儲存，以自動清除輸入資料夾或按預定時間間隔將輸出資料夾的內容移動到其他位置。 但是，確保在引用資料夾的批處理操作仍在運行時不會清除資料夾。

### 建立雲配置 {#create-a-cloud-configuration}

雲配置將你的Experience Manager實例連接到MicrosoftAzure儲存。 要建立雲配置：

1. 轉到「工具」>「Cloud Services」>「Azure儲存」
1. 開啟資料夾以承載配置，然後按一下建立。 使用全局資料夾或建立資料夾。
1. 指定連接到服務的配置和憑據的名稱。 你可以 [從你的MicrosoftAzure儲存門戶檢索這些憑據](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys)。
1. 按一下建立。

您的Experience Manager實例現在已準備好連接到MicrosoftAzure儲存，並在需要時使用它儲存和讀取內容。

### 建立批資料儲存配置 {#create-batch-data-store-configuration}

批處理資料配置可幫助您配置用於輸入和輸出的容器和資料夾。 您將客戶記錄保留在「源資料夾」中，生成的文檔將放在「目標資料夾」中。

要建立配置：

1. 轉至「工具」>「Forms」>「統一儲存連接器」。
1. 開啟資料夾以承載配置，然後按一下建立。 使用全局資料夾或建立資料夾。
1. 指定配置的標題和名稱。 在儲存中，選擇MicrosoftAzure儲存。
1. 在儲存配置路徑中，瀏覽並選擇包含客戶擁有的Azure儲存帳戶憑據的雲配置。
1. 在源資料夾中，指定Azure儲存容器的名稱和包含記錄的資料夾。
1. 在目標資料夾中，指定Azure儲存容器和資料夾的路徑以儲存生成的文檔。
1. 按一下建立。

你的Experience Manager實例現在已連接到MicrosoftAzure儲存，並配置為檢索資料並將其發送到MicrosoftAzure儲存上的特定位置。

### 將模板和其他資產上載到您的Experience Manager實例 {#upload-templates-and-other-assets-to-your-AEM-instance}

組織通常具有多個模板。 例如，信用卡對帳單、福利對帳單和索賠申請各有一個模板。 將所有此類XDP和PDF模板上載到您的Experience Manager實例。 要上載模板，請執行以下操作：

1. 開啟Experience Manager實例。
1. 轉到Forms>Forms和文檔
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立」(Create)>「檔案上載」(File Upload)並上載模板。

## 使用批處理API生成文檔 {#use-batch-API-to-generate-documents}

要使用批處理API，請建立批配置並基於該配置執行運行。 API文檔提供有關建立和運行批處理的API、相應參數和可能的錯誤的資訊。 您可以下載 [API定義檔案](assets/batch-api.yaml) 檔案並上載到 [郵遞員](https://go.postman.co/home) 或類似軟體，以testAPI來建立和運行批處理操作。

### 建立批 {#create-a-batch}

要建立批，請使用 `POST /config` API。 在HTTP請求正文中包括以下強制屬性：

* **配置名稱**:指定批的唯一名稱。 例如， `wknd-job`
* **資料源配置URI**:指定批資料儲存配置的位置。 它可以是配置的相對路徑或絕對路徑。 例如：`/conf/global/settings/forms/usc/batch/wknd-batch`
* **輸出類型**:指定輸出格式：PDF和打印。 如果使用PRINT輸出類型，請在 `printedOutputOptionsList` 屬性，至少指定一個打印選項。 打印選項由其渲染類型標識，因此目前不允許使用具有相同渲染類型的多個打印選項。 支援的格式為PS、PCL、DPL、IPL和ZPL。

* **模板**:指定模板的絕對路徑或相對路徑。 例如， `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

如果指定相對路徑，也提供內容根。 有關內容根的詳細資訊，請參見API文檔。

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

您可以使用 `GET /config /[configName]` 查看批配置的詳細資訊。

### 運行批處理 {#run-a-batch}

要運行（執行）批，請使用 `POST /config /[configName]/execution`。 例如，要運行名為wknd-demo的批處理，請使用/config/wknd-demo/execution。 伺服器在接受請求時返回HTTP響應代碼202。 API不返回伺服器上運行的批處理作業的HTTP響應報頭中唯一代碼（執行標識符）以外的任何負載。 您可以使用執行標識符來檢索批的狀態。

>[!NOTE]
>
>當批處理正在運行時，請不要對相應的源和目標資料夾、資料源配置和MicrosoftAzure雲配置進行任何更改。

### 檢查批的狀態 {#status-of-a-batch}

要檢索批的狀態，請使用 `GET /config /[configName]/execution/[execution-identifier]`。 該執行標識符包含在批處理執行請求的HTTP響應報頭中。

狀態請求的響應包含狀態部分。 它提供了有關批處理作業狀態、已在管道中（已讀取和正在處理）的記錄數以及每個outputType/renderType（正在進行、成功和失敗的項數）的狀態的詳細資訊。 狀態還包括批處理作業的開始和結束時間以及錯誤資訊（如果有）。 在批處理運行實際完成之前，結束時間為–1。

>[!NOTE]
>
>* 當您請求多個PRINT格式時，狀態包含多個條目。 例如，PRINT/ZPL、PRINT/IPL。
>* 批處理作業不會同時讀取所有記錄，而是會不斷讀取並增加記錄數。 因此，在讀取所有記錄之前，狀態將返回–1。


### 查看生成的文檔 {#view-generated-documents}

作業完成後，將生成的文檔儲存到 `success` 資料夾。 如果有任何錯誤，服務將建立 `failure` 的子菜單。 它提供了有關錯誤類型和原因的資訊。

讓我們通過一個示例來瞭解一下：假設有一個輸入資料檔案 `record1.xml` 和兩種輸出類型： `PDF` 和 `PCL`。 然後目標位置包含兩個子資料夾 `pdf` 和 `pcl`，每個輸出類型各一個。 假定PDF生成成功，然後 `pdf` 子資料夾包含 `success` 子資料夾，而子資料夾又包含實際生成的PDF文檔 `record1.pdf`。 假設PCL生成失敗，則 `pcl` 子資料夾包含 `failure` 子資料夾，而子資料夾又包含錯誤檔案 `record1.error.txt` 其中包含錯誤的詳細資訊。 此外，目標位置包含名為 `__tmp__` 包含批處理執行期間所需的某些檔案。 當沒有引用目標資料夾的活動批處理運行時，可以刪除此資料夾。

>[!NOTE]
>
>根據輸入記錄的數量和模板的複雜性，處理批處理可能需要一些時間，在檢查輸出檔案的目標資料夾之前等待幾分鐘。

## API參考文檔

API參考文檔提供了有關API提供的所有參數、驗證方法和各種服務的詳細資訊。 API參考文檔以.yaml格式提供。 您可以下載 [批處理API](assets/batch-api.yaml) 檔案並上傳到郵遞員，以檢查API的功能。
