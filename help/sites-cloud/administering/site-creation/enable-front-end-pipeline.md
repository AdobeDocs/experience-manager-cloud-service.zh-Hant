---
title: 啟用前端管道
description: 瞭解如何啟用現有網站的前端管道，以使用網站主題，更快地自訂您的網站。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: d6ecdae8dd78c3c93a410ca2c8b80322340f439e
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 啟用前端管道 {#enable-front-end-pipeline}

瞭解如何啟用現有網站的前端管道，以使用網站主題，更快地自訂您的網站。

## 概觀 {#overview}

前端管道是一種機制，可根據[網站主題](site-themes.md)和[網站範本，快速部署您網站的前端程式碼。](site-templates.md)

此管道僅處理前端計畫碼，這使得部署過程比完整棧疊部署更快。 它可讓前端開發人員輕鬆自訂您的網站，而不需要瞭解AEM。

根據網站範本的網站預設可以使用前端管道。 本檔案說明如何調整現有網站以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用它和網站範本來快速部署網站，請參閱[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)以取得簡介。

AEM可將您的網站設定為載入使用前端管道部署的主題，即使您的網站不是使用網站範本和主題建立的，方法是將其圖層到現有使用者端資料庫上。

## 技術細節 {#technical-details}

當您啟動網站的前端管道時，AEM會對您的網站結構做出以下變更。

* 網站的所有頁面都包含一個額外的CSS和JS檔案，您可以透過專用的Cloud Manager前端管道部署更新來修改這些檔案。
* 新增的CSS和JS檔案最初是空的。 不過，您可以下載「主題來源」資料夾，以設定透過管道部署CSS和JS程式碼更新所需的資料夾結構。
* 只有開發人員可以復原變更，方法是刪除此作業在`/conf/<site-name>/sling:configs`下方建立的`SiteConfig`和`HtmlPageItemsConfig`節點。

>[!NOTE]
>
>此動作不會自動將網站的現有使用者端程式庫轉換為使用前端管線。 將這些來源從使用者端程式庫資料夾移至前端管道資料夾是一項需要前端開發人員手動執行的任務。

## 要求 {#requirements}

AEM可以自動調整您的現有網站以使用前端管道。 若要執行此工作流程，您的網站必須使用[v2或更新版本的核心元件頁面元件。](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page)

## 啟用前端管道 {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

使用[網站邊欄](site-rail.md)從Sites主控台啟用您的網站。

1. 登入AEM並透過&#x200B;**全域導覽** > **網站**&#x200B;瀏覽您的網站。
1. 在主控台中選取您的網站。 選取網站的根目錄，而非任何子頁面。
1. 選取您的網站後，請開啟左側的[邊欄選取器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)，然後選擇&#x200B;**網站**。
1. 在&#x200B;**站台**&#x200B;邊欄中，按一下&#x200B;**啟用前端管道**&#x200B;按鈕。

   ![啟用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM會提示您確認已進行變更的概述。 確認並調整您的網站。

現在，您的網站已準備好使用前端管道。 若要深入瞭解前端管道和管理您的網站主題，請參閱：

* [使用網站邊欄管理您的網站主題](site-rail.md)
* [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) — 此檔案歷程為您提供使用前端管道和快速網站建立工具來快速部署網站的程式從頭到尾的概觀。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) — 本檔案說明完整棧疊和Web層管道內容中的前端管道。
