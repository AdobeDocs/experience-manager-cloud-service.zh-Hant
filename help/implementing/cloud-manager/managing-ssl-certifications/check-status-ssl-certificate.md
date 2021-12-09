---
title: 檢查SSL憑證的狀態 — 管理SSL憑證
description: 檢查SSL憑證的狀態 — 管理SSL憑證
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 檢查SSL憑證的狀態 {#checking-status-an-ssl-certificate}

您可從SSL憑證頁面一覽即可了解SSL憑證的狀態。

您可以透過下列色彩配置來識別SSL憑證的狀態：

* **綠色**
指出您的憑證在未來至少60天內有效。

* **橙色**
指出您的憑證將在60天內到期。 您可以確定有計畫續約憑證，並透過Cloud Manager UI加以取代，以避免可能的網站存取或中斷。 Cloud Manager會在UI中傳送定期通知，提醒您憑證即將到期。

* **紅色**
指出儘管有多個通知，您的SSL憑證仍已過期。

## 預先存在的CDN設定 {#pre-existing-cdn}

若客戶的環境包含IP允許清單、SSL憑證或自訂網域名稱的現有CDN設定，則會在 **IP允許清單** 和 **環境** 詳細資訊頁面。 當客戶透過UI完全移轉所有預先存在的環境設定後，UI上顯示的訊息就會消失，而訊息可能需要1到2個工作天才會消失。

>[!NOTE]
>若要查看及管理預先存在的設定，必須透過UI新增這些設定。 請參閱 [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 以取得更多詳細資訊。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
