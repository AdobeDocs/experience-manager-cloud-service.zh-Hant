---
title: 為螢幕中的顯示指定通道as a Cloud Service
description: 本頁介紹如何在螢幕as a Cloud Service中為顯示指定通道。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# 為螢幕中的顯示指定通道as a Cloud Service {#assign-channel-displays-screens-cloud}

項目設定完成後，必須將頻道分配給顯示器才能查看內容。

## 目標 {#objective}

此文檔可幫助您瞭解如何在顯示器準備就緒後將頻道分配給顯示器，並將內容添加到頻道並發佈。 閱讀後，您應該能夠瞭解如何從螢幕服務提供商為顯示器分配通道。

## 必備條件 {#prerequisites}

在執行以下步驟將通道分配給顯示器之前，必須完成學習：

* 建立和管理顯示
* 建立和管理渠道

## 為顯示器指定通道的步驟 {#assign-channel-to-display}

按照以下步驟為顯示器分配通道：

1. 導航到螢幕服務提供程式並選擇 **顯示** 的下界。

1. 按一下 **分配通道** 到

   ![影像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 填充以下欄位 **分配通道** 對話框。

   ![影像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 從下拉清單中選擇通道名稱。
   1. 選擇優先順序。

      >[!NOTE]
      >優先順序用於在多個分配匹配播放條件時對分配進行排序。 值最高的值總是優先於值較低的值。 例如，如果有兩個通道A和B。A的優先順序為1,B的優先順序為2，然後顯示通道B，因為它的優先順序高於A。
   1. 選擇開始日期和結束日期 **激活**。

1. 按一下 **+添加重複** 添加頻道的定期計畫。

   ![影像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以向您的渠道添加多個循環計畫。 定期計畫引入了「日分」，它允許您設定一個全局計畫，其中多個通道在一天中的特定時間運行，並同時將該設定重新用於所有顯示。

   可以設定以下選項：

   * **名稱**:定期計畫的標題。
   * **重複**:選擇計畫是運行「每日」、「每週」、「每月」還是「每年」。
   * **開始**:計畫的開始時間。
   * **結束**:計畫的結束時間。 可以按時間或持續時間設定。
   * **時間**:計畫將在指定時間結束。
   * **持續時間**:計畫以小時或分鐘為特定持續時間運行。

1. 按一下 **建立** 現在，您將看到為該顯示指定了通道，如下圖所示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步是什麼 {#whats-next}

現在，您已將頻道分配給顯示器，您應通過下一步查看文檔來繼續「螢幕」as a Cloud Service行程 [安裝和配置用於AEMas a Cloud Service的Screens Player](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md)。
