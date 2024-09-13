---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: fc578f35214327567aaa6f5d88a637df9428f87f
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 79%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.8.0 版) 的發行日期為 2024 年 8 月 29 日。下一個功能版本 (2024.9.0 版) 預計於 2024 年 9 月 26 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 8 月發行概觀影片，了解 2024.8.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 新功能 {#new-feature-sites}

**Edge Delivery Services 的 AEM Authoring**

現已支援現行站點[繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md)功能，包括：

* [AEM 啟動](/help/sites-cloud/authoring/launches/overview.md)
* [多網站管理器 (MSM)](/help/sites-cloud/administering/msm/overview.md) (頁面層級)

此外，現在也支援以下頁面管理功能：

* [AEM 標籤](/help/sites-cloud/authoring/sites-console/tags.md)可作為[分類](/help/edge/wysiwyg-authoring/taxonomy.md)匯出至 Edge Delivery Services。
* Edge Delivery Services 的[範本](/help/edge/wysiwyg-authoring/templates.md)即將推出！

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media的早期存取功能 {#dm-early-access}

**AI視訊標題**

Adobe Dynamic Media中的AI型視訊字幕會使用人工智慧為視訊內容自動產生字幕。 此功能旨在改善協助工具，並透過提供準確的即時註解來增強使用者體驗。 AI會分析視訊的音軌以轉譯語音並建立字幕，您可以編輯這些內容以提高準確性或加以自訂。 這些註解有助於滿足協助工具要求，並提升依賴或偏好文字型視訊支援之對象的視訊參與度。

### 資產視圖的新功能 {#assets-view-new-features}

**已更新「Adobe Firefly 影像生成」**

Assets as a Cloud Service 現在使用最新的 Firefly 小工具，讓您可以運用 Adobe Firefly 生成不同風格的影像。只要使用內建的 Firefly 編輯器定義其風格、構成、尺寸等等，就可以直接在 AEM Assets 存放庫中快速建立和儲存您需要的資產，方便立即使用。

![Adobe Firefly 影像生成](/help/assets/assets/bugatti-type-57.png)

**PSB 文件支援**

除了現有的 PSD 檔案支援之外，Assets as a Cloud Service 現在也開始支援 Photoshop 大型文件 (PSB 檔案)。

### 全新的 Content Hub 增強功能 {#content-hub-new-enhancements}

* 更利於處理長檔名，並可透過工具提示輕鬆擴展完整名稱。
* 改善縮圖，以更符合內容外觀比例，並涵蓋更大的內容區域。
* Content Hub 支援 AEM 的自訂縮圖體驗。
* 改善色彩搜尋。
* 改善設定儲存體驗。
* 已改善集合的資訊頁面，以反映建立者名稱。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的全新預發行功能 {#forms-new-prerelease-features}

#### 自動儲存以核心元件為主的調適型表單草稿

使用者現在可以享受自動儲存功能帶來的好處，此功能會將部分完成的表單自動儲存為草稿。他們可以稍後再回來，使用同一部裝置或其他裝置完成填寫。此功能可減少表單放棄率，藉以改善組織的轉換率，因為使用者不需要從頭開始填寫表單。


### AEM Forms 的優先體驗功能 {#forms-new-early-access-features}

AEM Forms 優先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需優先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 優先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI 助理

調適型表單的生成式 AI 全面提升表單開發流程的功能和易用性。它使您能夠建置更好的表單，速度也比以往更快。

![生成式 AI 助理、調適型表單](/help/forms/assets/generative-ai-assistant.png)

提供的生成式 AI 功能包括：

* **產品查詢的 AI 助理**：立即取得 AEM 表單相關問題的答案。AI 助理會成為您的個人知識庫，直接在平台內提供具深刻見解的指導和建議。

* **產生最適化表單**：輕鬆建立具有產生式AI提示的完整表單。 Adobe的創作AI會自動產生方便使用的表單，以減少流失並個人化體驗。

* **表單面板生成**：產生適合特定資料集需求的表單區段。例如：產生用於收集付款資訊、客戶偏好或旅行詳細資訊的區段。

* **變更表單版面配置**：使用產生式AI提示來實驗不同的版面配置和設計。 嘗試不同的版面配置，例如精靈或索引標籤檢視，找到最適合您的表單版面配置。使用創造性的AI提示來最佳化您的表單，以提供行動回應，並建立使用者喜愛的視覺化吸引人表單。

* **設定送出動作**：使用產生式AI提示，輕鬆設定表單的送出動作。 從預先建立的提交動作資料庫或由開發團隊建立和部署的自訂提交動作中選擇。

>[!IMPORTANT]
>
> 有興趣加入搶先體驗計畫以進行Forms創新嗎？ 從您的正式地址傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中包含您感興趣的功能清單。


## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

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
