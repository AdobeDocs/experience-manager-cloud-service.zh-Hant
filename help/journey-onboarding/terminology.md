---
title: AEMas a Cloud Service術語
description: 在登錄AEMaaCS之前，瞭解系統的一些術語及其基本結構會有所幫助。
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# AEMas a Cloud Service術語 {#terminology}

在 [登機之旅，](overview.md) 您將學習一些as a Cloud Service的術AEM語和基本結構。

## 目標 {#objective}

現在，您通過閱讀文檔瞭解了導致登機過程的原因 [準備，](preparation.md) 在登錄前，瞭解系統的一些術語及其基本結構是有幫助的。

AEMas a Cloud Service是一種功能強大、靈活的工具，使用任何工具時，您都應熟悉它的組織以及描述它所使用的術語和語言。 本文檔總結了在開始使用系統之前需要瞭解的一些關鍵術語。

閱讀完此文檔後，您將瞭解：

* 組成AEMaaCS的不同層。
* 每個層的基本功能。

## AEMaaCS結構 {#structure}

在登機旅程中，不必完全理解AEMas a Cloud Service的結構。 但熟悉以下概念會讓在旅途的後期更容易跟進。

![雲管理器結構](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **租戶**  — 每個客戶都有租戶。 租戶也稱為IMS組織（本次旅程稍後更涉及IMS）
* **程式。**  — 每個租戶都有一個或多個計畫，這些計畫通常反映客戶的許可解決方案。
* **環境**  — 每個計畫都有多個環境，例如為即時內容製作、一個用於試運行，一個用於開發。
* **儲存庫**  — 這些環境具有一個或多個Git儲存庫，其中維護了應用程式和前端代碼。
* **工具和工作流**  — 管道管理從儲存庫到環境的代碼部署。

一個示例通常有助於將此層次結構置於背景中。

* WKND旅行和冒險企業可能是 **租戶** 以旅行相關媒體為主。
* WKND旅遊和冒險企業租戶可能有兩個 **方案**:
   * WKND雜誌部門的一個網站方案
   * WKND媒體部門的&quot;一項資產&quot;方案
* WKND雜誌和WKND媒體項目都將進行開發、準備和製作 **環境**。
* **儲存庫** 用於維護WKND雜誌和WKND媒體的自定義代碼和應用程式。
* 各種 **工具和工作流** 在repo中使用CI/CD管道、訪問日誌、訪問等部AEM署代碼。

## 下一步是什麼 {#what-is-next}

現在，您已完成登機旅AEM程的這一部分，您應該明白：

* 組成AEMaaCS的不同層。
* 每個層的基本功能。

在此知識的基礎上再接再厲，AEM繼續您的登機之旅，繼續閱讀文檔 [訪問Admin Console](admin-console.md)中，您將學習如何訪問控制台並以系統管理員的身份驗證您的狀態。
