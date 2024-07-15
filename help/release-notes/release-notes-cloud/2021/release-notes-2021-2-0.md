---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0 版發行說明。'
description: "[!DNL Adobe Experience Manager]個2021.2.0as a Cloud Service發行說明。"
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 31%

---


# [!DNL Adobe Experience Manager]as a Cloud Service的發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]as a Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2021.2.0的發行日期為2021年2月25日。
下列版本(2021.3.0)將於2021年3月25日發行。

## [!DNL Adobe Experience Manager Sites]個as a Cloud Service {#sites}

### Headless內容管理 {#headless}

* **[用於內容片段傳送的GraphQL API](/help/headless/graphql-api/content-fragments.md)**：能夠使用GraphQL語法以及根據內容片段模型的結構描述來查詢內容片段，以產生JSON格式的輸出。

* **[GraphQL API要求的驗證支援](/help/headless/security/authentication.md)**：能夠使用伺服器端API的存取權杖來驗證GraphQL API要求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**：新增在AEM中檢視及編輯外部SPA的支援。

* **[在AEM內編輯外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**：已新增將獨立單頁應用程式上傳到AEM執行個體、新增可編輯的內容區段及啟用編寫的功能。

* GraphQL API的增強型JSON輸出，包括輸出JSON格式的RTF和地區設定的功能。

* 對巢狀內容片段模型的支援，允許透過專用內容片段參考資料型別或內嵌在多行文字欄位中的內容片段參考來建立巢狀內容片段結構。

* 內容片段模型資料型別中可用的其他驗證規則，包括「唯一」、「必要」和「可翻譯」。

* 標籤內容片段模型，以及允許在包含原則（依標籤或路徑）的資料夾中建立內容片段的功能。

* 內容片段編輯器中的可用性增強，包括發佈動作以及顯示片段所依據的模型。

* 直接在內容片段編輯器中預覽JSON輸出的功能。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 可使用[!DNL Experience Manager Assets Brand Portal]來取得Assets。 這有助於從機構使用者處取得資產，用於新的行銷活動、攝影和專案。

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service]有權擁有預先設定的[!DNL Brand Portal]執行個體。 [!DNL Cloud Manager]使用者可以在[!DNL Experience Manager Assets]啟動[!DNL Brand Portal]做為[!DNL Cloud Service]。 請參閱[啟用Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html)。

* 企業現在可以使用[!DNL Brand Portal]來取得資產。 資產來源功能使用[!DNL Brand Portal]來協助客戶與機構使用者互動，以獲取資產用於新的行銷活動、攝影和專案。 請參閱 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hant)中的[資產來源。

* [!DNL Brand Portal]使用報告現在只會顯示作用中的使用者。 現在不會顯示非作用中的使用者。 作用中的使用者是指已在[!DNL Admin Console]中將其帳戶指派給產品設定檔的使用者。 檢視[[!DNL Brand Portal] 報告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)。

* 在[!DNL Brand Portal]中引進了新的下載設定，此設定可讓您在下載資料夾、集合等專案時，為每個資產建立個別資料夾。 請參閱[下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

## [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 選取多個資產以更新屬性時，有時會發生錯誤或取消選取資產的屬性會更新。 (CQ-4316532)
* 嘗試開啟[!UICONTROL Assets Admin Search邊欄]時，頁面保持空白，按一下[!UICONTROL 編輯] > [!UICONTROL 設定]會產生錯誤。 (CQ-4315079)
* 解決命名衝突後建立現有資產的新版本時，原始資產的中繼資料會被覆寫。 (CQ-4313594)
* 列印具有長註釋文字的資產時，即使有可用空間，註釋文字也會被裁剪。 (CQ-4314101)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：使用體驗片段個別豐富產品目錄頁面。

* 擴充產品主控台屬性以顯示連結的Assets和體驗片段，包括快速導覽至關聯內容的動作。

* 已發行CIF Venia參考網站 — 2021.02.24，其中包含最新CIF核心元件1.8.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)。

* 已發行CIF Core Components v1.8.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 中 Cloud Manager 的發行日期為 2021 年 2 月 11 日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets 客戶現在可以透過 Cloud Manager UI 以自助方式選擇何時何地部署其 Brand Portal 執行個體。對於具有 Assets 解決方案的一般 (非沙箱) 計畫，現在可以在生產環境中佈建 Brand Portal。佈建只能在生產環境中進行一次。

* 專案和沙箱建立中使用的 AEM Project 原型已更新至版本 25。

* 程式碼掃描期間識別的已棄用 API 清單已改進，加入最新 Cloud Service SDK 版本中棄用的其他類別和方法。

* 已更新 Cloud Manager 的 SonarQube 設定檔，以移除 Sonar 規則 squid:S2142。這將不再與執行緒中斷檢查衝突。

* Cloud Manager UI 將通知可能暫時無法新增/更新網域名稱的使用者，因為相關環境已附加執行中的管道，或目前正在等候核准步驟。

* 前置詞為 sonar 的客戶 `pom.xml` 檔案中的屬性現在會動態移除，以避免建置和品質掃描失敗。

* 如果目前部署的網域名稱正在使用 SSL 憑證，Cloud Manager UI 將通知暫時無法選擇該憑證的使用者。

* 已新增其他程式碼品質規則，以涵蓋 Cloud Service 相容性問題。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 比對 SSL 憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合 2048 位元限制，Cloud Manager UI 現在會通知使用者，並顯示適當的錯誤訊息。

* 如果目前部署的網域名稱正在使用 SSL 憑證，Cloud Manager UI 將通知暫時無法選擇該憑證的使用者。

* 在某些情況下，內部問題可能會導致環境刪除卡住。

* 某些管道故障錯誤報告為管道錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.2.4的發行日期為2021年2月10日。

### 錯誤修正 {#bug-fixes-ctt}

* 對應多個使用者時，部分使用者的IMS ID對應不正確。 此問題已修正。

### 發行日期 {#release-date-ctt-feb}

內容轉移工具v1.2.2的發行日期為2021年2月1日。

### 內容轉移工具的新增功能 {#what-is-new-ctt}

* 內容轉移工具新增功能和UI — 使用者對應工具。 此功能會在內容移轉活動過程中，自動將現有的使用者和群組對應至其AdobeIdentity Management系統ID。
如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容轉移工具現在會移轉在移轉集中參考的所有群組和使用者（包括子項）。
* 建立移轉集時，允許使用者選取`/etc`下的特定路徑。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的發行日期為2021年2月18日。

### Best Practices Analyzer新增功能 {#what-is-new-bpa}

* 能夠偵測使用AEM Forms和AEM Forms實作，並指出與移轉至AEM Formsas a Cloud Service相關的區域。
* 能夠偵測並報告自訂元件和範本的使用量和計數。
* 能夠偵測使用的節點存放區和資料存放區型別。
* 能夠偵測Dynamic Media的使用情況。
* 能夠偵測使用的Java版本。

## 程式碼重構工具 {#code-refactoring-tools}

### 程式碼重構工具的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此外掛程式的最新版本包含Repository Modernizer的多項錯誤修正。
請參閱[整合式體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html#benefits)，深入瞭解此外掛程式。

### 錯誤修正 {#bug-fixes-crt}

* 對Repository Modernizer進行的多項錯誤修正。
如需詳細資訊，請參閱[GitHub資源： aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
