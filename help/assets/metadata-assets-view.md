---
title: 管理中繼資料
description: 管理  [!DNL Assets view] 中資產的中繼資料
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: cfc105d1-41fc-4418-9905-b2a28a348682
source-git-commit: e2efffe0192f7914fd97178884b7938b84fd9a27
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 64%

---

# 資產檢視中的中繼資料 {#metadata}

中繼資料為資料或資料相關的說明。例如，作為資產的影像可以包含其所按一下的相機資訊或任何版權資訊。此資訊是影像的中繼資料。中繼資料是進行高效率資產管理的關鍵所在。中繼資料雖然是資產所有可用資料的集合，但並不一定包含在資產內。

中繼資料有助於您進一步將資產分類，而且隨著數位資訊量成長，將相當實用。您可以僅根據檔案名稱、縮圖和記憶體體來管理數百個檔案。然而，此方法並不能調整規模。隨著相關人數和管理的資產數增加，此方法尚嫌不足。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

基於這些原因，Assets 提供建立、管理和交換數位資產的中繼資料的合適方式。

## 檢視中繼資料 {#view-metadata}

若要檢視資產的中繼資料，請瀏覽至資產或搜尋資產、選取資產，然後按一下工具列中的&#x200B;**[!UICONTROL 詳細資訊]**。

![檢視資產的中繼資料](assets/metadata-view1.png)

*圖：若要檢視資產及其中繼資料，請按一下&#x200B;**[!UICONTROL 詳細資料]**從工具列或按兩下資產。*

標題、說明和上傳日期之類的基本中繼資料可在[!UICONTROL 基本]標籤中取得。[!UICONTROL 進階]標籤包含更進階的中繼資料，例如相機型號、鏡頭詳細資訊和地理標籤。[!UICONTROL 標記]標籤會根據影像內容包含自動套用的標記。

## 更新中繼資料 {#update-metadata}

管理員設定中繼資料表單後，其他欄位即可手動更新。 您可能會想要變更此專案，因為它只會根據現成的中繼資料表單讀取。

## 智慧標記 {#smart-tags}

[!DNL Experience Manager Assets] 使用 [Adobe Sensei](https://www.adobe.com/tw/sensei.html) 所提供的人工智慧，自動將相關標記套用至您所有上傳的資產。這些標記名為智慧型標記，有助於您快速尋找相關資產，提高專案的內容速度。智慧型標記即是不含在影像內的中繼資料範例。

智慧型標記近乎即時套用，並根據影像內容產生。上傳資產時，使用者介面會在資產縮圖上顯示[!UICONTROL 處理]一段時間。待處理完成後，即可[檢視中繼資料](#view-metadata)和智慧型標記。

![檢視資產的智慧型標記](assets/metadata-view-tags.png)

*圖：若要檢視資產的智慧標籤，請按一下&#x200B;**[!UICONTROL 詳細資料]**從工具列或按兩下資產。*

智慧型標記也包含信賴分數 (以百分比呈現)。這表示與套用標記相關的信賴度。您可以審核自動套用的智慧型標記。

## 新增或更新關鍵字 {#manually-tag}

除了使用 [!DNL Adobe Sensei] 智慧型服務自動新增的智慧型標記之外，您還可新增更多標記到您的資產。開啟要預覽的資產，按一下[!UICONTROL 標記]，然後在[!UICONTROL 關鍵字]欄位中輸入所需的關鍵字。若要新增標記，請按一下「Return」。[!DNL Assets view] 會近乎即時地編製關鍵字的索引，因此您的團隊很快就能使用新的關鍵字搜尋更新的資產。

您也可以從[!UICONTROL 智慧標記]區段移除由 [!DNL Assets view] 自動新增到所有上傳資產的標記。

## 分類法管理 {#taxonomy-management}

標籤也可以巢狀內嵌到階層中，以支援類別和子類別等關係。 如果您需要插入階層式標籤，管理員可輕鬆管理這些標籤。 [!UICONTROL 分類管理] 部分 [!UICONTROL 設定]. 您可以建立一組受監管的名稱空間和標籤，讓所有使用者在描述內容時都可以存取這些名稱空間和標籤。 只有管理員可以在中設定標籤階層 [!UICONTROL 分類管理員] 確保值受到一致的控制和使用。

## 設定中繼資料表單 {#metadata-forms}

>[!CONTEXTUALHELP]
>id="assets_metadata_forms"
>title="中繼資料表單"
>abstract="[!DNL Experience Manager Assets] 預設會提供許多標準中繼資料欄位。組織擁有其他中繼資料需求，並需要更多中繼資料欄位以新增特定企業中繼資料。 中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的詳細資訊頁面。特定企業中繼資料能夠改善其資產的控管和探索。"

資產檢視預設會提供許多標準中繼資料欄位。 組織擁有其他中繼資料需求，並需要更多中繼資料欄位以新增特定企業中繼資料。中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的[!UICONTROL 詳細資訊]頁面。特定企業中繼資料能夠改善其資產的控管和探索。您可以從頭開始建立表單，或重新使用現有表單。

您可以為不同的資產類型 (不同的 MIME 類型) 設定中繼資料表單。使用與檔案的 MIME 類型相同的表單名稱。資產檢視會自動比對上傳的資產MIME型別與表單的名稱，並根據表單欄位更新上傳資產的中繼資料。

例如，如果存在名稱為 `PDF` 或 `pdf` 的中繼資料表單，則上傳的 PDF 文件會包含如表單中定義的中繼資料欄位。

「資產」檢視會使用下列順序來搜尋現有的中繼資料表單名稱，以將中繼資料欄位套用至特定型別的已上傳資產：

MIME 子類型 > MIME 類型 > `default` 表單 > 現成可用的表單

例如，如果存在名稱為 `PDF` 或 `pdf` 的中繼資料表單，上傳的 PDF 文件則包含如表單中定義的中繼資料欄位。如果中繼資料表單按名稱 `PDF` 或 `pdf` 不存在，如果存在名稱為的中繼資料表單，則資產檢視會相符 `application`. 如果存在名稱為的中繼資料表單 `application`，上傳的PDF檔案會包含如表單中定義的中繼資料欄位。 如果資產檢視仍找不到相符的中繼資料表單，則會搜尋 `default` 中繼資料表單，以將表單中定義的中繼資料欄位套用至上傳的PDF檔案。 如果上述任何步驟都無法運作，資產檢視會將現成可用表單中定義的中繼資料欄位套用至所有上傳的PDF檔案。

>[!IMPORTANT]
>
>特定檔案類型的新中繼資料表單會完成取代 [!DNL Assets view] 所提供的預設中繼資料表單。如果您刪除或重新命名中繼資料表單，新資產便可再次使用預設中繼資料欄位。

若要建立中繼資料表單，請依照下列步驟：

1. 在左側欄中按一下&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 中繼資料表單]**。

   ![左側邊欄中的中繼資料表單選項](assets/metadata-forms-sidebar.png)

1. 按一下使用者介面右上角區域中的&#x200B;**[!UICONTROL 建立]**。
1. 為表單命名，然後按一下&#x200B;**[!UICONTROL 建立]**。
1. 為右側欄中&#x200B;**[!UICONTROL 設定]**&#x200B;中的標籤命名。
1. 從左側欄中可用的&#x200B;**[!UICONTROL 元件]**&#x200B;拖曳表單中標籤上所需的元件。依照所需的序列拖曳元件。

   ![左側邊欄中的中繼資料表單選項](assets/metadata-form-new.png)

   *圖：中繼資料表單建立介面，其中包含新增元件的選項和預覽表單的選項。*

1. 針對每個元件，在 **[!UICONTROL 設定]** 在右側欄中，提供支援屬性的對應。
1. 或是對元件選取&#x200B;**[!UICONTROL 必要]**，讓中繼資料欄位成為必要欄位，並選取&#x200B;**[!UICONTROL 唯讀]**&#x200B;讓此欄位在資產[!UICONTROL 詳細資訊]頁面中無法編輯。
1. 或者按一下&#x200B;**[!UICONTROL 預覽]**&#x200B;以預覽您正在建立的表單。
1. 或者在每個標籤中新增更多標籤和所需元件。
1. 表單完成時，按一下&#x200B;**[!UICONTROL 儲存]**。

請觀看此影片以查看步驟的順序：

>[!VIDEO](https://video.tv.adobe.com/v/341275)

建立表單後，便會在使用者上傳相符 MIME 類型的資產時自動套用表單。

若要重複使用現有表單來建立新表單，請選取中繼資料表單，從工具列按一下&#x200B;**[!UICONTROL 複製]**、命名，然後按一下&#x200B;**[!UICONTROL 確認]**。您可以編輯中繼資料表單，進行變更。變更表單時，會在變更後用於上傳的資料。不會變更現有資產。

## 屬性元件 {#property-components}

您可以使用以下任何屬性元件來自訂中繼資料表單。 只需將元件型別拖放到表單中所需的位置，並修改元件設定即可。
以下為每種屬性型別及其儲存方式的概觀。

| 元件名稱 | 說明 |
|---|---|
| 收合式選單容器 | 為常用元件和屬性清單新增可摺疊的標題。 預設可展開或收合。 |
| 單行文字 | 新增單行文字屬性。 |
| 多行文字 | 新增多行文字或一個段落。 它會隨著使用者型別擴展以包含所有內容。 |
| 多值文字 | 新增多值文字屬性。 |
| 數字 | 新增數字元件。 |
| 核取方塊 | 新增布林值。 儲存值後儲存為TRUE或FALSE。 |
| 日期 | 新增日期元件。 |
| 下拉式清單 | 新增下拉式清單。 |
| 狀態 | 新增存放庫狀態屬性（對應至repo：state） |
| 資產狀態 | 新增預設資產狀態屬性（對應至dam：assetStatus） |
| 標記 | 從儲存在「分類管理」中的值新增標籤（對應至xcm：tags）。 |
| 關鍵字 | 新增任意格式關鍵字（對應至dc：subject）。 |
| 智慧標記 | 新增以透過自動新增中繼資料標籤來增強搜尋功能。 |

## 後續步驟 {#next-steps}

* [觀看在「資產」檢視中管理中繼資料表單的相關影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html)

* 使用提供產品意見回饋 [!UICONTROL 意見反應] 「資產」檢視使用者介面中可用的選項

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)

<!-- TBD: Cannot create a form using the second option. Documenting only the first option for now.
To reuse an existing form to create a new form, do one of these:

* Select a metadata form and click **[!UICONTROL Copy]** from the toolbar, provide a name, and click **[!UICONTROL Confirm]**.

* Click **[!UICONTROL Create]**, select **[!UICONTROL Use existing form structure as template]** option, and select an existing form. 
-->

<!-- TBD: Queries for PM and engg.

Can we edit the existing metadata in any form?

How to moderate smart tags?

Allow or deny list for smart tags?

What about Tags displayed just above Smart Tags in the UI?

Is there a detailed metadata tab. Where do the other details of an asset go?

How can one search based strictly on the metadata. Similar to AEM Assets GQL queries.
-->

<!-- TBD: Link to related articles if any.

>[!MORELIKETHIS]
>
>* [Search assets](search.md).
-->
