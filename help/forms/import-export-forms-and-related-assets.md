---
title: '導入和導出資產 '
seo-title: Import and export assets to [!DNL AEM Forms]
description: 您可以將Adaptive Forms和相關資產導入和導出到實AEM例。 這有助於遷移表單或跨系統移動表單。
seo-description: You can import and export Adaptive Forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---


# 導入和導出資產 {#importing-and-exporting-assets-to-aem-forms}

您可以在不同的表單、主題、模板、文檔片段、主題和其他資產之間移動 [!DNL AEM Forms] 實例。 在將系統或表單從開發伺服器或臨時伺服器遷移到生產伺服器時需要這種移動。

對於通過 [!DNL AEM Forms] 支援UI，建議使用FormsUI進行導出或導入。 建議不AEM要使用包管理器導出或導入此類資產。

## 下載或上載Forms和文檔資產 {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] 用戶介面允許您通過將資AEM產下載為AEMCRX包或二進位檔案來從實例導出資產。 然後，可以將下載AEM的CRX軟體包或二進位檔案導入另AEM一個實例。

通過 [!DNL AEM Forms] 除Adaptive Form模板和Adaptive Form內容策略外，所有資產都支援用戶介面。 因此，在從導出自適應窗體時 [!DNL AEM Forms] UI、相關的自適應表單模板和內容策略不會像其他相關資產一樣自動導出。

對於這些資產類型，必須AEM使用包管理器在源伺服器上創AEM建CRX包，並在目標伺服器上安裝包。 有關建立和安裝軟體包的資訊，請參見 [部署到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)。

### 下載Forms和文檔資產 {#download-forms-amp-documents-assets}

下載Forms和文檔資產：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇表單資產並點擊 **[!UICONTROL 下載]** 表徵圖
1. 在下載資產中，選擇以下選項之一，然後點擊 **[!UICONTROL 下載]**。

   * **下載為CRX包：** 使用此選項從 [!DNL AEM Forms] 例子。 它以crx包的形式下載所有資產和資料夾。 任何表單資產，包括在AEM(自適應Forms和自適應表單片段)、PDF文檔和資源（XSD、XFS、映像）中創作的表單，都可以作為包從 [!DNL AEM Forms] UI。
將資產作為包下載的好處是，它還下載被選擇下載的資產使用的資產。 例如，如果您有一個使用表單模板、XSD和影像的自適應表單。 選擇此自適應表單並將其作為包下載時，下載的包還包含表單模板、XSD和映像。 還下載與資產關聯的所有元資料屬性（包括自定義屬性）。

   * **將資產下載為二進位檔案：** 使用此選項只下載表單模板(XDP)、PDF forms(PDF)、文檔(PDF)和資源（影像、架構、樣式表）。 您可以使用外部應用程式編輯這些資產。 它將包含二進位檔案的表單資產(如XSD、XDP、映像、PDF和XDP)下載為.zip檔案。
無法下載自適應Forms、自適應表單片段和主題， **[!UICONTROL 將資產下載為二進位檔案]** 的雙曲餘切值。 要下載這些資產，您應使用 **[!UICONTROL 下載為CRX包]** 的雙曲餘切值。

   選定的資產將作為存檔（.zip檔案）下載。

   >[!NOTE]
   >
   >包文AEM件和二進位檔案都作為存檔檔案（.zip檔案）下載。 不會隨資產一起下載資產模板。 您需要單獨導出資產模板。

### 上載資產 {#upload-forms-amp-documents-assets}

要上載Forms和文檔資產：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **建立** >**檔案上載**。 將出現上載表單或包對話框。
1. 在對話框中，瀏覽並選擇要導入的包或存檔。 您還可以選擇PDF文檔、XSD、影像、樣式表和XDP表單。 點擊 **[!UICONTROL 開啟]**。 您選擇的資料夾或檔案名不得包含任何特殊字元。

   在對話框中，驗證上載的資產的詳細資訊，然後點擊 **[!UICONTROL 上載]**。

   如果您上載現有的表單資產，則會更新該資產。

   >[!NOTE]
   >
   >上載包不會替換現有資料夾層次結構。 例如，如果在一台伺服器上的/content/dam/formsanddocuments位置有一個名為「Training」的Adaptive Form。 您可以下載Adaptive Form，然後將表單上載到另一台伺服器上。 第二台伺服器在同一位置/content/dam/formsanddocuments還有一個名為「Training」的資料夾。 上載失敗。

## 下載或上載主題 {#downloading-or-uploading-a-theme}

與 [!DNL AEM Forms]，您可以建立、下載或上載主題。 建立主題時與表單、文檔和字母等其他資產類似。 您可以建立主題，下載主題，然後將其上載到單獨的實例上以重新使用主題。 有關主題的詳細資訊，請參見 [主題](themes.md) 在 [!DNL AEM Forms]。

### 下載主題 {#downloading-a-theme}

可以在中導出主題 [!DNL AEM Forms] 可用於其他項目或實例。 可AEM以將主題作為zip檔案下載，並可以在實例上載。

下載主題：

1. 登錄到 [!DNL AEM Forms] 實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/Smock_Compass_18_N.svg) 表徵圖> **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。
1. 選擇主題並點擊 **[!UICONTROL 下載]**。 主題將作為存檔檔案（.zip檔案）下載。

### 上載主題 {#uploading-a-theme}

可以將建立的主題與項目上的樣式預設一起使用。 您可以通過將其他人建立的主題包上載到項目中來導入它們。

上載主題：

1. 在Experience Manager中，導航到 **[!UICONTROL Forms]** > **[!UICONTROL Forms主題]**。
1. 在「主題」頁中，按一下 **[!UICONTROL Forms建立]** > **[!UICONTROL Forms檔案上載]**。
1. 在「File Upload（檔案上載）」提示符下，瀏覽並選擇電腦上的主題包，然後按一下 **[!UICONTROL Forms上傳]**。 主題已上載。

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

## 導出工作流應用程式 {#export-a-workflow-application}

可以使用包管AEM理器導出工作流應用程式。 此過程如下所列：

1. 開啟 [!DNL AEM Forms] 包管理器。
1. 按一下 **[!UICONTROL 建立包]**。 的 **[!UICONTROL 新建包]** 對話框。
1. 指定包的名稱、版本和組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 開啟 **[!UICONTROL 篩選器]** 頁籤。 按一下 **[!UICONTROL 添加篩選器]**。 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemtorgage。 按一下 **[!UICONTROL 添加規則]**。

1. 開啟 **[!UICONTROL 高級]** 頁籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆蓋]** 在「ACL處理」欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 生成]** 的子菜單。

   生成包後，您可以下載該包並將其導入到其他伺服器。 工作流應用程式出現在上載包的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式正常工作，還導出了相應的自適應表單和工作流模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

[!DNL AEM Forms] 用戶介面使用資料夾來排列資產。 這些資料夾用於安排在 [!DNL AEM Forms] 用戶介面。 您可以更名、建立子資料夾，並將這些資料夾中的資產和文檔儲存。 將文檔和資產組織在資料夾中，可以將檔案分組在一起，以便於管理。 您可以選擇資料夾並選擇下載或刪除它。

要建立資料夾，請完成以下步驟：

### 建立資料夾 {#create-a-folder}

1. 登錄到 [!DNL AEM Forms] 用戶介面 `https://<server>:<port>/aem/forms.html`。
1. 導航到要在其下建立資料夾的位置。
1. 點擊 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。
1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >預設情況下，名稱欄位的值會自動從標題中填充。 名稱只能包含字母數字字元或連字元(-)和下划線(_)特殊字元。 在標題中輸入的任何其他特殊字元將自動替換為連字元，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯它。

1. 在資產清單的當前位置顯示具有您定義的標題的新資料夾。

   如果存在具有指定名稱的資料夾，則提交將失敗並出現錯誤。 通過懸停在錯誤上方，可以查看錯誤消息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 表徵圖。

   您可以點擊新建立的資料夾進入資料夾並在資料夾中建立資產或資料夾。 此外，您可以選擇資料夾並選擇將其排入隊列以便下載、刪除或編輯其名稱。

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
