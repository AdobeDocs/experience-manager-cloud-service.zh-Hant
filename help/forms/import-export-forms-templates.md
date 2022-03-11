---
title: 進口、出口和組織自適應Forms、PDF forms和其他資產
seo-title: Learn to import, export, and organize Adaptive Forms, PDF forms, and other assets on an[!DNL AEM Forms] instance
description: '希望將Adaptive Forms和資產遷移到實例AEM或遷移？ 在此處瞭解如何從AdaptiveForms、PDF forms、主題和其他支援資產 [!DNL AEM Forms] 實例。 '
seo-description: Looking to migrate Adaptive Forms and assets to and from an AEM instances? Learn here how to import and export Adaptive Forms, PDF forms, themes, and other supporting assets from an [!DNL AEM Forms] instance.
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 1%

---

# 匯入、匯出及組織最適化表單、PDF 表單和其他資產{#importing-and-exporting-assets-to-aem-forms}

您可以在以下位置之間移動自適應Forms和相關資產：自適應表單主題、表單資料模型、自適應表單模板、文檔片段和PDF forms [!DNL AEM Forms] 實例。 可以以CRX包或二進位檔案格式導入和導出資產。

導出自適應表單時，不會導出內容策略和模板。 使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) 以導出這些資產。

## 下載AdaptiveForms、PDF forms或相關資產 {#download-forms-amp-documents-assets}

要下載表單或相關資產，請執行以下操作：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊 **[!UICONTROL Adobe Experience Manager]** ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 **[!UICONTROL 導航]** ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇資產並點擊 **[!UICONTROL 下載]** 表徵圖
1. In the Download Asset(s), choose one of the following options, and tap **[!UICONTROL Download]**.

   * **下載為CRX包：** 使用此選項從 [!DNL AEM Forms] 例子。 It downloads all assets and folders as a CRX package including the forms authored in AEM (Adaptive Forms and Adaptive Form Fragments), form sets, form data model, form templates, PDF documents, and referenced resources (XSDs and images).
The advantage of downloading assets as a package is that it also downloads referenced by selected assets. For example, If you have an Adaptive Form that uses a form template, XSD, and an image. When you select this Adaptive Form and download it as a package, the downloaded package also contains the form template, XSD, and the image. 還下載與資產關聯的所有元資料屬性（包括自定義屬性）。

   * **Download asset(s) as binary files:** Use the option to download only form templates (XDP), PDF forms (PDF), document (PDF), and resources (images, schemas, stylesheets). 您可以使用外部應用程式編輯這些資產。 It downloads the assets that have binaries, such as images, PDFs, and other supported formats  as a .zip file.
您無法下載帶有的自適應Forms、自適應表單片段、主題和表單集 **[!UICONTROL 將資產下載為二進位檔案]** 的雙曲餘切值。 要下載這些資產，您應使用 **[!UICONTROL 下載為CRX包]** 的雙曲餘切值。

   選定的資產將作為存檔（.zip檔案）下載。

   >[!NOTE]
   >
   >包文AEM件和二進位檔案都作為存檔檔案（.zip檔案）下載。 不會隨資產一起下載資產模板。 您需要單獨導出資產模板。

## 上載自適應Forms、PDF forms或相關資產 {#upload-forms-amp-documents-assets}

您可以單獨或作為ZIP存檔上載受支援的資產類型。 對於ZIP檔案，將顯示所有受支援資產的相對路徑。 ZIP中不支援的資產將被忽略，且未列出。 但是，如果ZIP存檔中只包含不受支援的資產，則會顯示一條錯誤消息，而不是彈出對話框。
要上載表單或相關資產，請執行以下操作：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊 **[!UICONTROL Adobe Experience Manager]** ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 **[!UICONTROL 導航]** ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上載]**。 對話方塊隨即顯示。
1. 在對話框中，瀏覽並選擇要導入的包或存檔。 也可以選擇其他支援的檔案類型。 點擊 **[!UICONTROL 開啟]**。 您選擇的資料夾或檔案名不得包含任何特殊字元。

   在對話框中，驗證上載的資產的詳細資訊，然後點擊 **[!UICONTROL 上載]**。

   如果您上載現有的表單資產，則會更新該資產。

   >[!NOTE]
   >
   > * 當名稱與不同的資源類型衝突時，上載包不會替換現有資料夾層次結構。 例如，如果在一台伺服器上的/content/dam/formsanddocuments位置有一個名為「Training」的Adaptive Form。 您可以下載Adaptive Form，然後將表單上載到另一台伺服器上。 第二台伺服器在同一位置/content/dam/formsanddocuments還有一個名為「Training」的資料夾。 上載失敗。
   > * 只有 `form-power-user` 組可以上載XDP檔案。



## 下載主題 {#downloading-a-theme}

可以在中導出主題 [!DNL AEM Forms] 可用於其他項目或實例。 可AEM以將主題作為zip檔案下載，並可以在實例上載。

下載主題：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊 **[!UICONTROL Adobe Experience Manager]** ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 **[!UICONTROL 導航]** ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖 **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。
1. 選擇主題並點擊 **[!UICONTROL 下載]**。 主題將作為存檔檔案（.zip檔案）下載。

## 上載主題 {#uploading-a-theme}

您可以上載和使用其他人在您的表單中建立的主題。 To upload a theme:

1. 在Experience Manager中，導航到 **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。
1. 在「主題」頁面上，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上載]**。
1. 在「File Upload（檔案上載）」提示符下，瀏覽並選擇電腦上的主題包，然後按一下 **[!UICONTROL 上載]**。 上載的主題可在主題頁面上找到。

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

## 導出工作流應用程式 {#export-a-workflow-application}

可以使用包管理器導出工作流應用程式。 此過程如下所列：

1. 開啟 [!DNL AEM Forms] 包管理器。 包管理器的URL是 `https://[server]:[port]/crx/packmgr`。
1. 按一下 **[!UICONTROL 建立包]**。 的 **[!UICONTROL 新建包]** 對話框。
1. 指定包的名稱、版本和組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 開啟 **[!UICONTROL 篩選器]** 頁籤。 按一下 **[!UICONTROL 添加篩選器]**。 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemtorgage。 按一下 **[!UICONTROL 添加規則]**。

1. 開啟 **[!UICONTROL 高級]** 頁籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆蓋]** 在「ACL處理」欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. Click **[!UICONTROL Build]** to create the package.

   生成包後，您可以下載該包並將其導入到其他伺服器。 工作流應用程式出現在上載包的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式正常工作，還導出了相應的自適應表單和工作流模型。

## 使用資料夾組織AdaptiveForms、PDF forms和相關資產  {#folders-and-organizing-assets}

您可以使用資料夾來排列和組織資產。 將文檔和資產組織在資料夾中，使您可以對檔案進行分組，以便輕鬆管理。 您可以選擇資料夾並選擇下載或刪除它。 要建立資料夾，請完成以下步驟：

### 建立資料夾 {#create-a-folder}

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。
1. 輸入以下詳細資訊：

   * **[!UICONTROL 標題]**:資料夾的顯示名稱
   * **[!UICONTROL Name]**: *(Mandatory)* The node name under which you want to store the folder in the repository

   >[!NOTE]
   >
   >預設情況下，名稱欄位的值會自動從標題中填充。 The name can only contain alphanumeric characters, or the hyphen (-) and underscore (_) special characters. 在標題中輸入的任何其他特殊字元將自動替換為連字元，並提示您確認新名稱。 You can choose to continue with the suggested name or edit it further.

1. 在資產清單的當前位置顯示具有您定義的標題的新資料夾。

   如果存在具有指定名稱的資料夾，則提交將失敗並出現錯誤。 通過懸停在錯誤上方，可以查看錯誤消息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 表徵圖。

   您可以點擊新建立的資料夾進入資料夾並在資料夾中建立資產或資料夾。 此外，您可以選擇資料夾並選擇將其排入隊列以便下載、刪除或編輯其名稱。


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
