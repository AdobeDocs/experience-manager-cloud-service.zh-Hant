---
title: 在螢幕中建立和管理顯示as a Cloud Service
description: 本頁面說明如何建立和管理Screensas a Cloud Service中的顯示。
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
source-git-commit: 9e0ab778e97658bc8d7669b1f582f3bcddd47915
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 在螢幕中建立和管理顯示as a Cloud Service {#create-displays-screens-cloud}

發佈管道後，您現在可以在Screens服務提供者中建立顯示畫面。

「顯示」是螢幕的虛擬分組，通常彼此相鄰。 對於安裝，顯示器通常是永久的。 這將是作者將使用的物件內容，且一律以邏輯顯示方式參照，而非其實體計數器部分。

## 目標 {#objective}

本檔案可協助您了解如何建立及管理Screens服務提供者中的顯示。 閱讀後，您應：

* 了解如何建立和刪除顯示
* 了解如何將顯示器整理到資料夾中

## 建立顯示的步驟 {#create-display}

請依照下列步驟，從Screens服務提供者建立顯示畫面：

1. 從您的AEM Cloud Service執行個體導覽至Screens Services Provider。
1. 選擇 **顯示** 按一下左側導覽面板中的 **建立** 從畫面的右上角。

   ![影像](/help/screens-cloud/assets/display/disp-1.png)

1. 選擇 **顯示** 從動作列。

   ![影像](/help/screens-cloud/assets/display/disp-2.png)

1. 將標題輸入為 **LoopingChannelDisplay** in **顯示名稱** 按一下 **建立**.

   ![影像](/help/screens-cloud/assets/display/disp3.png)

1. 標題為的顯示 **LoopingChannelDisplay** 現在會顯示在顯示清單中。

   ![影像](/help/screens-cloud/assets/display/disp-4.png)

### 刪除顯示 {#deleting-display}

您可以從Screens服務提供者刪除顯示。

選取顯示並按一下 **刪除** ，如下圖所示。

![影像](/help/screens-cloud/assets/display/disp-5.png)

## 將顯示器組織到資料夾中的步驟 {#organize-display}

## 如何切換資料夾邊欄 {#toggle-rail}

您可以將資料夾邊欄從顯示所有資料夾切換為特定資料夾：

1. 按一下以下醒目提示的按鈕，導覽至顯示的庫存檢視：

   ![影像](/help/screens-cloud/assets/display/display-inventory.png)

1. 隨即顯示資料夾側欄。

   ![影像](/help/screens-cloud/assets/display/toggle-rail.png)

1. 選擇 **隱藏資料夾** 再關上它。

## 如何建立新資料夾 {#create-folder}

您可以建立資料夾，以更妥善地組織顯示。

1. 定位至顯示的庫存視圖。
1. 確認您目前不在資料夾中，應該會看到下列內容：

   ![影像](/help/screens-cloud/assets/display/verify-view.png)

   注意： **全部顯示** 欄位，而階層連結導覽應僅顯示 **顯示**.

1. 按一下右上方的「建立」按鈕，然後選取 **資料夾** 選項。

   ![影像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填寫新資料夾的標題，然後按一下 **建立**.

   ![影像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何建立新的巢狀資料夾 {#nested-folder}

1. 定位至顯示的庫存視圖。

1. 從資料夾側邊欄或在清單檢視中瀏覽，選取所需的父資料夾。
1. 驗證是否已選取所需的父資料夾。

   ![影像](/help/screens-cloud/assets/display/Nestedview.png)

   * 應在資料夾側邊欄中選取資料夾。
   * 階層連結導覽應會在旁邊顯示目前的資料夾名稱 **顯示**.

1. 按一下  **建立**  並選取 **資料夾** 選項。

   ![影像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填寫新資料夾的標題，然後按一下 **建立**.

   ![影像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何將內容移至新資料夾 {#move-folder}

您可以將內容移至新資料夾，以更妥善地組織顯示。

1. 定位至顯示的庫存視圖。

1. 從資料夾側邊欄或從清單檢視中選取，以選取所需的父資料夾。

1. 確認您已選取所需的父資料夾。

![影像](/help/screens-cloud/assets/display/movetofolder.png)

**附註**:應在資料夾側邊欄中選取資料夾。 此外，階層連結導覽應會在旁邊顯示目前的資料夾名稱 **顯示**.

## 如何從資料夾刪除內容 {#delete-folder}

所有資料夾操作都可通過清單視圖中的選擇操作欄訪問。

1. 導覽至上層資料夾，或從側邊欄選取。

1. 在清單檢視中，選取您要刪除的子資料夾，並確定其為空。

1. 按一下 **刪除** 動作。 如果資料夾非空白，則會停用動作。


## 下一步 {#whats-next}

現在，您已學習如何建立和管理專案的顯示器，您應繼續進行Screensas a Cloud Service的歷程，繼續檢閱檔案 [為螢幕中的顯示指派頻道as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=en).
