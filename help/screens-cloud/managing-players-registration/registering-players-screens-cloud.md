---
title: 在螢幕中註冊播放器as a Cloud Service
description: 本頁說明如何在Screensas a Cloud Service註冊播放器。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: fb82970154fa37e3b3d1591a2e25989853ec6b90
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# 在螢幕中註冊播放器as a Cloud Service {#registering-players-screens-cloud}

在安裝並配置了Screensas a Cloud Service的播放器後，必須註冊播放器。

## 目標 {#objective}

本檔案可協助您了解在Screens服務提供者中註冊播放器。 閱讀後，您應該能夠：

* 了解如何註冊播放器
* 如何從Screens服務提供商完成註冊過程

## 註冊Screens播放器的步驟 {#register-players}

將播放器安裝到Screensas a Cloud Service後，即可從Screens服務提供商註冊您的播放器。

請依照下列步驟註冊您的播放器：

1. 登入Screens服務提供商。

1. 導覽至 **註冊代碼** 在 **播放器管理** 按一下左側導覽面板中的 **建立程式碼**.

   >[!NOTE]
   >如果不存在有效/未到期的代碼，請按一下「建立代碼」並輸入代碼名稱，然後根據您的要求選擇到期設定。

   ![影像](/help/screens-cloud/assets/player/register-player1.png)

1. 在中填入下列欄位 **建立註冊代碼** 對話框：

   ![影像](/help/screens-cloud/assets/player/register-player2.png)

   1. **註冊代碼名稱**:註冊代碼的名稱
   1. **註冊代碼過期**:註冊代碼的到期日
   1. **限制使用**:切換按鈕，關閉註冊代碼的使用限制。 依預設，「限制使用量」選項會關閉。
   1. **使用量限制**:選擇使用量限制的數字

1. 按一下 **建立** 來建立註冊代碼。 您會在清單中看到您的播放器包含註冊代碼。

   ![影像](/help/screens-cloud/assets/player/register-player3.png)

1. 按一下欄下方的值 **註冊代碼**  將值複製到剪貼簿。

1. 將此值貼入 **輸入代碼** 欄位 **播放器註冊** 標籤，然後按一下 **註冊**.

   ![影像](/help/screens-cloud/assets/player/register-player4.png)


1. 新增程式碼後，您就會看到播放器現在已從播放器的管理UI中註冊。

   ![影像](/help/screens-cloud/assets/player/register-player5.png)

1. 您應該會看到此播放器顯示於 **播放器** 從左側導覽面板。 Screens Services Provider中顯示的代碼與 **系統資訊** 從管理員UI的「播放器程式碼」下方取得面板。

   ![影像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**使用註冊代碼時的安全性最佳實務建議**
   >您可以限制註冊代碼的使用方式，這是最佳作法。 如果註冊代碼被洩露，但限制為100個註冊，則攻擊者只能註冊最多該號碼，但不能註冊更多。 在建立註冊代碼且客戶的某些播放器已註冊之後，您隨時可以更新使用限制。 如果客戶觀察到特定註冊代碼的異常註冊活動，則他們可以在調查時即時降低限制，如果是虛警，則可以增加數量，而不會影響已註冊的玩家。


## 下一步 {#whats-next}

現在，您已安裝播放器並將播放器設定為雲端模式，您應該繼續進行Screensas a Cloud Service歷程，方法是接下來檢閱檔案， [將播放器指派給螢幕中的顯示器as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) 從Screens服務提供商。
