---
title: AEM 6.5 Forms與AEM雲端服務之間的變更
description: '您是Experience Manager Forms使用者，且想要升級至Adobe Experience Manager Formsas a Cloud Service? 在升級或移轉至Cloud Service之前，請先了解最顯著的變更。  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# 現有Adobe Experience Manager Forms使用者的重大變更  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms Adobe Experience Manager與FormsOn-Premise和 [!DNL Adobe-Managed Service] 環境。 主要差異列於下列：

* 此服務提供本機和雲端原生開發環境。 您可以使用 [本地開發環境](setup-local-development-environment.md) 在將這些資產部署至雲端環境之前，先開發及測試您的自訂程式碼、元件、範本、主題、適用性Forms和其他資產。 有助於加速開發程式。
* [!DNL AEM] Cloud Service隨附內建的CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。
* 雲端原生環境沒有Web主控台(configuration manager)。 您可以使用 [[!DNL AEM Forms] as a Cloud ServiceSDK產生設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和CI/CD管道 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 至您的Cloud Service例項。

* 本地化適用性Forms的URL慣例現在支援在URL中指定地區設定。 新的URL慣例會啟用快取Dispatcher或CDN上的本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建議使用Dispatcher或CDN快取。 有助於改善預填表單的轉譯速度。
* 預填服務會將資料與用戶端上的最適化表單合併。 有助於縮短預填最適化表單的所需時間。 您隨時都可以設定在Adobe Experience Manager FormsServer上執行合併動作。
* 依預設，電子郵件僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用用於發送電子郵件的埠，並為您的環境啟用SMTP協定。
* Adobe Experience Manager Forms as a Cloud Service為您的AEM專案帶來許多新功能，並帶來許多可能性。 不過，Adobe Experience Manager Maven專案需進行一些變更，才能與AEM Cloud Service相容。 在高階層，AEM需要將內容和程式碼分離為離散子封裝，以遵循可變和不可變內容之間的分割。 使用 [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 工具，借由將內容和程式碼分離為獨立套件，以與為Adobe Experience Manager as a Cloud Service定義的專案結構相容，來重新建構現有專案套件。

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* 對機密OSGi設定值（例如密碼、私密API金鑰或任何其他值）使用環境專屬設定。 基於安全性考量，這些ID無法儲存至Git。 [使用機密環境專屬設定，在所有Adobe Experience Manager as a Cloud Service環境（包括預備和生產）上儲存機密值](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

如需Adobe Experience Manager as a Cloud Service中變更的完整清單，請參閱 [新增功能與不同之處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## 重要增強功能 {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

下列功能和增強功能僅適用於 [!DNL AEM Forms] as a Cloud Service:

**增強的可視化規則編輯器**
此服務提供強化的 [可視化規則編輯器](rule-editor.md#visual-rule-editor). 此服務已在Visual規則編輯器中新增下列功能，以協助您撰寫功能強大的規則：

* [新的提交事件](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`，和 `Error`

* [新資料類型 `scope`](rule-editor.md#custom-functions). 您可以使用 `scope` 自訂函式中的資料類型，可傳遞表單的整個範圍。

* 使用功能 [@this在自定義函式中指定JSDoc](rule-editor.md#custom-functions). 它可讓您在作用中元件中使用@this來叫用自訂函式。

* 能為屬性型規則新增條件。

**核心元件**
此 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 是一組標準化的Web內容管理(WCM)元件，供AEM加速開發時間並降低維護成本。 [!DNL AEM Forms] as a Cloud Service支援 **[!UICONTROL AEM Forms容器]** 核心元件。 您可以使用元件將適用性表單內嵌至AEM Sites頁面。

**AEM的Forms原型as a Cloud Service**
[AEM原型](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 可協助您開始開發 [!DNL AEM Forms] as a Cloud Service。 您可以使用原型27版或更新版本，建立與 [!DNL AEM Forms] as a Cloud Service環境。 原型也包含一些範例主題和範本，可協助您快速上手。

**表單與Sign之間資訊的安全與改善**
[適用性Forms與Adobe Sign整合](working-with-adobe-sign.md) Cloud Service提供同時提交資料和簽署活動。 它可讓表單提交與簽署狀態無關，進而加快提交速度。 此外，服務不會儲存Cloud Service例項上的任何資料，使簽署程式變得超級安全。

**Best Practices Analyzer和移轉工具**
Best Practices Analyzer可評估您目前的AEM實作。 先執行工具 [移轉至Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md). 它會評估從現有Adobe Experience Manager(AEM)部署移轉至AEMas a Cloud Service的準備程度。

此服務也提供 [改善移轉體驗](migrate-to-forms-as-a-cloud-service.md) 幫助輕鬆從 [!DNL AEM 6.4 Forms] 和 [!DNL AEM 6.5 Forms] to [!DNL AEM Forms] as a Cloud Service。

**更快速的表單轉譯和更快速的伺服器端驗證**
此服務會使用CDN和Dispatcher快取，為Adaptive Forms提供更快速的轉譯和伺服器端驗證。

**改良驗證碼**
您現在可以 [驗證驗證驗證碼](captcha-adaptive-forms.md) 適用性表單提交時或業務邏輯時。 您也可以新增條件，以針對使用者動作驗證CAPTCHA，並根據規則在適用性表單中顯示或隱藏CAPTCHA元件。

CAPTCHA元件提供與Google reCAPTCHA的現成整合。 如有需要，您也可以為元件設定更多驗證碼服務。

**記錄文檔的多個首頁**
您現在可以為記錄檔案的每個頁面使用不同的主版頁面，並透過分頁選項控制記錄檔案上適用性表單面板的放置位置。

**向無頭表添加列**
您可以新增欄和刪除沒有標題的表格。 隱藏的標題會新增至這些表格，以協助您新增和刪除欄。 這些標題在製作期間可見，但在已發佈的表單中仍隱藏。 沒有標題的表格大多可在使用Automated forms conversion服務建立的適用性Forms中找到。

**改善提交動作**
您可以使用 [傳送電子郵件](configuring-submit-actions.md#send-email#send-email) 提交操作以作為附件發送記錄文檔(DoR)PDF。

**為工作流程分組電子郵件**
您可以選擇 [傳送通知電子郵件](aem-forms-workflow-step-reference.md#assign-task-step) 從「分配任務」步驟分配給單個人員或組。

**增強叫用表單資料模型步驟**
您現在可以在叫用表單資料模型步驟中，為輸入服務引數的相對裝載選項指定資料夾路徑。 它可協助您將指定資料夾中的檔案對應至服務引數，而不需指定確切的檔案名稱。

**提高翻譯檔案的可讀性**
在Formsas a Cloud Service，適用性表單的欄位和面板的讀取順序以及對應翻譯檔案（.XLIFF檔案）的訊息索引鍵具有類似結構。 有助於提高手動翻譯速度。

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
