---
title: 檢查SSL證書的狀態——管理SSL證書
description: 檢查SSL證書的狀態——管理SSL證書
translation-type: tm+mt
source-git-commit: f426a9a653a3a3ae06abdbd2262e5d8f4beff277
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 正在檢查SSL證書的狀態{#checking-status-an-ssl-certificate}

從SSL憑證頁面一覽即可瞭解您的SSL憑證狀態。

您可以從下列色彩配置中識別SSL憑證的狀態：

* **綠**
色表示您的憑證在日後至少60天內有效。

* **橙**
色表示您的憑證將在60天內到期。您應該確定您有計畫續約憑證，並透過Cloud Manager UI加以取代，以避免可能的網站存取或中斷。 Cloud Manager會在UI中定期傳送通知，提醒您即將到期的憑證。

* **紅色**
表示儘管有多個通知，您的SSL憑證仍已過期。