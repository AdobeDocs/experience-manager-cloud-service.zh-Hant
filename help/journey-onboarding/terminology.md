---
title: AEM as a Cloud Service 技術
description: 在您登入 AEMaaCS 之前，了解系統的一些術語及其基本結構會很有幫助。
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 87%

---

# AEM as a Cloud Service 技術 {#terminology}

在[上線歷程](overview.md)的這一部分，您將瞭解AEM as a Cloud Service的一些術語及其基本結構。

## 目標 {#objective}

現在您已閱讀檔案[入門準備](preparation.md)，瞭解入門流程的內容，那麼在登入前瞭解系統的一些術語及其基本結構會很有幫助。

AEM as a Cloud Service 是一種功能強大且靈活的工具，要使用任何工具，您應該熟悉它的組織以及用於描述它的術語和語言。本文件總結了您在開始使用該系統之前需要了解的一些關鍵術語。

閱讀本文件後，您應會了解

* 構成 AEMaaCS 的不同層。
* 每層的基本功能。

## AEMaaCS 結構 {#structure}

在此次入門歷程中，無需全面了解 AEM as a Cloud Service 的結構。但是熟悉以下概念將讓您更容易理解之後的歷程。

![Cloud Manager 結構](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **租用戶** - 每個客戶都佈建了一個租用戶。租用戶也稱為 IMS 組織 (本歷程稍後將詳細介紹 IMS)
* **方案** - 每個租用戶都有一個或多個方案，這些方案通常反映了客戶的授權解決方案。
* **環境** - 每個方案都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發目的。
* **存放庫** - 環境有一個或多個 Git 存放庫，可用於維護應用方案和前端方案碼。
* **工具和工作流程** - 管道管理從存放庫到環境的方案碼部署。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租用戶**。
* WKND Travel and Adventure Enterprises 租用戶可能有兩個&#x200B;**方案**：
   * WKND Magazine 部門的 Sites 方案
   * WKND Media 部門的 Assets 方案
* WKND Magazine 和 WKND Media 方案都有開發、測試和生產&#x200B;**環境**。
* **存放庫**&#x200B;用於維護 WKND Magazine 和 WKND Media 的自訂方案碼和應用方案。
* 有&#x200B;**各種工具和工作流程**&#x200B;在存放庫上運作，以便使用 CI/CD 管道、存取記錄、存取 AEM 等來部署程式碼。

## 下一步 {#what-is-next}

您已完成此 AEM 入門歷程部分，您應該了解：

* 構成 AEMaaCS 的不同層。
* 每層的基本功能。

以此知識為基礎並繼續您的 AEM 上線歷程，接著檢閱文件「[存取 Admin Console](admin-console.md)」，從中了解如何存取主控台，並驗證您身為系統管理員的身分。
