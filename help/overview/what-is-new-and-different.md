---
title: 不同之處與新增功能 - Adobe Experience Manager as a Cloud Service
description: 不同之處與新增功能 - Adobe Experience Manager (AEM) as a Cloud Service。
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 97%

---

# 新增功能與不同之處 {#what-is-new-and-what-is-different}

AEM 這麼多年來一直透過以下方式提供：

* 內部部署

* as a Managed Service

這些先前的方法與 AEM as a Cloud Service 之間在本質上存在差異：

* [架構](#architecture)
* [升級](#upgrades)
* [Cloud Manager](#cloud-manager)
* [上線](#onboarding)
* [開發](#developing)
* [運作和效能](#operations-and-performance)
* [Identity Management](#identity-management)
* [編寫使用者介面](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>這些概述並不詳盡，而是旨在提供簡介。

>[!NOTE]
>
>如需內部部署和受管理服務版本的更多詳細資訊，請參閱 [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant) 的文件集。

## 架構 {#architecture}

>[!NOTE]
>
>如需更多詳細資訊，請參閱[架構](/help/overview/architecture.md)。

AEM as a Cloud Service 現已具備：

* AEM 影像數量可變的動態架構。

![動態架構](assets/introduction-03.png "動態架構")

此架構特色：

* 根據&#x200B;*實際*&#x200B;流量和&#x200B;*實際*&#x200B;活動調整規模。

* 需要時才會執行某些個別執行個體。

* 使用模組化應用程式。

* 以作者叢集為預設值，這能避免因執行維護任務而發生停機狀況。

如此一來，架構就能根據多變的使用模式，自動調整規模：

![根據多變的使用模式自動調整規模](assets/introduction-04.png "根據多變的使用模式自動調整規模")


## AEM 更新 {#aem-updates}

AEM as a Cloud Service 現在使用持續整合與持續傳送 (CI/CD) 來確保您的專案使用最新的 AEM 版本。這表示生產和預備執行個體會更新到最新的 AEM 版本，而不會對使用者中斷服務。

>[!NOTE]
>
>如果生產環境更新失敗，Cloud Manager 會自動復原預備環境。這是自動完成的，以確保在更新完成後，預備環境和生產環境使用相同的 AEM 版本。

AEM 版本更新有兩種類型：

* **AEM 維護更新**

   * 可以每天發行。
   * 主要用於維護目的，包括最新的錯誤修正和安全性更新。
   * 因為定期套用變更，可將影響降至最低。

* **新功能更新**

   * 透過可預測的每月排程發行。

>[!TIP]
>
>如需更多詳細資訊，請參閱 [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)。

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager 是 AEM as a Cloud Service 的持續升級方法不可或缺的一部分，因為它控制對您執行個體的所有更新 - 這是強制的。

當有新的雲端服務版本可用時，Adobe 可以觸發更新。或者，您可以使用 Cloud Manager 提供的管道觸發應用程式更新。

Cloud Manager 是：

* 用於管理 AEM 方案和環境，

* AEM as a Cloud Service 的重要元件；首先為每個新租用戶提供 Cloud Manager 存取權，

* 您的營運和開發人員的單一進入點。

具體而，可以從 Cloud Manager 建立之 AEM 方案的數量和類型來自：

* 客戶授權協議，

* 內部驅動的動作項目 (當 AEM as a Cloud Service 用於啟用或訓練時)，

* 外部驅動的流程，例如從 Adobe.com 開始的試用。

Cloud Manager 已經發展成自助式入口網站，可以在其中建立和設定 AEM as a Cloud Service 的主要元件：

* 建立及管理新方案。如需詳細資訊，請參閱[了解方案和方案類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

* 在這些方案中建立和管理 AEM 環境。如需詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md)。

* 建立和管理用於將客戶程式碼和相關設定部署到特定環境的管道。如需詳細資訊，請參閱[設定您的 CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

* 收到有關這些元件的重要生命週期事件的通知 (例如，產品更新)。

Cloud Manager 在跨多個地理區域的資料中心建立環境，使用範圍包含全球。CDN 網路服務提供點 (PoP) 確保為世界各地的客戶提供低延遲內容傳遞服務。


## 上線 {#onboarding}

使用 AEM as a Cloud service 時，啟動和管理 AEM 專案非常簡單，因為 Adobe 負責許多方面：

* 基準 AEM 影像針對特定使用案例進行最佳化。

* 許多手動設定工作已變得多餘。

它也與現在有很大不同：

* 確保滿足所有先決條件的評估階段；包括，例如：

   * 法律要求

   * 合同協議

   * 任何現有內容和/或客戶自訂程式碼的技術要求

* 部署要求：

   * 程式碼更新；為舊版 AEM 開發的任何客戶應用程式都需要審查並可能進行更新。

   * 內容移轉

>[!TIP]
>
>如需上線流程的完整概觀，請參閱[上線流程。](/help/journey-onboarding/overview.md)

## 開發 {#developing}

>[!NOTE]
>
>如需更多詳細資訊，您可以從[開發指南](/help/implementing/developing/introduction/development-guidelines.md)和[開發 - WKND 教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)開始。

支援 AEM as a Cloud Service 的新架構涉及對整體開發人員體驗的一些重要變更。AEM as a Cloud Service 的主要目標之一是讓有經驗的客戶 (已經在使用內部部署或做為 Adobe Managed Services 的 AEM) 盡快移轉到 AEM as a Cloud Service，而無需重寫他們的大部分自訂程式碼。但是，可能仍需要進行一些調整。

### 雲端開發 {#aem-as-a-cloud-service-developing-cloud-development}

對於要在 AEM as a Cloud Service 上執行的現有 AEM 應用程式，需要執行以下步驟：

* 應用程式的程式碼和設定必須儲存在關聯的 Cloud Manager 方案的 Git 程式碼存放庫中。
* 應用程式的程式碼和設定必須與最新版本的基準 AEM 影像 (可能每天都在變化) 相容。
   * 必須使用與 Cloud Manager 環境關聯的 Cloud Manager 管道建置和部署客戶應用程式。
* 客戶應用程式必須通過管道中強制執行的所有程式碼品質、安全性和效能閘道。
* 為客戶應用程式建置的影像必須由 Cloud Manager 管道部署。

此過程通常稱為雲端優先開發。由於端到端的持續時間預計需要幾分鐘 (從 20 到 50 不等，取決於應用程式的複雜性)，因此有必要採用快速開發方法，以避免在雲端嘗試變更擱置的程式碼和設定。

Web 主控台，這個管理 OSGI 套件及其關聯設定的地方，先前也是 AEM QuickStart 的一部分，現在 AEM as a Cloud Service 已不再提供。新的開發人員主控台提供了大部分執行階段資訊的唯讀介面。有了這個主控台，開發人員可以選擇並直接登入作者或發佈服務的任何特定節點，並檢視相關資訊。

>[!NOTE]
>
>另請參閱 [OSGi 設定](/help/implementing/deploying/overview.md#osgi-configuration)

開發人員的另一個常見需求是快速存取各種環境的記錄檔。有了 AEM as a Cloud Service，作者或發佈節點中的不同節點的記錄檔可經由 Cloud Manager 取得，採用可下載的檔案形式或透過 API。

由於程式碼和內容的明確分離，開發人員可以使用特定過程來更新內容作為部署的一部分。可變內容的典型使用案例：

* 客戶專案內含的標準&#x200B;*預設*&#x200B;內容 (例如資料夾、範本、工作流程等)

* 搜尋索引定義

* ACL 與權限

* 服務使用者和使用者群組

### 本機開發 {#aem-as-a-cloud-service-developing-local-development}

為了支援快速反複和開發，您也可以在AEMas a Cloud Service環境之外開發AEM應用程式。 為此，開發人員可以使用以下成品：

* AEM as a Cloud Service QuickStart：最新 AEM 程式碼庫的以 `.jar` 為基礎、獨立的安裝程式，具有相同的功能和 API 介面。

* AEM as a Cloud Service Dispatcher SDK：以影像為基礎的流程，用於在本機測試和驗證 Dispatcher 設定

>[!NOTE]
>
>應注意，Cloud QuickStart 不允許使用所有 AEM Sites 和 AEM Assets 功能。它包含一個簡單的作者環境，可以在其中開發和測試大部分的擴充功能。

## 運作和效能 {#operations-and-performance}

>[!NOTE]
>
>有關詳細資訊，請從[備份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他維護任務開始](/help/operations/maintenance.md)。

使用 AEM as a Cloud Service，此類操作是自動進行，因此不再需要中斷任何服務。

在這些區域：

* 許多任務已經自動化。

* 拓撲經過最佳化以實現最大的彈性和效率；例如，預設採用無二進位複製。

* 負載過重的任務 (例如佇列、工作和大量處理任務) 已移出核心 AEM 執行個體，由共用和專用微服務處理。

AEM as a Cloud Service 的操作也受到新的監控、報告和警報基礎結構的支援。這可讓 Adobe SRE (網站可靠性工程師) 主動維持這些服務的健康狀態。結構的各種元素都具有各種健康檢查。如果基於某種原因，結構的特定節點被視為不健康，該節點就會移出服務，並自動替換成健康的新節點。

## Identity Management {#identity-management}

>[!NOTE]
>
>如需更多詳細資訊，請參閱[安全性 - IMS 支援](/help/security/ims-support.md)。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取作者層。

這需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 來管理使用者和使用者群組。使用者帳戶可讓您的使用者存取 Adobe 產品和服務，因為使用者個人資料集中在 Adobe Identity Management System (IMS)，可跨所有雲端服務共用。獲得 AEM 存取權後，可以在 AEM as a Cloud Service 中參考使用者帳戶 (如同以往)；例如，用於定義 AEM 安全性使用者介面的角色和權限。

此做法結合以下優點：

* 可使用 Adobe Identity Management System (IMS) 提供跨所有 Adobe 雲端應用程式的單一登入。

* 每個特定 AEM as a Cloud Service 執行個體的使用者偏好設定續存在本機。

## 編寫使用者介面 {#authoring-user-interface}

>[!NOTE]
>
>如需更多詳細資訊，[基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)是很好的起點。

對於Sites和Assets而言，過去使用AEM的任何人都會非常熟悉編寫使用者介面(UI)的基本原則。

主要區別在於 UI 是純觸控的；不再提供傳統 UI。除此以外，基本原理保持不變，只有很小的變化明顯。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service 結合 AEM 內容管理系統與 AEM 數位資產管理的強大功能，協助您為客戶提供內容導向的個人化體驗。

如需詳細資訊，請參閱 [Sites 變更](/help/sites-cloud/sites-cloud-changes.md) 的概觀。

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service 為企業提供一種雲端原生的 PaaS 解決方案，不僅可以快速有效地執行數位資產管理和動態媒體操作，而且還使用始終最新、可用且不斷學習之系統的下一代智慧功能 (例如 AI/ML)。

資產方面的產品包括下一代雲端資產處理以及高效能資產擷取和搜尋。

如需詳細資訊，請參閱 [Assets as a Cloud Service 概觀和簡介](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

如需進一步詳細資訊，請參閱：

* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
* [AEM Sites as a Cloud Service 重大變更](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
* [AEM Assets as a Cloud Service 簡介](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

>[!TIP]
>
>大致了解 AEM as a Cloud Service 後，您可以透過查看[入門歷程](/help/journey-onboarding/overview.md)來快速入門。
>
>已經入門或準備好深入測試 AEM 功能？安裝 [AEM 參考示範附加元件](/help/journey-sites/demos-add-on/overview.md)以使用豐富的範例探索 AEM 的強大功能。
