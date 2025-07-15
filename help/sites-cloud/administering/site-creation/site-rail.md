---
title: 使用網站面板管理您的網站主題
description: 瞭解網站面板的強大功能，協助您透過發佈傳遞輕鬆自訂和管理傳統AEM製作專案的網站主題。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
source-git-commit: 076005e1ed1ca3303ed5843a3f27e0d707df5022
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---


# 使用網站面板管理您的網站主題 {#site-panel}

{{traditional-aem}}

瞭解網站面板的強大功能，協助您透過發佈傳遞輕鬆自訂和管理傳統AEM製作專案的網站主題。

## 概觀 {#overview}

「網站」面板可讓您透過[發佈傳遞，管理傳統AEM製作專案的主題和範本資源。](/help/sites-cloud/authoring/author-publish.md) [如同其他面板](/help/sites-cloud/authoring/sites-console/console-side-panel.md) （例如「內容樹狀目錄」、「參考」或「時間軸」面板），「網站」面板會顯示為網站主控台中最左側的面板，顯示選取專案的相關資訊。 與其他面板不同，「網站」面板僅適用於「網站」根。

「網站」面板可用來管理網站的主題和範本相關資訊，包括：

* [下載主題來源](#downloading-theme-sources)
* [下載範本資源，例如線框](#downloading-template-resources)
* [檢視和變更佈景主題版本](#theme-vrsions)
* [啟用前端管道](#enabling-the-front-end-pipeline)

>[!TIP]
>
>檢閱[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)，熟悉快速網站建立工具和前端管道，以輕鬆自訂網站主題。

## 下載主題來源 {#downloading-theme-sources}

當您根據[網站範本，](site-templates.md)在AEM中建立網站時，可以使用網站面板下載[網站主題](site-themes.md)。

在網站主控台中顯示的「網站」面板中，選取網站的根以顯示有關網站的主題資訊。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

選取&#x200B;**下載主題來源**，將網站主題的本機復本下載為`.zip`檔案以供自訂。

## 正在下載範本資源 {#downloading-template-resources}

[網站範本](site-templates.md)可以包含您的網站內容結構和[網站主題的資訊。例如，](site-themes.md)網站範本可包含線框設計或其他網站相關檔案。

如果您的網站是以網站範本為基礎，利用網站主控台中顯示的網站面板，選取網站的根以顯示有關網站的主題資訊，包括其他網站資源。

![下載主題來源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

選取標題&#x200B;**下載其他範本資源**&#x200B;下的一個或多個按鈕，以下載可用檔案的本機復本。

## 檢視和變更佈景主題版本 {#them-versions}

如果您的網站是以網站範本為基礎，其主題可能已由前端開發人員自訂。 使用網站面板，您可以檢視目前部署的網站主題版本，並切換至先前的版本。

在網站主控台中顯示的「網站」面板中，選取網站的根以顯示有關網站的主題資訊。

面板中的![網站版本](/help/sites-cloud/administering/assets/theme-versions.png)

主題的目前版本會顯示其認可雜湊及其上次更新的時間戳記。

選取&#x200B;**選取版本**&#x200B;以檢視舊版主題。

![選取主題版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

選取您要變更的版本，然後選取&#x200B;**套用**&#x200B;以進行變更。

如果AEM偵測到較新版本的主題已透過前端管道部署但未套用至您的網站，則會顯示通知圖示。

![較新版本的主題指標](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用&#x200B;**選取版本**&#x200B;按鈕來更新為新佈景主題版本。

## 啟用前端管道 {#enabling-front-end-pipeline}

如果您的網站不是使用網站範本建立的，則無法使用前端管道來自訂和部署其主題。

不過，您可以使用網站面板來啟用網站的前端管道。

在站台主控台中顯示的站台面板中，選取站台根以顯示有關站台的主題資訊，然後選取&#x200B;**啟用前端管道**。

![正在啟用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

如需詳細資訊，請參閱檔案[啟用前端管道。](enable-front-end-pipeline.md)
