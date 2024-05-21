---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0 版發行說明。'
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
source-git-commit: 02ad83eb9fa9ed3bf06cf7fe0ef10fd9577f66a9
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 83%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.10.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.10.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.10.0) 的發行日期為 2023 年 10 月 26 日。下一個功能版本 (2023.11.0) 計畫於 2023 年 11 月 30 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2023 年 10 月發行概觀影片，了解 2023.10.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 新功能 {#assets-features}

**適用於Adobe Express的AEM Assets附加元件**：Experience Manager Assets現在提供Adobe Express的附加元件。 此附加元件可讓您從 Adobe Express 使用者介面直接存取儲存在 Experience Manager Assets 的資源。您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。此附加元件提供以下主要優點：

* 透過在 AEM 中編輯和儲存新資源來提高內容重複使用率

* 減少建立新資產或現有資產新版本的整體時間和精力

  ![包括資產附加元件中的資產](/help/assets/assets/aem-assets-add-on-include-assets.png)

### 資產檢視中的新功能 {#assets-view-features}

* **從OneDrive資料來源大量匯入資產**：管理員現在能夠 [將大量資產從OneDrive匯入AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). 支援大量匯入的資料來源清單已更新，其中包括 Azure、AWS、Google Cloud、Dropbox 和 OneDrive。

  ![將中繼資料表單指派至資料夾](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **程式庫的跨組織權益支援**：Experience Manager Assets現在可讓您在其他IMS組織中設定Creative Cloud程式庫的存取權。 這允許更輕鬆地在 Creative Cloud 和 Experience Manager 之間存取最新跨產品工作流程，減少創作者工作所需時間和精力。

### [!DNL Experience Manager Assets] 中可用的搶鮮版功能 {#prerelease-features-assets}

* **Dynamic Media**： [Dynamic Media中的視訊支援多重註解與多重音訊曲目](/help/assets/dynamic-media/video.md#about-msma) — 您現在可以輕鬆地將多個字幕和多個音軌新增到主要視訊中。 此功能表示全球對象都可以存取您的影片。您可以以多種語言向全球對象自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。作者也可以從使用者介面的單一標籤管理註解和音訊曲目。

  ![在選取的視訊資產的「屬性」頁面上，使用註解和音訊曲目索引標籤。](/help/release-notes/assets/msma-aem-cs.png)*在選取的視訊資產的「屬性」頁面上，使用註解和音訊曲目索引標籤。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* **[調適型表單的自訂屬性](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**：您可以將自訂屬性 (鍵值配對) 與表單範本或調適型表單元件建立關聯，以允許表單開發人員提供根據這些自訂屬性值進行調整的動態表單行為。例如，開發人員可以根據自訂屬性值在行動裝置、桌面或 Web 平台上製作不同版本的 Headless Forms 元件，進而大幅增強各種裝置上的使用者體驗。

* **主題和範本**：使用我們全新主題和範本啟動您的表單建立流程，這些主題和範本都是專為支援經驗豐富的專業人士和新表單作者量身打造。使用調適型表單元核心元件無縫建置的這些精心策劃的主題和範本，可讓您迅速地開始針對常見使用案例建立表單。

  ![現成可用的範本](/help/forms/assets/form-templates-ootb.png)


### 早期採用計劃 {#forms-early-adopter}

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 流量篩選規則，包括 WAF {#traffic-filter-rules-waf}

[篩選 Adob&#x200B;&#x200B;e Managed CDN 的流量](/help/security/traffic-filter-rules-including-waf.md)，方法是透過聲明按屬性 (包括 url、IP 位址和使用者代理程式) 來匹配網站流量的規則，或設定自訂流量速率限制以防範 DoS 攻擊。客戶還可以授權一組進階 Web 應用程式防火牆 (WAF) 規則，以針對複雜的網站威脅提供額外的保護。

我們鼓勵您透過以下方式熟悉流量篩選規則 [試用教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)！ 此課程可引導您完成設定新的 Cloud Manager 設定管道、在設定檔中聲明規則，以及分析 CDN 記錄中的惡意流量。

流量篩選規則現可在開發環境中使用，且 11 月將逐步可在中繼和生產環境中使用。您可以透過傳送電子郵件至：**aemcs-waf-adopter@adobe.com**，要求提前在中繼和生產環境中存取。

進階 WAF 流量篩選規則可在今年稍後透過增強安全性或 WAF-DDoS 防護產品獲得授權。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
