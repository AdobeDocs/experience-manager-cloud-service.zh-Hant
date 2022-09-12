---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.2.0版發行說明。」'
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下章節概述的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service的2021.2.0是2021年2月25日。
下列版本(2021.3.0)將於2021年3月25日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### 無頭式內容管理 {#headless}

* **[用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md)**:可使用GraphQL語法查詢內容片段，以及根據內容片段模型的結構，以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/headless/security/authentication.md)**:可使用伺服器端API的存取權杖，驗證GraphQL API請求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**:新增在AEM中使用檢視和編輯外部SPA的支援。

* **[在AEM中編輯外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**:新增將獨立單頁應用程式上傳至AEM執行個體、新增可編輯的內容區段及啟用製作的功能。

* 從GraphQL API增強JSON輸出，包括以JSON格式和地區設定輸出RTF。

* 支援巢狀內容片段模型，以允許透過專用的內容片段參考資料類型或內嵌在多行文字欄位中的內容片段參考，建立巢狀內容片段結構。

* 內容片段模型資料類型中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 可標籤內容片段模型，以及允許在資料夾中建立內容片段，並依標籤或路徑使用原則。

* 內容片段編輯器中的可用性增強功能，包括發佈動作和片段所依據之模型的顯示。

* 可在內容片段編輯器中直接預覽JSON輸出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets]的新增功能 {#what-is-new-assets}

* 資產可來源為 [!DNL Experience Manager Assets Brand Portal]. 這有助於為新的行銷活動、像片和專案從代理商使用者處取得資產。

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 有權預先設定 [!DNL Brand Portal] 例項。 此 [!DNL Cloud Manager] 使用者可啟用 [!DNL Brand Portal] on [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. 請參閱 [啟用Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant).

* 企業現在可以使用 [!DNL Brand Portal]. 資產來源補充功能可運用 [!DNL Brand Portal] 協助客戶與代理商使用者互動，為新的行銷活動、像片和專案尋找資產。 請參閱 [資產來源 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* 此 [!DNL Brand Portal] 使用狀況報表現在只顯示使用中使用者。 現在不會顯示非使用中使用者。 作用中使用者是指將帳戶指派給 [!DNL Admin Console]. 請參閱 [[!DNL Brand Portal] 報告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* 在 [!DNL Brand Portal]，推出新的下載設定，可讓您在下載資料夾、集合等時，為每個資產建立個別的資料夾。 請參閱 [下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 選取多個資產以更新屬性時，有時會發生錯誤，或取消選取資產的屬性會更新。 (CQ-4316532)
* 嘗試開啟時 [!UICONTROL Assets管理搜尋邊欄]，則頁面會保留空白，然後按一下 [!UICONTROL 編輯] > [!UICONTROL 設定] 產生錯誤。 (CQ-4315079)
* 解決命名衝突後建立新版本的現有資產時，會覆寫原始資產的中繼資料。 (CQ-4313594)
* 打印具有長注釋文本的資產時，即使空間可用，注釋文本也會被修剪。 (CQ-4314101)

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：使用體驗片段，讓產品目錄頁面個別豐富。

* 延伸產品主控台屬性，以顯示連結的資產和體驗片段，包括快速導覽至相關內容的動作。

* CIF Venia Reference Site - 2021.02.24已發佈，其中包含最新CIF核心元件1.8.0版。請參閱 [CIF Venia參考站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) 以取得更多詳細資訊。

* CIF核心元件1.8.0版已發行。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) 以取得更多詳細資訊。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM 2021.2.0中的Cloud Manageras a Cloud Service日期為2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets客戶現在可以透過Cloud Manager UI以自助方式部署其Brand Portal執行個體，選擇時機和位置。 針對具有Assets解決方案的一般（非沙箱）方案，現在可在生產環境中布建Brand Portal。 布建只能在生產環境中執行一次。

* 專案和沙箱建立中使用的AEM專案原型已更新為25版。

* 程式碼掃描期間識別的已棄用API清單已經過細化，加入最新Cloud ServiceSDK版本中已棄用的其他類別和方法。

* 更新Cloud Manager的SonarQube設定檔，以移除Sonar規則squid:S2142。 這不再與執行緒中斷檢查衝突。

* Cloud Manager UI會通知暫時無法新增/更新網域名稱的使用者，因為相關環境已附加執行中的管道，或目前正在等候核准步驟。

* 客戶中設定的屬性 `pom.xml` 前置詞為「聲納」的檔案現在會動態移除，以避免建置和品質掃描失敗。

* 如果目前部署的網域名稱正在使用SSL憑證，Cloud Manager UI會通知暫時無法選取該憑證的使用者。

* 已新增其他程式碼品質規則，以涵蓋Cloud Service相容性問題。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者，並顯示適當的錯誤訊息。

* 如果目前部署的網域名稱正在使用SSL憑證，Cloud Manager UI會通知暫時無法選取該憑證的使用者。

* 在某些情況下，內部問題可能會導致環境刪除卡住。

* 某些管道故障錯誤報告為管道錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容轉移工具1.2.4版的發行日期為2021年2月10日。

### 錯誤修正 {#bug-fixes-ctt}

* 對應多個使用者時，部分使用者的IMS ID對應錯誤。 此問題已修正。

### 發行日期 {#release-date-ctt-feb}

內容轉移工具1.2.2版的發行日期為2021年2月1日。

### 「內容轉移工具」的新功能 {#what-is-new-ctt}

* 內容轉移工具 — 使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID，作為內容移轉活動的一部分。
請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 以取得更多詳細資訊。
* 「內容轉移工具」現在會移轉移集中參考的所有群組和使用者，包括子項。
* 使用者可在下選取特定路徑 `/etc` 建立移轉集時。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的發行日期為2021年2月18日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠偵測AEM Forms和AEM Forms實作的使用情形，並指出與移轉至AEM Formsas a Cloud Service相關的區域。
* 偵測及報告自訂元件和範本的使用情況和計數。
* 偵測所使用節點存放區類型和資料存放區的功能。
* 偵測Dynamic Media使用情形的功能。
* 偵測所使用Java版本的功能。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具的新功能 {#what-is-new-crt}

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本包含Repository Modernizer的多項錯誤修正。
請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以深入了解此外掛程式。

### 錯誤修正 {#bug-fixes-crt}

* Repository Modernizer上已完成多項錯誤修正。
請參閱 [GitHub資源：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以取得更多詳細資訊。
