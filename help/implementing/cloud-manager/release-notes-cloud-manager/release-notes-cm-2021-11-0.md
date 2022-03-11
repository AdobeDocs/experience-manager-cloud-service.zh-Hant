---
title: Cloud Manager在as a Cloud Service版AEM2021.11.0中的發行說明
description: 以下是as a Cloud Service版AEM2021.11.0中的Cloud Manager發行說明
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.11.0 {#release-notes}

本頁概述了as a Cloud Service2021.11.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service2021.11.0中的發AEM布日期為2021年11月4日。
下一版計畫於2021年12月16日發行。

## 新增功能 {#what-is-new}

* 用戶現在可以利用新的前端管道以加速的方式專門部署前端代碼。 請參閱 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 來瞭解更多資訊。

   >[!IMPORTANT]
   >您必須處於版AEM本 `2021.10.5933.20211012T154732Z` 利用新的前端管道。

* 通過以更有效的方式執行代碼分析而不需要構建整個影像，代碼質量流水線持續時間顯著AEM縮短。 此更改將在發佈後的幾週內逐步展開。

* Git提交ID現在將顯示在管道執行詳細資訊中，使跟蹤生成的代碼更容易。

* 現在可通過公開的API建立程式。

* 現在可通過公開的API建立環境。

* 的 `x-request-id` 響應標頭現在可在上的API Ploagn中看到 [www.adobe.io](https://www.adobe.io/)。 此標題在提交客戶關心問題以進行故障排除時非常有用。

* 作為用戶，我看到零管線的管線卡為我提供了適當的指導。

* 現在可以使用新的「活動」頁，其中可以查看諸如管道和代碼執行等活動及其關聯的詳細資訊。 隨著時間的推移，此頁中列出的活動將擴展範圍以及提供的詳細資訊。

* 現在可以使用一個新的「管線」(Pipelines)頁面，該頁面具有懸停時的狀態跨距，以便輕鬆查看詳細資訊摘要。 可以查看管道執行及其關聯的詳細資訊。

* 「編輯管道API」現在支援更改部署階段中使用的環境。

* 介紹了OakPal掃描過程中對大包裝的優化。

* 質量問題CSV檔案現在將包含每個質量問題的時間戳。

## 錯誤修正 {#bug-fixes}

* 某些非常規的生成配置導致不必要的檔案儲存在管道的Maven項目快取中，這導致在啟動和停止生成容器時產生額外的網路I/O。

* 如果部署階段不存在，管道PATCHAPI將失敗。

* 的 `ClientlibProxyResourceCheck` 當存在具有共同基本路徑的客戶端庫時，質量規則會產生誤報問題。

* 達到最大資料庫數時的錯誤消息未指定錯誤原因。

* 在少數情況下，管道由於某些響應代碼的重試處理不當而失敗。
