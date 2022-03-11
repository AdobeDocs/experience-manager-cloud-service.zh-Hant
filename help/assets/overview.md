---
title: Assets as簡介 [!DNL Cloud Service]
description: Assets中的新增功能 [!DNL Cloud Service]。
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 將資產作為 [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager資產 [!DNL Cloud Service] 為企業提供雲本地PaaS解決方案，不僅可以以快速和有效的速度執行其數字資產管理和Dynamic Media操作，還可以從始終最新、始終可用且始終學習的系統內使用新一代智慧功能，如AI/ML。

對於「Experience Manager作者」實例，同時接收許多資產或複雜資產是資源密集型任務。 在添加、處理甚至遷移資產時，主實例會佔用大量CPU、記憶體和I/O資源。 此類效能問題會影響最終用戶的創作和瀏覽體驗。

企業需要為多設備、跨地理位置和多語言使用案例支援多種檔案格式和內容解析。 資產處理和儲存需求要求資源和功能，這些資源和功能可能會給傳統解決方案帶來負擔。 有時，資產處理的技術限制無法產生預期的結果，有時，儲存成本會阻礙利潤率。

首先，要瞭解 [雲本機產品的優勢](#solution-benefits)。 查看值得注意的 [Experience Manager更改為 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 也影響了Experience Manager Assets的關注 [對資產的更改](/help/assets/assets-cloud-changes.md)。

閱讀以瞭解 [新資產功能的詳細資訊](#whats-new-assets) 和 [已知問題](/help/release-notes/known-issues.md)。 請參閱 [已棄用或刪除的功能](/help/release-notes/deprecated-removed-features.md) 瞭解此版本中刪除的內容，並查看此 [即將發佈的功能清單](/help/release-notes/known-issues.md#upcoming-assets-capabilities) 知道不久後會發生什麼。 最後，借助此功能瞭解Experience Manager術語 [術語](/help/overview/terminology.md)。

## 解決方案優勢 {#solution-benefits}

以下為Assets作為 [!DNL Cloud Service]。 要瞭解更多資訊，請參閱 [Experience Manager概述 [!DNL Cloud Service]](/help/overview/introduction.md)。

* **用於資產處理的現代雲服務**:新資產微服務是基於雲的、可擴展、可靠且無障礙的資產處理服務。
* **高度可擴展**:跨所有類型的部署的彈性可擴充性。 實際上無限制的資源，可根據需要隨時提供。 與傳統系統相比，節省了過度設計的成本。
* **最新軟體**:始終最新且始終更新。 所有用戶只有最新軟體，其中包含所有補丁程式、功能、安全性和錯誤修復。 開發人員和整合商可以使用最新的API集，而無多版本支援問題。
* **始終聯機**:零停機時間(0dt)，這要歸功於在具有備份和冗餘的群集中部署的實例。 升級也為0dt。
* **持續監控**:系統的監控是自動化的，內置的檢查和觸發有助於保持效能、可用性和總體魯棒性。
* **無障礙部署**:雲操作中的Experience Manager是完全自動化的，無需人工干預。 對於自動部署，雲管理器(CM)元件可自動生成包含自定義代碼的可部署Docker映像。

## 新資產功能 {#whats-new-assets}

重要的新功能包括：

* [資產微服務](/help/assets/asset-microservices-overview.md)
* [資產上載方法](/help/assets/add-assets.md)
