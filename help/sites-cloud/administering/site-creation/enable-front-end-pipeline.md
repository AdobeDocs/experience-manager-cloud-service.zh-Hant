---
title: 啟用前端管道
description: 了解如何為現有網站啟用前端管道，以運用網站主題，更快速自訂您的網站。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 啟用前端管道 {#enable-front-end-pipeline}

了解如何為現有網站啟用前端管道，以運用網站主題，更快速自訂您的網站。

## 總覽 {#overview}

前端管道是一種機制，可根據以下條件快速部署網站的前端程式碼： [網站主題](site-themes.md) 和 [網站範本。](site-templates.md)

與其部署完整堆疊，只有前端程式碼由此管道處理，讓流程更快速，也允許前端開發人員在不了解AEM的情況下，輕鬆快速自訂您的網站。

根據網站範本，網站預設可運用前端管道。 本檔案說明如何調整現有網站，以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道，以及如何使用前端管道和網站範本快速部署網站，請檢閱 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 介紹。

如果您尚未根據網站範本和主題建立現有網站，AEM可以設定您的網站，在現有用戶端程式庫之上，載入與前端管道一併部署的主題。

## 技術詳細資訊 {#technical-details}

當您為網站啟用前端管道時，AEM會對您的網站結構進行下列變更。

* 網站的所有頁面都會包含一個額外的CSS和JS檔案，您可透過專用的Cloud Manager前端管道部署更新，以修改此檔案。
* 新增的CSS和JS檔案一開始會是空的，但可下載「主題來源」資料夾，以引導資料夾結構，以便透過該管道部署CSS和JS程式碼更新。
* 此變更只能由開發人員透過刪除 `SiteConfig` 和 `HtmlPageItemsConfig` 此操作在下面建立的節點 `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>此動作不會自動轉換網站的現有用戶端程式庫，以使用字型端管道。 將這些源從客戶端庫資料夾移動到前端管道資料夾是一項需要前端開發人員手動完成的任務。

## 需求 {#requirements}

AEM可自動調整您現有的網站，以使用前端管道。 若要執行此動作，您的網站必須使用 [核心元件的頁面元件v2或更新版本。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## 啟用前端管道 {#enabling}

您可以從Sites主控台使用 [網站邊欄。](site-rail.md)

1. 登入AEM並透過 **全域導覽** > **網站**.
1. 在主控台中選取您的網站。 您必須選取網站的根目錄，而不是任何子頁面。
1. 在選取您的網站後，開啟 [邊欄選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 在左邊選擇 **網站**.
1. 在 **網站** 邊欄，按一下按鈕 **啟用前端管道**.

   ![啟用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM會提示您確認將進行的變更概述。 確認網站已調整。

現在，您的網站已準備好使用前端管道。 若要進一步了解前端管道及管理網站主題，請參閱：

* [使用網站邊欄管理網站主題](site-rail.md)
* [快速網站建立歷程](/help/journey-sites/quick-site/overview.md)  — 本檔案歷程提供您使用前端管道和快速網站建立工具快速部署網站的程式，從頭到尾概述。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本文檔描述完整堆棧和Web層管道的上下文中的前端管道。
