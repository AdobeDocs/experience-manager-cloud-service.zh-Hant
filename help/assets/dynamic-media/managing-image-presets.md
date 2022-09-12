---
title: 管理影像預設集
description: 了解影像預設集，以及如何建立、修改和管理影像預設集。
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: ca0385ee974c7b06725f687c0ef237880bb230ea
workflow-type: tm+mt
source-wordcount: '3629'
ht-degree: 8%

---

# 管理影像預設集{#managing-image-presets}

影像預設集可讓Adobe Experience Manager Assets以不同大小、不同格式，或透過動態產生的其他影像屬性來動態傳送影像。 每個影像預設集代表用於顯示影像的大小調整和格式設定命令的預定義集合。 建立影像預設集時，您會選擇影像傳送的大小。 您也可以選擇格式設定命令，以便在傳送影像以供查看時優化影像的外觀。

管理員可以建立匯出資產的預設集。 用戶在導出映像時可以選擇預設集，該預設集還會按照管理員指定的規範重新格式化映像。

您也可以建立回應式的影像預設集。 如果您將回應式影像預設集套用至資產，則會根據所檢視的裝置或螢幕大小而變更。 除了「RGB」或「灰色」外，您還可以配置影像預設集以在顏色空間中使用CMYK。

本節說明如何建立、修改和一般管理影像預設集。 您可以隨時預覽影像，將影像預設集套用至影像。 請參閱 [套用影像預設集](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>智慧型影像處理可與您現有的影像預設集搭配使用，並會在傳送時的最後毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 請參閱 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md) 以取得更多資訊。

## 了解影像預設集 {#understanding-image-presets}

像宏一樣，「影像預設集」是儲存在名稱下的大小調整和格式設定命令的預定義集合。 若要了解「影像預設集」的運作方式，假設您的網站要求每個產品影像以不同大小、不同格式，以及案頭和行動傳送的壓縮率顯示。

您可以建立兩個影像預設集：案頭版為500 x 500像素，行動版為150 x 150像素。 您可以建立兩個影像預設集，其中一個稱為 `Enlarge` 以500x500像素顯示影像，並稱為 `Thumbnail` 以150 x 150像素顯示影像。 若要在 `Enlarge` 和 `Thumbnail` 大小，Experience Manager可找到放大影像預設集和縮圖影像預設集的定義。 然後，Experience Manager會動態地根據每個影像預設集的大小和格式規格產生影像。

動態傳送時大小縮小的影像可能會失去清晰度和細節。 因此，每個影像預設集都包含格式控制項，用於在以特定大小傳送影像時對其進行最佳化。 這些控制項可確保影像在傳送至您的網站或應用程式時清晰清晰銳利。

管理員可以建立影像預設集。 若要建立影像預設集，您可以從草稿開始，也可以從現有的預設集開始，並以新名稱儲存。

## 管理影像預設集 {#managing-image-presets-1}

您可以選取Experience Manager標誌以存取全域導覽主控台，然後選取「工具」圖示並導覽至，以管理Experience Manager中的影像預設集 **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>您建立的任何影像預設集在您預覽或傳送資產時，也可以以動態轉譯的形式使用。
>
>你做 *not* 需要發佈影像預設集，因為會自動發佈影像預設集。
>
>請參閱 [發佈影像預設集](#publishing-image-presets).

>[!NOTE]
>
>當您選取「 **[!UICONTROL 轉譯]** 在資產的「詳細資料檢視」中。 您可以增加或減少顯示的影像預設集數目。 請參閱 [增加顯示的影像預設集數量](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Adobe Illustrator(AI)、PostScript®(EPS)和PDF檔案格式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

如果您想要支援擷取AI、EPS和PDF檔案，以便產生這些檔案格式的動態轉譯，請在建立影像預設集之前先檢閱下列資訊。

Adobe Illustrator的檔案格式是PDF的變體。 Experience Manager Assets的主要差異如下：

* Adobe Illustrator檔案包含單一頁面及多個層。 每個圖層都會擷取為主要Illustrator資產下的PNG子資產。
* PDF文檔包含一個或多個頁。 每個頁面都會擷取為主要多頁面PDF檔案下的單頁PDF子資產。

子資產由 `Create Sub Asset process` 整體 `DAM Update Asset` 工作流程。 要在工作流中查看此流程元件，請導航至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**.

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

您可以在開啟資產時檢視子資產或頁面，選取「內容」功能表，然後選取 **[!UICONTROL 子資產]** 或 **[!UICONTROL 頁面]**. 子資產。 也就是說，PDF頁面會由 `Create Sub Asset` 工作流程元件。 接著，這些資料會儲存為 `page1.pdf`, `page2.pdf`，以此類推，位於主要資產下方。 儲存後， `DAM Update Asset` 工作流程會處理它們。

若要使用Dynamic Media來預覽和產生AI、EPS或PDF檔案的動態轉譯，需要下列處理步驟：

1. 在 `DAM Update Asset` 工作流程， `Rasterize PDF/AI Image Preview Rendition` 處理元件將原始資產的第一頁（使用配置的解析度）柵格化為 `cqdam.preview.png` 轉譯。

1. 此 `cqdam.preview.png` 然後，將格式副本最佳化為PTIFF `Dynamic Media Process Image Assets` 工作流程中的處理元件。

>[!NOTE]
>
>在「DAM更新資產」工作流程中， **[!UICONTROL EPS縮圖步驟]** ，會為EPS檔案生成縮圖。

#### PDF/AI/EPS資產中繼資料屬性 {#pdf-ai-eps-asset-metadata-properties}

| **中繼資料屬性** | **說明** |
|---|---|
| dam:Physicalwidthinichs | 文檔寬度（英吋）。 |
| dam：物理高度 | 文檔高度（英吋）。 |

您可以存取 `Rasterize PDF/AI Image Preview Rendition` 流程元件選項(通過 `DAM Update Asset` 工作流程。

選取左上角的Adobe Experience Manager，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**. 在「工作流模型」頁上，選擇 **[!UICONTROL DAM更新資產]**，然後在工具列上選取 **[!UICONTROL 編輯]**. 在「 DAM更新資產」工作流程頁面上，點選兩下 `Rasterize PDF/AI Image Preview Rendition` 處理元件以開啟其「步驟屬性」對話框。

#### 柵格化PDF/AI影像預覽轉譯選項 {#rasterize-pdf-ai-image-preview-rendition-options}

![柵格化PDF或AI工作流的參數](assets/rasterize_pdf_ai_image_preview.png)

柵格化PDF或AI工作流的參數

| 進程參數 | 預設設定 | 說明 |
|---|---|---|
| Mime 類型 | application/pdf<br>application/postscript<br>application/illustrator | 被視為PDF或Illustrator文檔的文檔mime類型清單。 |
| 寬度上限 | 2048年 | 產生的預覽轉譯的最大寬度（像素）。 |
| 高度上限 | 2048年 | 產生的預覽轉譯的最大高度（像素）。 |
| 解析度 | 72 | 以ppi（每英吋像素）顯示第一頁的解析度。 |

使用預設進程參數，PDF/AI文檔的第一頁柵格化為72 ppi，生成的預覽影像的大小為2048 x 2048像素。 對於一般部署，您可將解析度提高至至少150 ppi或更高。 例如，300 ppi的美國字母大小文檔要求最大寬度和高度分別為2550 x 3300像素。

「最大寬度」和「最大高度」限制柵格化的解析度。 例如，如果最大值未變更，且「解析度」設為300 ppi，則美國信函檔案的光柵化為186 ppi。 也就是說，文檔為1581 x 2046像素。

此 `Rasterize PDF/AI Image Preview Rendition` 進程元件已定義最大值，以確保它不會在記憶體中建立過大的映像。 此類大型映像可能會使提供給JVM(Java™虛擬機)的記憶體溢出。 請務必注意，為JVM提供足夠的記憶體，以管理已配置的並行工作流數，每個工作流都有可能以最大配置的大小建立映像。

### InDesign(INDD)檔案格式 {#indesign-indd-file-format}

如果要支援擷取INDD檔案，以便產生此檔案格式的動態轉譯，請先檢閱下列資訊，再建立影像預設集。

對於InDesign檔案，只有在Adobe InDesign Server與Experience Manager整合時，才會擷取子資產。 參考的資產會根據其中繼資料進行連結。 InDesign Server不是連結的必要項目。 不過，在處理InDesign檔案之前，Experience Manager內必須有參考的資產，才會在InDesign檔案與參考的資產之間建立連結。

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

中的媒體擷取程式元件 `DAM Update Asset` 工作流程會執行數個預先設定的擴充指令碼，以處理InDesign檔案。

![媒體擷取程式引數中的ExtendScript路徑](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

ExtendScript會在「DAM更新資產」工作流程中，路徑為「媒體擷取」程式元件的引數。

下列指令碼供Dynamic Media整合使用：


| ExtendScript名稱 | 預設 | 說明 |
|---|---|---|
| ThumbnailExport.jsx | 是 | 產生300 PPI `thumbnail.jpg` 最佳化的轉譯，並透過 `Dynamic Media Process Image Assets` 處理元件。 |
| JPEGPagesExport.jsx | 是 | 為每個頁面產生300 PPIJPEG子資產。 JPEG子資產是儲存在InDesign資產下的實際資產。 也會經過最佳化，並由 `DAM Update Asset` 工作流程。 |
| PDFPagesExport.jsx | 否 | 為每個頁面產生PDF子資產。 PDF子資產會依照先前所述進行處理。 由於PDF僅包含單一頁面，因此不會產生任何子資產。 |

### 設定影像縮圖大小 {#configuring-image-thumbnail-size}

您可以在 **[!UICONTROL DAM更新資產]** 工作流程。 工作流程中有兩個步驟可讓您設定影像資產的縮圖大小。 一(**[!UICONTROL Dynamic Media處理影像資產]**)用於動態影像資產。 其他(**[!UICONTROL 處理縮圖]**)用於產生靜態縮圖，或當所有其他程式無法產生縮圖時。 無論如何， *both* 必須有相同的設定。

在「動 **[!UICONTROL 態媒體處理影像資產」步驟中]** ，影像伺服器會產生縮圖，此組態與套用至「處理縮圖」步驟的組態無關 **** 。透過「處理縮圖 **[!UICONTROL 」步驟產生縮圖]** ，是建立縮圖的最慢且記憶體最耗用的方式。

縮圖大小定義為下列格式： **[!UICONTROL 寬度:height:中心]**，例如 `80:80:false`. 寬度和高度會以像素為單位決定縮圖的大小。 中心值為false或true。 如果設為true，表示縮圖影像的大小與設定中指定的大小完全相同。 如果調整大小的影像較小，則會置於縮圖中。

>[!NOTE]
>
>* EPS檔案的縮圖大小是在 **[!UICONTROL EPS縮圖]** 步驟，在 **[!UICONTROL 引數]** 標籤。
>
>* 視訊的縮圖大小是在 **[!UICONTROL FFmpeg縮圖]** 步驟，在 **[!UICONTROL 程式]** 標籤 **[!UICONTROL 引數]**.
>


**若要設定影像縮圖大小：**

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**.
1. 選取 **[!UICONTROL Dynamic Media處理影像資產]** 步驟並選取 **[!UICONTROL 縮圖]** 標籤。 視需要變更縮圖大小，然後選取 **[!UICONTROL 確定]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. 選取 **[!UICONTROL 處理縮圖]** 步驟，然後選取 **[!UICONTROL 縮圖]** 標籤。 視需要變更縮圖大小，然後選取 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >「處理縮圖」步驟中縮圖引數中 **[!UICONTROL 的值必須與「動態媒體處理影像資產」]** 步驟中的縮圖引數相符 **** 。

1. 選擇 **[!UICONTROL 儲存]** 以儲存對工作流程的變更。

### 增加或減少顯示的影像預設集數量 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

您建立的影像預設集在您預覽資產時可以動態轉譯。 Experience Manager會在從 **[!UICONTROL 詳細資料檢視>轉譯]**. 您可以增加或減少顯示的轉譯限制。

**要增加或減少顯示的影像預設集數目，請執行以下操作：**

1. 導覽至CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 在導覽至影像預設集清單節點 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_deximentenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 在 **[!UICONTROL limit]** 屬性中，將預設設 ****&#x200B;定為15的值變更為所要的數字。
1. 導航到以下位置的影像預設資料源： `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 在limit屬性中，將數字變更為所需數字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 選擇 **[!UICONTROL 全部儲存]**.

### 建立影像預設集 {#creating-image-presets}

建立影像預設集，以便在預覽或發佈時可一致地套用各個影像的設定。

>[!NOTE]
>
>如果使用Internet Explorer 9，建立預設集在儲存後不會立即出現在預設集清單中。 若要解決此問題，請停用IE9的快取。

如果您想要支援擷取AI、PDF和EPS檔案，以便產生這些檔案格式的動態轉譯，請先檢閱下列資訊，再建立影像預設集。

請參閱 [Adobe Illustrator(AI)、PostScript®(EPS)和PDF檔案格式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

如果要支援擷取INDD檔案，以便產生此檔案格式的動態轉譯，請先檢閱下列資訊，再建立影像預設集。

請參閱 [InDesign(INDD)檔案格式](#indesign-indd-file-format).

**要建立影像預設集：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.
1. 選擇 **[!UICONTROL 建立]**。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >若要讓此影像預設變得自適應，請擦除 **[!UICONTROL 寬度]****[!UICONTROL 和高度欄]** 位中的值，並保留空白。

1. 在 **[!UICONTROL 編輯影像預設集]** ，請在 **[!UICONTROL 基本]** 和 **[!UICONTROL 進階]** 索引標籤，包括名稱。 這些選項在「影像預設 [集選項」中概述](#image-preset-options)。預設集會出現在左窗格中，並可與其他資產一起即時使用。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 選擇 **[!UICONTROL 儲存]**.

### 建立回應式影像預設集 {#creating-a-responsive-image-preset}

若要建立回應式影像預設集，請執行 [建立影像預設集](#creating-image-presets). 在 **[!UICONTROL 編輯影像預設集]** ，請拭除值並保留空白。

將它們留空會告訴Experience Manager此影像預設集是回應式的。 您可以視需要調整其他值。

>[!NOTE]
>
>若要在套用 **[!UICONTROL 影像預設集]** 至資產時查看 **** URL和RESS按鈕，必須發佈資產。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>影像預設集和影像資產會自動發佈。

### 影像預設集選項 {#image-preset-options}

建立或編輯影像預設集時，您有本節所述的選項。 此外，Adobe建議以下「最佳做法」選項作為開始：

* **[!UICONTROL 格式]** (**[!UICONTROL 基本]** 頁簽) — 選擇 **[!UICONTROL JPEG]** 或符合您要求的其他格式。 所有網頁瀏覽器都支援JPEG影像格式；它在小檔案大小和影像品質之間提供良好的平衡。但是，JPEG格式影像使用有損壓縮方案，如果壓縮設定太低，則該壓縮方案會引入不想要的影像偽影。因此，Adobe建議將壓縮品質設為75。此設定在影像品質和檔案大小之間取得良好的平衡。

* **[!UICONTROL 啟用簡單銳利化]** -請勿選取「啟用簡 **** 單銳利化」 (此銳利化濾鏡提供的控制力比「非銳利化遮色片」設定少)。

* **[!UICONTROL 銳利化：重新取樣模式]**  — 選擇 **[!UICONTROL Sharp2]**.

#### 基本索引標籤選項 {#basic-tab-options}

| 欄位 | 說明 |
| --- | --- |
| **名稱** | 輸入描述性名稱，不含任何空格。 要幫助用戶標識此影像預設集，請在名稱中包括影像大小規範。 |
| **寬度和高度** | 以像素輸入影像傳送的大小。 寬度和高度必須大於0像素。 如果其中一個值為0，則不會建立任何預設集。 如果兩個值皆空白，則會建立回應式影像預設集。 |
| **格式** | 從功能表中選擇格式。<br>選擇 **JPEG** 提供下列其他選項：<br>· **品質** -JPEG質量等級為1-100。 拖曳滑桿時，比例會顯示。<br>· **啟用JPG色度縮減取樣**  — 由於眼睛對高頻顏色資訊的敏感度比高頻亮度低，JPEG影像將影像資訊分為亮度和顏色分量。 當JPEG影像被壓縮時，亮度分量以全解析度保持，而顏色分量通過平均一組像素被縮減。 縮減取樣會將資料量減少一半或三分之一，幾乎不會影響感知的品質。 縮減採樣不適用於灰度影像。 此技術可減少對具有高對比度的影像（例如具有重疊文字的影像）有用的壓縮量。<br><br>選擇 **GIF** 或 **含Alpha的GIF** 提供 **GIF顏色量化** 選項：<br>· **類型**  — 選擇 **適應性** （預設）, **Web**，或 **Macintosh**. 如果您選取 **GIFAlpha**，則「Macintosh」選項不可用。<br>· **Dither**  — 選擇 **擴散** 或 **關閉**.<br>· **顏色數**  — 輸入數字2 - 256。<br>· **顏色清單**  — 輸入逗號分隔清單。 例如，對於白色、灰色和黑色，請輸入 `000000,888888,ffffff`.<br><br>選擇 **PDF**, **TIFF**，或 **含Alpha的TIFF** 提供此額外選項：<br>· **壓縮**  — 選擇壓縮算法。 PDF的演算法選項為 **無**, **郵遞區號**，和 **Jpeg**;TIFF **無**, **LZW**, **Jpeg**，和 **郵遞區號**;而使用Alpha的TIFF為 **無**, **LZW**，和 **郵遞區號**.<br><br>選擇 **PNG**, **含Alpha的PNG**，或 **EPS** 不提供其他選項。 |
| **銳利化** | 選擇 **啟用簡單銳利化** 以在所有縮放發生後，將基本銳利化濾鏡應用到影像。 銳利化有助於補償以不同大小顯示影像時可能產生的模糊性。 |

#### 進階索引標籤選項 {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>欄位</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>色域</strong></td>
   <td>選擇 <strong>RGB, CMYK,</strong> 或 <strong>灰階</strong> 顏色空間。</td>
  </tr>
  <tr>
   <td><strong>色彩設定檔</strong></td>
   <td>如果資產與工作設定檔不同，請選取您要轉換為的輸出色域設定檔。</td>
  </tr>
  <tr>
   <td><strong>渲染方法</strong></td>
   <td>您可以覆寫預設的呈現方式。 渲染意圖確定目標顏色配置檔案中無法再現的顏色（超出色域）的結果。 如果「渲染目的」與ICC配置檔案不相容，則將忽略它。
    <ul>
     <li>選擇 <strong>知覺</strong> 當原始影像中的一個或多個顏色超出目標顏色空間的色域時，將總色域從一個顏色空間壓縮到另一個顏色空間。</li>
     <li>選擇 <strong>相對比色</strong> 當當前顏色空間中的顏色超出目標顏色空間中的色域時。 而且，您希望將其映射到目標顏色空間的色域內最接近的可能顏色，而不影響任何其他顏色。 </li>
     <li>選擇 <strong>飽和度</strong> 如果要在轉換為目標顏色空間時重現原始影像顏色飽和度。 </li>
     <li>選擇 <strong>絕對比色</strong> 以完全匹配顏色，而不調整會改變影像亮度的白點或黑點。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黑點補償</strong></td>
   <td>如果輸出配置檔案支援此功能，請選擇此選項。 如果黑點補償與指定的ICC配置檔案不相容，則會忽略它。</td>
  </tr>
  <tr>
   <td><strong>正在遞色</strong></td>
   <td>選擇此選項以可能避免或減少色帶偽影。 </td>
  </tr>
  <tr>
   <td><strong>銳利化類型</strong></td>
   <td><p>選擇 <strong>無</strong>, <strong>銳利化</strong>，或 <strong>不銳利化遮色片</strong>. </p>
    <ul>
     <li>選擇 <strong>無</strong> 如果要停用銳利化。</li>
     <li>選擇 <strong>銳利化 </strong>以在所有縮放發生後，將基本銳利化濾鏡應用到影像。 銳利化有助於補償以不同大小顯示影像時可能產生的模糊性。 </li>
     <li>選擇<strong> 不銳利化遮色片</strong> 如果您想要微調最終縮減取樣影像的銳利化濾鏡效果。 您可以控制效果的強度、效果半徑（以像素計量），以及忽略的對比度臨界值。 此效果使用的選項與 Photoshop的「遮色片銳利化」濾鏡相同。</li>
    </ul> <p>在 <strong>不銳利化遮色片</strong>，您有下列選項：</p>
    <ul>
     <li><strong>金額</strong>  — 控制套用至邊緣像素的對比度量。 預設的實數值為1.0。對於高解析度影像，您可以將其增加到高達5.0。請將「量」想像為濾鏡強度的度量。</li>
     <li><strong>半徑</strong>  — 決定影響銳利化的邊緣像素周圍的像素數。 對於高解析度影像，請輸入從1到2的實數。 低值只會銳化邊緣像素；高值銳化較寬的像素帶。 正確值取決於影像的大小。</li>
     <li><strong>臨界值</strong>  — 決定套用遮色片銳利化濾鏡時要忽略的對比度範圍。 換句話說，此選項可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素且銳化。 為避免引入雜訊，請使用2到20的整數值進行實驗。 </li>
     <li><strong>套用至</strong>  — 確定未銳利化是應用於每種顏色還是亮度。</li>
    </ul>
    <div>
      銳利化在
     <a href="https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media">將影像銳利化與Experience ManagerDynamic Media</a> 視訊，在 <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/using/master-files/sharpening-image.html#master-files">銳利化影像</a> 線上說明主題，和 <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">銳利化Dynamic Media Classic影像的最佳作法</a> 可下載的PDF。
    </div> </td>
  </tr>
  <tr>
   <td><strong>重新取樣模式</strong></td>
   <td>選取 <strong>重採樣模式</strong> 選項。 這些選項會在縮減取樣時銳化影像：
    <ul>
     <li><strong>雙線性</strong>  — 最快的重採樣方法。某些鋸齒偽影是可以注意到的。</li>
     <li><strong>雙立方</strong>  — 增加CPU使用量，但產生更清晰的影像，並產生較少明顯的鋸齒偽影。</li>
     <li><strong>Sharp2</strong>  — 可產生比雙立方體稍銳的結果，但CPU成本更高。</li>
     <li><strong>雙銳</strong>  — 選取Photoshop預設重新取樣器以縮小影像大小，稱為 <strong>雙比克</strong> 在Adobe Photoshop。</li>
     <li><strong>每種顏色</strong> 和 <strong>亮度</strong>  — 每種方法都可依據顏色或亮度。 依預設 <strong>每種顏色</strong> 中所有規則的URL。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>打印解析度</strong></td>
   <td>選擇用於打印此影像的解析度；預設為72像素。</td>
  </tr>
  <tr>
   <td><strong>影像修飾元</strong></td>
   <td><p>除了UI中可用的通用影像設定，Dynamic Media還支援許多進階影像修改，您可以在 <strong>影像修飾元</strong> 欄位。 這些參數定義於 <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview.html">映像伺服器協定命令參考</a>.</p> <p>重要：不支援API中列出的下列功能：</p>
    <ul>
     <li>基本模板和文本呈現命令： <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> 和 <code>textPs=</code></li>
     <li>本地化命令： <code>locale=</code> 和 <code>req=xlate</code></li>
     <li><code>req=set</code> 無法用於一般用途。</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>非核心Dynamic Media服務：SVG、影像轉譯和網路印刷</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 使用影像修飾元定義影像預設集選項 {#defining-image-preset-options-with-image-modifiers}

除了「基本」和「進階」索引標籤中可用的選項外，您還可以定義影像修飾元，以在定義影像預設集時提供更多選項。 影像轉譯仰賴Dynamic Media影像轉譯API，於 [HTTP通訊協定參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction.html#image-rendering-api).

以下是一些您可以使用影像修飾元的基本範例。

>[!NOTE]
>
>一些影像修飾元 [無法用於Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html)  — 反轉負影像效果的每個顏色分量。

   ```xml {.line-numbers}
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html)  — 對影像應用模糊濾鏡。

   ```xml {.line-numbers}
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* 組合命令 — op_blur和op-invert

   ```xml {.line-numbers}
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html)  — 降低或增加亮度。

   ```xml {.line-numbers}
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html)  — 調整影像不透明度。 可讓您降低前景不透明度。

   ```xml {.line-numbers}
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### 編輯影像預設集 {#modifying-image-presets}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.

   ![6_5_imagepreset_editpreset](assets/6_5_imagepreset-editpreset.png)

1. 選取預設集，然後選取 **[!UICONTROL 編輯]**. 此 **[!UICONTROL 編輯影像預設集]** 窗口。
1. 進行變更並選取 **[!UICONTROL 儲存]** 儲存變更或 **[!UICONTROL 取消]** 來取消變更。

### 發佈影像預設集 {#publishing-image-presets}

系統會自動為您發佈影像預設集。

### 刪除影像預設集 {#deleting-image-presets}

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台並選擇「工具」表徵圖。
1. 導覽至 **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.
1. 選取預設集，然後選取 **[!UICONTROL 刪除]**. Dynamic Media會確認您要刪除它。 選擇 **[!UICONTROL 刪除]** 刪除或選擇 **[!UICONTROL 取消]** 返回影像預設集。
