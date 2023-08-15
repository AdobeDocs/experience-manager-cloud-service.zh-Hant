---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 49%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 目前發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的一般發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2021.8.0)為2021年8月26日。
下列版本(2021.9.0)將於2021年10月6日發行。

## 發行影片 {#release-video}

請檢視 [2021年8月版本總覽](https://video.tv.adobe.com/v/336277) 影片以瞭解新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 以連結形式共用數位資產時，使用者可以立刻將URL複製到剪貼簿。 此增強功能可讓您以更快、更方便的方式共用資產。 此功能可讓您更快、更方便地共用資產。

  ![以連結形式共用資產時複製URL選項](/help/assets/assets/link-share-copy-URL-option.png)
  *圖：以連結形式共用資產時，您現在可以複製URL以個別共用。*

* 當您上傳TXT檔案時，資產微服務會自動產生縮圖。 PNG縮圖是TXT檔案的轉譯，可幫助使用者在一定程度上識別內容或檔案，而不需要開啟檔案。 依預設，此功能不需要任何設定就能運作。

  ![系統會自動產生TXT檔案的轉譯 [!DNL Assets] PNG格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *圖：會自動產生TXT檔案的轉譯，協助您識別檔案而不開啟。*

### 中的新功能 [!DNL Assets] 發行前通道 {#assets-prerelease-features}

* 使用者現在可以在「欄」和「卡片」檢視中排序搜尋結果內所顯示的資產。 排序功能適用於「名稱」、「已建立」、「已修改」或「無」欄。

  ![將搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中](/help/assets/assets/sort-searched-assets.png)
  *圖：搜尋結果排序於 [!DNL Assets] 在欄和卡片檢視中。*

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

* 當貢獻者群組成員導覽至 [!DNL Assets] 主控台，額外的 `POST` 會產生要求以建立集合。 此請求不是必要請求；它因許可權問題而失敗，並在記錄中建立許多錯誤。 (CQ-4328856)
* 使用者檢視資產並選取 [!UICONTROL 時間表] 從左側面板的彈出式選單中，會顯示錯誤。 在記錄中，由於查詢錯誤，記錄了許多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* automated forms conversion服務可以 [轉換義大利文和葡萄牙文PDF forms文](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 最適化Forms。

* **根據 Acroform 的記錄文件**：除了根據 PDF 的表單範本以外，AEM Forms as a Cloud Service 也支援使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為BLOB儲存於Microsoft Azure儲存體。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 您現在可以啟用每個協議收件者，以便在最適化表單中設定其角色，並將簽署者設定為預設角色。

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

* **輕鬆將AEM Forms連線至Microsoft Dynamics和Salesforce.com**：此服務提供適用於Microsoft Dynamics和Salesforce.com的現成資料來源設定和資料模型，好讓開發人員更快且更輕鬆地將Microsoft Dynamics和Salesforce.com設定為最適化表單的資料來源。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的類別選擇器UI可改善使用者體驗、提高效率，以及更好地支援複雜的產品目錄

  ![新增類別選取器](/help/assets/CIF/category-picker.png)

* CIF核心元件的更佳A11Y支援

## Cloud Manager {#cloud-manager}

本節概述AEMas a Cloud Service2021.8.0和2021.7.0中Cloud Manager的發行說明

## 發行日期 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 中的 Cloud Manager 發行日期是 2021 年 8 月 12 日。下一版本計畫於2021年9月9日發行。

### 新增功能 {#what-is-new-aug}

* Cloud Service 客戶現在可以在 Cloud Manager 中檢視服務等級協定 (SLA) 報告。我們即將在未來幾個月以漸進方式推出這項功能。
如需了解更多，請參閱 [SLA 報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=zh-Hant)。

* IndexType 和 `IndexDamAssetLucene` 品質規則的類型和嚴重性已變更。這兩個規則現在都歸類於「阻斷錯誤」*嚴重性*。

* 我們引進了新的 Oak 索引品質規則來涵蓋非同步和 Tika 設定。

* 將每個計劃的 SSL 憑證數上限增加到 50。

* 可讓使用者透過 Cloud Manager UI 建立及管理多個存放庫的自助式功能。

* SonarQube 之前會讀取 Git 記錄資料，這是不必要的。在大型計劃碼基底中，這可能會導致不必要的建置效能損失。

* 現在有一個 API 可讓每個管道的 Maven 相依性快取失效。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 29。

### 錯誤修正 {#bug-fixes-aug}

* 當最新版本低於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織於初始入門時失敗。

* 有時，當管道由於某種原因被觸發兩次時，會導致其中一次執行失敗，並出現&#x200B;*無法更新管道執行狀態*&#x200B;錯誤。

## 內容轉移工具 {#content-transfer-tool}

### 發行日期 {#release-date-ctt-latest}

內容轉移工具v1.5.6的發行日期為2021年8月11日。

### 錯誤修正 {#bug-fixes-ctt}

* 在某些情況下，並非所有使用者都已移轉至目標執行個體。 若要取得此修正，目標AEMas a Cloud Service執行個體上需要CTT v1.5.6以及aem-ethos-tools 1.2.354或更新版本。

* 此 **停止內嵌** 在擷取至發佈執行個體期間已停用按鈕。 這並非必要，因為發佈內嵌期間沒有蒙戈還原步驟。

* CTT未清除 `/tmp` 成功擷取後的目錄。 這有時會導致磁碟空間問題。
