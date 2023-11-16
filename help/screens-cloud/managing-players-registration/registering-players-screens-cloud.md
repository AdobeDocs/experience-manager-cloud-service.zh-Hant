---
title: 在Screensas a Cloud Service註冊播放器
description: 本頁面說明如何在Screensas a Cloud Service中註冊播放器。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 在Screensas a Cloud Service註冊播放器 {#registering-players-screens-cloud}

安裝並設定Screensas a Cloud Service的播放器後，您必須註冊播放器。

## 目標 {#objective}

本檔案可協助您瞭解如何在Screens服務提供者中註冊播放器。 閱讀本檔案後，您應該能夠：

* 瞭解如何註冊玩家
* 如何從Screens服務提供者完成註冊程式

## 註冊Screens播放器的步驟 {#register-players}

將播放器安裝到Screensas a Cloud Service後，您就可以從Screens服務提供者註冊播放器了。

請依照下列步驟註冊您的播放器：

1. 登入Screens服務提供者。

1. 瀏覽至 **註冊代碼** 在 **播放器管理** 從左側導覽面板，然後按一下 **建立程式碼**.

   >[!NOTE]
   >如果不存在有效的/未過期的代碼，請按一下「建立代碼」並輸入代碼的名稱，然後依您的要求選擇到期設定。

   ![影像](/help/screens-cloud/assets/player/register-player1.png)

1. 將下列欄位填入 **建立註冊代碼** 對話方塊：

   ![影像](/help/screens-cloud/assets/player/register-player2.png)

   1. **註冊代碼名稱**：註冊代碼的名稱
   1. **註冊代碼有效期**：您的註冊代碼到期日
   1. **限制使用量**：切換按鈕，以關閉註冊代碼的使用量限制。 根據預設，「限制使用量」選項預設為關閉。
   1. **使用量限制**：選擇使用量限制的數字

1. 按一下 **建立** 以建立註冊代碼。 您可在清單中看到含有註冊碼的播放器。

   ![影像](/help/screens-cloud/assets/player/register-player3.png)

1. 按一下欄下的值 **註冊代碼**  將值複製到剪貼簿。

1. 將此值貼入 **輸入代碼** 中的欄位 **播放器註冊** 標籤從AEM Screens播放器的管理員UI開啟，然後按一下 **註冊**.

   ![影像](/help/screens-cloud/assets/player/register-player4.png)


1. 新增程式碼後，您可以看到播放器現在已從播放器的管理員UI註冊。

   ![影像](/help/screens-cloud/assets/player/register-player5.png)

1. 您應該會看到此播放器現在顯示於 **Players** 從左側導覽面板。 Screens服務提供者中顯示的程式碼會符合 **系統資訊** 面板，從「管理員UI」的「播放器代碼」下方。

   ![影像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**使用註冊代碼時的安全性最佳實務建議**
   >最佳做法是限制註冊代碼的使用方式。 如果註冊碼遭到破壞，但限製為100個註冊，則攻擊者最多只能註冊該號碼，但不能註冊更多號碼。 建立註冊代碼並註冊部分客戶播放器後，您隨時都可以更新使用量限制。 如果客戶發現特定註冊代碼有異常註冊活動，他們可以在調查時即時降低限制，並且如果這是誤報，還可以增加數量，而不會影響已註冊的玩家。


## 下一步 {#whats-next}

現在，您已安裝播放器並將其設定為雲端模式，接下來應該檢閱檔案以繼續Screensas a Cloud Service歷程， [將播放器指派給Screens中的as a Cloud Service顯示](/help/screens-cloud/managing-players-registration/assigning-player-display.md) 從Screens服務提供者。
