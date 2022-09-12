---
title: 使用網站邊欄管理網站主題
description: 了解網站邊欄的強大功能，協助您輕鬆自訂和管理網站主題。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 3e4c6fce54fe336c145d533c05e68e3a1f64c144
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 使用網站邊欄管理網站主題 {#site-rail}

了解網站邊欄的強大功能，協助您輕鬆自訂和管理網站主題。

## 總覽 {#overview}

「網站」邊欄可讓您管理網站的主題和範本資源。 [和其他導軌一樣](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 如「內容樹」、「參照」或「時間軸」滑軌，站點滑軌將在站點控制台中顯示為最左側的面板，顯示有關選定項的資訊。 與其他滑軌不同，站點滑軌僅適用於站點根。

網站邊欄可用於管理您網站的主題和範本相關資訊，包括：

* [下載主題源](#downloading-theme-sources)
* [正在下載模板資源，如無線幀](#downloading-template-resources)
* [查看和更改主題版本](#theme-vrsions)
* [啟用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>檢閱 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 熟悉快速網站建立工具和前端管道，輕鬆自訂您的網站主題。

## 下載主題來源 {#downloading-theme-sources}

當您在AEM中根據 [網站範本，](site-templates.md) 您可以下載 [網站主題](site-themes.md) 使用「網站」邊欄。

在網站主控台中顯示「網站」邊欄時，選取網站的根目錄以顯示網站的主題資訊。

![下載主題源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點選或按一下 **下載主題來源** 下載網站主題的本機副本，如 `.zip` 檔案以供自訂之用。

## 下載範本資源 {#downloading-template-resources}

[網站範本](site-templates.md) 可包含您網站內容結構和 [網站主題。](site-themes.md) 例如，網站範本可以包含線框設計或其他與網站相關的檔案。

如果您的網站是以網站範本為基礎，且網站控制台中顯示「網站」邊欄，請選取網站的根目錄，以顯示網站的主題資訊，包括其他網站資源。

![下載主題源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點選或按一下標題下方的按鈕或按鈕 **下載其他範本資源** 下載可用檔案的本機副本。

## 查看和更改主題版本 {#them-versions}

如果您的網站是以網站範本為基礎，則其主題可能已由您的前端開發人員自訂。 使用「網站」邊欄，您可以檢視目前部署的網站主題版本，並切換至舊版。

在網站主控台中顯示「網站」邊欄時，選取網站的根目錄以顯示網站的主題資訊。

![欄中的網站版本](/help/sites-cloud/administering/assets/theme-versions.png)

主題的當前版本顯示為其提交哈希及其上次更新的時間戳。

點選或按一下 **選擇版本** 來查看主題的舊版本。

![選擇主題版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

點選或按一下您要變更的版本，然後點選或按一下 **套用** 做出改變。

如果AEM偵測到已透過前端管道部署主題的較新版本，但未套用至您的網站，則會顯示通知圖示。

![主題指示器的較新版本](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用 **選擇版本** 按鈕以更新為新主題版本。

## 啟用前端管道 {#enabling-front-end-pipeline}

若您的網站並非使用網站範本建立，則無法使用前端管道來自訂和部署其主題。

不過，您可以使用「網站」邊欄為您的網站啟用前端管道。

在網站主控台中顯示「網站」邊欄時，選取網站的根目錄以顯示網站的主題資訊，然後點選或按一下 **啟用前端管道**.

![啟用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

如需詳細資訊，請參閱本檔案 [啟用前端管道。](enable-front-end-pipeline.md)
