---
title: AEM Cloud Service 中 AEM Sites 的重大變更
description: 了解如何使用 AEM Sites as a Cloud Service 進行編寫和管理，以及 AEM Cloud Service 中對 AEM Sites 的重要變更。
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 97%

---


# AEM Sites as a Cloud Service 重大變更 {#notable-changes}

AEM Sites as a Cloud Service 提供體驗管理功能，作為雲端原生 AEM as a Cloud Service 平台的一部分。除了 AEM as a Cloud Service 的核心優勢 (例如雲端原生擴充性、正常運行時間和始終保持最新狀態) 之外，AEM Sites as a Cloud Service 還提供了一些 Sites 特定的變更和新增功能。

>[!NOTE]
>本文件著重說明 AEM Sites 的顯著變更。有關 AEM as a Cloud Service 和其他模組的大致變更，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概觀 - 新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service 簡介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hant)

AEM Sites as a Cloud Service 中的變更與新增內容如下：

* [非同步頁面操作](#asynchronous-page-operations)
* [新的參考網站和教學課程](#new-reference-site-and-tutorial)

## 非同步頁面操作 {#asynchronous-page-operations}

在 AEM Cloud 服務中，傳統上已封鎖此 UI 的操作已分為在背景執行的較小任務。

* 行動頁面
* 推出頁面

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

您可以從[背景操作儀表板](/help/operations/asynchronous-jobs.md)檢視非同步作業的狀態。

>[!NOTE]
>
>系統使用者無需進行任何變更即可使用此新功能。這裡僅將其視為與先前內部部署的 AEM 版本相比的行為變更。

## 新的參考網站和教學課程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/) (新的 AEM 參考網站) 已更新並發布，以反映使用 AEM 以及 AEM 所提供全套功能、組件和部署模型來建立網站的最佳實務。新參考網站及[隨附的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)涵蓋基礎的主題，例如專案設定、核心元件、可編輯的範本、用戶資料庫以及使用 Adobe Experience Manager Sites 的元件開發。

先前，We.Retail 預設會隨 AEM 一起安裝 (在生產模式下啟動時除外)。在 AEM as a Cloud Service 中，依預設不會安裝參考網站。相反地，[&#x200B; git repo](https://github.com/adobe/aem-guides-wknd/) 和[隨附的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)提供了更新的 WKND 參考網站代碼。

## 執行階段時不適用的功能 {#capabilities-not-available-at-runtime}

AEM as a Cloud Service 隨時處於開啟狀態且隨時更新。若要達到此狀態，需要將 AEM 儲存庫中不可變內容和可變內容分開，並禁止在執行階段存取不可變內容。有關可變內容與不可變內容的更多詳細資訊，請參閱「[儲存庫的可變區域與不可變區域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)」。

在執行階段中無法存取不可變內容，因此，以下 AEM Sites 操作在執行階段不適用：

* i18n 翻譯字典
* AEM Sites 頁面編輯器中的開發人員模式

這些功能可以透過 AEM as a Cloud Service 的本機獨立開發人員執行個體使用，用來更新 AEM as a Cloud Service GIT 儲存庫中的內容和程式碼，但不能在託管執行階段執行個體中更新。
