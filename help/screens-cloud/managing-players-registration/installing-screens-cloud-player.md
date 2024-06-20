---
title: 在Screensas a Cloud Service中安裝和設定播放器
description: 本頁面說明如何在Screensas a Cloud Service安裝及設定播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# 在Screensas a Cloud Service中安裝和設定播放器 {#installing-players-screens-cloud}

本節說明如何安裝已註冊至內部部署AEM例項的AEM Screens播放器。 此外，您必須在工廠重設現有播放器，然後針對AEM Screensas a Cloud Service註冊新播放器。

## 目標 {#objective}

本檔案可協助您瞭解在註冊播放器之前如何設定播放器。 閱讀本檔案後，您應該能夠瞭解以下內容：

* 安裝播放器的位置
* 如何將播放器更新至雲端模式

## 將播放器設為雲端模式的步驟 {#cloud-mode-setup}

在您從下載最新的播放器後 [AEM Screens播放器下載](https://download.macromedia.com/screens/)，您現在已準備好將播放器更新至雲端模式。

請依照下列步驟更新您的播放器：

1. 開啟AEM Screens播放器。

   >[!NOTE]
   >您可以選擇使用專用的硬體裝置或您自己的播放器上的Web擴充功能進行測試。

1. 按一下 **設定** 標籤並按一下 **到工廠** 按鈕在 **重設** 選項。

   ![影像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 按一下 **確認** 以重設您的播放器。

1. 再次從 **設定** 標籤並按一下 **變更為雲端模式** 按鈕在 **切換執行模式** 選項。

   ![影像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 按一下 **確認** 在切換至雲端模式時提示取消註冊播放器的功能。

## 基本播放監視 {#playback-monitoring}

播放器會報告各種播放量度，每種 `ping` 預設為30秒。 根據這些量度，Adobe可以偵測各種邊緣情況，例如停滯體驗、空白畫面和排程問題。 此偵測可讓我們瞭解裝置的問題並進行疑難排解，因此可加快與您進行調查和採取修正措施。

AEM Screens播放器中的基本播放監視可讓我們：

* 遠端監視（如果播放器正確播放內容）。

* 改善對空白畫面或欄位中中斷體驗的反應能力。

* 減少向使用者顯示中斷體驗的風險。

### 瞭解屬性 {#understand-properties}

下列屬性包含在每個 `ping`：

| 屬性 | 說明 |
|---|---|
| id {string} | 播放器識別碼 |
| activeChannel {string} | 目前播放管道路徑，或若未排定任何專案，則為null |
| activeElements {string} | 以逗號分隔的字串，目前所有播放順序頻道中可見的元素（如果有多區域佈局，則為多個） |
| isDefaultContent {boolean} | 如果播放頻道被視為預設或遞補頻道（即優先順序為1且沒有排程），則為true |
| hasContentChange {boolean} | 如果內容在過去5分鐘內變更，則為true ；否則為false |
| lastContentChange {string} | 上次內容變更的時間戳記 |

>[!NOTE]
>或者，您也可以從播放器偏好設定中啟用更進階的屬性（啟用播放監視）：
>|屬性|說明|
>|—|—|
>|isContentRendering {boolean}|true，如果GPU可以確認它正在播放實際內容（根據畫素分析）|

### 限制 {#limitations}

基本播放監視的幾項限制列於下方：

* 播放器會向伺服器報告自己的播放狀態，因此需要使用中的連線。

* 此 `isContentRendering` 檢查GPU的屬性會過度消耗資源，預設為啟用，且需要播放器偏好設定中的明確選擇加入。 建議不要在生產環境中的影片中使用。

* 此功能僅支援序列頻道，尚未涵蓋互動式頻道(SPA)使用案例。

* 這些量度尚未完整開放給客戶；Adobe正在努力儘快啟用類似控制面板的報告和警報機制。

## 下一步 {#whats-next}

現在您已安裝播放器並將其設定為雲端模式，請繼續您的Screensas a Cloud Service歷程。 另請參閱 [在Screensas a Cloud Service註冊播放器](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 從Screens服務提供者。
