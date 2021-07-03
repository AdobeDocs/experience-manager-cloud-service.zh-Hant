---
title: assets as a [!DNL Cloud Service]簡介
description: assets as a [!DNL Cloud Service]的新增功能。
contentOwner: AG
feature: 資產管理
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 將資產作為[!DNL Cloud Service]簡介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service]提供雲端原生的PaaS解決方案，讓企業不僅能以速度和影響力執行其數位資產管理和Dynamic Media作業，還可在始終為最新、隨時可用且隨時學習的系統中使用新一代智慧功能，例如AI/ML。

多個資產或複雜資產的同時擷取，是AEM製作例項的資源密集型工作。 當資產新增、處理或甚至移轉時，主執行個體會耗用相當多的CPU、記憶體和I/O資源。 這類效能問題會影響使用者的製作和瀏覽體驗。

企業需要支援多種不同的檔案格式和內容解析度，適用於多裝置、跨地理區域和多語言使用案例。 資產處理和儲存需求需要資源和功能，這些資源和功能可能會使傳統解決方案不堪重負。 有時，資產處理的技術限制無法產生預期的結果，有時，儲存成本會阻礙利潤率。

首先，請了解雲端原生產品](#solution-benefits)的[優點。 查看AEM as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)的顯著[變更，其也會影響Experience Manager資產，隨後追蹤資產[的顯著變更。](/help/assets/assets-cloud-changes.md)

請閱讀以了解新Assets功能](#whats-new-assets)的詳細資訊，以及[已知問題](/help/release-notes/known-issues.md)。 [請參閱[已棄用或已移除功能的清單](/help/release-notes/deprecated-removed-features.md) ，了解此版本中已移除的內容，並參閱此[即將推出的功能清單](/help/release-notes/known-issues.md#upcoming-assets-capabilities) ，了解近期即將推出的內容。 最後，借助此[字彙表](/help/overview/terminology.md)了解AEM術語。

## 解決方案優點 {#solution-benefits}

以下是資產作為[!DNL Cloud Service]的主要優點。 如需詳細資訊，請參閱[Experience Manager概觀as a [!DNL Cloud Service]](/help/overview/introduction.md)。

* **適用於資產處理的現代雲端服務**:全新的資產微服務是雲端型、可擴充、可靠且無障礙的資產處理服務。
* **高度可擴展**:跨所有類型部署的彈性可擴充性。視需要提供幾乎無限的資源。 與傳統系統相比，節省了過度設計的成本。
* **最新軟體**:一律最新且一律更新。所有用戶只擁有最新的軟體，並有可用的所有修補程式、功能、安全性和錯誤修正。 開發人員和整合商可搭配最新的API集合使用，無需多版本支援問題。
* **始終聯機**:零停機(0dt)，這要歸功於在群集中部署的實例，該實例具有備份和冗餘。升級也為0dt。
* **持續監控**:系統的監控是自動的、內建的檢查和觸發器，有助於維護效能、可用性和整體健全性。
* **輕鬆部署**:AEM在雲端作業中是完全自動化的，不需要手動干預。對於自動部署，Cloud Manager(CM)元件會自動建立包含您自訂程式碼的可部署Docker影像。

## 新資產功能 {#whats-new-assets}

重要的新功能包括：

* [資產微服務](/help/assets/asset-microservices-overview.md)
* [資產上傳方法](/help/assets/add-assets.md)
