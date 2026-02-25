---
title: Experience現代化代理概述
description: 瞭解Experience現代化代理程式如何透過AI將新網站上線到Edge Delivery Services中。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: f286215d7094bffbec732c9ba6149d6bab168fc7
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---


# Experience現代化代理概述 {#experience-modernization-agent}

瞭解Experience現代化代理程式如何透過AI將網站匯入Edge Delivery Services。

>[!NOTE]
>
>體驗現代化代理程式會取代[品牌體驗代理程式的舊版移轉技能。](/help/ai-in-aem/agents/brand-experience/overview.md)

## 簡介 {#introduction}

Experience Modernization Agent透過快速且順暢地進行網站移轉和持續演化，釋放了Edge Delivery Services的全部價值(包括AEM製作)。

它結合了[網站建立和移轉技能](#creation-migration)，用於初始網站上線和[區塊開發功能](#block-development)，用於持續體驗開發（樣式更新、範本細分、登陸頁面建立）。 此外，它提供[體驗現代化主控台](#console)，作為可直接使用的託管AI輔助開發環境。 雖然使用者可直接透過該主控台操作代理程式，但開發人員仍可完全控制出廠內容。

此外，為確保成功完成複雜移轉，Adobe提供[代理結果工程師(AOE)傳遞模型](#delivery-model)。 此選項可作為加速器或戰術服務使用，以協助解除封鎖特定專案挑戰。

## 優點 {#benefits}

Experience Modernization Agent可加快採用[Edge Delivery Services](/help/edge/overview.md)的價值實現時間，並讓您能夠靈活調整品牌的Web體驗。

* **高速**： AI自動化可處理重複的移轉工作（內容匯入、區塊對應、設計系統應用程式），將幾個月的工作壓縮為數週
* **具成本效益**：自動化處理重複性的工作，將專業服務釋放給高價值的工作，例如整合和策略決策
* **任何人都可以存取**：自然語言要求可讓技術較不熟練的使用者存取網站變更，並可即時預覽以驗證變更
* **企業控管**：開發人員對與GitHub整合的稽核工作流程進行處理的專案維持完整許可權
* **連續值**：代理程式支援持續的網站演化，包括樣式更新、範本改良和建立登入頁面

## 網站建立和移轉技能 {#creation-migration}

Experience現代化代理程式提供建立新Edge Delivery Services網站和移轉現有網站的技能。 我們鼓勵所有新的Edge Delivery Services網站或移轉作業都充分利用這些技能。

* 加速網站建立和從幾個月移轉至幾週或幾天，大幅縮短採用Edge Delivery Services的價值實現時間
* 將網站從任何CMS、舊版AEM或設計系統（例如Figma）轉換為可立即投入使用的Edge Delivery Services專案
* 提供所有Edge Delivery Services承諾：針對代理功能的AI整備、快速效能（最佳化核心Web重要程式）、協助工具(WCAG 2.1 AA)、涵蓋所有中斷點的回應式設計，以及內容+程式碼敏捷度

詳細技能包括頁面移轉、大量匯入、設計擷取、導覽設定和網頁刮取。

## 區塊開發功能 {#block-development}

Experience Modernization Agent會利用一般Edge Delivery Services開發功能，提供各種開發任務，在初始網站建立或移轉之後提供持續價值。

* 遵循內容導向開發(CDD)方法，用於製作友善的內容模型
* 運用[區塊集合](https://www.aem.live/developer/block-collection)和[區塊派對](https://www.aem.live/developer/block-party/)來尋找參考實作和最佳實務
* 支援測試和偵錯工作流程，以在部署前驗證變更

詳細的功能包括區塊開發、內容模型、參考區塊探索、測試和偵錯。

## Experience現代化主控台 {#console}

Experience Modernization Agent為Edge Delivery Services提供託管式AI輔助開發環境，在[`aemcoder.adobe.io`.](https://aemcoder.adobe.io)以網頁介面顯示

* 主控台不需要進行本機設定，使用者就可以立即以自然語言開始提示變更。
* 透過即時AEM預覽快速執行日常體驗開發任務，並將內容同步到AEM。
* 由於開發人員可透過一般的GitHub檢閱和核准程式，保留對出貨專案的完整控制權，因此會強制執行企業控管。

自助式Experience Modernization Console現已正式推出。 感興趣的使用者可以請求存取權，以確保流暢的上線體驗。

## 傳遞模型 {#delivery-model}

針對複雜的移轉或加速的結果，Adobe提供代理成果工程師(AOE)交付模型。 這是一項選用服務，Adobe工程師可代表您操作AI工具。

* Adobe AOE會與您並肩操作代理程式，將AI自動化與專家指引相結合，以大規模提供生產就緒型結果。
* 針對實施作業延遲或舊版現代化挑戰，提供策略重設選項。
* AOE模型提供更快、風險更低的前進路徑，可利用AI自動化，同時確保治理、品質和成功結果。

若要進一步探索AOE傳送模型：

* 請聯絡您的Adobe代表或客戶團隊，以啟動範圍設定和排程。
* Adobe將確認資格、估計參與並建議參與計畫。

## 限制 {#limitations}

除了體驗現代化代理的技能外，以下使用案例還需要額外的實施工作。

刮削工具不支援下列來源。

* 內部網路或受保護的來源，例如驗證後的內容、VPN或無法存取的防火牆
* 複雜的動態內容，例如需要複雜使用者互動才能出現在DOM中的內容。
   * 如果內容可透過特定URL存取，則支援使用者端轉譯內容。
   * 也支援透過CSS隱藏但存在於DOM中的元素，例如索引標籤、摺疊式功能表或轉盤。

代理程式不支援下列目標。

* 網站使用HTL式傳送的AEM發佈環境
   * 此技能僅針對Edge Delivery Services。
* Headless傳送模式，例如，僅限API或SPA型傳送（例如Next.js）

下列需求尚未涵蓋在專門的自動化技能中，需要手動操作。

* 嚴格畫素完美
   * 只有實用的設計逼真度才能自動化
* 整合伺服器或使用者端協力廠商資料/服務
* 商務或搜尋功能的整合
* MarTech資料層或目標定位/實驗
* 隔離內容/體驗片段
* 多站台繼承(MSM)
* 自訂功能（例如電腦、組態程式）
* 自訂商業邏輯
