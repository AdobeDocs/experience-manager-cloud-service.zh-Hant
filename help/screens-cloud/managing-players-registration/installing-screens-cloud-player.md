---
title: 在螢幕中安裝和配置播放器as a Cloud Service
description: 本頁面說明如何在Screensas a Cloud Service安裝和設定播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# 在螢幕中安裝和配置播放器as a Cloud Service {#installing-players-screens-cloud}

本節說明如何安裝已註冊至內部部署AEM例項的AEM Screens播放器。 此外，您必須對現有播放器進行工廠重設，然後針對AEM Screensas a Cloud Service註冊新播放器。

## 目標 {#objective}

本檔案可協助您了解如何先設定播放器，再註冊播放器。 讀完書後，你應該能夠理解：

* 從何處安裝播放器
* 如何將播放器更新為雲端模式

## 將播放器設為雲端模式的步驟 {#cloud-mode-setup}

從下載最新播放器後 [AEM Screens播放器下載](https://download.macromedia.com/screens/)，您現在可以將播放器更新為雲端模式。

請依照下列步驟更新您的播放器：

1. 開啟AEM Screens播放器。

   >[!NOTE]
   >您可以選擇使用專用硬體裝置或在您自己的播放器上使用網頁擴充功能進行測試。

1. 按一下 **設定** 標籤，然後按一下 **到工廠** 按鈕 **重設** 選項。

   ![影像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 按一下 **確認** 重設播放器。

1. 再次從 **設定** 標籤，然後按一下 **變更為雲端模式** 按鈕 **切換執行模式** 選項。

   ![影像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 按一下 **確認** 切換至雲端模式時，系統會提示取消註冊播放器。

## 基本播放監控 {#playback-monitoring}

播放器會報告各自的各種播放量度 `ping` 預設為30秒。 根據這些量度，我們可以偵測各種邊緣案例，例如體驗停滯、空白畫面和排程問題。 這可讓我們了解和疑難排解裝置上的問題，進而加速與您一起進行調查和採取糾正措施。

AEM Screens播放器中的基本播放監控可讓我們：

* 如果播放器正確播放內容，則遠程監視。

* 改善欄位中空白畫面或體驗損毀的反應性。

* 降低向使用者顯示中斷體驗的風險。

### 了解屬性 {#understand-properties}

每個 `ping`:

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

### 限制 {#limitations}

以下列出基本播放監控的幾項限制：

* 播放器會向伺服器報告自己的播放狀態，因此需要使用中的連線。

* 此 `isContentRendering` 檢查GPU的屬性當前佔用的資源太多，預設情況下無法啟用，並且需要從播放器首選項中明確選擇加入。 建議您不要將其與生產中的影片搭配使用。

* 此功能僅支援序列管道，不涵蓋互動式管道(SPA)使用案例。

* 這些量度尚未完全公開給客戶，我們正在努力在不久的將來啟用類似控制面板的報表和警報機制。

## 下一步 {#whats-next}

現在，您已安裝播放器並將播放器設定為雲端模式，您應該繼續進行Screensas a Cloud Service歷程，方法是接下來檢閱檔案， [在螢幕中註冊播放器as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 從Screens服務提供商。
