---
title: ' [!DNL AEM Forms] as a Cloud Service 簡介'
description: 探索 AEM Forms 以便產生業務可用表單、建立業務流程的工作流程，以及使用文件服務來產生和保護文件。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表單。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 100%

---


# AEM Forms as a Cloud Service 簡介 {#introduction}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html) |
| AEM as a Cloud Service  | 本文章 |


Adobe [!DNL Experience Manager Forms as a Cloud Service] 為企業提供了雲端原生的平台即服務 (PaaS) 解決方案，用於建立、管理、發佈和更新複雜的數位表單，同時將提交的資料與後端流程、業務規則相整合並將資料儲存在資料存放區中。

該服務始終是最新的，始終可用，並且始終都在學習。最佳化可以使用 [!DNL AEM Forms] as a Cloud Service，並在需端獲得所有這些功能，而無需任何本機基礎架構。該服務也可使組織擺脫複雜的升級週期，因為它始終與最新功能同步。

Adobe [!DNL Experience Manager Forms as a Cloud Service] 是一個以客戶為中心的解決方案，支援客戶歷程的每一步：

## 數位化和簡化註冊和上線體驗

您可以使用該服務來建立和推出互動式和吸引人的數位表單。例如，以一個希望將其客戶註冊流程數位化的組織為例。他們擁有多個包含現有客戶資料的資料來源。他們正在尋求預先填入表單、新增電子簽名表單以及將填寫的表單封存為 PDF 檔案。此外，該組織擁有多種列印表單 (PDF 表單)，他們還希望將列印表單轉換為數位表單。

組織可以使用 [!DNL AEM Forms] as a Cloud Service 來建立數位表單、將表單連結到現有的資料來源、將表單與 [!DNL Adobe Sign] 整合以在表單中新增電子簽名並產生記錄文件 (DoR) 以將提交的表單封存為 PDF 檔案。組織也可以使用此服務將其現有的 PDF 表格轉換為數位表格。

在大型企業中，表單通常是建立一次並透過複製到內容管理系統來重複使用。維持大型表單資料庫的更新，且讓這些表單易於被發現可能是一項相當大的挑戰。AEM 提供可自訂的表單入口網站，確保客戶可透過 Web 和行動管道找到並存取他們需要的表單。您可以自訂表單入口網站的外觀、品牌和徽標，以滿足您組織的特定要求。

## 提供個人化的通訊

高效率自助服務數位體驗的一個重要組成元件是及時通訊，使用者可以從任何地方在任何裝置上存取個人化的資訊。個人化和及時的通訊可以提高轉換率和使用者滿意度。

使用 AEM Forms，商業使用者可以透過自訂文件範本，並將後端流程中的資訊整合到範本中來建立引人注目的個人化使用者體驗。一組具直覺性的 API 可幫助企業設定規則，這些規則決定何時根據查詢或批量的定期輪詢來產生通訊。


可以輕鬆產生個人化文件，例如收據、歡迎套組和報表。組織可以將流量吸引到個人化的 Web 入口網站，進而讓使用者註冊或購買額外的服務。


## 自動化後台工作流程

使用以表單為中心的工作流程，來自動處理表單資料並將其發送給不同的利益相關者 (例如經理或部門)，以供審查、核准或進一步處理。這些工作流程可透過確保表單資料的一致性和可稽核處理方式、自動執行手動任務、提供以角色為主的存取控制以及幫助遵守法規要求，幫助您的組織大幅降低風險並保持合規性。


## 最佳化表單效能

該服務會和 Adobe Analytics 整合，讓您可擷取和追蹤已發佈表單的效能量度。分析這些指標背後的目標是根據有關使表單或文件更有用所需的變更資料做出明智的決策。您可以使用 Adobe Analytics 來發掘使用者在使用最適化表單時遇到的交互模式和問題。


## 開始 {#key-features}

|  |  |
|---|---|
| 最適化表單 | 為您的網站、應用程式和其他數位與列印管道建立和管理互動式、動態、回應式、行動友善和資料驅動的表單。查看以下內容以展開、了解和實作註冊體驗： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html">建立最適化表單</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">建立最適化表單樣式</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> 將資料提交到資料儲存或工作流程</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> 建立表格記錄以供長期封存</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=zh-Hant">新增最適化表單至 AEM Sites 頁面</a></li></ul> |
| 通訊 API | 使用 RESTful API 按需求或按預定時間間隔 (如月度報表和帳戶通知) 自動建立、管理和傳遞個人化、資料驅動的通訊。查看以下內容並展開、了解和建立： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> 產生個人化通訊 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> 組合或分解 PDF 文件</a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">建立符合 PDF/A 標準的文件 </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html">使用 DocAssurance API 保護您的文件</a></li></ul> |
| 自動化表單轉換服務 | 將舊版 PDF 型表單轉換為可輕鬆上線管理和分發的最適化表單。查看以下內容以開始： <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">設定自動表單轉換服務</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html">將 PDF 表單轉換為最適化表單</a></li></ul> |
| Forms - 工作流程 | 自動化涉及表單和文件服務的業務流程。在業務流程的不同階段移動時分配、傳送、審查和核准表單和文件。查看以下內容以開始：  <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">發送表單或文件以供審核</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">建立核准拒絕工作流程</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">將記錄文件</a>或<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step">電子簽名</a>步驟加入商業工作流程</a></li></ul> |
| 電子簽名 | 與 Adobe Sign 和 Adobe Sign Solutions for Government 整合，輕鬆向使用者發送表單和文件以進行電子簽名： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">使用 Adobe Sign 在最適化表單上進行電子簽名</a></li><li></a> <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=zh-Hant#sign-document-step">使用 Adobe Sign 和 AEM 工作流程對文件進行電子簽名</a></li></ul> |
| Forms Analytics | 使用 Adobe Analytics 獲取有關使用者行為和偏好的寶貴見解： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html">使用 Adobe Analytics 連結最適化表單</a></li></ul> |
| 資料來源 | 輕鬆地將您的表單和文件與外部資料源連接起來，以檢索和發送資料： <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=zh-Hant">連接到 RDBMS 或 Rest 端點</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=zh-Hant">連接到 Microsoft® Dynamics 365 或 Salesforce 雲端服務</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=zh-Hant">連接至 Microsoft® Azure Blob 儲存體</a></li></ul> |


>[!MORELIKETHIS]
>
>* [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
>* [Cloud Service 環境上線](/help/forms/setup-forms-cloud-service.md)
>* [設定本機開發環境](/help/forms/setup-local-development-environment.md)
>* [從 AEM 6.5 Forms 移轉到 Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)

