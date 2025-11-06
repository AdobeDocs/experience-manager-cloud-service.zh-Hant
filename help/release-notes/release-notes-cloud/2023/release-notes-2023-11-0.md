---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 版發行說明。'
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 94%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.11.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2023.11.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2023.11.0) 的發行日期是 2023 年 11 月 30 日。下一個功能版本 (2023.12.0) 計畫於 2023 年 12 月 14 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2023 年 11 月發行概觀影片，了解 2023.11.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期採用者計劃 {#sites-early-adopter}

**[尋找並取代內容片段中的字串](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：內容片段主控台為使用者提供了一種簡單直覺的方法，可一次取代出現在多個內容片段中的單一字串，以協助加快內容速度。

![尋找並取代](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 **aemcs-headless-adopter@adobe.com**，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

* **嵌入在 AEM Assets 中的 Adobe Express 編輯器**：可存取 Express 的使用者現在可以直接在 AEM Assets 中使用整合在內的 Adobe Express 和 Adobe Firefly 影像編輯和建立工具，以提升內容重複使用效能並加快內容速度。

  ![將中繼資料表單指派至資料夾](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Insights 中的儲存空間使用量報告**：管理員現在可以查看作為 Insights 一部分提供的儲存空間使用量報告。

  ![儲存空間使用量深入解析](/help/assets/assets/storage-usage-insights.png)

* **搜尋優先首頁設定**：Experience Manager Assets 現在可讓您為組織設定首頁體驗。如果您選取搜尋優先作為首頁，您可以為您的組織設定搜尋列對齊方式、背景影像和標誌。

  ![搜尋優先設定](/help/assets/assets/search-first-configuration.png)

### 管理檢視搶鮮版中的新功能 {#admin-view-features-prerelease}

**視訊預視**：AEM Assets 現在預設產生所有支援的視訊格式的預視呈現，無需設定處理設定檔。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* **[核取方塊元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：以核心元件為主的最適化表單現在可以包含核取方塊元件。可讓使用者二選一，選取或取消選取特定選項。它通常為一個小方塊，可以按一下或點選以在兩種狀態之間切換：選取和取消選取。核取方塊是一種常見的表單元素，用來表示選擇是/否或真/假。

* **[條款與條件元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：以核心元件為主的最適化表單現在可以包含條款與條件元件。它允許表單作者在表單中引入特定區段，向使用者顯示與使用服務、產品或平台相關的條款、條件或法律協議。此元件的設計用意是在告知使用者他們透過提交表單同意的規則、法規和義務。

  ![核取方塊、條款與條件和垂直標籤元件](/help/forms/assets/forms-components.png)

* **[垂直標籤元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：以核心元件為主的最適化表單現在可以將表單內容組織成垂直的標籤清單，提供結構化、可導覽的版面。在表單中使用垂直標籤可以簡化導覽和改進表單內容組織，進而提升使用者整體體驗，特別是在表單包含多個部分或複雜資訊時。



### [!DNL Forms]發行前版本中的新功能 {#prerelease-features-forms}

* **[將最適化表單與 Microsoft® SharePoint 清單連接](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**：AEM Forms 提供 OOTB 整合，可將表單資料直接提交到 SharePoint 清單，使您能夠利用 SharePoint 清單功能。您可以將 Microsoft SharePoint 清單設定為表單資料模型的資料來源，並透過&#x200B;**使用表單資料模型提交**&#x200B;這個提交動作，將最適化表單與 SharePoint 清單連接。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期採用者計劃 {#forms-early-adopter}

* **將最適化表單提交到 Adobe Workfront Fusion 情境**：Forms as a Cloud Service 提供開箱即用的選項，可輕鬆將最適化表單與 Adobe Workfront 連接。這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

* **從右至左語言支援**：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的客群並進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的客群敞開大門，還可以確保遵守相關法律和法規。

  ![從右至左語言支援](/help/forms/assets/right-to-left-language-support.png)

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 現在可以授權WAF流量篩選器規則 {#cdn-waf-license}

流量篩選規則於 10 月發行，其中包含一項說明，即今年稍後將推出特殊類別的 Web 應用程式防火牆 (WAF) 規則，以補充 Sites 和 Forms 客戶已有的規則。作為更新，WAF-DDoS 保護產品現在可獲得授權。

獲得授權後，可以使用 Cloud Manager 設定管道將這些進階 WAF 規則部署到 CDN，多加一層保護來抵擋 Web 攻擊。

閱讀[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)，包括 WAF。請與您的 AEM 客戶團隊聯繫，以了解授權 WAF-DDoS 保護或增強安全性的相關資訊。

### 網域對應早期採用者計畫 {#cdn-config-early-adopter}

除了最近發行的[流量篩選規則 (包括 WAF)](/help/security/traffic-filter-rules-including-waf.md)，還有機會使用設定管道來宣告和部署其他類型的 CDN 設定。我們很想聽聽您的使用案例，包括：

* 301/302 用戶端重新導向
* 將邊緣要求代理到任意來源
* URL 轉換
* 設定或修改要求或回應標頭
* CDN 無法連接 AEM 時的自訂錯誤頁面
* 透過使用者名稱/密碼進行身份驗證
* 任何其他有用的 CDN 設定

使用您的官方電子郵件 ID 將您的回饋意見透過電子郵件寄送至：**aemcs-cdn-config-adopter@adobe.com**。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## 已知問題 {#known-issues}

* 無法提交以核心元件為主的最適化表單。使用核心元件版本 2.0.38 – 2.0.60 建立的最適化表單會出現此問題。

  若要解決問題。您可以移轉到最適化表單核心元件版本 2.0.62 或更新版本。若要為您的環境設定最適化Forms核心元件的版本，請在您的Forms as a Cloud Service存放庫或AEM Archetype型專案中設定`core.forms.components.version`、`core.forms.components.af.version`和`core.wcm.components.version component`相依性的版本，並將變更部署至您的Forms as a Cloud Service環境。 您可以在[最適化表單核心元件 Git 存放庫](https://github.com/adobe/aem-core-forms-components#system-requirements)找到最新版本的最適化表單核心元件相依性。
