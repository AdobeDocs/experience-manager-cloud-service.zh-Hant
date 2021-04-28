---
title: 使用 [!DNL Adobe Sensei] smart服務自動標籤資產
description: 使用人工智慧型服務來標籤資產，該服務會套用情境式和描述性的商業標籤。
contentOwner: AG
feature: 智慧標籤，標籤
role: Administrator,Business Practitioner
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
translation-type: tm+mt
source-git-commit: 87d7cbb4463235a835d18fce49d06315a7c87526
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 6%

---


# 將智慧標籤新增至資產以改善搜尋體驗{#smart-tag-assets-for-faster-search}

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制辭彙。 基本上，它包含員工、合作夥伴和客戶常用來參考及搜尋其數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，可確保在搜尋中輕鬆識別和擷取資產。

與自然語言辭彙相比，基於業務分類法的標籤有助於使資產與公司的業務保持一致，並確保最相關的資產出現在搜索中。 例如，汽車製造商可以使用型號名稱來標籤汽車影像，以便在搜尋以設計促銷活動時只顯示相關影像。

在背景中，該功能使用人為智慧的[Adobe Sensei](https://www.adobe.com/tw/sensei/experience-cloud-artificial-intelligence.html)框架，在標籤結構和業務分類上訓練其影像識別算法。 然後，此內容智慧會用來將相關標籤套用至不同的資產集。 預設情況下，新的[!DNL Experience Manager Assets]部署與[!DNL Adobe Developer Console]整合。 它可協助您更快速地設定智慧標籤功能。 在舊版部署中，管理員可以手動[設定智慧標籤整合](/help/assets/smart-tags-configuration.md#aio-integration)。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## 支援的資產類型{#smart-tags-supported-file-formats}

您可以標籤下列資產類型：

* **影像**:使用Adobe Sensei的智慧型內容服務，標籤許多格式的影像。您[建立訓練模型](#train-model)，然後[將智慧標籤](#tag-assets)套用至影像。 智慧型標籤會套用至支援的檔案類型，這些檔案類型會產生JPG和PNG格式的轉譯。
* **文字型資產**: [!DNL Experience Manager Assets] 在上傳時自動標籤支援的文字型資產。進一步瞭解[標籤文字型資產](#smart-tag-text-based-assets)。
* **視訊資產**:視訊標籤預設會以 [!DNL Adobe Experience Manager] a的形式啟用 [!DNL Cloud Service]。[當您上傳新視訊或](/help/assets/smart-tags-video-assets.md) 重新處理現有視訊時，視訊會自動標籤。

| 影像（MIME類型） | 文字型資產（檔案格式） | 視訊資產（檔案格式和轉碼器） |
|----|-----|------|
| image/jpeg | CSV | MP4(H264/AVC) |
| image/tiff | DOC | MKV(H264/AVC) |
| image/png | DOCX | MOV(H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI(indeo4) |
| image/gif | JSON | FLV(H264/AVC, vp6f) |
| image/pjpeg | PDF | WMV(WMV2) |
| image/x-portable-anymap | PPT |  |
| image/x-portable-bitmap | PPTX |  |
| image/x-portable-graymap | RTF |  |
| image/x-portable-pixmap | SRT |  |
| 影像/x-rgb | TXT |  |
| image/x-xbitmap | VTT |  |
| image/x-xpixmap | XML |  |
| image/x-icon |  |  |
| 影像/photoshop |  |  |
| image/x-photoshop |  |  |
| 影像/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] 依預設，自動將智慧型標籤新增至文字型資產和視訊。若要自動將智慧型標籤新增至影像，請完成下列工作。

* [瞭解標籤模型和准則](#understand-tag-models-guidelines)。
* [訓練模型](#train-model)。
* [標籤您的數位資產](#tag-assets)。
* [管理標籤和搜尋](#manage-smart-tags-and-searches)。

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## 使用智慧型標籤{#smart-tag-text-based-assets}標籤文字型資產

上傳時，支援的文字型資產會由[!DNL Experience Manager Assets]自動標籤。 預設會啟用。 智慧型標籤的效能不取決於資產中的文字數量，而取決於資產文字中顯示的相關關鍵字或實體。 對於文字型資產，智慧型標籤是顯示在文字中的關鍵字，但是最能說明資產的關鍵字。 對於受支援的資產，[!DNL Experience Manager]已擷取文字，接著會建立索引並用來搜尋資產。 不過，文字中以關鍵字為基礎的智慧型標籤提供專用、結構化和較高優先順序的搜尋Facet，與完整搜尋索引相比，可用來改善資產搜尋。

相較之下，對於影像和視訊，智慧型標籤是根據某些視覺方面衍生而來。

## 瞭解標籤模型和准則{#understand-tag-models-guidelines}

標籤模型是一組相關標籤，這些標籤與要標籤的影像的各種視覺方面相關聯。 標籤與影像的視覺方面有明顯不同的關係，因此套用標籤時，標籤有助於搜尋特定類型的影像。 例如，鞋類系列可以有不同的標籤，但所有標籤都與鞋類相關，且可屬於相同的標籤模型。 套用時，標籤會協助您尋找不同類型的鞋，例如依顏色、依設計或依使用情形。 若要瞭解[!DNL Experience Manager]中訓練模型的內容呈現，請將訓練模型視為頂層實體，由一組手動新增的標籤和每個標籤的範例影像組成。 每個標籤都可以排他性地套用至影像。

在您建立標籤模型並訓練服務之前，請先識別一組最能說明業務情境中影像物件的獨特標籤。 確定您所策劃的資產符合[訓練方針](#training-guidelines)。

### 訓練方針{#training-guidelines}

確保訓練集中的影像符合下列准則：

**數量和大小：每** 個標籤最少10張影像和最多50張影像。

**一致性**:請確定標籤的影像外觀類似。最好將與相同視覺層面（例如影像中的相同物件類型）相關的標籤加入單一標籤模型。 例如，將所有這些影像標籤為`my-party`（用於訓練）並不好，因為它們在視覺上並不相似。

![示例性影像，以示訓練指南](assets/do-not-localize/coherence.png)

**涵蓋範圍**:培訓中的影像應該有足夠的多樣性。我們的想法是提供一些比較多樣化的例子，AEM讓學習將注意力放在正確的事上。 如果您要在視覺上不相同的影像上套用相同的標籤，請至少包含5種不同類型的範例。 例如，對於標籤&#x200B;*model-down-pose*，為服務加入更多類似下方反白顯示影像的訓練影像，以便在標籤期間更精確地識別類似影像。

![示例性影像，以示訓練指南](assets/do-not-localize/coverage_1.png)

**干擾／妨礙**:該服務更能訓練那些分散注意力的影像（突出的背景、不相關的伴奏，如主題的物體／人）。例如，對於標籤&#x200B;*休閒鞋*，第二個影像不是好的訓練候選影像。

![示例性影像，以示訓練指南](assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤(例如 *Raincoat***&#x200B;和模型側檢視)，請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![示例性影像，以示訓練指南](assets/do-not-localize/completeness.png)

**標籤數**:Adobe建議您使用至少兩個不同的標籤和至少十個不同的影像來訓練模型。在單一標籤模型中，請勿新增超過50個標籤。

**範例數**:對於每個標籤，請至少新增十個範例。不過，Adobe建議大約30個例子。 每個標籤最多支援50個範例。

**防止誤報和衝突**:Adobe建議針對單一視覺方面建立單一標籤模型。以避免模型之間重疊標籤的方式來建構標籤模型。 例如，請勿在兩個不同的標籤模型中使用例如`sneakers`的常用標籤，例如`shoes`和`footwear`。 訓練程式會覆寫一個已訓練的標籤模型與另一個模型，以取代一個常用關鍵字。

**範例**:其他的指引範例包括：

* 建立包含、
   * 只有與車型相關的標籤。
   * 只有襯衫顏色相關的標籤。
   * 只有男女外套的標籤。
* 不要建立，
   * 一種標籤模型，包括2019年和2020年發佈的車型。
   * 包含相同數種車型的多種標籤模型。

**用於訓練的影像**:您可以使用相同的影像來訓練不同的標籤模型。不過，請勿將影像與標籤模型中的多個標籤建立關聯。 您可以使用屬於不同標籤模型的不同標籤來標籤相同影像。

您無法撤消培訓。 上述准則應協助您選擇要訓練的好影像。

## 針對您的自訂標籤訓練模型{#train-model}

要為業務特定標籤建立和培訓模型，請遵循以下步驟：

1. 建立必要的標籤和適當的標籤結構。 在DAM儲存庫中上傳相關影像。
1. 在[!DNL Experience Manager]使用者介面中，存取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 智慧型標籤訓練]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。提供&#x200B;**[!UICONTROL Title]**、**[!UICONTROL 說明]**。
1. 瀏覽並從`cq:tags`中要訓練模型的現有標籤中選擇標籤。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 選擇資產]**&#x200B;對話方塊中，針對每個標籤按一下&#x200B;**[!UICONTROL 新增資產]**。 在DAM儲存庫中搜索或瀏覽儲存庫以選擇至少10個和最多50個映像。 選取資產，而非資料夾。 選擇影像後，按一下「選擇&#x200B;****」。

   ![檢視培訓狀態](assets/smart-tags-training-status.png)

1. 若要預覽選取影像的縮圖，請按一下標籤前面的accordion。 您可以按一下「新增資產」，以修改您的選擇。 ****&#x200B;對選擇滿意後，按一下&#x200B;**[!UICONTROL 提交]**。 使用者介面在頁面底部顯示通知，指出已開始培訓。
1. 在&#x200B;**[!UICONTROL Status]**&#x200B;欄中檢查每個標籤模型的培訓狀態。 可能的狀態包括[!UICONTROL Pending]、[!UICONTROL Traned]和[!UICONTROL Failed]。

![為智慧型標籤訓練標籤模型的工作流程](assets/smart-tag-model-training-flow.png)

*圖：培訓工作流程中訓練標籤模型的步驟。*

### 檢視培訓狀態並報告{#training-status}

若要檢查智慧型標籤服務是否在訓練資產集中的標籤上接受訓練，請從報告主控台檢視訓練工作流程報告。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**。
1. 在&#x200B;**[!UICONTROL 資產報表]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 選擇&#x200B;**[!UICONTROL 智慧型標籤訓練]**&#x200B;報表，然後從工具列按一下&#x200B;**[!UICONTROL Next]**。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，從工具列按一下「建立」。****
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下工具列上的&#x200B;**[!UICONTROL 檢視]**。
1. 檢閱報表的詳細資訊。 報表會顯示您所訓練之標籤的訓練狀態。**[!UICONTROL 訓練狀態]**&#x200B;欄中的綠色表示智慧型標籤服務已接受標籤訓練。 黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。如果您在此報表中未看到標籤，請針對這些標籤重新執行培訓工作流程。標籤
1. 若要下載報表，請從清單中選取報表，然後從工具列按一下「下載&#x200B;**[!UICONTROL 」。]**&#x200B;報表會以[!DNL Microsoft Excel]試算表的形式下載。

## 標籤資產{#tag-assets}

在您培訓了「智慧標籤」服務後，可以觸發標籤工作流程，以自動套用標籤至不同的資產集。 您可以隨選套用標籤工作流程，或排程它定期執行。 標籤工作流程同時套用至資產和資料夾。

### 從工作流程控制台{#tagging-assets-from-the-workflow-console}標籤資產

1. 在[!DNL Experience Manager]介面中，轉至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從&#x200B;**[!UICONTROL 工作流模型]**&#x200B;頁面中，選擇&#x200B;**[!UICONTROL DAM智慧標籤資產]**&#x200B;工作流，然後從工具欄中按一下&#x200B;**[!UICONTROL 啟動工作流]**。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在&#x200B;**[!UICONTROL 執行工作流程]**&#x200B;對話方塊中，瀏覽至包含您要自動套用標籤之資產的裝載資料夾。
1. 指定工作流程的標題和選用的註解。 按一下&#x200B;**[!UICONTROL 運行]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   *圖：導覽至資產資料夾並檢閱標籤，以確認您的資產是否已正確標籤。如需詳細資訊，請參閱[管理智慧型標籤](#manage-smart-tags-and-searches)。*

### 從時間軸{#tagging-assets-from-the-timeline}標籤資產

1. 從[!DNL Assets]使用者介面中，選取包含您要套用智慧標籤之資產或特定資產的檔案夾。
1. 從左上角開啟&#x200B;**[!UICONTROL 時間軸]**。
1. 從左側邊欄底部開啟動作，然後按一下「開始工作流程」。****

   ![start_workflow](assets/start_workflow.png)

1. 選擇&#x200B;**[!UICONTROL DAM智慧型標籤資產]**&#x200B;工作流程，並指定工作流程的標題。
1. 按一下&#x200B;**[!UICONTROL 開始]**。 工作流程會將您的標籤套用在資產上。 導覽至資產資料夾並檢閱標籤，以確認您的資產已正確標籤。 如需詳細資訊，請參閱[管理智慧型標籤](#manage-smart-tags-and-searches)。

>[!NOTE]
>
>在後續的標籤週期中，只有修改過的資產會再次使用新訓練的標籤進行標籤。 不過，如果標籤工作流程的最後一個與目前標籤週期之間的間隔超過24小時，則即使未變更的資產也會被標籤。 對於定期標籤工作流程，未變更的資產會在時間間隔超過6個月時加以標籤。

### 標籤已上傳的資產{#tag-uploaded-assets}

[!DNL Experience Manager] 可自動標籤使用者上傳至DAM的資產。為此，管理員會設定工作流程，以新增可標籤資產的可用步驟。 請參閱[如何為已上傳的資產啟用智慧標籤](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)。

## 管理智慧標籤和資產搜尋{#manage-smart-tags-and-searches}

您可以組織智慧型標籤，移除可能指派給品牌資產的任何不正確標籤，如此只會顯示最相關的標籤。

協調智慧型標籤也有助於透過確保資產出現在搜尋結果中，以便找出最相關的標籤，來調整以標籤為基礎的資產搜尋。 實際上，它有助於消除不相關資產出現在搜尋結果中的可能性。

您也可以指派較高的排名給標籤，以增加標籤與資產的關聯性。 促銷資產的標籤會增加當根據特定標籤執行搜尋時，資產出現在搜尋結果中的機率。

若要協調資產的智慧標籤：

1. 在搜尋欄位中，根據標籤搜尋資產。

1. Inspect搜尋結果，以識別您找不到與您搜尋相關的資產。

1. 選擇資產，然後從工具列選擇![管理標籤圖示](assets/do-not-localize/manage-tags-icon.png)。

1. 從&#x200B;**[!UICONTROL 管理標籤]**&#x200B;頁面檢查標籤。 如果您不希望根據特定標籤來搜尋資產，請選取標籤並從工具列選取「刪除」圖示![。 ](assets/do-not-localize/delete-icon.png)或者，選擇標籤旁的`X`符號。

1. 若要指派較高的排名給標籤，請選取標籤，然後從工具列選取「提升」圖示![。 ](assets/do-not-localize/promote-icon.png)您促銷的標籤會移至&#x200B;**[!UICONTROL Tags]**&#x200B;區段。

1. 選擇&#x200B;**[!UICONTROL 保存]**，然後選擇&#x200B;**[!UICONTROL 確定]**&#x200B;以關閉[!UICONTROL 成功]對話框。

1. 導覽至資產的[!UICONTROL 屬性]頁面。 請注意，您促銷的標籤已指派高關聯性，因此在搜尋結果中會顯示高度。

### 使用AEM智慧型標籤{#understand-search}瞭解搜尋結果

依預設，AEM搜尋會將搜尋詞與`AND`子句結合。 使用智慧型標籤不會變更此預設行為。 使用智慧型標籤會新增`OR`子句，以尋找套用智慧型標籤中的任何搜尋詞。 例如，請考慮搜索`woman running`。 預設情況下，中繼資料中只包含`woman`或`running`關鍵字的資產不會出現在搜尋結果中。 但是，使用智慧標籤標籤以`woman`或`running`標籤的資產會出現在此類搜尋查詢中。 所以搜索結果是，

* 資產，其中包含中繼資料中的`woman`和`running`關鍵字。

* 資產智慧標籤為其中一個關鍵字。

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 與各中繼資料欄位中`woman running`的相符項目。
1. 與智慧型標籤中`woman running`的相符項目。
1. 在智慧型標籤中符合`woman`或`running`。

## 標籤限制和最佳做法{#limitations}

增強的智慧型標籤是以學習影像模型及其標籤為基礎。 這些模型在識別標籤時並不總是十分完美。 智慧標籤的目前版本有下列限制：

* 無法辨識影像的細微差異。 例如，修身與普通襯衫。
* 無法根據影像的微小圖樣／部分來識別標籤。 例如，T恤上的標誌。
* [!DNL Experience Manager]支援的語言支援標籤。 如需語言清單，請參閱[智慧型內容服務發行說明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages)。
* 未實際處理的標籤與：

   * 非視覺化、抽象化的方面。 例如，產品的發佈年份或季節、影像所誘發的情緒或情緒、影片的主觀內涵等。
   * 產品（例如襯衫、襯衫、襯衫和襯衫）中嵌入有領結或無領結的小型產品標誌的細微視覺差異。

<!-- TBD: Add limitations related to text-based assets. -->

若要使用智慧型標籤（一般或增強功能）搜尋資產，請使用[!DNL Assets]搜尋（全文搜尋）。 智慧型標籤沒有個別的搜尋述詞。

>[!NOTE]
>
>智慧型標籤在您的標籤上進行訓練，並將它們套用至其他影像的能力，取決於您用於訓練的影像品質。
>為獲得最佳效果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。

>[!MORELIKETHIS]
>
>* [配 [!DNL Experience Manager] 置智慧標籤](smart-tags-configuration.md)
>* [瞭解智慧型標籤如何協助管理資產](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [智慧標籤視訊資產](smart-tags-video-assets.md)

