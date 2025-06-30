---
title: 管理 [!DNL Adobe Experience Manager]中的PDF檔案。
description: 管理 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]中的PDF檔案。
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 4%

---

# 在Experience Manager Assets as a Cloud Service中管理PDF檔案 {#add-assets-to-experience-manager}

Experience Manager Assets與Document Cloud PDF Viewer緊密整合，可讓您預覽PDF檔案的多個頁面。 此外，您也可以使用進階Document Cloud PDF檢視器功能，例如註解、搜尋文字、使用書籤和縮圖導覽PDF檔案，以及其他位於相同屋頂的功能。 Experience Manager Assets也可讓您上傳其他支援格式的檔案，以及以PDF格式預覽檔案。

Document Cloud PDF檢視器可透過下列方式為AEM Assets提供好處：

* [支援PDF Document Cloud Viewer元件](#pdf-doc-cloud)
* [支援PDF資產的多頁預覽和註解](#multi-page)
* [支援其他格式檔案的多頁預覽](#multi-format)

>[!TIP]
>
> 如果您無法取得先前上傳之PDF檔案的多頁預覽，請選取PDF並按一下「重新處理![」](/help/assets/assets/Reprocess.svg)**「重新處理Assets**」。

## 支援PDF Document Cloud Viewer元件 {#pdf-doc-cloud}

原生PDF Doc Cloud檢視器在AEM Assets中有下列元件：

* 使用頁面縮圖的&#x200B;**PDF檢視器**&#x200B;縮圖檢視是PDF檔案頁面的小型預覽。 使用縮圖，您可以直接跳至所需的頁面。 您可以透過左窗格上的![縮圖](/help/assets/assets/thumbnail.svg)存取所選PDF檔案的縮圖。

* **使用書籤的PDF檢視器**&#x200B;書籤是直接連結，可引導您前往檔案中的內容。 您可以透過左窗格上的![書籤](/help/assets/assets/bookmark.svg)存取所選PDF檔案的書籤。

* **在PDF中搜尋**&#x200B;您可以使用搜尋![搜尋](/help/assets/assets/Search.svg)在PDF檔案中尋找文字。

* **Page Up/Page Down**&#x200B;使用Page Up ![Page Up](/help/assets/assets/ArrowUp.svg)或Page Down ![Page Down](/help/assets/assets/ArrowDown.svg)捲動檔案。

* **縮小/放大**&#x200B;使用縮小![縮小](/help/assets/assets/Zoom-out.svg)或放大![放大](/help/assets/assets/zoom-in.svg)以串連檔案。

* **頁面符合**&#x200B;使用寬度或高度尺寸，以符合您熒幕大小的檔案大小。

* **固定/取消固定PDF**&#x200B;您可以使用此選項來固定或取消固定原生PDF檢視器的元件。

## 支援PDF資產的多頁預覽和註解 {#multi-page}

Adobe Experience Manager Assets可讓您預覽包含數個頁面的PDF檔案。 若要預覽PDF檔案的多個頁面，請考量下列步驟：

1. 請依照步驟[在AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=zh-Hant)中上傳資產。
1. 瀏覽您要上傳及預覽的PDF檔案。
1. 開啟檔案。
1. 依預設，PDF檔案檢視器會載入。 您也可以在「轉譯」面板下選取「PDF轉譯」 。
1. 在「轉譯」下拉式清單中，選取&#x200B;**所有轉譯**。

您也可以在多頁預覽中將[註解](#pdf-annotations)套用至PDF檔案。

>[!NOTE]
>
> 您可以預覽的資產大小上限為100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF註解{#pdf-annotations}**

Experience Manager Assets可讓您將註解新增至PDF檔案。 PDF檔案可以有多個附註。

若要為PDF檔案加上註釋，請執行以下步驟：

1. 前往Assets介面，導覽至您要加上註解的PDF檔案。 原生PDF檢視器會在右側開啟，顯示所選PDF檔案的預覽。
1. 按一下頂端功能表中的&#x200B;**註釋**。
以下是可套用至PDF檔案的註解：

<table>
        <tr>
             <th> 註解 </th>
            <th> 說明 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg">個註解 </td>
            <td> 選取「註解」以表示觀察。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg">文字方塊 </td>
            <td> 選取文字方塊以輸入文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg">註解 </td>
            <td> 新增小文字或提醒，提醒您可以新增到PDF上的特定區域。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg">文字熒光筆 </td>
            <td> 選取要以不同顏色反白的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg">個文字底線 </td>
            <td> 選取要加底線的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg">刪除線 </td>
            <td> 選取要刪去的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg">繪圖 </td>
            <td> 將視覺效果插圖插入PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg">拭除工程圖 </td>
             <td> 移除或復原工程圖。 </td>
        </tr>
    </table>

>[!NOTE]
>
>您新增至PDF檔案的註解可在預覽模式下使用。 不過，當您下載或列印PDF檔案時，不會顯示註解。

## 支援其他格式檔案的多頁預覽 {#multi-format}

除了PDF檔案之外，您還可以預覽其他格式型別檔案的多個頁面。 支援的檔案格式型別為TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets會自動將這些檔案格式轉換為PDF格式，並且可供預覽。

![其他格式的檔案的多頁預覽](/help/assets/assets/multi-page-other-formats.png)

對於其他支援檔案格式的多頁預覽，請執行下列步驟：

1. 請依照步驟[在AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=zh-Hant)中上傳資產。
1. 瀏覽您要上傳和預覽的檔案。
1. 開啟檔案。
1. 在左側面板的靜態區段下選取PDF 。 右側面板會顯示資產的多個頁面預覽。 從左側面板中選取縮圖，以選擇要預覽的頁面。

>[!NOTE]
>
> * 您可以預覽的資產大小上限為100 MB。
> * 要預覽的XLS或XLSX檔案大小上限為20 MB。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
