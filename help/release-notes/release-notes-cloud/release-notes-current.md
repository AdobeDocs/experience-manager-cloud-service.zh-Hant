---
title: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
translation-type: tm+mt
source-git-commit: d20a729712c1dbd48150f813419b57c49074b492
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]做為雲端服務的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service 2021.1.0的發行日期為2021年2月3日。
下列版本(2021.2.0)將於2021年2月25日發行。

## [!DNL Adobe Experience Manager Sites] 雲端服務  {#sites}

### 無頭內容管理{#headless}

* **[內容片段傳送的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能夠使用GraphQL語法查詢內容片段，並根據內容片段模型來結構，以便以JSON格式輸出。

* **[GraphQL API請求的驗證支援](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能夠使用伺服器端API的存取Token來驗證GraphQL API請求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**:新增支援使用在AEM中檢視和編輯外部SPA。

* **[在AEM中編輯外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**:新增將獨立單頁應用程式上傳至AEM例項、新增可編輯的內容區段，以及啟用編寫功能的能力。

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

* [!DNL Experience Manager] 延伸「 [!DNL Cloud Service] 智慧標籤」功能，以支援在文字型資產中識別關鍵字和實體。文字會被識別、建立索引，並可做為中繼資料使用，以改善搜尋體驗，而不需進行任何設定。 請參閱[智慧型標籤](/help/assets/smart-tags.md)。

* 現在支援MXF檔案格式。 請參閱[支援的檔案格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：資產和體驗片段的新「商務」屬性標籤。 此標籤可讓您將產品／類別連結至資產和體驗片段。 此標籤也會顯示連結產品／類別的即時資料，以及在產品主控台中顯示詳細資料的連結。

* 發佈的CIF Venia參考網站- 2021.02.02，其中包含最新的CIF核心元件1.7.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* 已發佈CIF核心元件v1.7.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM中Cloud Manager作為Cloud Service 2021.2.0的發行日期為2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}

* Cloud Manager生產管道現在將包含自訂UI測試功能。

* 資產客戶現在可以選擇透過Cloud Manager UI以自助方式部署其品牌入口網站實例的時間和地點。 對於具有資產解決方案的一般（非沙盒）方案，現在可在生產環境中布建品牌入口網站。 在生產環境上只能執行一次置備。

* 「專案與沙盒建立」中使用的AEM專案原型已更新為版本25。

* 程式碼掃描期間識別的已過時API清單已改良，加入最新Cloud Service SDK版本中已淘汰的其他類別和方法。

* SonarQube的Cloud Manager描述檔已更新，以移除Sonar規則squid:S2142。 這將不再與「線程中斷檢查」衝突。

* Cloud Manager UI會通知暫時無法新增／更新網域名稱的使用者，因為相關環境會附加一個執行中的管道，或目前正在等待核准步驟。

* 現在，客戶`pom.xml`檔案中預先設定的Sonar屬性將會動態移除，以避免建置和品質掃描失敗。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者並顯示適當的錯誤訊息。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管線故障錯誤報告為管線錯誤。

## AEM as a Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 伺服器對伺服器的驗證API呼叫——產生適當的存取Token，以便在您的外部應用程式與AEM之間，以雲端服務環境的形式進行驗證的伺服器對伺服器API呼叫。 閱讀[說明檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或參閱[教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)，瞭解更多資訊。

### SDK Build Analyzers {#sdk-build-analyzers}

AEM as a Cloud Service SDK Build Analyzer Maven Plugin會偵測主要專案中的問題，包括缺少相依性。 它為開發人員提供了在本機開發期間發現問題的機會，而遠在使用Cloud Manager部署至雲端環境之前。

此版本新增了兩個分析器：

* 重點分析器
* bundle-nativecode

如需詳細資訊，請參閱說明檔案[這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.2的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}的新增功能

* 內容傳輸工具——使用者對應工具新增功能和UI。 這項功能會自動將現有的使用者和群組對應至其Adobe Identity Management System ID，做為內容移轉活動的一部分。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容傳輸工具現在會移轉移移集（包括子系）中參考的所有群組和使用者。
* 在建立遷移集時，允許用戶選擇`/etc`下的某些路徑。
