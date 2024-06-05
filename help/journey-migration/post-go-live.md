---
title: 上線後
description: 瞭解如何監控問題並改善效能
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 22%

---

# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM 的移難排解"
>abstract="檢閱持續開發和管理記錄檔的最佳做法以及開發人員主控台和 CRXDE Lite 之類的工具，以協助對 AEM 的問題進行移難排解"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=zh-Hant" text="存取和管理記錄檔"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=zh-Hant#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service 開發工具"

此歷程是最後一部分，因此您將瞭解如何監視問題，並在移轉完成後改善效能。 您應該確保清理暫存檔，並檢閱持續開發的最佳實務和管理記錄。

## 目前進度 {#story-so-far}

在此歷程的上一步中，您已瞭解如何執行移轉並 [上線](/help/journey-migration/go-live.md) 在程式碼和內容準備好移至AEMas a Cloud Service後。

## 目標 {#objective}

本檔案說明可用於疑難排解AEMas a Cloud Service環境的工具：

* **開發人員控制台**
* **CRXDE Lite**
* **管理記錄**

## 開發人員主控台 {#developer-console}

在開發、預備和生產環境的開發人員控制檯中，提供對AEMas a Cloud Service開發人員環境進行偵錯的功能。

另請參閱 [AEMas a Cloud Service實作](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) 以進一步瞭解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取CRXDE Lite，但不能在預備或生產環境中存取。

>[!IMPORTANT]
>寫入不可變的存放庫，例如 `/libs` 和 `/apps` 在執行階段導致錯誤。 此外，您也無法存取預備和生產環境的開發人員工具。

另請參閱 [使用CRXDE Lite開發](/help/implementing/developing/tools/crxde.md) 有關如何使用CRXDE Lite開發您的AEM應用程式的詳細資訊。

## 管理記錄檔 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

另請參閱 [存取和管理記錄檔](/help/implementing/cloud-manager/manage-logs.md) 瞭解如何透過使用者介面或透過Cloud Manager從API存取和管理記錄。

## 連絡支援人員 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="說明與支援"
>abstract="如需澄清或解決任何疑慮，請和 Adobe 的 AEM 支援團隊聯絡。"
>additional-url="https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud 的支援"

如果您對存取Cloud Service有任何疑問，請聯絡您的Adobe代表或 [支援Experience Cloud](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html) 以取得更多詳細資料。

## 檔案學習 {#document-learnings}

移轉一旦完成，即記錄在此過程中取得的知識。 可能有助於說明檔案流程的一些問題包括：

* 哪些專案運作良好，哪些專案沒有運作？
* 主要煩惱為何？
* 如果未來有移轉專案，則使用Recommendations。

與組織中的利害關係人和團隊分享這些移轉後學習。

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已完成AEMas a Cloud Service移轉歷程！ 您應該瞭解如何：

* 開始使用AEMas a Cloud Service
* 判斷您的部署是否已準備好移至AEMas a Cloud Service
* 讓您的程式碼和內容雲端就緒
* 執行移轉
* 監控問題並改善效能
