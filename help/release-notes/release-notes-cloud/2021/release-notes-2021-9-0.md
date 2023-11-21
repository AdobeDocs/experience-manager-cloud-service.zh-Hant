---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版發行說明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020和2021版的發行說明。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2021.9.0)為2021年10月6日。
下列版本(2021.10.0)將於2021年11月4日發行。

## 發行影片 {#release-video}

請檢視 [2021年9月版本總覽](https://video.tv.adobe.com/v/337381) 影片以瞭解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] 發行前通道 {#sites-prerelease-features}

* 內容片段模型現在會在發佈後自動設為唯讀狀態，以避免在重新發佈已編輯的模型後無意中中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 使用者現在可以在「欄」和「卡片」檢視中排序搜尋結果內所顯示的資產。 排序功能適用於「名稱」、「已建立」、「已修改」或「無」欄。

  ![將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
  *圖：搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中。*

* 為了以程式設計方式使用資產微服務叫用處理，我們引進了新的API。 開發人員現在可以將現有的檔案夾層級處理設定檔套用至檔案夾中的一或多個特定資產。 處理設定檔會根據自訂中繼資料屬性更新而套用。 另請參閱 `AssetProcessor` 在 [[!DNL Experience Manager] API參考](https://developer.adobe.com/experience-manager/reference-materials/). 和以前一樣，您可以 [從使用者介面使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature by way of CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-sep-2021}

* **在最適化表單中使用Adobe Sign角色**  — 適用於商業和企業服務等級的Adobe Sign可讓您選擇擴充協定收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 您現在可以 [啟用每個協定收件者，以便在最適化表單中設定其角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，並將簽署者設為預設角色。

* **Analytics for Adaptive Forms**  — 您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤一般使用者行為，以收集一般使用者的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般使用者體驗。

* **輕鬆將Adobe Experience Manager (AEM) Forms連線至Microsoft®Dynamics和Salesforce**  — 此服務提供適用於Microsoft® Dynamics和Salesforce的現成資料來源設定和資料模型。 這可讓它 [開發人員更快且更輕鬆地將Microsoft®Dynamics和Salesforce設定為最適化表單的資料來源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=zh-Hant).

* **使用DocuSign在最適化表單上進行電子簽章**  — 您可以使用DocuSign在最適化表單上進行電子簽章。 此服務會提供自訂提供動作，以搭配最適化表單使用 DocuSign。您可以安裝Software Distribution上可用的套件，以匯入提交動作。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **統一的儲存聯結器**  — 使用統一的儲存聯結器可將客戶管理的存放庫中的程式內資料外部化。 例如，您可以
   * 啟用Forms入口網站的儲存並繼續功能，並將最適化表單草稿儲存在客戶管理的資料存放庫中。
   * 將包含敏感個人資料 (SPD) 的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中。

* **[!DNL AEM Forms as a Cloud Service - Communications]** - [通訊API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 協助您合併XDP範本和XML資料，以產生多種格式的列印檔案。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* AEM Sites編輯器中新的「相關商務內容」索引標籤可快速存取目前內容的相關AEM產品內容，提升作者效率

  ![關聯的商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改良產品選擇器UI，提供更佳的使用者體驗、更高的效率，並支援複雜的產品目錄

  ![新的產品挑選器](/help/assets/CIF/product-picker.png)

* 在導覽元件中遵循「include_in_menu」屬性

### 錯誤修正 {#bug-fixes-cif}

* 功能表快取排清未按預期運作

* AEM CS部署步驟期間及未使用使用者端元件時的JS錯誤

* 無法在具有sling：configs節點的資料夾中建立CIF雲端設定

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screensas a Cloud Service現在可支援基本播放監控。 播放器現在會報告每次ping （預設為30秒鐘）的各種播放量度。 根據這些量度，它可以偵測各種邊緣情況（停滯體驗、空白熒幕、排程問題等）。 此功能可讓團隊在遠端監控播放器是否正確播放內容。 它改善了對於空白熒幕或現場中斷體驗的反應性，並降低向使用者顯示中斷體驗的風險。
另請參閱 [基本播放監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 以取得更多詳細資料。

* 現在Screensas a Cloud Service支援影片的縮圖。 內容作者可以定義影片的縮圖，好讓影像可以當做預留位置使用，並正確測試內容播放和目標定位，同時由適當的團隊完成實際影片。 如果影片播放失敗，也可以使用該影像。
另請參閱 [影片的縮圖支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 以取得更多詳細資料。

### 錯誤修正 {#bug-fixes-screens}

* 播放器無法顯示內嵌頁面的內容，此問題已修正。

* 成功登入後，導覽至預設頁面（管道）最後會進入內部伺服器錯誤頁面。

* 移除播放清單時未移除關聯的標籤專案。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service] 中的新功能 {#foundation-features}

**進階網路**

>[!INFO]
>
>進階網路功能是2021.9.0版的一部分，已於2021年10月中旬為客戶啟用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在提供數種進階網路功能，包括：

* 彈性的連線埠輸出可讓流量從非標準連線埠輸出。 現在無需連絡Adobe支援即可使用。
* 專用輸出IP位址，用於輸出AEMas a Cloud Service於唯一IP的流量，現在支援所有連線埠。
* VPN可保護您的基礎架構與AEMas a Cloud Service之間的流量。

閱讀 [檔案](/help/security/configuring-advanced-networking.md) 如需詳細資訊，包括如何使用Cloud Manager API自助布建進階網路。

**索引最佳化**

為了改善搜尋查詢和索引的效能，全文檢索lucene-2不再用於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 從此發行版本。 為了根據AEM客戶在AEM環境中移除此全文檢索索引，Adobe工程團隊會與客戶個別且主動合作，以溫和且可持續的方式移除Lucene全文檢索索引。 造訪 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [檔案](/help/operations/indexing.md#index-optimizations) 如需詳細資訊，如有疑問，請直接聯絡Adobe的支援人員。

## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.9.0和2021.8.0中Cloud Manager的發行說明

## 發行日期 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 中的 Cloud Manager 發行日期是 2021 年 9 月 09 日。下一版本計畫於2021年10月7日發行。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 30。

* Cloud Manager 登陸頁面上的計畫卡片及關聯的體驗現在都已更新。

* 程式碼品質步驟記錄現在包含有關 OakPal 掃描程序的詳細記錄資訊。

* 活動頁面選單現在包含一個選項，用於在程式碼產生器執行完成後&#x200B;**下載記錄**。選取此項可下載建置步驟的記錄。

* 現在直接按一下程式卡片會瀏覽至Cloud Manager概觀頁面。

### 錯誤修正 {#bug-fixes-sept}

* 現在，當嘗試在程式中新增IP允許清單時，使用者將看到一條更易於理解的消息，該程式已達到可配置的IP允許清單的最大允許數量。

* 從存放庫畫面選擇複製URL選單選項時複製了錯誤的URL。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者在可列印的預覽中檢視BPA報告，以便進行簡易列印或列印PDF，以輕鬆共用。 請參閱中的步驟6和7 [使用Best Practices Analysis卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具v1.6.0的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 透過簡化的使用者體驗改善使用者對應，包括以下列出的功能。 如需詳細資訊，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en#using-user-mapping-tool).
   * 在執行使用者對應之前測試與使用者管理API的連線
   * 正常略過錯誤，並繼續使用者對應活動
   * 如果存取Token過期（24小時後），使用者對應不再失敗。 可以從上次停止的位置重新執行使用者對應。

* 為了提高CTT穩健性，內容可以一次擷取到製作執行個體或發佈執行個體。

* 包含版本時，路徑 `/var/audit` 會自動包含在內，以移轉稽核事件。

## 最佳做法分析工具 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的發行日期為2021年9月2日。

### 新增功能 {#what-is-new}

* 可偵測節點總數並製作報表。

* 能夠偵測並報告節點存放區型別和大小。

### 錯誤修正 {#bug-fixes-bpa}

* BPA誤判偵測到Commerce integration framework的存在。
