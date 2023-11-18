---
title: Screensas a Cloud Service中的Screens通知服務
description: 本頁面說明如何在Screensas a Cloud Service設定「通知服務」。
index: true
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---


# Screens 通知服務 {#notification-service}

## 簡介 {#introduction}

### 概觀

如果AEM Screens播放器未在可設定時段內執行Ping動作，AEM Screens Notifications Service可讓管理員收到電子郵件。

### 如何設定

在AEM Screens Cloud上，客戶可建立支援票證，要求提供關於裝置閒置狀態的警報，其資訊如下：

* 客戶名稱
* IMS OrgID
* 排程頻率：指定此監視器應傳送電子郵件的時間或頻率（以小時為單位，例如1）。
* Ping逾時：指定間隔（以分鐘為單位），超過該間隔後，裝置即視為無法連線。
* 電子郵件ID ：將傳送報告的電子郵件ID