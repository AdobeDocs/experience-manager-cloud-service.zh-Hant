---
title: 動作中心
description: 善用行動中心，以方便對事件和其他重要資訊採取行動
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: ca7cad567a5f83cd1edc14def6d961b8ba3b7f1f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 32%

---

# 動作中心 {#actions-center}

>[!NOTE]
>此功能尚未推出。

AEM as Cloud Service會在發生需要立即採取行動的重大事件時，傳送行動中心電子郵件通知，以及主動最佳化建議。 例如，封鎖的佇列或即將到期的認證集；您可在 [下表](#supported-notification-types)，會隨著時間推移擴展。

收到「動作中心」電子郵件通知時，可以按一下該通知以開啟AEMas a Cloud Service的「動作中心」，並出現快顯視窗，顯示說明客戶應採取的動作的其他內容。

除了顯示有關剛點按的電子郵件通知的資訊外，「動作中心」也是您檢視和管理目前及舊通知集的中心。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

「作業中心」中會顯示兩種高層級的通知類別：

1. 操作事件 - 事件已經發生，通常需要及時解決。例如，解析阻塞的佇列。
1. 主動建議 - Adobe 建議客戶應該在近期採取行動。例如，停止參考已棄用的 UI。

請參閱 [下表](#supported-notification-types) 適用於動作中心目前支援的通知。

從「動作中心」中，您可以選取特定的方案和環境，其效果是篩選該範圍。

## 設定 {#configuration}

若要設定接收Actions Center電子郵件通知，請建立描述的產品設定檔 [本文章內容](/help/journey-onboarding/notification-profiles.md)，即事件通知 — Cloud Service和主動通知 — Cloud Service。 同時從您的組織指派適當的AdobeID給這些設定檔。 這可讓管理員判斷哪些使用者符合接收這些電子郵件通知的資格。

>[!NOTE]
>動作中心電子郵件通知會在組織層級運作，因此訂閱者會收到這些計畫中所有計畫和環境的通知。

## 詳細的使用者流程 {#detailed-user-flow}

按一下電子郵件即可將您帶至「警示中心」，其中快顯視窗會顯示您按一下之通知的前後關聯，在某些情況下，還會顯示其他資訊的連結，說明如何採取更正動作。

![事件詳細資料](/help/operations/assets/incident-details.png)

按一下 **瞭解更多** 連結會將使用者導覽至本文章，其中通知型別可在以下連結中參照： [支援的通知型別表格](#supported-notification-types) 下文，其中提供應採取哪些動作的指引。

在「動作中心」中，您可以看到其他最近通知的清單。 建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，快顯視窗應該會提供解決問題所需的所有內容。 不過，如果Adobe支援有任何問題，您可以按一下 **聯絡支援人員** 快顯視窗中的連結。 這會顯示一個表格，您可以在其中說明問題並提交以建立支援票證，其中也會包含特定通知的參考，以便Adobe支援工程師具有相關內容。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/tw/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 哪些通知會出現？ {#which-notification}

AEMas a Cloud Service有數種通知，但「動作中心」中只會出現一個子集，如下表所示。

| 通知類型 | 說明 | 如何設定 | 顯示在警示中心 |
|---|---|---|---|
| 操作事件 | 需要立即採取行動的嚴重事件 | 指派給「事件通知 — Cloud Service」產品設定檔的使用者 | X |
| 主動建議 | 應該計劃的最佳化 | 指派給「主動通知 — Cloud Service」產品設定檔的使用者 | X |
| Cloud Manager 管道狀態 | 有關管道狀態的資訊 | 具有企業所有者、方案管理員或部署管理員角色的使用者，[Experience Cloud 偏好設定](https://experience.adobe.com/preferences)中的「其他」核取方塊已選取， as [在此說明](/help/implementing/cloud-manager/notifications.md). |  |

## 支援的通知類型 {#supported-notification-types}

下表列出「動作中心」目前支援的通知型別。

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---|---|---|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |

