---
title: 啟用前端管線
description: 瞭解如何為現有站點啟用前端管道，以利用站點主題更快地自定義站點。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Enabling the Front-End Pipeline {#enable-front-end-pipeline}

瞭解如何為現有站點啟用前端管道，以利用站點主題更快地自定義站點。

## 概覽 {#overview}

前端管道是一種機制，可根據您的網站的前端代碼快速部署 [網站主題](site-themes.md) 和 [站點模板。](site-templates.md)

Instead of deploying the full-stack, only front-end code is handled by this pipeline making the process faster and also allows front-end developers to easily and quickly customize your site without knowledge of AEM.

預設情況下，基於站點模板的站點可以利用前端管道。 本文檔介紹如何調整現有站點以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用它和站點模板快速部署站點，請查看 [快速建立站點](/help/journey-sites/quick-site/overview.md) 的下一頁。

如果您尚未基於站點模板和主題建立現有站點，AEM則可以將站點配置為載入與現有客戶端庫上的前端管道一起部署的主題。

## 技術詳細資訊 {#technical-details}

激活站點的前端管線時，AEM對站點結構進行以下更改。

* 網站的所有頁面都將包含一個附加的CSS和JS檔案，通過專用的Cloud Manager前端管道部署更新可以修改該檔案。
* 添加的CSS和JS檔案最初將為空，但「主題源」資料夾可下載到引導資料夾結構，該結構允許通過該管道部署CSS和JS代碼更新。
* This change can only be undone by a developer, by deleting the `SiteConfig` and `HtmlPageItemsConfig` nodes that this operation creates below `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>This action won&#39;t automatically convert the existing client libraries of the site to use the font-end pipeline. 將這些源從客戶端庫資料夾移動到前端管道資料夾是一項需要前端開發人員手動完成的任務。

## Requirements {#requirements}

可AEM以自動調整現有站點以使用前端管線。 要能夠執行此操作，您的站點必須使用 [核心元件的頁面元件的v2或更高版本。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Enabling Front-End Pipeline {#enabling}

從「站點」控制台使用 [鐵軌。](site-rail.md)

1. 登錄AEM並通過 **全局導航** > **站點**。
1. 在控制台中選擇您的站點。 You must select the root of the site and not any child pages.
1. 選擇您的站點後，開啟 [軌道選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 在左邊選擇 **站點**。
1. In the **Site** rail, click the button **Enable Front End Pipeline**.

   ![Enable front-end pipeline](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM prompts you to confirm with an overview of the changes that will be made. 確認並調整您的站點。

Now your site is ready to use the front-end pipeline. 要瞭解有關前端管道和管理站點主題的詳細資訊，請參閱：

* [Using the Site Rail to Manage Your Site Theme](site-rail.md)
* [快速建立站點行程](/help/journey-sites/quick-site/overview.md)  — 本文檔將為您提供使用前端管道和快速站點建立工具快速部署站點的過程並從頭到尾的概述。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本文檔描述了整個堆棧和Web層管道上下文中的前端管道。
