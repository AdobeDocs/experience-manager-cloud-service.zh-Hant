---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service架構
description: 了解 [!DNL AEM Forms] as a Cloud Service了解平台的可擴充性、可復原性和效能方面。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 4%

---


# [!DNL AEM] as a Cloud Service架構 {#architecture}

[!DNL AEM Forms] as a Cloud Service使所有客戶的部署體系結構標準化，目標是讓客戶完全無需考慮體系結構。 例如，雖然新的AEMas a Cloud Service架構仍依賴微內核的概念來保持持續性，但客戶無需擔心要挑選哪個微內核。 製作端和發佈端所使用的微核均為 [!DNL AEM Cloud Service] 而不適用於內部部署安裝的客戶。

AEM as a Cloud Service具有可變AEM例項數的動態架構。 它提供開發、預備、生產和示範環境。 它提供工具來管理AEM例項(Cloud Manager)、維護使用者和驗證(Admin Console和IMS(Adobe身分管理)系統)、設定快取(Abmetly CDN)和雲端原生開發環境。 有關架構的詳細資訊，請參閱 [A.B.C. [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

Cloud Manager是 [AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). 的每個新租用戶 [!DNL AEM Forms] as a Cloud Service是先布建以供Cloud Manager存取。 Cloud Manager是客戶營運和開發人員角色的單一入口點。 這是可管理AEM程式和環境的位置。 Cloud Manager已發展為自助入口網站，可在此建立及設定AEMas a Cloud Service的主要元件：

* 建立和管理方案
* 在方案中建立和管理AEM環境
* 建立和管理管道，以便將客戶代碼和配置部署到特定環境
* 收到這些元件重要生命週期事件的通知（例如產品更新）如需Cloud Manager的詳細資訊，請參閱 [了解AdobeCloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) 和 [Cloud Manager簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant).

## 使用者與驗證 {#users-and-authentication}

AEMas a Cloud Service包含對AEM例項和AdobeIdentity Management系統(IMS)型驗證的Admin Console支援。 Admin Console 可讓管理員集中管理所有 Experience Cloud 使用者。管理員可將使用者和群組指派給與 AEM as a Cloud Service 例項相關聯的產品設定檔，讓他們能登入該例項。如需使用者、驗證和，以及存取AEMas a Cloud Service例項的詳細資訊，請參閱 [的IMS支援 [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

典型 [!DNL AEM Forms] 專案。 登入後 [!DNL AEM Forms] as a Cloud Service例項，您可以 [在admin console中新增使用者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) 適用於您的組織或項目的角色， [將使用者指派至內建群組](forms-groups-privileges-tasks.md) 提供所需的權限。

學習各種內建功能 [!DNL AEM Forms] 可用的特定用戶組和權限 [!DNL AEM Forms] 作為Cloud Services例項，請參閱 [配置、用戶、角色和組](forms-groups-privileges-tasks.md).

## 開發人員體驗 {#developer-experience}

支援AEM as a Cloud Service的新架構對整體開發人員體驗帶來一些重要改變。 開發人員體驗變更的主要目標之一，是允許盡快移轉至AEMas a Cloud Service，而對現有自訂程式碼幾乎不做任何修改。

## 雲端開發 {#cloud-development}

以下是在AEMas a Cloud Service環境中順利執行現有程式碼的准則：

* 將您的程式碼和設定儲存至相關Cloud Manager程式的Git存放庫。 讓管理程式碼與CI/CD輕鬆整合。
* 使應用程式代碼和配置與基線相容 [!DNL AEM Forms] 影像。 使用最新的API有助於建立更快速、安全的應用程式。
* 使用與Cloud Manager環境相關聯的Cloud Manager管道來建置和部署應用程式。 可協助您為 [!DNL AEM Forms] as a Cloud Service於您的環境。
* 請嘗試讓您的自訂應用程式傳遞管道中強制執行的所有程式碼品質、安全性和效能閘道。 它有助於構建安全且效能更好的應用程式，從而獲得更好的客戶體驗。 您一律可以使用Cloud Manager UI略過部分檢查。
此程式通常稱為雲端優先開發。 [!DNL AEM Forms] as a Cloud Service功能也提供SDK，以支援在雲端中嘗試擱置的程式碼和設定變更前快速開發。
AEMas a Cloud Service環境的使用者不再能使用先前屬於AEM QuickStart的某些介面。 例如，管理OSGI套件組合及其相關設定的Web主控台。 CRXDE Lite內容存放庫瀏覽器只能在非生產環境類型上存取。 開發人員需要的Web控制台功能子集，尤其是當涉及診斷和狀態用途時，可透過新的開發人員控制台提供。
此外，開發人員最常需要的一項要求是快速存取各種環境的記錄檔。 使用 [!DNL AEM Cloud Service]，則「製作發佈」中不同節點的記錄檔可透過Cloud Manager取得，其格式為可下載的檔案，或透過API追蹤記錄檔。 由於程式碼和內容之間有明確的分離，開發人員可運用特定程式來更新部署中的內容。 可變動內容的典型使用案例為：
* 屬於客戶專案的標準「預設」內容（例如資料夾、範本、工作流程……）
* 搜索索引定義
* ACL和權限
* 服務使用者和使用者群組設定您的開發環境、 [設定CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)，並學習 [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 在環境中。

## 地方開發 {#local-development}

當您設定並設定 [!DNL AEM Forms] as a Cloud Service環境，您可以設定開發、測試和生產環境。 此外，還可設定並設定本機開發環境，以快速反覆執行和開發。 您可以下載並設定AEM SDK，以及 [!DNL AEM Forms] 附加功能封存以設定本機 [!DNL Forms] as a Cloud Service開發環境。  如需詳細指示，請參閱 [設定本機開發環境](setup-local-development-environment.md).

## 除錯 {#debugging}

AEMas a Cloud Service在自助式、可擴充的雲端基礎架構上執行。 它需要AEM開發人員了解AEMas a Cloud Service的各個層面並除錯，從建立和部署，到取得執行AEM應用程式的詳細資訊。 如需詳細資訊，請參閱 [除錯AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
