---
title: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
translation-type: tm+mt
source-git-commit: a93db92689928a900662a39b11bb5a7ea9724e62
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節將[!DNL Experience Manager]的一般發行說明概述為Cloud Service。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.2.0的發行日期為2021年2月25日。
下列版本(2021.3.0)將於2021年3月25日發行。

## [!DNL Adobe Experience Manager Sites] Cloud Service  {#sites}

### 無頭內容管理{#headless}

* **[內容片段傳送的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能夠使用GraphQL語法查詢內容片段，並根據內容片段模型來結構，以便以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能夠使用伺服器端API的存取Token來驗證GraphQL API請求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**:新增支援在使用中檢視和編SPA輯外AEM部。

* **[在中編SPA輯外AEM部](/help/implementing/developing/hybrid/editing-external-spa.md)**:新增將獨立單頁應用程式上傳至例項、新增可編AEM輯的內容區段，以及啟用編寫功能的能力。

* 從GraphQL API增強JSON輸出，包括以JSON格式和地區設定輸出豐富型文字的功能。

* 支援巢狀內容片段模型，以允許透過多行文字欄位中的專屬內容片段參考資料類型或內容片段參考，建立巢狀內容片段結構。

* 內容片段模型資料類型中提供的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 可標籤內容片段模型，並允許在資料夾中依標籤或路徑建立內容片段原則。

* 內容片段編輯器中的可用性增強功能，包括發佈動作和片段所依據的模型顯示。

* 可直接在內容片段編輯器中預覽JSON輸出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] {#what-is-new-assets}的新增功能

* 在[!DNL Brand Portal]中，會引入新的下載設定，可讓您在下載檔案夾、系列等時，為每個資產建立個別的檔案夾。 請參閱[下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 在解決命名衝突後建立新版本的現有資產時，會覆寫原始資產的中繼資料。 (CQ-4313594)
* 當打印具有長注釋文本的資產時，即使有空格，注釋文本也會被修剪。 (CQ-4314101)
* 當選取多個資產以更新屬性時，有時候會發生錯誤，或未選取資產的屬性會更新。 (CQ-4316532)
* 當嘗試開啟[!UICONTROL 資產管理搜尋邊欄]時，頁面仍為空白，按一下[!UICONTROL 編輯] > [!UICONTROL 設定]會產生錯誤。 (CQ-4315079)

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager作為2021.2.0Cloud ServiceAEM的發行日期為2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* 資產客戶現在可以選擇透過Cloud Manager UI以自助方式部署其品牌入口網站實例的時間和地點。 對於具有資產解決方案的一般（非沙盒）方案，現在可在生產環境中布建品牌入口網站。 在生產環境上只能執行一次置備。

* 「專AEM案與沙盒建立」中使用的「專案原型」已更新為第25版。

* 在程式碼掃描期間識別的已過時API清單已經過改良，以包含最新版Cloud ServiceSDK中已過時的其他類別和方法。

* SonarQube的Cloud Manager設定檔已更新，以移除Sonar規則squid:S2142。 這將不再與「線程中斷檢查」衝突。

* Cloud Manager UI會通知暫時無法新增／更新網域名稱的使用者，因為相關環境會附加一個執行中的管道，或目前正在等待核准步驟。

* 現在會動態移除客戶`pom.xml`檔案中預先加上聲納的屬性，以避免建置和品質掃描失敗。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 已新增其他程式碼品質規則，以涵蓋Cloud Service相容性問題。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者並顯示適當的錯誤訊息。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管線故障錯誤報告為管線錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.4的發行日期為2021年2月10日。

### 錯誤修正 {#bug-fixes-ctt}

* 對應多個使用者時，有些使用者的IMS ID映射不正確。 這個問題已經修正。

### 發行日期 {#release-date-ctt-feb}

內容傳輸工具v1.2.2的發行日期為2021年2月1日。

### 內容傳輸工具{#what-is-new-ctt}的新增功能

* 內容傳輸工具——使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其Adobe的Identity Management系統ID，做為內容移轉活動的一部分。
如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容傳輸工具現在會移轉移移集（包括子系）中參考的所有群組和使用者。
* 在建立遷移集時，允許用戶選擇`/etc`下的某些路徑。

## 最佳做法分析器{#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的發行日期為2021年2月18日。

### Best Practices Analyzer {#what-is-new-bpa}的新增功能

* 能夠發現AEM Forms和AEM Forms執行情況的使用情況，並指出與移徙到AEM Forms有關的Cloud Service。
* 能夠偵測並報告自訂元件和範本的使用情況和計數。
* 能夠檢測所使用的節點儲存和資料儲存的類型。
* 能夠偵測到Dynamic Media的使用情況。
* 可偵測使用的Java版本。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具{#what-is-new-crt}的新增功能

* 新版AIO-CLI增效模組已發行。 此插件的最新版本包含Repository Modernizer的幾個錯誤修正。
請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以進一步瞭解此外掛程式。

### 錯誤修正 {#bug-fixes-crt}

* 在Repository Modernizer上完成的幾個錯誤修正。
請參閱[GitHub資源：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)以取得詳細資訊。








