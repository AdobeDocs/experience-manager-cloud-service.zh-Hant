---
title: AEM as a Cloud Service 版本 2022.01.0 中 Cloud Manager 的發行說明
description: 以下是 AEM as a Cloud Service 版本 2022.01.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: ht
source-wordcount: '246'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2022.01.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2022.01.0 中 Cloud Manager 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2022.01.0 中的 Cloud Manager 發行日期是 2022 年 1 月 20 日。下一版本計畫於 2022 年 2 月 10 日發行。

## 新增功能 {#what-is-new}

* Cloud Manager [在偵測到多個全堆疊管道執行中使用了相同的 Git 認可時，將避免重建計劃碼基底](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* 現在存取 AEM 環境記錄檔需要 **Deployment Manager** 產品設定檔。沒有此設定檔的使用者將在使用者介面中看到停用按鈕。
* UI 不允許針對未啟用 Sites 解決方案的計畫設定前端管道。
* 在產生 Git 密碼時，將立即顯示到期日期。

## 錯誤修正 {#bug-fixes}

* 已修正部署部分前端管道時發生的空指針異常。
* 現在可以在環境執行過時版本的 AEM 時新增、更新和刪除環境變數。
* 對於在某些極少數情況下使用計畫步驟的管道，建置影像步驟將不再標記為錯誤。
* 對於僅有一個存放庫的計畫，管道執行畫面現在將顯示存放庫名稱。
