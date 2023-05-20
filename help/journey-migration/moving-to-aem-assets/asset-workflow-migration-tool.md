---
title: 資產工作流程移轉工具
description: 資產工作流程移轉工具
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# 資產工作流程移轉工具 {#asset-workflow-migration}

「資產工作流程移轉工具」可用來從 AEM 的內部部署或 AMS 部署，將資產處理工作流程自動移轉至處理設定檔和 OSGi 設定，以便用於 AEM Assets as a Cloud Service。

## 簡介 {#introduction}

本節將說明關於「資產工作流程移轉工具」之資源與實作的詳細資訊。

此公用程式可讓 AEM 開發人員將現有的 AEM 資產處理工作流程移轉至 AEM as a Cloud Service。

## 支援的工作流 {#migration-support-for-workflows}

工作流具有不同級別的遷移支援。 查看 [特定工作流清單](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根據提供的支援，工作流按以下類別分類。 Adobe支援遷移中列出的工作流 `SUPPORTED`。 `REQUIRED`或 `OPTIONAL` 的下界。 不支援其他類別中提到的工作流步驟。

* `SUPPORTED`:支援的功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `OPTIONAL`:中的可選功能 [!DNL Experience Manager Assets] as a Cloud Service。
* `REQUIRED`:添加到工作流中的必需步驟。
* `UNNECESSARY`:在 [!DNL Experience Manager Assets] as a Cloud Service。
* `NUI_OOTB`:功能 [asset compute服務](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`:預設提供的功能 [!DNL Dynamic Media] 連接器。
* `NUI_MIGRATED`:遷移到 [處理Asset compute服務配置檔案](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`:中當前不支援 [!DNL Experience Manager Assets] as a Cloud Service。

## 使用資產工作流遷移工具 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**:Adobe建議使用「資產工作流遷移」工具 `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] 作為 [!DNL Cloud Service] 代碼重構插件 [!DNL Adobe I/O] CLI)。 要瞭解如何安裝和使用插件，請參見 [Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)。

* **獨立實用程式**:資產工作流遷移工具也可以作為獨立實用程式執行。 要瞭解有關從源安裝和生成代碼的資訊，請參見 [Git資源： [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service]  — 工作流遷移](https://github.com/adobe/aem-cloud-migration)。
