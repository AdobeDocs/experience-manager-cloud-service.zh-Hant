---
title: AEM Assets與Adobe Express的原生整合
description: AEM Assets與Adobe Express的原生整合可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 8bbf9a2ba8f708a5a03d11bc0388d39b32d4c7b3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 30%

---

# 與Adobe Express原生整合 {#native-integration-adobe-express}

AEM Assets與Adobe Express原生整合，可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。 您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。整合提供下列主要優點：

* 透過在AEM中編輯和儲存新資產，增加內容重複使用率。

* 減少建立新資產或建立現有資產新版本的整體時間和精力。

## 先決條件 {#prerequisites}

存取AEM Assets中Adobe Express和至少一個環境的權益。 此環境可以是 Assets as a Cloud Service 或 Assets Essentials 中的任何存放庫。


## 在 Adobe Express 編輯器中使用 AEM Assets {#use-aem-assets-in-express}

執行以下步驟，開始在Adobe Express編輯器中使用AEM Assets：

1. 開啟 Adobe Express Web 應用程式。

1. 載入新範本或專案，或建立資產，以開啟新的空白畫布。

1. 按一下 **[!UICONTROL 資產]** 可在左側導覽窗格中使用。 Adobe Express會顯示您有權存取的存放庫清單，以及在根層級可用的資產和資料夾清單。

1. 瀏覽或搜尋存放庫中的資產，以拖放至畫布上。 您可以使用各種可用的篩選器來篩選資產，例如檔案型別、MIME型別和維度。

   ![包括資產附加元件中的資產](assets/adobe-express-native-integration.png)


## 將 Adobe Express 專案儲存在 AEM Assets 中 {#save-express-projects-in-assets}

將適當的修改加入 Express 畫布後，您可以將其儲存在 AEM Assets 存放庫中。

1. 按一下 **[!UICONTROL 共用]** 以開啟 **[!UICONTROL 共用]** 對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-share.png)

1. 選取 **[!UICONTROL AEM Assets]** 從 **[!UICONTROL 儲存]** 區段可在右窗格中使用。 Adobe Express會顯示上傳對話方塊。
1. 指定資產的名稱和格式。您可以將畫布內容儲存為 PNG 或 JPEG 格式類型。

1. 按一下「**[!UICONTROL 位置]**」欄位旁邊的資料夾圖示，導覽至需要儲存資產的位置，然後按一下「**[!UICONTROL 選取]**」。資料夾名稱會顯示在「**[!UICONTROL 位置]**」欄位內。

   ![將資產儲存在 AEM 中](assets/adobe-express-upload.png)

1. 可選：您可以使用為上傳新增行銷活動中繼資料 **[!UICONTROL 專案或行銷活動名稱]** 欄位。 您可以使用現有的名稱或建立新名稱。 您可以為上傳定義多個專案或行銷活動名稱。 輸入名稱時，請在對話方塊中的其他任何位置按一下，或按下 `,` （逗號）金鑰來登入名稱。

   作為最佳實務，Adobe建議您在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。
1. 同樣地，定義 **[!UICONTROL 關鍵字]** 和 **[!UICONTROL 頻道]** 欄位。

1. 按一下「**[!UICONTROL 上傳]**」，將資產上傳到 AEM Assets。




## 限制 {#limitations}

從多個存放庫儲存包含資產的檔案時，某些具有多個Assets存放庫存取權的使用者會遇到已知錯誤。
