---
title: 使用人工智慧服務來標籤影像。
description: 使用人工智慧服務來標籤影像，這些服務會使用Adobe Sensei服務套用情境式和描述性的商業標籤。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '2400'
ht-degree: 5%

---


# 訓練智慧型標籤服務並標籤您的影像 {#train-service-tag-assets}

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制辭彙。 基本上，它包含員工、合作夥伴和客戶常用來參考及搜尋其數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，可確保透過標籤搜尋輕鬆識別和擷取資產。

與自然語言辭彙相比，基於業務分類法的標籤有助於使資產與公司的業務保持一致，並確保最相關的資產出現在搜索中。 例如，汽車製造商可以使用型號名稱來標籤汽車影像，以便在搜尋以設計促銷活動時只顯示相關影像。

在背景中，智慧型標籤使用 [](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) Adobe Sensei的人工智慧架構，針對您的標籤結構和商業分類訓練其影像識別演算法。 然後，此內容智慧會用來將相關標籤套用至不同的資產集。

<!-- TBD: Create a similar flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

若要使用智慧標籤，請完成下列工作：

* [將Experience Manager與Adobe Developer Console整合](#integrate-aem-with-aio)。
* [瞭解標籤模型和准則](#understand-tag-models-guidelines)。
* [訓練模型](#train-model)。
* [標籤您的數位資產](#tag-assets)。
* [管理標籤和搜尋](#manage-smart-tags-and-searches)。

智慧型標籤僅適用於 [!DNL Adobe Experience Manager Assets] 客戶。 智慧型標籤可做為附加元件購買 [!DNL Experience Manager]。

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? -->

## 與Adobe [!DNL Experience Manager] Developer Console整合 {#integrate-aem-with-aio}

您可以使 [!DNL Adobe Experience Manager] 用Adobe Developer Console與智慧標籤整合。 使用此配置可從中訪問智慧標籤服務 [!DNL Experience Manager]。

請參 [閱設定Experience Manager，以便為要設定智慧標籤的任務](smart-tags-configuration.md) ，智慧標籤資產。 在後端，伺服器會先 [!DNL Experience Manager] 使用Adobe Developer Console閘道驗證您的服務認證，然後再將您的要求轉送至智慧標籤服務。

## 瞭解標籤模型和准則 {#understand-tag-models-guidelines}

標籤模型是一組相關標籤，由影像的視覺方面所組成。 例如，鞋類系列可以有不同的標籤，但所有標籤都與鞋類相關，且可屬於相同的標籤模型。 標籤只能與影像截然不同的視覺層面相關。 為了瞭解中培訓模型的內容表示 [!DNL Experience Manager]，請將培訓模型視為頂層實體，由一組手動添加的標籤和每個標籤的示例影像組成。 每個標籤都可以排他性地套用至影像。

無法實際處理的標籤與：

* 非視覺化、抽象的方面，例如由影像所誘發的產品的年份或發佈季節、情緒或情緒。
* 產品（例如襯衫、襯衫、襯衫和襯衫）中嵌入有領結或無領結的小型產品標誌的細微視覺差異。

在您建立標籤模型並訓練服務之前，請先識別一組最能說明業務情境中影像物件的獨特標籤。 確定您所策劃的資產符合培訓 [方針](#training-guidelines)。

### 培訓方針 {#training-guidelines}

訓練集中的影像應符合下列准則：

**數量和大小：** 每個標籤最少10個影像，最多50個影像。

**一致性**: 標籤的影像應類似視覺效果。 最好將相同視覺層面（例如影像中相同類型的物件）的標籤一起新增至單一標籤模型。 例如，將所有這些影像標籤為（用於訓練）並不 `my-party` 好，因為它們的視覺上不類似。

![示例性影像，以示訓練指南](assets/do-not-localize/coherence.png)

**涵蓋範圍**: 培訓中的影像應該有足夠的多樣性。 其想法是提供幾個相當多樣化的範例，讓AEM學會專注在正確的事物上。 如果您要在視覺上不相同的影像上套用相同的標籤，請至少包含5種不同類型的範例。 例如，對於標籤下模 *式姿勢*，請加入更多類似下方反白顯示影像的訓練影像，讓服務在標籤時更精確地識別類似影像。

![示例性影像，以示訓練指南](assets/do-not-localize/coverage_1.png)

**干擾／妨礙**: 該服務更能訓練那些分散注意力的影像（突出的背景、不相關的伴奏，如主題的物體／人）。 例如，對於標籤休閒 *鞋*，第二張影像不是好的訓練候選影像。

![示例性影像，以示訓練指南](assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤(例如 *Raincoat***&#x200B;和模型側檢視)，請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![示例性影像，以示訓練指南](assets/do-not-localize/completeness.png)

**標籤數**: Adobe建議您使用至少兩個不同的標籤和至少10個不同的影像來訓練模型。 在單一標籤模型中，請勿新增超過50個標籤。

**範例數**: 對於每個標籤，請至少新增10個範例。 不過，Adobe建議使用約30個範例。 每個標籤最多支援50個範例。

**防止誤報和衝突**: Adobe建議針對單一視覺化方面建立單一標籤模型。 以避免模型之間重疊標籤的方式來建構標籤模型。 例如，請勿使用常用標籤，例如在兩 `sneakers` 種不同的標籤模型名稱 `shoes` 和 `footwear`中。 訓練程式會覆寫一個已訓練的標籤模型與另一個模型，以取代一個常用關鍵字。

**範例**: 其他的指引範例包括：

* 建立包含、
   * 只有與車型相關的標籤。
   * 只有襯衫顏色相關的標籤。
   * 只有男女外套的標籤。
* 不要建立，
   * 一種標籤模型，包括2019年和2020年發佈的車型。
   * 包含相同數種車型的多種標籤模型。

**用於訓練的影像**: 您可以使用相同的影像來訓練不同的標籤模型。 不過，不會將影像與標籤模型中的多個標籤產生關聯。 因此，可以使用屬於不同標籤模型的不同標籤來標籤相同影像。

您無法復原培訓。 上述准則應協助您選擇要訓練的好影像。

## 針對自訂標籤訓練模型 {#train-model}

要為業務特定標籤建立和培訓模型，請遵循以下步驟：

1. 建立必要的標籤和適當的標籤結構。 在DAM儲存庫中上傳相關影像。
1. 在使 [!DNL Experience Manager] 用者介面中，存取「 **[!UICONTROL 資產]** >訓 **[!UICONTROL 練模型」]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。提供 **[!UICONTROL 標題]**, **[!UICONTROL 說明]**。
1. 瀏覽並選取您要訓練模型的 `cq:tags` 現有標籤中的標籤。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在「選取 **[!UICONTROL 資產]** 」對話方塊中，按一 **[!UICONTROL 下每個標籤的「新增資產]** 」。 在DAM儲存庫中搜索或瀏覽儲存庫以選擇至少10個和最多50個映像。 選取資產，而非資料夾。 選取影像後，按一下「選 **[!UICONTROL 取」]**。
1. 若要預覽選取影像的縮圖，請按一下標籤前面的accordion。 您可以按一下「新增資產」來修 **[!UICONTROL 改您的選擇]**。 對選取結果滿意後，按一下「 **[!UICONTROL 提交]**」。 使用者介面在頁面底部顯示通知，指出已開始培訓。
1. 在「狀態」欄中檢查每個標 **[!UICONTROL 簽模型]** 的培訓狀態。 可能的狀態 [!UICONTROL 有「待定]」、「已 [!UICONTROL 培訓]」和「 [!UICONTROL 失敗]」。

![用於訓練標籤模型以用於智慧標籤的工作流](assets/smart-tag-model-training-flow.png)

*圖： 培訓工作流程中訓練標籤模型的步驟。*

### 檢視培訓狀態和報告 {#training-status}

若要檢查智慧型標籤服務是否在訓練資產集中的標籤上接受訓練，請從報告主控台檢視訓練工作流程報告。

1. 在介 [!DNL Experience Manager] 面中，前往「工 **[!UICONTROL 具>資產>報表」]**。
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。Then, click **[!UICONTROL Create]** from the toolbar.
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。To view the report, click **[!UICONTROL View]** from the toolbar.
1. 檢閱報表的詳細資訊。 報表會顯示您所訓練之標籤的訓練狀態。The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Tags service is trained for the tag. 黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。如果您在此報表中未看到標籤，請針對這些標籤重新執行培訓工作流程。標籤
1. 若要下載報表，請從清單中選取報表，然後按一下工 **[!UICONTROL 具列]** 中的下載。 報表會以Microsoft Excel試算表的形式下載。

## 標籤資產 {#tag-assets}

在您培訓了「智慧標籤」服務後，可以觸發標籤工作流程，以便自動在不同的類似資產集上套用適當的標籤。 您可以定期或視需要套用標籤工作流程。 標籤工作流程同時套用至資產和資料夾。

### 從工作流程主控台標籤資產 {#tagging-assets-from-the-workflow-console}

1. 在Experience Manager介面中，前往「工具>工 **[!UICONTROL 作流程>模型」]**。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在「執 **[!UICONTROL 行工作流程]** 」對話方塊中，瀏覽至包含資產的裝載資料夾，您要自動套用標籤。
1. 指定工作流程的標題和選用的註解。 按一 **[!UICONTROL 下Run]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   導覽至資產資料夾並檢閱標籤，以確認您的資產是否已正確標籤。 如需詳細資訊，請參 [閱「管理智慧標籤](#manage-smart-tags-and-searches)」。

### 從時間軸標籤資產 {#tagging-assets-from-the-timeline}

1. 從「資產」使用者介面中，選取包含您要套用智慧標籤之資產或特定資產的檔案夾。
1. 從左上角開啟時間 **[!UICONTROL 軸]**。
1. 從左側邊欄底部開啟動作，然後按一下「開 **[!UICONTROL 始工作流程」]**。

   ![start_workflow](assets/start_workflow.png)

1. 選取「 **[!UICONTROL DAM智慧型標籤資產」工作流程]** ，並指定工作流程的標題。
1. 按一 **[!UICONTROL 下開始]**。 工作流程會將您的標籤套用在資產上。 導覽至資產資料夾並檢閱標籤，以確認您的資產是否已正確標籤。 如需詳細資訊，請參 [閱「管理智慧標籤](#manage-smart-tags-and-searches)」。

>[!NOTE]
>
>在後續的標籤週期中，只有修改過的資產會再次使用新訓練過的標籤進行標籤。但是，如果標籤工作流程的最後一個標籤週期與目前標籤週期之間的間隔超過24小時，則甚至會標籤未更改的資產。 對於定期標籤工作流程，未變更的資產會在時間間隔超過6個月時加以標籤。

### 標籤上傳的資產 {#tag-uploaded-assets}

Experience Manager可自動標籤使用者上傳至DAM的資產。 為此，管理員會設定工作流程，以新增可用步驟至智慧標籤資產。 瞭解 [如何為上傳的資產啟用智慧標籤](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)。

## 管理智慧標籤和影像搜尋 {#manage-smart-tags-and-searches}

您可以組織智慧型標籤，移除可能指派給品牌影像的任何不正確標籤，以便只顯示最相關的標籤。

協調智慧型標籤也有助於調整以標籤為基礎的影像搜尋，確保影像出現在搜尋結果中，以找出最相關的標籤。 基本上，它有助於消除不相關影像在搜尋結果中顯示的機率。

您也可以指派較高的排名給標籤，以提高其與影像的相關性。 促銷影像的標籤會增加當根據特定標籤執行搜尋時，在搜尋結果中出現影像的機率。

1. 在Omnisearch方塊中，根據標籤搜尋資產。
1. 檢查搜尋結果，以識別與搜尋無關的影像。
1. 選取影像，然後按一下工具 **[!UICONTROL 列中的「管理標籤]** 」圖示。
1. 從「管 **[!UICONTROL 理標籤]** 」頁面檢查標籤。 如果您不想根據特定標籤來搜尋影像，請選取標籤，然後從工具列按一下刪除圖示。 或者，按一下 `X` 出現在標籤旁邊的符號。
1. 若要指派較高的排名給標籤，請選取標籤，然後從工具列按一下提升圖示。 您促銷的標籤會移至「標籤 **[!UICONTROL 」區]** 域。
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. 導覽至影像的屬性頁面。 請注意，您促銷的標籤已指派高關聯性，因此在搜尋結果中會顯示高度。

### 使用智慧型標籤瞭解AEM搜尋結果 {#understandsearch}

依預設，AEM搜尋會將搜尋詞與子句結 `AND` 合。 使用智慧型標籤不會變更此預設行為。 使用智慧型標籤會新增一 `OR` 個額外的子句，以尋找套用智慧型標籤中的任何搜尋詞。 For example, consider searching for `woman running`. 預設情況下， `woman` 中繼資 `running` 料中只包含或只包含關鍵字的資產不會出現在搜尋結果中。 但是，標籤有或使用智 `woman` 慧標 `running` 記的資產會出現在此類搜尋查詢中。 所以搜索結果是，

* 資產 `woman` 和 `running` 中繼資料中的關鍵字。

* 資產智慧標籤為其中一個關鍵字。

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 的匹配 `woman running` 項。
1. 在智慧型標 `woman running` 簽中的相符項目。
1. 在智慧標 `woman` 記中 `running` 的相符項目。

### 標籤限制 {#limitations}

增強的智慧型標籤是以品牌影像及其標籤的學習模型為基礎。 這些模型在識別標籤時並不總是十分完美。 智慧標籤的目前版本有下列限制：

* 無法辨識影像的細微差異。 例如，修身與普通襯衫。
* 無法根據影像的微小圖樣／部分來識別標籤。 例如，T恤上的標誌。
* 在支援AEM的地區設定中支援標籤。 如需語言清單，請參閱智慧標 [簽版本注意事項](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

若要使用智慧型標籤（一般或增強功能）搜尋資產，請使用資產搜尋（全文搜尋）。 智慧型標籤沒有個別的搜尋述詞。

>[!NOTE]
>
>智慧型標籤在您的標籤上進行訓練，並將它們套用至其他影像的能力，取決於您用於訓練的影像品質。
>為獲得最佳效果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。

>[!MORELIKETHIS]
>
>* [設定Experience Manager以進行智慧標籤](smart-tags-configuration.md)
>* [瞭解智慧型標籤如何協助管理資產](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)

