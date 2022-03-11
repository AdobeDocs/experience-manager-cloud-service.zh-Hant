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

AEM Sitesas a Cloud Service作為雲本地as a Cloud Service平台的一部分提供了經驗管AEM理功能。 除了as a Cloud Service的核心優勢AEM，如雲本機可擴充性、正常運行時間以及始終保持最新，AEM Sitesas a Cloud Service還提供了許多特定於站點的更改和添加。

>[!NOTE]
>本檔案突出了對AEM Sites的顯著變化。 有關對as a Cloud Service和其AEM他模組的常規更改，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概覽 - 新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM as a Cloud Service 重大變更 (發行說明)](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)
>* [介紹AEM Assetsas a Cloud Service](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


AEM Sitesas a Cloud Service之變動及增加如下：

* [非同步頁操作](#asynchronous-page-operations)
* [新建參考站點和教程](#new-reference-site-and-tutorial)

## 非同步頁操作 {#asynchronous-page-operations}

在雲AEM服務中，傳統上阻止UI的操作被分解為在後台運行的較小任務。

* 移動頁面
* 展開頁

此類操作的啟動器可以在新UI中檢查其狀態 `/mnt/overlay/dam/gui/content/asyncjobs.html`。

>[!NOTE]
>
>系統用戶無需更改即可使用此新功能。 此處僅指行為與以前的內部版本相比的變AEM化。

## 新建參考站點和教程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)，新的AEM參考站點已更新和發佈，以反映構建網站的最佳做法AEM，以及中提供的一組全面的功能、元件和部署模AEM型。 新參考站點和 [附帶教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 包括基本主題，如項目設定、核心元件、可編輯模板、客戶端庫和與Adobe Experience Manager Sites的元件開發。

以前，We.Retail預設安裝AEM為（在生產模式下啟動時除外）。  現在，預設情況下，將來不會安裝參考站點。  相反 [git crep](https://github.com/adobe/aem-guides-wknd/) 和 [附帶教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 提供了更新的WKND參考站點代碼。

## 運行時不提供功能 {#capabilities-not-available-at-runtime}

AEMas a Cloud Service始終處於最新狀態。 要實現這一點，需要將儲存AEM庫分離在不可變和可變內容中，並禁止在運行時訪問不可變內容。 有關可變內容與不可變內容的詳細資訊，請參閱 [儲存庫的可變區與不可變區](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由於在運行時無法訪問不可變的內容，因此在運行時不能使用以下AEM Sites操作：

* i18n字典翻譯
* AEM Sites頁面編輯器中的開發人員模式

這些功能可以通過as a Cloud Service的本地獨立開發者實例AEM來使用，用於更新as a Cloud ServiceGIT儲存庫中的內AEM容和代碼，但不能在托管的運行時實例中。
