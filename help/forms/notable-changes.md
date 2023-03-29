---
title: AEM 6.5 Forms與AEM雲端服務之間的差異
description: 您是Experience Manager Forms使用者，且想要升級至Adobe Experience Manager Formsas a Cloud Service? 比較AEM 6.5 Forms和AEM雲端服務，並了解最顯著的變更，再升級或移轉至Cloud Service。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 0%

---

# 現有Adobe Experience Manager 6.5 Forms使用者的重大變更  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service對現有功能進行了幾項重大變更，比如Adobe Experience Manager Forms On-Premise和 [!DNL Adobe-Managed Service] 環境。 主要差異列於下列：

## 雲端原生功能

* 該服務具有雲端原生架構，可根據負載自動調整規模、為升級提供零停機時間、頻繁和在推出新功能和更新之後，以及為實現最大可復原性和效率而優化的拓撲。

* 此服務不包含會將資料儲存至Adobe Experience ManagerCloud Service例項的提交動作，使其變得超級安全。 透過表單擷取的資料會直接傳送至設定的資料存放區。

* 此外，還隨附免費的CDN（內容傳遞網路），協助您以更快的速度傳遞及轉譯表單。


## 開發流程更新

* 此服務提供SDK，可在本機環境（本機電腦）中開發及測試自訂程式碼，再將程式碼部署至Cloud Service。 開發人員可在本機電腦上使用SDK，開發及測試自訂元件、主題、工作流程應用程式、設定、範本等。 在本機開發環境中測試自訂程式碼後，他們將自訂程式碼部署至 [Forms CS環境開發或預備環境](/help/implementing/cloud-manager/deploy-code.md) 以進一步測試，然後再將其提升至生產環境。

* 開發人員會以通用方式維護Cloud Service和本機開發環境的程式碼 [git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). 系統會在建立AEMas a Cloud Service程式時自動建立以AEM原型為基礎的Git存放庫。

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Service的開發流程符合AEM Cloud Service的AEM原型。 不過，Adobe Experience Manager Maven專案需進行一些變更，才能與AEM Cloud Service相容。 在高階層，AEM需要將內容和程式碼分離為離散子封裝，以遵循可變和不可變內容之間的分割。 使用 [Repository Modernizer工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 將內容和程式碼分離為獨立套件，以與為Adobe Experience Manager as a Cloud Service定義的專案結構相容，借此重新建構現有的專案套件。

* 在搭配Forms as a Cloud Service使用客戶套件組合之前，請使用最新版的adobe-aemfd-docmanager重新編譯自訂程式碼。

* 使用 [AEM Formsas a Cloud Service移轉公用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 準備和移轉適用性Forms、主題、範本和雲端設定，從 <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi和AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service。 使用 [程式的Git存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 匯入現有的最適化表單範本。

* 依預設，電子郵件僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用用於發送電子郵件的埠，並為您的環境啟用SMTP協定。

## 本土化

* 本地化適用性Forms的URL慣例現在支援在URL中指定地區設定。 新的URL慣例會啟用快取Dispatcher或CDN上的本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe建議使用Dispatcher或CDN快取。 有助於改善預填表單的轉譯速度。


## 最適化表單

* **規則編輯器：** AEM Formsas a Cloud Service [規則編輯器](rule-editor.md#visual-rule-editor). Forms as a Cloud Service上無法使用程式碼編輯器。

   此 [遷移實用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 可協助您移轉具有自訂規則的表單（在程式碼編輯器中建立）。 此公用程式會將這些規則轉換為Forms as a Cloud Service上支援的自訂函式。 您可以搭配規則編輯器使用可重複使用的函式，繼續取得使用規則指令碼取得的結果。 此 `onSubmitError` 或 `onSubmitSuccess` 函式現在可在規則編輯器中作為動作使用。

* **預填服務：** 預設情況下，預填服務會合併用戶端上的適用性表單資料，而非合併AEM 6.5 Forms中的伺服器上的資料。 此功能有助於縮短預填最適化表單的所需時間。 您一律可以設定在Adobe Experience Manager Forms伺服器上執行合併動作。

* **提交操作：** 此 **電子郵件** 「提交」操作提供了發送附件和附加「記錄文檔(DoR)」和電子郵件的選項。 您可以使用它來取代 **以電子郵件方式PDF** AEM 6.5 Forms中可用的動作。

* **automated forms conversion服務**:服務不提供Automated forms conversion服務的元模型。 您可以 [從Automated forms conversion服務檔案下載](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **基於XSD的適用性Forms:** 您可以使用XDP模板來設計「要記錄的文檔」模板。 此服務不支援以XFA為基礎的適用性Forms

* **元件**:您可以使用 [適用性Forms核心元件](/help/forms/creating-adaptive-form-core-components.md) 來設計表單。 這些元件以WCM核心元件為基礎，遵循BEM標準，且易於定制。 此服務不支援表單內簽署體驗，也不包含適用性表單的摘要和驗證元件

## 表單入口網站

* 您可以使用Forms Portal的搜尋與撰寫器、草稿與提交以及連結元件，列出登入使用者的表單。 無法立即取得對匿名使用Forms Portal的支援(OOTB)。 您可以自訂Forms Portal，為未登入的使用者啟用顯示表單功能。

* 服務不會保留草稿和已提交適用性Forms的中繼資料。

## 文件服務:

Formsas a Cloud Service提供檔案產生和檔案操作RESTful API。 您可以視需要使用這些API，依需求或批次產生或處理檔案：

* **文檔服務：檔案產生API（輸出服務）**:在單一API呼叫或批次中，您只能使用一個範本搭配多個DATA XML檔案。 不支援在單一API呼叫中使用多個範本及多個資料檔案。

* **文檔操作API（組合器服務）**:

   * 依賴文檔服務或應用程式的操作不可用。 例如，Microsoft Word轉PDF、Microsoft Excel轉PDF、HTML轉PDF、PostScript(PS)轉PDF、XDP轉PDF forms皆不支援。 這些操作分別依賴Microsoft Office、Adobe Acrobat、AdobeDistiller、Forms檔案服務。

   * 將非PDF格式的檔案轉換為PDF格式，再搭配「通訊檔案操作API」使用。 例如，如果您的檔案為Microsoft Office、HTML、PostScript(PS)、XDP格式，請先將這些檔案轉換為PDF格式，再將這些檔案與PDF檔案搭配使用。 您可以使用 [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) 服務。

* 您可以使用AEM 6.5 Forms環境進行數位簽名、加密、Reader擴充功能、傳送至印表機、轉換PDF和條碼式Forms服務。


## 資料整合（表單資料模型）

* 此服務還支援JDBC連接器、Microsoft Dynamics、SalesForce、基於SOAP的Web服務以及支援OData的服務。

* 您也可以連接AEM使用者設定檔以擷取和更新使用者資訊。

* Forms資料模型僅支援HTTP和HTTPS端點來提交資料。 此服務不支援REST連接器的Mutual SSL，以及SOAP資料來源的x509憑證式驗證。

* Forms as a Cloud Service允許將Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive和支援一般CRUD（建立、讀取、更新和刪除）操作的服務用作資料儲存，支援Open API規範2.0和Open API 3.0規範。


## 電子簽名

* 此服務提供與Adobe Sign的OOTB整合，並支援DocuSign進行電子簽名。

* 此服務也支援Adobe Sign角色。 您可以在適用性Forms編輯器中設定角色，供商務使用者輕鬆設定簽署工作流程。


## HTML5 Forms

* 您可以使用AEM 6.5 Forms環境來：

   * 將以XDP為基礎的表單轉譯為HTML5 Forms。 此服務不支援HTML5 Forms(行動Forms)。

   * 離線捕獲資料，並在您下次重新聯機時同步資料 [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 應用程式。

## 互動式通訊

* 您可以使用通訊API，依需求或針對Formsas a Cloud Service批次產生個人化檔案。 您可以針對互動式通訊和代理程式UI使用案例使用AEM 6.5 Forms環境。


