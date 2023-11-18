---
title: Adobe Experience Manager Formsas a Cloud Service有哪些最新創新？
description: 探索的最新功能 [!DNL AEM Forms] as a Cloud Service建立、管理和發佈企業級表單與業務流程。
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 5%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 重要 Adobe Experience Manager Forms 創新 {#latest-innovations}

Adobe Experience Manager Forms中的一些熱門創新包括：

| 創新 | 詳細資料 |
|---|---|
| Headless最適化Forms | 建立和管理 [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 在Adobe Experience Manager平台內。 讓您的開發人員建立、發佈和管理互動式表單，這些表單可透過API （而非透過傳統的圖形使用者介面）存取和互動。 <br/> <br/> 這些表單的提交方式完全不需要傳統的HTML表單介面。 換言之，它們可讓您透過API或後端程式碼以程式設計方式提交表單資料，且前端沒有任何可見的表單元素。 <br/> <!-- ![Headless adaptive form working](https://experienceleagueadobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?) --><br/> Headless表單可用於各種情況，例如建置單頁應用程式、漸進式網頁應用程式或行動應用程式時，在這些情況下傳統HTML表單介面可能不是必要或不實用。 Headless表單可讓開發人員直接透過API或後端程式碼提交表單資料，有助於簡化工作流程，並改善網頁應用程式的整體效能。 |
| 核心元件 | 此 [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開放原始碼、符合BEM規範的元件，建立在Adobe Experience Manager WCM核心元件的基礎上。 這些表單是專為建立最適化Forms所設計，是適合使用者裝置、瀏覽器和熒幕大小的表單。 <br/> <br/> 這些元件可用來建立優異的資料擷取和註冊體驗，方法是提供各式各樣的表單欄位選項，包括文字欄位、核取方塊、下拉式功能表等。 此外也包含驗證、條件式邏輯和回應式設計等功能，可用來建立簡單易用的表單。 <br/> ![核心元件的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?)<br/>  此外，由於這些元件是開放原始碼，開發人員可輕鬆自訂和擴充元件，以符合其組織的特定需求。 此外，這些元件建置於BEM方法上，可確保它們具有可擴充性和可維護性。 |
| Microsoft PowerAutomate聯結器 | AEM Forms Power Automate聯結器可讓您整合Adobe Experience Manager (AEM) Forms與Microsoft Power Automate (先前稱為Microsoft流量)。 Power Automate是雲端型服務，可讓您在不同應用程式和服務之間建立自動化工作流程。  <br/> <br/> 使用AEM Form Power Automate聯結器，您可以建立根據提交最適化表單自動觸發的工作流程。 例如，您可以建立工作流程，在使用者提交表單時自動傳送電子郵件通知給特定人員，或在使用者完成表單時在Microsoft Planner中建立任務。  <br/> ![microsoft PowerAutomate聯結器圖示](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999) <br/> AEM Forms Power Automate聯結器是一款功能強大的工具，可讓您將最適化Forms與其他與Microsoft Power Automate連線的應用程式和服務自動化及整合，讓您使用更廣泛的工具。 您可以建立符合您特定需求的工作流程，並有能力新增自訂動作、條件和觸發器。 此外，Power Automate提供詳細的分析和報告，可讓您隨著時間監視和最佳化工作流程。 |
| Microsoft儲存聯結器 | 適用於的AEM Forms Microsoft儲存聯結器 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-sharedrive">OneDrive</a>， <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-sharedrive"> SharePoint， </a> 和 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-azure-blob-storage"> Azure Blob儲存體 </a> 是聯結器，可讓您將Adobe Experience Manager (AEM) Forms與Microsoft OneDrive和SharePoint整合。 有了此聯結器，您可以直接從Adaptive Forms將資料檔案和附件上傳至OneDrive和SharePoint。 <br/> ![microsoft onedrive和sharepoint圖示](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/>OneDrive和SharePoint可以與其他業務應用程式整合，例如CRM系統、會計軟體和專案管理工具。 這可讓您簡化業務流程、減少手動資料輸入，並改善整體效率。 |
| 精靈UI | 最適化Forms精靈UI是快速輕鬆建立最適化表單的強大工具。 其簡單易用的介面和自訂選項可讓所有使用者存取，無論其技術專業水準為何。 <br/> <br/> 精靈UI透過引導使用者逐步完成表單建立流程，簡化了建立最適化表單的程式。 精靈UI分為多個索引標籤，每個索引標籤清楚提供設定調適型表單的選項。 表單作者會以線性方式逐一瀏覽標籤，以選取範本、提交動作和表單元件的資料來源等選項。 <br/> ![表單建立精靈的影像](/help/release-notes/assets/wizard.png) <br/>精靈介面可簡化探索最適化表單所有基本選項的流程，並使表單建立作業更容易，即使是不熟悉此技術的使用者也能做到。 |
| Adobe Analytics與Forms的Experience Cloud設定自動化 | 表單分析可透過測量使用者參與度、最佳化轉換率、監控表單效能和改善使用者體驗，提供表單效能的寶貴見解。  透過追蹤使用者行為和意見回饋，分析可以識別表單中導致挫折或混淆的區域，以指導表單設計和功能的改進。 <br/> <br/> 透過使用，您可以 [使用Experience Cloud設定自動化啟用Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html) 輕輕翻動幾個按鈕。 它可讓您連結AEM Formsas a Cloud Service與Experience Platform標籤和Adobe Analytics，以擷取及追蹤您已發佈表單的效能度量。 <br/> <br/> ![最適化表單使用者參與adobe analytics報告](/help/forms/assets/forms-analytics-report.png) <br/><br/> Formsas a Cloud Service提供Adobe Analytics報表OOTB。 這可幫助您輕鬆了解表單的效能。表單層級的量度可讓您深入了解表單在多個關鍵效能指標 (KPI) 上的表現，例如呈現、訪客、提交、平均填寫時間。<br/> <br/> 它也提供使用者存取面板中欄位內容說明的平均次數詳細資訊，以協助您確定在提供資訊之前讓使用者停止並搜尋資訊的欄位。 您可以進一步簡化這類欄位，或協助內容改善轉換。 |
| Edge傳遞 | 有了Edge Delivery，企業的員工都可以在他們偏好的工具(例如Microsoft Excel和Google Sheets)中建立表單，而不需要有關新UI工作流程的廣泛培訓。 <br/> <br/> 此外，Edge Delivery是以無與倫比的速度載入表單，在即時頁面上獲得近乎完美的Google Lighthouse分數，確保最佳效能和使用者體驗。<br/> <br/> ![建立表單的新一代可組合性工具](/help/forms/assets/web-vitals.jpeg) 此外，由於Edge Delivery提供的簡單工具，部署表單變得前所未有的輕鬆或快速。 只需最少的開發時間，您就可以輕鬆簡化上線的路徑，並為客戶提供卓越的表單體驗。 |
