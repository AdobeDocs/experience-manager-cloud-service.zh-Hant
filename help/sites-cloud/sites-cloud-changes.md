---
title: AEM 雲端服務中 AEM Sites 的重大變更
description: AEM 雲端服務中 AEM Sites 的重大變更
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 17%

---

# AEM Sites as a Cloud Service 的重大變更 {#notable-changes}

AEM Sites as aCloud Service是雲端原生AEM as aCloud Service平台的一部分，提供體驗管理功能。 除了AEM as aCloud Service的核心優點（例如雲端原生擴充性、正常運作時間以及隨時保持最新）外，AEM Sites as aCloud Service還提供多項Sites專屬的變更和新增功能。

>[!NOTE]
>本檔案重點說明AEM Sites的重大變更。 如需AEM as aCloud Service和其他模組的一般變更，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概覽 - 新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as aCloud Service簡介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


AEM Sites as aCloud Service的變更和新增如下：

* [非同步頁面操作](#asynchronous-page-operations)
* [新參考網站和教學課程](#new-reference-site-and-tutorial)

## 非同步頁面操作 {#asynchronous-page-operations}

在AEM雲端服務中，傳統上封鎖UI的作業已細分為在背景執行的較小作業。

* 移動頁面
* 轉出頁面

此類動作的發起者可在位於`/mnt/overlay/dam/gui/content/asyncjobs.html`的新UI中檢查其狀態。

>[!NOTE]
>
>系統的用戶無需更改即可使用此新功能。 此處僅指出為與舊版內部部署的AEM相較之下的行為變更。

## 新參考網站和教學課程 {#new-reference-site-and-tutorial}

[新的AEM參考網站WKND ](https://wknd.site/)已更新並發佈，以反映使用AEM建立網站的最佳實務，以及AEM中提供的完整功能、元件和部署模型集。新的參考網站和[隨附的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)涵蓋基本主題，例如專案設定、核心元件、可編輯範本、用戶端程式庫，以及使用Adobe Experience Manager Sites開發元件。

之前，We.Retail預設會與AEM一起安裝（生產模式中啟動時除外）。  現在，以後預設不會安裝參考網站。  而是提供附有更新WKND參考網站代碼的[git repo](https://github.com/adobe/aem-guides-wknd/)和[教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)。

## 運行時無法使用的功能 {#capabilities-not-available-at-runtime}

AEM as aCloud Service一律開啟且隨時保持最新。 要達到此目的，必須將AEM儲存庫分離在不可變和可變內容中，並禁止在運行時訪問不可變內容。 有關可變內容與不可變內容的詳細資訊，請參閱[儲存庫的可變內容與不可變區域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由於不可修改的內容在運行時無法訪問，因此以下AEM Sites操作在運行時不可用：

* i18n字典翻譯
* AEM Sites頁面編輯器中的開發人員模式

這些功能可透過本機的獨立開發人員例項，將AEM作為Cloud Service使用，以更新AEM作為Cloud ServiceGIT存放庫的內容和程式碼，但不適用於托管的執行階段例項。
