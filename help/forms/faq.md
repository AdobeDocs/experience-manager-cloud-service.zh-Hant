---
title: 'Formsas a Cloud Service常見問題 '
description: Formsas a Cloud Service常見問題
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# 常見問題 {#frequently-asked-questions}

* **我可以使用代碼編輯器來建立規則嗎？**
您可以使用可視化編輯器建立規則。 代碼編輯器無法在上使用 [!DNL Forms] as a Cloud Service。 如果您的適用性表單使用使用程式碼編輯器開發的規則指令碼，請使用 [遷移實用程式](migrate-to-forms-as-a-cloud-service.md) 將程式碼指令碼轉換為自訂函式。 您可以透過可視化編輯器使用自訂函式，繼續取得使用程式碼編輯器取得的結果。

* **我可以在Cloud Service例項上建立XFA型適用性表單嗎？**
可以，您可以在Cloud Service例項上建立XFA型適用性表單。 不過，AEM Formsas a Cloud ServiceSDK（本機開發環境）不支援以XFA為基礎的適用性Forms。 如果您想搭配AEM Formsas a Cloud ServiceSDK使用XFA型適用性Forms，請聯絡Adobe支援，提供您使用案例和特定需求的詳細資訊。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我可以從內部部署移轉內容嗎？ [!DNL Adobe-Managed Services] 環境 [!DNL Forms] as a Cloud Service環境？**
可以，您可以從內部部署移轉自訂程式碼、內容和資產，或 [!DNL Adobe-Managed Services] 環境 [!DNL Forms] as a Cloud Service環境。 如需詳細指示，請參閱 [移轉至Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **我可以在何處取得AEM [!DNL Forms] as a Cloud Service [!DNL Java™] API參考檔案？**
您可以從以下網址下載Java™ API參考檔案： [!DNL Maven Central Repository]. 若要下載：
   1. 前往 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到並開啟包含 [!DNL Experience Manager Forms] SDK.
   1. 按一下「查看全部」(View All)選項查看所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-javadocs`.jar。
   1. 開啟index.html檔案以檢視API參考檔案。

* **在哪裡可以找到 [!DNL JavaScript™] 適用性Forms的API參考資料？**
您可以下載 [!DNL JavaScript™] 來自的API參考檔案[!DNL  Maven Central Repository]. 若要下載：
   1. 開啟 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到並開啟包含 [!DNL Experience Manager Forms] SDK.
   1. 按一下「查看全部」(View All)選項查看所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. 開啟index.html檔案以檢視API參考檔案。

* **我可以繼續使用現有的主題和範本嗎？**
可以，在使用 [遷移實用程式](migrate-to-forms-as-a-cloud-service.md) 將其移至 [!DNL AEM Forms] as a Cloud Service。

   您也可以根據 [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 和使用包含的範例主題和範本。

* **我可以產生符合架構的資料嗎？**
是的，您可以建立適用性Forms，以產生符合架構的資料。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **我可以快取安全內容嗎？**
預設會停用快取安全內容功能。 若要啟用此功能，您可以執行 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

* **我有本地化的最適化表單；它未呈現本地化版本？ 原因何在，如何解決？**

   本地化適用性Forms的URL慣例現在支援在URL中指定地區設定。 新的URL慣例會啟用快取Dispatcher或CDN上的本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建議使用Dispatcher或CDN快取。 有助於改善預填表單的轉譯速度。

* **我已更新適用性表單；客戶無法使用更新的版本嗎？**
依預設，CDN會每5分鐘重新整理快取、等待5分鐘，然後檢查更新的版本。

* **我可以在適用性表單中使用簽名步驟來建立瀏覽器內簽署體驗嗎？**
否，「簽名」步驟不適用於 [!DNL Forms] as a Cloud Service。 移除最適化Forms中的簽章步驟。 與「簽名」步驟不同，讓使用者在提交後簽署最適化表單。 可協助您繼續提供瀏覽器內簽署體驗。

* **我可以在適用性表單中使用驗證步驟嗎？**
否，驗證步驟不適用於 [!DNL Forms] as a Cloud Service。 先移除現有適用性Forms中的驗證步驟，再將這類表單移至Cloud Service環境。

* **我可以將圖表新增至最適化表單嗎？**
可以，您可以將圖表新增至適用性Forms。 適用性Forms提供圖表元件。 您可以用它來將圖表新增至最適化表單。

* **我可以將表單資料模型連接到關係資料庫模型嗎？**
您可以將表單資料模型連結至 [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services]，並將使用者設定檔Experience Manager為資料來源。 無法支援將表單資料模型與關係資料庫連接。

* **我可以搭配表單資料模型使用自訂憑證進行驗證嗎？**
表單資料模型未提供使用自訂憑證進行驗證的方法。 因此，不支援x509和2向SSL等自訂憑證。

* **我可以使用Forms Portal提交動作適用性Forms嗎？**

   您可以修改現有的適用性Forms以使用 [提交到REST端點](configuring-submit-actions.md#submit-to-rest-endpoint), [傳送電子郵件](configuring-submit-actions.md#send-email), [使用表單資料模型提交](configuring-submit-actions.md#submit-using-form-data-model)，和 [叫用AEM工作流程](configuring-submit-actions.md#invoke-an-aem-workflow) 提交操作。 Forms Portal和Forms Portal提交動作尚未推出。 請留意每月的發行說明，以了解功能的可用性。

* **我可以使用 [!DNL AEM Forms] 應用程式搭配 [!DNL AEM Forms] as a Cloud Service?**

   適用性Forms提供回應式設計。 這些表單會根據基礎裝置改變外觀、設計和互動功能。 您可以在行動裝置上繼續使用適用性Forms，同時每月都會關注功能可用性的發行說明。

* **哪些功能不屬於初始GA版本？**
Forms門戶網站， [!DNL AEM Forms] 應用程式、Adobe Analytics整合以及Adobe Target整合不屬於初始GA版本。 如需新功能的相關資訊，請參閱每月發行說明。
