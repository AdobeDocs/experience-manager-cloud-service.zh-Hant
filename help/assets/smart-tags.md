---
title: 如何在AEM中新增智慧標籤至資產？
description: 透過AEM中可套用關聯式和描述性商業標籤的人工智慧服務，將智慧標籤新增至資產。
contentOwner: AG
feature: Smart Tags
role: Admin, User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 7%

---


# 將智慧標籤新增至AEM中的資產 {#smart-tags-assets-aem}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/enhanced-smart-tags.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制的辭彙。 基本上，它包括員工、合作夥伴和客戶通常用來參照和搜尋其數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，以確保在搜尋中可輕鬆識別和擷取資產。

相較於自然語言辭彙，根據商業分類法標籤有助於讓資產與公司的業務保持一致，並確保最相關的資產出現在搜尋中。 例如，汽車製造商可以使用模型名稱來標籤汽車影像，這樣在搜尋時便只會顯示相關影像，以設計促銷活動。

在背景中，此功能使用[Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html)的人工智慧型架構，根據您的標籤結構和商業分類訓練其影像辨識演演算法。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 依預設，AEM會自動將智慧標籤套用至已上傳的資產。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## AEM中智慧標籤支援的資產型別 {#smart-tags-supported-file-formats}

您可以標籤下列資產型別：

* **影像**：使用Adobe Sensei的智慧內容服務標籤許多格式的影像。 您[建立訓練模型](#train-model)，然後上傳的影像就會自動加上標籤。 智慧標籤會套用至支援的檔案型別，這些檔案型別會產生JPG和PNG格式的轉譯。
* **文字型資產**： [!DNL Experience Manager Assets]在上傳時會自動標籤支援的文字型資產。
* **視訊資產**：視訊標籤在[!DNL Adobe Experience Manager]中預設為[!DNL Cloud Service]啟用。 當您上傳新視訊或重新處理現有視訊時，[視訊會自動加上標籤](/help/assets/smart-tags-video-assets.md)。

| 影像（MIME型別） | 文字型資產（檔案格式） | 視訊資產（檔案格式和轉碼器） |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC，運動JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC、vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap | |  |
| image/x-xpixmap | |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

AEM預設會將智慧標籤自動新增至文字型資產和影片。 若要將智慧標籤自動新增至影像，請完成下列工作。

* [瞭解標籤模型與准則](#understand-tag-models-guidelines)。
* [訓練模型](#train-model)。
* [標籤您的數位資產](#tag-assets)。
* [管理標籤與搜尋](#manage-smart-tags-and-searches)。

## 瞭解標籤模型和指導方針 {#understand-tag-models-guidelines}

標籤模型是一組相關標籤，這些標籤與要標籤的影像的各種視覺方面相關聯。 標籤與影像明顯不同的視覺效果有關，因此套用標籤時，有助於搜尋特定型別的影像。 例如，一個鞋子系列可以有不同的標籤，但所有標籤都與鞋子相關，並且可以屬於相同的標籤模型。 套用時，標籤可協助尋找不同型別的鞋子，例如依設計或用途。 若要瞭解[!DNL Experience Manager]中訓練模型的內容表示法，請將訓練模型視覺化為由一組手動新增的標籤和每個標籤的範例影像組成的最上層實體。 每個標籤都只能套用到影像。

建立標籤模型並訓練服務之前，請先識別一組最能描述企業內容中影像中物件的唯一標籤。 確定已組織集中的資產符合[訓練准則](#training-guidelines)。

### 訓練准則 {#training-guidelines}

請確定訓練集中的影像符合下列准則：

**數量與大小：**&#x200B;每個標籤至少10個影像，最多50個影像。

**Coherence**：請確定標籤的影像在視覺上類似。 最好將相同視覺方面（例如影像中相同型別的物件）的標籤一起加入單一標籤模型中。 例如，將這些影像標示為`my-party` （用於訓練）是不好的做法，因為這些影像在視覺上並不相似。

![說明性影像，以示範訓練准則](assets/do-not-localize/coherence.png)

**涵蓋範圍**：訓練中的影像應有足夠的變化。 我們的想法是提供幾個但相當多樣化的範例，讓[!DNL Experience Manager]學習聚焦於正確的事。 如果您要在視覺上相異的影像上套用相同的標籤，請至少包含每種型別的五個範例。 例如，對於標籤&#x200B;*模型向下姿態*，請包含更多與下方反白影像類似的訓練影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像，以示範訓練准則](assets/do-not-localize/coverage_1.png)

**干擾/阻撓**：此服務會針對干擾較少的影像（顯著的背景、不相關的伴侶，例如主主題的物件/人員）提供更好的訓練。 例如，對於標籤&#x200B;*休閒鞋*，第二個影像不是良好的訓練候選項。

![說明性影像，以示範訓練准則](assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤(例如 *Raincoat***&#x200B;和模型側檢視)，請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![說明性影像，以示範訓練准則](assets/do-not-localize/completeness.png)

**標籤數目**：Adobe建議您使用至少兩個不同的標籤以及每個標籤至少十個不同的影像來訓練模型。 在單一標籤模型中，請勿新增超過50個標籤。

**範例數目**：請為每個標籤新增至少10個範例。 不過，Adobe建議使用約30個範例。 支援每個標籤最多50個範例。

**避免誤判和衝突**： Adobe建議為單一視覺方面建立單一標籤模型。 以可避免標籤在模型之間重疊的方式建構標籤模型。 例如，請勿在兩個不同的標籤模型名稱`shoes`和`footwear`中使用像`sneakers`這樣的通用標籤。 針對常見關鍵字，訓練程式會以一個已訓練標籤模型覆寫另一個已訓練標籤模型。

**範例**：更多指南範例為：

* 建立僅包含、

   * 和汽車模型相關的標籤。
   * 這些標籤與成人和兒童的夾克有關。

* 不要建立，

   * 標籤模型，包含2019年和2020年發行的汽車模型。
   * 包含相同幾個車型的多個標籤模型。

**用來訓練的影像**：您可以使用相同的影像來訓練不同的標籤模型。 不過，請勿將影像與標籤模型中的多個標籤相關聯。 您可以使用屬於不同標籤模型的不同標籤來標籤相同影像。

您無法復原培訓。 上述准則應可協助您選擇要訓練的良好影像。

## 為您的自訂標籤訓練模型 {#train-model}

若要建立並訓練特定企業標籤的模型，請遵循下列步驟：

1. 建立必要的標籤和適當的標籤結構。 上傳DAM存放庫中的相關影像。
1. 在[!DNL Experience Manager]使用者介面中，存取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 智慧標籤訓練]**。
1. 按一下「**[!UICONTROL 建立]**」。提供&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 描述]**。
1. 按一下&#x200B;**[!UICONTROL 標籤]**&#x200B;欄位中的資料夾圖示。 隨即開啟快顯視窗。
1. 從`cq-tags`中您想要新增至模型的現有標籤中，搜尋或選取適當的標籤。 按一下「**[!UICONTROL 下一步]**」。

   >[!NOTE]
   >
   >您可以根據&#x200B;**[!UICONTROL Name]** （字母順序）、**[!UICONTROL 已建立]**&#x200B;日期或&#x200B;**[!UICONTROL 已修改]**&#x200B;日期，以遞增或遞減順序來排序標籤結構。


1. 在&#x200B;**[!UICONTROL 選取Assets]**&#x200B;對話方塊中，針對每個標籤按一下&#x200B;**[!UICONTROL 新增Assets]**。 在DAM存放庫中搜尋，或瀏覽存放庫以選取至少10個和最多50個影像。 請選取資產，而非資料夾。 選取影像之後，按一下&#x200B;**[!UICONTROL 選取]**。

   ![檢視訓練狀態](assets/smart-tags-training-status.png)

1. 若要預覽所選影像的縮圖，請按一下標籤前方的摺疊式功能表。 您可以按一下&#x200B;**[!UICONTROL 新增Assets]**&#x200B;來修改您的選擇。 對選取專案滿意後，按一下&#x200B;**[!UICONTROL 提交]**。 使用者介面會在頁面底部顯示通知，指示已啟動培訓。
1. 檢查每個標籤模型在&#x200B;**[!UICONTROL 狀態]**&#x200B;欄中的訓練狀態。 可能的狀態為[!UICONTROL 擱置中]、[!UICONTROL 已訓練]及[!UICONTROL 失敗]。

![訓練智慧標籤的標籤模型的工作流程](assets/smart-tag-model-training-flow.png)

*圖：訓練工作流程以訓練標籤模型的步驟。*

### 檢視訓練狀態和報表 {#training-status}

若要檢查智慧型標籤服務是否已在您的資產培訓集中的標籤上接受培訓，請從「報表」控制檯檢閱培訓工作流程報表。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 報表]**。
1. 在&#x200B;**[!UICONTROL 資產報表]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 選取「**[!UICONTROL 智慧標籤培訓]**」報表，然後從工具列按一下「**[!UICONTROL 下一步]**」。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，從工具列按一下&#x200B;**[!UICONTROL 建立]**。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下工具列中的&#x200B;**[!UICONTROL 檢視]**。
1. 檢閱報告的詳細資訊。 報表會顯示您所訓練之標籤的訓練狀態。**[!UICONTROL 培訓狀態]**&#x200B;欄中的綠色表示智慧型標籤服務已接受標籤的培訓。 黃色表示服務已針對特定標籤進行部分訓練。 若要針對標籤完整地訓練服務，請使用特定標籤新增更多影像，並執行訓練工作流程。 如果您在此報告中未看到您的標籤，請再次執行這些標籤的培訓工作流程。標籤
1. 若要下載報表，請從清單中選取報表，然後按一下工具列中的[下載]。 ****&#x200B;報表會下載為試算表。

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## 在AEM中使用智慧標籤來標籤資產 {#tag-assets}

上傳時[!DNL Experience Manager Assets]會自動標籤所有支援的資產型別。 標籤功能預設為啟用並運作。 AEM會近乎即時套用適當的智慧標籤。<!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 針對影像和影片，智慧標籤是以某些視覺方面為基礎。

* 對於文字型資產，智慧標籤的功效並不取決於資產中的文字數量，而是取決於資產文字中出現的相關關鍵字或實體。 對於文字型資產，智慧標籤是出現在文字中的關鍵字，但最能描述資產的關鍵字。 針對支援的資產，[!DNL Experience Manager]已擷取文字，然後編制索引並用於搜尋資產。 不過，以文字中的關鍵字為基礎的智慧標籤可提供專用的、結構化的和較高優先順序的搜尋Facet。 相較於搜尋索引，後者有助於改善資產探索。

## 管理智慧標籤和資產搜尋 {#manage-smart-tags-and-searches}

您可以組織智慧標籤，移除任何可能已指派給品牌資產的不正確標籤，以便只顯示最相關的標籤。

仲裁智慧標籤也可確保您的資產出現在最相關標籤的搜尋結果中，藉此協助調整資產的標籤式搜尋。 基本上，它有助於避免無關資產出現在搜尋結果中的機會。

您也可以為標籤指派較高的排名，以增加標籤與資產的相關性。 根據特定標籤執行搜尋時，為資產促銷標籤會增加資產出現在搜尋結果中的機會。

若要稽核數位資產的智慧標籤：

1. 在搜尋欄位中，根據標籤搜尋數位資產。

1. 若要識別您找不到與搜尋相關的數位資產，請檢查搜尋結果。

1. 選取資產，然後從工具列選取![管理標籤圖示](assets/do-not-localize/manage-tags-icon.png)。

1. 從&#x200B;**[!UICONTROL 管理標籤]**&#x200B;頁面，檢查標籤。 如果您不想根據特定標籤搜尋資產，請選取標籤，然後從工具列選取![刪除圖示](assets/do-not-localize/delete-icon.png)。 或者，選取標籤旁的`X`符號。

1. 若要指派較高的排名給標籤，請選取該標籤，然後從工具列選取![促銷圖示](assets/do-not-localize/promote-icon.png)。 您促銷的標籤已移至&#x200B;**[!UICONTROL 標籤]**&#x200B;區段。

1. 選取「**[!UICONTROL 儲存]**」，然後選取「**[!UICONTROL 確定]**」以關閉[!UICONTROL 成功]對話方塊。

1. 導覽至資產的[!UICONTROL 屬性]頁面。 請注意，您提升的標籤會獲得較高的關聯性，因此出現在搜尋結果中較高的位置。

### 瞭解包含智慧標籤的[!DNL Experience Manager]搜尋結果 {#understand-search}

依預設，[!DNL Experience Manager]搜尋會將搜尋字詞與`AND`子句結合。 使用智慧標籤不會變更此預設行為。 使用智慧標籤會新增`OR`子句，以尋找套用的智慧標籤中的任何搜尋字詞。 例如，考慮搜尋`woman running`。 依預設，中繼資料中只有`woman`或只有`running`關鍵字的Assets不會出現在搜尋結果中。 但是，使用智慧標籤以`woman`或`running`標籤的資產會出現在這樣的搜尋查詢中。 所以搜尋結果是，

* Assets的中繼資料中有`woman`和`running`個關鍵字。

* 使用任一關鍵字加上標籤的Assets智慧標籤。

符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 在上述範例中，顯示搜尋結果的大約順序為：

1. 符合各種中繼資料欄位中的`woman running`。
1. 符合智慧標籤中的`woman running`。
1. 符合智慧標籤中的`woman`或`running`。

## 標籤相關的限制和最佳作法 {#limitations}

增強型智慧標籤是以影像及其標籤的學習模型為基礎。 這些模型並非總能完美地識別標籤。 目前版本的智慧標籤有下列限制：

* 無法辨認影像中的細微差異。 例如，超薄襯衫和一般襯衫。
* 無法根據影像的微小模式或部分識別標籤。 例如，襯衫上的標誌。
* [!DNL Experience Manager]支援的語言支援標籤。
* 未處理的標籤與：

   * 非視覺化抽象層面。 例如，產品發佈的年份或季節、影像引發的情緒或情感，以及視訊的主觀內涵。
   * 產品的細微視覺差異，例如有領襯衫和沒有領子的襯衫，或嵌入在產品上的小產品標誌。

若要訓練模型，請使用最適當的影像。 訓練無法還原，或訓練模型無法移除。 您的標籤正確性取決於目前的訓練，所以請謹慎行事。

<!-- TBD: Add limitations related to text files. -->

若要搜尋具有智慧標籤（一般或增強功能）的檔案，請使用[!DNL Assets]搜尋（全文檢索搜尋）。 智慧標籤沒有單獨的搜尋述詞。

>[!NOTE]
>
>智慧標籤培訓您的標籤以及將其套用至其他影像的能力取決於您用於培訓的影像品質。
>為達到最佳效果，Adobe建議您使用視覺上相似的影像，針對每個標籤來訓練服務。

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

>[!MORELIKETHIS]
>
>* [瞭解智慧標籤如何協助管理您的數位檔案](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [對影片使用智慧標籤](smart-tags-video-assets.md)
