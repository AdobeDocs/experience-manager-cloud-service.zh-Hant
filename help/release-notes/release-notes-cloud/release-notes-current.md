---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 19b52f733a592c7e84ba2e9d83d37e5e181f21ab
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 57%

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
>請參閱[近期文件更新](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2024.6.0)為2024年6月27日。 下一個功能版本(2024.7.0)計畫於2024年7月25日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**在內容片段控制台中瀏覽資產**

內容作者現在可以瀏覽、查看影像，並對影像執行動作，而無需離開內容片段控制台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 aemcs-headless-adopter@adobe.com，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Experience Manager Assets中的新功能 {#new-features-assets}

**Content Hub**

Content Hub是Experience Manager Assets as a Cloud Service的一部分，可讓組織及其業務合作夥伴普及對品牌上內容的存取。 透過Content Hub，您可以輕鬆尋找及發佈資產、重複使用和建立新的品牌上變體，並大規模加速啟用。

![Content Hub使用者介面](/help/release-notes/assets/content-hub-ui.png)

**具有OpenAPI功能的Dynamic Media**

Dynamic Media搭配OpenAPI功能，可跨Adobe和第三方應用程式延伸DAM，讓您可透過任何管道的Asset Selector或OpenAPI棧疊存取品牌核准的數位資產。 重要原則 — 無二進位副本，資產在邊緣經過最佳化和轉換，以實現快速效能、提供公開或安全的資產。

![新的Dynamic Media資料流程圖](/help/assets/assets/dm-openapi-dfd.png)


### Assets 檢視的新功能 {#assets-view-new-features}

**Assets Insights儀表板中有更多可用選項**

Assets Insights儀表板現在提供依資產型別和大小排列的資產計數。 這些選項可在您的Assets檢視環境中提供按大小範圍和資產型別分類的資產計數和百分比的即時資料。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms 的新功能 {#forms-new-prerelease-features}

#### 核心元件式最適化表單的增強型視覺規則編輯器

此版本包含基於核心元件的最適化表單之視覺規則編輯器重大升級。您現在可以：

* 在視覺規則編輯器中建立規則以 [覆寫預設表單提交成功/失敗訊息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* 在最適化表單規則編輯器中，新增[為 WHEN 運算選取不同類型欄位](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)的功能。

* 表單製作者現在可以[在提交之前套用自訂函數來預先處理資料](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)。

* 使用「[**儲存為草稿**](/help/forms/save-core-component-based-form-as-draft.md)」功能儲存部分完成的表單，以便日後提交。遇到使用者必須中斷表單填寫並稍後再繼續的情況時，這項功能非常實用。

### AEM Forms中的搶先使用功能 {#forms-new-early-access-features}

AEM Forms搶先體驗計畫提供絕佳機會，讓您可以搶在其他人之前獨佔使用最尖端的創新技術，並協助打造他們的開發成果。 您可以透過該計劃存取多項創新。

本發行說明列出目前版本中提供的創新內容。 如需「搶先體驗方案」下可用的創新完整清單，請參閱 [AEM Forms搶先使用計畫檔案](/help/forms/early-access-ea-features.md).

#### 強化機器人保護方法

AEM Forms 新增對於 Cloudflare Turnstile 和 hCaptcha 兩種熱門驗證碼解決方案的支援，藉此強化其安全性功能。這是在既有的 Google reCAPTCHA 以外新增的解決方案，讓使用者擁有更多保護表單的選擇和彈性，避免發生機器人和垃圾郵件提交資料的情況。

* **Cloudflare Turnstile**：這種無摩擦的驗證碼利用不需要明確互動的簡易挑戰來驗證使用者。它與您的表單無縫整合，可提升使用者體驗。
* **hCaptcha**：這種重視隱私的驗證碼提供簡單易用且著重資料隱私權的替代方案。其目的是在安全性和使用者體驗之間取得平衡。
* **Google reCAPTCHA**：AEM Forms 繼續支援 reCAPTCHA v2 和 reCAPTCHA Enterprise，提供可靠且完善的解決方案。

透過提供多個驗證碼選項，AEM Forms 讓您根據自己的具體需求選擇最合適的解決方案。

是否準備好將上述任一驗證碼解決方案與您的最適化表單整合？我們的文件提供各個解決方案的詳細操作指示，包括 [Cloudflare Turnstile](https://experienceleague.adobe.com/tw/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)、[hCaptcha](https://experienceleague.adobe.com/tw/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) 和 [Google reCAPTCHA](https://experienceleague.adobe.com/tw/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components)。


### Forms 服務

Forms 服務會產生用於資料擷取的互動式 PDF forms。它也可以用來匯入或匯出現有互動式PDF表單的資料，以及驗證提交的資料。 以下是其功能的詳細介紹：

* **轉譯表單**：從使用 AEM Forms Designer 建立的範本，並可以選擇搭配 XML 資料，產生互動式 PDF 表單。這實質上會產生一個可填寫的 PDF 表單，可選擇預先填入資料。
* **資料擷取和匯入**：將資料匯入現有 PDF 表單，以及從已填妥的 PDF 表單中擷取資料。支援 XDP 和 XML 資料格式，而匯入至非 XFA PDF forms (又稱為 AcroForms) 可額外支援 FDF 和 XFDF 資料。
* **資料驗證**：根據使用 AEM Forms Designer 建立的範本驗證以 XDP 或 XML 格式提交的資料。

>[!IMPORTANT]
>
> 如果您有興趣加入我們的搶先存取計畫以進行任何搶先存取創新，只要從您的官方地址傳送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 以要求存取權。 您可以要求存取所有或任何特定的創新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 內容健康相關動作中心通知早期採用者計畫 {#actions-center-notifications}

有重要事件發生時，或是我們注意到您的程式碼或設定中有些問題需要主動採取行動時，[行動中心](/help/operations/actions-center.md)就會寄送電子郵件通知。我們現在推出了數種與您的內容健康狀態相關的新通知型別。 這可透過早期採用者計畫取得。 若要參與，請聯絡Adobe客戶服務。

#### 頁面包含大量節點 {#page-nodes}

大量節點可能會降低演算效能並減少頁面載入時間。 在頁面上偵測到大量節點時，會透過動作中心接收主動通知，允許您採取必要步驟來減少頁面內的節點總數。

#### 大量執行中的工作流程例項 {#running-workflows}

當製作環境中有大量執行中的工作流程時，工作流程引擎效能會受到影響。 偵測到大量執行中的工作流程例項時，請透過「動作中心」接收主動通知，讓您設定清除工作以終止不需要的執行中的工作流程。

#### 直接新增到自訂群組的使用者 {#users-customgroups}

當使用者直接新增到自訂群組時，會透過動作中心收到主動通知，允許您遵循IMS最佳實務將使用者新增到相關的IMS群組，然後將IMS群組新增為AEM群組的成員。

#### 缺少 JCR 內容 {#jcr-content}

偵測到缺少JCR內容時，會透過動作中心收到主動通知，讓您新增缺少的JCR內容並避免某些AEM Assets功能失敗。

#### 已完成的工作流程未清除 {#workflows}

當超過90天未清除已完成的工作流程時，會透過「動作中心」收到主動通知，可讓您透過減少工作流程例項數量來改善工作流程引擎的效能。

#### 缺少Sling資源 {#sling-resource}

偵測到缺少Sling資源時，會透過動作中心接收主動通知，允許您新增缺少的Sling資源並避免某些AEM Assets功能失敗。

### 內容傳遞相關的早期採用者計畫 {#foundation-early-adopter}

請寄送電子郵件至 **<aemcs-cdn-config-adopter@adobe.com>**，指出您對以下哪些早期採用者計劃感興趣。

#### CDN的基本驗證（早期採用者計畫） {#basicauth-cdn}

Protect會彈出基本驗證對話方塊，要求使用者名稱和密碼，以顯示特定內容資源。 此功能主要用於輕度驗證使用案例（例如業務利害關係人審查內容），而不是作為一般使用者存取權的完整解決方案。 透過透過設定管道部署的Git中的設定檔案來管理中的使用者名稱和密碼清單，並參考機密型別Cloud Manager環境變數。 [了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### 使用自助式API金鑰清除CDN的內容（早期採用計畫） {#purge-cdn}

以自助方式註冊內容傳遞網路清除 API 金鑰，並利用它使內容傳遞網路上的內容失效，無論是全域或針對一個或多個資源。[了解更多](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 自助建立客戶管理的CDN的X-AEM-Edge-Key (BYOCDN) （早期採用計畫） {#byocdn-keys}

以前，需要支援服務單才能產生設定客戶管理之內容傳遞網路所需的 X-AEM-Edge-Key。現在則可以透過使用設定管道部署的設定檔，以自助方式完成此操作，因此新環境上線不會有任何延遲。[了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 使用者端重新導向（早期採用者計畫） {#client-side-redirects-early-adopter}

在原始碼控制系統中設定 301/302 用戶端重新導向，並部署到 CDN。[了解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 請注意，已經有一些與[內容傳遞網路設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)相關的其他功能可用，包括要求和回應轉換，以及將流量路由到 AEM 之外的網站。

#### 流量篩選規則警報 (早期採用者計畫) {#traffic-filter-rules-alerts-early-adopter}

最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包括可授權選項的 Web 應用程式防火牆 (WAF) 規則) 可讓您設定應該允許或拒絕哪些流量。

加入早期採用者計劃，您就可以在流量篩選規則觸發時收到提醒。發生某些流量狀況時，行動中心電子郵件通知會通知您，以利採取適當措施。

#### 商務使用者可以在Git外部宣告重新導向（早期採用計畫） {#apache-rewritemaps-early-adopter}

與 AEM 6.5 類似，Apache/Dispatcher 將收錄放在發佈存放庫中特定位置的重新寫入對應並將其載入，而不需要執行 Web 層級管道。商業使用者因此有機會使用試算表或 UI (例如由 ACS Commons Redirect Map Manager 提供或做為客戶應用程式的一部分建立者) 來宣告重新導向。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 用來載入動態內容的 Edge Side Includes (ESI) (早期採用者計劃) {#esi-early-adopter}

Adobe 管理的內容傳遞網路現在支援 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，這是一種用於邊緣層級動態 Web 內容組合的標記語言。透過包含 ESI 程式碼片段，您可以在內容傳遞網路上用較高的 TTL 快取整個 HTML 頁面，同時更頻繁地從來源擷取需要較高更新頻率 (TTL 較低) 的較小區段。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guides {#guides}

您可以找到最新版Adobe Experience Manager Guides完整的新功能與增強功能清單 [此處](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## Experience Cloud 發行說明 {#experience-cloud}

您可以在[這裡](https://experienceleague.adobe.com/tw/docs/release-notes/experience-cloud/current)查看其他 Experience Cloud 應用程式版本的相關資訊。若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。
