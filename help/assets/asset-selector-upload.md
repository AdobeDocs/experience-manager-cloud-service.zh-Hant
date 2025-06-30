---
title: 在「資產選擇器」中上傳資產
description: 使用上傳功能在資產選擇器MFE中上傳資產
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 將檔案和資料夾上傳至Asset Selector {#upload-files-folders}

您可以從您的本機檔案系統上傳檔案或資料夾至Asset Selector。 若要使用本機檔案系統上傳檔案，您通常需要使用Asset Selector微前端應用程式提供的上傳功能。

## 從本機檔案系統上傳資產 {#basic-upload}

若要將資產新增至「資產選取器」，請執行下列步驟：

1. 如果您正在使用邊欄檢視，請移至省略符號，然後按一下![上傳圖示](assets/upload-icon.svg) **[!UICONTROL 上傳]**。 另一方面，若是模組檢視，請按一下右上角的![上傳圖示](assets/upload-icon.svg) **[!UICONTROL 上傳]**。 [!UICONTROL 上傳Assets]畫面隨即顯示。

   ![將資產上傳至資產選擇器](assets/upload-assets.png)

   此外，在&#x200B;**[!UICONTROL 將檔案或資料夾拖曳到這裡]**&#x200B;區段中，您可以從本機檔案系統拖曳資產，或按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以手動選取本機檔案系統上可用的檔案或資料夾。 此清單是上傳檔案的一部分，可作為清單使用。

   ![將資產基本上傳至資產選擇器](assets/basic-upload.png)

   您也可以使用縮圖預覽選取的影像，然後按一下X圖示以從清單中移除任何特定影像。 只有當您將滑鼠停留在影像名稱或大小上時，才會顯示X圖示。 您也可以按一下&#x200B;**[!UICONTROL 全部移除]**，從上載清單中刪除所有專案。

1. 若要完成上傳程式，請按一下&#x200B;**[!UICONTROL 上傳]**。 您的上傳資產隨即顯示。 如需可設定的程式碼，請參閱[基本上傳](/help/assets/asset-selector-customization.md#basic-upload)。

## 上傳包含中繼資料的資產 {#upload-assets-with-metadata}

您可以將中繼資料新增到資產，同時立即將資產上傳到您的應用程式。 中繼資料包含各種欄位，例如業務主旨列、產品詳細資訊、行銷活動等。 要執行此操作，請使用`metadataSchema`屬性。 移至[資產選擇器屬性](/help/assets/asset-selector-properties.md)以進一步瞭解`metadataSchema`屬性。

請參閱使用中繼資料[&#128279;](/help/assets/asset-selector-customization.md#upload-with-metadata)上傳以取得組態所需的程式碼片段。

![上傳包含中繼資料的資產](assets/upload-with-metadata.png)

1. 使用&#x200B;**[!UICONTROL 行銷活動名稱]**&#x200B;欄位定義您上傳的名稱。 您可以使用現有的名稱或建立新名稱。 輸入名稱時，「資產選擇器」會提供您更多選項。

   作為最佳作法，Adobe建議您在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

1. 同樣地，定義&#x200B;**[!UICONTROL 關鍵字]**、**[!UICONTROL 管道]**、**[!UICONTROL 時間範圍]**&#x200B;和&#x200B;**[!UICONTROL 地區]**&#x200B;欄位的值。 依關鍵字、管道和位置來標籤和分組資產，可讓使用您核准公司內容的每個人都能找到這些資產並保持其井然有序。

1. 按一下&#x200B;**[!UICONTROL 上傳]**&#x200B;將資產上傳至「資產選擇器」。 [!UICONTROL 檢閱詳細資料]確認方塊出現。 按一下「[!UICONTROL 繼續]」。

1. Assets開始上傳。 按一下[!UICONTROL 新增上傳]以重新啟動上傳程式。 按一下[!UICONTROL 完成]以完成上傳。


## 自訂上傳 {#customize-upload}

資產選擇器可讓您新增自訂的上傳表單。 有數個自訂功能可供使用。 例如，[hideUploadButton](/help/assets/asset-selector-properties.md)屬性可讓您隱藏應用程式中預設顯示的上傳按鈕。 您可以視需要自訂該檔案，以便在MFE應用程式外部呈現。 請參閱組態的[自訂上傳](/help/assets/asset-selector-customization.md#customized-upload)。

![自訂上傳](assets/customized-upload.png)

>[!MORELIKETHIS]
>
>* [資產選擇器範例](/help/assets/asset-selector-examples.md)
>* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
