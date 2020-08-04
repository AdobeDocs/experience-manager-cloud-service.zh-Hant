---
title: 資產工作流程移轉工具
description: '資產工作流程移轉工具 '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# 資產工作流程移轉工具 {#asset-workflow-migration}

「資產工作流程移轉工具」可用來從 AEM 的內部部署或 AMS 部署，將資產處理工作流程自動移轉至處理設定檔和 OSGi 設定，以便用於 AEM Assets 雲端服務。

## 簡介 {#introduction}

本節將說明關於「資產工作流程移轉工具」之資源與實作的詳細資訊。

此公用程式可讓 AEM 開發人員將現有的 AEM 資產處理工作流程移轉至 AEM 雲端服務。

## 支援的工作流程 {#migration-support-for-workflows}

工作流程支援的移轉層級不同。 請參閱此 [特定工作流程清單](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 根據所提供的支援，工作流程分為下列類別。 Adobe支援移轉列在、或類別中 `SUPPORTED`的 `REQUIRED`工作 `OPTIONAL` 流程。 不支援其他類別中提及的工作流程步驟。

* `SUPPORTED`: 雲端服務 [!DNL Experience Manager Assets] 支援的功能。
* `OPTIONAL`: 雲端服務 [!DNL Experience Manager Assets] 中的可選功能。
* `REQUIRED`: 新增至工作流程的必要步驟。
* `UNNECESSARY`: 雲端服務中不 [!DNL Experience Manager Assets] 需要功能。
* `NUI_OOTB`: 資產計算服 [務提供的功能](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`: 預設連接器提供 [!DNL Dynamic Media] 的功能。
* `NUI_MIGRATED`: 移轉至資 [產計算服務的處理配置檔案](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`: 目前不支援 [!DNL Experience Manager Assets] 雲端服務。

## 安裝資產工作流程移轉工具 {#installing-tool}

請參考 **[Git 資源：AEM Assets 雲端服務 - 工作流程移轉](https://github.com/adobe/aem-cloud-migration)**，了解如何使用原始碼安裝和建置程式碼。
