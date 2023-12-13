---
title: AEM與Edge Delivery Services
description: 瞭解AEMas a Cloud Service如何受益於Edge Delivery Services所提供的效能和完美的Lighthouse分數。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: 9d26a4835dc331f2ff8b741a4c14847ead611874
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 48%

---


# AEM與Edge Delivery Services {#aem-edge}

透過 Edge Delivery Services，AEM 可提供促進參與度和轉換率的卓越體驗。AEM 會透過提供快速編寫和開發的高影響力體驗來實現這一目標。這是一組可組合的服務，有助建立快速開發環境；編寫作者可在其中快速更新和發佈，並且能快速推出新網站。因此，透過 Edge Delivery Services，您可以提高轉換率、降低成本並提供極高的內容速度。

使用Edge Delivery Services時，您可以：

* 建立具有完善 Lighthouse 分數功能的快速網站，並透過真實使用者監控 (RUM) 持續監控您的網站效能。
* 透過分離內容來源來提高編寫工作效率。您可以一開啟即使用 AEM 編寫和文件型編寫。因此，您可以在同一網站上使用多個內容來源。
* 使用內建的實驗框架，允許快速建立、執行測試而不影響效能，並快速發布測試獲勝者的生產。

## Edge Delivery Services概觀 {#edge-overview}

下圖說明如何在Microsoft Word中編輯內容（檔案式編輯）並發佈至Edge Delivery Services。 它也會顯示使用通用編輯器的AEM發佈方法。

![Edge Delivery 架構](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services是一組可撰寫的服務，可讓您在網站上撰寫內容的方式上擁有高度彈性。 如前所述，您可以使用兩者 [AEM內容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) 替換為 [Universal Editor製作](/help/implementing/universal-editor/introduction.md) 以及 [檔案式製作。](https://www.aem.live/docs/authoring)

例如，您可以直接使用 Microsoft Word 或 Google Docs 中的內容。這表示這些來源的文件可以成為您網站上的頁面。此外，標題、清單、影像、字體元素、都可以從初始來源傳輸到網站。新內容將立即加入，無需重建過程。

Edge Delivery Services使用GitHub，因此客戶可以直接從其GitHub存放庫管理和部署程式碼。 例如，您可以在Google檔案或Microsoft Word中撰寫內容，而您可以在GitHub中使用CSS和JavaScript開發網站功能。 準備好後，您可以使用 Sidekick 瀏覽器擴充功能來預覽和發佈內容更新。

進一步閱讀Edge Delivery Services檔案：

* 如需開始使用Edge Delivery的詳細資訊，請參閱 [建置區段。](https://www.aem.live/docs/#build)
* 若要瞭解如何使用Edge Delivery製作和發佈內容，請參閱 [發佈區段。](https://www.aem.live/docs/authoring)
* 若要瞭解如何正確啟動您的網站專案，請參閱 [「啟動」區段。](https://www.aem.live/docs/#launch)

## Edge Delivery Services和其他Adobe Experience Cloud產品 {#edge-other-products}

Edge Delivery Services是Adobe Experience Manager的一部分，因此這些Edge Delivery Services和AEM網站可以共存於同一個網域中。 這是較大型網站的常見使用案例。此外，Edge Delivery Services內容也可在您的AEM Sites頁面中輕鬆使用，反之亦然。

您也可以將 Edge Delivery Services 與 Adobe Target、Analytics 和 Launch 一起使用。

## 取得 Edge Delivery Services 存取權 {#getting-access}

開始使用 Edge Delivery Services 很容易。首先請遵循以下步驟 [快速入門 — 開發人員教學課程。](https://www.aem.live/developer/tutorial)

## 取得 Adobe 的協助 {#adobe-gethelp}

您可以透過預先被分配的產品協作頻道 (請參閱下文取得存取詳情) 與 Adobe 產品團隊互動，回答有關產品使用或最佳實務的問題。沒有透過產品共同作業管道與交談相關聯的服務等級目標(SLT)。 如果產品問題需要額外的調查和疑難排解，並且必須符合回應SLT，您可以遵循以下內容提交支援票證 [支援程式。](https://experienceleague.adobe.com/?support-tab=home#support)

Adobe 提供三個頻道來幫助您使用 Edge Delivery Services：

* 利用社群資源進行一般查詢
* 存取您的產品協作頻道來查詢特定問題
* 記錄支援服務單以解決主要和關鍵問題

### 存取社群資源 {#community-resource}

Adobe致力於為您提供最佳社群參與度，以及對Edge Delivery Services和檔案式編寫的支援。

* 參與 [Experience League社群](https://adobe.ly/3Q6kTKl) 提出問題、分享意見、展開討論、向Adobe專家和AEM顧問/Champs尋求協助，並即時與志同道合的個人進行交流。
* 加入我們的 [不和諧的頻道，](https://discord.gg/aem-live) 提供更休閒的平台，用於即時互動和快速構想交流。

### 如何存取您的產品共同作業管道 {#collab-channel}

考慮到與客戶直接溝通管道的價值，所有AEM客戶在上市時都會建立Slack管道，用於速度、關鍵更新以及體驗品質的規模化報告。 您會獲得 Adobe 邀請您加入針對您組織的 Slack 頻道。

若要了解更多資訊，請參閱「[使用 Slack 機器人](https://www.aem.live/docs/slack)」文件取得更多詳細資訊。

### 記錄支援服務單 {#support-ticket}

透過 Admin Console 記錄支援服務單的步驟：

1. [依照標準支援流程，](https://experienceleague.adobe.com/?support-tab=home#support) 建立票證。
1. 將 **Edge Delivery** 加入服務單標題中。
1. 在說明中提供以下詳細資訊：

   * 即時網站的 URL。例如：`www.mydomain.com`。
   * 來源網站的URL (`.hlx` URL)。

## 下一步 {#whats-next}

開始先檢閱「[使用 Edge Delivery Services](/help/edge/using.md)」。
