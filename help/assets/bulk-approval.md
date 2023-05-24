---
title: 檢閱資料夾和集合中的資產
description: 為資料夾或收藏集中的資產設定稽核工作流程，並與稽核者或創意合作夥伴分享，以徵求意見反應。
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 24%

---

# 檢閱資料夾和集合中的資產 {#review-folder-assets-and-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service  | 本文 |

使用Adobe Experience Manager資產，您可以為資料夾或集合中的資產設定臨時稽核工作流程。 您可以與評論者或創意合作夥伴分享，以徵求他們的意見反應。 您可以將稽核工作流程與專案建立關聯，也可以建立獨立的稽核任務。

共用資產後，稽核者可以核准或拒絕資產。 通知會在工作流程的不同階段傳送，以通知預期的收件者有關各種任務的完成。 例如，當您共用資料夾或集合時，稽核者會收到資料夾/集合已共用供稽核的通知。

複查者完成複查（核准或拒絕資產）後，您會收到複查完成通知。

## 建立資料夾的稽核任務 {#creating-a-review-task-for-folders}

1. 從「資產」使用者介面中，選取您要建立稽核任務的資料夾。
1. 從工具列中點選/按一下「建 **[!UICONTROL 立檢閱工作]** 」圖示，以開啟「 **** 檢閱工作」頁面。如果您在工具列中看不到圖示，請點選/按一下「更 **[!UICONTROL 多]** 」，然後選取圖示。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （選用）從 **[!UICONTROL 專案]** 清單中，選取要與稽核任務相關聯的專案。 根據預設， **[!UICONTROL 無]** 選項時才會選擇此選項。 如果您不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您擁有編輯器層級許可權（或更高版本）的專案才會顯示在 **[!UICONTROL 專案]** 清單。

1. 輸入稽核工作的名稱，然後從中選擇核准者 **[!UICONTROL 指派給]** 清單。

   >[!NOTE]
   >
   >所選專案的成員/群組可作為核准者出現在 **[!UICONTROL 指派給]** 清單。

1. 輸入複查工作的描述、工作優先順序和到期日。

   ![task_details](assets/task_details.png)

1. 在進階索引標籤中，輸入要用來建立URI的標籤。

   ![review_name](assets/review_name.png)

1. 點選/按一 **[!UICONTROL 下提交]**，然後點選/按一 **[!UICONTROL 下完成]** ，以關閉確認訊息。新任務的通知將發送給批准者。
1. 登入 [!DNL Experience Manager Assets] 以核准者身分導覽至「資產」UI。 若要核准資產，請按一下/點選 **[!UICONTROL 通知]** 圖示，然後從清單中選取稽核任務。

   ![通知](assets/notification.png)

1. 在「復 **[!UICONTROL 查任務]** 」頁中，檢查複查任務的詳細資訊，然後點選/按一下「 **[!UICONTROL 複查」]**。
1. 在「復 **[!UICONTROL 核任務]** 」頁面中，選擇資產，並點選/按一下「核准/拒絕 **** 」圖示以視情況核准或拒絕。

   ![review_task](assets/review_task.png)

1. 點選/按一下 **[!UICONTROL 完成]** 圖示加以檢視。 在對話方塊中，輸入註解並點選/按一下  **[!UICONTROL 完成]** 以確認。
1. 導覽至「資產」UI，然後開啟資料夾。 資產的核准狀態圖示會顯示在「卡片」和「清單」檢視中。

   **卡片檢視**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **清單檢視**

   ![review_status_listview](assets/review_status_listview.png)

## 建立集合的稽核任務 {#creating-a-review-task-for-collections}

1. 從「集合」頁面中，選取您要建立稽核任務的集合。
1. 從工具列中點選/按一下「建 **[!UICONTROL 立檢閱工作]** 」圖示，以開啟「 **** 檢閱工作」頁面。如果您在工具列中看不到圖示，請點選/按一下「更 **[!UICONTROL 多]** 」，然後選取圖示。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （選用）從 **[!UICONTROL 專案]** 清單中，選取要與稽核任務相關聯的專案。 根據預設， **[!UICONTROL 無]** 選項時才會選擇此選項。 如果您不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您擁有編輯器層級許可權（或更高版本）的專案才會顯示在 **[!UICONTROL 專案]** 清單。

1. 輸入稽核工作的名稱，然後從中選擇核准者 **[!UICONTROL 指派給]** 清單。

   >[!NOTE]
   >
   >所選專案的成員/群組可作為核准者出現在 **[!UICONTROL 指派給]** 清單。

1. 輸入複查工作的描述、工作優先順序和到期日。

   ![task_details-collection](assets/task_details-collection.png)

1. 點選/按一 **[!UICONTROL 下提交]**，然後點選/按一 **[!UICONTROL 下完成]** ，以關閉確認訊息。新任務的通知將發送給批准者。
1. 登入 [!DNL Experience Manager Assets] 以核准者身分導覽至「資產」主控台。 若要核准資產，請點選/按一下 **[!UICONTROL 通知]** 圖示，然後從清單中選取稽核任務。
1. 在「復 **[!UICONTROL 查任務]** 」頁中，檢查複查任務的詳細資訊，然後點選/按一下「 **[!UICONTROL 複查」]**。
1. 收藏集中的所有資產都會顯示在稽核頁面上。 選取資產，然後點選/按一下 **[!UICONTROL 核准/拒絕]** 圖示以核准或拒絕資產（視情況而定）。

   ![review_task_collection](assets/review_task_collection.png)

1. 點選/按一下 **[!UICONTROL 完成]** 圖示加以檢視。 在對話方塊中，輸入註解並點選/按一下 **[!UICONTROL 完成]** 以確認。
1. 導覽至「系列」主控台，並開啟系列。 資產的核准狀態圖示會顯示在「卡片」和「清單」檢視中。

   **卡片檢視**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **清單檢視**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
