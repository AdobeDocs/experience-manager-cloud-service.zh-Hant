---
title: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為Cloud Service的目前發行說明。'
translation-type: tm+mt
source-git-commit: 5d3a183efcd1355c1c5dc34519fbabee34e87578
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作為{#release-notes}Cloud Service的當前發行說明

以下章節概述[!DNL Experience Manager]目前（最新）版本的一般發行說明，做為Cloud Service。

>[!NOTE]
>您可從此處瀏覽至舊版的發行說明；例如2020年、2021年等。

>[!NOTE]
>
>如需與發行版本無直接關聯的檔案更新詳細資訊，請參閱[最新檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2021.2.0的發行日期為2021年2月25日。
下列版本(2021.3.0)將於2021年3月25日發行。

## [!DNL Adobe Experience Manager Sites] Cloud Service  {#sites}

* **[RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)**:新增支援在使用中檢視和編SPA輯外AEM部。

* **[在中編SPA輯外AEM部](/help/implementing/developing/hybrid/editing-external-spa.md)**:新增將獨立單頁應用程式上傳至例項、新增可編AEM輯的內容區段，以及啟用編寫功能的能力。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] {#what-is-new-assets}的新增功能

* [!DNL Experience Manager Assets] as  [!DNL Cloud Service] a有權擁有預先配置的實 [!DNL Brand Portal] 例。[!DNL Cloud Manager]使用者可以在[!DNL Experience Manager Assets]上啟動[!DNL Brand Portal]作為[!DNL Cloud Service]。 請參閱[啟用品牌入口網站](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en)。

* 企業現在可以使用[!DNL Brand Portal]來源資產。 資產來源搜尋功能運用[!DNL Brand Portal]，協助客戶與代理商使用者互動，為新的行銷宣傳、攝影和專案搜尋資產。 請參閱 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)中的[資產來源補充。

* [!DNL Brand Portal]使用狀況報表現在只會顯示作用中的使用者。 現在不會顯示非作用中的使用者。 作用中使用者是指其帳戶已指派至[!DNL Admin Console]中產品描述檔的使用者。 請參閱[[!DNL Brand Portal] reports](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)。

* 在[!DNL Brand Portal]中，會引入新的下載設定，可讓您在下載檔案夾、系列等時，為每個資產建立個別的檔案夾。 請參閱[下載設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

## [!DNL Assets] {#bug-fixes-assets}中的錯誤修正

* 在解決命名衝突後建立新版本的現有資產時，會覆寫原始資產的中繼資料。 (CQ-4313594)
* 當打印具有長注釋文本的資產時，即使有空格，注釋文本也會被修剪。 (CQ-4314101)
* 當選取多個資產以更新屬性時，有時候會發生錯誤，或未選取資產的屬性會更新。 (CQ-4316532)
* 當嘗試開啟[!UICONTROL 資產管理搜尋邊欄]時，頁面仍為空白，按一下[!UICONTROL 編輯] > [!UICONTROL 設定]會產生錯誤。 (CQ-4315079)

## Adobe Experience Manager商務Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品體驗管理：使用體驗片段讓產品目錄頁面更加豐富。

* 延伸產品主控台屬性以顯示連結的資產和體驗片段，包括快速導覽至相關內容的動作。

* 發佈的CIF Venia參考網站- 2021.02.24，其中包含最新的CIF核心元件1.8.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)。

* 已發佈CIF核心元件v1.8.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)。

## Cloud Manager {#cloud-manager}

本節將Cloud Manager發行說明概AEM述為Cloud Service2021.3.0。

## 發行日期 {#release-date-cm-march}

Cloud Manager作為2021.3.0Cloud ServiceAEM的發行日期為2021年3月11日。
下一版預計於2021年4月08日推出。


### 新功能 {#what-is-new-march}

* 具有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自訂域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂域名配置的環境的客戶將看到有關其先前現有配置的消息，並能夠通過UI自助服務。

* 具備必要權限的使用者現在可以編輯程式，讓他們以自助方式進行下列作業：

   * 將Sites解決方案新增至包含資產的現有計畫，反之亦然。
   * 將網站或資產從既有的計畫中移除，同時包含網站和資產。
   * 將第二個未使用的解決方案權益新增至現有的方案，或新增為新的方案。

* **現AEM在，「Pipeline  Execution」（管線執行）和「Activity」（活動）畫面都會** 顯 *示推播更新*  ** 標籤。

* 如果環境已休眠，但也有可用的更AEM新，則&#x200B;**已休眠**&#x200B;狀態將優先於&#x200B;**可用更新**。

* 現在，在導覽至Unified Shell的「使用者設定檔」圖示（右上角）後，使用者可以選取「檢視雲端管理員角色」選項，以查看其Cloud Manager角色。

* **申請批准**&#x200B;標籤已重新標籤至&#x200B;**生產批准**，以更清楚明瞭。

* **版本**&#x200B;標籤已重新標籤至「生產管線」執行畫面中的&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標籤，以反映其真實行為：**取消立即**&#x200B;和&#x200B;**批准立即**。

* 類別和方法取代清單已根據Cloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版AEM本更新。

* Cloud Manager生產管道現在將包含[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正 {#bug-fixes-cm-march}

* 在推播升級期間，在某些情況下會略過套AEM件版本。

* 在將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能是現有程式名稱的副本。

* 有時，如果用戶在啟動管線後立即導航離開管線執行頁面，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行開始。

* 當客戶建置導致無效包時，不必要地重新啟動建置步驟。

* 有時，即使未部署IP允許清單，用戶也會看到該配置旁邊的綠色「活動」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。


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

內容傳輸工具v1.3.4的發行日期為2021年3月19日。

### 錯誤修正 {#bug-fixes-ctt}

* CTT正在跳過同名但名稱中帶有連字型大小的資料夾中的內容。 這個問題已經修正。


### 發行日期 {#release-date-ctt-march}

內容傳輸工具v1.3.0的發行日期為2021年3月04日。

### 內容傳輸工具{#what-is-new-ctt-march}的新增功能

* CTT現在會安裝至`/apps`，而非`/libs`特定頁面的瀏覽器書籤可能不再有效。
* 當安裝CTT時，使用者將必須導覽其他層級，才能進入「內容傳輸」頁面。 如需詳細資訊，請參閱[使用內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)。

### 錯誤修正 {#bug-fixes-ctt-march}

* 從特定路徑移轉內容時，CTT會提取不相關的資源。 此問題已修正


### 發行日期 {#release-date-ctt-feb}

內容傳輸工具v1.2.4的發行日期為2021年2月10日。

### 錯誤修正 {#bug-fixes-ctt-feb}

* 對應多個使用者時，有些使用者的IMS ID映射不正確。 這個問題已經修正。

### 發行日期 {#release-date-ctt-feb01}

內容傳輸工具v1.2.2的發行日期為2021年2月1日。

### 內容傳輸工具{#what-is-new-ctt}的新增功能

* 內容傳輸工具——使用者對應工具新增功能和UI。 此功能會自動將現有的使用者和群組對應至其Adobe的Identity Management系統ID，做為內容移轉活動的一部分。
如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容傳輸工具現在會移轉移移集（包括子系）中參考的所有群組和使用者。
* 在建立遷移集時，允許用戶選擇`/etc`下的某些路徑。

## 最佳做法分析器{#best-practices-analyzer}

### 發行日期 {#release-date-bpa-march}

Best Practices Analyzer v2.1.8的發行日期為2021年3月22日。

### Best Practices Analyzer {#what-is-new-bpa-march}的新增功能

* 能夠從UI中的BPA報告以及導出為CSV檔案的報告中過濾掉ACS公域查找結果。

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

* 新版AIO-CLI增效模組已發行。 此插件的最新版本包含Repository Modernizer和Dispatcher Converter的幾項新功能和錯誤修正。    請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以進一步瞭解此外掛程式。

* Repository Modernizer的新功能和增強功能。 請參閱[GitHub資源：最新版本的Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 將OSGi組態標準化為偏好的。cfg.json格式（RepoInit組態除外）。
   * 將OSGi配置資料夾更名為指定格式。
   * 產生ui.apps.structure專案。
   * 建立分析模組。

* Dispatcher Converter的新功能和增強功能。 請參閱[GitHub資源：Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 為不同內含項目建立個別檔案，而非內容內嵌。
   * 能夠同時處理vhosts的資料夾路徑和vhost檔案的路徑。
   * 以超過600種客戶配置生成群檔案。

## [!DNL Adobe Experience Manager] 作為Cloud Service基金會  {#aem-as-a-cloud-service-foundation}

### 已知問題 {#known-issues-foundation}

**由於Build Analyzer外掛程式發生問題，部分建置可能會失敗**

在某些情況下，項目構建版本在執行`aemanalyser-maven-plugin`時可能失敗，並顯示以下錯誤消息：

```
[ERROR] repoinit: Parsing error in repoinit from extension : Encountered "" at line 15, column 37.
 
Was expecting one of:
 
     
 
[ERROR] Analyser detected errors on feature
```

**解決方法**

要解決此問題，請在父`pom.xml`檔案中選擇`aemanalyser-maven-plugin`的最新版本：

```xml
<aemanalyser.version>0.9.2</aemanalyser.version>
```

