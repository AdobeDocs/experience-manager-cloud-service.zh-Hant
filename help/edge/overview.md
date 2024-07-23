---
title: Edge Delivery Services 概觀
description: 了解 Edge Delivery Services 提供的效能和完善 Lighthouse 分數功能對 AEM as a Cloud Service 有什麼好處。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 6c7e704dff97e8549664618f879863c3ca0f8f86
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 55%

---


# Edge Delivery Services 概觀 {#edge-delivery-services}

透過 Edge Delivery Services，AEM 可提供促進參與度和轉換率的卓越體驗。AEM 會透過提供快速編寫和開發的高影響力體驗來實現這一目標。這是一組可組合的服務，有助建立快速開發環境；編寫作者可在其中快速更新和發佈，並且能快速推出新網站。因此，透過 Edge Delivery Services，您可以提高轉換率、降低成本並提供極高的內容速度。

透過 Edge Delivery Services，您可以：

* 建立具有完善 Lighthouse 分數功能的快速網站，並透過真實使用者監控 (RUM) 持續監控您的網站效能。
* 透過分離內容來源來提高編寫工作效率。開箱即用地使用WYSIWYG和檔案式製作。 因此，您可以在同一網站上使用多個內容來源。
* 使用內建的實驗框架，允許快速建立、執行測試而不影響效能，並快速發布測試獲勝者的生產。

## 靈活回應業務需求 {#agile-reaction}

Adobe是公認的業界領導者，知道為客戶快速建立並發佈有意義的新內容是多麼重要。 市場已清楚說明在擴展內容建立方面的常見挑戰，包括：

1. **對內容的需求持續成長。**
   * 需要解鎖新的內容作者以滿足此需求。
   * 內容建立流程必須在整個企業範圍內有效擴展。
   * 作者必須能夠快速回應不斷變化的趨勢。
1. **需要全頻道內容。**
   * 無論內容傳送為何，都需要版面控制。
   * 作者必須能夠直接變更內容配置。
1. **推動內容ROI的壓力增加。**
   * 作者本身需要能力來最佳化他們建立的內容。

事實證明，整個產業都呈現一致的趨勢。 不過，個別需求不可避免地會因專案而異。 任何Edge Delivery Services專案的目標都是著重尋找適合您的使用者的解決方案。

1. **專注於值而非功能。** — 決定為作者提供的最佳化工作流程，而不是在AEM龐大的功能集中迷路。
1. **利用AEM的彈性。** — 不需要在真空中使用AEM功能。 使用這些您根據使用案例需要的功能。
1. **利用您作者的專業知識。** — 從一開始就讓真正的內容作者參與專案，以確保您透過實作有意義的功能，提供他們所需的價值。

透過專注於為作者創造價值，您的Edge Delivery Services專案可滿足內容創作者面臨的現代產業需求，並快速提供內容以取悅客戶。

## 內容創作者適用的彈性撰寫工具 {#overview}

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。您可以使用 [AEM 內容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=zh-Hant)和 WYSIWYG 製作 (使用 [Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md) 以及[文件型製作)。](https://www.aem.live/docs/authoring)

下圖說明如何在 Microsoft Word (文件型製作) 中編輯內容並將其發佈到 Edge Delivery Services。圖表也展示使用 Universal Editor 的 WYSIWYG 編輯。

![Edge Delivery 架構](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services 會使用 GitHub，可讓您直接從自己的 GitHub 存放庫管理和部署程式碼。新內容會立即新增，不需要重新建置程式。

### 以文件為主的製作 {#document-based}

透過檔案式撰寫，您可以直接使用Microsoft Word或Google檔案中的內容，使這些來源成為您網站上的頁面。 標題、清單、影像、字型元素都可以從初始來源傳輸至網站。

* 透過檔案式撰寫，每位行銷人員都能使用已知的撰寫工具(Microsoft Word、Google Docs等)快速建立內容。
* 允許直接在來原始檔中編寫、檢閱和發佈，以簡化內容建立。
* 由於使用了已知工具，內容作者無需上線，即可提升內容速度。
* 您可以在GitHub中使用CSS和JavaScript開發您網站的功能。

![檔案式製作](assets/document-based-authoring.png)

進一步閱讀檔案型撰寫檔案：

* 若需如何開始使用 Edge Delivery 的詳細資訊，請參閱[「建置」部分](https://www.aem.live/docs/#build)。
* 若要了解如何使用 Edge Delivery 製作和發佈內容，請參閱[「發佈」部分](https://www.aem.live/docs/authoring)。
* 若要了解如何正確啟動您的網站專案，請參閱[「啟動」部分](https://www.aem.live/docs/#launch)。

### 所見即所得 {#wysiwyg-authoring}

隨心所欲(WYSIWYG)撰寫功能採用通用編輯器，這是一個可自訂的一站式位置，可讓您透過視覺預覽即時編輯內容與即時內容。

* 有了WYSIWYG撰寫功能，您就能提升Headless或Headful的撰寫效率。
* 您可以善用AEM全面的內容管理功能，包括工作流程與控管。
* 運用許多擴充功能點來支援您自己的流程和整合。
* 您可以在GitHub中使用CSS和JavaScript開發您網站的功能。

![所見即所得](assets/wysiwyg-authoring.png)

進一步閱讀WYSIWYG撰寫檔案：

* 如需Universal Editor和WYSIWYG編寫的概觀，請參閱檔案[WYSIWYG Content Authoring for Edge Delivery Services。](/help/edge/wysiwyg-authoring/authoring.md)
* 如需開發人員概觀，請參閱檔案[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊。](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### 決定您的撰寫方法 {#authoring-method}

AEM的彈性可確保滿足您的撰寫需求。 Adobe可協助您決定最符合需求的方法（或方法）。

* 一律讓內容作者參與決策。
* 可以實作多種編寫方法。
* 您一律可以在事後變更您的編寫方法。
* 您不得在實施之前作出決定，而是必須作為實施的一部分。

如需詳細資訊，請參閱檔案[選擇編寫方法](authoring-methods.md)。

## Edge Delivery Services 和其他 Adobe Experience Cloud 產品 {#edge-other-products}

Edge Delivery Services 屬於 Adobe Experience Manager 的一部分，因此 Edge Delivery Services 和 AEM Sites 可以在相同網域中共存 (較大型網站的常見使用案例)。此外，您可在 AEM Sites 頁面中輕鬆使用來自 Edge Delivery Services 的內容，反之亦然。

請參閱「[使用 Edge Delivery Services 進行 WYSIWYG 的開發人員入門指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)」，了解如何展開您自己的專案並使用 AEM 和 Edge Delivery Services 進行製作。

您也可以將 Edge Delivery Services 與 [Adobe Target、](https://www.aem.live/developer/target-integration) [真實使用者監控 (RUM)](https://www.aem.live/developer/rum) 結合使用，用來診斷網站的使用情況和效能，並且[啟動。](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/home)

## 開始使用 Edge Delivery Services {#getting-started}

輕鬆開始使用 Edge Delivery Services，請[開始使用 - 開發人員教學課程。](https://www.aem.live/developer/tutorial)

## 取得 Adobe 的協助 {#getting-help}

Adobe 提供三個頻道來幫助您使用 Edge Delivery Services：

* 利用[社群資源](#community-resources)進行一般查詢
* 存取您的[產品協作頻道](#collaboration-channel)來查詢特定問題。
* [記錄支援服務單](#support-ticket)以解決主要和關鍵問題。

### 存取社群資源 {#community-resources}

Adobe 致力為您提供 Edge Delivery Services、WYSIWYG 和文件型製作的最佳社群參與和支援服務。

* 參與 [Experience League 社群](https://adobe.ly/3Q6kTKl)，提出問題、分享意見、發起討論、尋求 Adobe 專家和 AEM 顧問/達人的協助，以及與志趣相投的人即時聯繫。
* 加入我們的[探索頻道](https://discord.gg/aem-live)，一個更輕鬆的即時互動和靈感想法交流平台。

### 如何存取您的產品協作頻道 {#collaboration-channel}

鑑於與使用者直接溝通管道的重要性，所有 AEM 專案在發佈時都會建立 Slack 頻道，以提升作業效率，並存取重要更新和體驗品質的擴充報告。您將獲得 Adobe 邀請您加入針對您組織的 Slack 頻道。

若要了解更多資訊，請參閱「[使用 Slack 機器人](https://www.aem.live/docs/slack)」文件取得更多詳細資訊。

您可以透過預先被分配的產品協作頻道與 Adobe 產品團隊互動，回答有關產品使用或最佳實務的問題。沒有與透過產品協作頻道進行對話相關的服務層級目標 (SLT)。

### 記錄支援服務單 {#support-ticket}

如果產品問題需要額外調查和故障排除，並且必須符合回應 SLT，您可以使用 Admin Console 按照此流程來提交支援服務單：

1. [依照標準支援流程](https://experienceleague.adobe.com/?support-tab=home#support)並建立服務單。
1. 將 **Edge Delivery** 加入服務單標題中。
1. 在描述中，除了問題描述之外，還提供以下詳細資訊：

   * 已上線網站的 URL。例如：`www.mydomain.com`。
   * 原始網站的 URL (`.hlx` URL)。

## 下一步 {#whats-next}

開始先檢閱[「使用 Edge Delivery Services」。](/help/edge/using.md)
