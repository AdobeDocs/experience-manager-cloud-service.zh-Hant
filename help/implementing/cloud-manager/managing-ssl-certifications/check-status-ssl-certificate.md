---
title: 檢查SSL證書的狀態——管理SSL證書
description: 檢查SSL證書的狀態——管理SSL證書
translation-type: tm+mt
source-git-commit: c6fe5e9dab0e119271c6cea272dddabe7babb1e4
workflow-type: tm+mt
source-wordcount: '233'
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

## IP允許清單{#pre-existing-cdn}的預先存在的CDN設定

具備IP允許清單、SSL憑證或自訂網域名稱之CDN預先存在組態的客戶，將會在&#x200B;**IP允許清單**&#x200B;和&#x200B;**環境**&#x200B;詳細資訊頁面中看到下列訊息。 當客戶透過UI完全移轉所有預先存在的環境設定後，UI上顯示的訊息將會消失，而且訊息可能需要1-2個工作天才能消失。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>為了查看並管理預先存在的配置，必須通過UI添加這些配置，如下圖所示。

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)