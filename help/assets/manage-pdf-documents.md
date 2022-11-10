---
title: 在 [!DNL Adobe Experience Manager].
description: 在中管理PDF檔案 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
source-git-commit: 9a600fb744c7064274fb4d849a5e01de2b83f575
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# 在Experience Manager Assets中管理PDF檔案as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets可與Document CloudPDF檢視器流暢整合，讓您預覽PDF檔案的多個頁面。 此外，您還可以使用高級Document CloudPDF查看器功能，如注釋、搜索文本、使用書籤和縮圖導航PDF文檔，以及在同一屋頂下的更多功能。 Experience Manager Assets也可讓您上傳其他支援格式的檔案，並以PDF格式預覽。

Document CloudPDF檢視器可讓AEM Assets以下列方式受益：
* [支援PDFDocument Cloud檢視器元件](#pdf-doc-cloud)
* [支援PDF資產的多頁預覽和註解](#multi-page)
* [支援其他格式的文檔的多頁預覽](#multi-format)

> 提示
> 如果您無法取得先前上傳之PDF檔案的多個頁面預覽，請選取PDF，然後按一下 **![重新處理](/help/assets/assets/Reprocess.svg) 重新處理資產**.

## 支援PDFDocument Cloud檢視器元件 {#pdf-doc-cloud}

原生PDFDoc Cloud檢視器在AEM Assets中有下列元件：

* **PDF檢視器（使用頁面縮圖）** 縮圖視圖是PDF文檔頁面的小預覽。 使用縮圖，您可以直接跳至所需的頁面。 您可以通過以下方式訪問所選PDF文檔的縮略圖： ![縮圖](/help/assets/assets/thumbnail.svg) 在左窗格中。

* **使用書籤的PDF檢視器** 書籤是將您導覽至檔案內容的直接連結。 您可以通過以下方式訪問所選PDF文檔的書籤： ![書籤](/help/assets/assets/bookmark.svg) 在左窗格中。

* **在PDF中搜尋** 您可以使用搜尋 ![搜尋](/help/assets/assets/Search.svg) 查找PDF文檔中的文本。

* **上/下頁** 向上使用頁面 ![向上頁面](/help/assets/assets/ArrowUp.svg) 或頁面向下 ![向下頁面](/help/assets/assets/ArrowDown.svg) 來滾動文檔。

* **縮小/放大** 使用縮小 ![縮小顯示](/help/assets/assets/ZoomOut.svg) 或放大 ![放大顯示](/help/assets/assets/ZoomIn.svg) 來分析檔案。

* **頁面大小** 根據螢幕大小使用寬度或高度尺寸來調整文檔。

* **停靠/取消停靠PDF** 您可以使用此選項固定或取消固定本機PDF檢視器的元件。

## 支援PDF資產的多頁預覽和註解 {#multi-page}

Adobe Experience Manager Assets可讓您預覽包含數個頁面的PDF檔案。 要預覽PDF文檔的多頁，請考慮以下步驟：

1. 請依照 [在AEM中上傳資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 瀏覽要上載和預覽的PDF文檔。
1. 開啟文檔。
1. 預設情況下，PDF文檔查看器將載入。 您也可以在轉譯面板下選取PDF轉譯。
1. 在「轉譯」下拉式清單下，選取 **所有轉譯**.

您也可以套用 [註解](#pdf-annotations) 預覽至PDF檔案。

> 注意
> 您可預覽的資產大小上限為100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF註解{#pdf-annotations}**

Experience Manager Assets可讓您將註解新增至PDF檔案。 PDF文檔可以有多個注釋。

要為PDF文檔添加註釋，請執行以下步驟：
1. 前往「PDF」介面，導覽至您要加上注釋的資產檔案。 原生PDF檢視器會在右側開啟，顯示所選PDF檔案的預覽。
1. 按一下 **注釋** 的上界。
以下是可應用於PDF文檔的注釋：

<table>
        <tr>
             <th> 附註 </th>
            <th> 說明 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> 評論 </td>
            <td> 選擇「注釋」(Comment)以表示觀察。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> 文字方塊 </td>
            <td> 選擇文本框以輸入文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 註解 </td>
            <td> 新增小型文字或提醒，讓您可以新增至PDF上的特定區域。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> 文字螢光筆 </td>
            <td> 選取要以不同顏色反白顯示的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> 文本底線 </td>
            <td> 選擇要加下划線的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> 三振 </td>
            <td> 選取要交叉的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 繪圖 </td>
            <td> 將視覺效果插入PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 拭除繪圖 </td>
             <td> 移除或撤消繪圖。 </td>
        </tr>
    </table>

## 支援其他格式的文檔的多頁預覽 {#multi-format}

除了PDF文檔之外，您還可以預覽其他格式類型的文檔的多個頁面。 支援的檔案格式類型為TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets會自動將這些檔案格式轉換為PDF格式，以供預覽。

![多頁預覽其他格式的文檔](/help/assets/assets/multi-page-other-formats.png)

對於其他支援的文檔格式的多頁預覽，請執行以下步驟：
1. 請依照 [在AEM中上傳資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 瀏覽要上載和預覽的文檔。
1. 開啟文檔。
1. 在左側面板的靜態區段下選取PDF。 右側面板會展示資產的多個頁面預覽。 從左側面板選取縮圖，以選擇您要預覽的頁面。

> 注意
> * 您可預覽的資產大小上限為100 MB。
> * 要預覽的XLS或XLSX檔案大小上限為20 MB。
> 

