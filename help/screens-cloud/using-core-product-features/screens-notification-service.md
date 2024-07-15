---
title: Screens中的Screens Notification Serviceas a Cloud Service
description: 本頁說明如何在Screensas a Cloud Service中設定「通知服務」。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# Screens 通知服務 {#notification-service}

## 簡介 {#introduction}

### 概觀

AEM Screens Notifications Service可讓管理員接收報表，其中包含未在電子郵件可設定時段內Ping的所有AEM Screens播放器清單。

### 如何設定

在AEM Screens Cloud上，客戶可以透過建立支援票證來請求裝置閒置狀態的報告，該票證包含下列資訊：

* 客戶名稱
* IMS OrgID
* 排程頻率：指定此監視器應傳送電子郵件的時間或頻率（以小時為單位，例如1）。
* Ping逾時：指定間隔（以分鐘為單位），超過該間隔後，裝置即視為無法連線。
* 電子郵件ID ：將傳送報告的電子郵件ID

>[!NOTE]
>只有在產生電子郵件時尚未針對指定Ping逾時偵測的裝置，才會回報電子郵件播放器。

### 範例使用案例

如果您將報表時間設定為5 am，而Ping逾時設定為1小時，則如果您的Screens裝置未在凌晨4:00至凌晨5:00之間Ping，您將會收到電子郵件通知，確認裝置閒置中。
