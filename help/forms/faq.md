---
title: 'Formsas a Cloud Service常見問題 '
description: Formsas a Cloud Service常見問題
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: a5cd8a49a74eb8372d1d363ff859e1aef921859b
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 2%

---

# 常見問題 {#frequently-asked-questions}

* **是否可以使用代碼編輯器建立規則？**
可以使用可視編輯器建立規則。 代碼編輯器在上不可用 [!DNL Forms] as a Cloud Service。 如果您的Adaptive Form使用使用代碼編輯器開發的規則指令碼，請使用 [遷移實用程式](migrate-to-forms-as-a-cloud-service.md) 將代碼指令碼轉換為自定義函式。 可以將自定義函式與可視編輯器一起使用，以繼續獲取使用代碼編輯器獲取的結果。

* **是否可以在Cloud Service實例上建立基於XFA的自適應表單？**
是，可以在Cloud Service實例上建立基於XFA的自適應表單。 但是，AEM Formsas a Cloud ServiceSDK（本地開發環境）不支援基於XFA的自適應Forms。 如果您打算將基於XFA的自適應Forms與AEM Formsas a Cloud ServiceSDK配合使用，請與Adobe支援部門聯繫，瞭解您的使用案例和特定要求的詳細資訊。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我是否可以從內部部署遷移內容或 [!DNL Adobe-Managed Services] 環境 [!DNL Forms] as a Cloud Service環境？**
是的，您可以從本地遷移您的自定義代碼、內容和資產，或 [!DNL Adobe-Managed Services] 環境 [!DNL Forms] as a Cloud Service環境。 有關詳細說明，請參見 [遷移到Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md)。

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **我在哪兒AEM? [!DNL Forms] as a Cloud Service [!DNL Java™] API參考文檔？**
您可以從下載Java™ API參考文檔 [!DNL Maven Central Repository]。 下載：
   1. 前往 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 查找並開啟包含最新版本的 [!DNL Experience Manager Forms] SDK。
   1. 按一下「查看全部」(View All)選項查看所有檔案。
   1. 下載並解壓 `aem-forms-sdk-api-<version>-javadocs`.jar。
   1. 開啟index.html檔案以查看API參考文檔。

* **我在哪裡能買到 [!DNL JavaScript™] 適應性Forms的API參考？**
您可以下載 [!DNL JavaScript™] API參考文檔，來自[!DNL  Maven Central Repository]。 下載：
   1. 開啟 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 查找並開啟包含最新版本的 [!DNL Experience Manager Forms] SDK。
   1. 按一下「查看全部」(View All)選項查看所有檔案。
   1. 下載並解壓 `aem-forms-sdk-api-<version>-jsdoc.jar`。
   1. 開啟index.html檔案以查看API參考文檔。

* **我能否繼續使用現有主題和模板？**
是的，在使用了以下AEM選項後，您可以繼AEM續使用6.4Forms和6.5Forms建立的主題 [遷移實用程式](migrate-to-forms-as-a-cloud-service.md) 將它們移動 [!DNL AEM Forms] as a Cloud Service。

   您還可以根據 [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 並使用包含的示例主題和模板。

* **是否可以生成符合架構的資料？**
是的，您可以建立自適應Forms以生成符合模式的資料。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **我能否快取受保護的內容？**
預設情況下，禁用快取安全內容功能。 要啟用該功能，可以執行 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

* **我有一個本地化的適應性表格；它不呈現本地化版本？ 原因何在，如何解決？**

   本地化的自適應Forms的URL約定現在支援在URL中指定區域設定。 新URL約定可在Dispatcher或CDN上快取本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求自適應表單的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`。 Adobe建議使用Dispatcher或CDN快取。 它有助於提高預填充表單的渲染速度。

* **我更新了一個適應性表格；更新的版本不可供客戶使用？**
預設情況下，CDN每5分鐘刷新一次快取，等待5分鐘，然後檢查更新的版本。

* **我是否可以使用自適應表單中的簽名步驟建立瀏覽器內簽名體驗？**
否，簽名步驟不可用於 [!DNL Forms] as a Cloud Service。 刪除自適應Forms中的簽名步驟。 不是「簽名」步驟，而是允許用戶在提交後簽署自適應表單。 它幫助您繼續提供瀏覽器內簽名體驗。

* **是否可以在自適應表單中使用「驗證」步驟？**
否，「驗證」步驟不可用於 [!DNL Forms] as a Cloud Service。 在將這些表單移到Cloud Service環境之前，請從現有的自適應Forms中刪除驗證步驟。

* **是否可以將圖表添加到自適應表單？**
是的，您可以將圖表添加到自適應Forms。 自適應Forms提供圖表元件。 可以使用它將圖表添加到自適應表單。

* **是否可以將表單資料模型連接到關係資料庫模型？**
可以將表單資料模型連接到 [!DNL RESTful web services]。 [!DNL SOAP-based web services]。 [!DNL OData services]和將用戶配置檔案Experience Manager為資料源。 不支援將表單資料模型與關係資料庫連接。

* **是否可以將自定義證書與表單資料模型一起用於身份驗證？**
表單資料模型未提供使用自定義證書進行身份驗證的方法。 因此，不支援自定義證書，如x509和雙向SSL。

* **我能否使用Forms門戶提交操作自適應Forms?**

   您可以修改現有的自適應Forms以使用 [提交到REST終結點](configuring-submit-actions.md#submit-to-rest-endpoint)。 [發送電子郵件](configuring-submit-actions.md#send-email)。 [使用表單資料模型提交](configuring-submit-actions.md#submit-using-form-data-model), [調用工AEM作流](configuring-submit-actions.md#invoke-an-aem-workflow) 提交操作。 Forms門戶和Forms門戶提交操作尚不可用。 請留意每月的發行說明，瞭解功能的可用性。

* **我能用 [!DNL AEM Forms] 應用 [!DNL AEM Forms] as a Cloud Service?**

   最適化表單提供回應式設計。這些表單會根據基礎裝置變更外觀、設計和互動。您可以繼續在移動設備上使用Adaptive Forms，同時在每月發佈說明中查看功能的可用性。

* **哪些功能不是初始GA版本的一部分？**
Forms門戶網站， [!DNL AEM Forms] 應用程式、與Adobe Analytics的整合以及與Adobe Target的整合併非首次正式發佈的一部分。 有關新功能的資訊，請查看每月發行說明。

* **我設計了一個 [JSON架構以建立自適應表單](adaptive-form-json-schema-form-model.md)。 JSON架構為自適應表單的某些元件定義事件。 AEM Formsas a Cloud Service支援事件嗎？**
在Experience Manager6.5Forms環境上基於JSON架構建立自適應表單，並使用 [遷移實用程式](migrate-to-forms-as-a-cloud-service.md) 將這種適應性Forms遷移到AEM Formsas a Cloud Service。 該實用程式將此類事件轉換為客戶端庫，您可以繼續在Cloud Service環境中使用Adaptive Forms來處理事件。

