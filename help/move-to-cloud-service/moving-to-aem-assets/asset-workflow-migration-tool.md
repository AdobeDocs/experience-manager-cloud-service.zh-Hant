---
title: 資產工作流程移轉工具
description: 資產工作流程移轉工具
exl-id: 18490295-ead6-4691-8983-a6d4054e4264
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---

# 資產工作流程移轉工具 {#asset-workflow-migration}

「資產工作流程移轉工具」可用來從 AEM 的內部部署或 AMS 部署，將資產處理工作流程自動移轉至處理設定檔和 OSGi 設定，以便用於 AEM Assets as a Cloud Service。

## 簡介 {#introduction}

本節將說明關於「資產工作流程移轉工具」之資源與實作的詳細資訊。

此公用程式可讓 AEM 開發人員將現有的 AEM 資產處理工作流程移轉至 AEM as a Cloud Service。

## 支援的工作流{#migration-support-for-workflows}

工作流程提供不同層級的移轉支援。 請參閱此[特定工作流程清單](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 工作流程會根據提供的支援分類為下列類別。 Adobe支援移轉`SUPPORTED`、`REQUIRED`或`OPTIONAL`類別中列出的工作流程。 不支援其他類別中提及的工作流程步驟。

* `SUPPORTED`:支援的 [!DNL Experience Manager Assets] Cloud Service功能。
* `OPTIONAL`:作為Cloud Service [!DNL Experience Manager Assets] 的選用功能。
* `REQUIRED`:新增至工作流程的必要步驟。
* `UNNECESSARY`:在中不需要功 [!DNL Experience Manager Assets] 能作為Cloud Service。
* `NUI_OOTB`:由Asset compute服 [務提供的功能](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`:預設連接器提供 [!DNL Dynamic Media] 的功能。
* `NUI_MIGRATED`:移轉至 [Asset compute服務的處理設定檔](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`:中目前不支 [!DNL Experience Manager Assets] 援作為Cloud Service。

## 安裝資產工作流程移轉工具 {#installing-tool}

請參考 **[Git 資源：AEM Assets as a Cloud Service - 工作流程移轉](https://github.com/adobe/aem-cloud-migration)**，了解如何使用原始碼安裝和建置程式碼。
