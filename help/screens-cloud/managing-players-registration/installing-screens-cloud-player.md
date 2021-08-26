---
title: 在螢幕中安裝和設定播放器作為Cloud Service
description: 本頁面說明如何在Screens中安裝和設定播放器，作為Cloud Service。
source-git-commit: 6afb71803ae24bed2d5d5662a7cdd4af5637e329
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# 在螢幕中安裝和設定播放器作為Cloud Service {#installing-players-screens-cloud}

本節說明如何安裝已註冊至內部部署AEM例項的AEM Screens播放器。 此外，您必須對現有播放器進行工廠重設，然後針對AEM Screens註冊新播放器作為Cloud Service。

## 目標 {#objective}

本檔案可協助您了解如何先設定播放器，再註冊播放器。 讀完書後，你應該能夠理解：

* 從何處安裝播放器
* 如何將播放器更新為雲端模式

## 將播放器設為雲端模式的步驟 {#cloud-mode-setup}

從[AEM Screens播放器下載](https://download.macromedia.com/screens/)下載最新播放器後，您就可以將播放器更新為雲端模式。

請依照下列步驟更新您的播放器：

1. 開啟AEM Screens播放器。

   >[!NOTE]
   >您可以選擇使用專用硬體裝置或在您自己的播放器上使用網頁擴充功能進行測試。

1. 按一下&#x200B;**Configuration**&#x200B;頁簽，然後按一下&#x200B;**Reset**&#x200B;選項下的&#x200B;**To Factory**&#x200B;按鈕。

   ![影像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 按一下&#x200B;**Confirm**&#x200B;以重設您的播放器。

1. 再次從&#x200B;**Configuration**&#x200B;標籤中，按一下&#x200B;**Toggle Runmode**&#x200B;選項下的&#x200B;**Change to Cloud Mode**&#x200B;按鈕。

   ![影像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 按一下&#x200B;**確認**，當切換至雲端模式時，系統會提示取消註冊播放器。

## 基本播放監控 {#playback-monitoring}

播放器會報告各種播放量度，每個`ping`預設為30秒。 您可以根據量度偵測各種邊緣案例，例如體驗停滯、空白畫面和排程問題。 這可讓您了解和疑難排解裝置上的問題，進而加速調查和修正措施。

AEM Screens播放器中的基本播放監控可讓您：

* 遠程監視播放器是否正確播放內容

* 改善欄位中空白畫面或中斷體驗的再活動性

* 降低向使用者顯示中斷體驗的風險

### 了解屬性 {#understand-properties}

每個`ping`中都包含下列屬性：

| 屬性 | 說明 |
|---|---|
| id {string} | 播放器識別碼 |
| activeChannel {string} | 當前正在播放通道路徑；如果未計畫任何內容，則為null |
| activeElements {string} | 逗號分隔字串，所有播放序列頻道中目前可見的元素（若為多區域版面，則為多個元素） |
| isDefaultContent {boolean} | 如果播放管道被視為預設或後援管道，則為true（亦即，優先順序1且無排程） |
| hasContentChanged {boolean} | 如果內容在過去5分鐘內變更，則為true；否則為false |
| lastContentChange {string} | 上次內容變更的時間戳記 |

>[!NOTE]
>您可以選擇從播放器偏好設定（啟用播放監控）啟用更進階的屬性，這是：
>|屬性|說明|
>|—|—|
>如果GPU可確認其正在播放實際內容（基於像素分析），則|isContentRendering {boolean}|true


## 下一步 {#whats-next}

現在，您已安裝播放器並將播放器設定為雲端模式，您應該繼續以Cloud Service的形式來執行Screens歷程，方法是接下來檢閱檔案[從Screens服務提供者將Screens中的播放器註冊為Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)。