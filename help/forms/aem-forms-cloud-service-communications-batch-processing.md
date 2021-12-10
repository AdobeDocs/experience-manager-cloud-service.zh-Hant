---
title: Experience Manager [!DNL Forms] as a Cloud Service通訊批次處理
description: 如何建立以品牌為導向的個人化通訊？
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 0%

---

# Formsas a Cloud Service通訊 — 批次處理

通信允許您建立、組合和提供面向品牌的個性化通信，如業務通信、文檔、對帳單、理賠處理信函、福利通知、理賠處理信函、每月賬單和歡迎套件。 您可以使用通信API將模板(XFA或PDF)與客戶資料結合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

通訊提供API，以供隨選和排程的檔案產生。 您可以針對隨需和批次API（非同步API）使用同步API，以排程產生檔案：

* 同步API適用於隨需、低延遲和單記錄檔案產生使用案例。 這些API更適合使用者動作的使用案例。 例如，在用戶填寫表單後生成文檔。

* 批次API（非同步API）適用於排程的高吞吐量多檔案產生使用案例。 這些API會以批次產生檔案。 例如，每月生成電話賬單、信用卡對帳單和福利對帳單。

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## 批處理操作 {#batch-operations}

批處理操作是按計畫間隔為一組記錄生成多個類似類型的文檔的過程。 批工序包含兩個部分：配置（定義）和執行。

* **配置（定義）**:批次設定會儲存各種資產和屬性的相關資訊，以針對產生的檔案進行設定。 例如，它提供有關XDP或PDF範本的詳細資訊，以及要使用的客戶資料的位置，並指定輸出PDF檔案的各種屬性。

* **執行**:要啟動批處理操作，請指定運行並將批處理配置名稱傳遞到批處理執行API。

### 批操作的元件 {#components-of-a-batch-operations}

**雲端設定**:Experience Manager Cloud設定可協助您將Experience Manager執行個體連結至客戶擁有的Microsoft Azure Storage。 它可讓您指定客戶擁有的Microsoft Azure帳戶的憑證，以便連線至該帳戶。

**批次資料儲存配置(USC)**:批次資料設定可協助您為批次API設定Blob儲存的特定例項。 它可讓您在客戶擁有的Microsoft Azure Blob儲存體中指定輸入和輸出位置。

**批次API**:可讓您建立批配置並根據這些配置執行批運行，以建立並執行批操作，以將PDF或XDP模板與資料合併，並以PDF、PS、PCL、DPL、IPL和ZPL格式生成輸出。 通訊提供批次API，以執行建立、讀取、更新和刪除操作。

![資料合併表](assets/communications-batch-structure.png)

**儲存**:通訊API使用客戶擁有的Microsoft Azure Cloud儲存空間，擷取客戶記錄並儲存產生的檔案。 您可以在「Microsoft設定」中設定Experience Manager Cloud Service Azure Storage。

**應用程式**:您的自訂應用程式，以使用批次API來產生和使用檔案。

## 使用批處理工序生成多個文檔 {#generate-multiple-documents-using-batch-operations}

您可以使用批處理操作以計畫的間隔生成多個文檔。

>[!VIDEO](https://video.tv.adobe.com/v/337425)

您可以觀看影片或執行以下指示，了解如何使用批次作業產生檔案。 影片中使用的API參考檔案以.yaml格式提供。 您可以下載 [批次API](assets/batch-api.yaml) 檔案並上傳至Postman，以檢查API的功能，並隨附影片。

### 先決條件 {#pre-requisites}

若要使用批次API，需執行下列操作：

* [Microsoft Azure儲存帳戶](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* PDF或XDP範本
* [要與範本合併的資料](#form-data)
* 具有Experience Manager管理員權限的用戶

### 設定您的環境 {#setup-your-environment}

使用批工序之前：

* 上傳客戶資料（XML檔案）至Microsoft Azure Blob儲存
* 建立雲端設定
* 建立批次資料儲存配置
* 將範本和其他資產上傳至您的Experience Manager FormsCloud Service例項

### 將客戶資料（XML檔案）上傳至Azure儲存 {#upload-customer-data-to-Azure-Storage}

在您的Microsoft Azure儲存上，建立 [容器](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) 和 [上傳客戶資料(XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) 到 [資料夾](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) 內。
>[!NOTE]
>
>您可以設定Microsoft Azure儲存空間，以自動清除輸入資料夾，或以排程間隔將輸出資料夾的內容移至不同位置。 但是，請確保當引用資料夾的批處理操作仍在運行時不會清理資料夾。

### 建立雲端設定 {#create-a-cloud-configuration}

雲端設定會將您的Experience Manager執行個體連線至Microsoft Azure Storage。 若要建立雲端設定：

1. 前往「工具>Cloud Services> Azure Storage」
1. 開啟資料夾以托管配置，然後按一下「建立」。 使用全局資料夾或建立資料夾。
1. 指定連接到服務的配置和憑據的名稱。 您可以 [從您的Microsoft Azure儲存入口網站擷取這些憑證](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. 按一下建立。

您的Experience Manager例項現在已準備好連線至Microsoft Azure Storage，並視需要使用它來儲存和讀取內容。

### 建立批次資料儲存配置 {#create-batch-data-store-configuration}

批次資料設定可協助您設定容器和資料夾以進行輸入和輸出。 您將客戶記錄保留在「源資料夾」中，並將生成的文檔放在「目標資料夾」中。

若要建立設定：

1. 前往「工具」>「Forms」>「輸出批次」 — 「統一儲存連接器」。
1. 開啟資料夾以托管配置，然後按一下「建立」。 使用全局資料夾或建立資料夾。
1. 指定設定的標題和名稱。 在儲存中，選取Microsoft Azure Storage。
1. 在儲存配置路徑中，瀏覽並選擇包含客戶擁有的Azure儲存帳戶憑據的雲配置。
1. 在源資料夾中，指定Azure儲存容器的名稱和包含記錄的資料夾。
1. 在目標資料夾中，指定Azure儲存容器的路徑和資料夾，以儲存生成的文檔。
1. 按一下建立。

您的Experience Manager執行個體現在已連線至Microsoft Azure Storage，並已設定為擷取資料，並將資料傳送至Microsoft Azure儲存上的特定位置。

### 上傳範本和其他資產至您的Experience Manager例項 {#upload-templates-and-other-assets-to-your-AEM-instance}

組織通常有多個範本。 例如，信用卡報表、福利報表和報銷申請各一個模板。 將所有這類XDP和PDF範本上傳至您的Experience Manager執行個體。 上傳範本：

1. 開啟您的Experience Manager例項。
1. 前往Forms > Forms和檔案
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。

## 使用批次API生成文檔 {#use-batch-API-to-generate-documents}

若要使用批次API，請建立批次設定，並根據該設定執行執行。 API檔案提供建立及執行批次的API、對應參數，以及可能錯誤的相關資訊。 您可以下載 [API定義檔案](assets/batch-api.yaml) 將檔案上傳至 [郵遞員](https://go.postman.co/home) 或類似的軟體來測試API以建立和執行批次操作。

### 建立批次 {#create-a-batch}

要建立批，請使用 `GET /config` API。 在HTTP要求內文中加入下列必要屬性：


* **configName**:指定批的唯一名稱。 例如， `wknd-job`
* **dataSourceConfigUri**:指定批資料儲存配置的位置。 它可以是配置的相對路徑或絕對路徑。 例如：`/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputTypes**:指定輸出格式：PDF或打印。 如果使用PRINT輸出類型，請在 `printedOutputOptionsList` 屬性，指定至少一個打印選項。 打印選項是通過其渲染類型標識的，因此目前不允許使用具有相同渲染類型的多個打印選項。 支援的格式為PS、PCL、DPL、IPL和ZPL。

* **範本**:指定模板的絕對路徑或相對路徑。 例如， `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

如果您指定相對路徑，也提供內容根。 如需內容根目錄的詳細資訊，請參閱API檔案。

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

建立批次後，您可以使用 `GET /config /[configName]/execution/[execution-identifier]` 以查看批的詳細資訊。

### 運行批處理 {#run-a-batch}

要運行（執行）批處理，請使用 `POST /config /[configName]/execution`. 例如，要運行名為wknd-demo的批處理，請使用/config/wknd-demo/execution。 伺服器在接受請求時傳回HTTP回應代碼202。 API不會針對伺服器上執行的批次作業，在HTTP回應標題中傳回除唯一代碼（執行識別碼）以外的任何裝載。 您可以使用執行標識符來檢索批的狀態。

>[!NOTE]
>
>當批處理正在運行時，請勿對相應的源資料夾和目標資料夾、資料源配置和Microsoft Azure Cloud配置進行任何更改。

### 檢查批的狀態 {#status-of-a-batch}

要檢索批的狀態，請使用 `GET /config /[configName]/execution/[execution-identifier]`. 執行識別碼包含在批次執行請求的HTTP回應標題中。  例如，下圖顯示批處理作業的執行標識符。

狀態請求的回應包含狀態區段。 它提供了有關批處理作業的狀態、已在管道中（已讀取和正在處理）的記錄數以及每個outputType/renderType（正在處理的項數、成功和失敗的項數）的狀態的詳細資訊。 狀態還包括批處理作業的開始和結束時間以及有關錯誤的資訊（如果有）。 結束時間為–1，直到批處理運行實際完成。

>[!NOTE]
>
>* 請求多種PRINT格式時，狀態包含多個條目。 例如，PRINT/ZPL、PRINT/IPL。
>* 批處理作業不會同時讀取所有記錄，而是繼續讀取和增加記錄數。 因此，狀態會在每次執行時傳回不同數量的記錄。


### 查看生成的文檔 {#view-generated-documents}

作業完成時，將生成的文檔儲存到 `success` 資料夾（位於批次資料儲存配置中指定的目標位置）。 如果有任何錯誤，服務會建立 `failure` 檔案夾。 它提供錯誤類型和原因的相關資訊。

讓我們透過範例來了解：假設有輸入資料檔案 `record1.xml` 和兩種輸出類型： `PDF` 和 `PCL`. 然後，目標位置包含兩個子資料夾 `pdf` 和 `pcl`，每個輸出類型各一個。 假設PDF產生成功，則 `pdf` 子資料夾包含 `success` 子資料夾，該子資料夾又包含實際生成的PDF文檔 `record1.pdf`. 假設PCL生成失敗，則 `pcl` 子資料夾包含 `failure` 子資料夾中又包含錯誤檔案 `record1.error.txt` 其中包含錯誤的詳細資訊。 此外，目標位置包含名為的臨時資料夾 `__tmp__` 它保存批處理執行期間所需的某些檔案。 當沒有參考目標資料夾的活動批處理運行時，可以刪除此資料夾。

>[!NOTE]
>
>根據輸入記錄的數量和模板的複雜性，處理批處理可能需要一些時間，然後等待幾分鐘，再檢查輸出檔案的目標資料夾。

## 考量事項  {#considerations-for-communications-apis}

### 表單資料 {#form-data}

通信API接受通常在設計工具中建立的表單設計和作為輸入的XML表單資料。 要用資料填充文檔，要填充的每個表單欄位的XML表單資料中必須存在XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 不需要匹配XML元素的顯示順序。 重要因素是XML元素需指定相應的值。

請考量下列貸款申請表範例：

![貸款申請表](assets/loanFormData.png)

要將資料合併到此表單設計中，請建立與表單對應的XML資料源。 以下XML表示與抵押申請表示例對應的XML資料源。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    - <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### 支援的文檔類型 {#supported-document-types}

若要完整存取通訊API的轉譯功能，建議您使用XDP檔案作為輸入。 有時可使用PDF檔案。 不過，使用PDF檔案作為輸入有以下限制：

不包含XFA資料流的PDF文檔無法呈現為PostScript、PCL或ZPL。 通訊API可將具有XFA資料流（即在Designer中建立的表單）的PDF檔案轉譯為雷射和標籤格式。 如果PDF檔案經過簽署、認證或包含使用權限(使用AEM FormsReader擴充功能服務套用)，則無法以這些列印格式呈現。

## API參考檔案

API參考檔案提供有關API所提供所有參數、驗證方法和各種服務的詳細資訊。 API參考檔案提供.yaml格式。 您可以下載 [批次API](assets/batch-api.yaml) 檔案並上傳至Postman以檢查API的功能。

## 已知問題 {#known-issues}

* 確保資料xml檔案不包含XML聲明標頭。 例如， `<?xml version="1.0" encoding="UTF-8"?>`

* 指定PRINT時，在打印選項清單中只能指定一次特定的渲染類型。 例如，不能有兩個打印選項，每個都指定PCL呈現類型。

* 運行批處理時，請勿修改批處理配置中使用的資料源USC配置/Azure雲配置。 即使在執行後，如果需要任何更新，請建立配置副本，而不是更新現有批配置中使用的配置副本。

## 最佳作法 {#best-practices}

* Adobe建議將資料檔案blob容器儲存在Experience Manager Cloud Service使用的雲端區域中。

## 常見問題 {#faq}

**我可以使用觀看的資料夾或其他儲存機制來儲存輸入和輸出嗎？**

目前，您可以使用Microsoft Azure Storage來儲存輸入資料和產生的檔案。 Microsoft Azure儲存提供 [自動化資料移動操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Microsoft Azure儲存帳戶是否隨Experience Manager FormsCloud Service授權包含？**

Microsoft Azure儲存帳戶獨立於Experience Manager FormsCloud Service授權。

**通訊API會將資料儲存在Experience Manager FormsCloud Service伺服器上嗎？**

輸入和輸出資料僅儲存在Microsoft Azure儲存上。

**通訊API是否僅適用於Experience Manager FormsCloud Service? 我可以在內部部署環境中取得類似的功能嗎？**

您可以使用AEM Forms輸出服務將範本(XFA或PDF)與客戶資料結合，以PDF、PS、PCL和ZPL格式產生檔案。

與內部部署環境相比，本Cloud Service可提供自動擴展和成本效益的額外優勢。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**我可以同時執行多個批處理操作嗎？**
是的，您可以簡單地運行多個批處理操作。 請始終對每個操作使用不同的源資料夾和目標資料夾，以避免任何衝突。
