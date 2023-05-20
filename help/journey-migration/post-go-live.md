---
title: 上線後
description: 瞭解如何監控問題並提高效能
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 39%

---

# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM 的移難排解"
>abstract="檢閱持續開發和管理記錄檔的最佳做法以及開發人員主控台和 CRXDE Lite 之類的工具，以協助對 AEM 的問題進行移難排解"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="存取和管理記錄檔"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service 開發工具"

這是遷移的最後一部分，因此您將學習如何在遷移完成後監控問題並提高效能。 您應確保清理臨時檔案，審查持續開發的最佳做法並管理日誌。

## 到目前為止 {#story-so-far}

在上一步中，您學習了如何執行遷移和 [上線](/help/journey-migration/go-live.md) 一旦代碼和內容準備好移到AEMas a Cloud Service。

## 目標 {#objective}

本文檔介紹了用於診斷as a Cloud Service環境的AEM工具：

* **開發人員控制台**
* **CRXDE Lite**
* **管理記錄**

## 開發人員控制台 {#developer-console}

在開發AEM人員控制台中，可以調試as a Cloud Service的開發人員環境，用於開發、階段和生產環境。

請參考[實作 AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，深入了解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取 CRXDE Lite，但不能在預備或生產環境中存取。

>[!IMPORTANT]
>寫入不可變的儲存庫，如 `/libs` 和 `/apps` 運行時會導致錯誤。 此外，您無權訪問用於暫存和生產環境的開發人員工具。

請參考[使用 CRXDE Lite 開發](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRXDE Lite 開發您的 AEM 應用程式。

## 管理記錄 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

請參考[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md)，了解如何透過 UI 或 Cloud Manager 的 API 存取和管理記錄。

## 聯繫支援 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="說明與支援"
>abstract="如需澄清或解決任何疑慮，請和我們的 AEM 支援團隊聯絡。"
>additional-url="https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud 的支援"

如果您對訪問Cloud Service有疑問，請與Adobe代表聯繫或 [支援Experience Cloud](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html) 的子菜單。

## 文檔學習 {#document-learnings}

遷移完成後，您應記錄在此過程中獲得的知識。 一些可能有助於文檔處理的問題包括：

* 什麼管用，什麼管用？
* 主要的痛點是什麼？
* Recommendations，以防未來移民。

然後，您應與組織內的利益相關方和團隊共用這些遷移後學習。

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已完成AEMas a Cloud Service遷移之旅！ 您應該瞭解如何：

* 開始轉到AEMas a Cloud Service
* 確定您的部署是否已準備好移動到AEMas a Cloud Service
* 使您的代碼和內容雲準備就緒
* 執行遷移
* 監控問題並提高效能
