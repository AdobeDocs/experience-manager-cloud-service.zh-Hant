---
title: 上線後
description: 了解如何監控問題並改善效能
source-git-commit: c9143d77e70476beb7f7dd162c36aeda8d1be506
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 20%

---


# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="疑難排解AEM"
>abstract="檢閱持續開發的最佳實務，並管理記錄，以及開發人員主控台和CRXDE Lite等工具，以協助疑難排解AEM的問題"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="存取和管理記錄檔"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEMas a Cloud Service開發工具"

這是歷程的最後一個部分，讓您了解如何在移轉完成後監控問題並改善效能。 您應確保清理臨時檔案、審查最佳作法以持續開發及管理記錄。

## 迄今為止的故事 {#story-so-far}

在歷程的上一步中，您學習了如何執行移轉， [上線](/help/journey-migration/go-live.md) 當程式碼和內容準備好移至AEMas a Cloud Service時。

## 目標 {#objective}

本檔案說明可用於疑難排解AEMas a Cloud Service環境的工具：

* **開發人員控制台**
* **CRXDE Lite**
* **管理記錄**

## 開發人員控制台 {#developer-console}

開發、預備和生產環境的開發人員控制台中提供對AEMas a Cloud Service開發人員環境進行偵錯的功能。

請參考[實作 AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，深入了解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取 CRXDE Lite，但不能在預備或生產環境中存取。

>[!IMPORTANT]
>寫入不可變的儲存庫，例如 `/libs` 和 `/apps` 在執行階段會導致錯誤。 此外，您無法存取預備和生產環境的開發人員工具。

請參考[使用 CRXDE Lite 開發](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRXDE Lite 開發您的 AEM 應用程式。

## 管理記錄 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

請參考[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md)，了解如何透過 UI 或 Cloud Manager 的 API 存取和管理記錄。

## 聯絡支援 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="說明與支援"
>abstract="請洽詢AEM支援團隊，以取得說明或解決任何疑慮。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="支援Experience Cloud"

如果您對存取Cloud Service有任何疑問，請連絡您的Adobe代表，或 [支援Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 以取得更多詳細資訊。

## 檔案學習 {#document-learnings}

完成移轉後，您應記錄此程式中獲得的知識。 可能有助於說明檔案程式的問題包括：

* 什麼管用，什麼管用不？
* 主要的痛點是什麼？
* Recommendations，以備日後移轉時使用。

接著，您應該與組織內的利害關係人和團隊分享這些移轉後的學習經驗。

## 歷程結束了，還是結束了？ {#journey-ends}

恭喜！ 您已完成AEMas a Cloud Service移轉歷程！ 您應了解如何：

* 開始移至AEMas a Cloud Service
* 判斷您的部署是否已準備好移至AEMas a Cloud Service
* 讓您的程式碼和內容雲端準備就緒
* 執行移轉
* 監控問題並改善效能
