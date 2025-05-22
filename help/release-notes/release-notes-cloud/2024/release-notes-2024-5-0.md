---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.5.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.5.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.5.0) 的發行日期為 2024 年 5 月 30 日。下一個功能版本 (2024.6.0) 預計於 2024 年 6 月 27 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 5 月版本概觀影片，了解 2024.5.0 版本新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Sites 的新功能 {#sites-new-features}

#### AEM 翻譯整合 {#translation-integration}

內容翻譯動作和工作流程現在會觸發事件，允許從外部應用程式追蹤相關流程步驟和狀態。所產生的事件如下所示。使用者將能夠使用 Adobe Developer Console 來訂閱事件。

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### 操作遙測服務 {#real-use-monitoring}

* **[操作遙測服務現在為GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**，可啟用AEM as a Cloud Service的使用者端資料收集。
實際使用監控服務，即用戶端資料收集，可以更準確地反映互動情形，確保網站參與度的測量結果可信。它為客戶提供有關頁面流量和效能的進階深入分析。這是深入了解您的頁面效能並透過深入分析進行改善的絕佳機會。

#### Edge Delivery Services 的 AEM 製作 {#edge-enhancements}

加強穩定性和各種不同的改良功能，提供更好的編寫體驗。

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**在內容片段控制台中瀏覽資產**

內容作者現在可以瀏覽、查看影像，並對影像執行動作，而無需離開內容片段控制台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 aemcs-headless-adopter@adobe.com，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視中的新功能 {#admin-view-new-features}

* WebM 現在是視訊處理設定檔支援的輸出檔案。
* Express 與 AEM 的原生整合現在支援 MP4 (匯入和匯出)。

### Assets 檢視的新功能 {#assets-view-new-features}

**發佈資產至 AEM 和 Dynamic Media**

現在，Experience Manager Assets 讓您無需切換到管理員視圖，而是使用 Assets 視圖快速[將資產發佈到 Experience Manager 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)。您可以在上傳、瀏覽和搜尋資產的同時發佈資產。

![檢查發佈狀態 1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms 的發行前新功能 {#forms-new-prerelease-features}

#### 核心元件式最適化表單的增強型視覺規則編輯器

此版本包含基於核心元件的最適化表單之視覺規則編輯器重大升級。您現在可以：

* 在視覺規則編輯器中建立規則，以[覆寫預設的表單提交成功/失敗訊息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers)。

* 在最適化表單規則編輯器中，新增[為 WHEN 運算選取不同類型欄位](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)的功能。

* 表單製作者現在可以[在提交之前套用自訂函數來預先處理資料](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)。

* 使用「[**儲存為草稿**](/help/forms/save-core-component-based-form-as-draft.md)」功能儲存部分完成的表單，以便日後提交。遇到使用者必須中斷表單填寫並稍後再繼續的情況時，這項功能非常實用。



### AEM Forms 的優先體驗功能 {#forms-new-early-access-features}

AEM Forms 優先體驗計劃為您提供獨一無二的機會，讓您比其他人更早獲得尖端創新的獨家存取權，並協助推動相關開發。您可以透過該計劃存取多項創新。

本發行說明列出目前版本提供的創新功能。如需優先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 優先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 強化機器人保護方法

AEM Forms 新增對於 Cloudflare Turnstile 和 hCaptcha 兩種熱門驗證碼解決方案的支援，藉此強化其安全性功能。這是在既有的 Google reCAPTCHA 以外新增的解決方案，讓使用者擁有更多保護表單的選擇和彈性，避免發生機器人和垃圾郵件提交資料的情況。

* **Cloudflare Turnstile**：這種無摩擦的驗證碼利用不需要明確互動的簡易挑戰來驗證使用者。它與您的表單無縫整合，可提升使用者體驗。
* **hCaptcha**：這種重視隱私的驗證碼提供簡單易用且著重資料隱私權的替代方案。其目的是在安全性和使用者體驗之間取得平衡。
* **Google reCAPTCHA**：AEM Forms 繼續支援 reCAPTCHA v2 和 reCAPTCHA Enterprise，提供可靠且完善的解決方案。

透過提供多個驗證碼選項，AEM Forms 讓您根據自己的具體需求選擇最合適的解決方案。

是否準備好將上述任一驗證碼解決方案與您的最適化表單整合？我們的文件提供各個解決方案的詳細操作指示，包括 [Cloudflare Turnstile](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)、[hCaptcha](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) 和 [Google reCAPTCHA](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components)。


### Forms 服務

Forms 服務會產生用於資料擷取的互動式 PDF forms。也可以利用此表單把資料匯入至現有的互動式 PDF 表單或將其中的資料匯出，並驗證提交的資料。以下是其功能的詳細介紹：

* **轉譯表單**：從使用 AEM Forms Designer 建立的範本，並可以選擇搭配 XML 資料，產生互動式 PDF 表單。這實質上會產生一個可填寫的 PDF 表單，可選擇預先填入資料。
* **資料擷取和匯入**：將資料匯入現有 PDF 表單，以及從已填妥的 PDF 表單中擷取資料。支援 XDP 和 XML 資料格式，而匯入至非 XFA PDF forms (又稱為 AcroForms) 可額外支援 FDF 和 XFDF 資料。
* **資料驗證**：根據使用 AEM Forms Designer 建立的範本驗證以 XDP 或 XML 格式提交的資料。

>[!IMPORTANT]
>
> 如果您有興趣加入我們的優先體驗計劃以使用任何優先體驗創新，請直接從您的正式地址寄送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 要求存取。您可以要求存取所有或任何特定的創新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### OAuth Server-to-Server 認證支援 AEM 與其他 Adobe 解決方案整合 {#S2S-OAuth-credentials}

Adobe Developer Console 是用來產生存取各種 API 的認證。其中一種認證類型，Service Account (JWT) 認證已淘汰，而改為使用 OAuth Server-to-Server 認證；AEM Cloud Service 現在支援該認證與其他 Adobe 解決方案 (例如 Adobe Analytics 和 Adobe Target) 整合。

[閱讀有關淘汰內容的資訊](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)並[了解如何使用 AEM 編寫 UI](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 設定與其他 Adobe 解決方案的整合。

### 來源出現流量尖峰警示 {#traffic-spike-origin}

在來源的流量模式顯示發 DDoS 攻擊時，透過行動中心[接收主動通知](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert)，讓您可以調查和設定流量篩選規則。

### RDE 的新功能 {#RDE-new-features}

[快速開發環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 讓開發人員在雲端中快速部署、審查和測試變更。多項新功能將在 6 月份推出。我們也邀請您到 [RDE Discord 頻道](https://discord.com/channels/1131492224371277874/1245304281184079872)直接與 Adobe 工程部門互動。


#### RDE 支援使用網站主題和網站範本的前端程式碼 {#rde-frontend}

[RDE 現在支援以](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)和[網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)為基礎的前端程式碼，方便早期採用者使用。經由 RDE，我們可以使用命令列指令完成，而不是使用[前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)來完成。

#### 增強 RDE 記錄 {#rde-logging}

在 RDE 中進行程式碼除錯時，開發人員現在可以使用命令列[來設定和串流記錄](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)，生產力更高，而且無需修改版本控制中的 OSGI 屬性。功能包含：

* 根據每個套件或類別層級聲明記錄層級
* 自訂記錄輸出格式
* 並行串流多個記錄

#### RDE CLI 增強功能 {#rde-cli-enhancements}

RDE 命令列介面有一些新功能，可改善開發人員體驗：

* [設定命令是互動式的](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)，可以更輕鬆在組織、計劃和環境之間進行選擇。現在也可以在命令列中覆寫這些值。
* [靜音模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)提供較簡潔的輸出。
* [json 模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)可在以程式設計方式呼叫時，提供實用的輸出。

### 新的行動中心通知 {#actions-center-notifications}

有重要事件發生時，或是我們注意到您的程式碼或設定中有些問題需要主動採取行動時，[行動中心](/help/operations/actions-center.md)就會寄送電子郵件通知。有三個新的通知類型：

* 透過進階網路基礎結構進行的傳出連線過多
* 使用已淘汰的服務使用者對應格式
* 有潛在的 DDoS 攻擊正在進行中

### 早期採用者計劃 {#foundation-early-adopter}

請寄送電子郵件至 **<aemcs-cdn-config-adopter@adobe.com>**，指出您對以下哪些早期採用者計劃感興趣。

#### 使用自助 API 金鑰清除內容傳遞網路上的內容 (早期採用者計畫) {#purge-cdn}

以自助方式註冊內容傳遞網路清除 API 金鑰，並利用它使內容傳遞網路上的內容失效，無論是全域或針對一個或多個資源。[了解更多](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 為客戶管理的內容傳遞網路 (BYOCDN) 自助建立 X-AEM-Edge-Key (早期採用者計劃) {#byocdn-keys}

以前，需要支援服務單才能產生設定客戶管理之內容傳遞網路所需的 X-AEM-Edge-Key。現在則可以透過使用設定管道部署的設定檔，以自助方式完成此操作，因此新環境上線不會有任何延遲。[了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 伺服器端重新導向（早期採用者計畫） {#server-side-redirects-early-adopter}

在原始檔控制中設定301/302伺服器端重新導向，並部署至CDN。 [了解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 請注意，已經有一些與[內容傳遞網路設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)相關的其他功能可用，包括要求和回應轉換，以及將流量路由到 AEM 之外的網站。

#### 流量篩選規則警報 (早期採用者計畫) {#traffic-filter-rules-alerts-early-adopter}

最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包括可授權選項的 Web 應用程式防火牆 (WAF) 規則) 可讓您設定應該允許或拒絕哪些流量。

加入早期採用者計劃，您就可以在流量篩選規則觸發時收到提醒。發生某些流量狀況時，行動中心電子郵件通知會通知您，以利採取適當措施。

#### 業務使用者可以在 Git 之外宣告重新導向 (早期採用者計劃) {#apache-rewritemaps-early-adopter}

與 AEM 6.5 類似，Apache/Dispatcher 將收錄放在發佈存放庫中特定位置的重新寫入對應並將其載入，而不需要執行 Web 層級管道。商業使用者因此有機會使用試算表或 UI (例如由 ACS Commons Redirect Map Manager 提供或做為客戶應用程式的一部分建立者) 來宣告重新導向。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 用來載入動態內容的 Edge Side Includes (ESI) (早期採用者計劃) {#esi-early-adopter}

Adobe 管理的內容傳遞網路現在支援 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，這是一種用於邊緣層級動態 Web 內容組合的標記語言。透過包含 ESI 程式碼片段，您可以在內容傳遞網路上用較高的 TTL 快取整個 HTML 頁面，同時更頻繁地從來源擷取需要較高更新頻率 (TTL 較低) 的較小區段。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guides {#guides}

* **將主題或其元素發佈到體驗片段**
現在，Experience Manager Guides 讓您可以將主題或其元素發佈到體驗片段。體驗片段是整合內容和版面的模組化內容單元。體驗片段很有用，可以協助您建立一致且引人入勝的體驗。
* **能夠將主題資產中繼資料傳遞至原生 PDF 輸出**
您可以在產生原生 PDF 輸出時新增主題資產中繼資料。此功能可協助您將不同主題的特定中繼資料 (例如主題標題和製作者) 新增至主題頁面的頁首和頁尾。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## Experience Cloud 發行說明 {#experience-cloud}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/release-notes/experience-cloud/current)查看其他 Experience Cloud 應用程式版本的相關資訊。若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。
