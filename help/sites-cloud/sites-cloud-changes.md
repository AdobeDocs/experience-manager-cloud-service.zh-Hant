---
title: AEM Cloud Service 中 AEM Sites 的重大變更
description: AEM Cloud Service 中 AEM Sites 的重大變更
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: 7becee73a64fbfd2b4f89c307f63868461b0e853
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 20%

---


# AEM Sites as a Cloud Service 的重大變更 {#notable-changes}

AEM Sitesas a Cloud Service是雲端原生AEMas a Cloud Service平台的一部分，提供體驗管理功能。 除了AEMas a Cloud Service的核心優點（例如雲端原生擴充性、正常運作時間以及隨時保持最新）外，AEM Sitesas a Cloud Service還提供多項Sites專屬的變更和新增功能。

>[!NOTE]
>本檔案重點說明AEM Sites的重大變更。 如需AEMas a Cloud Service和其他模組的一般變更，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概覽 - 新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service簡介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


AEM Sitesas a Cloud Service的變更及新增如下：

* [非同步頁面操作](#asynchronous-page-operations)
* [新參考網站和教學課程](#new-reference-site-and-tutorial)

## 非同步頁面操作 {#asynchronous-page-operations}

在AEM雲端服務中，傳統上封鎖UI的作業已細分為在背景執行的較小作業。

* 移動頁面
* 轉出頁面

此類動作的發起者可在新UI中檢查其狀態，位於 `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>系統的用戶無需更改即可使用此新功能。 此處僅指出為與舊版內部部署的AEM相較之下的行為變更。

## 新參考網站和教學課程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)，此新的AEM參考網站已更新並發佈，以反映使用AEM建立網站的最佳實務，以及AEM中提供的完整功能、元件和部署模型。 新的參考網站和 [隨附教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) 涵蓋基本主題，例如專案設定、核心元件、可編輯的範本、用戶端程式庫，以及使用Adobe Experience Manager Sites開發元件。

之前，We.Retail預設會與AEM一起安裝（生產模式中啟動時除外）。 在AEMas a Cloud Service中，預設不安裝參考網站。 而是 [git repo](https://github.com/adobe/aem-guides-wknd/) 和 [隨附教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) 提供更新的WKND參考網站代碼。

## 運行時無法使用的功能 {#capabilities-not-available-at-runtime}

AEMas a Cloud Service一律為開啟狀態，且一律為最新狀態。 要達到此目的，必須將AEM儲存庫分離在不可變和可變內容中，並禁止在運行時訪問不可變內容。 有關可變內容與不可變內容的詳細資訊，請參閱 [儲存庫的可變區與不可變區](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

由於不可修改的內容在運行時無法訪問，因此以下AEM Sites操作在運行時不可用：

* i18n字典翻譯
* AEM Sites頁面編輯器中的開發人員模式

這些功能可透過本機、獨立的AEMas a Cloud Service開發人員例項來使用，以更新AEMas a Cloud Service GIT存放庫中的內容和程式碼，但不適用於托管的執行階段例項。
