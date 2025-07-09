---
title: 使用Edge Delivery Services設定AEM Forms的提交動作
description: 瞭解如何使用Edge Delivery Services在AEM Forms中設定提交動作。 在Forms提交服務和AEM發佈提交動作之間選擇，以安全有效地處理表單資料。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# 設定表單提交：您的資料前往何處？

使用者按一下表單上的&#x200B;**提交**&#x200B;後，您需要告訴Edge Delivery Services如何處理該資料。 您有兩個主要選項：

## 方法1：使用AEM Forms提交服務（簡化）

此服務適用於常見且直接的動作，例如傳送資料至試算表或電子郵件。

**有什麼能協助您？**

[Forms提交服務](/help/forms/forms-submission-service.md)是Adobe代管的端點。 當您的表單提交資料給它時，此服務會接管並執行預先設定的動作。 其設計易於設定。 您可以設定：提交至試算表或電子郵件：

* **提交至試算表：**&#x200B;自動將提交的表單資料新增為Google工作表或Microsoft Excel檔案(儲存在OneDrive或SharePoint上)中的新列。
* **傳送電子郵件：**&#x200B;將包含表單資料的電子郵件傳送至您指定的一個或多個電子郵件地址。

#### 重要：設定需求

* **試算表存取：**&#x200B;若要將資料傳送至OneDrive/SharePoint上的Google工作表或Excel檔案，Adobe服務帳戶（通常為`forms@adobe.com`）通常需要該特定試算表的&#x200B;**編輯許可權**。
* **搶先存取方案：**&#x200B;此服務的部分功能，尤其是試算表功能，可能屬於搶先存取方案的一部分。 您可能需要透過寄送電子郵件給`aem-forms-ea@adobe.com`或填寫包含您專案詳細資料的特定Adobe表單來請求存取權。 請務必檢視最新的Adobe檔案。

**Forms提交服務流程圖**
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

![Forms提交](/help/forms/assets/eds-fss.png)

此流程圖顯示Forms提交服務如何接受提交的資料，並將其傳送至已設定的試算表或電子郵件。

## 方法2：提交至您的AEM發佈執行個體（進階）

針對更複雜的需求，[表單（尤其是使用通用編輯器建立的表單）可以直接將資料傳送至您的AEM as a Cloud Service發佈執行個體](/help/forms/configure-submit-actions-core-components.md)。 這可解鎖AEM的完整後端功能。

**您何時需要提交至AEM Publish？**

* 在提交後觸發自訂AEM工作流程。
* 使用AEM表單資料模型(FDM)來整合資料庫或其他企業系統。
* 連線第三方服務，例如Marketo、Microsoft Power Automate或Adobe Workfront Fusion。
* 將資料儲存在Azure Blob Storage或SharePoint清單/檔案庫等特定位置（不只是簡單的試算表）。
* 當您在AEM中有複雜的伺服器端驗證或資料處理邏輯時。

**可用的提交動作(AEM發佈提交)**

* [提交至REST端點](/help/forms/configure-submit-action-restpoint.md)
* [傳送電子郵件(使用AEM的郵件服務)](/help/forms/configure-submit-action-send-email.md)
* [使用表單資料模型(FDM)提交](/help/forms/configure-data-sources.md)
* [叫用 AEM 工作流程](/help/forms/aem-forms-workflow-step-reference.md)
* [提交至SharePoint （以清單專案或檔案的形式）](/help/forms/configure-submit-action-sharepoint.md)
* [提交至OneDrive （作為檔案）](/help/forms/configure-submit-action-onedrive.md)
* [提交到 Azure Blob 儲存體](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交至Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交至Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [提交至Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> 即使從AEM Publish鎖定Google工作表/Excel，它涉及的設定步驟與直接的Forms提交服務不同。

**AEM發佈提交流程圖**

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

![AEM發佈提交流程圖](/help/forms/assets/eds-aem-publish.png)
此流程圖顯示提交至AEM Publish的表單，該表單接著會處理複雜的後端工作。

### Forms提交服務與AEM發佈提交之比較

| 功能 | Forms提交服務 | AEM發佈提交內容 |
| :- | :- | :-- |
| **最適合** | 對試算表、電子郵件通知的簡單資料擷取 | 複雜的工作流程、企業整合、自訂邏輯 |
| **表單製作** | 適用於檔案型表單；適用於簡單UE表單，則為確定 | Best for Universal Editor編寫的表單 |
| **安裝工作量** | 低（通常為簡單的設定） | 更高(需要AEM Publish、Dispatcher、OSGi、CDN設定) |
| **後端系統** | Adobe託管服務 | 您的AEM as a Cloud Service發佈執行個體 |
| **彈性** | 僅限於工作表/電子郵件 | 彈性十足，提供各種AEM Forms動作 |
| **範例** | 連絡表單資料至Google工作表 | 觸發AEM核准工作流程的貸款申請 |

## 如何在不同的網站或頁面中內嵌Forms

有時，您會想要顯示在不同網頁或網站上的單一位置（例如中央「表單網站」）建立及管理的表單。

### 為什麼要內嵌表單？

* 您有一個使用通用編輯器建立的標準「聯絡我們」表單，該表單需要顯示在使用檔案式撰寫建立的多個登入頁面上。
* 您的主要網站內容位於檔案製作(DA)中，且您需要包含特殊表單。
* 您想要在多個不同的EDS專案中重複使用單一、維護良好的表單。

### 表單內嵌在技術上如何運作

您要顯示表單的頁面（我們將其稱為「主機頁面」）將包含一些程式碼（通常是特殊區塊或指令碼）。 當使用者造訪主機頁面時，此程式碼會對託管實際表單的URL提出請求(將其稱為「表單Source」)。 表單Source接著會傳回其HTML，並由主機頁面進行插入和顯示。

**內嵌式表單架構**

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

![內嵌式表單架構](/help/forms/assets/eds-embedded-form.png)
此圖表顯示從表單Source擷取表單HTML並顯示該表單的「主機頁面」 。 提交使用原始表單已設定的端點。

## 為內嵌Forms設定CORS

[CORS （跨原始資源共用）](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)是瀏覽器安全功能。 如果您的主機頁面（例如`site-a.com`）嘗試從不同的網域（例如`forms-site-b.com`）擷取表單，則瀏覽器會封鎖它，除非`forms-site-b.com`明確允許透過CORS標頭擷取表單。

**表單Source伺服器**&#x200B;上若沒有正確的CORS標頭，瀏覽器會導致Host Page無法載入表單，且您的內嵌表單不會顯示。

### 如何在提供表單的網站上設定CORS？

您必須設定主控&#x200B;**表單Source**&#x200B;的伺服器，以在其回應中傳送特定的HTTP標頭。 確切的方法取決於您的EDS設定（例如，對於Franklin專案，這通常會在控制CDN行為或邊緣工作者邏輯的GitHub存放庫中的`helix-config.yaml`或類似的設定檔案中完成）。
要新增至Source表單回應的關鍵標頭：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` （例如`https://your-site.com`）。 若要進行測試，您可以使用`*`，但若要用於生產，請指定確切的網域。
* `Access-Control-Allow-Methods: GET, OPTIONS` (如果表單提交本身也是跨來源的，您可能會需要`POST`，但通常提交會移至個別的（通常是相同來源或特別設定的）端點)。
* `Access-Control-Allow-Headers: Content-Type` （以及您的表單擷取可能使用的任何其他自訂標頭）。

**範例（設定檔的概念性）：**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## 其他考量事項： CDN和多個程式碼基底(Helix 4)

* **CDN規則：**&#x200B;您的CDN可能會提供Proxy要求的方法。 例如，CDN可以在內部路由對`host-page.com/embedded-form`的請求，以從`form-source.com/actual-form`擷取內容，使其對瀏覽器而言似乎是相同來源。 設定可能會很複雜。
* **多個程式碼基底(Helix 4)：**&#x200B;如果您的主機頁面和表單Source位於不同的GitHub存放庫（在Helix 4設定中很常見），請確定主機頁面的程式碼基底中可以使用轉譯或管理表單所需的任何JavaScript「表單區塊」，或者從Source表單擷取的表單HTML是獨立的，並包含其所有必要的JavaScript。 原始檔案提到，對於「helix4具有不同程式碼基底，則您需要在兩個程式碼基底上新增Form區塊」。

### 一般架構設定與組態步驟

以下是您可以設定表單的一些常見方式，這些方式結合了撰寫方法與提交策略以及關鍵設定點。

#### 以檔案為基礎的表單，具有試算表/電子郵件提交

這是最簡單的設定。 您在Word/Google Docs中建立表單，然後透過Forms提交服務將資料提交至試算表或電子郵件。

1. 在Word/Google Doc/Sheet中使用指定的表格結構或表單區塊來定義您的表單。
1. 在檔案（或相關設定）中，指定Forms提交服務的目標試算表URL或電子郵件地址。
1. 請確定`forms@adobe.com` （或相關的服務帳戶）具有目標試算表的編輯存取權。
1. 將檔案發佈到您的Edge Delivery網站。

**Doc型+ Forms提交服務架構**
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

![Doc型+ Forms提交服務架構](/help/forms/assets/eds-doc-fss.png)

#### 具有試算表/電子郵件提交的通用編輯器表單

您使用視覺化通用編輯器建置表單，但還是使用簡易的Forms提交服務來擷取資料。

1. 使用AEM中的通用編輯器建立您的表單。
1. 在UE中設定表單的提交動作，以使用「提交至Forms提交服務」選項。
1. 指定目標試算表URL或電子郵件地址。
1. 如果使用試算表，請確定`forms@adobe.com`具有編輯存取權。
1. 從AEM將包含表單的頁面發佈到Edge Delivery網站。

   **通用編輯器+ Forms提交服務架構**

   ![通用編輯器+ Forms提交服務架構](/help/forms/assets/eds-ue-fss.png)

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

#### 具有AEM發佈提交的通用編輯器表單（進階）

此設定使用通用編輯器建立表單，並使用AEM Publish執行個體進行強大的後端處理（工作流程、FDM等）。 這需要更多設定。

1. **在UE中建立表單：**&#x200B;在通用編輯器中建置您的表單。 設定其提交動作以指向AEM Forms動作(例如「叫用AEM工作流程」、「使用表單資料模型提交」)。
1. **AEM Dispatcher設定(在您的AEM發佈層級)：**
   * **沒有重新導向：**&#x200B;請確定您的Dispatcher規則&#x200B;*不會*&#x200B;對`/adobe/forms/af/submit/...`個路徑提出的重新導向要求。
   * **允許提交：**&#x200B;修改您的Dispatcher篩選器（例如，在`filters.any`中），從您的Edge Delivery網站的網域或IP位址明確`allow`個POST要求給`/adobe/forms/af/submit/...`。
1. AEM中的&#x200B;**OSGi反向連結篩選器(在您的AEM發佈層級)：**
   * 在AEM OSGi主控台(`/system/console/configMgr`)中，尋找並設定「Apache Sling反向連結篩選器」。
   * 將您的Edge Delivery網站網域（例如`https://your-eds-domain.hlx.page`、`https://your-custom-eds-domain.com`）新增至「允許主機」或「允許主機RegExp」清單。 這會告訴AEM接受源自您EDS網站的提交內容。
1. **CDN重新導向規則(在您的Edge Delivery CDN上)：**
   * 您的Edge Delivery網站（例如`your-eds-domain.hlx.page`）需要正確將提交請求路由傳送到您的AEM發佈執行個體。
   * 當您EDS頁面上的表單提交時，它可能會定位相對路徑，例如`/adobe/forms/af/submit/...`。 您的Edge Delivery CDN （或Edge Worker）上需要一條規則，指出：「如果請求到`your-eds-domain.hlx.page/adobe/forms/af/submit/...`，請將其轉寄（Proxy或重新導向）至`your-aem-publish-instance.com/adobe/forms/af/submit/...`。」
   * 確切的實作取決於您的CDN提供者（例如Fastly VCL、Akamai屬性管理員、Cloudflare Workers）。
1. **（選用） `constants.js`用於開發（在您的EDS專案的程式碼基底中）：**
   * 若是本機開發，或您的使用者端表單指令碼需要知道完整的AEM發佈URL，您可以在Edge Delivery專案的GitHub存放庫中的`constants.js`或類似的設定檔案中設定此URL。 範例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **發佈：**&#x200B;將您的表單頁面從AEM發佈至EDS，並確定所有AEM設定在您的AEM發佈執行個體上皆為作用中。

   **Universal Editor + AEM發佈架構**

![Universal Editor + AEM發佈架構](/help/forms/assets/eds-aem-publish.png)

以下流程顯示：使用者在EDS網站上提交，經CDN路由傳送至AEM Dispatcher，然後AEM發佈加以處理。

#### 將表單內嵌至檔案製作(DA)頁面

您的主要網站內容是在檔案製作(DA)中建立。 您可以分別使用檔案式製作或通用編輯器來建立表單，然後將其內嵌至DA頁面。

1. **建立並發佈表單：**
   * 使用檔案式製作或通用編輯器來建立您的表單。
   * 根據設定1、2或3，設定其提交方法(向Forms提交服務或AEM Publish)。
   * 發佈此表單，讓表單在其自己的Edge Delivery URL上線（例如`.../forms/my-special-form`）。
1. **設定CORS：**&#x200B;在代管此獨立表單的Edge Delivery網站/專案上，請確定CORS標題已設定為允許檔案編寫網站的網域擷取它。
1. **在DA中製作頁面：**&#x200B;在檔案製作中建立或編輯您的頁面。
1. **內嵌表單區塊：**&#x200B;在DA中使用適當的區塊來內嵌外部URL。 將此區塊指向您獨立發佈表單的URL。
1. **發佈DA頁面：**&#x200B;發佈您的DA頁面。 現在會擷取並顯示表單。

   **內嵌於DA架構中的Forms**

   ![內嵌於DA架構中的Forms](/help/forms/assets/eds-forms-embedd-da.png)

   這會顯示從其他EDS位置提取表單的DA頁面。 內嵌表單會處理自己的提交。

## 疑難排解

* **我的表單提交無法運作。**
   * **檢查主控台錯誤：**&#x200B;開啟瀏覽器的開發人員主控台（通常是F12），並在您提交時在[網路]索引標籤或[主控台]索引標籤上尋找錯誤。
   * **驗證提交URL：**&#x200B;表單是否嘗試提交至正確的端點(Forms提交服務URL或您的AEM發佈路徑)？
   * **Forms提交服務：**&#x200B;如果傳送至試算表，`forms@adobe.com`是否獲得編輯存取權？ 試算表URL正確嗎？
   * **AEM發佈提交：**
      * 您的Dispatcher是否允許`/adobe/forms/af/submit/...`張貼內容？
      * AEM Publish上的Sling查閱者篩選器是否已設定為允許您的EDS網域？
      * 您針對`/adobe/forms/af/submit/...`的CDN重新導向規則是否正常運作？

* **我的內嵌表單未出現。**

   * **CORS！**&#x200B;這是最常見的原因。 檢查瀏覽器主控台是否有CORS錯誤。 確定主控網站&#x200B;*的*&#x200B;表單具有正確的`Access-Control-Allow-Origin`標頭。
   * **表單URL是否正確？**&#x200B;主機頁面上的內嵌程式碼是否指向表單的正確即時URL？
   * **JavaScript區塊：**&#x200B;如果表單仰賴特定的JavaScript「表單區塊」來轉譯，該區塊的程式碼是否可在主機頁面上使用？

* **提交至AEM Publish時，我收到「403禁止」或「401未獲授權」。**

   * 這通常指向AEM Publish上的Sling反向連結篩選器，不允許來自EDS網域的請求。 仔細檢查其設定。
   * 如果您的AEM提交端點要求的話（雖然標準表單提交通常是匿名的），這也可能是驗證/授權問題。

## 後續步驟

本指南提供搭配AEM Edge Delivery Services使用表單的概觀。 如需特定設定的詳細逐步指示，請參閱Adobe Experience Manager官方檔案：

* [使用Edge Delivery Services Forms進行檔案式製作](/help/edge/docs/forms/tutorial.md)
* [具有Edge Delivery Services Forms的通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [檔案製作(DA)與內嵌內容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)