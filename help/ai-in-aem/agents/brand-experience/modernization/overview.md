---
title: Experience現代化代理概述
description: 瞭解體驗現代化代理如何在人工智慧的幫助下將新網站登入Edge Delivery Services。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 84fed5a82d6c23cd51d9796eb644121c6ef06a29
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Experience現代化代理概述 {#experience-modernization-agent}

瞭解Experience現代化代理程式如何透過AI將網站匯入Edge Delivery Services。

## 簡介 {#introduction}

[作為Brand Experience Agent的一部分，](/help/ai-in-aem/agents/brand-experience/overview.md) Experience Modernization Agent藉由自動化網站移轉和基礎網站設定，加速Edge Delivery Services上線。

它結合了[網站建立和移轉技巧](#creation-migration)，用於初始網站入門和[區塊開發功能](#block-development)，以支援網站建立和移轉工作流程。 此外，它提供[體驗現代化主控台](#console)作為網路型AI輔助開發環境，可直接提供給您使用。 While users can operate the agent directly through that console, developers retain full control over what ships.

For complex or high-priority migrations, Adobe offers the [Agentic Outcome Engineer (AOE) delivery model,](#aoe-delivery) an engineering-led service designed to deliver production-ready Edge Delivery sites using the Experience Modernization Agent.

## 優點 {#benefits}

體驗現代化代理可加快[Edge Delivery Services](/help/edge/overview.md)採用的價值實現時間，並讓您能夠靈活調整品牌的Web體驗。

* **高速**: AI自動化處理重複遷移工作（內容導入、塊映射、設計系統應用程式），與傳統方法相比壓縮遷移時間表
* **注重效率**：自動化減少了重複性工作，使團隊能夠專注於價值更高的實施工作
* **Accessible to anyone**: Natural language requests make website changes accessible to less technical users, with live preview to validate changes instantly
* **Enterprise governance**: Developers maintain full authority over what goes live through review workflows integrated with GitHub
* **Post-migration flexibility**: Enables teams to extend and refine migrated sites using Edge Delivery Services patterns

## Site Creation and Migration Skills {#creation-migration}

The Experience Modernization Agent offers skills for creating new Edge Delivery Services sites and migrating existing websites. Any new Edge Delivery Services site or migration is encouraged to take advantage of these skills.

* 加速網站建立和從幾個月移轉至幾週或幾天，大幅縮短採用Edge Delivery Services的價值實現時間
* 支援從各種CMS平台、舊版AEM或設計系統（如Figma）移轉至生產適用的Edge Delivery Services專案
* 根據Edge Delivery Services指引，支援效能、協助工具及回應式設計的最佳實務

詳細技能包括頁面遷移、批量導入、設計提取、導航設定和Web刮取。

## 塊開發功能 {#block-development}

Experience Modernization Agent會利用一般Edge Delivery Services開發功能，提供各種開發任務，在初始網站建立或移轉之後提供持續價值。

* 遵循內容導向開發(CDD)方法，用於製作友善的內容模型
* 運用[區塊集合](https://www.aem.live/developer/block-collection)和[區塊派對](https://www.aem.live/developer/block-party/)來尋找參考實作和最佳實務
* 支援測試和偵錯工作流程，以在部署前驗證變更

詳細的功能包括區塊開發、內容模型、參考區塊探索、測試和偵錯。

## Experience現代化主控台 {#console}

The Experience Modernization Agent provides a web-based AI-assisted development environment for Edge Delivery Services, exposed as a web interface at [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)

* The console requires no local setup for users to start prompting changes immediately in natural language.
* 快速執行日常體驗開發任務，同時通過即時預覽來預覽這些任AEM務，並將內容同步到AEM。
* 該控制台通過標準GitHub審核工作流支援企業治理。

自助服務體驗現代化控制台通常可用。 感興趣的用戶可以請求訪問，以確保流暢的登機體驗。

Get started with the Experience Modernization Console!

* If you are modernizing your site by targeting Document Authoring, [get started here.](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
* If you are modernizing your site by targeting AEM authoring, [get started here.](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)

## Agentic Outcome Engineer (AOE) Delivery {#aoe-delivery}

For complex migrations or accelerated outcomes, Adobe offers the Agentic Outcome Engineer (AOE) delivery. This is an optional service where Adobe engineers operate the Experience Modernization Agent on your behalf, combining AI automation with expert guidance to deliver production-ready results at scale. 如需AOE傳送的詳細資訊，請參閱檔案： [Experience Modernization Agent的AOE傳送。](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md)

如果您對下次移轉的AOE模式感興趣：

* 請與您的Adobe代表或客戶團隊聯繫以啟動範圍界定和計畫。
* Adobe將確認資格、估計項目並建議項目計畫。

## 限制 {#limitations}

除了體驗現代化代理的技能外，以下使用案例還需要額外的實施工作。

The scraping skill does not support the following sources.

* Intranet or protected sources such as content behind authentication, VPNs, or firewalls that is not accessible
* Complex dynamic content such as content requiring sophisticated user interaction to appear in the DOM.
   * 如果內容可通過特定URL訪問，則支援客戶端呈現的內容。
   * 還支援通過CSS隱藏但在DOM中存在的元素，如制表符、手風琴或箭頭。

The agent does not support the following targets.

* AEM publish environments where sites use HTL-based delivery
   * The skills target Edge Delivery Services only.
* Headless delivery patterns such as API-only or SPA-based delivery (e.g., Next.js)

The following requirements are not covered by dedicated automation skills and require manual effort.

* Strict pixel perfection
   * 只有實用的設計逼真度才能自動化
* 整合伺服器或使用者端協力廠商資料/服務
* 商務或搜尋功能的整合
* MarTech資料層或目標定位/實驗
* 內容/體驗片段的隔離
* 多站台繼承(MSM)
* 自訂功能（例如電腦、組態程式）
* 自訂商業邏輯

## 後續步驟 {#next-steps}

開始使用檔案[開始使用Experience Modernization Agent來移轉網站。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
