---
title: Cloud Manager的發行說明，作AEM為Cloud Service版本2020.4.0
description: Cloud Manager的發行說明，作AEM為Cloud Service版本2020.4.0
feature: 發行資訊
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 77%

---


# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2020.4.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2020.4.0。

## 發行日期 {#release-date}

Cloud Manager作為2020.4.0Cloud ServiceAEM的發行日期為2020年4月9日。

## 新功能 {#whats-new-cloud-manager}

* Cloud Manager UI 的「環境」頁面現在已可使用發佈者 URL。
* 導覽的變更項目可供使用者從 Cloud Manager 概覽頁面編輯、切換或新增程式。
* 變更項目可讓使用者在 Cloud Manager 登陸頁面上的程式資訊卡編輯程式。
* 新管道狀態&#x200B;**管道正在執行**&#x200B;會針對關聯環境而顯示。
* 改良管道執行頁面的可理解性。這項改良包括管道名稱 (僅限非生產用管道) 和類型的顯示，以及指出管道狀態為「處理中/已取消/失敗」的徽章。
* 透過工具提示改善使用者體驗及「新增程式/環境」按鈕遭停用原因的可理解性。
* 失敗的環境現在可透過 UI 和 API 刪除。
* 用於產生 git 密碼的程式對於基礎服務層的問題更具彈性。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 管道執行詳細資訊頁面上的中繼環境連結無法一致地導覽至正確位置。
* 環境建立程序中的各個步驟會比所需時間提前逾時，導致程序失敗。
* 已建置容器中使用的 Maven 設定經過更新，可避免在下載成品中繼資料時發生鎖死。
* 某些情況下，「建置影像」步驟會無法成功下載客戶封裝。
* 某些罕見情況會導致環境無法刪除。
* 無法一致地收到 Experience Cloud 通知。

