---
title: AEM Cloud Service 中 AEM Sites 的重大變更
description: 進一步瞭解AEM Cloud Service中AEM Sites的重大變更
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: d1da8559da856e028a5dcad1d0c0b2c00176af0c
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 19%

---


# AEM Sites as a Cloud Service 重大變更 {#notable-changes}

AEM Sitesas a Cloud Service在雲端原生AEMas a Cloud Service平台中提供體驗管理功能。 除了AEMas a Cloud Service的核心優點（例如雲端原生擴充性、運作時間和隨時保持最新狀態），AEM Sitesas a Cloud Service還提供許多Sites特有的變更和新增功能。

>[!NOTE]
>本檔案著重說明AEM Sites的重大變更。 如需AEMas a Cloud Service和其他模組的一般變更，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概覽 - 新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service 簡介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

AEM Sitesas a Cloud Service的變更和新增專案如下：

* [非同步頁面操作](#asynchronous-page-operations)
* [新增參考網站與教學課程](#new-reference-site-and-tutorial)

## 非同步頁面操作 {#asynchronous-page-operations}

在AEM Cloud Service中，傳統上封鎖UI的操作已分解成在背景執行的小型任務。

* 移動頁面
* 轉出頁面

此類動作的發起者可在新的UI中檢查其狀態，網址為 `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>系統使用者不需進行變更即可使用此新功能。 此處僅將它記錄為舊版AEM內部部署的行為變更。

## 新增參考網站與教學課程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)已更新並發佈，此為新的AEM參考網站，反映使用AEM建立網站的最佳實務，以及AEM中提供的全套功能、元件和部署模型。 新的參考網站和 [隨附的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) 涵蓋專案設定、核心元件、可編輯範本、使用者端資料庫和使用Adobe Experience Manager Sites開發元件等基本主題。

之前，We.Retail預設會與AEM一併安裝（除非是在生產模式下啟動）。 在AEMas a Cloud Service中，預設不會安裝參考網站。 而非 [git存放庫](https://github.com/adobe/aem-guides-wknd/) 和 [隨附的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) 並更新提供WKND參考網站程式碼。

## 在執行階段無法使用的功能 {#capabilities-not-available-at-runtime}

AEMas a Cloud Service會一律開啟且隨時保持最新狀態。 若要達到此目的，需要將AEM存放庫分隔為不可變和可變內容，並禁止在執行階段存取不可變內容。 如需可變內容與不可變內容的詳細資訊，請參閱 [可變動與存放庫不可變動區域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

由於在執行階段無法存取不可變內容，下列AEM Sites作業在執行階段無法使用：

* i18n字典翻譯
* AEM Sites頁面編輯器中的開發人員模式

您可以透過AEMas a Cloud Service的本機獨立開發人員執行個體使用這些功能，來更新AEMas a Cloud ServiceGIT存放庫中的內容和程式碼，但不能在託管的執行階段執行個體中使用。
