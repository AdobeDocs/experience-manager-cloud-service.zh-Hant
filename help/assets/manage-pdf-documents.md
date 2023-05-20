---
title: 管理PDF文檔 [!DNL Adobe Experience Manager]。
description: 管理PDF文檔 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# 在Experience Manager Assetsas a Cloud Service中管理PDF文檔 {#add-assets-to-experience-manager}

Experience Manager Assets與Document CloudPDF查看器無縫整合，允許您預覽PDF文檔的多頁。 此外，您還可以使用高級Document CloudPDF查看器功能，如批注、搜索文本、使用書籤和縮略圖瀏覽PDF文檔等，等等。 Experience Manager Assets還允許您以其他支援格式上載文檔，並以PDF格式預覽文檔。

Document CloudPDF查看器通過以下方式為AEM Assets帶來好處：
* [支援PDFDocument Cloud查看器元件](#pdf-doc-cloud)
* [支援多頁預覽和注釋PDF資產](#multi-page)
* [支援其他格式文檔的多頁預覽](#multi-format)

> 提示
> 如果無法獲取先前上載的PDF文檔的多頁預覽，請選擇PDF並按一下 **![重新處理](/help/assets/assets/Reprocess.svg) 重新處理資產**。

## 支援PDFDocument Cloud查看器元件 {#pdf-doc-cloud}

本機PDF文檔雲查看器在AEM Assets具有以下元件：

* **PDF使用頁面縮略圖的查看器** 縮略圖視圖是PDF文檔頁面的小預覽。 使用縮略圖，您可以直接跳轉到所需頁面。 您可以通過以下方式訪問所選PDF文檔的縮略圖 ![縮略圖](/help/assets/assets/thumbnail.svg) 的下界。

* **使用書籤的PDF查看器** 書籤是一個直接連結，用於導航到文檔中的內容。 您可以通過以下方式訪問所選PDF文檔的書籤 ![書籤](/help/assets/assets/bookmark.svg) 的下界。

* **在PDF中搜索** 您可以使用搜索 ![搜索](/help/assets/assets/Search.svg) 查找PDF文檔中的文本。

* **上/下頁** 使用上頁 ![上頁](/help/assets/assets/ArrowUp.svg) 或下頁 ![向下頁](/help/assets/assets/ArrowDown.svg) 來瀏覽文檔。

* **縮小/放大** 使用縮小 ![縮小](/help/assets/assets/ZoomOut.svg) 或放大 ![放大](/help/assets/assets/ZoomIn.svg) 來掃描文檔。

* **頁面大小** 使用寬度或高度尺寸根據螢幕大小調整文檔。

* **停靠/取消停靠PDF** 可以使用此選項將本機PDF查看器的元件停靠或取消停靠。

## 支援多頁預覽和注釋PDF資產 {#multi-page}

Adobe Experience Manager資產允許您預覽包含幾頁的PDF文檔。 要預覽PDF文檔的多頁，請考慮以下步驟：

1. 按照步驟執行 [上載資產AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en)。
1. 瀏覽要上載和預覽的PDF文檔。
1. 開啟文檔。
1. 預設情況下，PDF文檔查看器將載入。 也可以在PDF面板下選擇格式副本。
1. 在「格式副本」下拉下拉清單中，選擇 **所有格式副本**。

您也可以應用 [注釋](#pdf-annotations) 到PDF文檔。

> 注意
> 可預覽的資產的最大大小為100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF注釋{#pdf-annotations}**

Experience Manager Assets允許您向PDF文檔添加註釋。 PDF文檔可以具有多個批注。

要注釋PDF文檔，請執行以下步驟：
1. 轉至「資產」介面，導航到要批注的PDF文檔。 本機PDF查看器將在右側開啟，顯示所選PDF文檔的預覽。
1. 按一下 **注釋** 的上界。
以下是可應用於PDF文檔的注釋：

<table>
        <tr>
             <th> 附註 </th>
            <th> 說明 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> 評論 </td>
            <td> 選擇注釋以表示觀察。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> 文本框 </td>
            <td> 選擇文本框以輸入文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 便箋 </td>
            <td> 添加小文本或提醒，以便您可以添加到PDF的特定區域。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> 文字螢光筆 </td>
            <td> 選擇要以不同顏色加亮的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> 文本底線 </td>
            <td> 選擇要下划線的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> 刪除 </td>
            <td> 選擇要划出的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 繪圖 </td>
            <td> 將視覺藝術插入PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 拭除繪圖 </td>
             <td> 刪除或撤消繪圖。 </td>
        </tr>
    </table>

## 支援其他格式文檔的多頁預覽 {#multi-format}

除PDF文檔外，您還可以預覽其他格式類型文檔的多頁。 支援的文檔格式類型為TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets會自動將這些文檔格式轉換為PDF格式，並使其可用於預覽。

![多頁預覽其他格式的文檔](/help/assets/assets/multi-page-other-formats.png)

對於其它支援的文檔格式的多頁預覽，請執行以下步驟：
1. 按照步驟執行 [上載資產AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en)。
1. 瀏覽要上載和預覽的文檔。
1. 開啟文檔。
1. 在左側面板的靜態部分下選擇PDF。 右面板顯示資產的多頁預覽。 從左面板中選擇縮略圖以選擇要預覽的頁面。

> 注意
> * 可預覽的資產的最大大小為100 MB。
> * 要預覽的XLS或XLSX檔案的最大大小為20 MB。
>


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
