---
title: Assets 雲端服務簡介
description: 資產即雲端服務的新增功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Assets 雲端服務簡介 {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a Cloud Service為企業提供雲端原生PaaS解決方案，不僅可快速且有影響力地執行其數位資產管理和動態媒體作業，還可在永遠最新、永遠可用且永遠學習的系統中使用新一代智慧功能，例如AI/ML。

並行擷取許多資產或複雜資產是AEM Author例項的資源密集型工作。 在添加、處理或甚至遷移資產時，主實例會佔用大量CPU、記憶體和I/O資源。 這些效能問題會影響使用者的製作和瀏覽體驗。

企業需要針對多裝置、跨地理位置和多語言使用案例，支援各種檔案格式和內容解析度。 資產處理和儲存需求需要資源和功能，這些資源和功能可能會使傳統解決方案負擔過重。 有時，資產處理的技術限制無法產生預期結果，有時儲存成本會阻礙利潤率。

首先，請瞭解雲 [端原生產品的優點](#solution-benefits)。 查看AEM的Cloud Service [顯著變更](/help/release-notes/aem-cloud-changes.md) ，這些變更也會影響Experience Manager Assets，然後是資產 [的顯著變更](/help/assets/assets-cloud-changes.md)。

閱讀以瞭解新 [Assets功能的詳細資訊](#whats-new-assets) ，以及 [已知問題](/help/release-notes/known-issues.md)。 檢視已過時 [或已移除的功能清單](/help/release-notes/deprecated-removed-features.md) ，以瞭解此版本中已移除的功能，並 [檢視此即將推出的功能清單](/help/release-notes/known-issues.md#upcoming-assets-capabilities) ，以瞭解即將推出的功能。 最後，請透過此辭彙表瞭解AEM [詞語](/help/overview/terminology.md)。

## 解決方案優點 {#solution-benefits}

以下是資產作為雲端服務的主要優點。 如需詳細資訊，請 [參閱Experience Manager雲端服務概觀](/help/overview/introduction.md)。

* **適用於資產處理的Modern Cloud服務**: 全新的資產微服務是雲端、可擴充、可靠且簡單易用的資產處理服務。
* **高度可擴充**: 跨所有類型部署的彈性調整能力。 視需要提供無限資源。 與傳統系統相比，節省了過度設計的成本。
* **最新軟體**: 永遠是最新且隨時更新。 所有使用者都只有最新的軟體，並有所有修補程式、功能、安全性和錯誤修正可供使用。 開發人員和整合商可使用最新的API集，而不會產生多版本支援問題。
* **始終線上**: 由於在群集中部署了備份和冗餘的實例，因此零停機時間(0dt)。 升級也是0dt。
* **持續監控**: 系統的監控是自動化和內建的檢查與觸發，有助於維持效能、可用性和整體穩健性。
* **輕鬆部署**: 雲端作業中的AEM完全自動化，不需要手動干預。 對於自動部署，Cloud Manager(CM)元件會自動生成包含您的自定義代碼的可部署Docker映像。

## 新資產功能 {#whats-new-assets}

重要的新功能包括：

* [資產微服務](/help/assets/asset-microservices-overview.md)
* [資產上傳方法](/help/assets/add-assets.md)
