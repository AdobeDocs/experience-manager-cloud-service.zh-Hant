---
title: 上線後
description: 瞭解如何監控問題並改善效能。
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 22%

---

# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM 的移難排解"
>abstract="查看記錄持續開發和管理的最佳實務。了解 Developer Console 和 CRXDE Lite 等工具，以協助解決 AEM 的相關問題。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs" text="存取和管理記錄檔"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service 開發工具"

此歷程是最後一部分，協助您瞭解如何監視問題，並在移轉完成後改善效能。 確保清理暫存檔，檢閱持續開發的最佳實務，以及管理記錄。

## 目前進度 {#story-so-far}

在歷程的上一步中，您已瞭解如何在程式碼和內容準備好移轉到AEM as a Cloud Service時執行移轉和[上線](/help/journey-migration/go-live.md)。

## 目標 {#objective}

本檔案說明可用於疑難排解AEM as a Cloud Service環境的工具：

* **開發人員控制台**
* **CRXDE Lite**
* **管理記錄**

## Developer Console {#developer-console}

Developer Console中有提供開發、預備和生產環境的除錯AEM as a Cloud Service開發人員環境。

請參閱[實作AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)以進一步瞭解開發工具。

## CRXDE Lite {#crxde-lite}

身為使用者，您可以在開發環境中存取CRXDE Lite ，但無法在預備或生產環境中存取。

>[!IMPORTANT]
>在執行階段寫入不可變的存放庫（例如`/libs`和`/apps`）會產生錯誤。 此外，您也無法存取預備和生產環境的開發人員工具。

請參閱[使用CRXDE Lite開發](/help/implementing/developing/tools/crxde.md)，以取得有關如何使用CRXDE Lite開發AEM應用程式的詳細資訊。

## 管理記錄檔 {#managing-logs}

使用者可以存取所選環境的可用記錄檔清單。

請參閱[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md)，瞭解如何透過使用者介面或透過Cloud Manager從API存取和管理記錄。

## 連絡支援人員 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="說明與支援"
>abstract="如需澄清或解決任何疑慮，請和 Adobe 的 AEM 支援團隊聯絡。"
>additional-url="https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud 的支援"

如果您對Cloud Service的存取權有任何疑問，請聯絡您的Adobe代表或[Experience Cloud支援](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)以取得詳細資訊。

## 檔案學習 {#document-learnings}

移轉一旦完成，即記錄在此過程中取得的知識。 可能有助於說明檔案流程的一些問題包括：

* 哪些專案運作良好，哪些專案沒有運作？
* 主要煩惱為何？
* 建議（如果未來有移轉）。

與組織中的利害關係人和團隊分享這些移轉後學習。

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已完成AEM as a Cloud Service移轉歷程！ 您應該瞭解如何：

* 開始使用AEM as a Cloud Service
* 判斷您的部署是否已準備好移至AEM as a Cloud Service
* 讓您的程式碼和內容雲端就緒
* 執行移轉
* 監控問題並改善效能
