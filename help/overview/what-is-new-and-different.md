---
title: Adobe Experience Manager是Cloud Service
description: '什麼不同，什麼新—Adobe Experience Manager(AEM)作為Cloud Service。 '
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 10%

---


# 新增功能與不同之處 {#what-is-new-and-what-is-different}

多年來，AEM兩者都有：

* On-Premise

* 作為受管理服務

以前的這些方法和作為一個Cloud Service,AEM有著內在的差異：

* [架構](#architecture)
* [升級](#upgrades)
* [Cloud Manager](#cloud-manager)
* [入門](#onboarding)
* [開發](#developing)
* [操作與效能](#operations-and-performance)
* [Identity Management](#identity-management)
* [編寫使用者介面](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>這些概述並非詳盡無遺，但旨在作一介紹。

>[!NOTE]
>
>有關內部部署和受管理服務版本的詳細資訊，請參見[AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html)的文檔集。

## 架構 {#architecture}

>[!NOTE]
>
>有關詳細資訊，請參見[ Architecture](/help/core-concepts/architecture.md)。

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


## AEM更新{#aem-updates}

>[!NOTE]
>如需詳細資訊，請參閱[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

作AEM為Cloud Service，現在使用「持續整合與持續傳送」(CI/CD)來確保您的專案使用最新AEM版本。 這表示Production和Stage實例會更新為最新版本，AEM而不會中斷用戶的服務。

>[!NOTE]
> 如果更新到生產環境失敗，Cloud Manager將自動回滾階段環境。 這會自動執行，以確保更新完成後，階段和生產環境都位於同一版AEM本。

版本AEM更新有兩種類型：

* **推AEM送更新**

   * 可以每天發佈。
   * 主要是維護，包括最新的錯誤修正和安全性更新。

      隨著變更的定期套用，影響會逐漸增加，降低對服務的影響。

* **新功能更新**

   * 透過可預測的每月排程發佈。

## Cloud Manager {#cloud-manager}

Adobe雲管理器是Cloud Service的持續升級方AEM法的一部分，因為它控制對實例的所有更新——這是必備的。

當有新版雲端服務可供使用時，Adobe可觸發更新。 或者，您也可以使用Cloud Manager提供的管線觸發應用程式更新。

Cloud Manager是：

* 用於管理AEM程式和環境，

* 是Cloud Service的AEM重要組成部分；每個新租用戶都會先布建Cloud Manager存取權，

* 為您的營運與開發人員提供單一入門點。

具體來說，可從Cloud Manager建立的程AEM序的數量和類型可以派生：

* 從客戶授權合約，

* 當Cloud Service用於實AEM現或訓練時，從內部驅動的角色獲得，

* 來自外部驅動程式，例如從Adobe.com開始的試用。

Cloud Manager已發展為自助服務門戶，可以建立和配置作為AEMCloud Service的主要元件：

* 建立和管理新程式。 有關詳細資訊，請參閱[瞭解程式和程式類型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)。

* 在這些程式中創AEM建和管理環境。 有關詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md)。

* 建立並管理將客戶代碼和相關配置部署到特定環境的管道。 有關詳細資訊，請參閱[配置CI-CD管線](/help/implementing/cloud-manager/configure-pipeline.md)。

* 收到這些元件的重要生命週期事件通知（例如產品更新）。

Cloud Manager在多個地理區域的資料中心建立環境，提供全球覆蓋。 CDN線上存放點(PoP)可確保為全球各地的客戶提供低延遲的內容。

>[!NOTE]
>請參閱[以Cloud Service形式訪問Experience Manager](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md)以開始以Cloud Service形式使用Cloud ManagerAEM。

## 入門 {#onboarding}

>[!NOTE]
>
>如需詳細資訊，請參閱[入門](/help/onboarding/home.md)。

當以雲端服務AEM的身分使用專AEM案做為Adobe時，啟動和管理專案很簡單：

* 基線AEM影像會針對特定使用案例最佳化。

* 許多手動配置任務已變得冗餘。

與現在的情況也大不相同：

* 評估階段，以確保符合所有先決條件；包括，例如：

   * 法律要求

   * 合約協定

   * 客戶自訂之任何現有內容及／或程式碼的技術需求

* 部署需求：

   * 程式碼更新；任何針對舊版開發的客戶應用程式都AEM需要進行審查並可能進行更新。

   * 內容移轉

## 開發 {#developing}

>[!NOTE]
>
>如需詳細資訊，您可從[開發方針](/help/implementing/developing/introduction/development-guidelines.md)和[開發- WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)開始。

新的架構支援AEM為Cloud Service，包含對整體開發人員體驗的一些重要變更。 Cloud Service的主要目AEM標之一，是讓經驗豐富的客戶(已使用AEM內部部署或在Adobe Managed Services中)盡快移轉至AEMCloud Service，而不需重寫其自訂程式碼的大部分。 不過，可能仍需要進行一些調整。

### 雲端開發{#aem-as-a-cloud-service-developing-cloud-development}

對於要以AEMCloud Service形式運AEM行的現有應用程式，需要執行以下步驟：

* 應用程式碼和配置必須儲存在關聯的Cloud Manager程式的Git代碼儲存庫中。
* 應用程式碼和設定必須與最新版本的基準影AEM像相容（可能每天都會變更）。
   * 客戶應用程式必須使用與Cloud Manager環境關聯的Cloud Manager管道構建和部署。
* 客戶應用程式必須傳遞管道中強制執行的所有程式碼品質、安全性和效能閘道。
* 為客戶應用程式構建的映像必須由Cloud Manager管道部署。

此程式通常稱為雲端開發。 由於端對端持續時間預計需要幾分鐘（視應用程式的複雜性而定，從20到50），因此在雲端嘗試進行擱置中的程式碼和組態變更之前，必須採用快速開發方法。

Web Console（其中管理OSGI捆綁包及其相關配置，並且以前是QuickStart的一部分）不再作為Cloud Service環境的用戶直接訪問該Web Console（Web控制台）AEM。 此介面仍可透過使用新的開發人員主控台，以唯讀模式存取。 使用此主控台，開發人員可直接選擇並登入作者或發佈服務的任何特定節點，然後存取預設封鎖的區域。

>[!NOTE]
>
>另請參見[OSGi Configuration](/help/implementing/deploying/overview.md#osgi-configuration)

開發人員的另一個常見需求是快速存取各種環境的記錄檔。 作為AEMCloud Service，作者和發佈節點中不同節點的日誌檔案可通過Cloud Manager使用，其形式可以是可下載的檔案，也可以是通過API。

由於程式碼和內容的明確分離，開發人員可使用特定程式來更新部署中的內容。 可變內容的典型使用案例包括：

* 客戶專案的標準&#x200B;*預設*&#x200B;內容（例如，資料夾、範本、工作流程等）

* 搜索索引定義

* ACL和權限

* 服務使用者和使用者群組

### 本地開發{#aem-as-a-cloud-service-developing-local-development}

為了支援快速的反覆作業與開發，您也可在外部開AEM發應用程AEM式做為Cloud Service。 為此，開發人員可使用下列物件：

* 作為AEMCloud Service快速入門：以`.jar`為基礎、獨立安裝的最新程式碼AEM庫安裝程式，具有相同的功能和API表面。

* The AEM as aCloud ServiceDispatcher SDK:在本地測試和驗證Dispatcher配置的基於映像的過程

>[!NOTE]
>
>應當指出，雲快速入門不允許AEM Sites和AEM Assets的所有功能。 它由簡單的作者環境組成，其中大部分的擴充功能都可進行開發和測試。

## 操作和效能{#operations-and-performance}

>[!NOTE]
>
>有關詳細資訊，請從 [備份](/help/operations/backup.md)、索引 [和其](/help/operations/indexing.md)他維護任務開始 [](/help/operations/maintenance.md)。

作AEM為Cloud Service，此類操作可自動執行，因此不再需要任何服務中斷。

在這些領域：

* 許多任務都實現了自動化。

* 優化拓撲以實現最大的恢復能力和效率；例如，無二進位複製是預設值。

* 大量負載任務（如隊列、作業和批量處理任務）已移出核心實例，AEM由共用和專用的微服務處理。

新的監AEM控、報告和警報基礎架構也支援作為Cloud Service的操作。 這可讓AdobeSRE（現場可靠性工程師）主動保持服務的健康。 該建築的各種元素都配備了各種健康檢查。 如果由於某種原因，體系結構的某個特定節點被認為不健康，則該節點將從服務中刪除，並無訊息地被新的健康節點所取代。

## Identity Management{#identity-management}

>[!NOTE]
>
>如需詳細資訊，請參閱[安全性- IMS支援](/help/security/ims-support.md)。

Cloud Service的主AEM要變更是完全整合使用AdobeID來存取作者層。

這需要使用[Adobe管理控制台](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理使用者和使用者群組。 使用者帳戶可讓您的使用者存取Adobe產品和服務，因為使用者個人檔案資訊會集中在AdobeIdentity Management系統(IMS)中，以便在所有雲端服務間共用。 一旦將存取權指AEM派給，使用者帳戶就可AEM以參照為Cloud Service（如先前）;例如，用於從「安全」用戶介面定義角AEM色和權限。

這結合了以下優點：

* 使用AdobeIdentity Management系統(IMS)在所有Adobe雲端應用程式中提供單一登入。

* 使用者偏好設定仍屬於每個特定例項的本AEM機Cloud Service。

## 編寫用戶介面{#authoring-user-interface}

>[!NOTE]
>
>有關詳細資訊，[基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)是一個好的起點。

網站和資產的製作使用者介面(UI)的基本原則，對於過去使用過的人而言都非AEM常熟悉。

主要的不同在於，使用者介面完全可觸控；傳統UI已不再可用。 否則，基本功能保持不變，只有微小的變更。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites是Cloud Service，通過將內容管理系統的強大功能與數位資產管理相結合，您可以為客戶提供個AEM人化的內AEM容引導體驗。

如需詳細資訊，請參閱[網站變更](/help/sites-cloud/sites-cloud-changes.md)概觀。

## AEM Assets {#aem-assets}

Adobe Experience Manager資產Cloud Service提供雲端原生PaaS解決方案，讓企業不僅能以快速且具影響力的方式執行其數位資產管理和Dynamic Media業務，還可在永遠最新、永遠可用且永遠學習的系統中使用新一代智慧功能，例如AI/ML。

資產產品包括雲端的新一代資產處理，以及高效能資產擷取與搜尋。

如需詳細資訊，請參閱[概觀和資產Cloud Service簡介](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

如需詳細資訊，請參閱：

* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service [架構](/help/core-concepts/architecture.md)
* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
* [AEM Sites as a Cloud Service 重大變更](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
* [將AEM Assets作為Cloud Service](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教學課程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
