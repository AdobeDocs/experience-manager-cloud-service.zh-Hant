---
title: 瞭解Adobe Experience Manager Formsas a Cloud Service的最新創新。
description: 「瞭解 [!DNL AEM Forms] as a Cloud Service建立、管理和發佈企業級表單和業務流程。」
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 重要 Adobe Experience Manager Forms 創新 {#latest-innovations}

Adobe Experience Manager Forms的一些最大創新包括：

| 創新 | 詳細資料 |
|---|---|
| 無頭自適應Forms | 建立和管理 [無頭自適應Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 在Adobe Experience Manager平台內。 使您的開發人員能夠建立、發佈和管理可通過API訪問和交互的互動式表單，而不是通過傳統的圖形用戶介面。 <br/> <br/> 這些表格設計為無需傳統的HTML表格介面即可提交。 換句話說，它們允許您通過API或後端代碼以寫程式方式提交表單資料，前端有任何可見表單元素，前端沒有任何可見表單元素。 <br/> ![](https://experienceleagueadobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)<br/> 無頭表單在各種情況下非常有用，例如在構建單頁應用程式、漸進式Web應用程式或移動應用程式時，傳統的HTML表單介面可能不是必需的或實用。 通過允許開發人員直接通過API或後端代碼提交表單資料，無頭表單有助於簡化工作流並提高Web應用程式的整體效能。 |
| 核心元件 | 的 [自適應Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開源、符合BEM規範的元件，它們構建在Adobe Experience ManagerWCM核心元件的基礎上。 它們專門設計用於建立適應性Forms，後者是適應用戶的設備、瀏覽器和螢幕大小的表單。 <br/> <br/> 這些元件可通過提供多種表單域選項（包括文本域、複選框、下拉菜單等）來建立卓越的資料捕獲和註冊體驗。 它們還包括驗證、條件邏輯和響應設計等功能，這些功能可用於建立方便用戶且易於使用的表單。 <br/> ![](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?)<br/>  此外，由於這些元件是開源的，因此開發人員能夠輕鬆定制和擴展元件以滿足其組織的特定需求。 並且，這些元件都建立在BEM方法上，確保它們具有可擴充性和可維護性。 |
| MicrosoftPowerAutomet連接器 | AEM FormsPower Automate Connector允許您將Adobe Experience Manager(AEM)Forms與MicrosoftPower Automate(以前稱為Microsoft流)整合。 Power Automate是一種基於雲的服務，允許您在不同應用程式和服務之間建立自動化的工作流。  <br/> <br/> 使AEM用Form Power Automate Connector，您可以建立根據提交自適應表單自動觸發的工作流。 例如，您可以建立一個工作流，當用戶提交表單時自動向特定人員發送電子郵件通知，或者當用戶完成表單時在Microsoft計畫器中建立任務。  <br/> ![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999) <br/> AEM Forms電源自動連接器是一種功能強大的工具，它使您能夠將自適應Forms與與Microsoft電源自動化連接的其他應用程式和服務進行自動化和整合，使您能夠使用範圍更廣的工具。 您可以建立根據您的特定需要定製的工作流，並能夠添加自定義操作、條件和觸發器。 此外，Power Automate還提供詳細的分析和報告功能，讓您能夠監控和優化工作流。 |
| Microsoft儲存介面 | AEM FormsMicrosoft儲存介面 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-sharedrive">OneDrive</a>。 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-sharedrive"> SharePoint, </a> 和 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-azure-blob-storage"> Azure Blob儲存 </a> 是連接器，可讓您將Adobe Experience Manager(AEM)Forms與MicrosoftOneDrive和SharePoint整合。 使用此連接器，您可以直接從Adaptive Forms將資料檔案和附件上載到OneDrive和SharePoint。 <br/> ![](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/>OneDrive和SharePoint公司可以與其他業務應用程式整合，如CRM系統，會計軟體和項目管理工具。 這使您能夠簡化業務流程、減少手動資料輸入並提高整體效率。 |
| 嚮導UI | 自適應Forms嚮導UI是一種功能強大的工具，可快速輕鬆地建立自適應表單。 其用戶友好的介面和定制選項使所有用戶都能夠訪問它，而不管其技術專業水準如何。 <br/> <br/> 嚮導UI通過引導用戶逐步完成表單建立過程來簡化建立自適應表單的過程。 嚮導 — UI分為多個頁籤，每個頁籤都清楚地提供了配置自適應表單的選項。 表單作者以線性方式在頁籤中進行，以選擇表單元件的選項，如模板、提交操作和資料源。 <br/> ![](/help/release-notes/assets/wizard.png) <br/>嚮導介面簡化了發現自適應表單所有基本選項的過程，並使表單建立更加容易，即使對不熟悉該技術的用戶也是如此。 |
| Adobe Analytics，為Forms安裝Experience Cloud  [!BADGE 即將推出]{type=Informative tooltip="Adobe Analytics,Experience CloudForms安裝自動化"} | 表單分析可以通過測量用戶參與、優化轉換率、監控表單效能和改進用戶體驗來提供對表單效能的寶貴洞見。  通過跟蹤用戶行為和反饋，分析可以確定表單中導致沮喪或混亂的區域，指導對表單的設計和功能的改進。 <br/> <br/> 使用「You enableAdobe Analytics withExperience Cloud設定自動化」(Enable Setup Automation)，只需翻動兩個按鈕。 它使您能夠將AEM Formsas a Cloud Service與Experience Platform標籤和Adobe Analytics連接起來，以捕獲和跟蹤已發佈表單的效能指標。 <br/> <br/> ![](/help/forms/assets/forms-analytics-report.png) <br/><br/> Formsas a Cloud Service提供Adobe Analytics報告OOTB 它幫助您輕鬆瞭解表單的效能。 表單級度量使您能夠深入瞭解表單在多個關鍵績效指標(KPI)（如格式副本、訪問者、提交、平均填充時間）上的表現。 <br/> <br/> 它還提供用戶訪問面板中各欄位的上下文幫助的平均次數的詳細資訊，以幫助您確定在提供資訊之前讓用戶停止並查找資訊的欄位。 您可以進一步簡化此類欄位或幫助內容改進轉換。 |
| 下一代可組合性 | 使用下一代組合性，您企業中的員工可以使用他們的首選工具(如MicrosoftExcel和Google工作表)建立表單，而無需對新的UI工作流進行廣泛培訓。 <br/> <br/> 此外，Next Gen Composibility設計為以無與倫比的速度載入表單，在即時頁面上獲得近乎完美的Google燈塔評分，保證最佳效能和用戶體驗。<br/> <br/> ![](/help/forms/assets/web-vitals.jpeg) 此外，由於Next Gen Composability提供的直接工具，部署表格從來都不是簡單或快捷。 只需最少的開發時間，您就可以輕鬆地簡化實現生命的路徑，並為客戶提供卓越的表單體驗。 |
