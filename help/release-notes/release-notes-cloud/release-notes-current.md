---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 2d5fa0b15456ad9838fa236a2b5c79d41a9af7fe
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 68%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2024.9.0)的發行日期是2024年9月26日。 下一個功能版本(2024.10.0)計畫於2024年10月31日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!--  ## Release Video {#release-video}

Have a look at the September 2024 Release Overview video for a summary of the features added in the 2024.9.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 新功能 {#new-feature-sites}

#### 翻譯管理 {#translation-management}

AEM翻譯工作流程和API動作現在會觸發事件，以提供翻譯工作狀態變更的相關分析。 使用者可透過Adobe Developer Console訂閱這些事件。 請參閱[這裡](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/)，以取得有關AEM Translation Management API的詳細資訊。

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 的搶先體驗功能 {#dm-early-access}

**以 AI 產生的影片字幕**

Adobe Dynamic Media 中以 AI 產生的影片字幕，是使用人工智慧來自動產生影片內容的字幕。此功能旨在透過提供準確的即時字幕來改善可存取性並增強使用者體驗。AI 分析影片的音軌以轉錄語音並建立針對準確性或自訂可進行編輯的字幕。這些字幕有助於滿足可存取性的要求，並改善依賴或偏好文字式影片支援之客群的影片參與度。

若要在您的 Dynamic Media 帳戶搶先體驗 AI 產生的字幕支援，請[建立並提交 Adobe 客戶支援案例](/help/assets/dynamic-media/video.md##enable-dash)。

### Asset Selector中的新功能 {#asset-selector-new-features}

Asset Selector現在支援瀏覽收藏集，以尋找您想要的資產。
![資產選擇器集合](/help/assets/assets/collections-rail-modal-view.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的全新預發行功能 {#forms-new-prerelease-features}

#### 自動儲存以核心元件為主的調適型表單草稿

使用者現在可以享受自動儲存功能帶來的好處，此功能會將部分完成的表單自動儲存為草稿。他們可以稍後再回來，使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。


### AEM Forms 的優先體驗功能 {#forms-new-early-access-features}

AEM Forms 優先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需優先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 優先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI 助理

調適型表單的生成式 AI 全面提升表單開發流程的功能和易用性。它使您能夠建置更好的表單，速度也比以往更快。

![生成式 AI 助理、調適型表單](/help/forms/assets/generative-ai-assistant.png)

提供的生成式 AI 功能包括：

* **產品查詢的 AI 助理**：立即取得 AEM 表單相關問題的答案。AI 助理會成為您的個人知識庫，直接在平台內提供具深刻見解的指導和建議。

* **產生最適化表單**：使用生成式 AI 提示輕鬆建立形式完整的表單。Adobe 生成式 AI 會自動產生容易使用的表單，可降低流失率同時提供個人專屬體驗。

* **表單面板生成**：產生適合特定資料集需求的表單區段。例如：產生用於收集付款資訊、客戶偏好或旅行詳細資訊的區段。

* **變更表單版面配置**：使用生成式 AI 提示嘗試不同的版面配置和設計。嘗試不同的版面配置，例如精靈或索引標籤視圖，為您的表單找到最合適的版面配置。使用生成式 AI 提示來將表單最佳化，以利改善行動裝置的反應能力，並建立使用者喜歡的具有視覺吸引力的表單。

* **設定提交動作**：使用生成式 AI 提示輕鬆設定表單的提交動作。從預先建立提交動作的資料庫中選擇，或是從您的開發團隊建立和部署的自訂提交動作中選擇。

>[!IMPORTANT]
>
> 有興趣加入任何 Forms 創新的搶先體驗計劃？從您的官方地址發送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，並附上您感興趣的功能清單。

## CIF 附加元件 {#cloud-services-cif}

### 改善功能 {#improvements-fixes-cif}

* 讓類別限制可自訂。

### 錯誤修正 {#bug-fixes-cif}

* Commerce欄位未正確與Assets中繼資料結構編輯器整合。
* 傳送產品拖放多欄位的問題。
* 拖放的輪播類別多欄位問題。
* 在類別和產品編輯器頁面的頁面資訊中，按一下無法用於功能表。
* 訂單編號在訂單確認頁面中不可見。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### Edge Side Include (ESI)可載入動態內容 {#esi}

Adobe 管理的內容傳遞網路現在支援 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，這是一種用於邊緣層級動態 Web 內容組合的標記語言。透過包含 ESI 程式碼段，您可以在具有較高 TTL 的 CDN 上快取整個 HTML 頁面，同時更頻繁地從來源取得需要較高節奏更新 (較低 TTL) 的較小區段。此功能將逐步推出。

### CDN的基本驗證 {#basicauth-cdn}

透過彈出要求使用者名稱和密碼的基本驗證對話方塊來保護某些內容資源。此功能主要針對輕型身分驗證使用案例，例如業務利害關係人檢閱內容，而不是作為一般使用者存取權限的全面解決方案。使用者名稱和密碼清單可透過Git中的設定檔案進行管理，該檔案會透過設定管道部署，並參考機密型別的Cloud Manager環境變數。 [了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

### 使用者端重新導向 {#client-side-redirects}

在部署至CDN並在CDN上評估的組態檔Git中宣告[瀏覽器重新導向](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。 此功能在刪除頁面、變更的網站結構及SEO最佳化等情境中相當實用。

### 全新AEM Developer Console (公開Beta) {#aem-developer-console-beta}

嘗試改版的[AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，在雲端環境中偵錯程式碼時可提供更互動的體驗。

任何人都可以按一下目前AEM Developer Console中的&#x200B;*可用的新主控台*&#x200B;按鈕來存取公開測試版。 Adobe歡迎您提供意見回饋，您可以透過電子郵件傳送至&#x200B;**<aemcs-new-devconsole-ui-beta@adobe.com>**。

AEM Developer Console中的![OSGi套件組合畫面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### 業務使用者可以在 Git 之外宣告重新導向 (早期採用者計劃) {#apache-rewritemaps-early-adopter}

與AEM 6.5類似，Apache/Dispatcher會擷取重寫發佈存放庫中的特定位置的地圖，並在不需要Web層管道執行的情況下載入。 此方法可讓商務使用者使用試算表或UI （例如ACS Commons重新導向地圖管理員或自訂應用程式）來宣告重新導向。 透過寄送電子郵件給&#x200B;**<aemcs-cdn-config-adopter@adobe.com>**&#x200B;加入早期採用者計畫。

### RDE的設定管道（早期採用者計畫） {#config-pipeline-rdes-early-adopter}

[設定管道](/help/operations/config-pipeline.md)用於部署yaml檔案設定，包括CDN選項（流量篩選規則、請求/回應轉換等）。 透過寄送電子郵件給&#x200B;**<aemcs-cdn-config-adopter@adobe.com>**&#x200B;加入早期採用者計畫，將這些相同的設定部署至使用CLI的RDE （快速開發環境）。

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
