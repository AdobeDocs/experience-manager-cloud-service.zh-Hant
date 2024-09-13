---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 6194df9d-8c3c-4c7f-be59-099b970a565a
source-git-commit: fc578f35214327567aaa6f5d88a637df9428f87f
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 77%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.7.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.7.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.7.0) 的發行日期為 2024 年 7 月 25 日。下一個功能版本 (2024.8.0) 預計於 2024 年 8 月 29 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 7 月版本概觀影片，了解 2024.7.0 版本新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 新功能 {#new-feature-sites}

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**在內容片段控制台中瀏覽資產**

內容作者現在可以瀏覽、查看影像，並對影像執行動作，而無需離開內容片段控制台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 aemcs-headless-adopter@adobe.com，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**使用資產選擇器上傳資產**

Asset Selector現在提供內容作者直接從選取器上傳最終資產的功能，方法是拖曳或瀏覽本機檔案系統。 此功能允許您從所選的應用程式將最終資產上傳到DAM。

### Dynamic Media的早期存取功能 {#dm-early-access}

**AI視訊標題**

Adobe Dynamic Media中的AI型視訊字幕會使用人工智慧為視訊內容自動產生字幕。 此功能旨在改善協助工具，並透過提供準確的即時註解來增強使用者體驗。 AI會分析視訊的音軌以轉譯語音並建立字幕，您可以編輯這些內容以提高準確性或加以自訂。 這些註解有助於滿足協助工具要求，並提升依賴或偏好文字型視訊支援之對象的視訊參與度。

### 資產視圖的新功能 {#assets-view-new-features}

**Content Credentials 整合**

Experience Manager Assets 現在針對支援的影像格式提供 Content Credentials 支援。此功能提供有關資產歷程及其建立方式的資訊，包括是否使用GenAI進行修改。

![Content Credentials](/help/assets/assets/content-credentials.png)

**資料夾內容的視覺化預覽**

Experience Manager Assets現在會在瀏覽或搜尋內容時，在資料夾縮圖上顯示資料夾內容的視覺預覽，這可改善AEM Assets存放庫中可用資產的可發現性。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-prerelease-features}

#### 核心元件式最適化表單的增強型視覺規則編輯器

調適型表單作者可使用可重複的表單欄位和現成的視覺化規則編輯器函式，在表單中建立複雜的商業邏輯，而無需來自開發團隊的自訂或支援。

### AEM Forms 的優先體驗功能 {#forms-new-early-access-features}

AEM Forms 優先體驗計劃為您提供獨一無二的機會，讓您比其他人更早獲得尖端創新的獨家存取權，並協助推動相關開發。您可以透過該計劃存取多項創新。

本發行說明列出目前版本提供的創新功能。如需優先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 優先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 使用通用編輯器製作最適化表單

利用 Adobe Experience Manager [通用編輯器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)的所見即所得拖放工具建立最適化表單，以實現透過 Edge Delivery Service 傳遞的 (headless) 和有頭 (headful) 註冊體驗。最適化表單作者可針對網頁中的表單變化，輕鬆建立並啟動實驗。 此功能可讓他們為一般使用者決定最佳執行體驗。

>[!IMPORTANT]
>
> 如果您有興趣加入 Adobe 優先體驗計劃以使用任何優先體驗創新，請直接從您的正式地址寄送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 要求存取。您可以要求存取所有或任何特定的創新。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 使用自助 API 金鑰清除內容傳遞網路上的內容 {#purge-cdn}

使用 HTTP Cache-Control 標頭設定 TTL 是平衡內容傳遞效能和內容新鮮度的有效方法。不過，在必須立即提供更新內容的情況下，直接清除CDN快取可能會有助益。

[瞭解如何](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)使用Cloud Manager設定管道自助提供清除API Token的設定，以便您可以[叫用具有下列任何變數的清除API](/help/implementing/dispatcher/cdn-cache-purge.md)：

* 單一 URL
* 使用標記的多個 URL
* 全面 CDN 快取清除

### 客戶管理之 CDN 的 X-AEM-Edge-Key 自助設定 {#customermanaged-keys}

以前，需要支援服務單才能產生設定客戶管理之內容傳遞網路所需的 X-AEM-Edge-Key。此工作流程現在是自助式，透過在使用設定管道部署的設定檔案中宣告索引鍵值，消除新環境上線中的任何延遲。 [了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

### 流量篩選規則警報 {#traffic-filter-rules-alerts}

流量篩選規則包含可選擇性授權的Web應用程式防火牆(WAF)規則，可讓您設定應該封鎖哪些流量。

現在，只要流量篩選規則被觸發，您就可以[訂閱警示](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts)。 發生某些流量狀況時，行動中心電子郵件通知會通知您，以利採取適當措施。

### 與內容交付相關的早期採用者計劃 {#foundation-early-adopter}

請寄送電子郵件至 **<aemcs-cdn-config-adopter@adobe.com>**，指出您對以下哪些早期採用者計劃感興趣。

#### 內容傳遞網路的基本驗證 (早期採用者計劃) {#basicauth-cdn}

透過彈出要求使用者名稱和密碼的基本驗證對話方塊來保護某些內容資源。此功能主要針對輕型身分驗證使用案例，例如業務利害關係人檢閱內容，而不是作為一般使用者存取權限的全面解決方案。使用者名稱和密碼清單是由設定檔管理的，此設定檔位於透過設定管道部署的 Git 中，會參考祕密類型的 Cloud Manager 環境變數。[了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### 用戶端重新導向 (早期採用者計畫) {#client-side-redirects-early-adopter}

在原始碼控制系統中設定 301/302 用戶端重新導向，並部署到內容傳遞網路。[了解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 請注意，已經有一些與[內容傳遞網路設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)相關的其他功能可用，包括要求和回應轉換，以及將流量路由到 AEM 之外的網站。

#### 業務使用者可以在 Git 之外宣告重新導向 (早期採用者計劃) {#apache-rewritemaps-early-adopter}

與 AEM 6.5 類似，Apache/Dispatcher 擷取放在發佈存放庫中特定位置的重新寫入對應並將其載入，而不需要 Web 層級的管道執行。此方法可讓業務使用者使用試算表或 UI (例如 ACS Commons Redirect Map Manager 或自訂應用程式) 宣告重新導向。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 用來載入動態內容的 Edge Side Includes (ESI) (早期採用者計劃) {#esi-early-adopter}

Adobe 管理的內容傳遞網路現在支援 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，這是一種用於邊緣層級動態 Web 內容組合的標記語言。透過包含 ESI 程式碼片段，您可以在內容傳遞網路上用較高的 TTL 快取整個 HTML 頁面，同時更頻繁地從來源擷取需要較高更新頻率 (TTL 較低) 的較小區段。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### 內容健康相關行動中心通知早期採用者計劃 {#actions-center-notifications}

有重要事件發生時，或是我們注意到您的程式碼或設定中有些問題需要主動採取行動時，[行動中心](/help/operations/actions-center.md)就會寄送電子郵件通知。Adobe 現在推出了幾種與您的內容健康相關的新類型通知。此功能可透過早期採用者計畫使用。若要參與，請聯絡 Adobe 客戶服務。

#### 頁面包含大量節點 {#page-nodes}

大量節點會降低轉譯效能並減少頁面載入時間。當偵測到頁面有大量節點時，您會收到動作中心主動傳來的通知，從而允許您採取必要的步驟來減少頁面內的節點總數。

#### 大量執行中工作流程實例 {#running-workflows}

當製作環境中存在大量執行中工作流程時，工作流程引擎效能會受到影響。當偵測到大量執行中工作流程時，您會收到動作中心主動傳來的通知。此程序可讓您設定清除作業以終止不必要的執行中工作流程。

#### 直接新增到自訂群組的使用者 {#users-customgroups}

當使用者直接新增至自訂群組時，您會收到動作中心主動傳來的通知。此程序可讓您遵循 IMS 最佳實務，將使用者新增至相關 IMS 群組，然後將這些 IMS 群組納入 AEM 群組做為其成員。

#### 缺少 JCR 內容 {#jcr-content}

當偵測到缺少 JCR 內容時，動作中心會主動通知您。透過此方法，您可以新增缺少的內容並防止某些 AEM Assets 功能失敗。

#### 已完成的工作流程未清除 {#workflows}

當超過 90 天的已完成工作流程尚未清除時，動作中心會主動通知您。此方法透過減少工作流程實例數來幫助提高工作流程引擎的效能。

#### 缺少 Sling 資源 {#sling-resource}

當偵測到缺少 Sling 資源時，動作中心會主動通知您。透過此方法，您可以新增缺少的資源並防止某些 AEM Assets 功能失敗。

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## 通用編輯器 {#universal-editor}

您可以在[這裡](/help/release-notes/universal-editor/current.md)找到通用編輯器版本的完整清單。

## 產生變化版本 {#generate-variations}

您可以在[這裡](/help/generative-ai/release-notes-generate-variations.md)找到「產生變化版本」版本的完整清單。

## Experience Cloud 發行說明 {#experience-cloud}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/release-notes/experience-cloud/current)查看其他 Experience Cloud 應用程式版本的相關資訊。
