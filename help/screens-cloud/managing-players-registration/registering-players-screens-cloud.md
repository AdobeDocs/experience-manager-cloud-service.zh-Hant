---
title: 在螢幕中將播放器註冊為Cloud Service
description: 本頁說明如何在Screens中將播放器註冊為Cloud Service。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 在螢幕中將播放器註冊為Cloud Service {#registering-players-screens-cloud}

在您為Screens安裝並配置了Cloud Service後，必須註冊播放器。

## 目標 {#objective}

本檔案可協助您了解在Screens服務提供者中註冊播放器。 閱讀後，您應該能夠：

* 了解如何註冊播放器
* 如何從Screens服務提供商完成註冊過程

## 註冊Screens播放器的步驟 {#register-players}

在您將播放器以Cloud Service的形式安裝到Screens後，即可從Screens服務提供商註冊您的播放器。

請依照下列步驟註冊您的播放器：

1. 登入Screens服務提供商。

1. 從左側導覽面板導覽至&#x200B;**播放器管理**&#x200B;下的&#x200B;**註冊代碼**，然後按一下&#x200B;**建立代碼**。

   >[!NOTE]
   >如果不存在有效/未到期的代碼，請按一下「建立代碼」並輸入代碼名稱，然後根據您的要求選擇到期設定。

   ![影像](/help/screens-cloud/assets/player/register-player1.png)

1. 在&#x200B;**建立註冊代碼**&#x200B;對話框中填入以下欄位：

   ![影像](/help/screens-cloud/assets/player/register-player2.png)

   1. **註冊代碼名稱**:註冊代碼的名稱
   1. **註冊代碼過期**:註冊代碼的到期日
   1. **限制用途**:切換按鈕，關閉註冊代碼的使用限制。依預設，「限制使用量」選項會關閉。
   1. **使用量限制**:選擇使用量限制的數字

1. 按一下&#x200B;**Create**&#x200B;以建立註冊代碼。 您會在清單中看到您的播放器包含註冊代碼。

   ![影像](/help/screens-cloud/assets/player/register-player3.png)

1. 按一下列&#x200B;**REGISTRATION CODE**&#x200B;下的值，將值複製到剪貼簿。

1. 將此值貼到AEM Screens播放器管理員UI的&#x200B;**播放器註冊**&#x200B;標籤的&#x200B;**輸入代碼**&#x200B;欄位中，然後按一下&#x200B;**註冊**。

   ![影像](/help/screens-cloud/assets/player/register-player4.png)


1. 新增程式碼後，您就會看到播放器現在已從播放器的管理UI中註冊。

   ![影像](/help/screens-cloud/assets/player/register-player5.png)

1. 您應該會從左側導覽面板看到此播放器現在顯示在&#x200B;**播放器**&#x200B;中。 螢幕服務提供者中顯示的程式碼會符合「播放器程式碼」下管理UI的&#x200B;**系統資訊**&#x200B;面板。

   ![影像](/help/screens-cloud/assets/player/register-player6.png)

## 下一步 {#whats-next}

現在，您已安裝播放器並將播放器設定為雲端模式，您應該繼續以Cloud Service的形式來執行Screens歷程，方法是接下來檢閱檔案[從Screens服務提供者將播放器指派給Screens中的顯示器作為Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md)。