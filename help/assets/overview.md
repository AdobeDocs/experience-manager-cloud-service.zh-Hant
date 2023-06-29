---
title: Assets as a [!DNL Cloud Service] 簡介
description: Assets as a [!DNL Cloud Service] 的新功能。
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: d0deca8acbf6049d5be6c27275eedf9b52b27658
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 68%

---

# 介紹 Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 為企業提供一種雲端原生的 PaaS 解決方案，不僅可以快速有效地執行數位資產管理和動態媒體操作，而且還使用始終最新、可用且不斷學習之系統的下一代智慧功能 (例如 AI/ML)。

同時擷取許多資產或複雜資產是 Experience Manager 作者執行個體的資源密集型任務。主執行個體在新增、處理甚至移轉資產時會消耗大量 CPU、記憶體和 I/O 資源。此類效能問題會影響一般使用者的編寫和瀏覽體驗。

企業需要支援各種檔案格式和內容解析度，以適用於多設備、跨地理位置和多語言的使用案例。資產處理和儲存要求所需要的資源和功能可能會使傳統解決方案負擔過重。有時，資產處理的技術限制不會產生預期的結果，而在其他時候，儲存成本不利於營利。

一開始先了解[雲端原生產品的優勢](#solution-benefits)。查看值得注意的 [Experience Manager as a  [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 幾項變更，這些變更也會影響 Experience Manager Assets，接者是值得注意的 [Assets 變更](/help/assets/assets-cloud-changes.md)。

繼續閱讀以了解[新 Assets 功能的詳細資訊](#whats-new-assets)和[已知問題](/help/release-notes/maintenance/latest.md)。查看[已過時或移除的功能](/help/release-notes/deprecated-removed-features.md)清單以了解此版本已刪除的功能。最後，借助此[術語表](/help/overview/terminology.md)了解 Experience Manager 術語。

## 解決方案優勢 {#solution-benefits}

以下是 Assets as a [!DNL Cloud Service] 的主要優勢。如需更多資訊，請參閱 [Experience Manager as a  [!DNL Cloud Service]](/help/overview/introduction.md) 概述。

* **用於資產處理的現代雲端服務**：新的資產微服務是一種雲端型、可擴展、可靠且簡單易用的資產處理服務。
* **高度可擴展**：具擴展性、跨所有部署類型。隨時按需求提供實際上不限數量的資源。與傳統系統相比，節省了過度設計的成本。
* **最新軟體**：始終最新且始終更新。所有使用者都只能使用最新軟體，其中包含所有可用的修補程式、功能、安全性和錯誤修正。開發人員和整合者使用最新的一組 API，沒有多版本支援問題。
* **始終提供服務**：零停機時間 (0dt)，這要歸功於部署在具有備份和備援之叢集中的執行個體。升級也是 0dt。
* **持續監控**：系統監控是自動化的，內建的檢查和觸發機制有助於維護效能、可用性和整體穩健性。
* **輕鬆部署**：Experience Manager 在雲端中的操作完全自動化，無需人工介入。對於自動化部署，Cloud Manager (CM) 元件會自動建置包含您自訂程式碼的可部署 Docker 影像。

## 可用的角色型體驗 {#persona-based-experiences}

Adobe 為您提供健全的數位資產管理 (DAM) 解決方案，可供您善加利用您的數位資產。Adobe Experience Manager Assets有兩個使用相同Cloud Services存放庫的不同體驗：

* **管理員檢視**：現有的Assetsas a Cloud Service使用者介面。 使用「管理員檢視」即可執行所有進階資產管理功能，包括整合、工作流程、內容自動化、發佈等。

* **資產檢視**：Adobe的輕量型資產管理體驗，可儲存、管理、探索及使用數位資產。 包含基本資產管理功能的簡化使用者介面。 專為輕量型DAM使用者設計，著重於上傳、中繼資料管理、搜尋、下載和共用。

有權存取「管理員」檢視的使用者也可以存取「資產」檢視。 Assets View提供簡化的使用者介面，讓您輕鬆管理、探索和分發數位資產。 來自不同職能部門（包括創意人員、行銷團隊和業務線團隊）的廣泛使用者可以針對資產進行共同作業，並在需要時隨時隨地存取正確的已核准資產。 許多隨意DAM使用者偏好「資產」檢視，因為它只包含功能的子集。 體驗的目標是創意人員、唯讀資產消費者和重量較輕的DAM使用者。

DAM程式庫、開發人員和超級使用者可視需要繼續使用「管理員」檢視，或在使用者介面之間切換。 您可以選取最適合您角色的體驗。

![add-tag](assets/newui-overview.svg)

如需如何存取「資產」檢視及其透過「管理員」檢視提供的一些簡化操作的資訊，請參閱 [「資產」檢視簡介](/help/assets/assets-view-introduction.md).

## 新資產功能 {#whats-new-assets}

重要的新功能是：

* [資產微服務](/help/assets/asset-microservices-overview.md)
* [資產上傳方法](/help/assets/add-assets.md)

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
