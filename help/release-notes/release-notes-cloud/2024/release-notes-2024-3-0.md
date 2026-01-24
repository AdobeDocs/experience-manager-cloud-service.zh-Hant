---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0 版發行說明。'
exl-id: b3816929-2c0a-4d6a-b583-c928d2182ecd
feature: Release Information
role: Admin
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.3.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.3.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2021 或 2022。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hant)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2024.3.0) 的發行日期是 2024 年 4 月 11 日。下一個功能版本 (2024.4.0) 預計於 2024 年 4 月 25 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 3 月發行概觀影片，以了解 2024.3.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3450370?quality=12&captions=chi_hant)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新功能 {#sites-features}

**Edge Delivery Services 的 AEM 製作**

AEM Sites 現在可以用作 Edge Delivery Services 的內容來源。作者可使用內容 WYSIWYG 製作中的新 Universal Editor，在 AEM 中管理他們的網站。這樣做可讓公司能夠利用 Edge Delivery Services 來建立快速的高效能網頁，同時利用 AEM 強大的內容管理功能。

![AEM 製作](/help/edge/assets/universal_editor_edge_delivery_services.png)

若要了解更多資訊，請參閱[文件](/help/edge/overview.md)並觀看 [AEM Gems - 開始使用 AEM Authoring 和 Edge Delivery Services](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694?profile.language=zh-Hant#M43905)

**Headless 實作的 Universal Editor**

Universal Editor 還可讓分離的 Web 應用程式利用直觀內容 WYSIWYG 製作，這在以前僅適用於傳統網站。內容建立者現在可以使用內容片段以直觀方式建立版面配置，就如同在頁面中使用元件一樣輕鬆。

Universal Editor 與眾不同之處在於此工具適用於各種不同的 Web 架構，可容納伺服器端和用戶端的呈現、保持無框架狀態，且無需 AEM 託管。將現有 Web 應用程式與 Universal Editor 整合並進行內容編輯非常簡單，主要是需要開發人員將特定的資料屬性合併到其標記中。

這樣，無論內容結構或底層技術堆疊如何，Universal Editor 都可以確保一致的編輯體驗。若要了解更多資訊，請參閱「[Universal Editor 簡介](/help/implementing/universal-editor/introduction.md)」。

**適用於內容片段和模式的內容管理 OpenAPI**

開發人員現在可以編程方式與內容片段和內容片段模式互動，並可使用內容管理 OpenAPI 對他們執行 CruD 操作。如需詳細資訊，請參閱「[API 文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)」。

**對體驗片段的多網站管理支援**

多網站管理支援已擴展到儲存體驗片段的資料夾結構，允許使用者推出包含體驗片段的完整內容結構。

**比較內容片段版本**

新的內容片段編輯器現在允許內容作者比較和查看內容片段現有版本與先前版本之間的差異。

### 早期採用者計劃 {#sites-early-adopter}

**產生變化版本**

透過 AEM 新功能「[產生變化版本](/help/generative-ai/generate-variations.md)」運用 GenAI；此功能現在可於雲端服務中存取。產生變化版本可協助您透過使用生成式 AI 來產生和擴展內容建立。請聯絡您的 Adob&#x200B;&#x200B;e 客戶團隊以考慮參與該計劃。

**在內容片段控制台中瀏覽資產**

內容作者現在可以瀏覽、查看影像，並對影像執行動作，而無需離開內容片段控制台。

![資產瀏覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

有興趣嘗試該功能並分享回饋意見嗎？從您的官方電子郵件 ID 傳送電子郵件到 aemcs-headless-adopter@adobe.com，深入了解有關早期採用者計劃的資訊。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理員檢視中的新功能 {#admin-view}

**與 Adobe Express 原生整合**

AEM Assets 可與 Adobe Express 自然整合，讓您從 Adobe Express 使用者介面直接存取 AEM Assets 儲存的資源。您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。

![包括資產附加元件中的資產](/help/assets/assets/adobe-express-native-integration.png)

**預覽所有支援影片類型的轉譯版**

Experience Manager Assets 現在會依預設產生所有支援影片類型的預覽轉譯，而無需處理設定檔的設定。

### 資產檢視中的新功能 {#assets-view}

**管理集合權限**

Assets Essentials 可讓管理員管理存放庫中專用集合的存取層級。身為管理員，您可建立使用者群組並指派權限給這些群組，以管理存取層級。您還可以將權限管理權委派給使用者群組。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms 的新功能 {#forms-new-features}

* **[Adobe Experience Manager Forms Edge Delivery Services](/help/edge/docs/forms/overview.md)**：適用於AEM Forms的Edge Delivery Services是一組可撰寫的服務，可啟用快速開發環境，讓作者可快速更新、發佈和啟動新表單。 這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

  ![EDS 表單功能](/help/edge/assets/eds-forms-features.png)

這些服務可讓您：

* 在同一個表單網站上使用多個內容來源，並使用您偏好的製作工具，例如 Microsoft Excel、Google Sheets 或最適化表單編輯器。
* 提供數位註冊體驗，透過操作遙測快速且持續地載入及轉譯您的表單效能。
* 使用純 HTML、現代 CSS 和普通 JavaScript 來建立卓越的體驗，避免特定框架出現陡峭學習曲線。


### 發行前版本的 AEM Forms 新功能 {#forms-pre-release}

* **核心元件式最適化表單的增強型視覺規則編輯器**：此版本針核心元件式最適化表單的視覺規則編輯器進行重大升級。此版本對核心元件式最適化表單的視覺規則編輯器進行重大升級。此更新著重於簡化與自訂函數的互動，讓您能夠建立更強大、更有效率的表單。

  現在您可以透過以下方式簡化自訂函數互動：

   * 運用新註解以提供更清楚的函式定義。
   * 針對自訂函式使用快取機制，以提高表單效能。
   * 可順暢地使用自訂函式中的全域物件。
   * 在自訂函式中定義及使用選用引數。

  此更新還增強以下規則編輯器功能。您可以：

   * 針對條件式執行實作強大的「when-then-else」邏輯。
   * 利用現代 JavaScript 功能，如 let 和箭頭函數 (ES10 支援)。
   * 不僅可驗證或重設欄位，還可驗證或重設整個面板和表單，以擴大對使用者互動的控制。

  在視覺規則編輯器中建立規則和自訂函數時，這方面的進步可提供更直觀、更強大的體驗。

* **建立多版本的最適化表單**：您現在可以輕鬆管理現有表單的變化版本。這簡化了版本控制並可促進表單最佳化的比較，所有都可在一個簡化的工作流程中進行。

* **比較最適化表單**：您現在可以輕鬆比較兩個表單，識別兩個表單之間的差異。這可方便團隊成員有效地比較修訂版本並討論變更，進而讓成員可順利協作。

* **手寫簽名元件的協助工具功能增強**：這項更新為手寫簽名元件提供顯著的協助工具功能改善：

  **經改善的鍵盤導覽：**
   * 按 Tab 鍵允許使用者瀏覽簽章對話方塊中的所有互動元素。
   * 使用筆刷或鍵盤來簽名，並按 Enter 鍵關閉對話方塊。
   * 簽名並按一下「確定」後，仍然要著重簽署控制。

  **清除簽名功能：**

   * 可透過 Tab 鍵存取用來擦拭簽名的清除十字圖示。
   * 還可透過標籤導覽來存取「清除簽名確認」對話方塊。

  **增強的標籤和控制項：**
   * 鍵盤簽名按鈕的標籤現在更加清晰，使用「aria-label」來宣布功能 (例如「aria-label=&#39;Sign using Keyboard&#39;」)。
   * 改善的對比度可確保手寫簽名中的所有控制都項都易於區分。
   * 確定/勾選標記按鈕現在可以視覺方式表明功能為非使用狀態。

  **螢幕閱讀器的簽名意見回饋：**
   * 輸入簽名時，螢幕閱讀器使用者可以聽到用來建立簽名的文字。

此更新改善了手寫簽名元件的導覽、清晰度和意見回饋，可確保為殘障使用者提供更具包容性的體驗。

### 早期採用者計劃 {#forms-early-adopter}

* **[將最適化表單提交到 Adobe Workfront Fusion 情境](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供開箱即用的選項，可輕鬆將最適化表單與 Adobe Workfront 連接。這簡化了將最適化表單提交到 Adobe Workfront 情境的程序，讓您在提交最適化表單時觸發 Workfront Fusion 情境。

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> 使用 Adob&#x200B;&#x200B;e Workfront Fusion Connector，您可以設計在提交最適化表單時自動觸發的工作流程。例如，設想這樣一個場景：啟動工作流程以便將審查提交資料的任務分配給特定個人，進而允許根據透過最適化表單擷取的資訊來核准或拒絕申請。這種簡化的整合方式提高了效率，並為您的工作流程帶來了全新的自動化層級。

* **Reader 延伸模組服務**：AEM Forms Communication API 引入了 Reader 延伸模組服務，讓您可以為一般的 PDF 新增表單填寫和評論等功能，讓免費 Adob&#x200B;&#x200B;e Reader 的使用者可使用這些功能。

* [從右至左語言支援](/help/forms/supporting-new-language-localization-core-components.md)：以核心元件為主的最適化表單現在可以呈現從右至左 (RTL) 語言 (如阿拉伯文、波斯文和烏都文)。全球有超過 20 億人使用 RTL 語言。使用 RTL 語言的表單可讓您擴展最適化表單的範圍，以滿足這些不同的客群並選擇進入 RTL 市場。在某些地區，法律也強制要求以當地語言提供表單。透過適應當地語言，您不僅可以向更廣泛的客群敞開大門，還可以確保遵守相關法律和法規。

* **[使用 DocAssurance API (通訊 API 的一部分) 保護您的文件](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 可讓您透過在文件上簽名和加密來保護敏感資訊。透過加密，文件內容會被轉換為不可讀的格式，確保只有授權的使用者才能存取。這個強化的保護層不僅可以防止重要資料受到未經授權的查看，還可以讓您高枕無憂。簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。

  您可以透過您的官方電子郵件 ID 寫信給 `aem-forms-ea@adobe.com`，加入早期採用者計畫並要求存取該功能。

* **[您可以利用作業遙測服務](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;來啟用AEM as a Cloud Service的使用者端集合。
作業遙測服務可更精確地反映使用者互動，確保網站互動的可靠測量。 這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。此外，對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

  如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至`aemcs-rum-adopter@adobe.com`，連同您想要從與Adobe ID關聯的電子郵件地址為每個環境啟用作業遙測的網域名稱。 Adobe的產品團隊會接著為您啟用作業遙測服務。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 早期採用者計劃 {#foundation-early-adopter}

#### 流量篩選規則警報 (早期採用者計畫) {#traffic-filter-rules-alerts-early-adopter}

最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包括可授權選項的 Web 應用程式防火牆 (WAF) 規則) 可讓您設定應該允許或拒絕哪些流量。

現在您可以發送電子郵件 **<aemcs-cdn-config-adopter@adobe.com>** 加入早期採用者計劃，以便您在流量篩選規則被觸發時收到提醒。當發生某些流量狀況時，行動中心電子郵件通知將通知您，以便您採取適當的措施。

#### 網域對應（早期採用者計畫） {#cdn-config-early-adopter}

除了最近發佈的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) (其中包含可以選擇授權的 Web 應用程式防火牆 (WAF) 規則)，也可以使用設定管道來聲明及部署其他類型的 CDN 設定。[了解更多](/help/implementing/dispatcher/cdn-configuring-traffic.md)並加入早期採用者計劃，可發送電子郵件 **<aemcs-cdn-config-adopter@adobe.com>** 取得存取權限：

* 301/302伺服器端重新導向
* 將邊緣要求代理到任意來源 (例如非 AEM 應用程式)
* URL 轉換
* 設定或修改要求或回應標頭
* CDN 無法連接 AEM 時的自訂錯誤頁面

#### 重新寫入對應的 Apache/Dispatcher 執行時間擷取 (早期採用者計畫) {#apache-rewritemaps-early-adopter}

與 AEM 6.5 類似，Apache/Dispatcher 將擷取放在發佈存放庫中特定位置的重新寫入對應並將其載入，而不需要 Web 層級的管道執行。這讓商業使用者有機會使用 UI 來聲明重新導向，例如 ACS Commons Redirect Map Manager 提供的 UI。請聯絡 **<aemcs-cdn-config-adopter@adobe.com>** 了解更多。

#### 用來載入動態內容的 Edge Side Includes (ESI) (早期採用者計畫) {#esi-early-adopter}

Adobe Managed CDN 現在支援 Edge Side Includes (ESI)，這是一種用於邊緣層級動態 Web 內容組合的標記語言。透過包含 ESI 程式碼段，您可以在具有較高 TTL 的 CDN 上快取整個 HTML 頁面，同時更頻繁地從來源取得需要較高節奏更新 (較低 TTL) 的較小區段。請聯絡 **<aemcs-cdn-config-adopter@adobe.com>** 了解更多。

#### 使用網站主題和網站範本對前端程式碼的 RDE 支援 (早期採用者計劃) {#rde-frontend-early-adopter}

[快速開發環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 現在支援以[網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)和[網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)為主的前端程式碼 (適用於早期採用者)。對於 RDE，這是使用命令列指令完成，而不是使用 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)來完成。請聯絡 **<aemcs-rde-support@adobe.com>**，要求嘗試並提供意見回饋。

#### 增強的 RDE 記錄 (早期採用者計劃) {#rde-logging-early-adopter}

在[快速開發環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 中進行程式碼除錯時，開發人員現在可以使用命令列更有效設定和串流記錄，而無需修改版本控制中的 OSGI 屬性。功能包含：

* 在每個套件或類別層級聲明記錄層級
* 自訂記錄輸出格式
* 並行串流多個記錄

請聯絡 **<aemcs-rde-support@adobe.com>**，要求嘗試並提供意見回饋。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。
