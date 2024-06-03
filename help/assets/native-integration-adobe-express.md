---
title: AEM Assets與Adobe Express的原生整合
description: AEM Assets與Adobe Express的原生整合可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 4e33782dd8db0c1185b9a7733e7bcccfbcf3c3ba
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 17%

---

# 與Adobe Express原生整合 {#native-integration-adobe-express}

AEM Assets 可與 Adobe Express 自然整合，讓您從 Adobe Express 使用者介面直接存取 AEM Assets 儲存的資源。您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。整合提供下列主要優點：

* 透過在AEM中編輯和儲存新資產，增加內容重複使用率。

* 減少建立新資產或建立現有資產新版本的整體時間和精力。

## 先決條件 {#prerequisites}

存取AEM Assets中Adobe Express和至少一個環境的權益。 此環境可以是 Assets as a Cloud Service 或 Assets Essentials 中的任何存放庫。


## 在 Adobe Express 編輯器中使用 AEM Assets {#use-aem-assets-in-express}

執行以下步驟，開始在Adobe Express編輯器中使用AEM Assets：

1. 開啟 Adobe Express Web 應用程式。

2. 載入新範本或專案，或建立資產，以開啟新的空白畫布。

3. 按一下 **[!UICONTROL 資產]** 可在左側導覽窗格中使用。 Adobe Express會顯示您有權存取的存放庫清單，以及在根層級可用的資產和資料夾清單。

4. 瀏覽或搜尋存放庫中的資產，以拖放至畫布上。 您可以使用各種可用的篩選器來篩選資產，例如檔案型別、MIME型別和維度。

   >[!NOTE]
   >
   >依維度篩選不適用於視訊。

   ![包括資產附加元件中的資產](assets/adobe-express-native-integration.png)


## 將 Adobe Express 專案儲存在 AEM Assets 中 {#save-express-projects-in-assets}

在Express畫布中加入適當的修改後，您可以將其儲存至AEM Assets存放庫。

1. 按一下 **[!UICONTROL 共用]** 以開啟 **[!UICONTROL 共用]** 對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-share.png)

2. 從右窗格的「儲存」區段中，選取 **AEM Assets**. Adobe Express會顯示上傳對話方塊。
3. 選取 **目前頁面** 或 **所有頁面** 儲存選項。 選取 **目前頁面** 將檔案儲存在您的目的地資料夾中，但是，選取 **所有頁面** 會在目的地中為所有非PDF檔案建立新資料夾，並將它們儲存為個別檔案，而PDF檔案會儲存為目的地資料夾中的單一檔案。
4. 指定資產的名稱和格式。您可以以PNG、JPEG、PDF、MP4、MP4+PNG或MP4+JPEG格式儲存畫布內容。 格式會根據資產自動調整。
5. 按一下下方的資料夾圖示 **目的地資料夾** 以選取位置並儲存資產。

   ![將資產儲存在 AEM 中](/help/assets/assets/page-selection-and-destination-folder.svg)

6. 可選：您可以使用為上傳新增行銷活動中繼資料 **專案或行銷活動名稱** 欄位。 您可以使用現有的名稱或建立新名稱。 您可以為上傳定義多個專案或行銷活動名稱。 若要註冊名稱，只需輸入名稱並按Enter即可。
Adobe建議的最佳作法是在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

7. 同樣地，定義 **[!UICONTROL 關鍵字]** 和 **[!UICONTROL 頻道]** 欄位。

8. 按一下 **[!UICONTROL 上傳]** 將資產上傳至AEM Assets。

## 限制 {#limitations}

1. 對於匯入和匯出，支援的視訊檔案型別為MP4。

2. 針對MP4視訊匯入：

   1. 支援的檔案大小上限為200 MB。 如果超過此限制，便會顯示警告訊息。
   2. 支援的最大解析度是3840 X 3840畫素。
   3. 不支援具有透明背景（Alpha色版）的視訊。

3. 針對MP4視訊匯出：

   1. 支援的檔案大小上限為200 MB。 如果超過此限制，警報會建議將視訊縮減至200 MB以下，或在下載視訊後手動上傳至AEM Assets目的地資料夾。



