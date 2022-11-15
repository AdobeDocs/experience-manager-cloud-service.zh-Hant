---
title: AEM as a Cloud Service 版本 2021.11.0 中 Cloud Manager 的發行說明
description: 以下是 AEM as a Cloud Service 版本 2021.11.0 中 Cloud Manager 的發行說明。
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 4505f703754fa46cd746ae4794a3cab65cb19976
workflow-type: ht
source-wordcount: '458'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.11.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.11.0 中 Cloud Manager 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 發行日期是 2021 年 11 月 4 日。下一個版本計畫於 2021 年 12 月 16 日發行。

## 新增功能 {#what-is-new}

* 使用者現在可以善用新的前端管道以加速的方式專門部署前端計劃碼。 請參閱 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)來了解更多資訊。

   >[!IMPORTANT]
   >您必須使用 AEM 版本 `2021.10.5933.20211012T154732Z` 才可使用最新的前端管道。

* 透過以更有效的方式執行計劃碼分析來顯著減少計劃碼品質管道期限，而不需要建置整個 AEM 影像。此變更會在發佈後的未來幾週內逐步展開。

* Git 認可識別碼現在會顯示在管道執行詳細資訊中，如此將更易追蹤產生的計劃碼。

* 計劃建立現在可以透過公開顯示的 API 獲得。

* 環境建立現在可以透過公開顯示的 API 獲得。

* `x-request-id` 回應標題現可於 [www.adobe.io](https://www.adobe.io/) 網站上的 API Playground 中看到。此標題在提交客戶服務問題以進行故障排除時非常有用。

* 身為使用者，零管道的管道卡為我提供了適當的指引。

* 新活動頁面現已可用，其中可以查看管道和計劃碼執行等活動及其關聯的詳細資訊。長期下來，此頁面所列活動範圍會擴展，並提供詳細資訊。

* 新管道現在可以使用懸浮「狀態跨距」(status popover) 來輕鬆查看詳細資訊摘要。可以查看管道執行及其相關詳細資訊。

* 編輯管道 API 現在支援變更部署階段中使用的環境。

* 已針對大型套件引入了 OakPal 掃描流程中的最佳化。

* 品質問題 CSV 檔案現在包含每個品質問題的時間戳。

## 錯誤修正 {#bug-fixes}

* 某些非正統的組建設定會將不必要的檔案儲存在管道的 Maven 成品快取中，導致在啟動和停止組建容器時形成無關的網路 I/O。

* 如果部署階段不存在，管道 PATCH API 將失敗。

* `ClientlibProxyResourceCheck`當存在具有通用基本路徑的用戶端庫時，品質規則會產生誤判問題。

* 達到最大存放庫數時的錯誤訊息未指定錯誤原因。

* 在極少數情況下，由於對某些回應計劃碼的重試處理不當，管道會失敗。
