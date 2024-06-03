---
title: AEM Assets與Adobe Express的原生整合
description: AEM Assets與Adobe Express的原生整合可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: c6cde0a3f5a1513f8158c654167ec0332e4c42a7
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 21%

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

將適當的修改加入 Express 畫布後，您可以將其儲存在 AEM Assets 存放庫中。

1. 按一下 **[!UICONTROL 共用]** 以開啟 **[!UICONTROL 共用]** 對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-share.png)

2. 從右窗格的「儲存」區段中選取， **AEM Assets**. Adobe Express會顯示上傳對話方塊。
3. 指定資產的名稱和格式。您可以以PNG、JPEG、PDF、MP4、MP4+PNG或MP4+JPEG格式儲存畫布內容。 格式會根據資產自動調整。

   >[!NOTE]
   >
   >選取「目前頁面」會將檔案儲存在您的目的地資料夾中。 選取「所有頁面」會在目的地中為所有非PDF檔案建立一個新資料夾，並將它們儲存在那裡，而PDF檔案會儲存為目的地資料夾中的單一檔案。

4. 按一下底下的文字區域 **目的地資料夾** 以選取位置並儲存資產。

   ![將資產儲存在 AEM 中](/help/assets/assets/page-selection-and-destination-folder.svg)

5. 可選：您可以使用為上傳新增行銷活動中繼資料 **專案或行銷活動名稱** 欄位。 您可以使用現有的名稱或建立新名稱。 您可以為上傳定義多個專案或行銷活動名稱。 若要註冊名稱，只需輸入名稱並按Enter即可。
作為最佳實務，Adobe建議您在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

6. 同樣地，定義 **[!UICONTROL 關鍵字]** 和 **[!UICONTROL 頻道]** 欄位。

7. 按一下 **[!UICONTROL 上傳]** 將資產上傳至AEM Assets。




## 限制 {#limitations}

1. 對於匯入和匯出，支援的視訊檔案型別為MP4。

2. 針對MP4視訊匯入：

   a)支援的檔案大小上限為200 MB。 如果超過此限制，會出現警告訊息。
b)支援的最大解析度是3840 X 3840畫素。
c)不支援具有透明背景（Alpha色版）的視訊。

3. 針對MP4視訊匯出：

   a)支援的檔案大小上限為200 MB。 如果超過此限制，則會出現警告訊息，並提供暫時替代建議，如下圖所示。
   ![含因應措施的警報](/help/assets/assets/alert-with-workaround.png)
