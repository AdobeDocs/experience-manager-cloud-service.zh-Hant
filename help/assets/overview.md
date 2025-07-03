---
title: 使用 AEM 進行 Adobe 數位資產管理 (DAM)
description: 了解如何使用 Experience Manager Assets as a Cloud Service 來使用和管理 Adobe 數位資產管理 (DAM)。
contentOwner: AK
feature: Asset Management
role: User, Leader, Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '927'
ht-degree: 100%

---


# 在 AEM 中為數位資產管理引入 Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] 為企業提供一種雲端原生的 PaaS 解決方案，不僅可以快速有效地執行數位資產管理和動態媒體操作，而且還使用始終最新、可用且不斷學習之系統的下一代智慧功能 (例如 AI/ML)。

同時擷取許多資產或複雜資產是 Experience Manager 編寫執行個體的資源密集型任務。主執行個體在新增、處理甚至移轉資產時會消耗大量 CPU、記憶體和 I/O 資源。此類效能問題會影響一般使用者的編寫和瀏覽體驗。

企業需要支援各種檔案格式和內容解析度，以適用於多設備、跨地理位置和多語言的使用案例。資產處理和儲存要求所需要的資源和功能可能會使傳統解決方案負擔過重。有時，資產處理的技術限制不會產生預期的結果，而在其他時候，儲存成本不利於營利。

首先，了解對於數位資產管理而言，[雲端原生產品帶來的優勢](#solution-benefits)。查看值得注意的 [Experience Manager as a  [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) 幾項變更，這些變更也會影響 Experience Manager Assets，接者是值得注意的 [Assets 變更](/help/assets/assets-cloud-changes.md)。

繼續閱讀以了解[新 Assets 功能的詳細資訊](#whats-new-assets)和[已知問題](/help/release-notes/maintenance/latest.md)。查看[已過時或移除的功能](/help/release-notes/deprecated-removed-features.md)清單以了解此版本已刪除的功能。最後，借助此[術語表](/help/overview/terminology.md)了解 Experience Manager 術語。

## 解決方案優勢 {#solution-benefits}

以下是對於數位資產管理而言，Assets as a [!DNL Cloud Service] 帶來的重要優勢。如需更多資訊，請參閱 [Experience Manager as a  [!DNL Cloud Service]](/help/overview/introduction.md) 概觀。

* **用於資產處理的現代雲端服務**：新的資產微服務是一種雲端型、可擴展、可靠且簡單易用的資產處理服務。
* **高度可擴展**：具擴展性、跨所有部署類型。隨時按需求提供實際上不限數量的資源。與傳統系統相比，節省了過度設計的成本。
* **最新軟體**：始終最新且始終更新。所有使用者都只能使用最新軟體，其中包含所有可用的修補程式、功能、安全性和錯誤修正。開發人員和整合者使用最新的一組 API，沒有多版本支援問題。
* **始終提供服務**：零停機時間 (0dt)，這要歸功於部署在具有備份和備援之叢集中的執行個體。升級也是 0dt。
* **持續監控**：系統監控是自動化的，內建的檢查和觸發機制有助於維護效能、可用性和整體穩健性。
* **輕鬆部署**：Experience Manager 在雲端中的操作完全自動化，無需人工介入。對於自動化部署，Cloud Manager (CM) 元件會自動建置包含您自訂程式碼的可部署 Docker 影像。

## 適用於數位資產管理以角色為主的體驗 {#persona-based-experiences}

Adobe 為您提供健全的數位資產管理 (DAM) 解決方案，可供您善加利用您的數位資產。Adobe Experience Manager Assets 具有兩種使用同一雲端服務存放庫的獨立體驗：

* **管理員檢視**：現有的 Assets as a Cloud Service 使用者介面。使用管理視圖來實現所有高階數位資產管理功能，包括整合、工作流程、內容自動化、發布等。

* **資產檢視**：Adobe 的輕量型資產管理體驗，可儲存、管理、探索和使用數位資產。簡化的使用者介面包含基本的數位資產管理功能。專為輕量型 DAM 使用者設計，重點在上傳、中繼資料管理、搜尋、下載和共享。

可存取管理員檢視的使用者也可以存取資產檢視。資產檢視提供簡化的使用者介面，使您可輕鬆管理、探索和分發數位資產。來自不同職能部門 (包括創意、行銷和業務線團隊) 的廣泛使用者可以進行資產共同作業，並視需要隨時地存取正確的已核准資產。許多臨時 DAM 使用者偏好使用資產檢視，因為它只包含功能的子集。該體驗的目標對象是唯讀創意資產的取用者以及輕量型 DAM 使用者。

DAM 圖書管理員、開發人員和超級使用者可以繼續使用管理員檢視或視需要切換使用者介面。您可以選擇最適合您角色的體驗。

![新增標記](assets/newui-overview.svg)

如需了解如何存取資產檢視和管理員檢視帶來的一些簡化操作，請參閱[資產檢視簡介](/help/assets/assets-view-introduction.md)。

## 與 Edge Delivery Services 的文件型製作整合 {#integrate-doc-authoring-edge-and-assets}

Edge Delivery 讓您能夠建立快速、引人入勝的網站，作者可以在其中快速更新和發佈內容，並且可以快速啟動新網站。

將 AEM Assets 與 Edge Delivery Services 文件型製作整合，讓網站作者能夠在 Microsoft Word 或 Google Docs 中撰寫文件時使用 AEM Assets 存放庫中提供的影像。如需詳細資訊，請參閱「[將 AEM Assets 與文件型製作整合](/help/edge/using.md#integrate-assets-edge)」。

## 與 Adobe Journey Optimizer 整合 {#integration-with-ajo}

[Adobe Journey Optimizer](https://business.adobe.com/products/journey-optimizer/adobe-journey-optimizer.html)：可為客戶簡化歷程管理，以為全通道行銷活動提供智慧型決策和見解。使用 Journey Optimizer 設計訊息時，您可以直接從 Journey Optimizer 介面存取 Assets as a Cloud Service 存放庫。使用者使用 Experience Manager Assets 的嵌入使用者介面存取資產。有關詳細資訊，請參閱[使用 Experience Manager Assets 建立和管理資產](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/assets-images/assets.html?lang=zh-Hant)。

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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
