---
title: 在螢幕中註冊玩家as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中註冊玩家。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: fb82970154fa37e3b3d1591a2e25989853ec6b90
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# 在螢幕中註冊玩家as a Cloud Service {#registering-players-screens-cloud}

安裝並配置了螢幕as a Cloud Service的播放器後，必須註冊播放器。

## 目標 {#objective}

此文檔幫助您瞭解在螢幕服務提供商中註冊玩家。 閱讀後，您應能：

* 瞭解如何註冊玩家
* 如何從螢幕服務提供程式完成註冊過程

## 註冊螢幕播放器的步驟 {#register-players}

將播放器安裝到螢幕as a Cloud Service後，您就可以從螢幕服務提供商註冊播放器。

按照以下步驟註冊您的播放器：

1. 登錄到螢幕服務提供程式。

1. 導航到 **註冊代碼** 在 **玩家管理** 從左導航面板中，按一下 **建立代碼**。

   >[!NOTE]
   >如果沒有有效/未到期的代碼，請按一下建立代碼並輸入代碼名稱，然後根據您的要求選擇到期設定。

   ![影像](/help/screens-cloud/assets/player/register-player1.png)

1. 在中填充以下欄位 **建立註冊代碼** 對話框：

   ![影像](/help/screens-cloud/assets/player/register-player2.png)

   1. **註冊代碼名稱**:註冊代碼的名稱
   1. **註冊代碼到期**:註冊代碼的到期日
   1. **限制使用**:切換按鈕以關閉註冊代碼的使用限制。 預設情況下，「限制使用」選項處於關閉狀態。
   1. **使用限制**:選擇用量限制的編號

1. 按一下 **建立** 的子菜單。 您將在清單中看到您的播放器的註冊代碼。

   ![影像](/help/screens-cloud/assets/player/register-player3.png)

1. 按一下列下的值 **註冊代碼**  將值複製到剪貼簿。

1. 將此值貼上到 **輸入代碼** 的 **玩家註冊** 頁籤，然後按一下 **註冊**。

   ![影像](/help/screens-cloud/assets/player/register-player4.png)


1. 添加代碼後，您將看到播放器現在從播放器的管理UI中註冊。

   ![影像](/help/screens-cloud/assets/player/register-player5.png)

1. 你應該看到這個玩家 **球員** 的下界。 螢幕服務提供程式中顯示的代碼與 **系統資訊** 從Admin UI的「Player Code（播放器代碼）」下面的面板。

   ![影像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**使用註冊代碼時的安全最佳實踐建議**
   >作為最佳做法，您可以限制註冊代碼的使用。 如果註冊代碼被洩露，但註冊限制為100個，則攻擊者最多只能註冊該號碼，但不能註冊更多。 在建立註冊代碼並且客戶的某些玩家已經註冊後，您始終可以更新使用限制。 如果客戶發現特定註冊代碼的註冊活動異常，他們可以在調查時即時降低限制，如果是虛警，則可以增加返回數量，而不會影響已註冊的玩家。


## 下一步是什麼 {#whats-next}

現在，您已將播放器安裝並配置為雲模式，您應通過下一步查看文檔來繼續螢幕as a Cloud Service之旅， [為螢幕中的顯示器分配播放器as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) 從螢幕服務提供程式。
