---
title: '建立生產程式 '
description: 瞭解如何使用雲管理器建立您自己的生產程式來承載即時流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 3557ddbc76ff21bcfe4ac0338f116b02b5135f2c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# 建立生產程式 {#create-production-program}

生產程式面向熟悉和AEMCloud Manager並準備開始編寫、構建和測試代碼的用戶，目標是將其部署到即時流量主機。

瞭解有關文檔中程式類型的詳細資訊 [瞭解程式和程式類型。](program-types.md)

## 視頻Tutorials {#video-tutorials}

您可以觀看這兩個教程視頻，以瞭解如何在雲管理器中建立程式或 [按照我們的文檔說明進行操作。](#create)

>[!VIDEO](https://video.tv.adobe.com/v/334953)

>[!VIDEO](https://video.tv.adobe.com/v/334954)

## 建立生產程式 {#create}

按照以下步驟建立生產程式。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下 **添加程式** 從螢幕的右上角。

   ![雲管理器登錄頁](assets/first_timelogin1.png)

1. 選擇 **為生產設定** 建立程式嚮導中建立生產程式。 您可以接受預設程式名稱，或在按一下 **繼續**。

   ![建立程式嚮導](assets/create-prod1.png)

1. 在 **解決方案和附加模組** 頁籤。

   ![選擇解決方案](assets/setup-prod-select.png)

1. 按一下解決方案名稱前的雪佛龍，以顯示可選的附加項，如 **商業** 載入項選項 **站點**。

   ![選擇載入項](assets/setup-prod-commerce.png)

1. 選擇瞭解決方案和載入項後，按一下 **繼續**。

1. 在 **上線日期** 頁籤，輸入計畫生產程式開始運行的日期。

   ![定義計畫上線日期](assets/setup-go-live.png)

   * 此日期可以隨時編輯。
   * 此日期僅供參考，並觸發程式概述頁面上的「開始使用」小部件，以及時提供到AEMas a Cloud Service最佳做法文檔的產品內連結，以與您的旅程保持一致，最終獲得成功且流暢的開始使用體驗。

1. 按一下&#x200B;**建立**。

您的程式由雲管理器建立，在登錄頁上顯示和選擇。

![雲管理器概述](assets/navigate-cm.png)

## 訪問您的程式 {#acessing}

1. 在登錄頁上看到程式卡後，選擇省略號按鈕以查看可用的菜單選項。

   ![計畫概述](assets/program-overview.png)

1. 選擇 **計畫概述** 導航至雲管理器 **概述** 的子菜單。

1. 概述頁面上的主操作呼叫卡將指導您建立環境、非生產管道，最後建立生產管道。

   ![計畫概述](assets/set-up-prod5.png)

如果您需要隨時切換到其他程式或返回概覽頁以建立其他程式，請按一下螢幕左上角的程式名稱以顯示 **導航到** 的雙曲餘切值。

![導航到](assets/create-program-a1.png)

>[!NOTE]
>
>與 [沙盒程式，](introduction-sandbox-programs.md#auto-creation) 生產程式將要求具有相應雲管理器角色的用戶通過自助服務UI建立項目並添加環境。
