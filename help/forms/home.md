---
title: 簡介 [!DNL AEM Forms] as a Cloud Service
description: 探索 AEM Forms 並了解此表單如何幫助您製作業務適用的文件和表單內容。 了解關於 Platform-as-a-Service (PaaS)，以及如何管理企業級數位表單和業務流程，以及連接表單至現有的資料來源。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表單。
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 2f9c4d85c55ee63a769c0137d4a70b2126228d5b
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 5%

---

# 簡介 {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] 提供雲端原生的Platform as a Service(PaaS)解決方案，供企業建立、管理、發佈和更新複雜的數位表單，同時將提交的資料與後端流程、業務規則整合，並將資料儲存在外部資料存放區。 此服務始終是最新的，始終可用，並且始終學習。

您可以使用服務來建立和推出互動式及吸引人的數位表單。 例如，以想要將客戶註冊歷程數位化的組織為例。 他們有多個資料來源和現有客戶資料。 他們希望預先填入表單、新增表單的電子簽名，並將填入的表單封存為PDF檔案。 此外，該組織有多種列印表單(PDF forms)，他們也希望將所有列印表單轉換為數位表單。



組織可使用 [!DNL AEM Forms] as a Cloud Service於建立數位表單，將表單連結至現有的資料來源，將表單與 [!DNL Adobe Sign] 向表單添加電子簽名，並生成記錄文檔(DoR)以將提交的表單存檔為PDF檔案。 組織也可以使用服務將其現有PDF forms轉換為數位表單。

組織可使用 [!DNL AEM Forms] as a Cloud Service，無需任何本地基礎架構，即可在雲中獲取所有這些功能。 此服務還使組織從複雜的升級週期中解脫出來，因為它始終具有最新的功能。

## 重要功能 {#key-features}

<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] -->

| 調適型表單 | 通訊 API | automated forms conversion服務 | Forms Workflow | 電子簽名 | Forms Analytics | 資料模型 |
|---|---|---|---|---|---| ---|
| 為您的網站、應用程式及其他數位和列印管道，建立並管理互動式、動態、回應式、行動裝置易用且資料導向的表單。 | 按需或按計畫的間隔自動建立、管理和提供個人化、資料驅動的通信。 | 將舊式PDF型表單轉換為可輕鬆線上管理及分發的最適化Forms。 | 自動化涉及表單和文檔服務的業務流程。 當表單和文檔在業務流程的不同階段中移動時分配、傳送、審核和批准。 | 與Adobe Sign和DocuSign整合，以輕鬆傳送Forms和檔案給使用者，以供電子簽名使用。 | 使用Adobe Analytics獲得使用者行為和偏好的寶貴分析。 | 輕鬆將表單和檔案與外部資料來源連結，以便擷取和傳送資料。 |

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## 最新創新 {#latest-innovations}

>[!BEGINTABS]

>[!TAB 無頭式適用性&#x200B; Forms]

|| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?lang=en)|建立和管理 [無頭網路表單](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 在Adobe Experience Manager平台中。 讓您的開發人員可建立、發佈及管理互動式表單，這些表單可透過API存取和互動，而非透過傳統的圖形使用者介面。 <br/> <br/> 這些表單設計為可提交，無需傳統的HTML表單介面。 換言之，它們可讓您透過API或後端程式碼，以程式設計方式提交表單資料，而不要求前端有任何可見的表單元素。 <br/> <br/> 無頭表單在多種情況下都很有用，例如在建立單頁應用程式、漸進式網頁應用程式或行動應用程式時，傳統的HTML表單介面可能不是必需的或實用。 無頭式表單可讓開發人員直接透過API或後端程式碼提交表單資料，有助於簡化工作流程並改善網頁應用程式的整體效能。|




>[!TAB 核心元件]

|| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?lang=en) | [適用性Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開放原始碼、符合BEM規範的元件，建置於Adobe Experience Manager WCM核心元件之上。 這些表單經過專門設計，可用來建立最適化Forms，這些表單可適應使用者的裝置、瀏覽器和螢幕大小。 <br/> <br/> 這些元件可用於通過提供多種表單欄位選項（包括文本欄位、複選框、下拉菜單等）來建立卓越的資料捕獲和註冊體驗。 這些功能也包含驗證、條件式邏輯和回應式設計等功能，可用來建立方便使用且易於使用的表單。 <br/> <br/>  此外，由於這些元件是開放原始碼，開發人員可輕鬆自訂和擴充元件，以符合其組織的特定需求。 此外，這些元件均以BEM方法為基礎，可確保可擴充且可維護。|



>[!TAB Microsoft PowerAutomate Connector &#x200B;]

|| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector可讓您將Adobe Experience Manager(AEM)Forms與Microsoft Power Automate(先前稱為Microsoft Flow)整合。 Power Automate是一項基於雲的服務，允許您在不同應用程式和服務之間建立自動化的工作流。  <br/> <br/> 透過AEM Form Power Automate Connector，您可以建立根據提交適用性表單自動觸發的工作流程。 例如，您可以建立一個工作流，在用戶提交表單時自動向特定人員發送電子郵件通知，或在用戶完成表單時在Microsoft Planner中建立任務。  <br/> <br/> AEM Forms Power Automate Connector是一款功能強大的工具，可讓您將Adaptive Forms與與Microsoft Power Automate連接的其他應用程式和服務自動化並整合起來，讓您能夠使用更廣泛的工具。 您可以根據您的特定需求建立量身打造的工作流程，並新增自訂動作、條件和觸發器。 此外，Power Automate還提供詳細的分析和報告功能，允許您監視和優化隨時間變化的工作流。|


>[!TAB Microsoft Storage Connectors:OneDrive和Sharepoint]

|| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|AEM Forms Microsoft OneDrive和SharePoint的儲存連接器可讓您將Adobe Experience Manager(AEM)Forms與Microsoft OneDrive和SharePoint整合。 這些連接器可讓您在Microsoft的雲端儲存解決方案中儲存和管理AEM Forms資料和檔案。 <br/> <br/> 這些連接器可讓您在Microsoft OneDrive中儲存和管理AEM Forms資料和文檔。 使用此連接器，您可以直接從AEM Forms將資料檔案和附件上傳至OneDrive和SharePoint。 <br/> <br/> 將AEM Forms Microsoft Storage Connectors用於OneDrive和SharePoint有以下幾個優點： <ul><li> **整合**:這些連接器可讓您將AEM Forms與Microsoft的雲端儲存解決方案整合，讓您善用這些平台的強大功能。 </li> <li> **協作**:OneDrive和SharePoint是協作平台，使團隊成員能夠在檔案和文檔上協同工作。 將AEM Forms與這些平台整合後，您就能改善協作與團隊合作。 </li> <li> **安全性**:OneDrive和SharePoint提供強大的安全功能，確保資料和文檔的儲存和訪問是安全的。 </li> <br/> 總體而言，適用於OneDrive和SharePoint的AEM Forms Microsoft Storage Connectors是功能強大的工具，使您能夠在Microsoft基於雲的儲存解決方案中儲存和管理AEM Forms資料和文檔，從而改進協作和安全性。|


>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->