---
title: AEM Forms as a Cloud Service通訊API
description: 在雲端中使用AEM Forms Communication API產生、控制及保護檔案
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 3%

---


# AEM Forms as a Cloud Service通訊API {#communications-apis-overview}

> **版本可用性**
>
> * **AEM 6.5**： [AEM檔案服務總覽](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html)
> * **AEM as a Cloud Service**：此文章

## 簡介

AEM Forms as a Cloud Service中的通訊API可幫助您根據業務需求建立品牌核准、個人化和標準化的檔案。 這些強大的API可讓您以程式設計方式產生、控制及保護檔案，無論是隨選還是大量批次處理中。


### 主要優點

* **簡化檔案產生** — 將範本與客戶資料合併，以建立個人化檔案
* **強大的檔案操作** — 以程式設計方式組合、重新排列及驗證PDF檔案
* **彈性的部署選項** — 使用隨選API滿足低延遲需求，或使用批次API進行高輸送量作業
* **增強式安全性** — 套用數位簽章、憑證和加密，以保護機密檔案
* **雲端原生架構** — 利用可擴充、安全的雲端基礎結構，不需維護額外費用

## 主要功能

通訊API提供了一組完整的檔案處理功能，並歸納為下列功能區域：


| 檔案產生 | 檔案操作 | 檔案擷取 | 檔案轉換 | 檔案Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| 將範本與多種格式(包括PDF和列印格式)的資料合併，以產生個人化檔案。 | 以程式設計方式組合、重新排列和驗證PDF檔案，以建立新的檔案套件。 | 從PDF檔案擷取屬性、中繼資料和內容，以供進一步處理。 | 轉換不同格式的檔案，包括針對封存需求進行PDF/A合規性驗證。 | 套用數位簽章、憑證和加密，以保全和保護檔案。 |

## 檔案產生

Communications document generation API將範本(XFA或PDF)與客戶資料(XML)相結合，以在PDF和各種列印格式(PS、PCL、DPL、IPL、ZPL)中建立個人化檔案。

### 檔案產生的運作方式

典型的工作流程包括：

1. 使用[Designer](use-forms-designer.md)建立範本
2. 正在準備XML資料以填入範本
3. 使用Communications API將範本與資料合併
4. 產生所需格式的輸出檔案

![通訊文件產生工作流程](assets/communicaions-workflow.png)

### 建立PDF檔案

檔案產生API可讓您將XML資料與表單範本合併，以建立非互動式PDF檔案：

![建立PDF檔案](assets/outPutPDF_popup.png)

您可以透過下載將產生的PDF傳遞給使用者、將其儲存在存放庫中，或選擇上傳到Azure Blob儲存體。

<span class="preview">可透過[早期採用者計畫](/help/forms/early-access-ea-features.md)將產生的PDF上傳至Azure Blob儲存體。 透過您的正式電子郵件聯絡aem-forms-ea@adobe.com以加入。</span>

### 建立列印格式檔案

產生列印格式的檔案，包括：
* PostScript (PS)
* 印表機命令語言(PCL)
* 斑馬列印語言(ZPL)

這些格式適合大量列印作業及特殊列印需求。

### 多份檔案的批次處理

使用批次API有效地處理大量檔案：

![批次處理工作流程](assets/ou_OutputBatchMany_popup.png)

批次處理可讓您：

* 為XML資料來源中的每個記錄產生個別的檔案
* 以非同步方式處理檔案，以提升效能
* 設定批次處理的各種轉換引數

## 檔案操作

檔案操作API可協助您以程式設計方式組合、重新排列和轉換PDF檔案。

### 檔案元件

將多個PDF或XDP檔案合併為單一有凝聚力的檔案：

![從多個PDF檔案組合一個簡單的PDF檔案](assets/as_document_assembly.png)

檔案元件功能包括：
* 從多個來源建立簡單PDF檔案
* 建立PDF產品組合
* 組合加密檔案
* 新增合法檔案的Bates編號
* 平面化和組合互動式表單

### 檔案解壓縮

將大型PDF檔案劃分為較小、更易於管理的元件：

![根據書籤將來原始檔分割成多份檔案](assets/as_intro_pdfsfrombookmarks.png)

檔案反組分解可讓您：
* 從來原始檔擷取特定頁面
* 根據書籤分割檔案
* 從大型編譯建立邏輯檔案集

>[!NOTE]
>
> AEM Forms包含許多內建字型，可與PDF檔案順暢整合。 如需支援字型的完整清單，[請按一下這裡](/help/forms/supported-out-of-the-box-fonts.md)。

## 檔案擷取

<span class="preview">可透過[早期採用者方案](/help/forms/early-access-ea-features.md)使用檔案擷取。 透過您的正式電子郵件聯絡aem-forms-ea@adobe.com以加入。</span>

檔案擷取API可讓您從PDF檔案中擷取資訊，包括：

* 檔案屬性（是否為可填寫的表單、是否有附件等）
* 使用許可權和許可權
* 使用Adobe可延伸中繼資料平台(XMP)的中繼資料資訊

此功能在檔案管理系統、封存解決方案和工作流程自動化方面特別有用。

## 檔案轉換

### PDF/A轉換和驗證

將標準PDF檔案轉換為PDF/A格式以供長期封存之用：

* 支援PDF/A-1a、1b、2a、2b、3a及3b法規遵循標準
* 驗證PDF/A合規性
* 使用嵌入字型和未壓縮內容保持檔案完整性

### PDF至XDP轉換

<span class="preview">可透過[早期採用者計畫](/help/forms/early-access-ea-features.md)將PDF轉換為XDP。 透過您的正式電子郵件聯絡aem-forms-ea@adobe.com以加入。</span>

將包含XFA串流的PDF檔案轉換為XDP格式，以便編輯和重複使用範本。

## 檔案Assurance {#doc-assurance}

檔案Assurance包含簽名和加密API，可在檔案的整個生命週期中保護您的檔案。

### 簽名API

使用數位簽名和憑證保護PDF檔案：

* 新增可見或隱藏的簽名欄位
* 數位簽署簽名欄位
* 驗證檔案完整性
* 從檔案移除簽章
* 從檔案中刪除簽名欄位

<span class="preview">可透過[早期採用者程式](/help/forms/early-access-ea-features.md)移除簽章及刪除簽章欄位。 透過您的正式電子郵件聯絡aem-forms-ea@adobe.com以加入。</span>

### 加密API

使用加密保護檔案內容：

* 使用密碼加密PDF檔案
* 移除以密碼為基礎的加密
* 決定套用至檔案的安全性型別
* 從受保護檔案擷取安全性資訊

### 檔案公用程式 {#doc-utility}

檔案公用程式提供使用PDF檔案的其他功能：

#### 使用許可權API (Reader擴充功能)

<span class="preview">使用許可權(Reader擴充功能)可透過[早期採用者計畫](/help/forms/early-access-ea-features.md)取得。 透過您的正式電子郵件聯絡aem-forms-ea@adobe.com以加入。</span>

透過新增使用許可權至PDF檔案來擴充Adobe Reader的功能，啟用如下的功能：

* 表單填寫和儲存
* 新增註釋和註解
* 數位簽署
* 檔案附件
* 表單資料匯入/匯出
* 存取網站服務和資料庫

可用的使用許可權包括：

* **表單互動**：表單填寫、表單資料匯入/匯出、動態表單欄位/頁面
* **註解**：註解（線上及離線）、數位簽章
* **檔案處理**：內嵌檔案，送出獨立，條碼解碼
* **線上服務**：線上Forms，存取網站服務

## 通訊API的型別 {#types}

通訊提供兩種型別的API以符合不同的使用案例：

### 同步API

**最適合**：隨選、低延遲、單一檔案產生
**使用案例**：使用者觸發的檔案產生、互動式應用程式
**檔案**： [同步API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### 批次API （非同步）

**最適合**：已排程、高輸送量、多檔案產生
**使用案例**：月結單、帳單、通知、排程報告
**檔案**： [批次API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## 通訊API快速入門

### 上線流程

通訊以獨立模組或附加元件的形式提供給Forms as a Cloud Service使用者：

1. 聯絡Adobe銷售或您的Adobe代表以要求存取權
2. Adobe將為您的組織啟用存取權並授予管理員許可權
3. 然後，您的管理員可以授予組織中的開發人員存取權

### 在您的環境中啟用通訊

請依照下列步驟，為您的Forms as a Cloud Service環境啟用通訊：

1. 登入Cloud Manager並開啟AEM Forms as a Cloud Service執行個體
2. 開啟編輯計畫選項，然後前往解決方案和附加元件索引標籤
3. 選取&#x200B;**[!UICONTROL Forms — 通訊]**&#x200B;選項

   ![通訊](assets/communications.png)

   如果您已啟用&#x200B;**[!UICONTROL Forms — 數位註冊]**，請改為選取&#x200B;**[!UICONTROL Forms — 通訊附加元件]**&#x200B;選項。

   ![附加元件](assets/add-on.png)

4. 按一下&#x200B;**[!UICONTROL 更新]**
5. 執行建置管道 — 通訊API將在成功完成後啟用

>[!NOTE]
>
> 若要啟用檔案操作API，請將下列規則新增至您的[Dispatcher設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## API參考檔案 {#api-reference}

通訊API可組織成數個功能類別，每個類別都有詳細的參考檔案。 這些API參考資料提供有關端點、引數、請求/回應格式和驗證要求的完整資訊。

### Document Generation API

| API | 描述 | 參考連結 |
|-----|-------------|----------------|
| 檔案產生 — 同步 | 針對互動式案例，以低延遲隨選產生檔案 | [API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| 檔案產生 — 批次 | 以非同步方式處理排程作業的大量檔案 | [API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### Document Manipulation API

| API | 描述 | 參考連結 |
|-----|-------------|----------------|
| 檔案操作 — 同步 | 使用DDX指示組合、分割及轉換PDF檔案 | [API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### 檔案Assurance API

| API | 描述 | 參考連結 |
|-----|-------------|----------------|
| DocAssurance — 同步 | 套用數位簽名、認證、加密和Reader延伸模組 | [API參考](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### 常見API引數

每個API類別都有特定的引數，但部分常見引數包括：

#### 檔案產生引數

| 參數 | 類型 | 必要 | 描述 |
|-----------|------|----------|-------------|
| `template` | 字串 | 是 | xdp或PDF範本檔案的路徑 |
| `data` | 字串 | 否 | 要與範本合併的XML資料 |
| `outputOptions` | 物件 | 否 | 輸出檔案的組態選項 |

#### 檔案操作引數

| 參數 | 類型 | 必要 | 描述 |
|-----------|------|----------|-------------|
| `ddx` | 字串 | 是 | 檔案元件或反組譯的DDX指示 |
| `inputDocuments` | 物件 | 是 | 要處理的輸入檔案地圖 |
| `outputOptions` | 物件 | 否 | 輸出檔案的組態選項 |

#### 檔案Assurance引數

| 參數 | 類型 | 必要 | 描述 |
|-----------|------|----------|-------------|
| `inputPDF` | 字串 | 是 | 輸入要加密或簽署的PDF檔案 |
| `certificateAlias` | 字串 | 條件式 | 用於簽署作業的憑證別名 |
| `credentialPassword` | 字串 | 條件式 | 用於簽章的認證密碼 |

如需完整的引數詳細資料、驗證需求和請求/回應範例，請參閱上表連結的特定API參考檔案。

## 其他資源 {#see-also}

* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service架構](/help/forms/aem-forms-cloud-service-architecture.md)
* [API參考檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [早期採用者計畫功能](/help/forms/early-access-ea-features.md)
