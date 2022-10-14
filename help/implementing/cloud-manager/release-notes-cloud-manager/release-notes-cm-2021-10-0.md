---
title: AEM as a Cloud Service 版本 2021.10.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.10.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: f8a87b00-52ce-42a6-a955-45cb14703b40
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.10.0 中 Cloud Manager 的發行說明

>[!NOTE]
>若要閱讀 Adobe Experience Manager as a Cloud Service 的目前發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 發行日期是 2021 年 10 月 14 日。


### 新增功能 {#what-is-new}

* 為了準備一些即將發生的變化，現有的部署管道現在將在使用者界面中被引用和標記為&#x200B;**完整堆疊**&#x200B;管道。

* 管道卡已刷新，現在顯示一個整合的面，顯示生產和非生產管道，使用者可以直接從與每個管道關聯的操作選單中選擇執行/暫停/恢復。

* Deployment Manager 角色的使用者現在可以透過 UI 以自助方式刪除生產管道。

* 新增和編輯管道體驗已更新，現在可以使用熟悉的現代模式。

* Cloud Manager 的使用者現在可以透過使用者界面直接提交意見反饋&#x200B;**意見反饋**&#x200B;著陸頁右上角的按鈕。

* 現在可以從 Cloud Manager 的使用者界面下載年度 SLA 圖表。

* 計劃碼品質和非生產管道執行現在將在構建步驟中使用更有效的淺層克隆過程，從而為擁有特別大的 git 存放庫的客戶帶來更快的構建時間。

* 新增 IP 允許清單嚮導現在將通知使用者是否已達到 IP 允許清單的最大允許數量。

* Cloud Manager API 文件現在包括一個交互式遊樂場，允許登入使用者從他們的瀏覽器中試驗 API。查看 [Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 的更多細節。

* 如果停用「瀏覽至」下的選擇選項，則程序卡上的工具提示將更具描述性。現在會顯示「生產環境不存在。」

### 錯誤修正 {#bug-fixes}

* 在極少數情況下，當 Adobe 工作人員恢復客戶的環境時，在環境完全執行之前，恢復就被認為已完成。

* 在環境建立期間發出的某些內部請求沒有被重試。

* 如果在網域名稱驗證後出現部署失敗錯誤，則已更正錯誤消息以請求客戶聯繫其 Adobe 代表。
