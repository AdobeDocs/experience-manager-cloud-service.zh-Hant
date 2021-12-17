---
title: 資產工作流程移轉工具
description: 資產工作流程移轉工具
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# 資產工作流程移轉工具 {#asset-workflow-migration}

「資產工作流程移轉工具」可用來從 AEM 的內部部署或 AMS 部署，將資產處理工作流程自動移轉至處理設定檔和 OSGi 設定，以便用於 AEM Assets as a Cloud Service。

## 簡介 {#introduction}

本節將說明關於「資產工作流程移轉工具」之資源與實作的詳細資訊。

此公用程式可讓 AEM 開發人員將現有的 AEM 資產處理工作流程移轉至 AEM as a Cloud Service。

## 支援的工作流程 {#migration-support-for-workflows}

工作流程提供不同層級的移轉支援。 看這個 [特定工作流程清單](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). 工作流程會根據提供的支援分類為下列類別。 Adobe支援移轉中所列的工作流程 `SUPPORTED`, `REQUIRED`，或 `OPTIONAL` 類別。 不支援其他類別中提及的工作流程步驟。

* `SUPPORTED`:支援的功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `OPTIONAL`:中的選用功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `REQUIRED`:新增至工作流程的必要步驟。
* `UNNECESSARY`:在 [!DNL Experience Manager Assets] as a Cloud Service。
* `NUI_OOTB`:提供的功能 [asset compute服務](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`:預設提供的功能 [!DNL Dynamic Media] 連接器。
* `NUI_MIGRATED`:已移轉至 [處理Asset compute服務的設定檔](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`:目前不支援 [!DNL Experience Manager Assets] as a Cloud Service。

## 使用資產工作流程移轉工具 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**:Adobe建議您透過 `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] as a [!DNL Cloud Service] 程式碼重構外掛程式 [!DNL Adobe I/O] CLI)。 若要了解如何安裝和使用外掛程式，請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **獨立實用程式**:資產工作流程移轉工具也可以作為獨立公用程式執行。 若要了解如何從原始碼安裝和建立程式碼，請參閱 [Git資源： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]  — 工作流程移轉](https://github.com/adobe/aem-cloud-migration).
