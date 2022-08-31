---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版發行說明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 24%

---

# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 當前版本(2021.9.0)為2021年10月6日。
以下版本(2021.10.0)是2021年11月4日。

## 發佈視頻 {#release-video}

看看 [2021年9月發佈概述](https://video.tv.adobe.com/v/337381) 視頻，瞭解添加的功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] 預釋放通道 {#sites-prerelease-features}

* 內容片段模型在發佈後將自動設定為只讀狀態，以避免在重新發佈已編輯的模型後無意中中斷即時API查詢。 嘗試編輯已發佈模型時，系統會提示用戶出現警告。 接受警告後可進行編輯。

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 用戶現在可以對搜索結果中顯示的「列」和「卡」視圖中的資產進行排序。 排序在「名稱」(Name)、「已建立」(Created)、「已修改」(Modified)或「無」(None)列上工作。

   ![對搜索結果排序 [!DNL Assets] 列和卡視圖中](/help/assets/assets/sort-searched-assets.png)
   *圖：對搜索結果排序 [!DNL Assets] 的子菜單。*

* 為了用資產微服務寫程式調用處理，引入了新的API。 開發人員現在可以將現有資料夾級處理配置檔案應用於資料夾中的一個或多個特定資產。 基於自定義元資料屬性更新應用處理配置檔案。 請參閱 `AssetProcessor` 的 [[!DNL Experience Manager] API引用](https://www.adobe.io/experience-manager/reference-materials/)。 和以前一樣， [從用戶介面使用asset microservices](/help/assets/asset-microservices-configure-and-use.md)。

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms-sep-2021}

* **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。您現在可以[啟用每個協議收件者，以便在最適化表單中設定其角色](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，並將簽署者設定為預設角色。

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

* **輕鬆地將 AEM Forms 連線到 Microsoft Dynamics 和 Salesforce**：此服務會提供 Microsoft Dynamics 和 Salesforce 適用的資料模型，好讓[開發人員更快且更輕鬆地將 Microsoft Dynamics 和 Salesforce 設定為最適化表單的資料來源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)。

* **使用 DocuSign 在最適化表單上進行電子簽名：** 您可以使用 DocuSign 在最適化表單上進行電子簽名。此服務會提供自訂提供動作，以搭配最適化表單使用 DocuSign。您可以安裝軟體分發上可用的軟體包以導入提交操作。

### [!DNL Forms]的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **統一的儲存連接器：**&#x200B;使用統一的儲存連接器可將客戶管理的存放庫中的程序內資料外部化。 例如，您可以
   * 啟用 Forms Portal 的儲存並繼續功能，並將最適化表單草稿儲存在客戶管理的資料存放庫中。
   * 將包含敏感個人資料 (SPD) 的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中。

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   * 使用 XML 資料填寫範本檔案來產生文件。
   * 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   * 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 「站點」編輯器中新的「關聯商業內容」頁籤通過快速訪問當前上下文的AEM相關產品內容而提高了作者效率

   ![關聯的商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改進了產品選取器UI，以獲得更好的用戶體驗、提高效率和支援複雜產品目錄

   ![新產品選取器](/help/assets/CIF/product-picker.png)

* 在導航元件中尊重&quot;include_in_menu&quot;屬性

### 錯誤修正 {#bug-fixes-cif}

* 菜單快取刷新未按預期工作

* CS部署步驟AEM和不使用客戶端元件時的JS錯誤

* 無法在具有sling:configs節點的資料夾中建立CIF雲配置

## [!DNL Experience Manager Screens] 作為 [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* 螢幕as a Cloud Service現在支援基本的回放監視。 播放器現在將報告各種播放度量（預設為30秒）。 基於這些指標，它提供了檢測各種邊緣情況（停滯體驗、空白螢幕、調度問題等）的能力。 此功能允許團隊遠程監視玩家是否正確播放內容，提高對空白螢幕或現場中的中斷體驗的反應性，並降低向最終用戶顯示中斷體驗的風險。
請參閱 [基本播放監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 的子菜單。

* 螢幕as a Cloud Service中現在支援的視頻縮略圖支援。 內容作者可以定義視頻的縮略圖，以便影像可以用作佔位符並正確地test內容回放和目標，同時由適當的團隊最終確定實際視頻。 在視頻回放失敗時，也可以使用影像。
請參閱 [視頻縮略圖支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 的子菜單。

### 錯誤修正 {#bug-fixes-screens}

* Player無法顯示嵌入頁面的內容，此問題現已解決。

* 成功登錄後，導航到預設頁（通道）後，將出現在「內部伺服器錯誤」頁。

* 刪除播放清單時未刪除關聯的標籤項。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 中的新功能 [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**高級網路**

>[!INFO]
>
>高級網路功能是2021.9.0版的一部分，將在10月中旬為客戶啟用。

[!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 現在提供多種類型的高級網路功能，包括：

* 靈活的埠出口，以將流量從非標準埠中排出。 現在可以不聯繫Adobe支援。
* 專用出口IP地址，用於將通信從與AEM唯一IPas a Cloud Service的出口，現在支援所有埠。
* VPN以保護基礎架構和AEMas a Cloud Service之間的通信。

閱讀 [文檔](/help/security/configuring-advanced-networking.md) 詳細資訊，包括如何使用Cloud Manager API自助配置高級網路。

**索引優化**

為了提高搜索查詢和索引的效能，在中不再使用全文索引lucene-2 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 從這個版本。 為了根據客戶刪除有關環境的AEM全文索引AEM,Adobe工程部門單獨和主動地與客戶合作，以溫和、可持續地刪除Lucene全文索引。 請訪問 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] [文檔](/help/operations/indexing.md#index-optimizations) 如有任何疑問，請直接聯繫我們的支援人員。

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service和中的Cloud ManagerAEM的2021.9.0行說2021.8.0。

## 發行日期 {#release-date-cm-sept}

Cloud Manager在as a Cloud Service中的發AEM布日期為2021年9月9日。
下一版計畫於2021年10月7日發行。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager使用的AEM項目原型版本已更新為版本30。

* 已刷新Cloud Manager登錄頁上的程式卡和相關體驗。

* 代碼質量步驟日誌現在包含有關OakPal掃描過程的詳細記錄資訊。

* 「活動」頁菜單選項現在將包含一個選項 **下載日誌** 完成的代碼生成器執行。 選擇此項將下載生成步驟的日誌。

* 直接按一下程式卡將立即導航至Cloud Manager概述頁。

### 錯誤修正 {#bug-fixes-sept}

* 當嘗試在程式中添加新的IP允許清單時，用戶現在將看到一條更易理解的消息，該程式已達到可配置的最大允許IP允許清單數。

* 從「資料庫」螢幕選擇複製URL菜單選項時複製了錯誤的URL。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發佈日期為2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在允許用戶在可打印預覽中查看BPA報告，從而允許簡單打印或打印到PDF，以便於共用。 請參閱中的步驟6和7 [使用最佳做法分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis)。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容傳輸工具v1.6.0的發佈日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 通過簡化的用戶體驗改進了用戶映射，包括下面列出的以下功能。 有關詳細資訊，請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool)。
   * Test到用戶管理API的連接，然後運行用戶映射
   * 順利跳過錯誤並繼續「用戶映射」活動
   * 如果訪問令牌過期（24小時後），用戶映射不再失敗。 可以從上次停止的位置重新運行用戶映射。

* 為了增強CTT的健壯性，可以一次將內容攝取到Author實例或Publish實例。

* 包含版本時，路徑 `/var/audit` 自動包含以遷移審核事件。

## 最佳做法分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

最佳做法分析器2.1.18版的發佈日期為2021年9月2日。

### 新增功能 {#what-is-new}

* 能夠檢測並報告節點總數。

* 能夠檢測並報告節點儲存類型和大小。

### 錯誤修正 {#bug-fixes-bpa}

* BPA錯誤地檢測了Commerce Integration Framework的存在。
