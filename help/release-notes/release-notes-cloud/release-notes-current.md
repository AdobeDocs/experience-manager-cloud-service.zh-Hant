---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 99a36bab3ca8d5e6a64e1fdb9c179cf8a3190a14
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 52%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2024.8.0)的發行日期是2024年8月29日。 下一個功能版本(2024.9.0)計畫於2024年9月26日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 8 月發行概觀影片，了解 2024.8.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 新功能 {#new-feature-sites}

**Edge Delivery Services 的 AEM 製作**

現在支援現有的網站[繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md)功能，包括：

* [AEM 啟動](/help/sites-cloud/authoring/launches/overview.md)
* 頁面層級的[MSM](/help/sites-cloud/administering/msm/overview.md)

此外，現已支援下列頁面管理功能：

* [AEM標籤](/help/sites-cloud/authoring/sites-console/tags.md)可以作為[分類](/help/edge/wysiwyg-authoring/taxonomy.md)匯出給Edge Delivery Services。
* 即將推出適用於Edge Delivery Services的[範本](/help/edge/wysiwyg-authoring/templates.md)！

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產檢視中的新功能 {#assets-view-new-features}

**已更新Adobe Firefly影像產生**

Assets as a Cloud Service現在使用Firefly最新的Widget，可讓您使用Adobe Firefly產生不同樣式的影像。 透過定義其樣式、構成、維度等，使用內建的Firefly編輯器，您可以直接在AEM Assets存放庫中快速建立和儲存您需要的資產，以立即使用。

![Adobe Firefly影像產生](/help/assets/assets/bugatti-type-57.png)

**PSB檔案支援**

除了現有的as a Cloud Service檔案支援外，Assets現在還支援PhotoshopPSD大型檔案（PSB檔案）。

### Content Hub中的新增強功能 {#content-hub-new-enhancements}

* 更妥善地處理長檔案名稱，透過工具提示輕鬆擴充完整名稱。
* 改善縮圖，以更符合內容外觀比例，並涵蓋更大的內容區域。
* 透過內容中心支援AEM的自訂縮圖體驗。
* 改善色彩搜尋。
* 改善設定可儲存體驗。
* 已改善集合的資訊頁面，以反映建立者名稱。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms中的新搶鮮版功能 {#forms-new-prerelease-features}

#### 根據最適化Forms自動儲存核心元件的草稿

使用者現在可以受益於自動儲存功能，該功能會自動將部分完成的表單儲存為草稿。 他們可以稍後再回來，在相同或其他裝置上完成填寫。 此功能可減少表單放棄率，改善組織的轉換率，因為使用者不需要從頭開始填寫表單。


### AEM Forms 的優先體驗功能 {#forms-new-early-access-features}

AEM Forms搶先體驗計畫提供您獨一無二的機會，讓您以獨家方式存取尖端創新技術，並幫助打造其開發流程。

本發行說明列出目前版本提供的創新功能。如需優先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 優先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI助理

最適化Forms的創作AI為您的表單開發流程帶來全新境界的強大功能和簡易性。 這可讓您以前所未有的速度建置更好的表單。

![Generative AI助理，最適化Forms](/help/forms/assets/generative-ai-assistant.png)

提供的Generative AI功能包括：

* **產品查詢的AI小幫手**：取得您的AEM表單相關問題的立即解答。 AI助理就像您自己的個人知識庫，直接在平台內提供有見地的指引和建議。

* **產生最適化表單**：輕鬆建立具有產生AI提示的完整表單。 我們的Generative AI會自動產生方便使用的表單，以減少流失並個人化體驗。

* 為Forms **產生**&#x200B;面板：產生符合特定資料收集需求的表單區段。 例如，產生用於收集付款資訊、客戶偏好設定或旅行詳細資訊的區段。

* **變更表單版面配置**：使用Generative AI提示嘗試不同版面配置和設計。 嘗試不同的版面（如精靈或索引標籤檢視），以找出最符合您表單的版面。 使用Generative AI提示將您的表單最佳化為行動回應，並建立使用者喜愛的具有視覺吸引力的表單。

* **設定送出動作**：使用Generative AI提示輕鬆設定表單的送出動作。 從預先建立的提交動作資料庫或由您自己的開發團隊建立和部署的自訂提交動作清單中選擇。

>[!IMPORTANT]
>
> 如果您有興趣加入Early Access Program以進行任何創新，只要將您感興趣的功能清單從您的官方地址傳送給[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)即可。


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
