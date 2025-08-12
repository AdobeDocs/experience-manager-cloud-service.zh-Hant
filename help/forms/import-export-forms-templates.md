---
title: 如何在AEM Forms執行個體上匯入、匯出及組織最適化Forms或PDF forms？
description: 瞭解如何移轉最適化Forms、PDF forms、主題和其他支援資產到AEM執行個體，以及從中移轉這些資產。
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---

# 匯入或匯出最適化Forms和AEM Forms資產 {#importing-and-exporting-assets-to-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service  | 本文章 |

您可以在[!DNL AEM Forms]個執行個體之間移動最適化Forms和相關資產，例如最適化表單主題、表單資料模型(FDM)、最適化表單範本、片段和PDF forms。

## 下載最適化Forms、PDF forms或相關資產 {#download-forms-amp-documents-assets}

若要下載表單或相關資產：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

   ![選取Forms](/help/forms/assets/select-forms.png)

1. 選取資產，然後按一下上方邊欄中的&#x200B;**[!UICONTROL 下載]**&#x200B;圖示。

   ![下載Forms](/help/forms/assets/download-form.png)

   下載表單時，會出現&#x200B;**[!UICONTROL 下載資產]**&#x200B;對話方塊。

   ![下載表單資產](/help/forms/assets/download-form-assets.png)

1. 按一下「**[!UICONTROL 下載]**」。

選取的資產會下載為封存（.zip檔案）。

## 上傳最適化Forms、PDF forms或相關資產 {#upload-forms-amp-documents-assets}

您可以個別上傳支援的資產型別，或以ZIP封存檔的形式上傳。 對於ZIP檔案，會顯示所有支援資產的相對路徑。 ZIP內不支援的資產會遭忽略，不會列出。 不過，如果ZIP封存僅包含不支援的資產，則會顯示錯誤訊息，而非快顯對話方塊。
若要上傳表單或相關資產：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

   ![選取Forms](/help/forms/assets/select-forms.png)

1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**。 對話方塊隨即顯示。

   ![上傳Forms](/help/forms/assets/form-upload.png)

1. 在對話方塊中，瀏覽並選取要匯入的封裝或封存。 您也可以選取其他支援的檔案型別。 選取&#x200B;**[!UICONTROL 開啟]**。 您選取的資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，確認要上傳之資產的詳細資料，並選取&#x200B;**[!UICONTROL 上傳]**。

   如果上傳現有的表單資產，資產會隨之更新。

   >[!NOTE]
   >
   > 當名稱與不同的資源型別衝突時，上傳套件不會取代現有的資料夾階層。 例如，如果一台伺服器上的位置`/content/dam/formsanddocuments`有一個名為&#39;Training&#39;的最適化表單。 您可以下載最適化表單並將表單上傳到其他伺服器。 第二個伺服器的相同位置`/content/dam/formsanddocuments`也有一個名為&#39;Training&#39;的資料夾。 上傳失敗。

## 下載主題

您可以匯出[!DNL AEM Forms]中可用於其他專案或執行個體的主題。 AEM可讓您將主題下載為zip檔案，以便在執行個體上傳。
若要下載佈景主題：

1. 登入您的 [!DNL Experience Manager Forms] 作者實例。
1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 主題]**。

   ![選取主題](/help/forms/assets/select-theme.png)

1. 在「佈景主題」頁面上，選取佈景主題，然後從上方邊欄按一下&#x200B;**[!UICONTROL 下載]**&#x200B;圖示。

   ![下載主題](/help/forms/assets/download-theme.png)

   下載主題時，會出現&#x200B;**[!UICONTROL 下載資產]**&#x200B;對話方塊。

   ![下載主題資產](/help/forms/assets/download-theme-asset.png)

1. 按一下「**[!UICONTROL 下載]**」。

選取的資產會下載為封存（.zip檔案）。

## 上傳主題 {#uploading-a-theme}

您可以上傳並使用其他人在您的表單中建立的主題。
上傳佈景主題：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 在Experience Manager中，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 主題]**。

   ![選取主題](/help/forms/assets/select-theme.png)

1. 在[佈景主題]頁面上，按一下[建立&#x200B;**&#x200B; > [檔案上傳]**]。**&#x200B;**

   ![上傳佈景主題](/help/forms/assets/theme-upload.png)

1. 瀏覽並選取您電腦上的主題封裝，然後按一下&#x200B;**[!UICONTROL 上傳]**。 上傳的主題即會顯示在「主題」頁面上。

## 使用資料夾整理Adaptive Forms、PDF forms和相關資產  {#folders-and-organizing-assets}

您可以使用資料夾來排列及組織資產。 在資料夾中組織檔案和資產可讓您將檔案分組，以方便管理。 您可以選取資料夾，然後選擇下載或刪除資料夾。

### 建立資料夾 {#create-a-folder}

若要建立資料夾：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

   ![選取表單](/help/forms/assets/select-forms.png)

1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。

   ![建立資料夾](/help/forms/assets/create-folder.png)

   **[!UICONTROL 新增資料夾]**&#x200B;對話方塊就會顯示。
1. 輸入&#x200B;**[!UICONTROL 標題]**。 當您輸入&#x200B;**[!UICONTROL 標題]**&#x200B;時，**[!UICONTROL 名稱]**&#x200B;會自動填入。

   ![新增資料夾](/help/forms/assets/add-folder.png)

1. 按一下「**[!UICONTROL 建立]**」。

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 在標題中輸入的任何其他特殊字元都會自動取代為連字型大小，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯。

具有您定義標題的新資料夾會顯示在資產清單中的目前位置。

如果具有指定名稱的資料夾存在，則提交會失敗並出現錯誤。 您可以將游標移至名稱欄位旁邊顯示的錯誤![aem6forms_error_alert](assets/Smock_Alert_18_N.svg)圖示上，以檢視錯誤訊息。

您可以選取建立的資料夾以移至資料夾內，並在資料夾內建立資產或資料夾。 此外，您可以選取資料夾，並選擇將資料夾排入下載佇列、刪除資料夾或編輯資料夾名稱。

### 建立一個或多個資產的副本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用現有資產，快速建立具有類似屬性、內容和繼承資產的資產。

若要建立資產復本：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 在相關的資產頁面上，選取一或多個資產。 UI顯示&#x200B;**[!UICONTROL 複製]**&#x200B;圖示。
1. 選取&#x200B;**[!UICONTROL 複製]**。 UI會顯示![貼上圖示](/help/forms/assets/Smock_Paste_18_N.svg)圖示。

   ![複製資產](/help/forms/assets/copy-asset.png)

   您也可以在貼上之前，選擇在資料夾中前往/導覽。 不同的資料夾可以包含具有相同名稱的資產。 如需資料夾的詳細資訊，請參閱[資料夾及組織資產](#folders-and-organizing-assets)。
1. 選取&#x200B;**[!UICONTROL 貼上]**。

   ![貼上資產](/help/forms/assets/paste-asset.png)

1. **[!UICONTROL 貼上]**&#x200B;對話方塊就會顯示。 系統會自動產生資產新復本的名稱和標題，但您可以編輯資產的標題和名稱。

   如果您要在相同位置複製和貼上資產，系統會將尾碼「 — CopyXX」新增至「`asset`」的現有名稱。 如果複製的資產沒有標題，自動產生的標題欄位會維持空白。

   ![在新位置貼上資產](/help/forms/assets/paste-click-asset.png)

   如有必要，請編輯您想要用來儲存資產復本的&#x200B;**[!UICONTROL 標題]**。 當您輸入&#x200B;**[!UICONTROL 標題]**&#x200B;時，**[!UICONTROL 名稱]**&#x200B;會自動填入。
1. 選取&#x200B;**[!UICONTROL 貼上]**。 複製的資產會建立新復本。

## 搜尋 {#search-forms}

當您擁有大量資產時，搜尋合適的資產相當耗時。 您可以在資產頁面上執行特定資產的文字式搜尋。

若要搜尋資產：

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 按一下![搜尋圖示](assets/folder-search-icon.svg)搜尋圖示。

   ![搜尋表單](/help/forms/assets/search-form.png)

1. 在搜尋列中輸入您要搜尋的資產名稱。

1. 相關資產清單隨即顯示。 從顯示的資產清單中選取所需的資產。

   ![搜尋資產](/help/forms/assets/search-bar.png)

如需有關使用搜尋的詳細資訊與指示，請參閱[搜尋](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=zh-Hant)。

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## 另請參閱 {#see-also}

{{see-also}}
