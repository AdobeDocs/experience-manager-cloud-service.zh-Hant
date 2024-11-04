---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 08b23f093e4362a9885919a3e3d87bdcaada8876
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 58%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2024.10.0)的發行日期是2024年10月31日。 下一個功能版本(2024.11.0)計畫於2024年11月21日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**現代化頁面事件**

下列AEM Sites頁面事件現在可作為基於AEM as a Cloud Service事件平台的外部消耗性事件使用。 事件可透過Adobe I/O處理，以與外部程式互動。
* 頁面已發佈
* 頁面已取消發佈
* 頁面已刪除

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**用於內容片段傳送的AEM REST OpenAPI**

內容片段傳送的[AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)現在可用於AEM as a Cloud Service。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 的搶先體驗功能 {#dm-early-access}

**以 AI 產生的影片字幕**

Adobe Dynamic Media 中以 AI 產生的影片字幕，是使用人工智慧來自動產生影片內容的字幕。此功能旨在透過提供準確的即時字幕來改善可存取性並增強使用者體驗。AI 分析影片的音軌以轉錄語音並建立針對準確性或自訂可進行編輯的字幕。這些字幕有助於滿足可存取性的要求，並改善依賴或偏好文字式影片支援之客群的影片參與度。

若要在您的 Dynamic Media 帳戶搶先體驗 AI 產生的字幕支援，請[建立並提交 Adobe 客戶支援案例](/help/assets/dynamic-media/video.md##enable-dash)。

### 使用 Assets 檢視的新功能 {#assets-view-new-features}

**排程報告**

現在可以根據週期排程或在未來日期在Assets檢視中自動產生報表，減少發掘資料導向深入分析的工作。

![排程報告 — ](/help/assets/assets/scheduled-reports-tab.png)

### 全新的 Content Hub 功能 {#content-hub-new-features}

已授權資產的&#x200B;**數位版權管理**

組織現在可以利用DRM為Content Hub的使用者授權資產，提高授權規範並儘可能降低與授權條款共用資產的風險，這要求使用者必須先檢閱並接受授權條款，才能開始下載授權資產。

![下載多重授權](/help/assets/assets/download-multiple-license.png)

**資產卡中繼資料組態**

Content Hub現在可讓您設定關鍵中繼資料欄位，以顯示在資產卡上，最多6個欄位。

資產卡上的![金鑰中繼資料](/help/assets/assets/asset-card-key-metadata.png)

**設定過期資產的可見度和下載**

管理員現在可以控制是否需要在 Content Hub 顯示過期資產。如果要在上面顯示過期資產，這些資產還可以定義使用者是否可以下載資產。

![Content Hub 上的過期資產](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的全新預發行功能 {#forms-new-prerelease-features}

#### 自動儲存以核心元件為主的最適化表單草稿

使用者現在可以享受自動儲存功能帶來的好處，此功能會將部分完成的表單自動儲存為草稿。他們可以稍後再回來，使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI 助理

最適化表單的生成式 AI 全面提升表單開發流程的功能和易用性。它使您能夠建置更好的表單，速度也比以往更快。

![生成式 AI 助理、最適化表單](/help/forms/assets/generative-ai-assistant.png)

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

### 錯誤修正 {#bug-fixes-cif}

* 修正UI測試，使其可正確搭配核心CIF元件運作。
* 已解決類別URL格式在雲端例項中無法如預期運作的問題。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 控制表單提交的設定 {#configuration-submissions}

為了控制Coral或Foundation表單在特定位置的表單提交，AEM已引入新的設定： `com.adobe.granite.ui.components.FormRestrict`。 此設定包含兩個欄位：

1. **新增允許的路徑**：指定允許表單動作的路徑。
1. **限制行為**：決定限制路徑（未包含在允許清單中的路徑）的行為。 您可以選擇兩個選項：
   * **快顯視窗** （預設）：顯示快顯通知。
   * **防止**：封鎖表單提交。

>[!NOTE]
>
>位於`/apps`、`/libs`、`/mnt/overlay`和`/mnt/override`下的所有Coral或Foundation表單都不支援此設定。

### 具有進階網路選項的自助式記錄檔轉送 {#log-forwarding}

雖然可以從Cloud Manager下載AEM (包括Apache/Dispatcher)和CDN記錄，但許多組織認為將這些記錄串流到偏好的記錄目的地會很有幫助。 AEM現在支援[記錄轉送](/help/implementing/developing/introduction/log-forwarding.md)至Azure Blob Storage、Datadog、HTTPS、Elasticsearch （和OpenSearch）和Splunk。 AEM記錄檔可選擇透過進階網路設定進行轉送，例如使用專用IP位址。

此功能由使用者以自助方式設定，並使用[設定管道](/help/operations/config-pipeline.md)進行部署。

### 適用於企業使用者的管道免費URL重新導向 {#pipeline-free-redirects}

當網頁已停止或移動，或其他情況時，瀏覽器端重新導向相當實用。 透過[沒有管道的URL重新導向](/help/implementing/dispatcher/pipeline-free-url-redirects.md)，您可以將Apache重寫對應檔案放置在AEM發佈位置，該檔案會自動載入 — 不需要將檔案認可到原始檔控制或起始Cloud Manager管道。

發佈重寫檔案的選項包括將其上傳為資產、使用ACS Commons Rewrite Map Manager，或與自訂使用者介面互動。

### RDE的設定管道 {#config-pipeline-rdes}

快速開發環境是一款強大的工具，可在雲端環境中快速部署和測試程式碼和設定。 RDE現在支援[同步設定YAML檔案](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)，包括流量篩選規則、要求/回應轉換、記錄轉送及其他設定選項等CDN設定。 [如需詳細資訊，請參閱支援的組態選項完整清單](/help/operations/config-pipeline.md)。

### 新的產品設定檔 {#new-product-profiles}

建立新的AEM環境時，產品設定檔會自動出現在Adobe Admin Console中，讓管理員指派存取權給授權的解決方案和功能。

新環境現在包含一組更新的產品設定檔，使其與未來的功能相容，包括在Adobe Developer Console中產生API認證。 現有環境將能夠更新其在未來版本中的產品設定檔。 [了解更多](/help/onboarding/aem-cs-team-product-profiles.md)。

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 歡迎您提供意見回饋，請透過電子郵件發送至 **<aemcs-new-devconsole-ui-beta@adobe.com>**。

![AEM Developer Console 中的 OSGi 套件螢幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

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
