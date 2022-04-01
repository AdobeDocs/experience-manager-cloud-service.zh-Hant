---
title: 自動標籤資產 [!DNL Adobe Sensei] 智慧服務
description: 使用應用上下文和描述性業務標籤的人工智慧服務標籤資產。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 5bf764c84d6676b575371bd865538a3f2c13a2ab
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 5%

---


# 將智慧標籤添加到資產並改進搜索體驗 {#smart-tag-assets-for-faster-search}

處理數字資產的組織越來越多地在資產元資料中使用分類控制辭彙。 實際上，它包括一個關鍵字清單，員工、合作夥伴和客戶通常用來引用和搜索其數字資產。 使用分類控制辭彙標籤資產可確保在搜索中很容易識別和檢索資產。

與自然語言辭彙相比，基於業務分類的標籤有助於將資產與公司的業務相協調，並確保在搜索中出現最相關的資產。 例如，汽車製造商可以用型號名稱標籤汽車影像，因此在搜索以設計促銷活動時只顯示相關影像。

在後台，該功能使用人工智慧框架 [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) 根據標籤結構和業務分類來訓練其影像識別算法。 然後，該內容智慧被用於對不同的資產集應用相關標籤。 [!DNL Experience Manager Assets] 預設情況下，自動將智慧標籤應用於上載的資產。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## 支援的資產類型 {#smart-tags-supported-file-formats}

可以標籤以下類型的資產：

* **影像**:使用Adobe Sensei的智慧內容服務標籤多種格式的影像。 你 [建立培訓模型](#train-model) 然後自動對上傳的影像進行標籤。 智慧標籤將應用於支援的檔案類型，這些檔案類型以JPG和PNG格式生成格式副本。
* **基於文本的資產**: [!DNL Experience Manager Assets] 上載時自動標籤支援的基於文本的資產。
* **視頻資產**:預設情況下，在 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。 [視頻已自動標籤](/help/assets/smart-tags-video-assets.md) 上載新視頻或重新處理現有視頻時，

| 影像（MIME類型） | 基於文本的資產（檔案格式） | 視頻資產（檔案格式和編解碼器） |
|----|-----|------|
| image/jpeg | CSV | MP4(H264/AVC) |
| image/tiff | DOC | MKV(H264/AVC) |
| image/png | DOCX | MOV(H264/AVC，動作JPEG) |
| image/bmp | HTML | AVI(indeo4) |
| image/gif | PDF | FLV(H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV(WMV2) |
| 影像/x可移植任意圖 | PPTX |  |
| 影像/x可移植點陣圖 | RTF |  |
| 影像/x可移植灰度圖 | SRT |  |
| 影像/x攜帶型像素映射 | TXT |  |
| 影像/x-rgb | VTT |  |
| 影像/x-x點陣圖 |  |  |
| 影像/x-xpixmap |  |  |
| 影像/x表徵圖 |  |  |
| 影像/photoshop |  |  |
| 影像/x-photoshop |  |  |
| 影像/PSD |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] 預設情況下，自動將智慧標籤添加到基於文本的資產和視頻中。 要自動將智慧標籤添加到映像，請完成以下任務。

* [瞭解標籤模型和准則](#understand-tag-models-guidelines)。
* [訓練模型](#train-model)。
* [標籤您的數字資產](#tag-assets)。
* [管理標籤和搜索](#manage-smart-tags-and-searches)。

## 瞭解標籤模型和准則 {#understand-tag-models-guidelines}

標籤模型是一組相關標籤，它們與被標籤影像的各種視覺方面相關聯。 標籤與影像的明顯不同的視覺方面相關，因此當應用時，標籤有助於搜索特定類型的影像。 例如，鞋類收藏可以有不同的標籤，但所有標籤都與鞋類相關，並且可以屬於同一標籤模型。 應用時，標籤有助於查找不同類型的鞋，例如按設計或使用。 瞭解培訓模型的內容表示 [!DNL Experience Manager]，將培訓模型視為由一組手動添加的標籤和每個標籤的示例影像組成的頂級實體。 每個標籤可以排他地應用於影像。

在建立標籤模型並培訓服務之前，請確定一組最能描述業務上下文中影像中對象的唯一標籤。 確保所管理集中的資產符合 [培訓指南](#training-guidelines)。

### 培訓指南 {#training-guidelines}

確保培訓集中的影像符合以下准則：

**數量和大小：** 每個標籤最少10個影像和最多50個影像。

**一致性**:確保標籤的影像在視覺上相似。 最好將與相同視覺方面（例如影像中相同類型的對象）相關的標籤添加到單個標籤模型中。 例如，將所有這些影像標籤為 `my-party` （用於培訓），因為它們在視覺上不相似。

![說明性影像為培訓指南的範例](assets/do-not-localize/coherence.png)

**覆蓋範圍**:在訓練中，影像應該有足夠的多樣性。 我們的想法是提供一些比較多樣的例子，這樣 [!DNL Experience Manager] 學會專注於正確的事情。 如果在視覺上不相同的影像上應用相同的標籤，請至少包括五種不同類型的示例。 例如，對於標籤 *模型下姿態*，包括與下面突出顯示的影像類似的更多培訓影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像為培訓指南的範例](assets/do-not-localize/coverage_1.png)

**分心/妨礙**:該服務對分散度較小的影像（突出背景、不相關的伴奏，如主題對象/人）進行更好的訓練。 例如，對於標籤 *休閒鞋*&#x200B;第二幅不是很好的訓練對象。

![說明性影像為培訓指南的範例](assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤(例如 *Raincoat***&#x200B;和模型側檢視)，請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![說明性影像為培訓指南的範例](assets/do-not-localize/completeness.png)

**標籤數**:Adobe建議您使用至少兩個不同標籤和至少十個不同標籤的影像來訓練模型。 在單個標籤模型中，不要添加超過50個標籤。

**示例數**:對於每個標籤，至少添加十個示例。 但Adobe建議舉出約30個例子。 每個標籤最多支援50個示例。

**防止誤報和衝突**:Adobe建議為單個可視方面建立單個標籤模型。 以避免模型之間重疊標籤的方式構造標籤模型。 例如，不要使用類似 `sneakers` 兩個不同的標籤模型名稱 `shoes` 和 `footwear`。 該訓練過程將一個訓練的標籤模型與另一個標籤模型覆蓋一個公共關鍵字。

**示例**:指導的更多示例有：

* 建立僅包括、

   * 與車型相關的標籤。
   * 這些標籤與成人和兒童的外套有關。

* 不要建立，

   * 包括2019年和2020年發佈的車型的標籤模型。
   * 多個標籤型號，包括相同的幾款車型。

**用於訓練的影像**:可以使用相同的影像訓練不同的標籤模型。 但是，不要將影像與標籤模型中的多個標籤相關聯。 可以使用屬於不同標籤模型的不同標籤標籤同一影像。

無法撤消培訓。 以上准則應幫助您選擇好的影像進行培訓。

## 為自定義標籤培訓模型 {#train-model}

要為特定於業務的標籤建立和培訓模型，請執行以下步驟：

1. 建立必要的標籤和相應的標籤結構。 在DAM儲存庫中上載相關映像。
1. 在 [!DNL Experience Manager] 用戶介面，訪問 **[!UICONTROL 資產]** > **[!UICONTROL 智慧標籤培訓]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。提供 **[!UICONTROL 標題]**。 **[!UICONTROL 說明]**。
1. 按一下中的資料夾表徵圖 **[!UICONTROL 標籤]** 的子菜單。 將開啟一個彈出窗口。
1. 從中的現有標籤中搜索或選擇相應的標籤 `cq-tags` 要添加到模型中。 按一下&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >您可以根據 **[!UICONTROL 名稱]** （按字母順序排列）, **[!UICONTROL 已建立]** 日期或 **[!UICONTROL 已修改]** 日期。


1. 在 **[!UICONTROL 選擇資產]** 對話框，按一下 **[!UICONTROL 添加資產]** 標籤。 在DAM儲存庫中搜索或瀏覽儲存庫以選擇至少10個和最多50個映像。 選擇資產，而不是資料夾。 選擇影像後，按一下 **[!UICONTROL 選擇]**。

   ![查看培訓狀態](assets/smart-tags-training-status.png)

1. 要預覽所選影像的縮略圖，請按一下標籤前面的折疊面板。 可通過按一下 **[!UICONTROL 添加資產]**。 對所選內容感到滿意後，按一下 **[!UICONTROL 提交]**。 用戶介面在頁面底部顯示指示培訓已開始的通知。
1. 檢查中培訓的狀態 **[!UICONTROL 狀態]** 列。 可能的狀態為 [!UICONTROL 待定]。 [!UICONTROL 已培訓], [!UICONTROL 失敗]。

![用於為智慧標籤培訓標籤模型的工作流](assets/smart-tag-model-training-flow.png)

*圖：培訓工作流中培訓標籤模型的步驟。*

### 查看培訓狀態和報告 {#training-status}

要檢查智慧標籤服務是否在資產培訓集中的標籤上進行培訓，請從「報告」控制台查看培訓工作流報告。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。
1. 在 **[!UICONTROL 資產報表]** 的 **[!UICONTROL 建立]**。
1. 選擇 **[!UICONTROL 智慧標籤培訓]** 報告，然後按一下 **[!UICONTROL 下一個]** 的子菜單。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，按一下 **[!UICONTROL 建立]** 的子菜單。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。要查看報告，請按一下 **[!UICONTROL 視圖]** 的子菜單。
1. 查看報告的詳細資訊。 報表會顯示您所訓練之標籤的訓練狀態。中的綠色 **[!UICONTROL 培訓狀態]** 清單示已為標籤培訓智慧標籤服務。 黃色表示服務已針對特定標籤進行部分培訓。 要對服務進行完全的標籤培訓，請添加更多帶有特定標籤的影像並執行培訓工作流。 如果在此報告中看不到標籤，請再次執行這些標籤的培訓工作流。標籤
1. 要下載報告，請從清單中選擇它，然後按一下 **[!UICONTROL 下載]** 的子菜單。 報告以電子錶格形式下載。

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

所有類型的受支援資產都自動由 [!DNL Experience Manager Assets] 上載時。 預設情況下，標籤已啟用且有效。 [!DNL Experience Manager] 近即時應用相應的標籤。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 對於影像和視頻，智慧標籤基於某些視覺方面。

* 對於基於文本的資產，智慧標籤的效力不取決於資產中文本的數量，而取決於資產文本中存在的相關關鍵字或實體。 對於基於文本的資產，智慧標籤是文本中顯示的關鍵字，但是最能描述資產的關鍵字。 對於受支援的資產， [!DNL Experience Manager] 已提取文本，然後將其編入索引並用於搜索資產。 但是，基於文本中關鍵字的智慧標籤提供了專用、結構化和更高優先順序的搜索方面。 與搜索索引相比，後者有助於改善資產發現。

## 管理智慧標籤和資產搜索 {#manage-smart-tags-and-searches}

您可以建立智慧標籤，以刪除可能已分配給品牌資產的任何不準確標籤，以便只顯示最相關的標籤。

調整智慧標籤還有助於優化基於標籤的資產搜索，確保您的資產出現在最相關標籤的搜索結果中。 本質上，它有助於消除不相關資產出現在搜索結果中的可能性。

您還可以為標籤指定更高的等級，以增加標籤與資產的相關性。 當基於特定標籤執行搜索時，提升資產的標籤增加了在搜索結果中出現資產的可能性。

要調整數字資產的智慧標籤：

1. 在搜索欄位中，基於標籤搜索數字資產。

1. 要確定您找不到與搜索相關的數字資產，請檢查搜索結果。

1. 選擇資產，然後選擇 ![「管理標籤」表徵圖](assets/do-not-localize/manage-tags-icon.png) 的子菜單。

1. 從 **[!UICONTROL 管理標籤]** 頁面，檢查標籤。 如果不希望根據特定標籤搜索資產，請選擇該標籤並選擇 ![刪除表徵圖](assets/do-not-localize/delete-icon.png) 的子菜單。 或者，選擇 `X` 的子菜單。

1. 要為標籤分配更高的級別，請選擇標籤並選擇 ![「升級」表徵圖](assets/do-not-localize/promote-icon.png) 的子菜單。 您升級的標籤將移到 **[!UICONTROL 標籤]** 的子菜單。

1. 選擇 **[!UICONTROL 保存]** ，然後選擇 **[!UICONTROL 確定]** 關閉 [!UICONTROL 成功] 對話框。

1. 導航到 [!UICONTROL 屬性] 的子菜單。 請注意，您提升的標籤被分配為高相關性，因此在搜索結果中會顯示更高。

### 瞭解 [!DNL Experience Manager] 使用智慧標籤搜索結果 {#understand-search}

預設情況下， [!DNL Experience Manager] 搜索將搜索詞與 `AND` 。 使用智慧標籤不會更改此預設行為。 使用智慧標籤添加 `OR` 子句，以查找應用的smart標籤中的任何搜索項。 例如，請考慮搜索 `woman running`。 僅具有 `woman` 或者 `running` 預設情況下，元資料中的關鍵字不會出現在搜索結果中。 但是，標有 `woman` 或 `running` 在此類搜索查詢中顯示使用智慧標籤。 所以搜索結果是，

* 資產 `woman` 和 `running` 元資料中的關鍵字。

* 標籤了任一關鍵字的智慧資產。

首先顯示與元資料欄位中的所有搜索項相匹配的搜索結果，然後顯示與智慧標籤中任何搜索項相匹配的搜索結果。 在上例中，搜索結果的大致顯示順序是：

1. 匹配項 `woman running` 的子菜單。
1. 匹配項 `woman running` 在智慧標籤中。
1. 匹配項 `woman` 或 `running` 在智慧標籤中。

## 與標籤相關的限制和最佳做法 {#limitations}

增強的智慧標籤是基於影像及其標籤的學習模型。 這些模型在識別標籤方面並不總是十分完美。 智慧標籤的當前版本具有以下限制：

* 無法識別影像中的細微差異。 例如，修身襯衫和普通襯衫。
* 無法根據影像的微小圖案或部分識別標籤。 例如，襯衫上的徽標。
* 支援在以下語言中添加標籤 [!DNL Experience Manager] 支援。 有關語言的清單，請參見 [《 Smart Content Service發佈說明》](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages)。
* 未處理的標籤涉及：

   * 非視覺、抽象方面。 例如，產品發佈的年份或季度、影像所激發的情緒或情緒以及視頻的主觀內涵。
   * 產品中的細微視覺差異，例如在產品上嵌入或不嵌入領子或小產品標識的襯衫。

要訓練模型，請使用最合適的影像。 無法還原培訓或無法刪除培訓模型。 您的標籤準確性取決於當前培訓，因此請小心進行。

<!-- TBD: Add limitations related to text files. -->

要搜索具有智慧標籤（常規或增強）的檔案，請使用 [!DNL Assets] 搜索（全文搜索）。 智慧標籤沒有單獨的搜索謂詞。

>[!NOTE]
>
>智慧標籤在標籤上進行培訓並將其應用於其他影像的能力取決於您用於培訓的影像質量。
>為獲得最佳效果，Adobe建議您使用視覺上相似的影像來為每個標籤培訓服務。

>[!MORELIKETHIS]
>
>* [瞭解智慧標籤如何幫助管理數字檔案](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [將智慧標籤用於視頻](smart-tags-video-assets.md)

