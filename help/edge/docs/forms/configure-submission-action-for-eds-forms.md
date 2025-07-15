---
title: 透過 Edge Delivery Services 設定 AEM Forms 的提交動作
description: 了解如何使用 Edge Delivery Services 設定 AEM Forms 中的提交動作。選擇表單提交服務或 AEM Publish 提交動作，安全有效率地處理表單資料。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 99%

---

# 設定表單提交：資料的去處為何？

使用者按一下表單上的「**提交**」之後，您需要告訴 Edge Delivery Services 該如何處理這些資料。您有兩個主要選項︰

## 方法 1：使用 AEM Forms 提交服務 (簡易)

這項服務適合常見、簡單的動作，例如將資料傳送至試算表或電子郵件。

**這項服務的內容及所能提供的協助為何？**

[表單提交服務](/help/forms/forms-submission-service.md)是 Adobe 託管的端點。當您的表單將資料提交至該服務後，其會接管並執行預先設定的動作。這項服務的設定方式相當容易。您可以設定：提交至試算表或電子郵件：

* **提交至試算表：**&#x200B;自動將所提交的表單資料新增為 Google Sheet 或 Microsoft Excel 檔案中新的一列 (儲存於 OneDrive 或 SharePoint 上)。
* **傳送電子郵件：**&#x200B;將內含表單資料的電子郵件傳送至您指定的一個或多個電子郵件地址。

#### 重要：進行設定所需的條件

* **試算表存取權：**&#x200B;若要將資料傳送至 OneDrive/SharePoint 上的 Google Sheet 或 Excel 檔案，Adobe 服務帳戶 (大多為 `forms@adobe.com`) 通常需要該特定試算表的&#x200B;**編輯權限**。
* **搶先體驗計劃：**&#x200B;這項服務的某些功能 (尤其是試算表相關功能)，可能屬於搶先體驗計劃的一部分。您可能需要傳送電子郵件至 `aem-forms-ea@adobe.com`，或填寫含有專案詳細資料的特定 Adobe 表單來請求存取權。請務必查看最新的 Adobe 文件。

**表單提交服務流程圖**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->
![表單提交](/help/forms/assets/eds-fss.png)

此流程圖呈現出表單提交服務如何取得所提交的資料，以及將其傳送至已設定的試算表或電子郵件。

## 方法 2：提交至您的 AEM Publish 執行個體 (進階)

對於較複雜的需求，[表單 (尤其是以通用編輯器所建立的表單) 可以將資料直接傳送至您的 AEM as a Cloud Service Publish 執行個體](/help/forms/configure-submit-actions-core-components.md)。這能發揮 AEM 的完整後端功能。

**什麼情況下需要提交至 AEM Publish？**

* 若要於提交後觸發自訂的 AEM 工作流程。
* 若要使用 AEM Form 資料模型 (FDM) 與資料庫或其他企業系統進行整合。
* 若要連接第三方服務，像是 Marketo、Microsoft Power Automate 或 Adobe Workfront Fusion。
* 若要將資料儲存在特定位置，例如 Azure Blob Storage 或 SharePoint 清單/文件資料庫 (而非僅是簡單的試算表)。
* AEM 內具有複雜的伺服器端驗證或資料處理邏輯。

**可供使用的提交動作 (AEM Publish 提交)**

* [提交至 REST 端點](/help/forms/configure-submit-action-restpoint.md)
* [傳送電子郵件 (使用 AEM 的郵件服務)](/help/forms/configure-submit-action-send-email.md)
* [使用表單資料模型 (FDM) 提交](/help/forms/configure-data-sources.md)
* [叫用 AEM 工作流程](/help/forms/aem-forms-workflow-step-reference.md)
* [提交至 SharePoint (以清單項目或文件形式)](/help/forms/configure-submit-action-sharepoint.md)
* [提交至 OneDrive (以文件形式)](/help/forms/configure-submit-action-onedrive.md)
* [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [提交至Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> 即使是從 AEM Publish 將目標選擇為 Google Sheet/Excel，其中也包含與直接的表單提交服務不同的設定步驟。

**AEM Publish 提交流程圖**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![AEM Publish 提交流程圖](/help/forms/assets/eds-aem-publish.png)
此流程圖呈現出表單提交至 AEM Publish，以及該處接續處理的複雜後端任務。

### 表單提交服務與 AEM Publish 提交的比較

| 功能 | 表單提交服務 | AEM Publish 提交 |
| :- | :- | :-- |
| **最適合** | 簡單地將資料擷取至試算表、電子郵件通知 | 複雜的工作流程、企業整合、自訂邏輯 |
| **表單製作** | 最適合文件型內容；適合簡單的 UE 表單 | 最適合以通用編輯器所製作的表單 |
| **設定工作量** | 低 (通常為簡單設定) | 較高 (需要 AEM Publish、Dispatcher、OSGi、CDN 設定) |
| **後端系統** | Adobe 託管服務 | 您的 AEM as a Cloud Service Publish 執行個體 |
| **靈活性** | 僅限於 Sheet/電子郵件 | 非常靈活，全方位的 AEM Forms 動作 |
| **範例** | 將聯絡表單資料連結至 Google Sheet | 觸發 AEM 核准工作流程的貸款申請 |

## 如何跨不同網站或頁面嵌入表單

有時，您會希望在不同的網頁或網站上，顯示自同一個地方 (例如，中心「表單網站」) 所建立和管理的表單。

### 嵌入表單的可能原因有哪些？

* 您有一個以通用編輯器建立的標準「聯絡我們」表單，需要出現在透過文件型製作所建置的多個登陸頁面上。
* 您網站的主要內容位於文件製作 (DA) 中，而您需要納入一個專門的表單。
* 您希望在多個不同的 EDS 專案中重複使用維護良好的單一表單。

### 表單嵌入作業的技術原理

您希望表單出現的頁面 (接下來稱之為「主機頁面」) 會包含一些程式碼 (通常是特殊的區塊或指令碼)。使用者造訪主機頁面時，此程式碼會向託管實際表單的 URL (接下來稱之為「表單來源」) 發出請求。然後，表單來源會傳回其 HTML，由主機頁面將其注入並顯示出來。

**嵌入式表單架構**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->
![嵌入式表單架構](/help/forms/assets/eds-embedded-form.png)
此圖表呈現主機頁面自表單來源取得表單 HTML 並將其顯示的過程。提交會使用原始表單已設定的端點。

## 設定嵌入式表單的 CORS

[CORS (跨來源資源共用)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) 是一種瀏覽器安全性功能。如果您的主機頁面 (例如，`site-a.com`) 嘗試從不同的網域取得表單 (例如，`forms-site-b.com`)，瀏覽器會將其封鎖，除非 `forms-site-b.com` 透過 CORS 標頭明確地允許它。

若&#x200B;**表單來源伺服器**&#x200B;未具備正確的 CORS 標頭，瀏覽器會阻止主機頁面載入表單，因此您所嵌入的表單將不會出現。

### 如何在提供表單服務的網站上設定 CORS？

您需要設定託管&#x200B;**表單來源**&#x200B;的伺服器，藉以在其回應中傳送特定的 HTTP 標頭。具體方法取決於您的 EDS 設定 (例如，針對 Franklin 專案，通常會是於 GitHub 存放庫中控制 CDN 行為或 Edge 工作程式邏輯的 `helix-config.yaml` 或類似設定檔中完成)。
用於新增至表單來源回應的主要標頭如下：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (例如，`https://your-site.com`)。若為測試目的，您可以使用 `*`，但若用於生產，請指定確切的網域。
* `Access-Control-Allow-Methods: GET, OPTIONS` (若表單提交本身亦屬於跨來源形式，您可能會需要 `POST`，但提交基本上會是獨立且通常同來源或專門設定的端點)。
* `Access-Control-Allow-Headers: Content-Type` (以及您表單取得過程中可能使用的任何其他自訂標頭)。

**範例 (設定檔案的概念)：**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## 其他考量：CDN 和多個程式碼庫 (Helix 4)

* **CDN 規則：**&#x200B;您的 CDN 可能會提供代理請求的途徑。例如，向 `host-page.com/embedded-form` 的請求可以透過 CDN 內部路由取得內容 `form-source.com/actual-form`，使其在瀏覽器中看起來為相同來源。設定方式可能很複雜。
* **多個程式碼庫 (Helix 4)：**&#x200B;若您的主機頁面和表單來源位於不同的 GitHub 存放庫 (這在 Helix 4 設定中很常見)，請確保轉譯或管理表單所需的任何 JavaScript「表單區塊」在主機頁面的程式碼庫中皆可供使用，或者自表單來源所取得的表單 HTML 皆包含其所有必要的 JavaScript。來源文件提到，對於「具有不同程式碼庫的 helix4，需要在兩個程式碼庫上都新增 Form 區塊」。

### 常見的架構設定與設定步驟

以下為設定表單的一些常用方法，並結合製作方法和提交策略，以及主要設定點。

#### 搭配試算表/電子郵件提交功能的文件型表單

此為最簡單的設定。您在 Word/Google Docs 中建立表單，其便會透過表單提交服務將資料提交至試算表或電子郵件。

1. 使用指定的表格結構或表單區塊在 Word/Google Doc/Sheet 中定義您的表單。
1. 在文件 (或相關設定) 中，指定表單提交服務的目標試算表 URL 或電子郵件地址。
1. 確保 `forms@adobe.com` (或相關的服務帳戶) 具有目標試算表的編輯存取權。
1. 將文件發佈至您的 Edge Delivery 網站。

**文件型 + 表單提交服務架構**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![文件型 + 表單提交服務架構](/help/forms/assets/eds-doc-fss.png)

#### 搭配試算表/電子郵件提交功能的通用編輯器表單

您會使用視覺化通用編輯器建置表單，但仍以簡單的表單提交服務擷取資料。

1. 在 AEM 中使用通用編輯器建立表單。
1. 在 UE 中設定表單的提交動作，使用「提交至表單提交服務」選項。
1. 指定目標試算表 URL 或電子郵件地址。
1. 若使用試算表，請確保 `forms@adobe.com` 具有編輯存取權。
1. 將內含表單的頁面自 AEM 發佈到您的 Edge Delivery 網站。

   **通用編輯器 + 表單提交服務架構**

   ![通用編輯器 + 表單提交服務架構](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### 搭配 AEM 發佈提交功能的通用編輯器表單 (進階)

此設定使用通用編輯器建立表單，並使用 AEM Publish 執行個體進行強大的後端處理 (工作流程、FDM 等)。需要更多的設定步驟。

1. **在 UE 中建立表單：**&#x200B;於通用編輯器中建立表單。將其提交動作設定為指向 AEM Forms 動作 (例如，「叫用 AEM 工作流程」、「使用表單資料模型提交」)。
1. **AEM Dispatcher 設定 (於 AEM Publish 層級上)：**
   * **無重新導向：**&#x200B;確保您的 Dispatcher 規則&#x200B;*不會*&#x200B;將對 `/adobe/forms/af/submit/...` 路徑發出的請求重新導向。
   * **允許提交：**&#x200B;修改您的 Dispatcher 篩選器 (例如，在 `filters.any` 中)，藉以明確定義從您的 Edge Delivery 網站網域或 IP 位址向 `/adobe/forms/af/submit/...` 發送的 `allow` POST 請求。
1. **AEM 中的 OSGi 反向連結篩選器 (於 AEM Publish 層級上)：**
   * 在 AEM OSGi 控制台 (`/system/console/configMgr`) 中，找到並設定「Apache Sling 反向連結篩選器」。
   * 將您的 Edge Delivery 網站網域 (例如，`https://your-eds-domain.hlx.page`、`https://your-custom-eds-domain.com`) 新增至「允許主機」或「允許主機 RegExp」清單。此操作會告知 AEM 接受來自您 EDS 網站的提交。
1. **CDN 重新導向規則 (於 Edge Delivery CDN 上)：**
   * 您的 Edge Delivery 網站 (例如，`your-eds-domain.hlx.page`) 需要將提交請求正確地路由至您的 AEM Publish 執行個體。
   * 當您 EDS 頁面上的表單提交後，其可能會以類似 `/adobe/forms/af/submit/...` 的相對路徑為目標。您需要在 Edge Delivery CDN (或 Edge 工作程式) 上訂立一條規則，規定：「如果請求到達 `your-eds-domain.hlx.page/adobe/forms/af/submit/...`，將其轉寄 (代理或重新導向) 至 `your-aem-publish-instance.com/adobe/forms/af/submit/...`」。
   * 具體實施方式取決於您的 CDN 提供者 (例如，Fastly VCL、Akamai Property Manager、Cloudflare Workers)。
1. **(選用) `constants.js` 用於開發 (於 EDS 專案程式碼庫中)：**
   * 針對本機開發，或者如果您的用戶端表單指令碼需要得知完整的 AEM Publish URL，您可以在 Edge Delivery 專案 GitHub 存放庫中的 `constants.js` 或類似設定檔案中進行設定。範例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **發佈：**&#x200B;將您的表單頁面從 AEM 發佈至 EDS，並確保所有 AEM 設定在您的 AEM Publish 執行個體上屬於使用中狀態。

   **通用編輯器 + AEM Publish 架構**

![通用編輯器 + AEM Publish 架構](/help/forms/assets/eds-aem-publish.png)

此架構圖呈現出以下流程：使用者在 EDS 網站上提交，CDN 路由至 AEM Dispatcher，然後 AEM Publish 進行處理。

#### 將表單嵌入文件製作 (DA) 頁面

您的主要網站內容會於文件製作 (DA) 中建立。您可以使用文件型製作或通用編輯器分別建立表單，然後將其嵌入至您的 DA 頁面中。

1. **建立與發佈表單：**
   * 使用文件型製作或通用編輯器建立表單。
   * 設定其提交方法 (根據設定 1、2 或 3，設定為表單提交服務或 AEM Publish)。
   * 發佈此表單，使其在自身的 Edge Delivery URL (例如，`.../forms/my-special-form`) 上生效。
1. **設定 CORS：**&#x200B;在託管此獨立表單的 Edge Delivery 網站/專案上，確保設定好 CORS 標頭，讓您的文件製作網站網域能夠取得它。
1. **DA 中的製作頁面：**&#x200B;在文件製作中建立或編輯您的頁面。
1. **嵌入表單區塊：**&#x200B;使用 DA 中的相應區塊嵌入外部 URL。將此區塊指向獨立發佈之表單的 URL。
1. **發佈 DA 頁面：**&#x200B;發佈您的 DA 頁面。現在其便能夠取得並顯示表單。

   **嵌入 DA 架構的表單**

   ![嵌入 DA 架構的表單](/help/forms/assets/eds-forms-embedd-da.png)

   此架構圖呈現出 DA 頁面從另一個 EDS 位置提取表單。已嵌入的表單會處理其自己的提交。

## 疑難排解

* **我的表單提交未生效。**
   * **查看控制台錯誤：**&#x200B;開啟瀏覽器的開發人員控制台 (通常為 F12)，並尋找「網路」索引標籤或「控制台」標籤上的提交相關錯誤。
   * **驗證提交 URL：**&#x200B;表單是否嘗試提交至正確的端點 (表單提交服務 URL 或您的 AEM Publish 路徑)？
   * **表單提交服務：**&#x200B;若為傳送至試算表，`forms@adobe.com` 是否已授予編輯存取權？試算表 URL 是否正確？
   * **AEM Publish 提交：**
      * 您的 Dispatcher 是否允許至 `/adobe/forms/af/submit/...` 的 POST？
      * AEM Publish 上的 Sling 反向連結篩選器是否設定為允許您的 EDS 網域？
      * 您的 CDN 重新導向規則 `/adobe/forms/af/submit/...` 是否正常運作？

* **嵌入的表單沒有出現。**

   * **CORS！**&#x200B;這是最常見的原因。確認瀏覽器控制台是否有 CORS 錯誤。確保&#x200B;*託管*&#x200B;表單的網站具有正確的 `Access-Control-Allow-Origin` 標頭。
   * **表單 URL 是否正確？**&#x200B;主機頁面上的嵌入程式碼是否指向表單的正確即時 URL？
   * **JavaScript 區塊：**&#x200B;若表單依賴特定的 JavaScript「表單區塊」進行轉譯，該區塊的程式碼是否可以在主機頁面上使用？

* **提交至 AEM Publish 時，出現「403 禁止」或「401 未授權」。**

   * 這通常表示 AEM Publish 上的 Sling 反向連結篩選器不允許來自您 EDS 網域的請求。再次檢查其設定。
   * 若您的 AEM 提交端點有驗證/授權的需要，也可能是此類問題，雖然標準表單提交通常是匿名的。

## 後續步驟

本指南的內容概述了如何搭配 AEM Edge Delivery Services 使用表單。有關具體設定的更詳細逐步說明，請參閱 Adobe Experience Manager 官方文件：

* [文件型製作與 Edge Delivery Services 表單](/help/edge/docs/forms/tutorial.md)
* [通用編輯器與 Edge Delivery Services 表單](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文件製作 (DA) 和嵌入內容](https://www.aem.live/developer/da-tutorial)
* [AEM 表單提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
