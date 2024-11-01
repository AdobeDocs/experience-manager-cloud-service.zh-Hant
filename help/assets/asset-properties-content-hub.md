---
title: ' [!DNL the Content Hub]中的資產屬性'
description: 瞭解如何在 [!DNL Content Hub]中檢視及管理資產屬性
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 9%

---

# 在Content Hub中管理資產屬性 {#asset-properties}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![中繼資料橫幅影像](assets/metadata-banner-image.png)

[!DNL The Content Hub]可讓您檢視對有效率資產發佈至關重要的資產相關資訊。 這是資產所有可用資料的集合。

檢視資產屬性可協助您進一步將資產分類，而且隨著數位資訊量成長，這項功能也會很有幫助。 您可以僅根據檔案名稱、縮圖和記憶體體來管理數百個檔案。但是，當涉及的人數以及管理的資產數量增加時，此方法將無法擴充。 此外，數位資產的價值會隨著資產成長：

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 — 您可以輕鬆找到具有同一組屬性的資產，並將變更套用至這些資產。
* 完整 — 資產攜帶更多資訊和內容。

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以執行本文中提到的動作。

## 檢視資產屬性 {#properties-ui}

使用、分享或下載資產前，您可以更密切地檢視資產。預覽功能不僅可讓您檢視影像，也可檢視一些其他支援的資產型別。 您不僅可以檢視資產，也可以檢視其詳細資訊並採取其他動作。 若要檢視資產的資訊，請導覽至該資產，或[搜尋](search-assets.md)該資產，然後按一下該資產以開啟其屬性。 下圖示範資產屬性頁面上可用的欄位：

![資產UI的屬性](assets/properties-ui.png)

* **A：**&#x200B;資產的標題
* **B：**&#x200B;放大或縮小比例，可更密切地縮放或預覽資產
* **C：**&#x200B;復原縮放至先前選取的百分比
* **D：**&#x200B;繼續前一個或下一個資產
* **E：** Assets計數
* **F：**&#x200B;下載資產
* **G：**&#x200B;使用[!DNL Adobe Express]編輯資產
* **高：**&#x200B;收合或預覽資產資訊
* **I：**&#x200B;共用資產
* **J：**&#x200B;新增資產到[!DNL Collection]
* **K：**&#x200B;關閉預覽畫面
* **L：**&#x200B;資產的資訊，包括標題、格式、大小、解析度、標籤、顏色標籤和智慧標籤。

## 支援的格式 {#supported-formats}

下表示範[!DNL the Content Hub]中支援的檔案格式：

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

* **大小：**&#x200B;大小會依據資產的維度來示範資產的邏輯值。 它會釐清資產在存放庫中佔據的空間。 [!DNL The Content Hub]支援高達2GB的資產。

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **智慧標籤：** [!DNL The Content Hub]使用Adobe Sensei的智慧內容服務，在標籤架構上使用辨識演演算法來訓練資產。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 智慧標籤可協助您快速找到相關資產，提升專案的內容速度。 智慧型標籤即是不含在影像中的資產資訊範例。 [!DNL The Content Hub]預設會自動將智慧標籤套用至資產。

* **顏色標籤：** [顏色標籤](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en)可協助您使用在資產中自動識別顏色(使用Adobe的Sensei AI功能)來識別資產。

* 上傳日期

* 上傳者

* 上次修改時間

* 上次修改者

將資產新增至Content Hub時，也會指定屬性。 如需詳細資訊，請參閱[將品牌核准的資產新增至Content Hub](upload-brand-approved-assets.md)。 這些屬性也會顯示在資產屬性頁面上。

管理員也可以設定為每個資產顯示的屬性。 如需詳細資訊，請參閱[設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-asset-details-content-hub)。

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->
