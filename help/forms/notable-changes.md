---
title: 6.5FormsAEM與AEM雲服務之間的更改
description: '您是Experience Manager Forms用戶並且希望升級到Adobe Experience Manager Formsas a Cloud Service嗎？ 在升級或遷移到Cloud Service之前，瞭解最顯著的更改。  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 5%

---

# 現有Adobe Experience Manager Forms用戶發生顯著變化  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Formsas a Cloud Service與Adobe Experience ManagerFormsOn-Premise和FormsOn-Premise相比，對現有特性有一些顯著的改變 [!DNL Adobe-Managed Service] 環境。 主要差異如下：

* 該服務提供本地和雲本地開發環境。 您可以使用 [地方開發環境](setup-local-development-environment.md) 開發和test您的自定義代碼、元件、模板、主題、Adaptive Forms和其他資產，然後將這些資產部署到雲環境。 有助於加快開發過程。
* [!DNL AEM] 因為Cloud Service隨內置CDN一起提供。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。
* 雲本地環境沒有Web控制台（配置管理器）。 您可以使用 [[!DNL AEM Forms] as a Cloud ServiceSDK以生成配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和CI/CD管道到 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 你的Cloud Service。

* 本地化的自適應Forms的URL約定現在支援在URL中指定區域設定。 新URL約定可在Dispatcher或CDN上快取本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求自適應表單的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`。 Adobe建議使用Dispatcher或CDN快取。 它有助於提高預填充表單的渲染速度。
* 預填充服務將資料與客戶端上的自適應表單合併。 它有助於縮短預填自適應表單所需的時間。 您始終可以配置為在Adobe Experience ManagerFormsServer上運行合併操作。
* 預設情況下，電子郵件僅支援HTTP和HTTP協定。 [聯繫支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用用於發送電子郵件的埠，並啟用環境的SMTP協定。
* Adobe Experience Manager Formsas a Cloud Service為您的項目帶來了許多新的功能AEM和可能性。 但是，Adobe Experience Manager馬文項目需要一些變化，以與AEM Cloud Service相容。 在高級別上，AEM需要將內容和代碼分離成離散子包，以考慮可變內容和不可變內容之間的分離。 使用 [儲存庫現代化器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 將內容和代碼分離為離散的包，以與為Adobe Experience Manager as a Cloud Service定義的項目結構相容，從而重組現有項目包。

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* 使用特定於環境的配置來獲取機密OSGi配置值，如口令、專用API密鑰或任何其他值。 出於安全原因，這些不能儲存到Git中。 [使用特定於機密環境的配置在所有Adobe Experience Manager as a Cloud Service環境（包括舞台和生產）中儲存機密的價值](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values)。

有關Adobe Experience Manager as a Cloud Service更改的全面清單，請參閱 [新增和不同](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html)。

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



## 關鍵增強 {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

以下功能和增強功能僅在 [!DNL AEM Forms] as a Cloud Service:

**增強的可視規則編輯器**
該服務提供加固 [可視規則編輯器](rule-editor.md#visual-rule-editor)。 該服務已將下列功能添加到可視規則編輯器中，以幫助您編寫可用規則：

* [新提交事件](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`。 `Step Completion`。 `Successful Submission`, `Error`

* [新資料類型 `scope`](rule-editor.md#custom-functions)。 您可以使用 `scope` 在自定義函式中鍵入資料以傳遞表單的整個範圍。

* 使用能力 [@this在自定義函式中指定JSDoc](rule-editor.md#custom-functions)。 它允許在活動元件中使用@this來調用自定義函式。

* 能夠為基於屬性的規則添加條件。

**核心元件**
的 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 是一組標準化的Web內容管理(WCM)元件，AEM用於加快開發時間並降低維護成本。 [!DNL AEM Forms] as a Cloud Service支援 **[!UICONTROL AEM Forms集裝箱]** 核心元件。 您可以使用元件將自適應表單嵌入到AEM Sites頁。

**AEMFormsas a Cloud Service原型**
[原AEM型](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 幫助您開始開發 [!DNL AEM Forms] as a Cloud Service。 可以使用Archetype版本27或更高版本建立與 [!DNL AEM Forms] as a Cloud Service環境。 原型還包括一些樣例主題和模板，幫助您快速啟動。

**在表單和符號之間安全且改進的資訊流**
[自適應Forms與Adobe Sign整合](working-with-adobe-sign.md) Cloud Service提供資料同時提交和簽名活動。 它使表單提交與簽署狀態無關，為更快提交鋪平了道路。 此外，服務不會在Cloud Service實例上保存任何資料，使簽名過程變得超級安全。

**最佳做法分析器和遷移工具**
最佳做法分析器提供對您當前實施的AEM評估。 在之前運行工具 [遷移到Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md)。 它評估是否準備從現有Adobe Experience Manager(AEM)部署遷AEM至as a Cloud Service。

該服務還提供 [改進的遷移體驗](migrate-to-forms-as-a-cloud-service.md) 幫助您輕鬆地從 [!DNL AEM 6.4 Forms] 和 [!DNL AEM 6.5 Forms] 至 [!DNL AEM Forms] as a Cloud Service。

**更快的表單格式副本和更快的伺服器端驗證**
該服務使用CDN和Dispatcher快取為Adaptive Forms提供更快的格式副本和伺服器端驗證。

**改進的驗證碼**
你現在可以 [驗證驗證驗證碼](captcha-adaptive-forms.md) 在Adaptive Form提交或業務邏輯上。 您還可以添加條件，以在用戶操作上驗證驗證碼查，並根據規則在自適應表單中顯示或隱藏驗證碼查元件。

驗證碼元件提供了與GooglereCAPTCHA的現成整合。 如有必要，您還可以為元件配置更多驗證碼服務。

**記錄文檔的多個母版頁**
現在，您可以為「記錄文檔」的每頁使用不同的母版頁，並可以控制「記錄文檔」上的「自適應表單」面板的位置，並帶有分頁選項。

**向無頭表添加列**
您可以向沒有標題的表添加列並刪除列。 隱藏的標題會添加到這些表中，以幫助您添加和刪除列。 這些標題在創作過程中可見，但仍隱藏在已發佈的窗體中。 沒有標題的表大多位於使用Automated forms conversion服務建立的AdaptiveForms中。

**改進的提交操作**
您可以使用 [發送電子郵件](configuring-submit-actions.md#send-email#send-email) 提交操作以將記錄文檔(DoR)PDF作為附件發送。

**為工作流分組電子郵件**
您可以選擇 [發送通知電子郵件](aem-forms-workflow-step-reference.md#assign-task-step) 從「分配任務」步驟分配給單個人員或組。

**增強的調用表單資料模型步驟**
現在，您可以在調用表單資料模型步驟中為輸入服務參數的「相對負載」選項指定資料夾路徑。 它幫助您將指定資料夾中存在的檔案映射到服務參數，而無需指定確切的檔案名。

**提高翻譯檔案的可讀性**
在Formsas a Cloud Service上，自適應表單的欄位和面板的讀取順序和相應翻譯檔案（.XLIFF檔案）的消息鍵具有相似的結構。 它有助於提高手動翻譯速度。

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
