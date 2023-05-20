---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.8.0 版發行說明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 50%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本版本(2021.8.0)為2021年8月26日。
以下版本(2021.9.0)是2021年10月6日。

## 發行影片 {#release-video}

看看 [2021年8月發佈概述](https://video.tv.adobe.com/v/336277) 視頻，瞭解添加的功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 當將數字資產作為連結共用時，用戶可以立即將URL複製到剪貼簿。 增強功能使您能夠以更快、更方便的方式共用資產。 此功能允許更快、更方便的資產共用。

   ![將資產共用為連結時複製URL選項](/help/assets/assets/link-share-copy-URL-option.png)
   *圖：當將資產作為連結共用時，您現在可以複製URL以單獨共用它。*

* 上載TXT檔案時，資產microservices會自動生成縮略圖。 PNG縮略圖是TXT檔案的格式副本，它幫助用戶在一定程度上標識內容或檔案，而不開啟檔案。 此功能不需要任何配置，並且預設情況下可以工作。

   ![TXT檔案的格式副本由 [!DNL Assets] 格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *圖：TXT檔案的格式副本將自動生成，以幫助您識別檔案而不開啟。*

### 中的新功能 [!DNL Assets] 預釋放通道 {#assets-prerelease-features}

* 用戶現在可以對搜索結果中顯示的「列」和「卡」視圖中的資產進行排序。 排序在「名稱」(Name)、「已建立」(Created)、「已修改」(Modified)或「無」(None)列上工作。

   ![對搜索結果排序 [!DNL Assets] 列和卡視圖中](/help/assets/assets/sort-searched-assets.png)
   *圖：對搜索結果排序 [!DNL Assets] 的子菜單。*

### 修正在[!DNL Assets]中的錯誤 {#assets-bugs-fixed}

* 當參與者組的成員導航到 [!DNL Assets] 控制台，額外 `POST` 生成請求以嘗試和建立集合。 此請求不是必需的，由於權限問題而失敗，並在日誌中建立了許多錯誤。 (CQ-4328856)
* 當用戶查看資產並選擇 [!UICONTROL 時間軸] 從左面板的彈出菜單中，顯示錯誤。 由於查詢錯誤，日誌中記錄了許多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* automated forms conversion服務 [用義大利語和葡萄牙語轉換PDF forms語](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 適應Forms。

* **根據 Acroform 的記錄文件**：除了根據 PDF 的表單範本以外，AEM Forms as a Cloud Service 也支援使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

* **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 您現在可以啟用每個協議收件者，以便在最適化表單中設定其角色，並將簽署者設定為預設角色。

* **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

* **輕鬆將AEM Forms與Microsoft動力和Salesforce.com連接**:該服務為MicrosoftDynamics和Salesforce.com提供現成的資料源配置和資料模型，使開發人員能夠更快更輕鬆地將MicrosoftDynamics和Salesforce.com配置為適應性表單的資料源。

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的類別選取器UI可改善用戶體驗、提高效率並更好地支援複雜的產品目錄

   ![新建類別選取器](/help/assets/CIF/category-picker.png)

* 更好地支援CIF核心元件

## Cloud Manager {#cloud-manager}

本節概述了as a Cloud Service和中的Cloud ManagerAEM的2021.8.0行說2021.7.0。

## 發行日期 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 中的 Cloud Manager 發行日期是 2021 年 8 月 12 日。下一版計畫於2021年9月09日發行。

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

內容傳輸工具v1.5.6的發佈日期為2021年8月11日。

### 錯誤修正 {#bug-fixes-ctt}

* 在某些情況下，並非所有用戶都遷移到目標實例。 要獲得此修復，需要在目標as a Cloud Service實例上使用CTT v1.5.6以及aem-ethos-tools 1.2.354或更高版本AEM。

* 的 **停止攝取** 在接收到「發佈」實例期間禁用了按鈕。 由於在發佈接收期間沒有單點恢復步驟，因此不必這樣做。

* CTT沒有清理 `/tmp` 成功抽取後的目錄。 這有時會導致磁碟空間問題。
