---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service體系結構
description: 瞭解 [!DNL AEM Forms] as a Cloud Service瞭解平台的可擴充性、恢復性和效能方面。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 4%

---


# [!DNL AEM] as a Cloud Service架構 {#architecture}

[!DNL AEM Forms] as a Cloud Service標準化了所有客戶的部署體系結構，目標是讓客戶完全免受體系結構考慮因素的影響。 例如，儘管新的AEMas a Cloud Service體系結構仍然依賴於微內核的概念來永續，但客戶不需要擔心從哪個微內核中挑選出來。 作者和發佈端使用的微內核是 [!DNL AEM Cloud Service] 否則，客戶將無法進行內部安裝。

AEMas a Cloud Service具有可變實例數的動態體AEM系結構。 它提供了開發、階段、生產和演示環境。 它提供了管理實AEM例（雲管理器）、維護用戶和身份驗證(Admin Console和IMS(Adobe身份管理)系統)、配置快取(Abmisty CDN)和雲本地開發環境的工具。 有關體系結構的詳細資訊，請參見 [淺談建築 [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en)。

## Cloud Manager{#cloud-manager}

雲管理器是 [AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en)。 每個新租戶 [!DNL AEM Forms] as a Cloud Service首先設定為Cloud Manager訪問。 Cloud Manager是我們客戶的運營和開發人員角色的單一入口點。 它是管理程式和AEM環境的場所。 Cloud Manager已演變為自助服務門戶，在該門戶中可以建立AEM和配置as a Cloud Service的主要元件：

* 建立和管理程式
* 建立和管理AEM程式內的環境
* 建立和管理管道，以將客戶代碼和配置部署到特定環境
* 獲取有關這些元件的重要生命週期事件（如產品更新）的通知有關Cloud Manager的詳細資訊，請參閱 [瞭解Adobe雲管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) 和 [雲管理器簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)。

## 用戶和身份驗證 {#users-and-authentication}

AEMas a Cloud Service包括對實例的Admin ConsoleAEM支援和基於AdobeIdentity Management系統(IMS)的驗證。 Admin Console 可讓管理員集中管理所有 Experience Cloud 使用者。管理員可將使用者和群組指派給與 AEM as a Cloud Service 例項相關聯的產品設定檔，讓他們能登入該例項。有關用戶、身份驗證和訪問as a Cloud Service實例的詳細信AEM息，請參見 [支助 [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction)。

各種人物都參與 [!DNL AEM Forms] 項目。 登錄後 [!DNL AEM Forms] as a Cloud Service實例， [在管理控制台中添加用戶](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) 適用於您的組織或項目和 [將用戶分配給內置組](forms-groups-privileges-tasks.md) 提供所需權限。

學習各種內置 [!DNL AEM Forms] 可用的特定用戶組和權限 [!DNL AEM Forms] 作為Cloud Services實例，請參閱 [配置、用戶、角色和組](forms-groups-privileges-tasks.md)。

## 開發人員體驗 {#developer-experience}

支援as a Cloud Service的新體AEM系結構給整個開發人員體驗帶來了一些關鍵變化。 對開發人員體驗進行更改的主要目標之一是盡可能快AEM地遷移到as a Cloud Service，而對現有自定義代碼的修改很少。

## 雲開發 {#cloud-development}

以下是在as a Cloud Service環境中平穩運行現有代碼的AEM准則：

* 將代碼和配置儲存到關聯的Cloud Manager程式的Git儲存庫。 它使代碼與CI/CD的管理和整合變得簡單易行。
* 使應用程式碼和配置與基線相容 [!DNL AEM Forms] 影像。 使用最新的API有助於構建更快且安全的應用程式。
* 使用與Cloud Manager環境關聯的Cloud Manager管道構建和部署應用程式。 它可幫助您為 [!DNL AEM Forms] as a Cloud Service於您的環境。
* 嘗試您的自定義應用程式通過管道中強制實施的所有代碼質量、安全性和效能門。 它有助於構建安全且效能更好的應用程式，從而獲得更好的客戶體驗。 您始終可以使用Cloud Manager UI跳過某些檢查。
此過程通常稱為雲優先開發。 [!DNL AEM Forms] as a Cloud Service還提供SDK，在雲中嘗試掛起的代碼和配置更改之前支援快速開發。
以前屬於QuickStart的某AEM些介面不再可供as a Cloud Service環境的AEM用戶使用。 例如，管理OSGI捆綁包及其相關配置的Web控制台。 CRXDE Lite內容儲存庫瀏覽器僅可在非生產環境類型上訪問。 開發人員需要的Web控制台功能的子集，特別是當涉及診斷和狀態目的時，可通過新的開發人員控制台提供。
此外，開發人員最常見的要求之一是快速訪問各種環境的日誌檔案。 與 [!DNL AEM Cloud Service]，「作者」中不同節點的日誌檔案可通過雲管理器（可下載的檔案或通過API跟蹤日誌）提供。 由於代碼和內容的明確分離，開發人員可以利用特定的過程來更新內容，作為部署的一部分。 可變內容的典型使用案例有：
* 作為客戶項目一部分的標準「預設」內容（例如資料夾、模板、工作流……）
* 搜索索引定義
* ACL和權限
* 服務用戶和用戶組設定開發環境， [配置CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)，並學習 [部署代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 環境。

## 地方發展 {#local-development}

設定和配置 [!DNL AEM Forms] as a Cloud Service環境，您可以設定開發、試運行和生產環境。 此外，還設定和配置本地開發環境，以便快速重複和開發。 您可以下載並設定AEMSDK和 [!DNL AEM Forms] 附加功能存檔以設定本地 [!DNL Forms] as a Cloud Service發展環境。  有關詳細說明，請參見 [設定本地開發環境](setup-local-development-environment.md)。

## 調試 {#debugging}

AEMas a Cloud Service運行在自助服務、可擴展的雲基礎架構上。 它要求開AEM發人員瞭解和調試as a Cloud Service的各個方面，AEM從構建和部署到獲取運行應用程式的詳細AEM資訊。 有關詳細資訊，請參見 [調試AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en)。
