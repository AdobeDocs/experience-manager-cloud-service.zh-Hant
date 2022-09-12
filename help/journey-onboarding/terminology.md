---
title: AEMas a Cloud Service術語
description: 登入AEMaaCS之前，請先了解系統的一些術語及其基本結構，這是很有幫助的。
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# AEMas a Cloud Service術語 {#terminology}

在 [入門旅程，](overview.md) 您將學習AEM as a Cloud Service的一些術語及其基本結構。

## 目標 {#objective}

現在，您已了解導致上線程式的原因，請閱讀檔案 [入門準備，](preparation.md) 在登錄前，先了解系統的一些術語及其基本結構，這是很有幫助的。

AEM as a Cloud Service是功能強大且有彈性的工具，可讓您使用您應熟悉其組織以及用來說明的術語和語言的任何工具。 本檔案概述開始使用系統之前需要了解的一些重要術語。

閱讀本檔案後，您將了解：

* 組成AEMaaCS的不同層。
* 每個圖層功能的基本概念。

## AEMaCS結構 {#structure}

就本入門歷程而言，您不需要完全了解AEM as a Cloud Service的結構。 但熟悉下列概念後，在歷程的後續步驟將更為容易。

![Cloud Manager結構](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **租用戶**  — 每個客戶都布建了租用戶。 租用戶也稱為IMS組織（稍後此歷程會在IMS上提供更多資訊）
* **計畫。**  — 每個租戶都有一個或多個程式，這些程式通常反映客戶的授權解決方案。
* **環境**  — 每個方案有多個環境，例如針對即時內容的生產、一個用於測試，以及一個用於開發用途。
* **存放庫**  — 環境擁有一或多個Git存放庫，可維護應用程式和前端程式碼。
* **工具與工作流程**  — 管道管理從儲存庫到環境的代碼部署。

範例通常有助於將此階層與情境結合。

* WKND Travel and Adventure Enterprises可能是 **用戶** 以旅行相關媒體為主。
* WKND Travel and Adventure Enterprises租戶可能有兩個 **方案**:
   * WKND雜誌部的One Sites計畫
   * WKND媒體部一項資產計畫
* 《WKND雜誌》和《WKND Media》節目都有開發、測試和生產 **環境**.
* **儲存庫** 用於維護WKND雜誌和WKND媒體的自定義代碼和應用程式。
* 各種 **工具和工作流程** 跨存放區使用CI/CD管道、存取記錄、存取AEM等來部署程式碼。

## 下一步 {#what-is-next}

現在您已完成AEM入門歷程的這一部分，請您了解：

* 組成AEMaaCS的不同層。
* 每個圖層功能的基本概念。

借由下次閱讀檔案，繼續您的AEM入門歷程 [存取Admin Console](admin-console.md)，您將在此了解如何存取主控台，以及以系統管理員的身分驗證您的狀態。
