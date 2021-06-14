---
title: 將頻道指派給螢幕中的顯示作為Cloud Service
description: 本頁說明如何將頻道指派給Screens中的顯示器，作為Cloud Service。
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# 將通道指派給螢幕中的顯示，作為Cloud Service{#assign-channel-displays-screens-cloud}

專案設定完成後，您必須將頻道指派給顯示器以檢視內容。

## 目標 {#objective}

本檔案可協助您了解當您的顯示準備就緒且已新增內容至頻道並發佈後，如何將頻道指派給顯示器。 閱讀後，您應該能了解如何從Screens服務提供者將頻道指派給顯示器。

## 必備條件 {#prerequisites}

在執行下列步驟以將管道指派給顯示器之前，您必須已完成學習：

* 建立和管理顯示
* 建立和管理管道

## 將通道分配給顯示器的步驟{#assign-channel-to-display}

請依照下列步驟，將管道指派給顯示器：

1. 導航至Screens Services Provider，並從左側導航面板中選擇&#x200B;**Displays**。

1. 按一下「**指定通道**」以顯示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 從&#x200B;**Assign a channel**&#x200B;對話方塊填入下列欄位。

   ![影像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 從下拉式清單中選取管道名稱。
   1. 選擇優先順序。

      >[!NOTE]
      >優先順序可用來排序指派，以備多個指派符合播放條件時使用。 值最高的一律優先於值較低的。 例如，如果有兩個管道A和B。A的優先順序為1,B的優先順序為2，則顯示管道B，因為其優先順序高於A。
   1. 從&#x200B;**Activation**&#x200B;中選擇開始日期和結束日期。

1. 按一下&#x200B;**+新增循環**&#x200B;以新增通道的循環排程。

   ![影像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以新增多個循環排程至管道。 週期排程引入了DayParting，可讓您設定具有在一天中特定時間執行之多個管道的全域排程，並一次對所有顯示器重複使用該設定。

   您可以設定下列選項：

   * **名稱**:定期排程的標題。
   * **重複**:選擇排程是執行每日、每週、每月或每年。
   * **開始**:排程的開始時間。
   * **結束**:排程的結束時間。您可以依時間或持續時間來設定。
   * **時間**:排程將在指定時間結束。
   * **持續時間**:排程會以小時或分鐘為單位，執行特定時段。

1. 按一下&#x200B;**建立**，現在您會看到已為該顯示指派通道，如下圖所示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步是什麼{#whats-next}

現在，您已將頻道指派給顯示器後，您應繼續以Cloud Service的形式來執行Screens歷程，方法是先檢閱檔案&#x200B;**安裝並設定AEM適用的Screens播放器作為Cloud Service**。
