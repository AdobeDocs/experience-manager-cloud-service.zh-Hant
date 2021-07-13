---
title: 上線後階段
description: 上線後階段
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 60%

---

# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="疑難排解AEM"
>abstract="檢閱持續開發的最佳實務，並管理記錄，以及開發人員主控台和CRXDE Lite等工具，以協助疑難排解AEM的問題"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="存取和管理記錄檔"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service開發工具"


在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

下列工具可用來為 AEM as a Cloud Service 環境進行疑難排解：

* **開發人員控制台**
* **CRX/DE Lite**
* **管理記錄**


## 開發人員控制台 {#developer-console}

可以在開發、預備和生產環境的開發人員控制台中，針對 AEM as a Cloud Service 開發人員環境進行除錯。

請參考[實作 AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)，深入了解開發工具。

## CRX/DE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取 CRX/DE Lite，但無法在預備或生產環境中存取。

>[!IMPORTANT]
>在運行時寫入不可變的存放庫 (例如 `/libs` 和 `/apps`) 將發生錯誤。此外，身為客戶，您將無法存取預備和生產環境的開發人員工具。

請參考[使用 CRX/DE Lite 開發](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRX/DE Lite 開發您的 AEM 應用程式。

## 管理記錄 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

請參考[存取和管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html)，了解如何透過 UI 或 Cloud Manager 的 API 存取和管理記錄。

### 其他支援 {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="說明與支援"
>abstract="請洽詢AEM支援團隊，以取得說明或解決任何疑慮。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="支援Experience Cloud"

如果您對存取Cloud Service有任何疑問，請聯絡您的Adobe代表，或[Experience Cloud支援](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html)以取得詳細資訊。
