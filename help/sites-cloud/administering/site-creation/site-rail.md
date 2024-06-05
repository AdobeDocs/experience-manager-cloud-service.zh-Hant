---
title: 使用網站面板管理您的網站主題
description: 瞭解網站面板的強大功能，協助您輕鬆自訂和管理網站主題。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---


# 使用網站面板管理您的網站主題 {#site-panel}

瞭解網站面板的強大功能，協助您輕鬆自訂和管理網站主題。

## 概觀 {#overview}

「網站」面板可讓您管理網站的主題和範本資源。 [喜歡其他面板](/help/sites-cloud/authoring/sites-console/console-side-panel.md) 例如「內容樹」、「參照」或「時間軸」面板，「場地」面板會顯示為場地主控台中最左側的面板，顯示有關所選專案的資訊。 與其他面板不同，「網站」面板僅適用於「網站」根。

「網站」面板可用來管理網站的主題和範本相關資訊，包括：

* [下載主題來源](#downloading-theme-sources)
* [下載範本資源，例如線框](#downloading-template-resources)
* [檢視和變更佈景主題版本](#theme-vrsions)
* [啟用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>檢閱 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 以熟悉快速網站建立工具和前端管道，輕鬆自訂網站主題。

## 下載主題來源 {#downloading-theme-sources}

當您根據以下專案在AEM中建立網站時 [網站範本，](site-templates.md) 您可以下載 [網站主題](site-themes.md) 使用網站面板。

在網站主控台中顯示的「網站」面板中，選取網站的根以顯示有關網站的主題資訊。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

選取 **下載主題來源** 將網站主題的本機副本下載為 `.zip` 檔案進行自訂。

## 正在下載範本資源 {#downloading-template-resources}

[網站範本](site-templates.md) 可包含您的網站內容結構以外的資訊， [網站主題。](site-themes.md) 例如，網站範本可包含線框設計或其他網站相關檔案。

如果您的網站是以網站範本為基礎，利用網站主控台中顯示的網站面板，選取網站的根以顯示有關網站的主題資訊，包括其他網站資源。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

選取標題下的一或多個按鈕 **下載其他範本資源** 下載可用檔案的本機復本。

## 檢視和變更佈景主題版本 {#them-versions}

如果您的網站是以網站範本為基礎，其主題可能已由前端開發人員自訂。 使用網站面板，您可以檢視目前部署的網站主題版本，並切換至先前的版本。

在網站主控台中顯示的「網站」面板中，選取網站的根以顯示有關網站的主題資訊。

![面板中的網站版本](/help/sites-cloud/administering/assets/theme-versions.png)

主題的目前版本會顯示其認可雜湊及其上次更新的時間戳記。

選取 **選取版本** 以檢視舊版主題。

![選取主題版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

選取您要變更的版本，然後選取 **套用** 進行變更。

如果AEM偵測到較新版本的主題已透過前端管道部署但未套用至您的網站，則會顯示通知圖示。

![較新版本的主題指標](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用 **選取版本** 按鈕以更新為新佈景主題版本。

## 啟用前端管道 {#enabling-front-end-pipeline}

如果您的網站不是使用網站範本建立的，則無法使用前端管道來自訂和部署其主題。

不過，您可以使用網站面板來啟用網站的前端管道。

在網站主控台中顯示的「網站」面板中，選取網站的根以顯示有關網站的主題資訊，然後選取「 」 **啟用前端管道**.

![啟用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

如需詳細資訊，請參閱檔案 [啟用前端管道。](enable-front-end-pipeline.md)
