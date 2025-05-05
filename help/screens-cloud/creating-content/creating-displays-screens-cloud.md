---
title: 在Screens中建立和管理顯示區as a Cloud Service
description: 本頁面說明如何建立及管理Screensas a Cloud Service中的顯示區。
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 3%

---

# 在Screens中建立和管理顯示區as a Cloud Service {#create-displays-screens-cloud}

發佈管道後，您就可以在Screens服務提供者中建立顯示區。

「顯示」是一組虛擬的熒幕，通常位於彼此旁邊。 顯示通常是永久性的安裝。 此物件內容是作者搭配使用的內容，且一律會參照為邏輯顯示，而非其實體計數器部分。

## 目標 {#objective}

本檔案可協助您瞭解如何建立及管理Screens服務提供者中的顯示區。 閱讀本文件後，您應該：

* 瞭解如何建立和刪除顯示區
* 瞭解如何將您的顯示器整理到資料夾中

## 建立顯示的步驟 {#create-display}

請依照下列步驟，從Screens服務提供者建立顯示區：

1. 從您的AEM Cloud Service執行個體導覽至Screens服務提供者。
1. 從左側導覽面板中選取&#x200B;**顯示器**，然後在熒幕的右上角按一下&#x200B;**建立**。

   ![影像](/help/screens-cloud/assets/display/disp-1.png)

1. 從動作列中選取&#x200B;**顯示**。

   ![影像](/help/screens-cloud/assets/display/disp-2.png)

1. 在&#x200B;**顯示名稱**&#x200B;中輸入標題為&#x200B;**LoopingChannelDisplay**，然後按一下&#x200B;**建立**。

   ![影像](/help/screens-cloud/assets/display/disp3.png)

1. 標題為&#x200B;**LoopingChannelDisplay**&#x200B;的顯示現在將顯示在顯示清單中。

   ![影像](/help/screens-cloud/assets/display/disp-4.png)

### 刪除顯示區 {#deleting-display}

您可以從Screens服務提供者中刪除顯示區。

選取顯示，然後從面板底部按一下&#x200B;**刪除**，如下圖所示。

![影像](/help/screens-cloud/assets/display/disp-5.png)

## 將顯示器組織到資料夾中的步驟 {#organize-display}

## 如何切換資料夾邊欄 {#toggle-rail}

您可以將資料夾邊欄從顯示所有資料夾切換為特定資料夾：

1. 按一下下面醒目提示的按鈕，瀏覽至顯示詳細目錄檢視：

   ![影像](/help/screens-cloud/assets/display/display-inventory.png)

1. 資料夾側邊欄隨即顯示。

   ![影像](/help/screens-cloud/assets/display/toggle-rail.png)

1. 選取&#x200B;**隱藏資料夾**&#x200B;以再次關閉它。

## 如何建立資料夾 {#create-folder}

您可以建立資料夾以更妥善地組織您的顯示。

1. 切換作業選項至顯示存貨檢視表。
1. 確認您目前不在資料夾中，您應會看到下列內容：

   ![影像](/help/screens-cloud/assets/display/verify-view.png)

   注意：資料夾側邊欄中應該選取&#x200B;**所有顯示區**，而且階層連結導覽應該只會顯示&#x200B;**顯示區**。

1. 按一下右上方的[建立]按鈕，然後選取&#x200B;**資料夾**&#x200B;選項。

   ![影像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填寫新資料夾的標題，然後按一下&#x200B;**建立**。

   ![影像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何建立巢狀資料夾 {#nested-folder}

1. 切換作業選項至顯示存貨檢視表。

1. 從資料夾側邊欄中或透過在詳細目錄檢視中瀏覽來選取所需的父資料夾。
1. 確認已選取所需的父資料夾。

   ![影像](/help/screens-cloud/assets/display/Nestedview.png)

   * 您應在資料夾側邊欄中選取資料夾。
   * 階層連結導覽應在&#x200B;**顯示器**&#x200B;旁顯示目前的資料夾名稱。

1. 按一下右上角的&#x200B;**建立**，然後選取&#x200B;**資料夾**&#x200B;選項。

   ![影像](/help/screens-cloud/assets/display/Createfolder.png)

1. 填寫新資料夾的標題，然後按一下&#x200B;**建立**。

   ![影像](/help/screens-cloud/assets/display/Createfolder2.png)

## 如何將內容移至新資料夾 {#move-folder}

您可以將內容移至新資料夾，以更妥善地組織您的顯示。

1. 切換作業選項至顯示存貨檢視表。

1. 從資料夾側邊欄選取所需的父資料夾，或從「詳細目錄」檢視中選取。

1. 確認您已選取所需的父資料夾。

![影像](/help/screens-cloud/assets/display/movetofolder.png)

**注意**：資料夾應在資料夾側邊欄中選取。 此外，階層連結導覽應在&#x200B;**顯示器**&#x200B;旁顯示目前的資料夾名稱。

## 如何從資料夾中刪除內容 {#delete-folder}

所有檔案夾作業都可透過詳細目錄檢視中的選取動作列存取。

1. 導覽至上層資料夾，或從側邊欄選取資料夾。

1. 在詳細目錄檢視中，選取您要刪除的子資料夾，並確定它是空的。

1. 按一下選取動作列中的&#x200B;**刪除**&#x200B;動作。 如果資料夾不是空的，則會停用動作。


## 下一步 {#whats-next}

現在您已瞭解如何建立和管理專案的顯示器，接下來應該檢閱檔案[指派頻道給Screens中的顯示器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=zh-Hant)，以繼續您的Screensas a Cloud Service歷程as a Cloud Service。
