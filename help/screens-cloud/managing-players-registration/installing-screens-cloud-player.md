---
title: 在螢幕中安裝和設定播放器作為Cloud Service
description: 本頁面說明如何在Screens中安裝和設定播放器，作為Cloud Service。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '270'
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

## 下一步 {#whats-next}

現在，您已安裝播放器並將播放器設定為雲端模式，您應該繼續以Cloud Service的形式來執行Screens歷程，方法是接下來檢閱檔案[從Screens服務提供者將Screens中的播放器註冊為Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)。