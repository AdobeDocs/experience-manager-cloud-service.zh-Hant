---
title: AEM Forms as a Cloud Service 常見問題
description: AEM Forms as a Cloud Service 常見問題
contentOwner: khsingh
role: User
feature: Adaptive Forms
index: false
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 100%

---

# 常見問題 {#frequently-asked-questions}

* **我可以使用程式碼編輯器建立規則嗎？**
您可以使用視覺編輯器來建立規則。[!DNL Forms] as a Cloud Service 無法使用程式碼編輯器。如果您的最適化表單使用由程式碼編輯器開發的規則指令碼，請使用[移轉公用程式](migrate-to-forms-as-a-cloud-service.md)將您的程式碼指令碼轉換為自訂函數。您可以使用視覺編輯器搭配自訂函數，繼續取得使用程式碼編輯器取得的結果。

* **我可以在 Cloud Service 執行個體上建立基於 XFA 的最適化表單嗎？**&#x200B;是，您可以在 Cloud Service 執行個體上建立基於 XFA 的最適化表單。但是，AEM Forms as a Cloud Service SDK (本機開發環境) 不支援基於 XFA 的最適化表單。如果您打算搭配 XFA 型最適化表單使用 AEM Forms as a Cloud Service SDK，請聯絡 Adobe 支援並附上使用案例和特定要求的詳細資料。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我是否可以把內部部署或 [!DNL Adobe-Managed Services] 環境的內容移轉到 [!DNL Forms] as a Cloud Service 環境？**
是的，您可以把內部部署或 [!DNL Adobe-Managed Services] 環境的自訂程式碼、內容和資產移轉到 [!DNL Forms] as a Cloud Service 環境。詳細指示請參閱「[移轉到 Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md)」。

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **在哪裡可以取得 AEM[!DNL Forms] as a Cloud Service [!DNL Java™]API 參考文件？**
您可以從 [!DNL Maven Central Repository] 下載 Java™ API 參考文件。要下載：
   1. 前往 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api)。
   1. 找到並開啟包含最新版本 [!DNL Experience Manager Forms] SDK 的頁面。
   1. 按一下「查看全部」選項以查看所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-javadocs`.jar。
   1. 開啟 index.html 檔案以查看 API 參考文件。

* **我可以從哪裡取得最適化表單的 [!DNL JavaScript™] API 參考？**
您可以下載 [!DNL JavaScript™] API 參考文件，下載位置是 [!DNL  Maven Central Repository]。要下載：
   1. 開啟 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api)。
   1. 找到並開啟包含最新版本 [!DNL Experience Manager Forms] SDK 的頁面。
   1. 按一下「查看全部」選項以查看所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-jsdoc.jar`。
   1. 開啟 index.html 檔案以查看 API 參考文件。

* **我可以繼續使用現有的主題和範本嗎？**
是的，您使用[移轉公用程式](migrate-to-forms-as-a-cloud-service.md)將由 AEM 6.4 Forms 和 AEM 6.5 Forms 建立的主題移至 [!DNL AEM Forms] as a Cloud Service 之後，可以繼續使用這些主題。

  您也可以根據 [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)建立專案，並使用內含的主題範例和範本。

* **我可以產生符合綱要的資料嗎？**
是的，您可以建立最適化表單來產生符合綱要的資料。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **我可以快取安全內容嗎？**
預設停用快取安全內容的功能。要啟用該功能，您可以執行「[快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html)」提供的指示。

* **我有一個本地化的最適化表單；它並未轉譯本地化版本嗎？可能是什麼原因以及如何解決？**

  本地化最適化表單的 URL 慣例現在支援在 URL 中指定地區設定。新的 URL 慣例允許快取 Dispatcher 或 CDN 上的本地化表單。在 Cloud Service 環境中，使用 URL 格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` 來請求最適化表單的本地化版本。Adobe 建議使用 Dispatcher 或 CDN 快取。其有助於改善預填表單的轉譯速度。

* **我已經更新最適化表單；更新後的版本無法供客戶使用？**
按照預設，CDN 每 5 分鐘重新整理快取記憶體一次，等待 5 分鐘，然後檢查更新的版本。

* **我可以使用最適化表單中的簽名步驟來建立瀏覽器內簽名體驗嗎？**
不，[!DNL Forms] as a Cloud Service 無法使用簽名步驟。刪除最適化表單中的簽名步驟。允許使用者在提交後簽署最適化表單，而不是使用簽名步驟。它幫助您繼續提供瀏覽器內簽名體驗。

* **我可以在最適化表單中使用驗證步驟嗎？**
不，[!DNL Forms] as a Cloud Service 無法使用驗證步驟。將最適化表單移至 Cloud Service 環境之前，請移除現有最適化表單中的驗證步驟。

* **我可以將圖表新增到最適化表單嗎？**
是，您可以將圖表新增到最適化表單中。最適化表單提供一個圖表元件。您可以使用該元件將圖表新增到最適化表單。

* **我可以將表單資料模型 (FDM) 連接到關聯式資料庫模型嗎？**
您可以將表單資料模型 (FDM) 連接到 [!DNL RESTful web services]、[!DNL SOAP-based web services]、[!DNL OData services] 和 Experience Manager 使用者設定檔做為資料來源。不支援將表單資料模型 (FDM) 與關聯式資料庫連接。

* **我可以使用自訂憑證搭配表單資料模型 (FDM) 進行驗證嗎？**
表單資料模型 (FDM) 不提供使用自訂憑證進行驗證的方法。因此，不支援 x509 和雙向 SSL 等自訂憑證。

* **我可以使用表單入口網站提交動作最適化表單嗎？**

  您可以修改現有的自適應表單以使用[提交至 REST 端點](configuring-submit-actions.md#submit-to-rest-endpoint)、[傳送電子郵件](configuring-submit-actions.md#send-email)、[使用表單資料模型 (FDM) 提交](configuring-submit-actions.md#submit-using-form-data-model)和[叫用 AEM 工作流程](configuring-submit-actions.md#invoke-an-aem-workflow)提交動作。尚未提供表單入口網站與表單入口網站提交動作。各項功能的可用情況請留意每月發行說明。

* **我可以將 [!DNL AEM Forms] 應用程式與 [!DNL AEM Forms] as a Cloud Service 一起使用嗎？**

  最適化表單提供回應式設計。這些表單會根據基礎裝置變更外觀、設計和互動。您可以繼續在行動裝置上使用最適化表單，同時留意每月發行說明以掌握各項功能的可用情況。

* **初始 GA 版本並不包括哪項功能？**
表單入口網站、[!DNL AEM Forms] 應用程式、與 Adobe Analytics 整合以及與 Adobe Target 整合並不是初始 GA 版本的一部分。請查看每月發行說明掌握新功能相關資訊。

* **我設計一個[用來建立最適化表單的 JSON 綱要](adaptive-form-json-schema-form-model.md)。JSON 綱要定義最適化表單某些元件的事件。AEM Forms as a Cloud Service 是否支援事件？**
在 Experience Manager 6.5 Forms 環境中根據 JSON 綱要建立最適化表單，並使用[移轉公用程式](migrate-to-forms-as-a-cloud-service.md)將此類最適化表單移轉至 AEM Forms as a Cloud Service。該公用程式將此類事件轉換為用戶端資料庫，而您可以繼續在 Cloud Service 環境中使用最適化表單來處理事件。

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->
