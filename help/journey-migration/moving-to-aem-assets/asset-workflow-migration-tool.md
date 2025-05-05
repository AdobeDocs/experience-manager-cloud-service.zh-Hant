---
title: 資產工作流程移轉工具
description: 資產工作流程移轉工具
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 30%

---

# 資產工作流程移轉工具 {#asset-workflow-migration}

「資產工作流程移轉工具」可用來從 AEM 的內部部署或 AMS 部署，將資產處理工作流程自動移轉至處理設定檔和 OSGi 設定，以便用於 AEM Assets as a Cloud Service。

## 簡介 {#introduction}

本節將說明關於「資產工作流程移轉工具」之資源與實作的詳細資訊。

此公用程式可讓 AEM 開發人員將現有的 AEM 資產處理工作流程移轉至 AEM as a Cloud Service。

## 支援的工作流程 {#migration-support-for-workflows}

工作流程支援不同層級的移轉。 檢視此[特定工作流程清單](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根據提供的支援，工作流程會分為以下類別。 Adobe支援移轉`SUPPORTED`、`REQUIRED`或`OPTIONAL`類別中列出的工作流程。 不支援其他類別中提及的工作流程步驟。

* `SUPPORTED`： [!DNL Experience Manager Assets]as a Cloud Service支援的功能。
* `OPTIONAL`： [!DNL Experience Manager Assets]as a Cloud Service中的選用功能。
* `REQUIRED`：新增至工作流程的必要步驟。
* `UNNECESSARY`： [!DNL Experience Manager Assets]as a Cloud Service中不需要功能。
* `NUI_OOTB`： [Asset compute服務](/help/assets/asset-microservices-configure-and-use.md)所提供的功能。
* `DMS7_OOTB`：預設[!DNL Dynamic Media]聯結器所提供的功能。
* `NUI_MIGRATED`：已移轉至Asset compute服務[&#128279;](/help/assets/asset-microservices-configure-and-use.md)的處理設定檔。
* `UNSUPPORTED`： [!DNL Experience Manager Assets]as a Cloud Service目前不支援。

## 使用資產工作流程移轉工具 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**： Adobe建議透過`aio-cli-plugin-aem-cloud-service-migration`使用資產工作流程移轉工具（[!DNL Experience Manager]當作[!DNL Adobe I/O] CLI的[!DNL Cloud Service]程式碼重構外掛程式）。 若要瞭解如何安裝和使用外掛程式，請參閱[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)。

* **獨立公用程式**：資產工作流程移轉工具也可以作為獨立公用程式執行。 若要瞭解如何從原始程式碼安裝和建置程式碼，請參閱[Git資源： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]  — 工作流程移轉](https://github.com/adobe/aem-cloud-migration)。
