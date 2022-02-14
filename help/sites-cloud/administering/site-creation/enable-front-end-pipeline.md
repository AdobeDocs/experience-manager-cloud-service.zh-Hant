---
title: 啟用前端管線
description: 瞭解如何為現有站點啟用前端管道，以利用站點主題更快地自定義站點。
feature: Administering
role: Admin
source-git-commit: dc7e89c601bb02c78f65ca58eff34c15092b5561
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 啟用前端管線 {#enable-front-end-pipeline}

瞭解如何為現有站點啟用前端管道，以利用站點主題更快地自定義站點。

## 概覽 {#overview}

前端管道是一種機制，可根據您的網站的前端代碼快速部署 [網站主題](site-themes.md) 和 [站點模板。](site-templates.md)

與部署完整堆棧不同，只有前端代碼由此管道處理，使流程更快，並且允許前端開發人員輕鬆、快速地定制您的站點，而無需知AEM道。

預設情況下，基於站點模板的站點可以利用前端管道。 本文檔介紹如何調整現有站點以利用前端管道。

>[!TIP]
>
>如果您不熟悉前端管道以及如何使用它和站點模板快速部署站點，請查看 [快速建立站點](/help/journey-sites/quick-site/overview.md) 的下一頁。

如果您尚未基於站點模板和主題建立現有站點，AEM則可以將站點配置為載入與現有客戶端庫上的前端管道一起部署的主題。

## 要求 {#requirements}

可AEM以自動調整現有站點以使用前端管線。 要能夠執行此操作，您的站點必須使用 [核心元件的頁面元件的v2或更高版本。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## 啟用前端管線 {#enabling}

啟用您的站點可從「站點」控制台完成。

1. 登錄AEM並通過 **全局導航** > **站點**。
1. 在控制台中選擇您的站點。 必須選擇站點的根，而不是任何子頁。
1. 選擇您的站點後，開啟 [軌道選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 在左邊選擇 **站點**。
1. 在 **站點** 欄，按一下按鈕 **啟用前端管線**。

   ![啟用前端管道](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. 提AEM示您以將進行的更改的概述進行確認。 確認並調整您的站點。

現在，您的站點已準備好使用前端管道。 要瞭解有關前端管道的更多資訊，請參閱：

* [快速建立站點行程](/help/journey-sites/quick-site/overview.md)  — 本文檔將為您提供使用前端管道和快速站點建立工具快速部署站點的過程並從頭到尾的概述。
* [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)  — 本文檔描述了整個堆棧和Web層管道上下文中的前端管道。
