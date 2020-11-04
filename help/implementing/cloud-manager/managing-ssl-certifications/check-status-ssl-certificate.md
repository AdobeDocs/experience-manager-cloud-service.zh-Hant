---
title: 檢查SSL證書的狀態——管理SSL證書
description: 檢查SSL證書的狀態——管理SSL證書
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 檢查SSL證書的狀態 {#checking-status-an-ssl-certificate}

從SSL憑證頁面或「環境詳細資訊」頁面，一覽即可瞭解您的SSL憑證狀態。

您可以從下列色彩配置中識別SSL憑證的狀態：

* **綠色**：表示您的憑證在日後至少60天內有效。

* **橙色**&#x200B;表示您的證書將在60天內到期。 您應該確定您有計畫續約憑證，並透過Cloud Manager UI加以取代，以避免可能的網站存取或中斷。 Cloud Manager會在UI中定期傳送通知，提醒您即將到期的憑證。

* **紅色**&#x200B;表示儘管有多個通知，您的SSL憑證仍已過期。