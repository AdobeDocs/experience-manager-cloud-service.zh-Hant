---
title: 使用站點導軌管理站點主題
description: 瞭解「站點」欄的強大功能，幫助您輕鬆定制和管理站點主題。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 使用站點導軌管理站點主題 {#site-rail}

瞭解「站點」欄的強大功能，幫助您輕鬆定制和管理站點主題。

## 概覽 {#overview}

「站點」(Site)欄允許您管理站點的主題和模板資源。 [和其他導軌一樣](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) 如「內容樹」、「參照」或「時間軸」滑軌，「站點」滑軌將作為站點控制台中最左側的面板顯示，顯示有關選定項的資訊。 與其他滑軌不同，「站點」滑軌僅適用於「站點」根。

站點導軌用於管理站點的主題和模板相關資訊，包括：

* [正在下載主題源](#downloading-theme-sources)
* [下載模板資源（如無線幀）](#downloading-template-resources)
* [查看和更改主題版本](#theme-vrsions)
* [啟用前端管線](#enabling-the-front-end-pipeline)

>[!TIP]
>
>查看 [快速建立站點行程](/help/journey-sites/quick-site/overview.md) 熟悉快速站點建立工具和前端管道，以便輕鬆自定義站點主題。

##  下載主題源 {#downloading-theme-sources}

在中建立站AEM點時 [站點模板，](site-templates.md) 您可以下載 [網站主題](site-themes.md) 使用「站點」欄。

在站點控制台中顯示「站點」欄時，選擇站點的根以顯示有關站點的主題資訊。

![下載主題源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點擊或按一下 **下載主題源** 下載網站主題的本地副本 `.zip` 檔案，用於自定義。

##  下載模板資源 {#downloading-template-resources}

[網站模板](site-templates.md) 可以包含除站點內容結構和 [的子菜單。](site-themes.md) 站點模板可以包含線框設計或其他與站點相關的檔案。

如果您的站點基於站點模板，且站點欄顯示在站點控制台中，請選擇站點的根目錄以顯示有關站點的主題資訊，包括其他站點資源。

![下載主題源](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

點擊或按一下標題下方的按鈕 **下載其他模板資源** 下載可用檔案的本地副本。

## 查看和更改主題版本 {#them-versions}

如果您的站點基於站點模板，則其主題可能已由您的前端開發人員自定義。 使用「站點」(Site)軌道，您可以查看當前部署的站點主題的版本，並切換到以前的版本。

在站點控制台中顯示「站點」欄時，選擇站點的根以顯示有關站點的主題資訊。

![鐵路中的站點版本](/help/sites-cloud/administering/assets/theme-versions.png)

顯示主題的當前版本及其提交哈希和上次更新的時間戳。

點擊或按一下 **選擇版本** 的子菜單。

![選擇主題版本](/help/sites-cloud/administering/assets/select-theme-versions.png)

點擊或按一下要更改的版本，然後點擊或按一下 **應用** 來改變。

如AEM果檢測到已通過前端管道部署了較新版本的主題，但未應用到您的站點，則將顯示通知表徵圖。

![較新版本的主題指示器](/help/sites-cloud/administering/assets/new-theme-version.png)

您可以使用 **選擇版本** 按鈕以更新到新主題版本。

## 啟用前端管線 {#enabling-front-end-pipeline}

如果您的站點不是使用站點模板建立的，則無法使用前端管道自定義和部署其主題。

但是，您可以使用「站點」導軌為站點啟用前端管道。

在站點控制台中顯示「站點」欄時，選擇站點的根以顯示有關站點的主題資訊，然後點擊或按一下 **啟用前端管線**。

![啟用前端管道](/help/sites-cloud/administering/assets/enable-fep.png)

有關詳細資訊，請參閱文檔 [啟用前端管線。](enable-front-end-pipeline.md)
