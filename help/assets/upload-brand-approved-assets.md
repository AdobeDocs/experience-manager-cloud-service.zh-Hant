---
title: 將您的品牌核准資產上傳至 [!DNL Content Hub]
description: 瞭解如何將您的品牌核准資產上傳至Content Hub
role: User
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 14%

---

# 將品牌核准的資產上傳到 Content Hub {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="將品牌核准的資產上傳到 Content Hub"
>abstract="將核准的資產新增至 Content Hub，可以從本機檔案系統或從 OneDrive 或 Dropbox 資料來源匯入資產。無論資料夾結構為何，所有資產將顯示在 Content Hub 的頂層，以增強搜尋功能。"

[有權新增資產的Content Hub使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)可以從本機檔案系統新增資產到Content Hub，或是從OneDrive或Dropbox資料來源匯入資產。 不論本機檔案系統或OneDrive和Dropbox資料來源提供的檔案夾結構為何，所有資產都會顯示在Content Hub的頂層，以增強搜尋功能。

在Assets as a Cloud Service中標示為`Approved`的資產會自動在Content Hub中使用。 如需更多資訊，請參閱[為 Content Hub 核准資產](/help/assets/approve-assets-content-hub.md)。

若要進一步增強資產搜尋，Content Hub可讓您：

* 定義與資產上傳相關的關鍵細節，例如行銷活動名稱、關鍵字、管道等。

* 成功上傳後為每個資產自動產生更多屬性，例如檔案大小、格式、解析度和其他某些屬性。

* 使用[Adobe Sensei](https://www.adobe.com/tw/sensei.html)所提供的人工智慧，自動將相關標籤套用至您所有上傳的資產。 這些標籤名為智慧型標籤，有助於您快速尋找相關資產，提高專案的內容速度。

請確定您僅將[品牌核准的資產上傳至Content Hub](/help/assets/approve-assets.md)。

![上傳品牌核准的資產](assets/upload-brand-approved-assets.png)

## 先決條件 {#prerequisites-add-assets}

[有權新增資產的Content Hub使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)可以將資產上傳至Content Hub。

## 從本機檔案系統新增資產至Content Hub {#add-assets-local-file-system}

若要將資產新增至Content Hub，請執行下列步驟：

1. 按一下&#x200B;**[!UICONTROL 新增Assets]**&#x200B;以檢視&#x200B;**[!UICONTROL 新增您核准的資產]**&#x200B;對話方塊，讓您建立上傳。

1. 在右窗格中的&#x200B;**[!UICONTROL 將檔案或資料夾拖曳到這裡]**&#x200B;區段中，您可以從本機檔案系統拖曳資產，或按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以手動選取本機檔案系統上可用的檔案或資料夾。 此清單是上傳檔案的一部分，可作為清單使用。


   您也可以使用縮圖預覽選取的影像，然後按一下X圖示以從清單中移除任何特定影像。 只有當您將滑鼠停留在影像名稱或大小上時，才會顯示X圖示。 您也可以按一下&#x200B;**[!UICONTROL 全部移除]**，從上載清單中刪除所有專案。

   若要完成上傳程式並啟用&#x200B;**[!UICONTROL 上傳按鈕]**，您必須將資產群組在行銷活動名稱下。

   ![將資產上傳至Content Hub](assets/upload-assets-content-hub.png)

1. 使用&#x200B;**[!UICONTROL 行銷活動名稱]**&#x200B;欄位定義您上傳的名稱。 您可以使用現有的名稱或建立新名稱。 輸入名稱時，Content Hub會提供您更多選項。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   作為最佳作法，Adobe建議您在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

1. 同樣地，定義&#x200B;**[!UICONTROL 關鍵字]**、**[!UICONTROL 管道]**、**[!UICONTROL 時間範圍]**&#x200B;和&#x200B;**[!UICONTROL 地區]**&#x200B;欄位的值。 依關鍵字、管道和位置來標籤和分組資產，可讓使用您核准公司內容的每個人都能找到這些資產並保持其井然有序。

1. 按一下&#x200B;**[!UICONTROL 上傳]**&#x200B;將資產上傳至Content Hub。 [!UICONTROL 檢閱詳細資料]確認方塊出現。 按一下「[!UICONTROL 繼續]」。

1. Assets開始上傳。 按一下[!UICONTROL 新增上傳]以重新啟動上傳程式。 按一下[!UICONTROL 完成]以完成上傳。

管理員也可以設定上傳資產時顯示的必填和選用欄位，例如行銷活動名稱、關鍵字、管道等。 如需詳細資訊，請參閱[設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-upload-options-content-hub)。


## 從OneDrive或Dropbox資料來源將資產新增至Content Hub {#add-assets-onedrive-dropbox}

若要從OneDrive或Dropbox資料來源將資產新增至Content Hub：

1. 按一下&#x200B;**[!UICONTROL 新增Assets]**&#x200B;以檢視&#x200B;**[!UICONTROL 新增核准的資產]**&#x200B;對話方塊，讓您從OneDrive或Dropbox匯入資產。

1. 按一下&#x200B;**[!UICONTROL OneDrive]**&#x200B;或&#x200B;**[!UICONTROL Dropbox]**&#x200B;以開始匯入程式。 Content Hub會提示您登入OneDrive或Dropbox帳戶，然後在左窗格中顯示您的OneDrive或Dropbox資料夾結構。

1. 按一下檔案或資料夾名稱旁的+圖示，以檢視所選專案清單中的專案。 選取您需要新增至Content Hub入口網站的所有檔案後，從本機檔案系統[&#128279;](#add-assets-local-file-system)重複步驟3至6 (將資產新增至Content Hub)以完成上傳程式。

   ![從OneDrive或Dropbox將資產上傳至Content Hub](assets/add-assets-onedrive-dropbox.png)

管理員也可以設定上傳資產時顯示的必填和選用欄位，例如行銷活動名稱、關鍵字、管道等。 如需詳細資訊，請參閱[設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-upload-options-content-hub)。

## 管理使用Content Hub上傳的資產 {#manage-assets-uploaded-using-content-hub}

[有權新增資產的Content Hub使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)可以從本機檔案系統，或從OneDrive或Dropbox資料來源匯入資產，將[資產新增至Content Hub](/help/assets/upload-brand-approved-assets.md)。 不論本機檔案系統或OneDrive和Dropbox資料來源提供的檔案夾結構為何，所有資產都會顯示在Content Hub的頂層，以增強搜尋功能。

是否顯示使用Content Hub上傳的資產，取決於您是否已啟用[自動核准切換](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)：

* 如果啟用&#x200B;**[!UICONTROL 自動核准]**&#x200B;切換開關，您使用 Content Hub 上傳的資產則會自動顯示。

* 如果停用&#x200B;**[!UICONTROL 自動核准]**&#x200B;切換開關，您使用 Content Hub 上傳的資產就不會自動顯示。這些資產會顯示在您 Assets as a Cloud Service 環境的 `hydrated-assets` 資料夾中。導覽至該資料夾，並將資產狀態[大量編輯](#bulk-approve-assets-content-hub)為 `Approved`，使資產顯示於 Content Hub 中。

![Content Hub核准流程](/help/assets/assets/content-hub-approval.png)
