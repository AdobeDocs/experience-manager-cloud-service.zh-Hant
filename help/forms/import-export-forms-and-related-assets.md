---
title: '匯入和匯出資產 '
seo-title: Import and export assets to [!DNL AEM Forms]
description: 您可以匯入和匯出適用性Forms和相關資產至AEM例項。 這有助於移轉表單或跨系統移動表單。
seo-description: You can import and export Adaptive Forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---


# 匯入和匯出資產 {#importing-and-exporting-assets-to-aem-forms}

您可以在不同的表單、主題、範本、檔案片段、主題和其他資產之間移動 [!DNL AEM Forms] 例項。 在將系統移轉或表單從開發或中繼伺服器移至生產伺服器時，需要進行此類移動。

針對透過 [!DNL AEM Forms] 支援UI，建議使用Forms UI來匯出或匯入。 不建議使用AEM Package Manager匯出或匯入這類資產。

## 下載或上傳Forms和檔案資產 {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] 使用者介面可讓您以AEM CRX套件或二進位檔案的形式下載資產，以從AEM例項匯出資產。 然後，您可以將下載的AEM CRX套件或二進位檔案匯入另一個AEM例項。

透過 [!DNL AEM Forms] 除「最適化表單範本」和「最適化表單」內容原則外，所有資產均支援使用者介面。 因此，從 [!DNL AEM Forms] 與其他相關資產一樣，系統不會自動匯出UI、相關適用性表單範本和內容原則。

對於這些資產類型，您必須使用AEM Package Manager在來源AEM伺服器上建立CRX套件，並在目標伺服器上安裝套件。 有關建立和安裝軟體包的資訊，請參閱 [部署至AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html).

### 下載Forms和檔案資產 {#download-forms-amp-documents-assets}

若要下載Forms和檔案資產：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取表單資產，然後點選 **[!UICONTROL 下載]** 表徵圖。
1. 在「下載資產」中，選擇下列其中一個選項，然後點選 **[!UICONTROL 下載]**.

   * **下載為CRX套件：** 使用選項，從 [!DNL AEM Forms] 例項。 它會以crx套件下載所有資產和資料夾。 任何表單資產，包括在AEM中製作的表單(適用性Forms和適用性表單片段)、PDF檔案和資源（XSD、XFS、影像），都可從以套件形式下載 [!DNL AEM Forms] UI。
以套件形式下載資產的好處，在於也會下載被選取下載的資產所使用的資產。 例如，如果您的適用性表單使用表單範本、XSD和影像。 當您選取此適用性表單並以套件形式下載時，下載的套件也會包含表單範本、XSD和影像。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。

   * **以二進位檔案形式下載資產：** 使用選項僅下載表單模板(XDP)、PDF forms(PDF)、文檔(PDF)和資源（影像、結構、樣式表）。 您可以使用外部應用程式編輯這些資產。 它會以.zip檔案的形式下載含有二進位檔的表單資產，例如XSD、XDP、影像、PDF和XDP。
您無法下載適用性Forms、適用性表單片段和主題，具有 **[!UICONTROL 以二進位檔案形式下載資產]** 選項。 若要下載這些資產，您應使用 **[!UICONTROL 下載為CRX套件]** 選項。

   選取的資產會以封存檔（.zip檔案）的形式下載。

   >[!NOTE]
   >
   >AEM套件和二進位檔案都會以封存檔（.zip檔案）的形式下載。 系統不會隨資產下載資產的範本。 您需要個別匯出資產範本。

### 上傳資產 {#upload-forms-amp-documents-assets}

上傳Forms和檔案資產：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** >**檔案上傳**. 上傳表單或套件對話方塊隨即顯示。
1. 在對話方塊中，瀏覽並選取要匯入的套件或封存。 您也可以選擇PDF文檔、XSD、影像、樣式表和XDP表單。 點選 **[!UICONTROL 開啟]**. 所選資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，驗證要上傳之資產的詳細資訊，然後點選 **[!UICONTROL 上傳]**.

   如果您上傳現有的表單資產，資產便會更新。

   >[!NOTE]
   >
   >上傳套件不會取代現有的資料夾階層。 例如，如果您有一個名為「培訓」的適用性表單，其位置為/content/dam/formsanddocuments，位於單一伺服器上。 您可以下載適用性表單並在其他伺服器上傳表單。 第二台伺服器的相同位置/content/dam/formsanddocuments也有一個名為「Training」的資料夾。 上傳失敗。

## 下載或上傳主題 {#downloading-or-uploading-a-theme}

使用 [!DNL AEM Forms]，您可以建立、下載或上傳主題。 主題的建立方式與其他資產（如表單、檔案和信函）相同。 您可以建立主題、下載主題，然後將其上傳至個別例項以重複使用。 如需主題的詳細資訊，請參閱 [主題](themes.md) in [!DNL AEM Forms].

### 下載主題 {#downloading-a-theme}

您可以在 [!DNL AEM Forms] 供您用於其他專案或例項。 AEM可讓您以zip檔案的形式下載主題，以便上傳至執行個體。

若要下載主題：

1. 登入 [!DNL AEM Forms] 例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL 主題]**.
1. 選取主題並點選 **[!UICONTROL 下載]**. 主題會下載為封存（.zip檔案）。

### 上傳主題 {#uploading-a-theme}

您可以在專案上使用具有樣式預設集的已建立主題。 您可以在您的專案上上傳其他人建立的主題套件，借此匯入這些套件。

上傳主題：

1. 在Experience Manager中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL Forms主題]**.
1. 在主題頁中，按一下 **[!UICONTROL Forms建立]** > **[!UICONTROL Forms檔案上傳]**.
1. 在「檔案上傳」提示中，瀏覽並選擇電腦上的主題包，然後按一下 **[!UICONTROL Forms上傳]**. 主題已上傳。

<!--

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

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

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

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
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## 匯出工作流程應用程式 {#export-a-workflow-application}

您可以使用AEM套件管理器來匯出工作流程應用程式。 此程式如下所列：

1. 開啟 [!DNL AEM Forms] 套件管理器。
1. 按一下 **[!UICONTROL 建立套件]**. 此 **[!UICONTROL 新套件]** 對話框。
1. 指定套件的名稱、版本和群組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 然後開啟 **[!UICONTROL 篩選器]** 標籤。 按一下 **[!UICONTROL 新增篩選]**. 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemortgage。 按一下 **[!UICONTROL 新增規則]**.

1. 開啟 **[!UICONTROL 進階]** 標籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆寫]** 在ACL處理欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 建置]** 來建立套件。

   建置套件後，您可以下載套件並將其匯入至其他伺服器。 工作流程應用程式會顯示在上傳套件的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式正常工作，還導出與工作應用程式對應的最適化表單和工作流模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

[!DNL AEM Forms] 使用者介面使用資料夾來排列資產。 這些資料夾可用來排列在中建立的資產 [!DNL AEM Forms] 使用者介面。 您可以重新命名、建立子資料夾，以及儲存這些資料夾中的資產和檔案。 在資料夾中組織檔案和資產可讓您將檔案分組，以方便管理。 您可以選取資料夾，然後選擇下載或刪除資料夾。

若要建立資料夾，請完成下列步驟：

### 建立資料夾 {#create-a-folder}

1. 登入 [!DNL AEM Forms] 使用者介面(於 `https://<server>:<port>/aem/forms.html`.
1. 導覽至您要建立資料夾的位置。
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**.
1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 標題中輸入的任何其他特殊字元都會自動以連字型大小取代，系統會提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯它。

1. 資產清單中的目前位置會顯示帶有您所定義標題的新資料夾。

   如果資料夾存在並指定名稱，則提交會失敗，並出現錯誤。 您可以將游標移至錯誤上以檢視錯誤訊息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 表徵圖，顯示在名稱欄位旁邊。

   您可以點選新建立的資料夾，以前往資料夾內，並在資料夾內建立資產或資料夾。 此外，您可以選取資料夾，並選擇將其排入佇列以供下載、刪除或編輯其名稱。

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Tap Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI allows you to search your content. Using the top bar, you can tap Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->
