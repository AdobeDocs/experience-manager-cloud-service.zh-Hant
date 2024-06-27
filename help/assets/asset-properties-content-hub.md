---
title: 中的資產屬性 [!DNL the Content Hub]
description: 瞭解如何在中檢視及管理資產屬性 [!DNL Content Hub]
role: User
source-git-commit: e590c34c177e6b45b6a52370caa88da54b61ebc0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 8%

---


# 在Content Hub中管理資產屬性 {#asset-properties}

![中繼資料的橫幅影像](assets/metadata-banner-image.png)

[!DNL The Content Hub] 可讓您檢視對有效率資產發佈至關重要的資產相關資訊。 這是資產所有可用資料的集合。

檢視資產屬性可協助您進一步將資產分類，而且隨著數位資訊量成長，這項功能也會很有幫助。 您可以僅根據檔案名稱、縮圖和記憶體體來管理數百個檔案。但是，當涉及的人數以及管理的資產數量增加時，此方法將無法擴充。 此外，數位資產的價值會隨著資產成長：

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 — 您可以輕鬆找到具有同一組屬性的資產，並將變更套用至這些資產。
* 完整 — 資產攜帶更多資訊和內容。

## 檢視資產屬性 {#properties-ui}

使用、分享或下載資產前，您可以更密切地檢視資產。預覽功能不僅可讓您檢視影像，也可檢視一些其他支援的資產型別。 您不僅可以檢視資產，也可以檢視其詳細資訊並採取其他動作。 若要檢視資產的資訊，請導覽至該資產或 [搜尋](search-assets.md) 資產，然後按一下資產以開啟其屬性。 下圖示範資產屬性頁面上可用的欄位：

![資產UI的屬性](assets/properties-ui.png)

* **答：** 資產標題
* **B：** 透過放大或縮小縮小顯示更密切地縮放或預覽資產的百分比
* **C：** 復原縮放至先前選取的百分比
* **D：** 繼續上一個或下一個資產
* **E：** Assets計數
* **F：** 下載資產
* **G：** 編輯資產，使用 [!DNL Adobe Express]
* **高：** 收合或預覽資產資訊
* **我：** 共用資產
* **J：** 將資產新增至 [!DNL Collection]
* **K：** 關閉預覽畫面
* **L：** 資產的資訊，包括標題、格式、大小、解析度、標籤、顏色標籤和智慧標籤。

## 支援的格式 {#supported-formats}

下表示範中支援的檔案格式 [!DNL the Content Hub]：

<table> 
    <tbody>
     <tr>
      <th><strong>檔案型別</strong></th>
      <th><strong>支援的格式</strong></th>
     </tr>
     <tr>
      <td>影像</td>
      <td>
        <ul>
            <li>[！UICONTROLJPEG]</li> 
            <li>[！UICONTROL PNG]</li> 
            <li>[！UICONTROLSVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>影片</td>
      <td>
        <ul>
            <li>[！UICONTROL Quicktime]</li>  
            <li>[！UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>文件</td>
      <td>
        <ul>
            <li>[！UICONTROL txt] （純文字）</li>  
            <li>[！UICONTROL Doc/Docx]</li> 
            <li>[！UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>列印媒體</td>
      <td>
        <ul>
            <li>[！UICONTROLPDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### 上傳資產後衍生的屬性 {#derived-properties}

上傳資產後，Content Hub會衍生出一些自動產生的屬性。 以下是其中一些的清單：

* **大小：** 大小會根據資產的維度來示範資產的邏輯值。 它會釐清資產在存放庫中佔據的空間。 [!DNL The Content Hub] 支援高達2GB的資產。

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **智慧標籤：** [!DNL The Content Hub] 使用Adobe Sensei的智慧內容服務，透過標籤架構上的辨識演演算法來訓練資產。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 智慧標籤可協助您快速找到相關資產，提升專案的內容速度。 智慧型標籤即是不含在影像中的資產資訊範例。 [!DNL The Content Hub] 預設會自動將智慧標籤套用至資產。

* **顏色標籤：** [顏色標籤](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) 協助您使用Adobe的Sensei AI功能，透過資產中自動識別的顏色，來識別資產。

* 上傳日期

* 上傳者

* 上次修改時間

* 上次修改者

將資產新增至Content Hub時，也會指定屬性。 如需詳細資訊，請參閱 [將品牌核准的資產新增至Content Hub](upload-brand-approved-assets.md). 這些屬性也會顯示在資產屬性頁面上。

管理員也可以設定為每個資產顯示的屬性。 如需詳細資訊，請參閱 [設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

