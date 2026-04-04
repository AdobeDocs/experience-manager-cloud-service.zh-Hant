---
title: Experience現代化代理概述
description: 瞭解Experience現代化代理程式如何透過AI將新網站上線到Edge Delivery Services中。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Experience現代化代理概述 {#experience-modernization-agent}

瞭解Experience現代化代理程式如何透過AI將網站匯入Edge Delivery Services。

## 簡介 {#introduction}

[作為Brand Experience Agent的一部分，](/help/ai-in-aem/agents/brand-experience/overview.md) Experience Modernization Agent藉由自動化網站移轉和基礎網站設定，加速Edge Delivery Services上線。

它結合了[網站建立和移轉技巧](#creation-migration)，用於初始網站入門和[區塊開發功能](#block-development)，以支援網站建立和移轉工作流程。 此外，它提供[體驗現代化主控台](#console)作為網路型AI輔助開發環境，可直接提供給您使用。 雖然使用者可直接透過該主控台操作代理程式，但開發人員仍可完全控制出廠內容。

對於複雜或高優先順序的移轉，Adobe提供[Agentic Output Engineer (AOE)傳遞模型，](#aoe-delivery)由工程領導的服務，旨在使用Experience Modernization Agent提供生產就緒的Edge Delivery網站。

## 優點 {#benefits}

Experience Modernization Agent可加快採用[Edge Delivery Services](/help/edge/overview.md)的價值實現時間，並讓您能夠靈活調整品牌的Web體驗。

* **高速**： AI自動化可處理重複的移轉工作（內容匯入、區塊對應、設計系統應用程式），與傳統方式相比，可壓縮移轉時間表
* **以效率為中心**：自動化可減少重複工作，讓團隊專注於更高價值的實作工作
* **任何人都可以存取**：自然語言要求可讓技術較不熟練的使用者存取網站變更，並可即時預覽以驗證變更
* **企業控管**：開發人員對與GitHub整合的稽核工作流程進行處理的專案維持完整許可權
* **移轉後的彈性**：可讓團隊使用Edge Delivery Services模式來擴充及調整移轉的網站

## 網站建立和移轉技能 {#creation-migration}

Experience現代化代理程式提供建立新Edge Delivery Services網站和移轉現有網站的技能。 我們鼓勵所有新的Edge Delivery Services網站或移轉作業都充分利用這些技能。

* 加速網站建立和從幾個月移轉至幾週或幾天，大幅縮短採用Edge Delivery Services的價值實現時間
* 支援從各種CMS平台、舊版AEM或設計系統（如Figma）移轉至生產適用的Edge Delivery Services專案
* 根據Edge Delivery Services指引，支援效能、協助工具及回應式設計的最佳實務

詳細技能包括頁面移轉、大量匯入、設計擷取、導覽設定和網頁刮取。

## 區塊開發功能 {#block-development}

Experience Modernization Agent會利用一般Edge Delivery Services開發功能，提供各種開發任務，在初始網站建立或移轉之後提供持續價值。

* 遵循內容導向開發(CDD)方法，用於製作友善的內容模型
* 運用[區塊集合](https://www.aem.live/developer/block-collection)和[區塊派對](https://www.aem.live/developer/block-party/)來尋找參考實作和最佳實務
* 支援測試和偵錯工作流程，以在部署前驗證變更

詳細的功能包括區塊開發、內容模型、參考區塊探索、測試和偵錯。

## Experience現代化主控台 {#console}

Experience Modernization Agent為Edge Delivery Services提供網頁式AI輔助開發環境，在[`aemcoder.adobe.io`.](https://aemcoder.adobe.io)以網頁介面顯示

* 主控台不需要進行本機設定，使用者就可以立即以自然語言開始提示變更。
* 透過即時AEM預覽快速執行日常體驗開發任務，並將內容同步到AEM。
* 主控台透過標準GitHub稽核工作流程支援企業管治。

自助式Experience Modernization Console現已正式推出。 感興趣的使用者可以請求存取權，以確保流暢的上線體驗。

開始使用Experience現代化主控台！

* 如果您要透過目標檔案製作來更新網站，[從這裡開始。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
* 如果您要以AEM撰寫為目標來匯入最新的網站，請[從這裡開始。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)

## 代理結果工程師(AOE)傳遞 {#aoe-delivery}

針對複雜的移轉或加速的結果，Adobe提供代理成果工程師(AOE)交付。 這是一項選用服務，Adobe工程師會代表您操作Experience Modernization Agent，將AI自動化與專家指引結合，以大規模提供生產就緒的結果。 如需AOE傳送的詳細資訊，請參閱檔案： [Experience Modernization Agent的AOE傳送。](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md)

如果您對下次移轉的AOE模式感興趣：

* 請聯絡您的Adobe代表或客戶團隊，以啟動範圍設定和排程。
* Adobe將確認資格、估計參與並建議參與計畫。

## 限制 {#limitations}

除了體驗現代化代理的技能外，以下使用案例還需要額外的實施工作。

刮削技能不支援下列來源。

* 內部網路或受保護的來源，例如驗證後的內容、VPN或無法存取的防火牆
* 複雜的動態內容，例如需要複雜使用者互動才能出現在DOM中的內容。
   * 如果內容可透過特定URL存取，則支援使用者端轉譯內容。
   * 也支援透過CSS隱藏但存在於DOM中的元素，例如索引標籤、摺疊式功能表或轉盤。

代理程式不支援下列目標。

* 網站使用HTL式傳送的AEM發佈環境
   * 此技能僅針對Edge Delivery Services。
* Headless傳送模式，例如，僅限API或SPA型傳送（例如Next.js）

下列要求不在專屬自動化技能的涵蓋範圍內，需要手動操作。

* 嚴格畫素完美
   * 只有實用的設計逼真度才能自動化
* 整合伺服器或使用者端協力廠商資料/服務
* 商務或搜尋功能的整合
* MarTech資料層或目標定位/實驗
* 隔離內容/體驗片段
* 多站台繼承(MSM)
* 自訂功能（例如電腦、組態程式）
* 自訂商業邏輯

## 後續步驟 {#next-steps}

開始使用檔案[開始使用Experience Modernization Agent來移轉網站。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
