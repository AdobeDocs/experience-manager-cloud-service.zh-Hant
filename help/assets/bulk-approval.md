---
title: 查看資料夾和集合中的資產
description: 設定資料夾或集合中資產的審閱工作流，並與審閱人或創意合作夥伴共用以尋求反饋。
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 21%

---

# 查看資料夾和集合中的資產 {#review-folder-assets-and-collections}

使用Adobe Experience Manager資產，可以設定資料夾或集合中資產的臨時複查工作流。 您可以與審閱人或創意合作夥伴分享它以尋求他們的反饋。 您可以將審閱工作流與項目關聯，或建立獨立的審閱任務。

共用資產後，審閱人可以批准或拒絕這些資產。 在工作流的各個階段發送通知，以通知目標接收者有關各種任務的完成。 例如，當您共用資料夾或集合時，審閱者會收到一則通知，表明已共用了資料夾/集合以供審閱。

審閱者完成審閱（批准或拒絕資產）後，您將收到審閱完成通知。

## 為資料夾建立審閱任務 {#creating-a-review-task-for-folders}

1. 從「資產」用戶介面中，選擇要為其建立審閱任務的資料夾。
1. 從工具列中點選/按一下「建 **[!UICONTROL 立檢閱工作]** 」圖示，以開啟「 **** 檢閱工作」頁面。如果您在工具列中看不到圖示，請點選/按一下「更 **[!UICONTROL 多]** 」，然後選取圖示。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （可選） **[!UICONTROL 項目]** 清單中，選擇要與審閱任務關聯的項目。 預設情況下， **[!UICONTROL 無]** 的雙曲餘切值。 如果不想將任何項目與審閱任務關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您具有編輯器級別權限（或更高權限）的項目在 **[!UICONTROL 項目]** 清單框。

1. 輸入審閱任務的名稱，然後從 **[!UICONTROL 分配給]** 清單框。

   >[!NOTE]
   >
   >選定項目的成員/組可作為批准者在 **[!UICONTROL 分配給]** 清單框。

1. 輸入複查任務的說明、任務優先順序和到期日。

   ![任務詳細資訊](assets/task_details.png)

1. 在「高級」頁籤中，輸入要用於建立URI的標籤。

   ![review_name](assets/review_name.png)

1. 點選/按一 **[!UICONTROL 下提交]**，然後點選/按一 **[!UICONTROL 下完成]** ，以關閉確認訊息。新任務的通知將發送給批准者。
1. 登錄到 [!DNL Experience Manager Assets] 作為批准者並導航至「資產」UI。 要批准資產，請按一下/點擊 **[!UICONTROL 通知]** 表徵圖，然後從清單中選擇審閱任務。

   ![通知](assets/notification.png)

1. 在「復 **[!UICONTROL 查任務]** 」頁中，檢查複查任務的詳細資訊，然後點選/按一下「 **[!UICONTROL 複查」]**。
1. 在「復 **[!UICONTROL 核任務]** 」頁面中，選擇資產，並點選/按一下「核准/拒絕 **** 」圖示以視情況核准或拒絕。

   ![審閱任務](assets/review_task.png)

1. 點擊/按一下 **[!UICONTROL 完成]** 的子菜單。 在對話框中，輸入注釋並點擊/按一下  **[!UICONTROL 完成]** 確認。
1. 導航到「資產」UI，然後開啟資料夾。 資產的批准狀態表徵圖將同時顯示在「卡」和「清單」視圖中。

   **卡視圖**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **清單視圖**

   ![review_status_listview](assets/review_status_listview.png)

## 為集合建立審閱任務 {#creating-a-review-task-for-collections}

1. 從「收集」頁中，選擇要為其建立審閱任務的收集。
1. 從工具列中點選/按一下「建 **[!UICONTROL 立檢閱工作]** 」圖示，以開啟「 **** 檢閱工作」頁面。如果您在工具列中看不到圖示，請點選/按一下「更 **[!UICONTROL 多]** 」，然後選取圖示。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （可選） **[!UICONTROL 項目]** 清單中，選擇要與審閱任務關聯的項目。 預設情況下， **[!UICONTROL 無]** 的雙曲餘切值。 如果不想將任何項目與審閱任務關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您具有編輯器級別權限（或更高權限）的項目在 **[!UICONTROL 項目]** 清單框。

1. 輸入審閱任務的名稱，然後從 **[!UICONTROL 分配給]** 清單框。

   >[!NOTE]
   >
   >選定項目的成員/組可作為批准者在 **[!UICONTROL 分配給]** 清單框。

1. 輸入複查任務的說明、任務優先順序和到期日。

   ![task_details_collection](assets/task_details-collection.png)

1. 點選/按一 **[!UICONTROL 下提交]**，然後點選/按一 **[!UICONTROL 下完成]** ，以關閉確認訊息。新任務的通知將發送給批准者。
1. 登錄到 [!DNL Experience Manager Assets] 作為批准者並導航至「資產」控制台。 要批准資產，請點擊/按一下 **[!UICONTROL 通知]** 表徵圖，然後從清單中選擇審閱任務。
1. 在「復 **[!UICONTROL 查任務]** 」頁中，檢查複查任務的詳細資訊，然後點選/按一下「 **[!UICONTROL 複查」]**。
1. 集合中的所有資產都可在審閱頁面上看到。 選擇資產並點擊/按一下 **[!UICONTROL 批准/拒絕]** 表徵圖以批准或拒絕資產。

   ![review_task_collection](assets/review_task_collection.png)

1. 點擊/按一下 **[!UICONTROL 完成]** 的子菜單。 在對話框中，輸入注釋並點擊/按一下 **[!UICONTROL 完成]** 確認。
1. 導航到「集合」控制台並開啟集合。 資產的批准狀態表徵圖將同時顯示在「卡」和「清單」視圖中。

   **卡視圖**

   ![集合_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **清單視圖**

   ![集合_reviewstatuslistview](assets/collection_reviewstatuslistview.png)
