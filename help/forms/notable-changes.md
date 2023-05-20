---
title: 6.AEM5Forms與AEM雲服務的差異
description: 您是Experience Manager Forms用戶並且希望升級到Adobe Experience Manager Formsas a Cloud Service嗎？ 比較AEM6.5Forms和AEM雲服務，在升級或遷移到Cloud Service之前瞭解最顯著的更改。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 0%

---

# 現有Adobe Experience Manager6.5Forms用戶發生顯著變化  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Formsas a Cloud Service與Adobe Experience Manager Forms本地及本地相比，對現有特點有顯著改變 [!DNL Adobe-Managed Service] 環境。 主要差異如下：

## 雲本機功能

* 該服務具有雲本地架構，可根據負載進行自動擴展、升級時不停機、頻繁推出新功能和更新後不停機、以及為實現最大恢復力和效率而優化的拓撲。

* 該服務不包括將資料儲存到Adobe Experience ManagerCloud Service實例的提交操作，使其超級安全。 通過表單捕獲的資料會直接發送到配置的資料儲存。

* 還包括免費CDN（內容分發網路），以幫助您更快地分發和呈現表單。


## 更新開發流

* 該服務提供SDK，用於在將代碼部署到Cloud Service之前在本地環境（本地電腦）中開發和test自定義代碼。 開發人員在本地電腦上使用SDK開發和test自定義元件、主題、工作流應用程式、配置、模板等。 在其本地開發環境中測試自定義代碼後，他們將自定義代碼部署到 [FormsCS環境開發或階段環境](/help/implementing/cloud-manager/deploy-code.md) 在將其推廣到生產環境之前進行進一步測試。

* 開發人員維護Cloud Service和本地開發環境的代碼 [git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html)。 基於原型的AEMGit儲存庫在建立as a Cloud Service程式時自AEM動建立。

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Service的發展流程與AEM Cloud ServiceAEM的原型相一致。 但是，Adobe Experience Manager馬文項目需要一些變化，以與AEM Cloud Service相容。 在高級別上，AEM需要將內容和代碼分離成離散子包，以考慮可變內容和不可變內容之間的分離。 使用 [儲存庫現代化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 通過將內容和代碼分離為離散的包來重組現有項目包，以與為Adobe Experience Manager as a Cloud Service定義的項目結構相容。

* 在將客戶捆綁包與Formsas a Cloud Service一起使用之前，請使用最新版本的adobe-aemfd-docmanager重新編譯您的自定義代碼。

* 使用 [AEM Formsas a Cloud Service遷移實用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 準備和遷移您的自適應Forms、主題、模板和雲配置 <!-- AEM 6.3 Forms--> OSGiAEM上的Forms6.4 AEMOSGi上的Forms6.5 [!DNL AEM] as a Cloud Service。 使用 [程式的Git儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 導入現有的自適應表單模板。

* 預設情況下，電子郵件僅支援HTTP和HTTP協定。 [聯繫支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用用於發送電子郵件的埠，並啟用環境的SMTP協定。

## 本土化

* 本地化的自適應Forms的URL約定現在支援在URL中指定區域設定。 新URL約定可在Dispatcher或CDN上快取本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求自適應表單的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`。

* Adobe建議使用Dispatcher或CDN快取。 它有助於提高預填充表單的渲染速度。


## 最適化表單

* **規則編輯器：** AEM Formsas a Cloud Service提供 [規則編輯器](rule-editor.md#visual-rule-editor)。 代碼編輯器在Formsas a Cloud Service上不可用。

   的 [遷移實用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 幫助您遷移具有自定義規則的表單（在代碼編輯器中建立）。 該實用程式將這些規則轉換為Formsas a Cloud Service支援的自定義函式。 可以使用規則編輯器中的可重用函式繼續獲取使用規則指令碼獲得的結果。 的 `onSubmitError` 或 `onSubmitSuccess` 現在，函式在規則編輯器中可用作操作。

* **預填充服務：** 預設情況下，預填充服務將資料與客戶端上的Adaptive Form合併，而不是合併FormsAEM6.5版伺服器上的資料。 該功能有助於縮短預填自適應表單所需的時間。 您始終可以配置在Adobe Experience Manager Forms伺服器上運行合併操作。

* **提交操作：** 的 **電子郵件** 提交操作提供了發送附件和將記錄文檔(DoR)與電子郵件附加的選項。 你可以用它代替 **電子郵件作為PDF** 可在AEMForms6.5採取行動。

* **automated forms conversion服務**:該服務未為Automated forms conversion服務提供元模型。 你可以 [從Automated forms conversion服務文檔下載](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model)。

* **基於XSD的自適應Forms:** 可以使用XDP模板為「記錄文檔」設計模板。 該服務不支援基於XFA的自適應Forms

* **元件**:您可以使用 [自適應Forms核心元件](/help/forms/creating-adaptive-form-core-components.md) 來設計表單。 這些元件基於WCM核心元件，遵循BEM標準，並且可以輕鬆定制。 該服務不支援表單簽名體驗，也不包括Adaptive Form的「摘要」和「驗證」元件

## 表單入口網站

* 您可以使用Forms門戶的Search &amp; Lister、Drafts and Submission和Link元件來列出登錄用戶的表單。 對匿名使用Forms門戶的支援不是現成的(OOTB)。 您可以自定義Forms門戶，以啟用非登錄用戶的顯示表單。

* 該服務不保留草稿的元資料，並已提交自適應Forms。

## 文件服務:

Formsas a Cloud Service提供文檔生成和文檔處理REST風格API。 您可以根據需要使用這些API按需或批量生成或處理文檔：

* **文檔服務：文檔生成API（輸出服務）**:在單個API調用或批處理中，只能使用一個模板和多個DATA XML檔案。 不支援在單個API調用中使用具有多個資料檔案的多個模板。

* **文檔操作API（匯編器服務）**:

   * 依賴於文檔服務或應用程式的操作不可用。 例如，不支援將MicrosoftWordPDF、將MicrosoftExcelPDF、將HTMLPDF、PostScript(PS)PDF、XDPPDF forms。 這些業務分別依賴Microsoft辦事處、Adobe Acrobat、AdobeDistiller、Forms檔案處。

   * 在使用「通信文檔操作API」之前，將非PDF格式的文檔轉換為PDF格式。 例如，如果文檔為MicrosoftOffice、HTML、PostScript(PS)和XDP格式，請在將文檔與PDF文檔一起使用之前，將這些文檔轉換為PDF格式。 您可以使用 [轉換PDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) 服務。

* 您可以使用AEM6.5Forms環境進行數字簽名、加密、Reader擴展、發送到打印機、轉換PDF和條形碼Forms服務。


## 資料整合（表單資料模型）

* 該服務還支援JDBC連接器、Microsoft Dynamics、SalesForce、基於SOAP的Web服務以及支援OData的服務。

* 您還可以連AEM接用戶配置檔案以檢索和更新用戶資訊。

* Forms資料模型只支援HTTP和HTTPS端點提交資料。 該服務不支援REST連接器的Mutual SSL和SOAP資料源的基於x509證書的身份驗證。

* Formsas a Cloud Service允許將MicrosoftAzure Blob、MicrosoftSharepoint、MicrosoftOneDrive和支援一般CRUD（建立、讀取、更新和刪除）操作的服務用作資料儲存，支援Open API規範2.0和Open API 3.0規範。


## 電子簽名

* 該服務提供與Adobe Sign的OOTB整合，並支援DocuSign進行電子簽名。

* 該服務還支援Adobe Sign角色。 您可以在AdaptiveForms編輯器中為業務用戶配置角色，以便輕鬆配置簽名工作流。


## HTML5 Forms

* 您可以使用AEM6.5Forms環境：

   * 將基於XDP的表單呈現為HTML5Forms。 該服務不支援FormsHTML(移動Forms)。

   * 將資料離線捕獲並同步，下次您返回聯機時 [AEM Forms工作區](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 的子菜單。

## 互動式通訊

* 您可以使用Communications API按需或在Formsas a Cloud Service批量生成個性化文檔。 您可以將AEM6.5Forms環境用於Interactive Communications和Agent UI用例。


