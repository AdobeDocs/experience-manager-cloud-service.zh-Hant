---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2021.2.0發行說明。」'
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.2.0是2021年2月25日。
以下版本(2021.3.0)將於2021年3月25日發佈。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### 無頭內容管理 {#headless}

* **[用於內容片段傳遞的GraphQL API](/help/headless/graphql-api/content-fragments.md)**:能夠使用GraphQL語法和基於內容片段模型的架構查詢內容片段，以便以JSON格式輸出。

* **[GraphQL API請求的身份驗證支援](/help/headless/security/authentication.md)**:能夠使用伺服器端API的訪問令牌驗證GraphQL API請求。

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**:添加了對使用中查看和編SPA輯外部AEM的支援。

* **[編輯SPA外部AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**:增加了將獨立單頁應用程式上載到實AEM例、添加可編輯內容部分並啟用創作的功能。

* GraphQL API的增強JSON輸出，包括以JSON格式和區域設定輸出富格文本的能力。

* 支援嵌套內容片段模型，以允許通過多行文本欄位中的專用內容片段引用資料類型或內容片段引用內聯建立嵌套的內容片段結構。

* 內容片段模型資料類型中提供的其他驗證規則，包括「唯一」、「必需」和「可翻譯」。

* 功能標籤內容片段模型，並允許在資料夾中按標籤或路徑建立包含策略的內容片段。

* 內容片段編輯器中的可用性增強功能，包括發佈操作和片段所基於模型的顯示。

* 能夠直接在內容片段編輯器中預覽JSON輸出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets]的新增功能 {#what-is-new-assets}

* 資產可使用 [!DNL Experience Manager Assets Brand Portal]。 它有助於為新的營銷活動、照片和項目從代理用戶處獲取資產。

* [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] 有權預先配置 [!DNL Brand Portal] 實例。 的 [!DNL Cloud Manager] 用戶可激活 [!DNL Brand Portal] 上 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service]。 請參閱 [激活Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant)。

* 企業現在可以使用 [!DNL Brand Portal]。 資產來源補充功能利用 [!DNL Brand Portal] 幫助客戶與代理用戶接觸，為新的營銷活動、照片和項目尋找資產。 請參閱 [資產來源補充 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)。

* 的 [!DNL Brand Portal] 「 usage 」報告現在只顯示活動用戶。 此時不顯示非活動用戶。 活動用戶是指其帳戶已分配給產品配置檔案的用戶 [!DNL Admin Console]。 請參閱 [[!DNL Brand Portal] 報告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)。

* 在 [!DNL Brand Portal]，將引入新的下載設定，使您可以在下載資料夾、集合等時為每個資產建立單獨的資料夾。 請參閱 [下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

## [!DNL Assets]中的錯誤修正 {#bug-fixes-assets}

* 當選擇多個資產來更新屬性時，有時會發生錯誤或更新取消選定資產的屬性。 (CQ-4316532)
* 嘗試開啟時 [!UICONTROL 資產管理搜索欄]，頁面仍為空，然後按一下 [!UICONTROL 編輯] > [!UICONTROL 設定] 生成錯誤。 (CQ-4315079)
* 在解決命名衝突後建立現有資產的新版本時，將覆蓋原始資產的元資料。 (CQ-4313594)
* 當打印具有長注釋文本的資產時，即使空間可用，也會修剪注釋文本。 (CQ-4314101)

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：使用經驗片段單獨豐富產品目錄頁。

* 擴展產品控制台屬性，用於顯示連結的資產和體驗片段，包括快速導航到相關內容的操作。

* 已發佈CIF Venia參考站點 — 2021.02.24，包括最新的CIF核心元件版本v1.8.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) 的子菜單。

* 已發佈CIF核心元件v1.8.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) 的子菜單。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* 資產客戶現在可以通過Cloud Manager UI選擇何時以自助服務方式部署其Brand Portal實例以及在何處部署。 對於具有資產解決方案的常規（非沙箱）計畫，現在可以在生產環境中配置Brand Portal。 在生產環境上只能進行一次設定。

* 在項AEM目和沙盒建立中使用的項目原型已更新為版本25。

* 代碼掃描期間識別的已過時API清單已細化，以包括最新Cloud ServiceSDK版本中已棄用的其他類和方法。

* SonarQube雲管理器的配置檔案已更新，以刪除Sonar規則squid:S2142。 這將不再與線程中斷檢查衝突。

* Cloud Manager UI將通知暫時無法添加/更新域名的用戶，因為關聯環境有一個正在運行的管道附加到它，或者當前正在等待批准步驟。

* 客戶中設定的屬性 `pom.xml` 現在將動態刪除以聲納為前置詞的檔案，以避免生成和質量掃描失敗。

* 如果SSL證書正由當前正在部署的域名使用，Cloud Manager UI將通知暫時無法選擇該證書的用戶。

* 已添加其他代碼質量規則以涵蓋Cloud Service相容性問題。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 與域名匹配的SSL證書不再區分大小寫。

* 如果證書私鑰不滿足2048位限制，Cloud Manager UI將立即通知用戶，並顯示相應的錯誤消息。

* 如果SSL證書正由當前正在部署的域名使用，Cloud Manager UI將通知暫時無法選擇該證書的用戶。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管道故障錯誤地報告為管道錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.4的發佈日期為2021年2月10日。

### 錯誤修正 {#bug-fixes-ctt}

* 映射多個用戶時，某些用戶的IMS ID映射不正確。 這個已經修復了。

### 發行日期 {#release-date-ctt-feb}

內容傳輸工具v1.2.2的發佈日期為2021年2月1日。

### 內容傳輸工具中的新增功能 {#what-is-new-ctt}

* 新功能和UI已添加到內容傳輸工具 — 用戶映射工具。 此功能會自動將現有用戶和組映射到其AdobeIdentity Management系統ID，作為內容遷移活動的一部分。
請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 的子菜單。
* 內容傳輸工具現在可以遷移遷移集中引用的所有組和用戶，包括子代。
* 允許用戶在 `/etc` 建立遷移集時。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.2版的發佈日期為2021年2月18日。

### 最佳做法分析器中的新增功能 {#what-is-new-bpa}

* 能夠發現AEM Forms和AEM Forms執行情況的使用情況，並指出與遷往AEM Formsas a Cloud Service有關的領域。
* 能夠檢測並報告自定義元件和模板的使用情況和計數。
* 能夠檢測所使用的節點儲存和資料儲存的類型。
* 檢測Dynamic Media的使用。
* 能夠檢測使用的Java版本。

## 程式碼重構工具 {#code-refactoring-tools}

### 代碼重構工具中的新增功能 {#what-is-new-crt}

* 已發佈新版本的AIO-CLI插件。 此插件的最新版本包括儲存庫現代化器的幾個錯誤修復程式。
請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 瞭解有關此插件的詳細資訊。

### 錯誤修正 {#bug-fixes-crt}

* 在Repository Modernizer上完成了幾個錯誤修復。
請參閱 [GitHub資源：aem雲服務源遷移](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 的子菜單。
