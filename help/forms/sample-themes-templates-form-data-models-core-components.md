---
title: 核心元件中的範例主題、範本和表單資料模型
description: AEM Forms核心元件提供範例最適化表單主題、範本和表單資料模型
solution: Experience Manager Forms
topic: Administration
role: Admin, User
hide: true
hidefromtoc: true
level: Intermediate
source-git-commit: 2b290be134be05bc15891082e8b54efef62076d0
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 3%

---


# 核心元件中的範例主題、範本和表單資料模型 {#sample-themes-templates-and-data-models}

[!DNL AEM Forms] 核心元件提供立即可用的範例主題、範本和表單資料模型，以便快速建立多樣化的調適型表單。 這也有助於讓作者瞭解的擴充性、適應性和回應能力 [AEM Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 能夠快速建立簡易的表單，並輕鬆建立複雜的表單，同時與資料庫緊密連線。

參考內容套件中包含的範例主題、範本和表單資料模型包括：

| 範本 | 主題 | 表單資料模型 |
---------|----------|---------
| 基本 | 畫布 | Microsoft® Dynamics 365 |
| 空白 | WKND | Salesforce |
| 聯絡我們 | 畫架 |  |
| 聯絡詳細資料更新 |   |   |
| 同意表單 | |  |
| 記錄服務要求 |  |  |
| 提供意見回饋 |  |  |
| 福利註冊 |  |   |
| 員工福利彙總 |   |   |
| 要求帳戶對帳單 |   |   |
| 安全檢查表 |   |   |
| 品質控制檢查 |   |   |
| 購買要求 |  |  |

## 範例主題 {#Sample-Themes}

參考範例主題可協助作者定義及自訂表單的樣式，即使具備CSS基本知識的作者也可以視需要自訂主題。

**如何取得這些主題？**
* 若要開啟這些主題 **Formsas a Cloud Service** 環境， [啟用最適化Forms核心元件](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) 並使用 [前端管道](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) 以部署這些主題。
* 若要將這些主題放在 **AEM 6.5 Forms** 環境， [啟用最適化Forms核心元件](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) 並使用 [封裝管理員](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components) 以部署這些主題。

此 **立即可用** [最適化表單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 主題說明如下：

![OOTB主題](assets/OOTB-themes.png)

### 畫布 {#Canvas}

畫布布主題是表單的預設主題，並強調使用基本顏色、透明度與平面圖示。 在下方熒幕擷圖中，您可以看到畫布布佈景主題的外觀。

![畫布主題](assets/Safety-Inspection-Theme-Canvas.png)

### WKND {#WKND}

WKND主題包含生動、富有想象力且吸引人的設計，以展現您表單的時尚外觀。 主題是根據 [WKND網站](https://wknd.site/us/en.html) 這是一個旅遊和冒險網站，建立在 [Adobe Experience Manager核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html).

![WKND主題](assets/Safety-Inspection-Form-Theme.png)


### 畫架 {#Easel}

畫框主題有助於建立吸引人且易於設定的表單外觀，而且會經過客製化，以簡化操作且方便使用。 畫架主題是以一個可攜式支架的概念為基礎，藝術家在創作畫作時可使用此支架來支援畫布。

![畫框主題](assets/Safety-Inspection-Theme-Easel.png)

## 範例範本 {#Sample-templates}

範本會定義要在您的表單中復寫的初始表單結構、內容和動作，或是使用與您的表單類似的範本結構，例如，同意表單、權益登錄檔單等等。

**如何取得這些範本？**
您可以部署 [以AEM Archetype 43或更新版本為基礎的專案](https://github.com/adobe/aem-project-archetype) 至您的 **AEM Formsas a Cloud Service** 或 **AEM 6.5** Forms環境。

此 **立即可用** [最適化表單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 範本的說明如下：

![參考範本](assets/reference-templates-core-components.png)

### 基本 {#Basic}

基本範本可幫助您快速建立註冊體驗表單。 您也可以用它來預覽功能 [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction). 它提供精靈版面配置，用於逐節呈現資料。

![基本範本](assets/Basic-template-desktop-view.png)

### 空白 {#Blank}

空白畫布範本可用來從頭開始建立最適化表單結構、內容和規則。 空白範本中未預先納入任何表單元件。

![空白範本](assets/Blank-temp-desktop-view.png)

### 聯絡我們 {#Contact-Us}

聯絡我們表單範本是用來建立表單，以促進網站訪客與表單管理員之間的通訊。 使用者可以透過表單提交查詢、意見回饋或支援請求。

![聯絡我們範本](assets/Contact-us-desktop-view.png)

### 連絡人詳細資料更新 {#Contact-Details-Update}

聯絡資料詳細資料更新範本可協助作者建立客戶地址和聯絡資料更新的表單。 此表單也可協助客戶更新與訂閱或權益相關的個人資訊，以確保順暢的通訊以及不間斷地存取服務或權益。

![Contact-details-update](assets/Contact-details-update.png)

### 同意表單 {#Consent-Form}

同意表單範本可用來建立表單，以從參與特定活動、研究研究、醫療程式或可能涉及其個人資訊或權利的任何情況的參與者取得法律檔案。 表單可確保透明度、保護參與者的權利，並清楚瞭解個人同意的內容。

![同意表單](assets/Consent-form-desktop-view.png)

### 記錄服務要求 {#Log-Service-Request}

記錄服務要求範本可協助建立向服務提供者要求記錄特定記錄服務的表單。 表單可作為正式請求，針對記錄以監控或追蹤狀態的事件、活動或資料建立票證。

![記錄服務請求範本](assets/Log-service-request-desktop-view.png)


### 提供意見回饋 {#Give-Feedback}

提供意見回饋表單範本有助於建立表格，向其他人員或團隊提供具建設性的意見回饋。 此表單有助於確保意見反應清晰、明確且可行，可促進開放式溝通和改進。

![提供意見反應範本](assets/Give-feedback-desktop-view.png)


### 福利註冊 {#Benefits-Enrollment}

福利登錄檔單範本可用來建立表單，以收集員工有關其偏好福利與保險選項的基本資訊。 它通常伴隨年度福利註冊期間。

![福利註冊範本](assets/Benefits-enrollment-form-template.png)


### 員工福利彙總 {#Employee-Benefits-Summary}

員工福利摘要表單範本可用來建立表單，以收集有關個人福利的基本詳細資訊。 它有助於快速準確地評估涵蓋範圍，提供有效協助和支援的完整概觀。
![員工福利彙總](assets/Employee-benefits-summary.png)


### 要求帳戶對帳單 {#Request-for-Account-Statement}

Request for account statement template可協助建立表單，以啟動取得準確且最新之客戶對帳單的程式。 對帳單提供財務交易、活動的詳細記錄，或使用此表單之客戶的其他相關資訊。

![帳戶請求宣告](assets/Request-for-account-statment.png)

### 安全檢查 {#Safety-Inspection}

安全檢查表單範本可協助建立表單，以輸入安全工作環境的詳細資訊。 使用此表格進行定期檢查，即可識別潛在危險。 此表格涵蓋各種層面，例如緊急出口、防火安全、電氣安全、危險材料、個人防護裝置、工作站人體工學，以保障員工、訪客和客戶的安全與福祉。

![安全檢查表單](assets/Safety-inspection-form.png)

### 品質控制檢查 {#Quality-Control-Inspection}

品質控制檢查表單範本可用來建立表單，以評估和記錄產品或專案的視覺外觀、尺寸、功能、檔案、測試結果以及整體品質。 它有助於識別缺陷、不符合項以及確保符合品質標準所需的更正動作。

![品質控制檢查](assets/Quality-Control-Inspection.png)


### 購買要求 {#Purchase-Request}

採購請求表單範本可協助建立表單，以啟動採購程式，並允許員工正式要求購買其工作所需的商品或服務。 此表單會擷取必要的明細，例如料號摘要、數量、偏好的供應商（如果適用）、預算配置、採購理由、交貨資訊以及必要的核准。

![purchase-request-form](assets/Purchase-request-form.png)

## 參考表單資料模型 {#reference-models}

在您建立 [最適化表單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#adaptive-forms-core-components) 根據 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction#adaptive-forms-core-components)，您可以將表單與資料庫Microsoft®Dynamics 365和Salesforce伺服器連線，以啟用業務工作流程。 例如：

* 在Microsoft® Dynamics 365和Salesforce中寫入資料於最適化表單提交時。
* 透過「表單資料模型」中定義的自訂實體在Microsoft®Dynamics 365和Salesforce中寫入資料，反之亦然。
* 查詢Microsoft®Dynamics 365和Salesforce伺服器以取得資料，並預先填入Adaptive Forms。
* 從Microsoft® Dynamics 365和Salesforce伺服器讀取資料。

您可以透過安裝以下表單資料模型 [參考內容封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* Microsoft® Dynamics 365
* Salesforce

如需使用這些模型的詳細資訊，請參閱 [設定Microsoft® Dynamics 365和Salesforce雲端服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html#configure-dynamics-cloud-service)
