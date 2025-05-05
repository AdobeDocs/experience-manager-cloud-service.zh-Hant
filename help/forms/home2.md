---
title: ' [!DNL AEM Forms] as a Cloud Service 簡介'
description: 探索 AEM Forms 以便產生業務可用表單、建立業務流程的工作流程，以及使用文件服務來產生和保護文件。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表單。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 4b4bc6f754c6336136d409cf49617c7fafd4f4c3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 11%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>在尋找其他版本的說明檔案嗎？</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html?lang=zh-Hant">AEM 6.5 Forms檔案</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong> （目前）</li>
  </ul>
</div>

## 什麼是AEM Forms as a Cloud Service？

AEM Forms as a Cloud Service是Adobe的雲端原生解決方案，用於建立、管理和提供數位表單和通訊。 它可讓組織在整個客戶歷程中，將複雜的交易轉換為簡單的數位體驗。 您可以使用該服務來：

* 數位化和簡化註冊和上線體驗
* 提供個人化的通訊
* 自動化後台工作流程
* 將表單和通訊體驗與資料來源整合
* 追蹤及最佳化表單效能

該服務始終是最新的，始終可用，並且始終都在學習。最佳化可以使用 [!DNL AEM Forms] as a Cloud Service，並在需端獲得所有這些功能，而無需任何本機基礎架構。該服務也可使組織擺脫複雜的升級週期，因為它始終與最新功能同步。

Adobe [!DNL Experience Manager Forms as a Cloud Service] 是一個以客戶為中心的解決方案，支援客戶歷程的每一步：

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>調適型表單</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>建立因應使用者輸入和裝置型別的回應式動態表單：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">建立最適化Forms</a> — 建立可自動調整不同熒幕大小和使用者輸入的表單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type">豐富元件庫</a> — 使用各種輸入欄位和UI元件</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components">樣式最適化Forms</a> — 將一致的品牌和視覺設計套用至您的表單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">使用預先建立的主題和範本</a> — 透過現成的元件加速開發</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components">表單驗證</a> — 實作使用者端和伺服器端驗證規則</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components">提交動作</a> — 設定使用者提交表單時會發生什麼情況</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components">記錄檔案</a> — 建立已提交表單資料的永久記錄</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">將Forms新增至AEM Sites頁面</a> — 將表單無縫整合至您的網站</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page">將Forms新增至協力廠商網站頁面</a> — 順暢地將表單整合至您的網站</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>通訊API</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>以程式設計方式產生、操控及保護檔案：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation">產生個人化通訊</a> — 根據範本和資料建立自訂檔案</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">組合與操控PDF</a> — 組合、分割與修改PDF檔案</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">建立PDF/A檔案</a> — 產生封存品質檔案</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis">套用簽章</a> — 含有簽章的安全檔案</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">加密和解密PDF</a> — 保護敏感檔案內容</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">將XDP轉換為PostScript</a> — 將XDP檔案轉換為PostScript格式</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">將XDP轉換為PCL</a> — 將XDP檔案轉換為印表機命令語言</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">將XDP轉換為ZPL</a> — 將XDP檔案轉換為Zebra列印語言</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">將PDF轉換為PDF/A標準</a> — 建立符合封存要求的PDF檔案</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards">新增數位簽章</a> — 以數位簽署檔案以進行驗證</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>適用於Forms的Edge Delivery Services</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>使用Edge Delivery Services建立及傳遞表單：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Edge Delivery Forms總覽</a> — 瞭解使用Edge Delivery Services的表單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">適用於Forms的通用編輯器</a> — 使用WYSIWYG通用編輯器建立表單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial">檔案式製作</a> — 使用Microsoft Word或Google Docs建立表單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">樣式Edge Delivery Forms</a> — 套用自訂樣式至您的表單</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Headless Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>跨任何管道或前端框架提供表單體驗：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-headless-adaptive-forms/using/overview">無頭式Forms簡介</a> — 瞭解Headless的表單處理方式</li>
        <li>使用React或其他前端框架建置表單</li>
        <li>將表單整合至行動應用程式、網站和聊天應用程式</li>
        <li>透過表單功能善用您現有的UI元件</li>
        <li>保持後端表單邏輯，同時具備前端彈性</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>工作流程自動化</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>自動化涉及表單和檔案的業務流程：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step">建立業務流程</a> — 傳送表單以供核准或回饋、提交後工作流程或後端工作流程來管理註冊流程</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">在AEM工作流程中使用Adobe Sign</a> — 傳送要簽署的檔案 </li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">產生記錄檔案</a> — 隨選產生或表單提交</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>電子簽名</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>在您的表格和檔案中新增合法的電子簽章：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Adobe Sign整合</a> — 啟用最適化Forms中的電子簽章</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">將電子簽章新增至工作流程</a> — 在業務流程中包含簽章步驟</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">簽章的記錄檔案</a> — 產生表單提交的已簽署記錄</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Analytics與Insights</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>深入瞭解表單使用情形和效能：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">啟用Adobe Analytics</a> — 追蹤表單使用情況和效能</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics">手動Analytics整合</a> — 設定分析以進行詳細追蹤</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports">檢視Analytics報表</a> — 分析表單效能和使用者行為</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>資料整合</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>將表單連線至您現有的資料來源和系統：</p>
      <h4>Adobe生態系統</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> — 透過Adobe Sign傳送電子簽章</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a> — 整合表單與Adobe Marketo Engage</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">AEM工作流程</a> — 透過表單提交觸發AEM工作流程</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> — 提交最適化表單至Adobe Workfront Fusion</li>
      </ul>
      <h4>Microsoft整合</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> — 與Microsoft的CRM整合</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Azure Blob儲存體</a> — 將表單資料儲存在Microsoft的雲端儲存空間</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">SharePoint檔案庫</a> — 連線至Microsoft SharePoint檔案庫</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">SharePoint清單</a> — 連線至Microsoft SharePoint清單</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a> — 連線至Microsoft OneDrive</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a> — 觸發Microsoft Power Automate流程</li>
      </ul>
      <h4>其他資料來源與服務</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> — 與Salesforce CRM整合</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">RESTful Services</a> — 連線至任何REST API端點</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">RDBMS資料庫</a> — 連線到關聯式資料庫</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email">電子郵件</a> — 透過電子郵件傳送表單資料</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Forms入口網站</a> — 提交至Forms入口網站以儲存草稿</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email">透過電子郵件傳送PDF</a> — 透過電子郵件傳送已提交表單的PDF版本</li>
        <li><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model">使用表單資料模型提交</a> — 使用表單資料模型提交資料</li>
      </ul>
    </div>
  </div>
</div>

## AEM Forms as a Cloud Service快速入門

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>適用於商業使用者</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>瞭解基本知識</strong>：瞭解<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">最適化Forms</a>，以及它們如何協助將您的業務流程數位化。</li>
        <li style="margin-bottom: 8px;"><strong>探索範本</strong>：瀏覽<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">預先建立的範本和主題</a>，為您的表單專案開一個好頭。</li>
        <li style="margin-bottom: 8px;"><strong>瞭解表單製作</strong>：依照<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring">表單製作指南</a>建立您的第一個表單。</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>適用於開發人員</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>設定環境</strong>：設定AEM Forms的<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">本機開發環境</a>。</li>
        <li style="margin-bottom: 8px;"><strong>瞭解架構</strong>：瞭解AEM Forms as a Cloud Service的<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">架構</a>。</li>
        <li style="margin-bottom: 8px;"><strong>探索API</strong>：熟悉<a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/">可用的API </a>和SDK，以擴充及整合Forms。</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>適用於管理員</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>加入Cloud Service</strong>：依照<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">加入指南</a>設定AEM Forms as a Cloud Service。</li>
        <li style="margin-bottom: 8px;"><strong>設定服務</strong>：設定<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">與其他Adobe服務</a>的整合，例如Adobe Analytics。</li>
        <li style="margin-bottom: 8px;"><strong>從AEM 6.5移轉</strong>：如果您是來自AEM 6.5，請依照<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=zh-Hant">移轉指南</a>操作，移轉到Cloud Service。</li>
      </ol>
    </div>
  </div>
</div>

## 早期採用者功能

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; margin-bottom: 30px;">
  <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
    <h3>AEM Forms搶先體驗計畫</h3>
  </div>
  <div class="card-body" style="padding: 20px; background-color: #ffffff;">
    <p><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms搶先存取計畫</a>在尖端功能正式推出前便提供獨家存取功能，包括：</p>
    <ul style="margin-top: 10px; padding-left: 25px;">
      <li style="margin-bottom: 8px;"><strong>AEM Forms AI Assistant (Gen AI)</strong> — 使用AI支援的建議更快建立表單</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms Workfront Fusion Connector</strong> — 自動化表單提交所觸發的工作流程</li>
      <li style="margin-bottom: 8px;"><strong>對話式Forms</strong> — 在任何AEM Sites頁面上建立聊天式表單體驗</li>
      <li style="margin-bottom: 8px;"><strong>適用於Edge Delivery的WYSIWYG製作</strong> — 使用Edge Delivery Services的通用編輯器建置表單</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms到Marketo Connector</strong> — 將表單提交與Marketo Engage整合</li>
    </ul>
    <p>如需搶先存取創新技術的完整清單和詳細檔案，請造訪<a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms搶先存取計畫頁面</a>。</p>
  </div>
</div>

<div style="background-color: #f0f7ff; border-left: 4px solid #1473e6; padding: 20px; margin: 30px 0; border-radius: 4px;">
  <h3 style="margin-top: 0; color: #1473e6;">準備好開始使用了嗎？</h3>
  <p><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" style="font-weight: bold; color: #1473e6;">立即加入AEM Forms as a Cloud Service</a>，並轉換您組織的數位表格體驗。</p>
</div>
