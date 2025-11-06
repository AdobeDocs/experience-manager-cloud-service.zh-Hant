---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.10.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.10.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 7a63f04f-10f0-4879-bd06-4182bb288a9b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.10.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.10.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.10.0) 的發行日期為 2024 年 10 月 31 日。下一個功能版本 (2024.11.0) 規劃於 2024 年 11 月 21 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 10 月發行概觀影片，了解 2024.10.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3440501?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**現代化的頁面事件**

以下 AEM Sites 頁面事件現在可作為以 AEM as a Cloud Service 事件平台為基礎的外部可使用事件。這些事件可以透過 Adobe I/O 處理，以便與外部程序互動。

* 頁面已發佈
* 頁面已取消發佈
* 頁面已刪除

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**用於內容片段傳送的 AEM REST OpenAPI**

[用於內容片段傳送的 AEM REST OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) 現在已可用於 AEM as a Cloud Service。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 的搶先體驗功能 {#dm-early-access}

**以 AI 產生的影片字幕**

Adobe Dynamic Media 中的 AI 生成影片字幕功能會使用人工智慧，為影片內容自動生成字幕。透過提供準確的即時字幕，這項功能可改善可存取性並增強使用者體驗。AI 分析影片的音軌以轉錄語音並建立針對準確性或自訂可進行編輯的字幕。這些字幕有助於滿足可存取性的要求，並改善依賴或偏好文字式影片支援之客群的影片參與度。

若要在您的 Dynamic Media 帳戶搶先體驗 AI 產生的字幕支援，請[建立並提交 Adobe 客戶支援案例](/help/assets/dynamic-media/video.md##enable-dash)。

### 資產檢視的新功能 {#assets-view-new-features}

**排程報告**

現在起，可以按照定期排程或在未來的日期，在資產檢視中自動產生報告，從而減少發掘資料導向深入解析所需的工作量。

![排程報告-](/help/assets/assets/scheduled-reports-tab.png)

### Content Hub 的新功能 {#content-hub-new-features}

**授權資產的 Digital Rights Management**

組織現在可以利用 Content Hub 使用者授權資產的 DRM，要求使用者在開始下載授權資產前檢閱並接受授權條款，以提高授權合規性，且將具有授權條款之資產的共用風險降至最低。如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

![下載多個授權](/help/assets/assets/download-multiple-license.png)

**資產卡片中繼資料設定**

現在起，Content Hub 可讓您設定需要在資產卡片上顯示的重要中繼資料欄位，最多可設定 6 個欄位。如需詳細資訊，請參閱[設定 Content Hub](/help/assets/configure-content-hub-ui-options.md#asset-card) 中的「資產卡片」區段。

![資產卡片上的重要中繼資料](/help/assets/assets/asset-card-key-metadata.png)

**設定已到期之資產的可見度與下載操作**

管理員現在可以控制是否需要在 Content Hub 上顯示已到期的資產。如果顯示已到期的資產，管理員還可以定義使用者是否可以下載這些資產。如需詳細資訊，請參閱[設定 Content Hub](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) 中的「已到期的資產」區段。

![Content Hub 上的過期資產](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

* [使用面板版面的導覽按鈕增強使用者體驗](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)：您現在可以在面板版面新增導覽按鈕，例如水平標籤、垂直標籤、摺疊式面板或精靈。這些按鈕簡化轉換不同面板的操作，專注於所選取的面板，藉此增強使用者體驗。

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### AEM Forms 的全新預發行功能 {#forms-new-prerelease-features}

* [自動儲存基於核心元件的最適化表單草稿](/help/forms/save-core-component-based-form-as-draft.md)：使用者現在可以享受自動儲存的好處，此功能會將部分完成的表單自動儲存為草稿。使用者可以稍後再使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

* [輕鬆更新 Adobe Sign 範圍](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms)：您可以直接從 AEM Cloud 設定頁面修改 Adobe Sign 設定的範圍，讓您更新現有設定更快速、更輕鬆。

* [最適化表單的非同步函數支援](/help/forms/using-async-funct-in-rule-editor.md)：當最適化表單需要非同步操作 (例如等待外部流程或資料擷取) 時，您可以使用自訂函數來執行這些操作並在規則編輯器中進行設定。

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI 助理

[最適化表單的生成式 AI](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) 全面提升表單開發流程的功能和易用性。它使您能夠建置更好的表單，速度也比以往更快。

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

* 修正使用者介面測試，以便與核心 CIF 元件正常搭配運作。
* 解決類別 URL 格式在雲端執行個體中未如預期運作的問題。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 表單提交的控制設定 {#configuration-submissions}

為了控制特定位置的 Coral 或 Foundation 表單提交，AEM 引進了一個新設定：`com.adobe.granite.ui.components.FormRestrict`。此項設定由兩個欄位組成：

1. **新增允許的路徑**：指定允許表單動作的路徑。
1. **限制行為**：決定限制路徑 (未包含在允許清單中之路徑) 的行為。您可以在以下兩個選項中進行選擇：
   * **快顯視窗** (預設)：顯示快顯視窗通知。
   * **防止**:Blocks&#x200B;表單提交。

>[!NOTE]
>
>位於 `/apps`、`/libs`、`/mnt/overlay` 和 `/mnt/override` 下的所有 Coral 或 Foundation 表單，均不支援此設定。

### 具備進階網路選項的自助式記錄轉送功能 {#log-forwarding}

雖然可以從 Cloud Manager 下載 AEM (包括 Apache/Dispatcher) 和內容傳遞網路記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是有益處的。AEM 現在支援將[記錄轉送](/help/implementing/developing/introduction/log-forwarding.md)到 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。可選擇透過進階網路設定轉送 AEM 記錄，例如使用專屬的 IP 位址。

此功能由使用者以自助方式設定，並透過[設定管道](/help/operations/config-pipeline.md)進行部署。

### 適合商業使用者的無管道 URL 重新導向 {#pipeline-free-redirects}

網頁遭撤下、移動或發生其他情況時，瀏覽器端的重新導向就非常實用。透過[無管道 URL 重新導向](/help/implementing/dispatcher/pipeline-free-url-redirects.md)，您可以將 Apache 重心寫入對應檔案放置在 AEM 發佈位置，該檔案會在其中自動載入，無需將其提交到來源控制或啟動 Cloud Manager 管道。

發佈重新寫入檔案的選項包括將其作為資產上傳、使用 ACS Commons Rewrite Map Manager，或與自訂使用者介面互動。

### 設定 RDE 的管道 {#config-pipeline-rdes}

快速開發環境是一項強大的工具，用來在雲端環境中快速部署及測試程式碼與設定。RDE 現在支援[同步設定 YAML 檔案](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)，包括流量篩選規則和請求/回應轉換等內容傳遞網路設定，以及記錄轉送和其他設定選項。如需更多詳細資訊，請參閱支援之設定選項的[完整清單](/help/operations/config-pipeline.md)。

### 全新產品設定檔 {#new-product-profiles}

建立新的 AEM 環境時，產品設定檔會自動顯示在 Adobe Admin Console 中，使管理員能夠指派對授權解決方案與功能的存取權。

現在起，新的環境包含一組更新的產品設定檔，使其能與未來的功能相容，包括在 Adobe Developer Console 中產生 API 認證。現有環境將能夠在未來版本中更新其產品設定檔。[了解更多](/help/onboarding/aem-cs-team-product-profiles.md)。

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 歡迎您提供意見回饋，請透過電子郵件發送至 **<aemcs-new-devconsole-ui-beta@adobe.com>**。

![AEM Developer Console 中的 OSGi 套件螢幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

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
