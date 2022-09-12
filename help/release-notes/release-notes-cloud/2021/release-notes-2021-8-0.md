---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 22%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2021.8.0)為2021年8月26日。
下列版本(2021.9.0)將於2021年10月6日發行。

## 發行影片 {#release-video}

查看 [2021年8月發行概述](https://video.tv.adobe.com/v/336277) 視訊，以取得新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 以連結形式共用數位資產時，使用者可以立即將URL複製到剪貼簿。 增強功能可讓您以更快速且更方便的方式共用資產。 此功能可讓您更快速且便利地共用資產。

   ![以連結形式共用資產時複製URL選項](/help/assets/assets/link-share-copy-URL-option.png)
   *圖：以連結形式共用資產時，您現在可以複製URL以個別共用。*

* 上傳TXT檔案時，資產微服務會自動產生縮圖。 PNG縮圖是TXT檔案的轉譯，可協助使用者在某些程度上識別內容或檔案，而不需開啟檔案。 此功能不需要任何設定，且預設可運作。

   ![TXT檔案的轉譯由 [!DNL Assets] PNG格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *圖：系統會自動產生TXT檔案的轉譯，協助您識別檔案，而不需開啟。*

### 中的新功能 [!DNL Assets] 預發行管道 {#assets-prerelease-features}

* 使用者現在可以在「欄」和「卡片」檢視中，對搜尋結果中顯示的資產進行排序。 排序適用於「名稱」、「已建立」、「已修改」或「無」欄。

   ![在中排序搜尋結果 [!DNL Assets] 欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
   *圖：在中排序搜尋結果 [!DNL Assets] 欄和卡片檢視。*

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

* 貢獻者群組的成員導覽至 [!DNL Assets] 主控台，額外 `POST` 會產生請求以嘗試並建立集合。 此要求並非必要項目，但會因權限問題而失敗，且會在記錄中建立許多錯誤。 (CQ-4328856)
* 使用者檢視資產並選取 [!UICONTROL 時間表] 從左側面板的彈出式功能表中，會顯示錯誤。 在記錄中，由於查詢錯誤，會記錄許多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* automated forms conversion服務可以 [用義大利語和葡萄牙語轉換PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 最適化Forms。

* **根據 Acroform 的記錄文件**：除了根據 PDF 的表單範本以外，AEM Forms as a Cloud Service 也支援使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 您現在可以啟用每個協議收件者，以便在最適化表單中設定其角色，並將簽署者設定為預設角色。

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

* **輕鬆連接AEM Forms與Microsoft Dynamics和Salesforce.com**:此服務提供Microsoft Dynamics和Salesforce.com的現成資料來源設定和資料模型，讓開發人員能更快速、更輕鬆地將Microsoft Dynamics和Salesforce.com設定為最適化表單的資料來源。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更完善地支援複雜的產品目錄

   ![新類別選擇器](/help/assets/CIF/category-picker.png)

* 更A11Y支援CIF核心元件

## Cloud Manager {#cloud-manager}

本節概述AEM 2021.8.0和2021.7.0as a Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date-cm-aug}

AEM 2021.8.0中的Cloud Manageras a Cloud Service日期為2021年8月12日。
下一版預計於2021年9月9日發行。

### 新增功能 {#what-is-new-aug}

* Cloud Service客戶現在可以在Cloud Manager中檢視「服務等級協定(SLA)」報表。 這將在今後幾個月內逐步提供。
請參閱 [SLA報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) 了解更多。

* IndexType和的類型和嚴重性 `IndexDamAssetLucene` 品質規則已變更。 這兩個都是Blocker的錯誤 *伺服器*.

* 已引入新的Oak索引品質規則，涵蓋非同步和tika設定。

* 將每個程式的SSL憑證上限提高至50個。

* 自助服務功能可讓使用者透過Cloud Manager UI建立和管理多個存放庫。

* SonarQube在不必要地閱讀Git歷史資料。 在大型程式碼基底中，這可能會導致不必要的組建效能損失。

* 現在有API可用來使每個管道的Maven相依性快取失效。

* Cloud Manager使用的AEM專案原型版本已更新為29版。

### 錯誤修正 {#bug-fixes-aug}

* 最新版本小於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織無法首次上線。

* 有時候，當管道因某些原因而觸發兩次時，會導致其中一個執行失敗 *無法更新管道執行狀態* 錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具1.5.6版的發行日期為2021年8月11日。

### 錯誤修正 {#bug-fixes-ctt}

* 在某些情況下，並非所有使用者都移轉至目標例項。 若要取得此修正，需在目標AEMas a Cloud Service執行個體上，連同aem-ethos-tools 1.2.354或更新版本一併取得CTT v1.5.6。

* 此 **停止擷取** 將擷取至發佈執行個體期間，按鈕已停用。 這不是必要的，因為在發佈擷取期間沒有進行單次還原步驟。

* CTT未清理 `/tmp` 目錄。 這有時會導致磁碟空間問題。
