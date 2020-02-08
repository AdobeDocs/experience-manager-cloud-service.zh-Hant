---
title: AEM cloud服務中AEM網站的顯著變更
description: 'AEM cloud服務中AEM網站的顯著變更 '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# AEM Sites雲端服務的顯著變更 {#notable-changes}

AEM Sites as a Cloud Service是雲端原生AEM的雲端服務平台，提供體驗管理功能。 除了AEM做為雲端服務的核心優點（例如雲端原生的延展性、正常運作時間以及隨時都是最新的）之外，AEM Sites作為雲端服務也提供許多網站特定的變更和新增功能。

>[!NOTE]
>本檔案著重說明AEM Sites的顯著變更。 如需Cloud中AEM的一般變更，請參閱：
>
>* [Adobe Experience Manager(AEM)雲端服務的顯著變更](/help/release-notes/aem-cloud-changes.md)


AEM Sites中的Cloud Service變更和新增如下：

* [非同步頁面作業](#asynchronous-page-operations)
* [新參考網站和教學課程](#new-reference-site-and-tutorial)

## 非同步頁面作業 {#asynchronous-page-operations}

在AEM cloud服務中，傳統上封鎖UI的作業已細分為在背景執行的較小工作。

* 移動頁面
* 展開頁面

此類動作的啟動者可在新的UI中檢查其狀態，網址為 `/mnt/overlay/dam/gui/content/asyncjobs.html`。

>[!NOTE]
>
>系統用戶無需更改即可使用此新功能。 這裡僅指出這是與舊版AEM的內部部署版本相比，行為上的變更。

## 新參考網站和教學課程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)是新的AEM參考網站，已更新並發佈，以反映使用AEM建立網站的最佳實務，以及AEM提供的完整功能、元件和部署模型。 新的參考網站和隨附的教 [學課程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，涵蓋專案設定、核心元件、可編輯範本、用戶端程式庫，以及使用Adobe Experience Manager Sites進行元件開發等基本主題。

之前，We.Retail預設會與AEM一起安裝（除非在生產模式中開始安裝）。  現在，依預設，未來將不會安裝參考網站。  相反地， [提供了git repo](https://github.com/adobe/aem-guides-wknd/) 和隨附 [的教程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，以及更新的WKND參考站點代碼。

## Runtime無法使用的功能 {#capabilities-not-available-at-runtime}

AEM即雲端服務隨時都是最新的。 若要達成此目的，必須將AEM儲存庫分離在不可變和可變內容中，並禁止在執行時期存取不可變內容。 有關可變內容與不可變內容的詳細資訊，請參 [閱儲存庫的可變內容與不可變區域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由於不可變的內容在執行時期無法存取，所以下列AEM Sites作業在執行時期無法使用：

* i18n字典翻譯
* AEM Sites頁面編輯器中的開發人員模式

這些功能可透過AEM的本機、獨立開發人員例項（即雲端服務）來使用，以將AEM中的內容和程式碼更新為Cloud Service GIT儲存庫，但不適用於代管的執行階段例項。
