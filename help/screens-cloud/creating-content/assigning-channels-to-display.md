---
title: 將頻道指派給Screens中的顯示區as a Cloud Service
description: 本頁面說明如何將頻道指派給Screens中的as a Cloud Service顯示區。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# 將頻道指派給Screens中的顯示區as a Cloud Service {#assign-channel-displays-screens-cloud}

專案設定完成後，您必須將頻道指派給顯示區，以便檢視內容。

## 目標 {#objective}

本檔案可協助您瞭解如何在顯示準備就緒且已新增內容至頻道並發佈後，將頻道指派給顯示。 閱讀本檔案後，您應該能夠瞭解如何從Screens服務提供者將頻道指派給顯示器。

## 先決條件 {#prerequisites}

您必須完成下列步驟，才能將頻道指派給顯示區：

* 建立和管理顯示器
* 建立和管理管道

## 指派頻道給顯示的步驟 {#assign-channel-to-display}

請依照下列步驟，將頻道指派給顯示器：

1. 導覽至Screens服務提供者，然後從左側導覽面板中選取&#x200B;**顯示器**。

1. 按一下&#x200B;**指派頻道**&#x200B;給顯示區。

   ![影像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. 從&#x200B;**指派管道**&#x200B;對話方塊填入下列欄位。

   ![影像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. 從下拉式清單中選取管道名稱。
   1. 選擇優先順序。

      >[!NOTE]
      >當有多個指派符合播放條件時，優先順序可用於排序指派。 值最高的總是優先於較低的值。 例如，如果有兩個管道A和B。A的優先順序為1，而B的優先順序為2，則會顯示管道B，因為其優先順序高於A。

   1. 從&#x200B;**啟用**&#x200B;選取開始日期和結束日期。

1. 按一下「**+新增週期**」為您的頻道新增週期排程。

   ![影像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >您可以將多個週期性排程新增到您的頻道。 遞回排程會引入DayParting，讓您設定在特定時間執行多個管道的全域排程，並重複使用一次針對所有顯示設定的排程。

   您可以設定下列選項：

   * **名稱**：您的週期性排程表標題。
   * **重複**：選擇排程是每日、每週、每月還是每年執行。
   * **開始**：排程的開始時間。
   * **結束**：排程的結束時間。 您可以依時間或持續時間進行設定。
   * **時間**：排程在指定的時間結束。
   * **期間**：排程會以小時或分鐘為單位在特定期間內執行。

1. 按一下「**建立**」。您可以看到已為該顯示指派管道，如下圖所示。

   ![影像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 下一步 {#whats-next}

現在您已指派頻道給顯示區，接下來應該檢閱檔案[安裝和設定AEM as a Cloud Service的Screens Player &#x200B;](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md)，以繼續您的Screensas a Cloud Service歷程。
