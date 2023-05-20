---
title: 通知中心
description: 利用通知中心可輕鬆對事件和其他重要資訊採取行動
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 3aa753fb5cc5130ced7e9baafde63e8825394dce
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 100%

---

# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未推出。

AEM as Cloud Service 在發生需要立即採取行動的嚴重事件時會傳送通知，並提出主動建議以進行最佳化。例如，佇列阻塞或一組過期的憑證；您可在[下表](#supported-notification-types)檢視整套通知類型，通知類型會隨時間增加。

這些通知可以設定為透過電子郵件和通知 Widget 接收，按一下 Adobe Experience Cloud 畫面右上角的鈴鐺圖示即可存取。

收到通知後，可以按一下它開啟 AEM as a Cloud Service 通知中心，這會彈出顯示附加內容的快顯視窗，說明要客戶採取的動作。

除了顯示有關剛剛點擊的通知資訊外，通知中心還可充當中樞，讓您在其中查看和管理目前和較舊的通知組。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

有兩種基本通知類別會出現在通知中心：

1. 操作事件 - 事件已經發生，通常需要及時解決。例如，解析阻塞的佇列。
1. 主動建議 - Adobe 建議客戶應該在近期採取行動。例如，停止參考已棄用的 UI。

請參閱[下表](#supported-notification-types)了解目前支援的通知。

從通知中心，您可以選取特定的程序和環境，這可對該範圍進行篩選。

## 設定 {#configuration}

請按照以下步驟設定接收通知：

1. 建立以下產品設定檔，如[本文](/help/journey-onboarding/notification-profiles.md)中所述，也將您組織的適當 Adobe ID 指派給這些設定檔。這可讓管理員確定哪些使用者有資格接收這些通知。
1. 在上一步驟中每個被指派的使用者都可以設定其接收通知的方式。在 [Experience Cloud 偏好設定頁面](https://experience.adobe.com/preferences/notification-section)，確保 Experience Manager 訂閱已啟用，並且應用程式內和電子郵件欄的「**操作事件**」和「**主動建議**」核取方塊已選取 (請見下圖)。此外，建議將電子郵件區段設定為&#x200B;**即時通知**，以便您在事件發生後立即收到通知。

![設定訂閱](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>通知在組織層級執行，因此訂閱者將收到有關這些程序中的所有程序和環境通知。

## 詳細的使用者流程 {#detailed-user-flow}

點擊電子郵件會將您帶到通知中心，快顯視窗會顯示您點擊的通知內容，在某些情況下，還會顯示說明如何採取糾正措施的其他資訊連結。

![事件詳細資料](/help/operations/assets/incident-details.png)

點擊&#x200B;**了解更多**&#x200B;連結可將使用者導覽至本文，下表可參考其中的通知，其提供採取何種動作的指導。

在通知中心，您可以看到其他最近通知的清單。建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，通知應提供解決問題的所有必要內容。但是，如果對 Adobe 支援有疑問，您可以點擊通知快顯視窗中的&#x200B;**聯絡支援人員**&#x200B;連結。這將彈出一個表格，您可以在表格中描述問題並提交它以建立支援票證，其中可包含對特定通知的參考，以便 Adobe 支援工程師了解相關內容。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/tw/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 哪些通知會出現？ {#which-notification}

AEM as a Cloud Service 有多種類型的通知，但只有一部分出現在通知中心，如下表所示。

| 通知類型 | 說明 | 如何設定 | 出現在通知中心 |
|---|---|---|---|
| 操作事件 | 需要立即採取行動的嚴重事件 | 使用者被指派到「事件通知 - Cloud Service」產品設定檔，[Experience Cloud 偏好設定](https://experience.adobe.com/preferences)中的「操作事件」核取方塊已選取 | X |
| 主動建議 | 應該計劃的最佳化 | 用者被指派到「主動通知 - Cloud Service」產品設定檔，[Experience Cloud 偏好設定](https://experience.adobe.com/preferences)中的「主動建議」核取方塊已選取 | X |
| Cloud Manager 管道狀態 | 有關管道狀態的資訊 | 具有企業所有者、方案管理員或部署管理員角色的使用者，[Experience Cloud 偏好設定](https://experience.adobe.com/preferences)中的「其他」核取方塊已選取 |  |

## 支援的通知類型 {#supported-notification-types}

下表列出了目前支援的通知類型。

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---|---|---|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |

