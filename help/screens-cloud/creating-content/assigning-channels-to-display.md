---
title: 為螢幕中的顯示指派頻道as a Cloud Service
description: 本頁說明如何將頻道指派給螢幕中的顯示器，as a Cloud Service。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# 為螢幕中的顯示指派頻道as a Cloud Service {#assign-channel-displays-screens-cloud}

專案設定完成後，您必須將頻道指派給顯示器以檢視內容。

## 目標 {#objective}

本檔案可協助您了解當您的顯示準備就緒且已新增內容至頻道並發佈後，如何將頻道指派給顯示器。 閱讀後，您應該能了解如何從Screens服務提供者將頻道指派給顯示器。

## 必備條件 {#prerequisites}

在執行下列步驟以將管道指派給顯示器之前，您必須已完成學習：

* 建立和管理顯示
* 建立和管理管道

## 將管道指派給顯示器的步驟 {#assign-channel-to-display}

請依照下列步驟，將管道指派給顯示器：

1. 導覽至Screens Services Provider並選取 **顯示** 從左側導覽面板。

1. 按一下 **指派管道** 顯示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 填入下列欄位，從 **指派管道** 對話框。

   ![影像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 從下拉式清單中選取管道名稱。
   1. 選擇優先順序。

      >[!NOTE]
      >優先順序可用來排序指派，以備多個指派符合播放條件時使用。 值最高的一律優先於值較低的。 例如，如果有兩個管道A和B。A的優先順序為1,B的優先順序為2，則顯示管道B，因為其優先順序高於A。
   1. 選擇開始日期和結束日期 **啟動**.

1. 按一下 **+新增週期** 新增管道的週期排程。

   ![影像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以新增多個循環排程至管道。 週期排程引入了DayParting，可讓您設定具有在一天中特定時間執行之多個管道的全域排程，並一次對所有顯示器重複使用該設定。

   您可以設定下列選項：

   * **名稱**:定期排程的標題。
   * **重複**:選擇排程是執行每日、每週、每月或每年。
   * **開始**:排程的開始時間。
   * **結束**:排程的結束時間。 您可以依時間或持續時間來設定。
   * **時間**:排程將在指定時間結束。
   * **持續時間**:排程會以小時或分鐘為單位，執行特定時段。

1. 按一下 **建立** 現在，您會看到已為該顯示指派管道，如下圖所示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步 {#whats-next}

現在，您已將管道指派給顯示器，您應繼續進行Screensas a Cloud Service歷程，方法是接下來檢閱檔案 [安裝和設定AEMas a Cloud Service的Screens Player](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
