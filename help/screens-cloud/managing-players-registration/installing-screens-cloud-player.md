---
title: 在螢幕中安裝和配置播放器as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中安裝和配置播放器。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# 在螢幕中安裝和配置播放器as a Cloud Service {#installing-players-screens-cloud}

本節介紹如何安裝註冊到內部實例的AEM Screens玩AEM家。 此外，您必須對現有播放器進行出廠重置，然後針對AEM Screensas a Cloud Service註冊新播放器。

## 目標 {#objective}

此文檔可幫助您瞭解如何在註冊玩家之前設定播放器。 讀完後，您應該能夠理解：

* 從何處安裝播放器
* 如何將播放器更新為雲模式

## 將播放器設定為雲模式的步驟 {#cloud-mode-setup}

從下載最新播放器後 [AEM Screens播放器下載](https://download.macromedia.com/screens/)現在，您已準備好將播放器更新為雲模式。

按照以下步驟更新您的播放器：

1. 開啟AEM Screens球員。

   >[!NOTE]
   >您可以選擇與專用硬體設備test，或在自己的播放器上使用Web擴展。

1. 按一下 **配置** 按鈕 **到工廠** 按鈕 **重置** 的雙曲餘切值。

   ![影像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 按一下 **確認** 來重置玩家。

1. 從 **配置** 按鈕 **更改為雲模式** 按鈕 **切換運行模式** 的雙曲餘切值。

   ![影像](/help/screens-cloud/assets/player/installplayer-1.png)

1. 按一下 **確認** 將取消註冊播放器。

## 基本播放監視 {#playback-monitoring}

播放器報告各個播放度量 `ping` 預設為30秒。 基於這些指標，我們可以檢測各種邊緣情況，如停滯體驗、空白螢幕和調度問題。 這樣，我們便能瞭解和排除設備上的問題，從而加快您的調查和糾正措施。

在AEM Screens播放器中進行基本播放監視，可以：

* 如果播放器正在正確播放內容，則遠程監視。

* 提高對空白螢幕或現場破壞經驗的反應性。

* 降低向最終用戶顯示中斷體驗的風險。

### 瞭解屬性 {#understand-properties}

以下屬性包括在 `ping`:

| 屬性 | 說明 |
|---|---|
| id {string} | 播放器標識符 |
| activeChannel {string} | 當前正在播放通道路徑，如果未計畫任何內容，則為空 |
| activeElements {string} | 逗號分隔的字串，當前所有播放序列通道中的可見元素（多區域佈局時為多個） |
| isDefaultContent {boolean} | 如果播放頻道被視為預設或回退頻道（即優先順序為1且無計畫），則為true |
| 有ContentChanged {boolean} | 如果內容在過去5分鐘內更改為true，否則為false |
| lastContentChange {string} | 上次內容更改的時間戳 |

>[!NOTE]
>可選地，可以從播放器首選項（啟用回放監視）啟用更高級的屬性，即：
>|屬性|說明|
>|—|
>如果GPU能確認其正在播放實際內容（基於像素分析），則|isContentRendering {boolean}|true

### 限制 {#limitations}

下面列出了基本播放監視的幾個限制：

* 播放器向伺服器報告自己的播放狀態，因此需要活動連接。

* 的 `isContentRendering` 檢查GPU的屬性當前資源過於密集，預設情況下無法啟用，並且需要從播放器首選項中明確選擇加入。 建議不要將其與視頻一起用於製作。

* 此功能僅支援序列通道，尚不涵蓋交互通道(SPA)使用情形。

* 這些指標尚未完全向客戶公開，我們正在努力在不久的將來啟用類似於儀表板的報告和警報機制。

## 下一步是什麼 {#whats-next}

現在，您已將播放器安裝並配置為雲模式，您應通過下一步查看文檔來繼續螢幕as a Cloud Service之旅， [在螢幕中註冊玩家as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) 從螢幕服務提供程式。
