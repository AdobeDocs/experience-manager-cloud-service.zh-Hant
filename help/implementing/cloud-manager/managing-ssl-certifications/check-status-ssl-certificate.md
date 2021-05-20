---
title: 檢查SSL憑證的狀態 — 管理SSL憑證
description: 檢查SSL憑證的狀態 — 管理SSL憑證
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 檢查SSL證書{#checking-status-an-ssl-certificate}的狀態

您可從SSL憑證頁面一覽即可了解SSL憑證的狀態。

您可以透過下列色彩配置來識別SSL憑證的狀態：

* ****
綠色表示您的憑證在未來至少60天內有效。

* ****
OrangeIndections您的憑證將在60天內到期。您可以確定有計畫續約憑證，並透過Cloud Manager UI加以取代，以避免可能的網站存取或中斷。 Cloud Manager會在UI中傳送定期通知，提醒您憑證即將到期。

* ****
RedIddes即使有多則通知，您的SSL憑證仍會過期。

## IP允許清單的預先存在CDN設定{#pre-existing-cdn}

若環境中包含IP允許清單、SSL憑證或自訂網域名稱的現有CDN設定，則客戶會在&#x200B;**IP允許清單**&#x200B;和&#x200B;**環境**&#x200B;詳細資訊頁面中看到下列訊息。 當客戶透過UI完全移轉所有預先存在的環境設定後，UI上顯示的訊息就會消失，而訊息可能需要1到2個工作天才會消失。

>[!NOTE]
>若要查看及管理預先存在的設定，必須透過UI新增這些設定。 如需詳細資訊，請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
