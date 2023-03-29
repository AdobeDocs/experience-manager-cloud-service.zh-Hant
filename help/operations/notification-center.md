---
title: 通知中心
description: 利用通知中心可輕鬆對事件和其他重要資訊採取行動
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: ht
source-wordcount: '638'
ht-degree: 100%

---


# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未推出。

設定後，AEM as Cloud Service 會發送有關客戶應採取行動的重要資訊通知。通知的範例包括鎖定佇列或即將到期的認證組。完整的通知類型集可以在[下表](#current-notification-types)中查看，其會隨時間推移增加。通知透過電子郵件和通知小工具下的新項目接收，可透過點擊整個 Adobe Experience Cloud 右上角的鈴鐺圖示來存取。可設定通知設定。

收到通知後，可以點擊它打開 AEM as a Cloud Service 的通知中心，這會彈出顯示附加內容的快顯視窗，說明建議客戶採取的動作。

除了顯示有關剛剛點擊的通知資訊外，通知中心還可充當中樞，讓您在其中查看和管理目前和較舊的通知組。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

有兩種高級通知類別：

1. 事件 - 事件已經發生，通常需要及時解決。例如，解析鎖定的佇列
1. 主動 - Adobe 建議客戶應在近期採取行動。例如，停止參考已棄用的 UI。

請參閱[下表](#current-notification-types)了解目前支援的通知。

從通知中心畫面中，您可以選擇特定的程序和環境，這可對該範圍進行篩選。

## 設定 {#configuration}

您可以按照以下步驟設定接收通知：

1. 建立以下產品設定檔，如[本文](/help/journey-onboarding/notification-profiles.md)中所述，將您組織的適當 Adobe ID 分配給這些設定檔。
1. 決定通知設定。[在此頁面](https://experience.adobe.com/preferences/notification-section)上，確保已啟用 Experience Manager 訂閱並選取&#x200B;**其他**&#x200B;核取方塊。此外，建議將電子郵件部分設定為&#x200B;**即時通知**，以便您在事件發生後立即收到通知。

>[!NOTE]
>訂閱在組織層級執行，因此訂閱者將收到有關這些程序中的所有程序和環境通知。

## 詳細的使用者流程 {#detailed-user-flow}

點擊電子郵件會將您帶到通知中心，快顯視窗會顯示您點擊的通知內容，在某些情況下，還會顯示說明如何採取糾正措施的其他資訊連結。

![事件詳細資料](/help/operations/assets/incident-details.png)

點擊&#x200B;**了解更多**&#x200B;連結可將使用者導覽至本文，下表可參考其中的通知，其提供採取何種動作的指導。

在通知中心，您可以看到其他最近通知的清單。建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，通知應提供解決問題的所有必要內容。但是，如果對 Adobe 支援有疑問，您可以點擊通知快顯視窗中的&#x200B;**聯絡支援人員**&#x200B;連結。這將彈出一個表格，您可以在表格中描述問題並提交它以建立支援票證，其中可包含對特定通知的參考，以便 Adobe 支援工程師了解相關內容。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 目前通知類型 {#current-notification-types}

下表列出了目前支援的通知類型

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---|---|---|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |
