---
title: 不同之處與新增功能 — Adobe Experience Manager as a Cloud Service
description: 不同與新增功能 — Adobe Experience Manager(AEM)as a Cloud Service。
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: f8695dd8fdc9ffb203bab943c335ab2957df6251
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 新增功能與不同之處 {#what-is-new-and-what-is-different}

多年來，AEM已同時提供：

* On-Premise

* as a Managed Service

先前的這些方法與AEM的as a Cloud Service有內在差異：

* [架構](#architecture)
* [升級](#upgrades)
* [Cloud Manager](#cloud-manager)
* [入門](#onboarding)
* [開發](#developing)
* [操作與效能](#operations-and-performance)
* [Identity Management](#identity-management)
* [製作使用者介面](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>這些概述並非詳盡無遺，而是旨在提供簡介。

>[!NOTE]
>
>如需內部部署和托管服務版本的詳細資訊，請參閱 [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant).

## 架構 {#architecture}

>[!NOTE]
>
>如需詳細資訊，請參閱 [架構](/help/overview/architecture.md).

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


## AEM更新 {#aem-updates}

>[!NOTE]
>如需詳細資訊，請參閱 [AEM版本更新](/help/implementing/deploying/aem-version-updates.md).

AEM as a Cloud Service現在使用「持續整合」和「持續傳送」(CI/CD)，確保您的專案使用最新的AEM版本。 這表示生產和預備執行個體會更新至最新的AEM版本，而不會中斷使用者的服務。

>[!NOTE]
> 如果更新至生產環境失敗，Cloud Manager將自動回滾預備環境。 這會自動完成，以確保更新完成後，預備和生產環境都處於相同的AEM版本。

AEM版本更新有兩種類型：

* **AEM推播更新**

   * 可每天發佈。
   * 主要是維護作業，包括最新的錯誤修正和安全性更新。

      由於定期應用更改，因此影響是增量的，因此減少了對服務的影響。

* **新功能更新**

   * 透過可預測的每月排程發佈。

## Cloud Manager {#cloud-manager}

AdobeCloud Manager是AEMas a Cloud Service持續升級方法的必要元件，因為它可控制您執行個體的所有更新 — 此為必要項目。

有新版本的雲端服務可供使用時，Adobe可觸發更新。 或者，您也可以使用Cloud Manager提供的管道觸發應用程式更新。

Cloud Manager是：

* 用於管理AEM程式和環境，

* AEM as a Cloud Service的必要元件；每個新租用戶都先布建為Cloud Manager存取權，

* 操作和開發人員的單一入口點。

具體而言，可從Cloud Manager建立的AEM程式數目和類型可衍生出來：

* 從客戶授權合約，

* 使用AEMas a Cloud Service進行培訓或訓練時，從內部驅動的演員開始，

* 從Adobe.com開始的試驗等外部驅動過程。

Cloud Manager已演變為自助入口網站，可在此建立及設定AEMas a Cloud Service的主要元件：

* 建立和管理新方案。 請參閱 [了解方案和方案類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) 以取得更多詳細資訊。

* 在這些方案中建立和管理AEM環境。 請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 以取得更多詳細資訊。

* 建立和管理管道，以便將客戶代碼和相關配置部署到特定環境。 請參閱 [設定CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 以取得更多詳細資訊。

* 系統會通知這些元件的重要生命週期事件（例如產品更新）。

Cloud Manager在多個地理區域的資料中心中建立環境，提供全球覆蓋。 CDN線上連結(PoP)可確保為遍布全球的客戶提供低延遲的內容傳遞。


## 入門 {#onboarding}

>[!NOTE]
>
>如需詳細資訊，請參閱 [入門](/help/onboarding/home.md).

使用AEM as a Cloud Service作為Adobe時，啟動和管理AEM專案的作業相當簡單明瞭，因為其需負責許多方面：

* 基線AEM影像會針對特定使用案例最佳化。

* 許多手動配置任務都是冗餘的。

與現在的情況也有很大不同：

* 評估階段，以確保滿足所有必要條件；包括，例如：

   * 法律要求

   * 合同協定

   * 客戶自訂的任何現有內容和/或代碼的技術要求

* 部署需求：

   * 代碼更新；任何針對舊版AEM開發的客戶應用程式都需經過審核，且可能需要更新。

   * 內容移轉

## 開發 {#developing}

>[!NOTE]
>
>如需詳細資訊，請先 [開發准則](/help/implementing/developing/introduction/development-guidelines.md) 和 [開發 — WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

支援AEMas a Cloud Service的新架構包含對整體開發人員體驗的一些重要變更。 AEMas a Cloud Service的主要目標之一，是讓經驗豐富的客戶(在內部部署或Adobe Managed Services的情境下使用AEM)能盡快移轉至AEMas a Cloud Service，而無須重寫其大量自訂程式碼。 然而，可能仍需要一些調整。

### 雲端開發 {#aem-as-a-cloud-service-developing-cloud-development}

若要在AEMas a Cloud Service上執行現有AEM應用程式，請執行下列步驟：

* 應用程式碼和設定必須儲存在相關Cloud Manager程式的Git程式碼存放庫中。
* 應用程式程式碼和設定必須與最新版本的基線AEM影像相容（可能每天都會變更）。
   * 必須使用與Cloud Manager環境相關聯的Cloud Manager管道來建立和部署客戶應用程式。
* 客戶應用程式必須傳遞管道中強制執行的所有程式碼品質、安全性和效能閘道。
* 為客戶應用程式建立的映像必須由Cloud Manager管道部署。

此程式通常稱為雲端優先開發。 由於端對端持續時間預計需要數分鐘（根據應用程式的複雜性，從20到50），因此在雲中嘗試掛起的代碼和配置更改之前，必須採用快速開發方法。

AEMas a Cloud Service環境的使用者不再可直接存取Web主控台，以管理OSGI套件組合及其相關設定，且先前是AEM QuickStart的一部分。 此介面仍可使用新的開發人員主控台，以唯讀模式存取。 透過此主控台，開發人員可以選取並直接登入製作或發佈服務的任何特定節點，然後存取預設封鎖的區域。

>[!NOTE]
>
>另請參閱 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration)

開發人員的另一個常見需求是快速存取各種環境的記錄檔。 透過AEMas a Cloud Service，製作和發佈節點中不同節點的記錄檔可透過Cloud Manager取得，格式為可下載的檔案或透過API取得。

由於程式碼和內容之間有明確的分隔，開發人員可以使用特定程式來更新內容，作為部署的一部分。 可變動內容的典型使用案例為：

* 標準 *預設* 屬於客戶專案的內容（例如資料夾、範本、工作流程等）

* 搜索索引定義

* ACL和權限

* 服務使用者和使用者群組

### 地方開發 {#aem-as-a-cloud-service-developing-local-development}

為了支援快速的迭代和開發，也可以在AEMas a Cloud Service環境之外開發AEM應用程式。 為此，開發人員可使用下列成品：

* AEMas a Cloud Service快速入門：a `.jar` 最新AEM程式碼基底的獨立安裝程式，具有相同的功能和API表面。

* AEMas a Cloud ServiceDispatcher SDK:在本機測試和驗證Dispatcher設定的影像程式

>[!NOTE]
>
>請注意，雲端快速入門不允許所有AEM Sites和AEM Assets功能。 它包含簡單的製作環境，可開發及測試大部分的擴充功能。

## 操作與效能 {#operations-and-performance}

>[!NOTE]
>
>有關詳細資訊，請從 [備份](/help/operations/backup.md)、索引 [和其](/help/operations/indexing.md)他維護任務開始 [](/help/operations/maintenance.md)。

透過AEMas a Cloud Service，這類操作會自動執行，因此不再需要任何服務中斷。

在以下方面：

* 許多任務已自動執行。

* 拓撲經過優化，可實現最大的可復原性和效率；例如，無二進位復寫是預設值。

* 重載任務（例如佇列、工作和大量處理任務）已移出核心AEM例項，以由共用和專用的微服務處理。

新的監控、報告和警報基礎架構也支援AEMas a Cloud Service的操作。 這可讓AdobeSRE（站點可靠性工程師）主動保持服務的健康。 該架構的各種元素都配備了各種健康檢查。 由於某些原因，如果架構的特定節點被視為不健康，則會從服務中移除，並靜默更換為健康的新節點。

## Identity Management {#identity-management}

>[!NOTE]
>
>如需詳細資訊，請參閱 [安全性 — IMS支援](/help/security/ims-support.md).

AEMas a Cloud Service的重大變更，是完整整合使用AdobeID來存取作者階層。

這需要使用 [AdobeAdmin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 使用者帳戶可讓您的使用者存取Adobe產品和服務，因為使用者設定檔資訊會集中在AdobeIdentity Management系統(IMS)中，以便在所有雲端服務間共用。 指派存取權至AEM後，即可在AEMas a Cloud Service中參考使用者帳戶（如前所述）;例如，用於從AEM Security使用者介面定義角色和權限。

這結合了以下優點：

* 使用AdobeIdentity Management系統(IMS)在所有Adobe雲端應用程式中提供單一登入。

* 使用者偏好設定保留在AEMas a Cloud Service的每個特定例項的本機。

## 製作使用者介面 {#authoring-user-interface}

>[!NOTE]
>
>欲知更多詳情， [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md) 是個好起點。

過去使用AEM的任何人，都會非常熟悉Sites和Assets的製作使用者介面(UI)的基本原則。

主要差異在於UI完全可觸控；傳統UI已無法使用。 否則，基本要素保持不變，只有微小的變化是顯而易見的。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service結合AEM內容管理系統與AEM數位資產管理的強大功能，讓您為客戶提供內容導向的個人化體驗。

如需詳細資訊，請參閱 [網站變更](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service為企業提供雲端原生的PaaS解決方案，不僅能以快速和有影響力的方式執行其數位資產管理和Dynamic Media操作，還能在始終最新、始終可用且始終學習的系統中使用新一代智慧功能，如AI/ML。

資產產品包括雲端的新一代資產處理，以及高效能的資產擷取和搜尋。

如需詳細資訊，請參閱 [資產as a Cloud Service概述與簡介](/help/assets/overview.md).

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

如需詳細資訊，請參閱：

* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
* [AEM Sites as a Cloud Service 重大變更](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
* [AEM Assets as a Cloud Service簡介](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)
