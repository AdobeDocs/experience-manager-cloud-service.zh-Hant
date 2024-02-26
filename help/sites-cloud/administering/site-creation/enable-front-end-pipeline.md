---
title: 啟用前端管道
description: 瞭解如何啟用現有網站的前端管道，以使用網站主題，更快速地自訂您的網站。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 啟用前端管道 {#enable-front-end-pipeline}

瞭解如何啟用現有網站的前端管道，以使用網站主題，更快速地自訂您的網站。

## 概觀 {#overview}

前端管道是一種機制，可以根據快速部署網站的前端計畫碼 [網站主題](site-themes.md) 和 [網站範本。](site-templates.md)

此管道僅處理前端計畫碼，而非部署完整棧疊，這可讓流程更快速，並允許前端開發人員輕鬆快速地自訂您的網站，而無需瞭解AEM。

根據網站範本的網站預設可以使用前端管道。 本檔案說明如何調整現有網站以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用前端管道和網站範本快速部署網站，請參閱 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 以取得簡介。

如果您尚未根據網站範本和主題建立現有網站，AEM可以設定您的網站，以載入使用前端管道部署在現有使用者端資料庫之上的主題。

## 技術細節 {#technical-details}

當您啟動網站的前端管道時，AEM會對您的網站結構做出以下變更。

* 網站的所有頁面都將包含一個額外的CSS和JS檔案，您可以透過專用的Cloud Manager前端管道部署更新來修改這些檔案。
* 新增的CSS和JS檔案最初是空的，但可以下載「主題來源」資料夾以啟動資料夾結構，從而允許透過該管道部署CSS和JS程式碼更新。
* 此變更只能由開發人員透過刪除 `SiteConfig` 和 `HtmlPageItemsConfig` 此操作建立的節點如下 `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>此動作不會自動將網站的現有使用者端程式庫轉換為使用前端管線。 將這些來源從使用者端程式庫資料夾移至前端管道資料夾是一項需要前端開發人員手動執行的任務。

## 要求 {#requirements}

AEM可以自動調整您的現有網站以使用前端管道。 若要這麼做，您的網站必須使用 [核心元件的頁面元件v2或更新版本。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## 啟用前端管道 {#enabling}

使用從網站主控台啟用您的網站 [網站邊欄。](site-rail.md)

1. 登入AEM並透過以下方式導覽至您的網站： **全域導覽** > **網站**.
1. 在主控台中選取您的網站。 選取網站的根目錄，而非任何子頁面。
1. 選取您的網站後，開啟 [邊欄選擇器](/help/sites-cloud/authoring/basic-handling.md#rail-selector) 在左側，然後選擇 **網站**.
1. 在 **網站** 邊欄，按一下按鈕 **啟用前端管道**.

   ![啟用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM會提示您確認將進行的變更概述。 確認並調整您的網站。

現在您的網站已準備好使用前端管道。 若要深入瞭解前端管道和管理您的網站主題，請參閱：

* [使用網站邊欄管理您的網站主題](site-rail.md)
* [快速網站建立歷程](/help/journey-sites/quick-site/overview.md)  — 本檔案歷程為您提供使用前端管道和快速網站建立工具快速部署網站的流程的全方位概觀。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本檔案說明完整棧疊和Web層管道上下文中的前端管道。
