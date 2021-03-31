---
title: 批次集預設集
description: 了解如何使用 Dynamic Media 中的批次集預設集自動建立影像集和迴轉集。
contentOwner: Rick Brough
feature: 影像預設集，檢視器預設集
topic: 業務從業人員
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '3435'
ht-degree: 1%

---


# 關於批集預設集{#about-bsp}

使用&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;協助您在個別或使用大量擷取將資產檔案上傳至檔案夾時，輕鬆建立和組織影像集或回轉集中的多個資產。 您可以在[!DNL Dynamic Media]中排程的資產匯入工作旁邊執行預設集。 每個預設集都是一組唯一命名的自含指令，這些指令定義如何使用符合預設配方中定義之命名慣例的影像來建構影像集或回轉集。

>[!IMPORTANT]
>
>如果您在[!DNL Dynamic Media Classic]中使用批集預設集，而您要從[!DNL Dynamic Media Classic]移轉至Adobe Experience Manager作為Cloud Service，則必須手動在[!DNL Adobe Experience Manager as a Cloud Service]中重新建立批集預設集定義。

**最佳實務** -使用批次集預設集時，Adobe建議使用下列工作流程：

1. 建立批次集預設集。 請參閱[為影像集或回轉集建立批次集預設集](#creating-bsp)。
1. 建立資產資料夾或使用現有的資產資料夾，並確保它與[!DNL Dynamic Media]同步。 請參閱[建立資料夾](/help/assets/manage-digital-assets.md#creating-folders)。
1. 將批集預設套用至資產檔案夾。 請參閱[關於將批集預設集套用至資料夾](#apply-bsp)。
1. 上傳影像至資產檔案夾。 請參閱[上傳影像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)、[上傳回轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或[將數位資產新增至Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 建立影像集或回轉集。 請參閱[影像集](/help/assets/dynamic-media/image-sets.md)或[回轉集](/help/assets/dynamic-media/spin-sets.md)。
1. 發佈影像集或回轉集。 請參閱[發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 為影像集或回轉集{#creating-bsp}建立批次集預設集

若要建立批次集預設集，請務必熟悉並瞭解規則運算式。

理想情況下，您的公司已針對資產在集合中的分組方式定義命名慣例。
為協助您瞭解使用命名慣例的重要性，請假設您公司的定義命名慣例為`<style>-<color>-<view>`。 此外，集的基本名稱必須始終為`<style>-<color>`，而集的名稱副檔名必須為`-SET`。 如果您上傳名為`0123-RED-01`的影像，則會建立名為`0123-RED-SET`的影像集。 如果您稍後上傳影像`0123-RED-03`和`0123-BLUE-01`，則會將`RED-03`影像新增至第二個位置的集合，因為影像的排序低於`01`。 但是，`BLUE-01`影像會是名為`0123-BLUE-SET`的新集合的一部分。 對於下次資產上傳，您會新增檔案`0123-RED-02`和`0123-BLUE-02`。 每項資產將新增至其各自的資產集。 由於排序順序，`RED-02`影像會在現有`01`和`03`影像之間自動排序。

[!DNL Dynamic Media]中的&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面可讓您建立、編輯或刪除批集預設集，以及將批集預設集套用或從資產檔案夾移除。 您可以使用表單欄位下拉式清單來定義批次集預設集，或使用「原始程式碼」欄位（可讓您輸入規則運算式語法）。****

您可以視需要建立任意數量的批次集預設集，以涵蓋所有需要的資產收錄工作。

**關於資產命名慣例**

**[!UICONTROL 批集預設集]**&#x200B;頁面上的&#x200B;**[!UICONTROL 資產命名約定]**&#x200B;區域包含兩個元素，可用來定義批集預設集：**[!UICONTROL Match]**&#x200B;和&#x200B;**[!UICONTROL 基本名稱]**。 這些元素可讓您定義命名慣例，並識別用來命名其所包含之集之約定的部分。<!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的個別命名慣例通常會從這兩個元素中的每一行使用一或多行定義。 您可以使用任意多行來定義獨特元素，並將它們分組為不同的元素，例如主影像、顏色元素、替代檢視元素和色票元素。

例如，常值符合規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

**關於序列順序**

您可以選擇定義在[!DNL Dynamic Media]中對影像集或旋轉集分組後顯示影像的順序。 依預設，資產會以英數字元排序。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您指定規則以特定方式強制排序資產（如有需要）。 例如，假設您的第一個資產一律命名為`_main`，而且您希望它後面跟著`_alt1`、`_alt2`、`_alt3`等。 在這種情況下，您可以使用下列語法建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然可以強制排序序列，但最好盡可能依賴字母數字編號來排序序列。 此外，您還可使用[!DNL Dynamic Media]中的影像集或回轉集編輯器工具，輕鬆重新排列資產順序，或使用拖放操作新增和刪除資產集中的新資產。

完成建立批集預設集後，可將其應用於已建立的一個或多個資料夾。 請參閱[關於將批集預設集套用至資料夾](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要為影像集或回轉集建立批集預設集：**

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次設定預設集]**」。

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在右上角的&#x200B;**[!UICONTROL 「批次集預設集」頁面上，點選**[!UICONTROL 「建立&#x200B;]**」。]**
1. 在&#x200B;**[!UICONTROL 建立批集預設集]**&#x200B;對話框的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;文本欄位中，輸入描述性名稱。 如果您稍後決定變更預設集名稱，則無法編輯它。

1. 在&#x200B;**[!UICONTROL 預設類型]**&#x200B;下拉式清單中，選擇&#x200B;**[!UICONTROL ImageSet]**&#x200B;或&#x200B;**[!UICONTROL SpinSet]**。 請務必選擇正確的預設集類型；以後無法編輯。
1. 點選&#x200B;**[!UICONTROL Create]**。
1. 在&#x200B;**[!UICONTROL 編輯批集預設]**&#x200B;頁的右側，在&#x200B;**[!UICONTROL 預設詳細資料]**&#x200B;和&#x200B;**[!UICONTROL 設定命名約定]**標題下設定所需的可編輯選項。
如要進一步瞭解可供您使用的可編輯選項，請參閱[預設集詳細資訊、設定命名慣例和規則結果- RegX選項](#features-options-bsp)。

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一或多個規則運算式群組。

   * 在&#x200B;**[!UICONTROL 編輯批集預設集]**&#x200B;頁的左側，在&#x200B;**[!UICONTROL Match]**、**[!UICONTROL 基本名稱]**&#x200B;或&#x200B;**[!UICONTROL 順序]**&#x200B;下，點選&#x200B;**[!UICONTROL 新增群組]**。
   * **[!UICONTROL Match]**&#x200B;欄位為必填欄位。 **[!UICONTROL 只有當「]** 匹配」欄位尚未使 **** 用括弧群組來指定基本名稱時，「基本名稱」才為必要名稱。**[!UICONTROL 序列]** 訂購是可選的。
   * 使用群組表單中的下拉式清單和文字方塊，指定您要用來定義影像集或回轉集資產成員之命名准則的運算式群組。
      * 當您選取並指定群組的運算式時，請注意實際的規則運算式語法會反映在頁面右下方的&#x200B;**[!UICONTROL 規則結果- RegX]**&#x200B;標題下（點選表單區域以外的任何位置，以檢視在右下方更新的規則運算式字串）。 這些規則運算式字串代表您要在搜尋[!DNL Dynamic Media]資產以建立影像集或回轉集時比對的模式。
      * 若要移除已新增的群組，請點選&#x200B;**[!UICONTROL X]**。
   * 當您新增兩個或兩個以上的群組時，在&#x200B;**[!UICONTROL And]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL And]**，將新新增的群組與您新增的任何先前運算式群組結合。 或者，選擇&#x200B;**[!UICONTROL Or]**&#x200B;以在上一個表達式組和您建立的新組之間添加更改。 **[!UICONTROL Or]**&#x200B;運算元是使用規則運算式語法本身中的垂直行字元`|`來定義。

1. 執行下列任一項作業：

   * 若要新增另一個新群組，請在&#x200B;**[!UICONTROL Match]**、**[!UICONTROL Base Name]**&#x200B;或&#x200B;**[!UICONTROL Sequencing Order]**&#x200B;下，點選&#x200B;**[!UICONTROL Add Group]**。 建立另一個規則運算式群組，就像您在上一步驟中所做的一樣。
   * 查看&#x200B;**[!UICONTROL 規則結果- RegX]**&#x200B;區域中的規則運算式語法。 如果您必須變更語法，請在頁面左側的個別群組中進行編輯。
   * 如果您已完成運算式群組的建立，請繼續下一個步驟。

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL Save]**。

您現在可以讀取，將批次集預設套用至一或多個資產檔案夾、上傳資產至檔案夾，然後建立影像集或回轉集。 請參閱[關於將批集預設集套用至資料夾](#apply-bsp)。

### 預設詳細資料、設定命名慣例和規則結果- RegX選項{#features-options-bsp}

在建立或編輯批集預設集時，這些選項可在&#x200B;**[!UICONTROL 編輯批集預設集]**&#x200B;頁上使用。

請參閱[為影像集或回轉集](#creating-bsp)或[建立批次集預設集](#edit-bsp)。

| **[!UICONTROL 預設集詳細資訊]** | 說明 |
| --- | --- |
| 預設集名稱 | 唯讀. 首次建立批集時指定的名稱。 如果必須更名預設，則可以複製現有批集預設並指定新名稱。 請參閱[複製現有批集預設集](#copy-bsp)。 |
| 類型 | 唯讀. 首次建立批集時指定了類型。 複製現有批集預設集不允許您更改其[!UICONTROL Type];您必須改為建立預設集。 |
| 包括衍生資產 | 選填。要使[!DNL Dynamic Media]的IPS（映像生產系統）包含已生成或「派生」的映像以及回轉集或映像集，請選擇&#x200B;**[!UICONTROL 是]**（預設）。 衍生資產是使用者未直接上傳的影像。 而是由IPS在上傳主資產時產生的資產。 例如，IPS在[!DNL Dynamic Media]中上傳PDF時，從PDF的頁面產生的影像資產，會被視為衍生資產。 |
| 目的地資料夾 | 選填。如果您定義大量的影像集或回轉集，Adobe建議您將這些集與包含資產本身的檔案夾分開。 因此，請考慮建立「影像集」或「回轉集」檔案夾，並將應用程式重新導向至此處放置產生的批次集。<br>在這種情況下，請指定「Experience Manager資產」檔案夾結構(`/content/dam`)中哪個檔案夾具有作用中的批次集預設集。請確定該資料夾已啟用[!DNL Dynamic Media]同步，以允許其作為目標資料夾。 請參閱[在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)的資料夾層級設定選擇性發佈。<br>如果您透過資料夾的「屬性」套用預設集，多個資料夾可以指派給指定的批次集預 **[!UICONTROL 設集]**。請參閱[從資產資料夾的「屬性」頁面](#apply-bsp-to-folders-via-properties)套用批次集預設集。<br>如果您未指定檔案夾，批次集預設會建立在與資產上傳檔案夾相同的檔案夾中。 |
| **[!UICONTROL 設定命名慣例]** |  |
| 前置詞<br>或<br>尾碼 | 選填。在各自的欄位中輸入前置詞、尾碼或兩者。<br>前置詞和尾碼欄位允許您使用特定內容集的備用自定義檔案命名慣例建立盡可能多的批集預設。在公司定義的預設命名方案有例外的情況下，此方法特別有用。<br>首碼或尾碼將添加到您在「資 **[!UICONTROL 產命]** 名約定」區域中定 **[!UICONTROL 義的「基本]** 名稱」。借由新增前置詞或後置詞，您可以確保影像集或回轉集會以獨立方式與其他資產建立。 它也可協助其他人識別檔案類型。 例如，要確定使用的顏色模式，可以添加前置詞或尾碼`rgb`或`cmyk`。<br>雖然使用批處理集預設功能不需要指定集命名約定，但最佳做法建議您使用集命名約定。此實務可讓您定義想要在一組中分組的命名慣例元素，以簡化批次集的建立。 |
| **[!UICONTROL 規則結果 - RegX]** |  |
| 資產命名慣例——符合 | 唯讀. 根據您選擇的「符合」表單選項或您輸入的原始程式碼，顯示規則運算式語法。 |
| 資產命名慣例——基本名稱 | 唯讀. 根據您選擇的「基本名稱」表單選項或您輸入的原始程式碼顯示規則運算式語法。 |
| 序列順序——匹配 | 唯讀. 根據您選擇的表單選項或您輸入的原始程式碼，顯示規則運算式語法。 |

## 關於將批集預設集應用到資料夾{#apply-bsp}

將批集預設集指派給一或多個檔案夾時，任何子檔案夾都會自動從其父檔案夾繼承預設集。

您可以將多個批次集預設集套用至資料夾。

在用戶介面中，在&#x200B;**[!UICONTROL Card]**&#x200B;視圖中，將指定為其分配了批預設的資料夾，其名稱顯示在資料夾中。

若要將批集預設集套用至檔案夾，請使用下列兩種方法之一：

* [從「批集預設集」頁面將批集預設集套用至資產檔案夾](#apply-bsp-to-folders-via-bsp-page) -此方法提供您最大的彈性。您可以將單一預設集或多個預設集套用至單一檔案夾或多個檔案夾。
* [從資產資料夾的「屬性」頁面應用批集預設集](#apply-bsp-to-folders-via-properties) -此方法可讓您將一個或多個批集預設集套用到單個資料夾。

最佳實務是，請確定資產資料夾已同步[!DNL Dynamic Media]，然後套用您想要的預設集。

如果您遇到下列兩種情況之一，請重新處理資料夾中的資產：

* 您想要在已上傳資產的現有資產資料夾上執行批次集預設集。
* 您稍後會編輯先前套用至資產資料夾的現有批次集預設集。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 從「批集預設集」頁{#apply-bsp-to-folders-via-bsp-page}將批集預設集套用至資產檔案夾

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次設定預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要應用於資料夾的每個批集預設集的複選框。
1. 在工具列中，點選「**[!UICONTROL 將批次預設套用至資料夾]**」。
1. 在&#x200B;**[!UICONTROL 「選擇資料夾]**」頁上，選中要應用批集預設的每個資料夾的複選框。
1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁的右上角，按一下&#x200B;**[!UICONTROL 應用]**。

### 從資產資料夾的「屬性」頁面{#apply-bsp-to-folders-via-properties}套用批次集預設集

1. 點選Adobe Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 導覽至您要套用一或多個批次集預設集的檔案夾。
1. 在頁面上，選擇&#x200B;**[!UICONTROL Name]**&#x200B;列左側的資料夾複選框。
1. 在工具列中，點選&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，點選「**[!UICONTROL Dynamic Media處理]**」標籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;下，從&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉式清單方塊中，選取您要套用的批集預設集名稱。 上述螢幕擷取顯示套用至資料夾的兩個選取批次集預設集。

   如果&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉式清單方塊中沒有批次集預設集名稱，表示您尚未建立任何批次集預設集。 請參閱[為影像集或回轉集建立批次集預設集](#creating-bsp)。

   若要移除套用的批次集預設集，請點選預設集類型右側的&#x200B;**[!UICONTROL X]**。

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL 儲存並關閉]**。

## 編輯批集預設集{#edit-bsp}

您可以編輯已建立的現有批集預設集。 您可以變更為資產命名慣例或序列順序所建立的任何運算式群組。 如有需要，您也可以更新目標資料夾並設定命名慣例。

但是，您無法變更預設集的名稱或預設集類型（影像集或回轉集）。 如果需要變更預設集的名稱，您只需複製現有的預設集並指定新名稱。 請參閱[複製批集預設集](#copy-bsp)。

如果您編輯先前套用至檔案夾的批次集預設集，新編輯的預設集只會套用至上傳至檔案夾的新資產。

如果您想要將新編輯的預設重新套用至資料夾中的現有資產，您必須重新處理資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->如此一來，現有資產現在可以成為影像集或回轉集的一部分並加以新增。此外，根據先前使用的批次集預設集，已包含在影像集或回轉集中的現有資產不會移除（假設這些資產不再符合新編輯的預設集）並依現狀顯示。

**要編輯批集預設集，請執行以下操作：**

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集」。]**
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄左側，勾選您要變更的批集預設集。
1. 在工具列中，點選「編輯批集預設」。]****[!UICONTROL 
1. 視需要編輯預設集。
1. 在「**[!UICONTROL 批集預設集]**」頁面的右上角，點選「儲存」。]****[!UICONTROL 

## 複製現有批集預設集{#copy-bsp}

您可以複製現有的批集預設集，以避免手動重新建立複雜的預設集，或只要重新命名預設集即可。 但是，您無法變更使用的預設類型（影像集或回轉集）。

如果您複製由資產檔案夾參考的現有預設集，這些檔案夾將不受影響。

**要複製現有批集預設集，請執行以下操作：**

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集」。]**
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要複製的批集預設集複選框。
1. 在工具列中，點選&#x200B;**[!UICONTROL Copy]**。
1. 在&#x200B;**[!UICONTROL 複製批集預設集]**&#x200B;對話框的&#x200B;**[!UICONTROL 標題]**&#x200B;文本框中，為預設集鍵入新名稱。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 點選「 **[!UICONTROL 複製]**」。

## 關於從資料夾{#remove-bsp-from-folder}中刪除批集預設集

從檔案夾移除批次集預設集時，您上傳至這些檔案夾的任何新資產都不會套用批次集預設集。 資料夾中已新增至影像集或以套用至資料夾的批次集預設為基礎的點陣集的現有資產，會繼續顯示為「原樣」。

如果要改為從資料夾中刪除&#x200B;**&#x200B;預設集，請參閱[刪除批集預設集](#delete-bsp)。

有兩種方法可用來從檔案夾移除批次集預設集。

* [通過「批集預設」頁從資料夾中刪除批集預設](#remove-bsp-from-folders-via-bsp-page) -此方法提供了最大的靈活性。您可以從單一檔案夾或多個檔案夾移除單一預設集或多個預設集。
* [從資料夾的「屬性」頁中刪除批集預設集](#remove-bsp-from-folders-via-properties) -此方法僅允許從單個資料夾中刪除一個或多個批集預設集。

### 通過「批集預設集」頁{#remove-bsp-from-folders-via-bsp-page}從資料夾中刪除批集預設集

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次設定預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄左側，選中要從一個或多個資料夾中刪除的一個或多個批集預設集的複選框。
1. 在工具列中，點選&#x200B;**[!UICONTROL 從資料夾中移除批次預設集]**。

1. 在&#x200B;**[!UICONTROL 「選擇資料夾]**」頁上，選擇要刪除批集預設集的一個或多個資料夾。
1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁的右上角，按一下&#x200B;**[!UICONTROL 刪除]**。

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在&#x200B;**[!UICONTROL 移除描述檔]**&#x200B;對話方塊中，點選&#x200B;**[!UICONTROL 移除]**。

### 從資料夾的「屬性」頁面{#remove-bsp-from-folders-via-properties}刪除批集預設集

1. 點選Adobe Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 導覽至您要移除一或多個批次集預設集的檔案夾。
1. 在頁面上，選擇&#x200B;**[!UICONTROL Name]**&#x200B;列左側的資料夾複選框。
1. 在工具列中，點選&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，點選「Dynamic Media處理」**[!UICONTROL 。]**

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在&#x200B;**[!UICONTROL 「批次設定預設集」下，點選預設集類型右側的**[!UICONTROL  X ]**。]**

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL 儲存並關閉]**。

## 刪除批集預設集{#delete-bsp}

您可以刪除批集預設集，以便從[!DNL Dynamic Media]中永久移除。 也就是說，它們不再顯示在[!UICONTROL 批集預設集]頁面上，也不再顯示在資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上&#x200B;**[!UICONTROL 「批集預設集」下拉式清單中。]******&#x200B;因此，預設集不會套用至資料夾重新處理上的現有資產，或是在資料夾中上傳新資產時。

如果您刪除先前已套用至一或多個檔案夾的預設集，從這些檔案夾中的資產建立的任何影像集或回轉集會繼續「原樣」顯示。

如果要從資料夾中移去&#x200B;*預設集，請參閱[從資料夾中移去批集預設集。*](#remove-bsp-from-folder)

**要刪除批集預設集，請執行以下操作：**

1. 點選Adobe Experience Manager標誌並導覽至「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 批次設定預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄左側，選中要刪除的一個或多個批集預設集的複選框。
1. 在工具列中，點選「刪除批集預設集」**[!UICONTROL 。]**

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在&#x200B;**[!UICONTROL 刪除批集預設集]**&#x200B;對話方塊中，點選&#x200B;**[!UICONTROL 刪除]**。

   如果要刪除的預設集被資產資料夾參考，請改為點選「強制刪除」。****

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [影像集](/help/assets/dynamic-media/image-sets.md)
>* [迴轉集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media的資料夾層級設定選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) -請參閱主題中的「同步模式」，以進一步瞭解將單一資料夾同步至的相關資訊 [!DNL Dynamic Media]。
>* [在Cloud Services中建立Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) -請參閱主題中的「Dynamic Media同步模式」，瞭解有關將所有資料夾同步到的詳細資訊 [!DNL Dynamic Media]。