---
title: 匯入、匯出和組織最適化Forms、PDF forms和其他資產
seo-title: Learn to import, export, and organize Adaptive Forms, PDF forms, and other assets on an[!DNL AEM Forms] instance
description: '想要將適用性Forms和資產移轉至AEM例項或從例項移轉？ 在此了解如何從匯入和匯出適用性Forms、PDF forms、主題和其他支援資產 [!DNL AEM Forms] 例項。 '
seo-description: Looking to migrate Adaptive Forms and assets to and from an AEM instances? Learn here how to import and export Adaptive Forms, PDF forms, themes, and other supporting assets from an [!DNL AEM Forms] instance.
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 0%

---

# 匯入、匯出和組織最適化Forms、PDF forms和其他資產{#importing-and-exporting-assets-to-aem-forms}

您可以在下列之間移動適用性Forms和相關資產：適用性表單主題、表單資料模型、適用性表單範本、檔案片段和PDF forms [!DNL AEM Forms] 例項。 您可以匯入和匯出CRX套件或二進位檔案格式的資產。

匯出適用性表單時，內容原則和範本不會匯出。 使用 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) 匯出這些資產。

## 下載適用性Forms、PDF forms或相關資產 {#download-forms-amp-documents-assets}

若要下載表單或相關資產：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示> **[!UICONTROL 導覽]** ![羅盤](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取資產，然後點選 **[!UICONTROL 下載]** 表徵圖。
1. 在「下載資產」中，選擇下列其中一個選項，然後點選 **[!UICONTROL 下載]**.

   * **下載為CRX套件：** 使用選項，從 [!DNL AEM Forms] 例項。 它會以CRX套件形式下載所有資產和資料夾，包括以AEM(適用性Forms和適用性表單片段)製作的表單、表單集、表單資料模型、表單範本、PDF檔案和參考資源（XSD和影像）。
以套件形式下載資產的好處，在於也會下載所選資產所參考的資產。 例如，如果您的適用性表單使用表單範本XSD和影像。 選取此適用性表單並以套件形式下載時，下載的套件也會包含表單範本、XSD和影像。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。

   * **以二進位檔案形式下載資產：** 使用選項僅下載表單模板(XDP)、PDF forms(PDF)、文檔(PDF)和資源（影像、結構、樣式表）。 您可以使用外部應用程式編輯這些資產。 它會將具有二進位檔的資產(例如影像、PDF和其他支援格式)下載為.zip檔案。
您無法下載適用性Forms、適用性表單片段、主題和表單集，具有 **[!UICONTROL 以二進位檔案形式下載資產]** 選項。 若要下載這些資產，您應使用 **[!UICONTROL 下載為CRX套件]** 選項。

   選取的資產會以封存檔（.zip檔案）的形式下載。

   >[!NOTE]
   >
   >AEM套件和二進位檔案都會以封存檔（.zip檔案）的形式下載。 系統不會隨資產下載資產的範本。 您需要個別匯出資產範本。

## 上傳適用性Forms、PDF forms或相關資產 {#upload-forms-amp-documents-assets}

您可以個別上傳支援的資產類型，或以ZIP封存的形式上傳。 若為ZIP檔案，則會顯示所有受支援資產的相對路徑。 系統會忽略ZIP中不支援的資產，且不會列出。 不過，如果ZIP封存檔僅包含不支援的資產，則會顯示錯誤訊息，而非快顯對話方塊。
若要上傳表單或相關資產：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示> **[!UICONTROL 導覽]** ![羅盤](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**. 對話方塊隨即顯示。
1. 在對話方塊中，瀏覽並選取要匯入的套件或封存。 您也可以選取其他支援的檔案類型。 點選 **[!UICONTROL 開啟]**. 所選資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，驗證要上傳之資產的詳細資訊，然後點選 **[!UICONTROL 上傳]**.

   如果您上傳現有的表單資產，資產便會更新。

   >[!NOTE]
   >
   > * 當名稱與不同的資源類型衝突時，上傳套件不會取代現有的資料夾階層。 例如，如果您有一個名為「培訓」的適用性表單，其位置為/content/dam/formsanddocuments，位於單一伺服器上。 您可以下載適用性表單並在其他伺服器上傳表單。 第二台伺服器的相同位置也有一個名為「Training」的資料夾/content/dam/formsanddocuments。 上傳失敗。
   > * 只有 `form-power-user` 群組可上傳XDP檔案。



## 下載主題 {#downloading-a-theme}

您可以在 [!DNL AEM Forms] 供您用於其他專案或例項。 AEM可讓您以zip檔案的形式下載主題，以便上傳至執行個體。

若要下載主題：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示> **[!UICONTROL 導覽]** ![羅盤](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL 主題]**.
1. 選取主題並點選 **[!UICONTROL 下載]**. 主題會下載為封存（.zip檔案）。

## 上傳主題 {#uploading-a-theme}

您可以上傳並使用其他人在您的表單中建立的主題。 上傳主題：

1. 在Experience Manager中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL 主題]**.
1. 在主題頁上，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**.
1. 在「檔案上傳」提示中，瀏覽並選擇電腦上的主題包，然後按一下 **[!UICONTROL 上傳]**. 已上傳的主題可在主題頁面上使用。

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## 匯出工作流程應用程式 {#export-a-workflow-application}

您可以使用套件管理器來匯出工作流程應用程式。 此程式如下所列：

1. 開啟 [!DNL AEM Forms] 套件管理器。 套件管理器的URL為 `https://[server]:[port]/crx/packmgr`.
1. 按一下 **[!UICONTROL 建立套件]**. 此 **[!UICONTROL 新套件]** 對話框。
1. 指定套件的名稱、版本和群組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 然後開啟 **[!UICONTROL 篩選器]** 標籤。 按一下 **[!UICONTROL 新增篩選]**. 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemortgage。 按一下 **[!UICONTROL 新增規則]**.

1. 開啟 **[!UICONTROL 進階]** 標籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆寫]** 在ACL處理欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 建置]** 來建立套件。

   建置套件後，您可以下載套件並將其匯入至其他伺服器。 工作流程應用程式會顯示在上傳套件的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式正常工作，還導出相應的最適化表單和工作流模型與工作應用程式。

## 使用資料夾來組織適用性Forms、PDF forms和相關資產  {#folders-and-organizing-assets}

您可以使用資料夾來排列和組織資產。 在資料夾中組織檔案和資產可讓您將檔案分組，以便輕鬆管理。 您可以選取資料夾，然後選擇下載或刪除資料夾。 若要建立資料夾，請完成下列步驟：

### 建立資料夾 {#create-a-folder}

1. 登入 [!DNL AEM Forms] 例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**.
1. 輸入以下詳細資訊：

   * **[!UICONTROL 標題]**:資料夾的顯示名稱
   * **[!UICONTROL 名稱]**: *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會從標題自動填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 標題中輸入的任何其他特殊字元都會自動以連字型大小取代，系統會提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯。

1. 資產清單中的目前位置會顯示帶有您所定義標題的新資料夾。

   如果資料夾存在並指定名稱，則提交會失敗，並出現錯誤。 您可以將游標移至錯誤上以檢視錯誤訊息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 表徵圖，顯示在名稱欄位旁邊。

   您可以點選新建立的資料夾，以前往資料夾內，並在資料夾內建立資產或資料夾。 此外，您可以選取資料夾，並選擇將其排入佇列以供下載、刪除或編輯其名稱。


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Tap **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->
