---
title: 檢閱資料夾和集合中的資產
description: 為資料夾或集合中的資產設定稽核工作流程，並與稽核者或創意合作夥伴共用以徵求意見反應。
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 9%

---

# 檢閱資料夾和集合中的資產 {#review-folder-assets-and-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

使用Adobe Experience Manager Assets，您可以為資料夾或集合中的資產設定臨時稽核工作流程。 您可以與檢閱者或創意合作夥伴分享，以徵求他們的意見回饋。 您可以將稽核工作流程與專案建立關聯，或建立獨立的稽核任務。

共用資產後，稽核者可以核准或拒絕資產。 通知會在工作流程的不同階段傳送，以通知預期的收件者有關各種任務的完成。 例如，當您共用資料夾或集合時，檢閱者會收到資料夾/集合已共用以供檢閱的通知。

複查者完成複查（核准或拒絕資產）後，您會收到複查完成通知。

## 建立資料夾的稽核任務 {#creating-a-review-task-for-folders}

1. 在Assets使用者介面中，選取您要建立稽核任務的資料夾。
1. 從工具列中選取&#x200B;**[!UICONTROL 建立稽核工作]**&#x200B;圖示以開啟&#x200B;**[!UICONTROL 稽核工作]**&#x200B;頁面。 如果您在工具列中看不到圖示，請選取&#x200B;**[!UICONTROL 更多]**，然後選取圖示。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （選擇性）從&#x200B;**[!UICONTROL 專案]**&#x200B;清單中，選取您想要與稽核任務關聯的專案。 依預設，會選取&#x200B;**[!UICONTROL 無]**&#x200B;選項。 如果不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >**[!UICONTROL 專案]**&#x200B;清單中只會顯示您具有編輯器層級許可權（或更高版本）的專案。

1. 輸入稽核工作的名稱，並從&#x200B;**[!UICONTROL 指派給]**&#x200B;清單中選取核准者。

   >[!NOTE]
   >
   >所選專案的成員/群組可在&#x200B;**[!UICONTROL 指派給]**&#x200B;清單中作為核准者使用。

1. 輸入複查工作的說明、工作優先順序及到期日。

   ![工作詳細資料](assets/task_details.png)

1. 在進階索引標籤中，輸入要用來建立URI的標籤。

   ![檢閱名稱](assets/review_name.png)

1. 選取&#x200B;**[!UICONTROL 提交]**，然後選取&#x200B;**[!UICONTROL 完成]**&#x200B;以關閉確認訊息。 新任務的通知將發送給批准者。
1. 以核准者身分登入[!DNL Experience Manager Assets]並導覽至Assets UI。 若要核准資產，請選取&#x200B;**[!UICONTROL 通知]**&#x200B;圖示，然後從清單中選取稽核工作。

   ![通知](assets/notification.png)

1. 在&#x200B;**[!UICONTROL 檢閱工作]**&#x200B;頁面中，檢查檢閱工作的詳細資訊，然後選取&#x200B;**[!UICONTROL 檢閱]**。
1. 在&#x200B;**[!UICONTROL 稽核任務]**&#x200B;頁面中，選取資產，並選取&#x200B;**[!UICONTROL 核准/拒絕]**&#x200B;圖示以核准或拒絕（視情況而定）。

   ![review_task](assets/review_task.png)

1. 從工具列選取&#x200B;**[!UICONTROL 完成]**&#x200B;圖示。 在對話方塊中，輸入註解並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以進行確認。
1. 導覽至Assets UI，然後開啟資料夾。 資產的核准狀態圖示會顯示在「卡片」和「清單」檢視中。

   **卡片檢視**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **清單檢視**

   ![review_status_listview](assets/review_status_listview.png)

## 建立集合的稽核任務 {#creating-a-review-task-for-collections}

1. 從「集合」頁面中，選取您要建立稽核工作的集合。
1. 從工具列中選取&#x200B;**[!UICONTROL 建立稽核工作]**&#x200B;圖示以開啟&#x200B;**[!UICONTROL 稽核工作]**&#x200B;頁面。 如果您在工具列中看不到圖示，請選取&#x200B;**[!UICONTROL 更多]**，然後選取圖示。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （選擇性）從&#x200B;**[!UICONTROL 專案]**&#x200B;清單中，選取您想要與稽核任務關聯的專案。 依預設，會選取&#x200B;**[!UICONTROL 無]**&#x200B;選項。 如果不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >**[!UICONTROL 專案]**&#x200B;清單中只會顯示您具有編輯器層級許可權（或更高版本）的專案。

1. 輸入稽核工作的名稱，並從&#x200B;**[!UICONTROL 指派給]**&#x200B;清單中選取核准者。

   >[!NOTE]
   >
   >所選專案的成員/群組可在&#x200B;**[!UICONTROL 指派給]**&#x200B;清單中作為核准者使用。

1. 輸入複查工作的說明、工作優先順序及到期日。

   ![task_details-collection](assets/task_details-collection.png)

1. 選取&#x200B;**[!UICONTROL 提交]**，然後選取&#x200B;**[!UICONTROL 完成]**&#x200B;以關閉確認訊息。 新任務的通知將發送給批准者。
1. 以核准者身分登入[!DNL Experience Manager Assets]並導覽至Assets主控台。 若要核准資產，請選取&#x200B;**[!UICONTROL 通知]**&#x200B;圖示，然後從清單中選取稽核工作。
1. 在&#x200B;**[!UICONTROL 檢閱工作]**&#x200B;頁面中，檢查檢閱工作的詳細資訊，然後選取&#x200B;**[!UICONTROL 檢閱]**。
1. 收藏集中的所有資產都會顯示在稽核頁面上。 選取資產，並選取&#x200B;**[!UICONTROL 核准/拒絕]**&#x200B;圖示以核准或拒絕資產（視情況而定）。

   ![review_task_collection](assets/review_task_collection.png)

1. 從工具列選取&#x200B;**[!UICONTROL 完成]**&#x200B;圖示。 在對話方塊中，輸入註解並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以進行確認。
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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
