---
title: 在Screens中註冊播放器as a Cloud Service
description: 本頁面說明如何在Screens中註冊播放器as a Cloud Service。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# 在Screens中註冊播放器as a Cloud Service {#registering-players-screens-cloud}

安裝並設定Screensas a Cloud Service的播放器後，您必須註冊播放器。

## 目標 {#objective}

本檔案可協助您瞭解如何在Screens服務提供者中註冊播放器。 閱讀本檔案後，您應該能夠：

* 瞭解如何註冊玩家
* 如何從Screens服務提供者完成註冊程式

## 註冊Screens播放器的步驟 {#register-players}

將播放器安裝到Screens as a Cloud Service後，您就可以從Screens服務提供者註冊播放器了。

請依照下列步驟註冊您的播放器：

1. 登入Screens服務提供者。

1. 從左側導覽面板瀏覽至&#x200B;**播放器管理**&#x200B;下的&#x200B;**註冊代碼**，然後按一下&#x200B;**建立代碼**。

   >[!NOTE]
   >如果不存在有效的/未過期的代碼，請按一下「建立代碼」並輸入代碼的名稱，然後依您的要求選擇到期設定。

   ![影像](/help/screens-cloud/assets/player/register-player1.png)

1. 在&#x200B;**建立註冊代碼**&#x200B;對話方塊中填入下列欄位：

   ![影像](/help/screens-cloud/assets/player/register-player2.png)

   1. **註冊代碼名稱**：您的註冊代碼名稱
   1. **註冊代碼到期日**：您的註冊代碼到期日
   1. **限制使用量**：切換按鈕以關閉註冊代碼的使用量限制。 根據預設，「限制使用量」選項預設為關閉。
   1. **使用量限制**：選擇使用量限制的數字

1. 按一下&#x200B;**建立**&#x200B;以建立註冊代碼。 您可在清單中看到含有註冊碼的播放器。

   ![影像](/help/screens-cloud/assets/player/register-player3.png)

1. 按一下&#x200B;**註冊代碼**&#x200B;欄下的值，將該值複製到剪貼簿。

1. 從AEM Screens播放器的Admin UI中，將此值貼到&#x200B;**播放器註冊**&#x200B;索引標籤的&#x200B;**輸入代碼**&#x200B;欄位中，然後按一下&#x200B;**註冊**。

   ![影像](/help/screens-cloud/assets/player/register-player4.png)


1. 新增程式碼後，您可以看到播放器現在已從播放器的管理員UI註冊。

   ![影像](/help/screens-cloud/assets/player/register-player5.png)

1. 您應該會看到此播放器現在出現在左側導覽面板的&#x200B;**播放器**&#x200B;中。 Screens服務提供者中顯示的程式碼符合「播放器程式碼」下管理UI中的&#x200B;**系統資訊**&#x200B;面板。

   ![影像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >使用註冊代碼時&#x200B;**安全性最佳實務建議**
   >作為最佳實務，您可以限制註冊代碼的使用。如果註冊代碼被洩露，但註冊次數限制為 100 次，則攻擊者最多只能註冊該數量而不是更多。在建立註冊代碼並且部分客戶的播放器已經註冊後，您可以隨時更新使用限制。如果客戶發現特定註冊代碼有異常註冊活動，他們可以在調查時即時降低限制，並且如果這是誤報，還可以增加數量，而不會影響已註冊的玩家。


## 下一步 {#whats-next}

現在，您已安裝播放器並將其設定為雲端模式，接下來應該檢閱檔案[從Screens服務提供者將播放器指派給Screensas a Cloud Service中的顯示](/help/screens-cloud/managing-players-registration/assigning-player-display.md)，以繼續您的Screensas a Cloud Service歷程。
