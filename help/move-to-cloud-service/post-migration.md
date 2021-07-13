---
title: 移轉後階段
description: 移轉後階段
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 93%

---


# 移轉後 {#post-migration}

在「移轉後」階段中，請務必清理暫存檔，並回顧最佳作法以便持續開發及留下管理記錄。

下列工具可用來為 AEM as a Cloud Service 環境進行疑難排解：

* **開發人員控制台**
* **CRXDE Lite**
* **管理記錄**

## 開發人員控制台 {#developer-console}

可以在開發、預備和生產環境的開發人員控制台中，針對 AEM as a Cloud Service 開發人員環境進行除錯。

請參考[實作 AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)，深入了解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取 **CRXDE Lite**，但不能在預備或生產環境中存取。

>[!IMPORTANT]
>在運行時寫入不可變的存放庫 (例如 `/libs` 和 `/apps`) 將發生錯誤。此外，身為客戶，您將無法存取預備和生產環境的開發人員工具。

請參考[使用 CRXDE Lite 開發](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRXDE Lite 開發您的 AEM 應用程式。

## 管理記錄 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

請參考[存取和管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html)，了解如何透過 UI 或 Cloud Manager 的 API 存取和管理記錄。

### 其他支援 {#additional-support}

如有關於存取雲端服務的疑問，請洽詢您的 Adobe 代表或 Adobe AEM CQ 支援入口網站。
