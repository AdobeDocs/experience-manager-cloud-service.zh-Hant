---
title: AEM Assets與Adobe Express的原生整合
description: AEM Assets與Adobe Express的原生整合可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 3046da6d16b2494f6a3f18c60df7a4600afcd7ba
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 14%

---

# 與 Adobe Express 原生整合 {#native-integration-adobe-express}

AEM Assets 可與 Adobe Express 自然整合，讓您從 Adobe Express 使用者介面直接存取 AEM Assets 儲存的資源。您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。整合提供下列主要優點：

* 透過在AEM中編輯和儲存新資產，增加內容重複使用率。

* 減少建立新資產或建立現有資產新版本的整體時間和精力。

## 先決條件 {#prerequisites}

存取Adobe Express和AEM Assets內至少一個環境的許可權。 此環境可以是 Assets as a Cloud Service 或 Assets Essentials 中的任何存放庫。

## 在 Adobe Express 編輯器中使用 AEM Assets {#use-aem-assets-in-express}

執行以下步驟，開始在Adobe Express編輯器中使用AEM Assets：

1. 開啟 Adobe Express Web 應用程式。

2. 載入新範本或專案，或建立資產，以開啟新的空白畫布。

3. 按一下左側導覽窗格中可用的&#x200B;**[!UICONTROL Assets]**。 Adobe Express會顯示您有權存取的存放庫清單，以及在根層級可用的資產和資料夾清單。

4. 瀏覽或搜尋存放庫中的資產，然後將它們拖放到畫布上。 或者，按一下資產以將其放在畫布上。 您也可以依各種條件篩選資產，例如檔案型別、MIME型別和維度。

   >[!NOTE]
   >
   >依維度篩選不適用於視訊。

   ![包括資產附加元件中的資產](assets/adobe-express-native-integration.png)

### 使用AEM上傳功能取代影像 {#replace-image-using-aem-upload}

此外，您可以使用&#x200B;**[!UICONTROL AEM上傳]**&#x200B;來取代新增的影像。 要執行此操作，請執行下列步驟：

1. 瀏覽或搜尋資產，並將它拖放至畫布上。

1. 選取您要取代的影像。 按一下「取代」**&#x200B;**，然後選取&#x200B;**[!UICONTROL 「AEM Assets」]**。

   ![AEM取代](assets/aem-replace.png)

1. **[!UICONTROL AEM上傳]**&#x200B;面板在左側導覽窗格中開啟。 Adobe Express會顯示您有權存取的存放庫清單，以及在根層級可用的資產和資料夾清單。 從那裡選取要預覽畫布上取代的資產，然後按一下[取代]確認。**&#x200B;**

   >[!NOTE]
   >
   > 不支援SVG檔案型別。

## 將 Adobe Express 專案儲存在 AEM Assets 中 {#save-express-projects-in-assets}

在Express畫布中加入適當的修改後，您可以將其儲存至AEM Assets存放庫。

1. 按一下[共用]&#x200B;**&#x200B;**&#x200B;開啟[共用]&#x200B;**&#x200B;**&#x200B;對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-share.png)

2. 從右窗格的&#x200B;**[!UICONTROL 建議]**&#x200B;區段中，選取&#x200B;**AEM Assets**。 Adobe Express會顯示上傳對話方塊。

   ![將資產儲存在 AEM 中](assets/adobe-express-aem.png)

3. 選取&#x200B;**目前頁面**&#x200B;或&#x200B;**所有頁面**。 指定要匯出的資產的名稱和格式。 您可以匯出PNG、JPEG、PDF、MP4、MP4+PNG或MP4+JPEG格式的畫布內容。 格式會根據畫布頁面上的資產自動調整。
選取&#x200B;**目前頁面**&#x200B;會將目前頁面上的資產儲存到您的目的地資料夾。 如果您選取「**所有頁面**」，且匯出格式不是PDF，則所有畫布頁面都會以個別檔案的形式儲存在目的地資料夾的新資料夾中。 如果匯出格式為PDF，則所有畫布頁面都會儲存為目的地資料夾中的單一PDF檔案。

4. 按一下&#x200B;**目的地資料夾**&#x200B;下的資料夾圖示，以選取位置並儲存資產。

   ![將資產儲存在 AEM 中](/help/assets/assets/page-selection-and-destination-folder.svg)

5. 可選：您可以使用&#x200B;**專案或行銷活動名稱**&#x200B;欄位，新增您上傳的行銷活動中繼資料。 您可以使用現有的名稱或建立新名稱。 您可以為上傳定義多個專案或行銷活動名稱。 若要註冊名稱，只需輸入名稱並按Enter即可。
作為最佳作法，Adobe建議在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

6. 同樣地，定義&#x200B;**[!UICONTROL 關鍵字]**&#x200B;和&#x200B;**[!UICONTROL 管道]**&#x200B;欄位的值。

7. 按一下&#x200B;**[!UICONTROL 上傳]**&#x200B;以將資產上傳至AEM Assets。

<table> 
    <tbody>
     <tr>
      <th><strong>支援的格式</strong></th>
      <th><strong>大小</strong></th>
     </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
        <td> 6500萬畫素（例如8K x 8K或16K x 4K） </td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
        <td> 6500萬畫素（例如8K x 8K或16K x 4K） </td>
    </tr>
    <tr>
        <td>[!UICONTROL SVG]</td>
        <td> 最大250 KB</td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
        <td> 3840 X 3840畫素，最大200 MB</td>
    </tr>
    <tr>
      <td colspan="2"> <i>桌上型電腦裝置的資產大小必須小於80 MB，行動裝置必須小於40 MB。</i></td>
   </tr>
    </tbody>
</table>

## 限制 {#limitations}

1. 對於匯入和匯出，支援的視訊檔案型別為MP4。

2. 對於&#x200B;**MP4視訊匯入**，不支援具有透明背景（Alpha色版）的視訊。
   <!--
   1. The maximum file size supported is 200 MB. If this limit exceeds, an alert message displays.
   2. The maximum supported resolution is 3840 X 3840 pixels.
   3. Videos with transparent backgrounds (alpha channel) are not supported.
   -->

3. 對於&#x200B;**MP4視訊匯出**，支援的檔案大小上限為200 MB。 如果超過此限制，警報會建議將視訊縮減至200 MB以下，或在下載視訊後手動上傳至AEM Assets目的地資料夾。



