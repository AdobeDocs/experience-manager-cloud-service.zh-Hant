---
title: 通知中心
description: 利用通知中心可輕鬆對事件和其他重要資訊採取行動
hidefromtoc: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: b72d22e8788c04ab4faa3616a4a0ce5e6d8ce991
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 36%

---

# 通知中心 {#notification-center}

>[!NOTE]
>此功能尚未推出。

AEM as Cloud Service會在發生需要立即行動的重大事件時傳送通知，並針對最佳化提出主動建議。 例如，已封鎖的佇列或即將到期的憑證集；您可以在 [下表](#supported-notification-types)，會隨著時間而擴展。

這些通知可設定為透過電子郵件和通知介面工具集(按一下Adobe Experience Cloud右上角的鈴聲圖示即可存取)下方的接收。

收到通知時，您可以按一下通知，開啟AEMas a Cloud Service的通知中心，彈出式視窗顯示說明客戶所採取動作的其他內容。

除了顯示關於點按通知的資訊外，通知中心還作為中心，您可以在其中查看和管理當前和舊通知集。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知中心中會顯示兩個高階通知類別：

1. 操作事件 — 已發生事件，通常需要迅速解決。 例如，解析鎖定的佇列.
1. 主動建議 — Adobe有建議，建議客戶在不久的將來應採取的動作。 例如，停止參考已棄用的 UI。

請參閱[下表](#supported-notification-types)了解目前支援的通知。

從通知中心，您可以選擇特定的程式和環境，這將對該範圍進行篩選。

## 設定 {#configuration}

請依照下列步驟配置接收通知：

1. 建立下列產品設定檔，如所述 [本文](/help/journey-onboarding/notification-profiles.md)，也會從您的組織將適當的AdobeID指派給這些設定檔。 這可讓管理員判斷哪些使用者有資格接收這些通知。
1. 在上一步驟中指派的每個指派使用者都可設定如何接收通知。 在 [Experience Cloud偏好設定頁面](https://experience.adobe.com/preferences/notification-section)，確定Experience Manager訂閱已啟用，且 **業務事件** 和 **主動建議** 複選框被選中。 此外，建議將「電子郵件」區段設為 **即時通知** 因此，在發生事件時，會立即收到通知。

>[!NOTE]
>通知可在組織層級運作，因此訂閱者將會收到這些方案中所有方案和環境的通知。

## 詳細的使用者流程 {#detailed-user-flow}

點擊電子郵件會將您帶到通知中心，快顯視窗會顯示您點擊的通知內容，在某些情況下，還會顯示說明如何採取糾正措施的其他資訊連結。

![事件詳細資料](/help/operations/assets/incident-details.png)

點擊&#x200B;**了解更多**&#x200B;連結可將使用者導覽至本文，下表可參考其中的通知，其提供採取何種動作的指導。

在通知中心，您可以看到其他最近通知的清單。建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，通知應提供解決問題的所有必要內容。但是，如果對 Adobe 支援有疑問，您可以點擊通知快顯視窗中的&#x200B;**聯絡支援人員**&#x200B;連結。這將顯示一個表單，您可以在其中描述問題並提交它以建立支援票證，該表單還包括對特定通知的引用，以便Adobe支援工程師具有相關上下文。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 會出現哪些通知？ {#which-notification}

AEMas a Cloud Service有數種通知，但只有子集會出現在通知中心，如下表所示。

| 通知類型 | 說明 | 如何配置 | 顯示在通知中心 |
|---|---|---|---|
| 業務事件 | 需要立即採取行動的重大事件 | 分配給「事件通知 — Cloud Service」產品配置檔案的用戶，在 [Experience Cloud偏好設定](https://experience.adobe.com/preferences) | X |
| 主動建議 | 應計畫的最佳化 | 指派給「主動通知 — Cloud Service」產品設定檔的使用者，在 [Experience Cloud偏好設定](https://experience.adobe.com/preferences) | X |
| Cloud Manager管道狀態 | 管道狀態的相關資訊 | 具有業務所有者、計畫經理或部署經理角色的用戶，在 [Experience Cloud偏好設定](https://experience.adobe.com/preferences) |  |

## 支援的通知類型 {#supported-notification-types}

下表列出目前支援的通知類型。

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---|---|---|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |

