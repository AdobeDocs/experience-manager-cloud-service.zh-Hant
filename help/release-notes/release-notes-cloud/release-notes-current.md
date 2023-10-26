---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 6e834244f3de7e615df12b137f2ae90a11e64ad0
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 54%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2023.10.0)為2023年10月26日。 下一個功能版本(2023.11.0)計畫於2023年11月30日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2023 年 10 月發行概觀影片，了解 2023.10.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 新功能 {#assets-features}

**適用於Adobe Express的AEM Assets附加元件**：Experience Manager Assets現在提供 [Adobe Express的附加元件](/help/assets/addon-adobe-express.md). 附加元件可讓您從Adobe Express使用者介面直接存取儲存在Experience Manager Assets中的資產。 您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。此附加元件提供以下主要優點：

* 透過在 AEM 中編輯和儲存新資源來提高內容重複使用率

* 減少建立新資產或現有資產新版本的整體時間和精力

  ![包括資產附加元件中的資產](/help/assets/assets/aem-assets-add-on-include-assets.png)

### 資產檢視中的新功能 {#assets-view-features}

* **從OneDrive資料來源大量匯入資產**：管理員現在能夠 [將大量資產從OneDrive匯入AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). 支援大量匯入的資料來源更新清單包括Azure、AWS、Google Cloud、Dropbox和OneDrive。

  ![將中繼資料表單指派至資料夾](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **程式庫的跨組織權益支援**：Experience Manager Assets現在可讓您在其他IMS組織中設定Creative Cloud程式庫的存取權。 它可讓您更輕鬆地存取Creative Cloud和Experience Manager之間最新的跨產品工作流程，並減少創意內容的時間和精力。

### [!DNL Experience Manager Assets] 中可用的搶鮮版功能 {#prerelease-features-assets}

* **Dynamic Media**：[對 Dynamic Media 影片的多語言字幕和多語言音訊支援](/help/assets/dynamic-media/video.md#about-msma) - 您現在可以輕鬆地將多語字幕和多語言音訊新增至主要影片中。此功能表示全球對象都可以存取您的影片。您可以以多種語言向全球對象自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。作者還可以從使用者介面中的單個標籤管理字幕和音訊。

  ![所選視頻資產「屬性」頁面上「字幕和音訊」標籤。](/help/release-notes/assets/msma-aem-cs.png)*所選視頻資產「屬性」頁面上「字幕和音訊」標籤。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* **最適化Forms的自訂屬性**：您可以將自訂屬性（索引鍵值配對）與表單範本或調適型表單元件建立關聯，好讓表單開發人員能夠根據這些自訂屬性的值調整動態表單行為。 例如，開發人員可以根據自訂屬性的值，在行動、桌上型電腦或Web平台上製作Headless Forms元件的不同轉譯，藉此大幅提升各種裝置的使用者體驗。

* **主題和範本**：透過我們的新主題和範本，開始您的表單建立流程，量身打造以增強經驗豐富的專業人員和新表單作者的能力。 使用調適型表單元核心元件無縫建置的這些精心策劃的主題和範本，可讓您迅速地開始針對常見使用案例建立表單。

  ![現成可用的範本](/help/forms/assets/form-templates-ootb.png)

### [!DNL Forms] 中可用的搶鮮版功能 {#pre-release-features-available-in-forms-channel}

* **將Forms提交至Microsoft SharePoint清單**： AEM Forms提供OOTB整合，可直接將表單資料提交至SharePoint清單，讓您運用SharePoint的清單功能。

  >[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

### 早期採用計劃 {#forms-early-adopter}

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-early-adopter-program@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 流量篩選器規則，包括WAF {#traffic-filter-rules-waf}

[在Adobe管理的CDN篩選流量](/help/security/traffic-filter-rules-including-waf.md) 透過宣告規則來比對網站流量（包括url、IP位址和使用者代理程式），或設定自訂流量速率限制來防禦DoS攻擊。 客戶也可以授權一組進階的Web應用程式防火牆(WAF)規則，針對複雜的網站威脅提供額外的保護。

我們鼓勵您透過以下方式熟悉流量篩選規則 [試用教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)！ 它會逐步引導您設定新的Cloud Manager設定管道、在設定檔案中宣告規則，以及分析CDN記錄檔中的惡意流量。

流量篩選規則現在適用於開發環境，並於11月逐步推出至預備和生產環境。 您可以透過傳送電子郵件至stage和prod，要求更早的存取權 **aemcs-waf-adopter@adobe.com**.

進階WAF流量篩選規則可於今年稍後透過「增強式安全性」或「WAF-DDoS保護」方案授權。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
