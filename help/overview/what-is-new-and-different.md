---
title: 有何不同和新增 — Adobe Experience Manager as a Cloud Service
description: What Different and What New -Adobe Experience Manager(AEM)as a Cloud Service。
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 10%

---

# 新增功能與不同之處 {#what-is-new-and-what-is-different}

多年來，AEM兩者都有：

* On-Premise

* as a Managed Service

這些先前的方法之間存在內在的差異AEM,as a Cloud Service:

* [架構](#architecture)
* [升級](#upgrades)
* [Cloud Manager](#cloud-manager)
* [入門](#onboarding)
* [開發](#developing)
* [操作和效能](#operations-and-performance)
* [Identity Management](#identity-management)
* [創作用戶介面](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>這些概述並非詳盡無遺，但旨在介紹一下。

>[!NOTE]
>
>有關本地和托管服務版本的詳細資訊，請參閱 [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)。

## 架構 {#architecture}

>[!NOTE]
>
>有關詳細資訊，請參閱 [建築](/help/overview/architecture.md)。

AEM as a Cloud Service 現已具備：

* AEM 映像數量可變的動態架構。

![動態架構](assets/introduction-03.png "動態架構")

此架構特色：

* 根據&#x200B;*實際*&#x200B;流量和&#x200B;*實際*&#x200B;活動調整規模。

* 需要時才會執行某些個別例項。

* 使用模組化應用程式。

* 以製作叢集為預設值，這能避免因執行維護任務而發生停機狀況。

如此一來，架構就能根據多變的使用模式，自動調整規模：

![根據多變的使用模式自動調整規模](assets/introduction-04.png "根據多變的使用模式自動調整規模")


## 更AEM新 {#aem-updates}

AEMas a Cloud Service現在使用連續整合和連續交付(CI/CD)來確保項目處於最新的AEM版本。 這意味著生產實例和交叉實例將更新為最AEM新版本，而不會中斷用戶服務。

>[!NOTE]
>
>如果更新到生產環境失敗，Cloud Manager將自動回退登台環境。 此操作將自動執行，以確保在更新完成後，轉移環境和生產環境都處於同一AEM版本。

有兩種版本更AEM新類型：

* **維AEM護更新**

   * 可以每天發佈。
   * 主要用於維護目的，包括最新的錯誤修復和安全更新。
   * 由於定期應用更改，因此影響最小。

* **新功能更新**

   * 通過可預測的每月計畫發佈。

>[!TIP]
>
>有關詳細資訊，請參閱 [版AEM本更新](/help/implementing/deploying/aem-version-updates.md)。

## 雲管理器 {#cloud-manager}

Adobe雲管理器是as a Cloud Service的連續升級方法的一AEM個組成部分，因為它控制對您實例的所有更新 — 這是強制性的。

當新版本的雲服務可用時，Adobe可觸發更新。 或者，您可以使用Cloud Manager提供的管道觸發應用程式更新。

雲管理器是：

* 用於管理AEM程式和環境，

* as a Cloud Service的AEM要素；每個新租戶都首先設定為雲管理器訪問，

* 您的運營和開發人員的單一入口點。

具體而言，可從雲管理器AEM建立的程式的數量和類型可派生：

* 從客戶許可協定，

* 當as a Cloud Service用於AEM啟用或培訓時，

* 從外部驅動的流程(如從Adobe.com啟動的試驗)。

Cloud Manager已發展為自助服務門戶，在該門戶中可以建立AEM和配置as a Cloud Service的主要元件：

* 建立和管理新程式。 請參閱 [瞭解程式和程式類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 的子菜單。

* 在這些程式中創AEM建和管理環境。 請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 的子菜單。

* 建立和管理管道，以將客戶代碼和相關配置部署到特定環境。 請參閱 [配置CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 的子菜單。

* 收到有關這些元件的重要生命週期事件（例如產品更新）的通知。

Cloud Manager在多個地理區域的資料中心建立環境，提供全球覆蓋。 CDN存在點(PoP)確保為遍布全球的客戶提供低延遲內容。


## 入門 {#onboarding}

當將項目用作雲服AEM務時，啟動和管AEM理項目非常簡單，因為Adobe負責很多方面：

* 基線AEM影像針對特定使用情形進行優化。

* 許多手動配置任務已變為冗餘。

與現在的情況相比，這也有明顯不同：

* 一個評估階段，確保滿足所有先決條件；包括，例如：

   * 法律要求

   * 合同協定

   * 客戶定製的任何現有內容和/或代碼的技術要求

* 部署要求：

   * 代碼更新；任何為以前版本開發的客戶應用程式AEM都需要審查並可能更新。

   * 內容遷移

>[!TIP]
>
>有關登機過程的完整概述，請參閱 [登機之旅。](/help/journey-onboarding/overview.md)

## 開發 {#developing}

>[!NOTE]
>
>有關詳細資訊，請從 [發展指南](/help/implementing/developing/introduction/development-guidelines.md) 和 [開發 — WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

支援as a Cloud Service的新體AEM系結構涉及對整體開發人員體驗的一些關鍵更改。 as a Cloud Service的主要目標之AEM一是允許經驗豐富的客戶（已使用本地或Adobe Managed Services的上下文）盡可能快地遷移到AEMas a Cloud Service，而不必重寫其定制代碼的大部分。 不過，可能仍需要一些調整。

### 雲開發 {#aem-as-a-cloud-service-developing-cloud-development}

對於要在AEMas a Cloud Service上運行的現AEM有應用程式，需要執行以下步驟：

* 應用程式碼和配置必須儲存在關聯的Cloud Manager程式的Git代碼儲存庫中。
* 應用程式碼和配置必須與最新版本的基AEM線映像相容（可能每天都在更改）。
   * 必須使用與Cloud Manager環境關聯的Cloud Manager管道構建和部署客戶應用程式。
* 客戶應用程式必須通過管道中強制實施的所有代碼質量、安全性和效能門。
* 為客戶應用程式構建的映像必須由Cloud Manager管道部署。

此過程通常稱為雲優先開發。 由於端到端的持續時間預計需要幾分鐘（取決於應用程式的複雜性，從20分鐘到50分鐘），因此在雲中嘗試掛起的代碼和配置更改之前，必須採用快速開發方法。

Web控制台（其中管理OSGI捆綁包及其關聯配置，並且以前是QuickStart的一部分）在AEMas a Cloud Service中不再AEM可用。 新的開發人員控制台為大多數運行時資訊提供只讀介面。 使用此控制台，開發人員可以直接選擇並登錄作者或發佈服務的任何特定節點，並查看相關資訊。

>[!NOTE]
>
>另請參閱 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration)

開發人員的另一個常見要求是快速訪問各種環境的日誌檔案。 使用AEMas a Cloud Service，作者和發佈節點中不同節點的日誌檔案可通過雲管理器以可下載檔案或API的形式提供。

由於代碼和內容的明確分離，開發人員可以使用特定流程來更新內容作為部署的一部分。 可變內容的典型使用案例有：

* 標準 *預設* 作為客戶項目一部分的內容（例如，資料夾、模板、工作流等）

* 搜索索引定義

* ACL和權限

* 服務用戶和用戶組

### 地方發展 {#aem-as-a-cloud-service-developing-local-development}

為了支援快速迭代和開發，還有可能在as a Cloud Service上AEM下文之外開AEM發應用。 為此，開發人員可以使用以下項目：

* AEMas a Cloud Service快速啟動：a `.jar` 基於、獨立的最新代AEM碼庫安裝程式，具有相同的功能和API表面。

* AEMas a Cloud ServiceDispatcher SDK:用於本地測試和驗證調度程式配置的基於映像的過程

>[!NOTE]
>
>應該指出，雲快速啟動不允許AEM Sites和AEM Assets的所有功能。 它由一個簡單的作者環境組成，其中大多數的擴展都可以開發和測試。

## 操作和效能 {#operations-and-performance}

>[!NOTE]
>
>有關詳細資訊，請從 [備份](/help/operations/backup.md)、索引 [和其](/help/operations/indexing.md)他維護任務開始 [](/help/operations/maintenance.md)。

通AEM過as a Cloud Service，這些操作被自動化，因此不再需要任何服務中斷。

在以下方面：

* 許多任務已自動完成。

* 拓撲優化以實現最大的恢復力和效率；例如，預設為binaryless複製。

* 重負載任務（如隊列、作業和批量處理任務）已從核心實例中移AEM出，由共用和專用微服務處理。

新的監AEM控、報告和警報基礎架構還支援as a Cloud Service操作。 這使AdobeSRE（站點可靠性工程師）能夠主動保持服務的健康。 該建築的各種元素都配備了各種健康檢查。 如果由於某種原因認為體系結構的某個特定節點不健康，則該節點將從服務中刪除，並以靜默方式替換為新的健康節點。

## Identity Management {#identity-management}

>[!NOTE]
>
>有關詳細資訊，請參閱 [安全 — IMS支援](/help/security/ims-support.md)。

對as a Cloud Service的一AEM個主要改變是完全整合地使用AdobeID訪問作者層。

這需要使用 [Adobe管理控制台](https://helpx.adobe.com/enterprise/using/admin-console.html) 用於管理用戶和組。 用戶帳戶使您的用戶能夠訪問Adobe產品和服務，因為用戶配置檔案資訊集中在AdobeIdentity Management系統(IMS)中，以便在所有雲服務中共用。 一旦分配了訪AEM問權限，用戶帳戶就可以AEM在as a Cloud Service中引用（如以前）;例如，用於從「安全」用戶介面定AEM義角色和權限。

這結合了以下優點：

* 使用AdobeIdentity Management系統(IMS)在所有Adobe雲應用程式中提供單點登錄。

* 用戶首選項保留給每個特定的AEMas a Cloud Service實例。

## 創作用戶介面 {#authoring-user-interface}

>[!NOTE]
>
>有關進一步詳情， [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md) 是個好起點。

對於「站點」和「資產」，創作用戶介面(UI)的基本原則對於過去使用過的任何人都AEM非常熟悉。

主要區別是用戶介面完全支援觸摸；經典UI不再可用。 否則，基本要素保持不變，只有微小的變化。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sitesas a Cloud Service通過將內容管理系統與數字資產管理功能相結合，為客戶提供個性化、以內AEM容為導向的AEM體驗。

有關詳細資訊，請參閱 [站點更改](/help/sites-cloud/sites-cloud-changes.md)。

## AEM Assets {#aem-assets}

Adobe Experience Manager資產as a Cloud Service提供雲本地PaaS解決方案，讓企業不僅能夠以快速和有影響的方式執行其數字資產管理和Dynamic Media操作，而且還使用新一代智慧功能，如AI/ML，從始終最新、始終可用且始終學習的系統中進行。

資產產品包括雲中的下一代資產處理以及高效能資產接收和搜索。

有關詳細資訊，請參閱 [資產概述和簡介as a Cloud Service](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

有關詳細資訊，請參閱：

* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
* [AEM Sites as a Cloud Service 重大變更](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
* [介紹AEM Assetsas a Cloud Service](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

>[!TIP]
>
>一旦您概述了AEMas a Cloud Service，您就可以通過查看 [登機之旅。](/help/journey-onboarding/overview.md)
>
>已裝上或準備好深入測試功AEM能？ 安裝 [參AEM考演示附件](/help/journey-sites/demos-add-on/overview.md) 使用豐AEM富的示例來探索功能。
