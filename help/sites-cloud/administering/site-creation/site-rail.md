---
title: 使用網站邊欄管理您的網站主題
description: 瞭解網站邊欄的強大功能，協助您輕鬆自訂和管理網站主題。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 使用網站邊欄管理您的網站主題 {#site-rail}

瞭解網站邊欄的強大功能，協助您輕鬆自訂和管理網站主題。

## 概觀 {#overview}

「網站」邊欄可讓您管理網站的主題和範本資源。 [如同其他導軌](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 例如「內容樹」、「參照」或「時間軸」邊欄，「場地」邊欄會顯示為場地主控台中最左側的面板，顯示有關所選專案的資訊。 與其他邊欄不同，網站邊欄僅適用於網站根目錄。

「網站」邊欄可用來管理網站的主題和範本相關資訊，包括：

* [下載主題來源](#downloading-theme-sources)
* [下載範本資源，例如線框](#downloading-template-resources)
* [檢視和變更佈景主題版本](#theme-vrsions)
* [啟用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>檢閱 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 以熟悉快速網站建立工具和前端管道，輕鬆自訂網站主題。

## 下載主題來源 {#downloading-theme-sources}

當您根據以下專案在AEM中建立網站時 [網站範本，](site-templates.md) 您可以下載 [網站主題](site-themes.md) 使用網站邊欄。

利用站台主控台中顯示的站台邊欄，選取站台的根以顯示有關站台的主題資訊。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點選或按一下 **下載主題來源** 將網站主題的本機副本下載為 `.zip` 檔案進行自訂。

## 正在下載範本資源 {#downloading-template-resources}

[網站範本](site-templates.md) 可包含您的網站內容結構以外的資訊， [網站主題。](site-themes.md) 例如，網站範本可包含線框設計或其他網站相關檔案。

如果您的網站是以網站範本為基礎，利用網站主控台中顯示的網站邊欄，選取網站的根以顯示有關網站的主題資訊，包括其他網站資源。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點選或按一下標題下方的一或多個按鈕 **下載其他範本資源** 下載可用檔案的本機復本。

## 檢視和變更佈景主題版本 {#them-versions}

如果您的網站是以網站範本為基礎，其主題可能已由前端開發人員自訂。 使用網站邊欄，您可以檢視目前部署的網站主題版本，並切換至先前的版本。

利用站台主控台中顯示的站台邊欄，選取站台的根以顯示有關站台的主題資訊。

![邊欄中的網站版本](/help/sites-cloud/administering/assets/theme-versions.png)

主題的目前版本會顯示其認可雜湊及其上次更新的時間戳記。

點選或按一下 **選取版本** 以檢視舊版主題。

![選取主題版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

點選或按一下您要變更的版本，然後點選或按一下 **套用** 進行變更。

如果AEM偵測到較新版本的主題已透過前端管道部署但未套用至您的網站，則會顯示通知圖示。

![較新版本的主題指標](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用 **選取版本** 按鈕以更新為新佈景主題版本。

## 啟用前端管道 {#enabling-front-end-pipeline}

如果您的網站不是使用網站範本建立的，則無法使用前端管道來自訂和部署其主題。

不過，您可以使用網站邊欄啟用網站的前端管道。

利用站台主控台中顯示的站台邊欄，選取您的站台根以顯示有關站台的主題資訊，然後點選或按一下 **啟用前端管道**.

![啟用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

如需詳細資訊，請參閱檔案 [啟用前端管道。](enable-front-end-pipeline.md)
