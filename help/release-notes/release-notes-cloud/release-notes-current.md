---
title: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 作為Cloud Service的最新發行說明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 49e88e18e17a2675151a11339a01b3ea7b71d555
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作為Cloud Service的最新發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的目前（最新）版本的一般發行說明。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>如需與發行不直接相關的檔案更新詳細資訊，請參閱[最近的檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前版本(2021.8.0)的發行日期為2021年8月26日。
下列版本(2021.9.0)將於2021年10月6日發行。

## 發行影片 {#release-video}

查看2021年8月[發行概述](https://video.tv.adobe.com/v/336277)影片，以取得新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]中的新功能 {#assets-features}

* 以連結形式共用數位資產時，使用者可以立即將URL複製到剪貼簿。 增強功能可讓您以更快速且更方便的方式共用資產。 此功能可讓您更快速且便利地共用資產。

   ![以連結形式共用資產時複製URL選項](/help/assets/assets/link-share-copy-URL-option.png)
   *圖：以連結形式共用資產時，您現在可以複製URL以個別共用。*

* 上傳TXT檔案時，資產微服務會自動產生縮圖。 PNG縮圖是TXT檔案的轉譯，可協助使用者在某些程度上識別內容或檔案，而不需開啟檔案。 此功能不需要任何設定，且預設可運作。

   ![PNG格式會自動產生TXT檔 [!DNL Assets] 案的轉譯](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *圖：系統會自動產生TXT檔案的轉譯，協助您識別檔案，而不需開啟。*

### [!DNL Assets]發行前通道中的新功能 {#assets-prerelease-features}

* 使用者現在可以在「欄」和「卡片」檢視中，對搜尋結果中顯示的資產進行排序。 排序適用於「名稱」、「已建立」、「已修改」或「無」欄。

   ![在「欄」和「卡片」檢 [!DNL Assets] 視中排序搜尋結果](/help/assets/assets/sort-searched-assets.png)
   *圖：在「欄」和「卡片」檢 [!DNL Assets] 視中排序搜尋結果。*

### [!DNL Assets]中修正的錯誤 {#assets-bugs-fixed}

* 當貢獻者群組的成員導覽至[!DNL Assets]主控台時，會產生額外的`POST`請求，以嘗試建立集合。 此要求並非必要項目，但會因權限問題而失敗，且會在記錄中建立許多錯誤。 (CQ-4328856)
* 當使用者檢視資產並從左側面板的快顯功能表選取[!UICONTROL 時間軸]時，會顯示錯誤。 在記錄中，由於查詢錯誤，會記錄許多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]中的新增功能 {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* Forms作為Cloud Service的AEM原型專案現在包含Microsoft Dynamics和Salesforce.com的[表單資料模型。](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment)

* **基於Acroform的記錄文檔**:AEM Forms作為Cloud Service，除了 [以XFA為基礎的表單範本外，支援使用Adobe Acrobat表單PDF(Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為記錄檔案的範本。

* **Microsoft Azure資料儲存連接器**:您現在可 [以將表單資料模型連接到Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您將最適化表單資料擷取並儲存至Microsoft Azure Storage，作為BLOB。

### [!DNL Forms]的Beta功能 {#aug-what-is-new-forms-prerelease}

* **統一儲存連接器：** 使用統一儲存連接器將客戶管理的儲存庫中的處理中資料外部化。例如，您可以
   * 啟用Forms Portal的儲存和繼續功能，並將最適化表單草稿儲存在客戶管理的資料存放庫中。
   * 儲存在客戶管理存放庫中包含敏感個人資料(SPD)的AEM工作流程資料(AEM工作流程變數資料)。

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) 訊API可以結合XDP範本和XML資料，以產生各種格式的列印檔案。此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   * 使用XML資料填入範本檔案，以產生檔案。
   * 以各種格式產生輸出表單，包括非互動式PDF列印資料流。
   * 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

您可以寫入[!DNL formscsbeta@adobe.com]以註冊測試版程式。

### [!DNL Forms]發行前通道中提供的新功能 {#prerelease-features-forms}

* **在適用性表單中使用Adobe Sign角色**:Adobe Sign（適用於業務和企業服務層級）可以選擇除簽署者外，擴展協定收件者的角色，以更符合其工作流程需求。您現在可以[啟用協定的每個收件者以在適用性表單](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform)中設定其角色，預設角色為簽署者。

* **適用性Forms的Analytics**:您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤一般使用者行為，以收集一般使用者分析。它有助於根據資料做出明智的決策，以改善一般使用者體驗。

* **輕鬆連接AEM Forms與Microsoft Dynamics和Salesforce.com**:此服務為Microsoft Dynamics和Salesforce.com提供現成的資料源配置和資料模型，使開發 [人員能夠更快、更輕鬆地將Microsoft Dynamics和Salesforce.com配置為最適化表單的資料源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html)。

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* 以Cloud Service形式顯示的螢幕現在支援基本播放監控。 播放器現在會報告各種播放量度，每次偵測（預設為30秒）。 它可根據量度偵測各種邊緣案例（停滯體驗、空白畫面、排程問題等）。 此功能可讓團隊遠端監視播放器是否正確播放內容、改善對空白畫面或欄位中中斷體驗的再活動，並降低向使用者顯示中斷體驗的風險。
如需詳細資訊，請參閱[基本播放監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 。

* Screens as aCloud Service現在支援的視訊縮圖支援。 內容作者可以定義視訊的縮圖，以便影像可作為預留位置，並在適當團隊完成實際視訊時，正確測試內容播放和鎖定目標。 當視訊播放失敗時，也可以使用影像。
如需詳細資訊，請參閱[視訊的縮圖支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 。

### 錯誤修正 {#bug-fixes-screens}

* 播放器無法顯示內嵌頁面的內容，此問題現已修正。

* 成功登入後，導覽至預設頁面（管道）最後會顯示「內部伺服器錯誤」頁面。

* 移除播放清單時，未移除相關的標籤項目。


## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更完善地支援複雜的產品目錄

   ![新類別選擇器](/help/assets/CIF/category-picker.png)

* 更A11Y支援CIF核心元件

## Cloud Manager {#cloud-manager}

本節概述AEM as a 2021.9.0和2021.8.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date-cm-sept}

AEM as aCloud Service2021.9.0中的Cloud Manager發行日期為2021年9月9日。
下一版預計於2021年10月7日發行。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager使用的AEM專案原型版本已更新為30版。

* Cloud Manager登陸頁面上的方案卡片和相關聯的體驗已重新整理。

* 程式碼品質步驟記錄現在包含OakPal掃描程式的詳細記錄資訊。

* 「活動」頁面功能表選項現在包含已完成代碼產生器執行的&#x200B;**下載記錄**&#x200B;選項。 選取此選項將下載建置步驟的記錄檔。

* 直接按一下「方案」卡片，現在會導覽至「Cloud Manager概觀」頁面。


### 錯誤修正 {#bug-fixes-sept}

* 在程式中新增IP允許清單時，使用者現在會看到更容易理解的訊息，此程式已達到可設定的IP允許清單允許數量上限。

* 從「儲存庫」螢幕選擇「複製URL」菜單選項時，複製了錯誤的URL。

## 發行日期 {#release-date-cm-aug}

AEM as aCloud Service2021.8.0中的Cloud Manager發行日期為2021年8月12日。

### 新增功能 {#what-is-new-aug}

* Cloud Service客戶現在可以在Cloud Manager中檢視「服務等級協定(SLA)」報表。 這將在今後幾個月內逐步提供。
請參閱[SLA報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)以了解更多資訊。

* IndexType和`IndexDamAssetLucene`質量規則的類型和嚴重性已更改。 這兩個都是Blocker *serverity*&#x200B;的錯誤。

* 已引入新的Oak索引品質規則，涵蓋非同步和tika設定。

* 將每個程式的SSL憑證上限提高至50個。

* 自助服務功能可讓使用者透過Cloud Manager UI建立和管理多個存放庫。

* SonarQube在不必要地閱讀Git歷史資料。 在大型程式碼基底中，這可能會導致不必要的組建效能損失。

* 現在有API可用來使每個管道的Maven相依性快取失效。

* Cloud Manager使用的AEM專案原型版本已更新為29版。

### 錯誤修正 {#bug-fixes-aug}

* 最新版本小於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織無法首次上線。

* 有時，當管道因某些原因觸發兩次時，會導致其中一個執行失敗，並出現&#x200B;*無法更新管道執行狀態*&#x200B;錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.5.6版的發行日期為2021年8月11日。

### 錯誤修正 {#bug-fixes-ctt}

* 在某些情況下，並非所有使用者都移轉至目標例項。 若要取得此修正CTT v1.5.6，必須在目標AEM上以Cloud Service例項的形式提供aem-ethos-tools 1.2.354或更新版本。

* 在擷取至Publish執行個體期間，已停用&#x200B;**停止擷取**&#x200B;按鈕。 這不是必要的，因為在發佈擷取期間沒有進行單次還原步驟。

* 成功提取後，CTT未清除`/tmp`目錄。 這有時會導致磁碟空間問題。

## Best Practices Analyzer {#best-practices-analyzer}

### 發行日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的發行日期為2021年9月2日。

### 新增功能 {#what-is-new}

* 偵測和報告總節點計數的功能。

* 偵測及報告節點存放區類型和大小的功能。

### 錯誤修正 {#bug-fixes-bpa}

* BPA錯誤偵測是否存在商務整合架構。

