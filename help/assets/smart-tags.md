---
title: 自動標籤資產，具有 [!DNL Adobe Sensei] 智慧服務
description: 使用套用情境式和描述性商業標籤的人工智慧服務來標籤資產。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 5bf764c84d6676b575371bd865538a3f2c13a2ab
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 5%

---


# 新增智慧標籤至資產並改善搜尋體驗 {#smart-tag-assets-for-faster-search}

處理數位資產的組織，在資產中繼資料中越來越多地使用分類法控制的辭匯。 基本上，它包含員工、合作夥伴和客戶通常用來參考和搜尋其數位資產的關鍵字清單。 使用分類控制的辭匯來標籤資產，以確保在搜尋中輕鬆識別及擷取資產。

與自然語言辭匯相比，基於業務分類法的標籤有助於使資產與公司的業務一致，並確保最相關的資產出現在搜尋中。 例如，汽車製造商可以用型號標籤汽車影像，以便在搜索以設計促銷活動時只顯示相關影像。

在後台，該功能使用人工智慧框架 [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) 在您的標籤結構和業務分類上訓練其影像識別算法。 然後，系統會使用此內容智慧，將相關標籤套用至不同的資產集。 [!DNL Experience Manager Assets] 依預設，會自動將智慧標籤套用至已上傳的資產。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## 支援的資產類型 {#smart-tags-supported-file-formats}

您可以標籤下列類型的資產：

* **影像**:使用Adobe Sensei的智慧內容服務來標籤多種格式的影像。 您 [建立培訓模型](#train-model) 然後，上傳的影像會自動加上標籤。 智慧標籤會套用至支援的檔案類型，這些檔案類型會以JPG和PNG格式產生轉譯。
* **文字型資產**: [!DNL Experience Manager Assets] 上傳時自動標籤支援的文字型資產。
* **影片資產**:視訊標籤預設為在 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. [視訊會自動加上標籤](/help/assets/smart-tags-video-assets.md) 上傳新影片或重新處理現有影片時。

| 影像（MIME類型） | 文字型資產（檔案格式） | 視訊資產（檔案格式和轉碼器） |
|----|-----|------|
| image/jpeg | CSV | MP4(H264/AVC) |
| image/tiff | DOC | MKV(H264/AVC) |
| image/png | DOCX | MOV(H264/AVC，運動JPEG) |
| image/bmp | HTML | AVI(indeo4) |
| image/gif | PDF | FLV(H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV(WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| 影像/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] 依預設，自動將智慧標籤新增至文字型資產和影片。 若要自動將智慧標籤新增至影像，請完成下列工作。

* [了解標籤模型和准則](#understand-tag-models-guidelines).
* [訓練模型](#train-model).
* [標籤數位資產](#tag-assets).
* [管理標籤和搜尋](#manage-smart-tags-and-searches).

## 了解標籤模型和准則 {#understand-tag-models-guidelines}

標籤模型是一組相關標籤，它們與被標籤影像的各種視覺方面相關聯。 標籤與影像的明顯不同的視覺方面相關，以便當應用時，標籤有助於搜索特定類型的影像。 例如，鞋類集合可以有不同的標籤，但所有標籤都與鞋類相關，且可屬於相同的標籤模型。 套用時，標籤有助於尋找不同類型的鞋，例如依設計或使用方式。 若要了解 [!DNL Experience Manager]，可將訓練模型視為由一組手動新增的標籤和每個標籤的範例影像所組成的頂層實體。 每個標籤皆可專門套用至影像。

在建立標籤模型並訓練服務之前，請先識別一組唯一標籤，以最好地描述業務環境中影像中的物件。 確定組織集中的資產符合 [培訓指南](#training-guidelines).

### 培訓准則 {#training-guidelines}

確保訓練集中的影像符合以下准則：

**數量和大小：** 每個標籤最少10個影像和最多50個影像。

**一致性**:確認標籤的影像在視覺上類似。 最好將與相同視覺層面（例如影像中的相同物件類型）相關的標籤一併新增至單一標籤模型。 例如，將這些影像標籤為 `my-party` （用於訓練），因為視覺上不類似。

![說明性影像，以說明訓練准則](assets/do-not-localize/coherence.png)

**涵蓋範圍**:訓練中的影像應該有足夠的多樣性。 我們的想法是提供一些比較多樣的例子，這樣 [!DNL Experience Manager] 學會專注於正確的事情。 如果您要在視覺上不同的影像上套用相同的標籤，請至少包含五種類型的範例。 例如，對於標籤 *下姿態*，請加入更多類似下方醒目提示影像的訓練影像，讓服務在標籤時更準確地識別類似影像。

![說明性影像，以說明訓練准則](assets/do-not-localize/coverage_1.png)

**干擾/障礙**:該服務對分散注意力較少的影像進行更好的訓練（顯著背景、不相關的伴奏，如主題對象/人）。 例如，對於標籤 *休閒鞋*)，第二張影像不是好的訓練候選者。

![說明性影像，以說明訓練准則](assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤(例如 *Raincoat***&#x200B;和模型側檢視)，請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![說明性影像，以說明訓練准則](assets/do-not-localize/completeness.png)

**標籤數**:Adobe建議您針對每個標籤至少使用兩個不同標籤和至少十個不同影像來訓練模型。 在單一標籤模型中，請勿新增超過50個標籤。

**範例數**:請為每個標籤至少新增十個範例。 不過，Adobe建議大約30個範例。 每個標籤最多支援50個範例。

**防止誤判和衝突**:Adobe建議針對單一視覺效果建立單一標籤模型。 以避免模型之間重疊標籤的方式來結構標籤模型。 例如，請勿使用 `sneakers` 兩個不同的標籤模型名稱 `shoes` 和 `footwear`. 訓練程式會針對通用關鍵字，將一個訓練的標籤模型覆寫到另一個標籤模型。

**範例**:指引的其他範例包括：

* 建立僅包含、

   * 與車型相關的標籤。
   * 與成人和孩子穿的夾克相關的標籤。

* 請勿建立

   * 一種標籤型號，包括2019年和2020年發行的車型。
   * 包含相同數量車型的多個標籤模型。

**用於訓練的影像**:您可以使用相同的影像來訓練不同的標籤模型。 不過，請勿將影像與標籤模型中的多個標籤建立關聯。 可以使用屬於不同標籤模型的不同標籤來標籤相同影像。

您無法撤消培訓。 上述准則應可協助您選擇要訓練的良好影像。

## 訓練自訂標籤的模型 {#train-model}

若要建立並訓練業務特定標籤的模型，請遵循下列步驟：

1. 建立必要的標籤和適當的標籤結構。 在DAM存放庫中上傳相關影像。
1. 在 [!DNL Experience Manager] 使用者介面，存取 **[!UICONTROL 資產]** > **[!UICONTROL 智慧標籤訓練]**.
1. 按一下&#x200B;**[!UICONTROL 建立]**。提供 **[!UICONTROL 標題]**, **[!UICONTROL 說明]**.
1. 按一下 **[!UICONTROL 標籤]** 欄位。 隨即開啟彈出窗口。
1. 在中，從現有標籤搜尋或選取適當的標籤 `cq-tags` 要添加到模型中。 按一下&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >您可以根據 **[!UICONTROL 名稱]** （字母順序）, **[!UICONTROL 已建立]** 日期，或 **[!UICONTROL 已修改]** 日期。


1. 在 **[!UICONTROL 選取資產]** 對話框，按一下 **[!UICONTROL 新增資產]** 標籤。 在DAM存放庫中搜尋，或瀏覽存放庫以選取至少10個影像和最多50個影像。 選取資產，而非資料夾。 選取影像後，按一下 **[!UICONTROL 選擇]**.

   ![查看培訓狀態](assets/smart-tags-training-status.png)

1. 若要預覽所選影像的縮圖，請按一下標籤前方的折疊式功能表。 您可以按一下 **[!UICONTROL 新增資產]**. 對選取項目滿意後，按一下 **[!UICONTROL 提交]**. 用戶介面在頁面底部顯示通知，指示培訓已啟動。
1. 檢查 **[!UICONTROL 狀態]** 欄。 可能的狀態包括 [!UICONTROL 待定], [!UICONTROL 已訓練]，和 [!UICONTROL 失敗].

![為智慧標籤訓練標籤模型的工作流程](assets/smart-tag-model-training-flow.png)

*圖：訓練工作流程步驟，以訓練標籤模型。*

### 查看培訓狀態和報告 {#training-status}

若要檢查智慧標籤服務是否在資產訓練集的標籤上接受訓練，請從報表控制台檢閱訓練工作流程報表。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 **[!UICONTROL 資產報表]** 頁面，按一下 **[!UICONTROL 建立]**.
1. 選取 **[!UICONTROL 智慧標籤訓練]** 報告，然後按一下 **[!UICONTROL 下一個]** 的上界。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，按一下 **[!UICONTROL 建立]** 的上界。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下 **[!UICONTROL 檢視]** 的上界。
1. 檢閱報表的詳細資訊。 報表會顯示您所訓練之標籤的訓練狀態。中的綠色 **[!UICONTROL 培訓狀態]** 欄會指出智慧標籤服務已接受標籤的訓練。 黃色表示服務已針對特定標籤進行部分訓練。 若要完全針對標籤訓練服務，請使用特定標籤新增更多影像並執行訓練工作流程。 如果在此報告中看不到您的標籤，請再次執行這些標籤。標籤的培訓工作流
1. 若要下載報表，請從清單中選取報表，然後按一下 **[!UICONTROL 下載]** 的上界。 報表會以試算表形式下載。

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

## 使用智慧標籤標籤資產 {#tag-assets}

所有支援的資產類型都會自動加上標籤 [!DNL Experience Manager Assets] 上傳時。 預設會啟用標籤並運作。 [!DNL Experience Manager] 以近乎即時的方式套用適當的標籤。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 對於影像和視訊，智慧標籤會以某些視覺方面為基礎。

* 對於文字型資產，智慧標籤的功效不取決於資產中的文字數量，而取決於資產文字中出現的相關關鍵字或實體。 對於文字型資產，智慧標籤是顯示在文字中的關鍵字，但是最能說明資產的關鍵字。 針對支援的資產， [!DNL Experience Manager] 已擷取文字，接著會編列索引，用於搜尋資產。 不過，基於文字中關鍵字的智慧標籤可提供專用、結構化和高優先順序的搜尋面向。 與搜尋索引相比，後者有助於改善資產探索。

## 管理智慧標籤和資產搜尋 {#manage-smart-tags-and-searches}

您可以組織智慧標籤來移除指派給您品牌資產的任何不準確標籤，以便僅顯示最相關的標籤。

協調智慧標籤也可確保資產出現在最相關標籤的搜尋結果中，借此協助調整資產的標籤式搜尋。 基本上，這有助於消除不相關資產出現在搜索結果中的可能性。

您也可以指派較高的排名給標籤，以提高標籤與資產的相關性。 根據特定標籤執行搜尋時，提升資產的標籤會增加資產出現在搜尋結果中的機會。

若要協調數位資產的智慧標籤：

1. 在搜尋欄位中，根據標籤搜尋數位資產。

1. 若要識別您找不到與搜尋相關的數位資產，請檢查搜尋結果。

1. 選取資產，然後選取 ![「管理標籤」圖示](assets/do-not-localize/manage-tags-icon.png) 的上界。

1. 從 **[!UICONTROL 管理標籤]** 頁面，檢查標籤。 如果您不想要根據特定標籤來搜尋資產，請選取標籤並選取 ![刪除圖示](assets/do-not-localize/delete-icon.png) 的上界。 或者，選取 `X` 符號。

1. 若要指派較高的排名給標籤，請選取標籤並選取 ![「促銷」圖示](assets/do-not-localize/promote-icon.png) 的上界。 您促銷的標籤會移至 **[!UICONTROL 標籤]** 區段。

1. 選擇 **[!UICONTROL 儲存]** 然後選取 **[!UICONTROL 確定]** 關閉 [!UICONTROL 成功] 對話框。

1. 導覽至 [!UICONTROL 屬性] 頁面。 請注意，您促銷的標籤被指派為高關聯性，因此在搜尋結果中會顯示得較高。

### 了解 [!DNL Experience Manager] 使用智慧標籤搜尋結果 {#understand-search}

依預設， [!DNL Experience Manager] 搜尋會將搜尋詞與 `AND` 條。 使用智慧標籤不會變更此預設行為。 使用智慧標籤會新增 `OR` 子句，在應用的智慧標籤中查找任何搜索詞。 例如，請考慮搜尋 `woman running`. 只有 `woman` 或 `running` 預設情況下，中繼資料中的關鍵字不會出現在搜尋結果中。 不過，標籤有 `woman` 或 `running` 使用智慧標籤會出現在這類搜尋查詢中。 搜索結果是，

* 具有 `woman` 和 `running` 中繼資料中的關鍵字。

* 以任一關鍵字標示的資產智慧型。

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示約略順序為：

1. 比對 `woman running` 在各種中繼資料欄位中。
1. 比對 `woman running` 在智慧標籤中。
1. 比對 `woman` 或 `running` 在智慧標籤中。

## 標籤相關限制和最佳作法 {#limitations}

增強的智慧標籤是以學習影像及其標籤的模型為基礎。 這些模型在識別標籤時並非總是十分完美。 智慧標籤的目前版本有下列限制：

* 無法識別影像中的細微差異。 例如，纖薄與普通襯衫。
* 無法根據影像的微小模式或部分識別標籤。 例如，襯衫上的標誌。
* 支援在 [!DNL Experience Manager] 支援。 如需語言清單，請參閱 [智慧內容服務發行說明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* 未處理的標籤與下列項目相關：

   * 非視覺、抽象的方面。 例如，產品的發佈年份或季數、影像所誘發的情緒或情緒，以及視訊的主觀內涵。
   * 產品中的細微視覺差異，例如襯衫與襯衫之間有無領結，或產品上嵌入的小產品標誌。

要訓練模型，請使用最合適的影像。 無法還原培訓或無法刪除培訓模型。 標籤的正確性取決於當前培訓，因此請小心。

<!-- TBD: Add limitations related to text files. -->

若要搜尋含有智慧標籤的檔案（一般或增強），請使用 [!DNL Assets] 搜尋（全文搜尋）。 智慧標籤沒有單獨的搜尋述詞。

>[!NOTE]
>
>智慧標籤是否能在標籤上訓練並套用至其他影像，取決於您用於訓練的影像品質。
>為獲得最佳結果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。

>[!MORELIKETHIS]
>
>* [了解智慧標籤如何協助管理您的數位檔案](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [使用影片智慧標籤](smart-tags-video-assets.md)

