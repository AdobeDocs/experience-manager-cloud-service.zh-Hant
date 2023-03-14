---
title: 通知中心
description: 利用通知中心方便地對事件和其他重要資訊採取行動
hidefromtoc: true
source-git-commit: a5977c667d831c47d41cd86b68e9196fbe726899
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未發行。

設定後，AEM as Cloud Service會傳送有關客戶應採取動作之重要資訊的通知。 通知的範例包括已封鎖的佇列或即將到期的憑證集。 您可以在 [下表](#current-notification-types)、和會隨著時間而擴展。 通知會透過電子郵件和以新項目的形式接收，可在通知介面工具集下存取，方法是按一下Adobe Experience Cloud右上角的鈴聲圖示。 可以配置通知設定。

收到通知時，您可以按一下通知，開啟AEMas a Cloud Service的通知中心，彈出式視窗顯示其他內容，說明客戶應採取的建議動作。

除了顯示關於點按通知的資訊外，通知中心還作為中心，您可以在其中查看和管理當前和舊通知集。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知分為兩個高階類別：

1. 事件 — 已發生事件，通常需要迅速解決。 例如，解析已阻止的隊列
1. 主動 — Adobe建議客戶在不久的將來應採取的動作。 例如，若要停止參考已棄用的UI。

請參閱 [下表](#current-notification-types) 以了解目前支援的通知。

從「通知中心」螢幕中，您可以選擇特定的程式和環境，這將對該範圍進行篩選。

## 設定 {#configuration}

您可以依照下列步驟來設定接收通知：

1. 建立下列產品設定檔，如所述 [本文](/help/journey-onboarding/user-groups.md)，從您的組織將適當的AdobeID指派給這些設定檔。
1. 確定通知配置設定。 [在此頁面](https://experience.adobe.com/preferences/notification-section)，請確定Experience Manager訂閱已啟用，且 **其他** 複選框。 此外，建議將「電子郵件」區段設為 **即時通知** 這樣，您就會在事件發生後立即收到通知。

>[!NOTE]
>訂閱可在組織層級運作，讓訂閱者會收到這些方案中所有方案和環境的通知。

## 詳細的使用者流程 {#detailed-user-flow}

按一下電子郵件會帶您前往通知中心，彈出式視窗會顯示您所點按之通知的內容，在某些情況下，連結會顯示其他資訊，說明如何採取更正動作。

![事件詳細資訊](/help/operations/assets/incident-details.png)

按一下 **更多詳情** 連結會導覽使用者至本文，以下表格會參照通知，提供採取動作的相關指引。

在通知中心，您可以看到其他最近通知的清單。 建議您使用「動作」清單確認通知，以Adobe您的組織已知該任務，並稍後在採取更正動作時解決通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，通知應提供解決問題的所有必要內容。 不過，如果Adobe支援有問題，您可以按一下 **聯絡支援** 通知快顯視窗中的連結。 這將顯示一個表單，您可以在其中描述問題並提交它以建立支援票證，該表單還包括對特定通知的引用，以便Adobe支援工程師具有相關上下文。

![聯繫支援1](/help/operations/assets/contact-support1.png)

![聯繫支援2](/help/operations/assets/contact-support2.png)

如同所有支援票證，它會顯示在 [Adobe Admin Console的支援案例索引標籤](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)，您可在此追蹤並新增其他備注。

![Admin Console支援](/help/operations/assets/admin-console-support.png)

## 目前的通知類型 {#current-notification-types}

下表列出目前支援的通知類型

| 通知類型 | 相關產品設定檔 | 更正操作 |
|---|---|---|
| 阻止的複製隊列 | 事件 | 按照 [復寫檔案](/help/operations/replication.md#troubleshooting) |
| 即將到期的S2S憑證 | 主動 | 了解如何在 [產生伺服器端API檔案的存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
