---
title: 檢查SSL證書的狀態 — 管理SSL證書
description: 檢查SSL證書的狀態 — 管理SSL證書
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Checking Status of an SSL Certificate {#checking-status-an-ssl-certificate}

The status of your SSL certificates can be understood at a glance from the SSL certificate page.

您可以通過以下顏色方案標識SSL證書的狀態：

* **綠色**
表示您的證書在將來至少60天內有效。

* **Orange**
Indicates that your certificate is due to expire in under 60 days. 現在是時候確保您有計畫續訂證書並通過Cloud Manager UI替換它，以避免可能的站點訪問或中斷。 Cloud Manager將在UI中發送定期通知，以提醒您即將到期的證書。

* **Red**
Indicates that despite multiple notifications, your SSL certificate has expired.

## 預先存在的CDN配置 {#pre-existing-cdn}

如果客戶的環境包括IP允許清單、SSL證書或自定義域名的預先存在的CDN配置，則會在 **IP允許清單** 和 **環境** 的子菜單。 一旦客戶通過UI完全遷移了所有預先存在的環境配置，則UI上顯示的消息將消失，消息可能需要1-2個工作日才能消失。

>[!NOTE]
>為了查看和管理預先存在的配置，必須通過UI添加這些配置。 請參閱 [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 的子菜單。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
