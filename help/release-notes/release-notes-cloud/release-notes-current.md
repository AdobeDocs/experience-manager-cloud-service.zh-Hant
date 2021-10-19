---
title: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 540e380b01629cb17aae9b993e871e3496a2e86b
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 2%

---


# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2021.9.0)為2021年10月6日。
下列版本(2021.10.0)將於2021年10月27日發行。

## 發行影片 {#release-video}

查看 [2021年9月發行概述](https://video.tv.adobe.com/v/337381) 視訊，以取得新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] 預發行管道 {#sites-prerelease-features}

* 內容片段模型現在會在發佈後自動設為唯讀狀態，以避免重新發佈已編輯的模型後，無意中中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 現在支援使用Adobe Document Cloud的原生注釋和注釋工具來註解PDF檔案。 直接在檔案預覽視窗中新增文字、醒目提示、註解和繪圖，為PDF內容加上注釋。 使用者也可以按一下特定留言，跳至PDF中感興趣的頁面

* 使用者現在可以在「欄」和「卡片」檢視中，對搜尋結果中顯示的資產進行排序。 排序適用於「名稱」、「已建立」、「已修改」或「無」欄。

   ![在中排序搜尋結果 [!DNL Assets] 欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
   *圖：在中排序搜尋結果 [!DNL Assets] 欄和卡片檢視。*

### 中的新功能 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

* [!DNL Assets] 現在包含的內建連接器 [!DNL Azure Media Services] 用於音頻和視頻轉錄。 配置後，將自動轉錄支援的檔案並生成WebVTT檔案。 WebVTT字幕用於更有效的搜索、字幕或翻譯，以用作字幕。

<!-- TBD: 'Unpublishing' this feature as suggested by engineering.

* To programmatically invoke processing using asset microservices, a new API is introduced. Developers can now apply an existing folder-level processing profile on one or more specific assets in a folder. The processing profile gets applied based on custom metadata properties updates. See `AssetProcessor` in the [[!DNL Experience Manager] API reference](https://www.adobe.io/experience-manager/reference-materials/). As before, it is possible to [use asset microservices from the user interface](/help/assets/asset-microservices-configure-and-use.md).

-->
<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep prerelease channel.
A/V transcription feature via CQ-4303854 has moved to Oct prerelease now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 新增功能 [!DNL Forms] {#what-is-new-forms-sep-2021}

* **在適用性表單中使用Adobe Sign角色**:Adobe Sign（適用於業務和企業服務層級）可以選擇除簽署者外，擴展協定收件者的角色，以更符合其工作流程需求。 您現在可以 [讓每個合約收件者都能在適用性表單中設定其角色](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，預設角色為簽署者。

* **適用性Forms**:您現在可以擷取 [透過Adobe Analytics追蹤一般使用者行為](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-aem-forms-with-adobe-analytics.html) 以收集一般使用者分析。 它有助於根據資料做出明智的決策，以改善一般使用者體驗。

* **輕鬆連接AEM Forms與Microsoft Dynamics和Salesforce**:此服務提供Microsoft Dynamics和Salesforce的現成可用資料來源設定和資料模型，讓 [開發人員可更快更輕鬆地將Microsoft Dynamics和Salesforce設定為最適化表單的資料來源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **使用DocuSign對最適化表單進行電子簽署：** [您可以使用DocuSign對最適化表單進行電子簽署](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-docusign-adaptive-forms.html). 此服務提供自訂提交動作，以搭配最適化表單使用DocuSign。

### 測試版功能 [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **統一儲存連接器：** 使用Unified Storage Connector將客戶管理的儲存庫中的處理中資料外部化。 例如，您可以將包含敏感個人資料(SPD)的處理中AEM工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) 幫助您結合XDP模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   * 使用XML資料填入範本檔案，以產生檔案。
   * 以各種格式生成輸出表單，包括非互動式PDF打印流。
   * 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* Sites編輯器中新的「關聯商務內容」索引標籤可快速存取目前內容的相關AEM產品內容，進而提高作者效率

   ![關聯商務內容](/help/assets/CIF/associated-commerce-content.png)

* 改善產品選擇器UI，提供更佳的使用者體驗、更高的效率，以及對複雜產品目錄的支援

   ![新產品選擇器](/help/assets/CIF/product-picker.png)

* 在導航元件中遵循「include_in_menu」屬性

### 錯誤修正 {#bug-fixes-cif}

* 菜單快取刷新未如預期工作

* AEM CS部署步驟期間和不使用clientside元件時的JS錯誤

* 無法在具有sling:configs節點的資料夾中建立CIF雲端設定

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screens as a Cloud Service現在支援基本播放監控。 播放器現在會報告各種播放量度，每次偵測（預設為30秒）。 它可根據量度偵測各種邊緣案例（停滯體驗、空白畫面、排程問題等）。 此功能可讓團隊遠端監視播放器是否正確播放內容、改善對空白畫面或欄位中中斷體驗的再活動，並降低向使用者顯示中斷體驗的風險。
請參閱 [基本播放監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 以取得更多詳細資訊。

* Screens as a Cloud Service現在支援的視訊縮圖支援。 內容作者可以定義視訊的縮圖，以便影像可作為預留位置，並在適當團隊完成實際視訊時，正確測試內容播放和鎖定目標。 當視訊播放失敗時，也可以使用影像。
請參閱 [影片的縮圖支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes-screens}

* 播放器無法顯示內嵌頁面的內容，此問題現已修正。

* 成功登入後，導覽至預設頁面（管道）最後會顯示「內部伺服器錯誤」頁面。

* 移除播放清單時，未移除相關的標籤項目。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 中的新功能 [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**高級網路**

>[!INFO]
>
>進階網路功能是2021.9.0版的一部分，將於10月中旬為客戶啟用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在提供多種類型的進階網路功能，包括：

* 靈活的埠輸出，以將流量從非標準埠導出。 現在無需聯絡Adobe支援即可。
* 專用的輸出IP位址，可從唯一IP將流量從AEMas a Cloud Service中輸出，現在支援所有埠。
* VPN以保護基礎架構與AEMas a Cloud Service之間的流量。

閱讀 [檔案](/help/security/configuring-advanced-networking.md) 如需詳細資訊，包括如何使用Cloud Manager API自助服務布建進階網路。

**索引最佳化**

為了改善搜尋查詢和索引的效能，全文索引lucene-2不再包含於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 從此版本。 為了根據AEM客戶在AEM環境上移除此全文索引，Adobe工程部會與客戶個別且主動地合作，以緩慢且持續地移除Lucene全文索引。 請造訪 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [檔案](/help/operations/indexing.md#index-optimizations) 如需詳細資訊，如有任何疑問，請直接聯絡我們的支援。

## Cloud Manager {#cloud-manager}

本節概述AEM as a Cloud Service 2021.10.0和2021.9.0中Cloud Manager的發行說明。

## 發行日期 {#release-date-cm-oct}

AEMas a Cloud Service的Cloud Manager發行日期為2021.10.0年10月14日。
下一版預計於2021年11月4日發行。

### 新增功能 {#what-is-new-cm-oct}

* 為準備日後的一些變更，現在會在使用者介面中參照現有的部署管道，並將其標示為 **完整堆棧** 管道。

* 管道卡已重新整理，現在會顯示顯示生產管道和非生產管道的單一整合面板，且使用者可從與每個管道相關聯的動作功能表中直接選取「執行/暫停/繼續」。

* 部署管理員角色中的使用者現在可以透過UI以自助方式刪除生產管道。

* 新增和編輯管道體驗已重新整理，現在可使用熟悉的現代模組。

* Cloud Manager的使用者現在可以透過 **意見反應** 按鈕。

* 每年的SLA圖表現在可以從Cloud Manager的使用者介面下載。

* 程式碼品質和非生產管道執行現在會在建置步驟期間使用更有效率的淺層復製程式，為擁有特別大型Git存放庫的客戶提供更快的建置時間。

* 「新增IP允許清單」精靈現在會通知使用者已達到允許的IP允許清單數目上限。

* Cloud Manager API檔案現在包含互動式操作場，可讓登入的使用者透過瀏覽器試驗API。 請參閱 [Cloud Manager API遊樂場](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以取得更多詳細資訊。

* 如果禁用「導航到」下的選擇選項，則「程式」卡上的工具提示將更具描述性。 現在會顯示「生產環境不存在」。

## 發行日期 {#release-date-cm-sept}

AEM 2021.9.0中的Cloud Manageras a Cloud Service日期為2021年9月9日。

### 錯誤修正 {#bug-fixes-cm-oct}

* 在極少數情況下，當Adobe員工恢復客戶的環境時，在環境完全運行之前，會將恢復視為已完成。

* 環境建立期間提出的某些內部請求未重試。

* 如果在域名驗證後發生部署失敗錯誤，則錯誤消息已更正，以請客戶聯繫其Adobe代表。


### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager使用的AEM專案原型版本已更新為30版。

* Cloud Manager登陸頁面上的方案卡片和相關聯的體驗已重新整理。

* 程式碼品質步驟記錄現在包含OakPal掃描程式的詳細記錄資訊。

* 「活動」頁面功能表選項現在包含 **下載記錄檔** 完成的代碼生成器執行。 選取此選項將下載建置步驟的記錄檔。

* 直接按一下「方案」卡片，現在會導覽至「Cloud Manager概觀」頁面。

### 錯誤修正 {#bug-fixes-sept}

* 在程式中新增IP允許清單時，使用者現在會看到更容易理解的訊息，此程式已達到可設定的IP允許清單允許數量上限。

* 從「儲存庫」螢幕選擇「複製URL」菜單選項時，複製了錯誤的URL。

## Cloud Acceleration Manager {#cam}

### 發行日期 {#release-date-october-cam}

Cloud Acceleration Manager的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在讓使用者能以可列印的預覽方式檢視BPA報表，輕鬆列印或列印至PDF，以方便共用。 請參閱 [使用最佳實務分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.6.0版的發行日期為2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 透過簡化的使用者體驗改善使用者對應工具，包括下列功能。 如需詳細資訊，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * 在執行使用者對應之前，測試與使用者管理API的連線
   * 適度略過錯誤，並繼續進行「使用者對應」活動
   * 若 **存取權杖** 24小時後過期。 可以從上次停止的位置重新運行用戶映射。

* 若要提高「內容轉移工具」的健全性，一次可將內容擷取至「製作」例項或「發佈」例項。 請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 以取得更多詳細資訊。

* 包含版本時，路徑 `/var/audit` 會自動納入，以移轉稽核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 偵測及報告節點名稱長度的功能。

* 能夠偵測並報告總索引大小。

* 能夠偵測遺失原始轉譯的資產並製作報表。

