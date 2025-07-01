---
title: Edge Delivery Services 概觀
description: 了解 Edge Delivery Services 提供的效能和完善 Lighthouse 分數功能對 AEM as a Cloud Service 有什麼好處。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 207926d68f42f5b398841b92c0a8c72a3f852292
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 37%

---


# Edge Delivery Services 概觀 {#edge-delivery-services}

## 什麼是Edge Delivery Services？ {#what-is-edge}

Edge Delivery Services是一個現代化的內容傳遞架構，可重新構想網站的建立和傳遞方式，以最佳化速度、簡化和擴充性。 這是Adobe Experience Manager的核心部分，可讓呈現和傳送在網路邊緣更接近使用者，提供更快速的數位體驗。

它不是內容傳遞網路(CDN)的替代品，但是與您自己的CDN或隨附的[Adobe管理的CDN緊密整合。](/help/implementing/dispatcher/cdn.md)

>[!TIP]
>
>**想立即親手操作嗎？**
>
>若想立即親手操作，只要[查看 aem.live 上的教學課程](https://www.aem.live/developer/ue-tutorial)，即可在不到 30 分鐘的時間內，使用 AEM 創作啟動您自己的 Edge Delivery Services 專案。


## 為何選擇Edge Delivery Services？ {#why-edge}

### 增加可發現性和流量 {#increase-traffic}

Edge Delivery網站是針對LLM最佳化的搜尋引擎(SEO)和創作引擎最佳化(GEO)。 這可確保所有現有和即將推出的有機流量來源具有高可見度和可發現性。 **效能優先的端對端架構**&#x200B;可確保令人愉快的客戶體驗，進而對參與產生正面影響。

### 開發人員效率 {#developer-efficientcy}

只需幾天或幾週即可上線，無需等待數月或數年時間！ Edge Delivery提供所有工具&#x200B;**現代網頁開發人員**&#x200B;所愛：GitHub、具有自動重新載入功能的本機開發、效能、簡易性，而且沒有複雜性：無整合、無套件組合、無設定、無額外負荷。

Edge Delivery的簡單性不需要您使用複雜的架構、工具或程式，這些都是AI程式碼建立的理想選擇。 使用純HTML、現代化CSS和vanilla JavaScript，以前所未有的速度建立卓越的體驗。 專注於工作，減少花在培訓和學習新工具上的時間。

Edge Delivery可讓每個開發人員取得100的Lighthouse分數。

### 支援多個內容來源 {#multiple-content-sources}

來自各種解決方案的內容可直接與Edge Delivery整合，**包括所有現有的AEM執行個體**。 作者可以從任何系統(例如SharePoint)管理內容，並將內容&#x200B;**發佈到Edge Delivery**，以使用他們已知的工具獲得更快的速度。

### 可撰寫的架構 {#composable-architeture}

不論Headless或Headful，您都可以以正確格式提供正確的內容，並新增正確的裝飾，使其成為任何頻道中脫穎而出的體驗。

## 如何運作 {#how-does-it-work}

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。它以多雲端SaaS解決方案和純前端開發方法，取代AEM Publish/Dispatcher和使用AEM核心元件建立體驗的傳統方式。

![Edge Delivery 架構](assets/AEM-with-EDS-architecture.png)

Edge Delivery Services 會使用 GitHub，可讓您直接從自己的 GitHub 存放庫管理和部署程式碼。新內容將立即加入，無需重建過程。

## 製作 {#authoring}

### In-context editing {#in-context-editing}

[通用編輯器](/help/implementing/universal-editor/introduction.md)是可自訂的、一站式位置，讓您透過視覺預覽即時編輯內容與內容中的所見即所得(WYSIWYG)。

* 有了AEM撰寫和通用編輯器，您就可以提高Headless或Headful的撰寫效率。
* 您可以利用 AEM 全面的內容管理功能，包括工作流程和治理。
* 您可以善用許多擴充功能點來支援您自己的流程和整合。
* 您可以使用 GitHub 中的 CSS 和 JavaScript 來開發網站的功能。

![使用通用編輯器進行 AEM 製作](assets/wysiwyg-authoring.png)

### 檔案式編輯 {#document-based-editing}

[另一種方法是檔案式製作](https://www.aem.live/docs/authoring)，內容會以檔案的形式管理。 由於許多企業都有SharePoint來建立初始內容，因此Microsoft Word是熱門的選擇。 您不需要學習新工具，直接從SharePoint發佈內容，Word也免除了複製內容並貼到AEM的麻煩。 沒有SharePoint的客戶也可以使用Google Drive作為替代方案。

## 作業遙測 {#telemetry}

Adobe Experience Manager使用[作業遙測](https://www.aem.live/docs/operational-telemetry)來收集發現並修正Adobe Experience Manager支援之網站上的功能和效能問題所必須的作業資料。 作業遙測資料可用來診斷效能問題，以及測量實驗的成效。 操作遙測透過[取樣](https://www.aem.live/docs/operational-telemetry#operational-telemetry-data-is-sampled) （只監視所有頁面檢視的一小部分）和[明智排除個人識別資訊](https://www.aem.live/docs/operational-telemetry#what-data-is-being-collected) (PII)，保留訪客的隱私權。

## 開始探索 {#start-exploring}

開始使用AEM撰寫搭配Universal Editor和Edge Delivery Services：

* Edge Delivery Services檔案[Edge Delivery Services](https://www.aem.live)
* 有關使用通用編輯器進行 AEM 製作的概觀，請參閱 aem.live 文件中[使用適用於 Edge Delivery Services 的 AEM 進行製作](https://www.aem.live/docs/aem-authoring)的文件。
* 有關開發人員概觀，請參閱 aem.live 文件中[開始使用 - 通用編輯器開發人員教學課程](https://www.aem.live/developer/ue-tutorial)的文件。

## Edge Delivery Services 和其他 Adobe Experience Cloud 產品 {#edge-other-products}

Edge Delivery Services 是 Adobe Experience Manager 的一部分。因此，Edge Delivery Services 和 AEM Sites 可以在同一網域中共存，這是大型網站的常見使用案例。此外，您的 AEM Sites 頁面可以無縫地使用 Edge Delivery Services 中的內容，反之亦然。

您也可以搭配[Adobe Target](https://www.aem.live/developer/target-integration)和[Launch.](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/home)使用Edge Delivery Services

## 取得 Adobe 的協助 {#getting-help}

Adobe提供三層來協助您使用Edge Delivery Services：

* 利用[社群資源](#community-resources)進行一般查詢
* 存取您的[產品協作頻道](#collaboration-channel)來查詢特定問題。
* [登入支援票證](#support-ticket)以解決合約支援SLA **內的重大和嚴重問題**。

### 存取社群資源 {#community-resources}

透過為 Edge Delivery Services、使用通用編輯器進行 AEM 製作以及文件型製作提供最佳的社群參與和支援服務，Adobe 致力於增強您的能力。

* 參與 [Experience League 社群](https://adobe.ly/3Q6kTKl)，提出問題、分享回饋意見、發起討論、尋求 Adobe 專家和 AEM 顧問/達人的協助，以及與志趣相投的人即時交流。
* 加入 [Discord 頻道](https://discord.gg/aem-live)，這個較輕鬆的平台可讓您即時互動和交換靈感。

### 記錄支援服務單 {#support-ticket}

{{support-ticket}}
