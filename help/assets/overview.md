---
title: Assets as a簡介 [!DNL Cloud Service]
description: Assets as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 為企業提供雲本地的PaaS解決方案，不僅可以以速度和影響力執行其數字資產管理和Dynamic Media操作，還可以在始終最新、始終可用且始終學習的系統中使用新一代智慧功能，如AI/ML。

多個資產或複雜資產的同時擷取，是Experience Manager製作例項耗用大量資源的工作。 當資產新增、處理或甚至移轉時，主執行個體會耗用相當多的CPU、記憶體和I/O資源。 這類效能問題會影響使用者的製作和瀏覽體驗。

企業需要支援多種不同的檔案格式和內容解析度，適用於多裝置、跨地理區域和多語言使用案例。 資產處理和儲存需求需要資源和功能，這些資源和功能可能會使傳統解決方案不堪重負。 有時，資產處理的技術限制無法產生預期的結果，有時，儲存成本會阻礙利潤率。

首先，請了解 [雲本機產品的優勢](#solution-benefits). 查看顯著 [變更Experience Manager為 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 這也影響了Experience Manager Assets的後續行動 [資產變更](/help/assets/assets-cloud-changes.md).

請閱讀以了解 [新Assets功能的詳細資訊](#whats-new-assets) 和 [已知問題](/help/release-notes/known-issues.md). 查看 [過時或移除的功能](/help/release-notes/deprecated-removed-features.md) 了解此版本中移除的項目，並查看此 [近期功能清單](/help/release-notes/known-issues.md#upcoming-assets-capabilities) 知道不久後會發生什麼。 最後，借助此，了解Experience Manager術語 [字彙表](/help/overview/terminology.md).

## 解決方案優點 {#solution-benefits}

以下為Assets作為 [!DNL Cloud Service]. 要了解更多資訊，請參閱 [Experience Manager作為 [!DNL Cloud Service]](/help/overview/introduction.md).

* **適用於資產處理的現代雲端服務**:全新的資產微服務是雲端型、可擴充、可靠且無障礙的資產處理服務。
* **高度可擴展**:跨所有類型部署的彈性可擴充性。 視需要提供幾乎無限的資源。 與傳統系統相比，節省了過度設計的成本。
* **最新軟體**:一律最新且一律更新。 所有用戶只擁有最新的軟體，並有可用的所有修補程式、功能、安全性和錯誤修正。 開發人員和整合商可搭配最新的API集合使用，無需多版本支援問題。
* **始終聯機**:零停機(0dt)，這要歸功於在群集中部署的實例，該實例具有備份和冗餘。 升級也為0dt。
* **持續監控**:系統的監控是自動的、內建的檢查和觸發器，有助於維護效能、可用性和整體健全性。
* **輕鬆部署**:雲端作業中的Experience Manager完全自動化，不需要手動干預。 對於自動部署，Cloud Manager(CM)元件會自動建立包含您自訂程式碼的可部署Docker影像。

## 新資產功能 {#whats-new-assets}

重要的新功能包括：

* [資產微服務](/help/assets/asset-microservices-overview.md)
* [資產上傳方法](/help/assets/add-assets.md)
