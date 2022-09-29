---
title: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e59e5e79bfcdd19e159aadd4ed9567dfe624b21e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.8.0)為2022年9月1日。
下一版(2022.9.0)預計於2022年10月13日發行。

## 發行影片 {#release-video}

請觀看2022年8月版本概述影片，以取得2022.8.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 電子郵件元件可在AEM中建立內容，然後透過Campaign Classic以電子郵件傳送。 核心電子郵件元件：
   * 是根據 [核心WCM元件](https://github.com/adobe/aem-core-wcm-components) 支援可編輯的模板和樣式系統。
   * 提供10個電子郵件最佳化的生產就緒元件（頁面、容器、標題、文字、影像、按鈕、預告、體驗片段、內容片段、細分）。
   * 多虧了 [插入促銷活動變數](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) 在大多數對話欄位上，以及靈活的 [區段元件](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * 借助於 [CSS樣式內嵌](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), [HTML屬性內線](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)，和 [HTML消毒劑](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * 可隨處建立電子郵件。

### [!DNL Sites] 搶鮮版頻道中可用的新功能 {#prerelease-features-sites}

* 此 [內容片段主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 為使用者提供可顯示與內容片段相關聯的語言副本總數的選項。 提供一鍵式存取，也可檢視所有語言副本。 使用者也可以依所感興趣的地區來篩選表格檢視。

![內容片段語言](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#features-assets}

* 您現在可以將Adobe Experience Manager Assets設定為 [根據MIME類型限制使用者可上傳的資產類型](/help/assets/configure-asset-upload-restrictions.md).

   ![資產上傳限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* [適用性Forms精靈](/help/forms/creating-adaptive-form.md):AEM Forms提供商務使用者易記精靈，可快速撰寫最適化Forms。 精靈提供快速的索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。 此版本對精靈進行下列改良：

   * 選擇或取消選擇欄位：精靈可讓您根據JSON和表單資料模型結構建立最適化表單。 您現在可以選取結構內要納入適用性表單的欄位子集。 選取的欄位會轉換為對應的最適化表單資料擷取元件，以快速建立所需的最適化表單。

   * 使用靜態範本：如果客戶現有投資於舊版靜態範本，則可在精靈中使用靜態範本來撰寫最適化表單，以繼續雲端採用歷程。 這可讓客戶將舊靜態範本移轉至現代可編輯的範本，以提供額外的時間。

* [在伺服器端處理時，從記錄檔案(DoR)中移除隱藏欄位](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md):您可以為最終用戶生成記錄PDF文檔，該文檔僅包含在資料捕獲體驗期間對他們可見的欄位。 提交表單時，伺服器會根據提交的資料驗證向最終用戶隱藏的欄位，並從記錄中排除以保持一致。

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 透過AEM頁面屬性將AEM頁面與產品和類別關聯，並在產品座艙中提供概覽
   ![產品座艙頁面關聯](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
