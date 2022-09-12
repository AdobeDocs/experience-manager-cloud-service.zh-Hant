---
title: 建立生產計畫
description: 了解如何使用Cloud Manager建立您自己的生產程式來托管即時流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 3557ddbc76ff21bcfe4ac0338f116b02b5135f2c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# 建立生產計畫 {#create-production-program}

生產計畫是專為熟悉AEM和Cloud Manager且準備好開始編寫、建立和測試程式碼，以將程式碼部署至托管即時流量的使用者而設計。

進一步了解檔案中的方案類型 [了解方案和方案類型。](program-types.md)

## 視訊Tutorials {#video-tutorials}

您可以觀看這兩個教學課程影片，了解如何在Cloud Manager中建立方案，或 [請依照我們記錄的指示操作。](#create)

>[!VIDEO](https://video.tv.adobe.com/v/334953)

>[!VIDEO](https://video.tv.adobe.com/v/334954)

## 建立生產計畫 {#create}

請依照下列步驟建立生產程式。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下 **添加程式** 從螢幕的右上角。

   ![Cloud manager登陸頁面](assets/first_timelogin1.png)

1. 選擇 **為生產環境設定** 在「建立程式」嚮導中建立生產程式。 您可以接受預設程式名稱，或在按一下 **繼續**.

   ![建立程式嚮導](assets/create-prod1.png)

1. 在 **解決方案和附加元件** 頁簽中，選擇要包含在程式中的解決方案。

   ![選擇解決方案](assets/setup-prod-select.png)

1. 按一下解決方案名稱前的>形圖示，即可顯示選用的附加元件，例如選取 **商務** 下方的附加選項 **網站**.

   ![選擇附加元件](assets/setup-prod-commerce.png)

1. 在選取解決方案和附加元件後，按一下 **繼續**.

1. 在 **上線日期** 頁簽，輸入計畫生產計畫的上線日期。

   ![定義計畫上線日期](assets/setup-go-live.png)

   * 您可以隨時編輯此日期。
   * 此日期僅供參考，並會觸發計畫概述頁面上的上線介面工具集，即時提供產品內連結至AEMas a Cloud Service最佳實務檔案，以符合您的歷程，最終達成成功且順暢的上線體驗。

1. 按一下&#x200B;**建立**。

您的程式由Cloud Manager建立，並會在登陸頁面上顯示及選取。

![Cloud Manager概述](assets/navigate-cm.png)

## 存取您的方案 {#acessing}

1. 在登陸頁面上看到節目卡後，請選取刪節號按鈕，檢視可用的選單選項。

   ![方案概述](assets/program-overview.png)

1. 選擇 **計畫概述** 導覽至 **概述** 頁面。

1. 概述頁面上的主要動作呼叫卡會引導您建立環境、非生產管道，最後是生產管道。

   ![方案概述](assets/set-up-prod5.png)

如果您隨時需要切換至其他程式或返回概覽頁面以建立其他程式，請按一下畫面左上角的程式名稱以顯示 **導覽至** 選項。

![導航到](assets/create-program-a1.png)

>[!NOTE]
>
>不同於 [沙箱方案，](introduction-sandbox-programs.md#auto-creation) 生產計畫需要具有適當Cloud Manager角色的使用者，才能建立專案並透過自助服務UI新增環境。
