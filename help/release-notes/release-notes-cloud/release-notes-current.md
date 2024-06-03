---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: f8fc51051393ef154e02391843fe1e73e6194e6f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 30%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本(2024.5.0)為2024年5月30日。 下一個功能版本(2024.6.0)計畫於2024年6月27日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看2024年5月版本概觀影片，瞭解2024.5.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 網站中的新功能 {#sites-new-features}

**Edge Delivery Services 的 AEM 製作**

增強的穩定性及各種改良功能，提供更出色的撰寫體驗。

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**在內容片段控制台中瀏覽資產**

內容作者現在可以瀏覽、查看影像，並對影像執行動作，而無需離開內容片段控制台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 aemcs-headless-adopter@adobe.com，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視中的新功能 {#admin-view-new-features}

* WebM現在是處理視訊設定檔時支援的輸出檔案。
* AEM in Express的原生整合（匯入和匯出）現在支援MP4。

### 資產檢視中的新功能 {#assets-view-new-features}

**將資產發佈到AEM和Dynamic Media**

Experience Manager Assets現在可讓您快速 [將資產發佈到Experience Manager和Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) 使用「資產」檢視，而不切換至「管理員」檢視。 您可以在上傳、瀏覽和搜尋資產時發佈資產。

![檢查發佈狀態1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms中的新搶鮮版功能 {#forms-new-prerelease-features}

#### 核心元件型最適化Forms的增強視覺規則編輯器

此版本對核心元件式最適化表單的視覺規則編輯器進行重大升級。您現在可以：

* 在視覺規則編輯器中建立規則以 [覆寫預設表單提交成功/失敗訊息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* 在最適化Forms規則編輯器中，新增以下功能 [為WHEN作業選取不同型別的欄位](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* 表單作者現在可以將自訂函式套用至 [提交前先行處理資料](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* 使用 [**另存為草稿**](/help/forms/save-core-component-based-form-as-draft.md) 儲存部分完成的表單以供稍後提交的功能。 當使用者需要中斷填寫表單並稍後返回表單時，這將很有用。



### AEM Forms中的早期採用者功能 {#forms-new-early-adopter-features}

AEM Forms早期採用者計畫為您提供獨一無二的機會，讓您搶在其他人之前取得尖端創新的存取權，並幫助塑造其開發。
此計畫提供多種創新的存取權。

本發行說明列出目前版本中推出的創新功能。 如需早期採用者計畫下可用的創新完整清單，請參閱 [AEM Forms早期採用者計畫檔案](/help/forms/early-adopter-ea-features.md).

#### 增強的機器人保護方法

AEM Forms已新增兩個熱門驗證碼解決方案的支援，以加強其安全性功能：Cloudflare Turnstile和hCaptcha。 這為現有的Google reCAPTCHA增添了功能，讓使用者在保護表單免受機器人和垃圾郵件提交影響時，擁有更多選擇和靈活性。

* **Cloudflare Turnstile**：此順暢的驗證碼可透過不需要明確互動的簡單挑戰來驗證使用者。 它可順暢地整合至您的表單中，進而改善使用者體驗。
* **驗證碼**：此針對隱私權的驗證碼提供使用者易用的替代方案，著重於資料隱私權。 其目標是在安全性與使用者體驗之間取得平衡。
* **Google reCAPTCHA**： AEM Forms持續支援reCAPTCHA v2和reCAPTCHA Enterprise，提供穩定可靠的成熟解決方案。

透過提供多個驗證碼選項，AEM Forms可讓您選擇最符合您特定需求的解決方案。

準備好將任何這些驗證碼解決方案與您的Adaptive Forms整合了嗎？ 本檔案提供各項的詳細指示： [Cloudflare Turnstile](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)， [驗證碼](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、和 [Google reCAPTCHA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms 服務

Forms服務會產生互動式PDF forms以進行資料擷取。 它也可以用來匯入現有互動式PDF表單的匯出資料，以及驗證提交的資料。 其功能劃分如下：

* **呈現Forms**：從使用AEM Forms Designer建立的範本產生互動式PDF表單，並可選擇產生XML資料。 這基本上會產生一個可填寫的PDF表單，可選擇預先填入資料。
* **資料擷取和匯入**：將資料匯入現有的PDF表單，並從已填寫的PDF表單中擷取資料。 支援XDP和XML資料格式，並且匯入到非XFAPDF forms（也稱為AcroForms）還支援FDF和XFDF資料。
* **資料驗證**： ：根據使用AEM Forms Designer建立的範本，驗證XDP或XML格式的已提交資料。

>[!IMPORTANT]
>
> 如果您有興趣加入我們的早期採用者計畫，以進行任何早期採用者創新，只要將您的官方地址中的電子郵件傳送至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 以要求存取權。 您可以要求存取所有或任何特定的創新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### AEM與其他Adobe解決方案整合的OAuth伺服器對伺服器憑證支援 {#S2S-OAuth-credentials}

Adobe Developer Console可產生存取各種API的認證。 其中一種認證型別，服務帳戶(JWT)認證，已遭取代以支援OAuth伺服器對伺服器認證，AEM Cloud Service現在支援將其與其他Adobe解決方案(例如Adobe Analytics和Adobe Target)整合。

[閱讀有關棄用的資訊](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) 和 [瞭解如何使用AEM作者UI](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 以設定與其他Adobe解決方案的整合。

### 來源警示的流量尖峰 {#traffic-spike-origin}

[接收主動通知](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) 當來源處的流量模式顯示DDoS攻擊時，可透過Actions Center進行檢查，讓您能夠調查並設定流量篩選規則。

### RDE的新功能 {#RDE-new-features}

[快速開發環境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 讓開發人員快速部署、檢閱及測試雲端中的變更。 有數項新功能將在6月期間推出。 我們也邀請您直接參與Adobe工程部的 [RDE不和諧通道](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### 使用網站主題和網站範本的前端計畫碼RDE支援 {#rde-frontend}

[RDE現在支援前端計畫碼](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) 根據 [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md) 和 [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)，適用於早期採用者。 若使用RDE，這是使用命令列指示詞完成的，而非 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### 增強RDE的記錄功能 {#rde-logging}

在RDE中偵錯程式碼時，開發人員現在可以 [更有效率地設定和串流記錄檔](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)，使用命令列，且無需修改版本控制中的OSGI屬性。 功能包含：

* 在每個套件或類別層級上宣告記錄層級
* 自訂日誌輸出格式
* 並行串流多個記錄檔

#### RDE CLI增強功能 {#rde-cli-enhancements}

RDE命令列介面有一些新功能，可改善開發人員體驗：

* [setup指令是互動式的](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)，讓您更輕鬆地在組織、方案和環境之間進行選擇。 現在也可以在命令列覆寫這些值。
* [安靜模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) 以取得較不詳細的輸出。
* [json模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) 以程式呼叫時用於有用的輸出。

### 新動作中心通知 {#actions-center-notifications}

[動作中心](/help/operations/actions-center.md) 當重要事件發生時，或當我們注意到您的程式碼或設定中您應該採取主動行動的內容時，會傳送電子郵件通知。 有三種新型別的通知：

* 透過進階網路基礎架構的傳出連線太多
* 使用過時的服務使用者對應格式
* 潛在的DDoS攻擊正在進行

### 早期採用者計劃 {#foundation-early-adopter}

電子郵件 **<aemcs-cdn-config-adopter@adobe.com>**，指出您對下列哪些早期採用者程式感興趣。

#### 使用自助式API金鑰清除CDN的內容（早期採用計畫） {#purge-cdn}

以自助方式註冊CDN清除API金鑰，並使用它來使CDN的內容（全域或一個或多個資源）失效。 [了解更多](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 針對客戶管理的CDN (BYOCDN)自助建立X-AEM-Edge-Key （早期採用計畫） {#byocdn-keys}

之前，需要支援票證來產生設定客戶管理的CDN所需的X-AEM-Edge-Key。 現在可以自助方式透過使用設定管道部署的設定檔案完成此操作，消除了新環境上線中的任何延遲。 [了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 用戶端重新導向 (早期採用者計畫) {#client-side-redirects-early-adopter}

在原始碼控制系統中設定 301/302 用戶端重新導向，並部署到 CDN。[了解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 請注意，還有許多其他功能與相關 [CDN設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)，包括請求和回應轉換，以及將流量路由至AEM以外的網站。

#### 流量篩選規則警報 (早期採用者計畫) {#traffic-filter-rules-alerts-early-adopter}

最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包括可授權選項的 Web 應用程式防火牆 (WAF) 規則) 可讓您設定應該允許或拒絕哪些流量。

加入早期採用者計畫，以便在流量篩選器規則觸發時收到警報。 當發生某些流量狀況時，行動中心電子郵件通知將通知您，以便您採取適當的措施。

#### 商務使用者可以在Git外部宣告重新導向（早期採用計畫） {#apache-rewritemaps-early-adopter}

與 AEM 6.5 類似，Apache/Dispatcher 將擷取放在發佈存放庫中特定位置的重新寫入對應並將其載入，而不需要 Web 層級的管道執行。這開啟了商業使用者使用試算表或UI宣告重新導向的機會，例如ACS Commons重新導向地圖管理員提供或建立為客戶應用程式一部分的重新導向。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 用來載入動態內容的 Edge Side Includes (ESI) (早期採用者計畫) {#esi-early-adopter}

Adobe Managed CDN現在支援 [Edge Side Include (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，邊緣層級動態網頁內容元件的標籤語言。 加入ESI程式碼片段，您就能快取CDN的整體HTML頁面，其中包含較高TTL，同時更頻繁地從來源擷取需要較高步調更新（較低TTL）的較小區段。 <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

#### Real User Monitoring (RUM) Data Service (Early Adopter Program)

* **[您可以利用真實使用者監控 (RUM) 資料服務](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;啟用 AEM as a Cloud Service 的用戶端系列。真實使用者監控 (RUM) 資料服務可以更準確地反映使用者互動，確保可靠地測量網站參與度。這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。此外，對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

  如果您有興趣測試此新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件地址，傳送電子郵件至 `aemcs-rum-adopter@adobe.com`，並在郵件中附上要啟用 RUM 的每個環境網域名稱。Adobe 的產品團隊隨後會為您啟用真實使用者監控 (RUM) 資料服務。

## [!DNL Experience Manager] Guides {#guides}

您可以找到最新版Adobe Experience Manager Guides完整的新功能與增強功能清單 [此處](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2404-release/whats-new-2024-04-0).

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
