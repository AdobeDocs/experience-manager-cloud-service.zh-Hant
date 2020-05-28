---
title: 遷移後階段
description: 遷移後階段
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---


# 移轉後 {#post-migration}

在遷移後階段，您應確保清理臨時檔案、審查持續開發的最佳做法並管理日誌。

下列工具可用於疑難排解AEM的雲端服務環境：

* **Developer Console**
* **CRXDE Lite**
* **管理記錄檔**


## Developer Console {#developer-console}

AEM的雲端服務開發人員環境除錯功能可從Developer Console取得，以用於開發、階段和生產環境。

請參閱「 [以雲端服務形式實施AEM](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) 」以進一步瞭解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環 **境中存取CRXDE Lite** ，但不能在舞台或生產環境中存取。

>[重要]
>寫入不可變的儲存庫(例 `/libs` 如和 `/apps` 在執行時期)將會導致錯誤。 此外，身為客戶，您將無法存取測試和生產環境的開發人員工具。

請參閱「 [使用CRXDE Lite開發」](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) ，以瞭解如何使用CRXDE Lite開發AEM應用程式。

## 管理記錄檔 {#managing-logs}

用戶可以訪問選定環境的可用日誌檔案清單。

請參閱存 [取和管理記錄](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) ，瞭解如何透過UI或透過Cloud Manager從API存取和管理記錄檔。

### 其他支援 {#additional-support}

如果您對Cloud Service的存取有任何疑問，請連絡您的Adobe代表或Adobe AEM CQ支援入口網站。
