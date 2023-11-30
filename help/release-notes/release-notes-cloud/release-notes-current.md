---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 0290e40094147a1c85eacf157904c7ef7388c5e7
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 24%

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

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2023.11.0)為2023年11月30日。 下一個功能版本(2023.12.0)計畫於2023年12月14日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看2023年11月版本概觀影片，瞭解2023.11.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期採用計劃 {#sites-early-adopter}

**[尋找和取代內容片段中的字串](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：內容片段控制檯為使用者提供簡單且直覺的方式，取代同時出現在多個內容片段中的字串，以加速內容速度。

![尋找和取代](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

有興趣嘗試該功能並分享回饋意見嗎？傳送電子郵件至 **aemcs-headless-adopter@adobe.com** 從您的官方電子郵件ID瞭解有關早期採用者計畫的更多資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-features}

* **AEM Assets中的內嵌Adobe Express編輯器**：具有Express存取許可權的使用者現在已整合影像編輯和建立工具，可直接在AEM Assets中使用Adobe Express和Adobe Firefly，以改進內容重複使用和加快內容速度。

  ![將中繼資料表單指派至資料夾](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Insights中的儲存使用情況報表**：管理員現在能夠檢視儲存空間使用量報表，這些報表是深入分析的一部分。

  ![儲存使用情況深入分析](/help/assets/assets/storage-usage-insights.png)

* **搜尋第一個首頁設定**：Experience Manager Assets現在可讓您設定組織的首頁體驗。 如果您選取「搜尋優先」作為首頁，則可設定您組織的搜尋列對齊方式、背景影像和標誌。

  ![搜尋第一個設定](/help/assets/assets/search-first-configuration.png)

### 管理檢視搶鮮版中的新功能 {#admin-view-features-prerelease}

**視訊預視**：AEM Assets現在依預設會產生所有支援視訊格式的預覽轉譯，而不需要設定處理設定檔。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新功能 {#forms-features}

* **[核取方塊元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：以核心元件為基礎的最適化Forms現在可以包含核取方塊元件。 它可讓使用者進行二進位選擇，選取或取消選取特定選項。 它通常會顯示為一個小方塊，可以按一下或點選以在兩個狀態之間切換：核取和未核取。 核取方塊是常見的表單元素，用於呈現是/否或真/假選擇。

* **[條款與條件元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：根據核心元件的最適化Forms現在可以包含條款與條件元件。 它可讓表單作者在表單中推出特定區段，向使用者呈現與使用服務、產品或平台相關的條款、條件或法律協定。 此元件的設計目的，是透過提交表單告知使用者其同意的規則、法規與義務。

  ![核取方塊、條款與條件，以及垂直標籤元件](/help/forms/assets/forms-components.png)

* **[垂直索引標籤元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：以核心元件為基礎的最適化Forms現在可以將表單內容整理到垂直索引標籤清單中，提供結構化和可導覽的版面。 在表單中使用垂直標籤可簡化導覽並改善表單內容的組織，進而增強整體使用者體驗，尤其是在表單包含多個區段或複雜資訊的情況下。



### [!DNL Forms] 發行前版本的新功能 {#prerelease-features-forms}

* **[連線最適化Forms與Microsoft® SharePoint清單](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**： AEM Forms提供OOTB整合，可直接將表單資料提交至SharePoint清單，讓您運用SharePoint的清單功能。 您可以將Microsoft SharePoint清單設定為表單資料模型的資料來源，並使用 **使用表單資料模型提交** 提交動作以將最適化表單與SharePoint清單連線。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期採用計劃 {#forms-early-adopter}

* **提交最適化表單至Adobe Workfront Fusion案例**：Formsas a Cloud Service提供立即可用的選項，讓您輕鬆將最適化表單與Adobe Workfront連結。 這可簡化將最適化表單提交至Adobe Workfront情境的程式，讓您在提交最適化表單時觸發Workfront Fusion情境。

* **從右至左語言支援**：建置在核心元件上的調適型Forms現在能以從右至左(RTL)語言顯示，例如阿拉伯文、波斯文和烏都文。 全球超過20億人使用RTL語言。 使用RTL語言中的表單，可讓您延伸最適化表單的觸角，以迎合這些不同的受眾，並拓展RTL市場。 在某些地區，提供當地語言的表格也是法律義務。 您可以因應當地語言，不僅為更廣大的受眾敞開大門，也確保符合相關法律法規。

  ![從右至左語言支援](/help/forms/assets/right-to-left-language-support.png)

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-early-adopter-program@adobe.com`，加入早期採用者計畫並要求存取該功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 現在可以授權WAF流量篩選規則 {#cdn-waf-license}

流量篩選規則已於10月發行，其中包括一項備註說明，說明特殊類別的Web應用程式防火牆(WAF)規則將於今年晚些時候推出，以補充Sites和Forms客戶已有的規則。 作為更新，現在可以授權WAF-DDoS Protection產品。

在授權後，這些進階WAF規則可以使用Cloud Manager設定管道部署到CDN以新增一層額外的保護來抵禦Web攻擊。

閱讀關於 [流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)，包括WAF。 與您的AEM客戶團隊討論授權WAF-DDoS保護或增強式安全性。

### CDN設定早期採用者計畫 {#cdn-config-early-adopter}

除了最近發行的 [流量篩選規則（包括WAF）](/help/security/traffic-filter-rules-including-waf.md)，您有機會使用設定管道來宣告和部署其他型別的CDN設定。 我們很樂意瞭解您的使用案例，包括：
* 301/302使用者端重新導向
* 在邊緣將請求代理到任意來源
* URL轉換
* 設定或修改要求或回應標頭
* CDN無法連線AEM時的自訂錯誤頁面
* 依使用者名稱/密碼驗證
* 任何其他有用的CDN設定

傳送電子郵件至 **aemcs-cdn-config-adopter@adobe.com** 來自您的正式電子郵件ID以及您的意見回饋。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## 已知問題 {#known-issues}

* 使用者無法根據核心元件提交最適化Forms。 使用核心元件2.0.38 - 2.0.60版建置的最適化Forms會發生問題。

  以解決問題。 您可以移至最適化表單核心元件2.0.62版或更新版本。 若要為您的環境設定最適化Forms核心元件版本， [設定core.forms.components.version、core.forms.components.af.version和core.wcm.components.version元件的版本](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) 您的Formsas a Cloud Service存放庫或AEM原型專案和中的相依性 [將變更部署至您的Formsas a Cloud Service環境](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). 您可以在下列位置找到最新版的最適化Forms核心元件相依性： [最適化Forms核心元件Git存放庫](https://github.com/adobe/aem-core-forms-components#system-requirements).
