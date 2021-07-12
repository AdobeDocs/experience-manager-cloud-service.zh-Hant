---
title: 批次集預設集
description: 了解如何使用 Dynamic Media 中的批次集預設集自動建立影像集和迴轉集。
contentOwner: Rick Brough
feature: 影像預設集，檢視器預設集
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3446'
ht-degree: 1%

---

# 關於批集預設集 {#about-bsp}

當您將資產檔案個別上傳至資料夾或使用大量內嵌時，請使用&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;在影像集或回轉集中建立和組織多個資產。 您可以讓預設集與您在[!DNL Dynamic Media]中排程的資產匯入工作一併執行。 每個預設集都是一組唯一命名的自包含指令，定義如何使用符合預設方式中已定義命名慣例的影像來建構影像集或回轉集。

>[!IMPORTANT]
>
>您在[!DNL Dynamic Media Classic]中使用批次集預設集，並從[!DNL Dynamic Media Classic]移轉至Adobe Experience Manager作為Cloud Service嗎？ 如果是，您必須手動在[!DNL Adobe Experience Manager as a Cloud Service]中重新建立批集預設集定義。

**最佳作法**  — 使用批次集預設集時，Adobe建議使用下列工作流程：

1. 建立批集預設集。 請參閱[為影像集或回轉集建立批次集預設集](#creating-bsp)。
1. 建立資產資料夾或使用現有資產資料夾，並確認其已同步至[!DNL Dynamic Media]。 請參閱[建立資料夾](/help/assets/manage-digital-assets.md#creating-folders)。
1. 將批次集預設集套用至資產資料夾。 請參閱[關於將批集預設集應用於資料夾](#apply-bsp)。
1. 上傳影像至資產資料夾。 請參閱[上傳影像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)、[上傳回轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或[新增數位資產至Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 影像集或回轉集會在所需資料夾中自動產生。
1. 發佈影像集或回轉集。 請參閱[發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 為影像集或回轉集建立批集預設集 {#creating-bsp}

若要建立批集預設集，您應熟悉並了解規則運算式。

理想情況下，您的公司已定義資產在集合中分組方式的命名慣例。
為協助您了解使用命名慣例的重要性，假設貴公司定義的命名慣例為`<style>-<color>-<view>`。 而且，集的基名必須始終為`<style>-<color>`，而集的名副檔名必須為`-SET`。 如果上傳名為`0123-RED-01`的影像，則會建立名為`0123-RED-SET`的集合。 如果您稍後上傳影像`0123-RED-03`和`0123-BLUE-01`，則會將`RED-03`影像新增至第二個位置中的集合，因為其排序順序低於`01`。 不過，`BLUE-01`影像將是名為`0123-BLUE-SET`的新集的一部分。 對於下次資產上傳，您會新增檔案`0123-RED-02`和`0123-BLUE-02`。 每項資產將加入其各自的資產組。 由於排序順序，`RED-02`影像將在現有`01`和`03`影像之間自動排序。

**[!UICONTROL [!DNL Dynamic Media]中的「批集預設集」]**&#x200B;頁允許您建立、編輯或刪除批集預設集，以及在資產資料夾中應用或移除批集預設集。 您可以使用表單欄位下拉式清單來定義批次集預設集，或使用&#x200B;**[!UICONTROL 原始程式碼]**&#x200B;欄位，該欄位可讓您輸入規則運算式語法。

您可以建立許多批次集預設集，以涵蓋所有您需要的資產內嵌作業。

### 關於資產命名慣例

**[!UICONTROL 批集預設集]**&#x200B;頁上的&#x200B;**[!UICONTROL 資產命名約定]**&#x200B;區域有兩個元素，可用來定義批集預設集：**[!UICONTROL 符合]**&#x200B;和&#x200B;**[!UICONTROL 基本名稱]**。 這些元素可讓您定義命名慣例，並識別用來為其所包含集命名的慣例部分。<!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的個別命名慣例通常會從這兩個元素中的每一行使用一或多行定義。 您可以針對唯一定義使用任意數行，並將它們分組為不同的元素，例如主影像、顏色元素、替代視圖元素和色票元素。

例如，常值比對規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

### 關於序列順序

您可以選擇定義在[!DNL Dynamic Media]中對影像集或回轉集進行分組後，影像的顯示順序。 依預設，您的資產依字母順序排列。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您需要指定規則，以特定方式強制排序資產。 例如，假設您的第一個資產一律命名為`_main`，且您想要其後接`_alt1`、`_alt2`、`_alt3`等。 在這種情況下，您可以使用下列語法來建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然可以強制排序序列，但最好盡可能依靠字母數字編號來排序序列。 此外，您可以使用[!DNL Dynamic Media]中的影像集或回轉集編輯器工具來重新排列資產的順序，或使用拖放操作來在集合中新增和刪除新資產。

完成建立批集預設集後，可將其應用於已建立的一個或多個資料夾。 請參閱[關於將批集預設集應用於資料夾](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要為影像集或回轉集建立批集預設集：**

1. 選取Experience Manager標誌，然後前往「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**」。

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的右上角附近，選擇&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立批集預設集]**&#x200B;對話框的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;文本欄位中，輸入描述性名稱。 如果您稍後決定變更預設集名稱，該預設集名稱將無法編輯。

1. 在&#x200B;**[!UICONTROL 預設類型]**&#x200B;下拉清單中，選擇&#x200B;**[!UICONTROL ImageSet]**&#x200B;或&#x200B;**[!UICONTROL SpinSet]**。 請務必選擇正確的預設集類型；以後無法編輯。
1. 選擇 **[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 編輯批集預設集]**&#x200B;頁的右側，在&#x200B;**[!UICONTROL 預設詳細資訊]**&#x200B;和&#x200B;**[!UICONTROL 設定命名約定]**標題下設定所需的可編輯選項。
若要進一步了解您可用的可編輯選項，請參閱[預設集詳細資訊、設定命名慣例和規則結果 — RegX選項](#features-options-bsp)。

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一或多個規則運算式群組。

   * 在&#x200B;**[!UICONTROL 編輯批集預設集]**&#x200B;頁左側的&#x200B;**[!UICONTROL Match]**、**[!UICONTROL 基本名稱]**&#x200B;或&#x200B;**[!UICONTROL 序列排序]**&#x200B;下，選擇&#x200B;**[!UICONTROL 添加組]**。
   * 需要&#x200B;**[!UICONTROL Match]**&#x200B;欄位。 **[!UICONTROL 只有]** 在「匹配」欄位尚未 **** 使用括弧分組來指定基本名稱時，「基本名稱」才是必填項。**[!UICONTROL 序列]** 排序是可選的。
   * 使用組窗體中的下拉清單和文本框，指定要用來定義影像集或回轉集資產成員命名標準的表達式組。
      * 當您選擇並指定群組的運算式時，請注意實際規則運算式語法反映在頁面右下角的&#x200B;**[!UICONTROL Rule Results - RegX]**&#x200B;標題下方。 若要查看右下角更新的規則運算式字串，請選取表單區域以外的任何位置。 這些規則運算式字串代表您在搜尋[!DNL Dynamic Media]資產以建立影像集或回轉集時所要比對的模式。
      * 如果已添加組並要將其刪除，請選擇&#x200B;**[!UICONTROL X]**。
   * 新增兩個或多個群組時，在&#x200B;**[!UICONTROL And]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL And]** ，將新新增的群組與您新增的任何先前運算式群組連結。 或者，選擇&#x200B;**[!UICONTROL 或]**&#x200B;以添加前一個表達式組和新建組之間的交互。 **[!UICONTROL Or]**&#x200B;操作數由規則運算式語法本身中使用垂直行字元`|`來定義。

1. 執行下列任一操作：

   * 若要添加另一個新組，請在&#x200B;**[!UICONTROL Match]**、**[!UICONTROL Base Name]**&#x200B;或&#x200B;**[!UICONTROL Secunding Order]**&#x200B;下，選擇&#x200B;**[!UICONTROL Add Group]**。 建立另一個規則運算式群組，如上一步所述。
   * 查看&#x200B;**[!UICONTROL 規則結果 — RegX]**&#x200B;區域中的規則運算式語法。 如果您必須變更語法，請在頁面左側的個別群組中進行編輯。
   * 如果已完成運算式群組的建立，請繼續下一個步驟。

1. 在頁面的右上角，選擇&#x200B;**[!UICONTROL Save]**。

您現在可以將批次集預設集套用至資產資料夾。 接著，您上傳資產至該資料夾。 此工作流程會自動產生影像集或回轉集。 請參閱[關於將批集預設集應用於資產資料夾](#apply-bsp)。

### 預設集詳細資訊、設定命名慣例和規則結果 — RegX選項 {#features-options-bsp}

建立或編輯批集預設集時，這些選項可在&#x200B;**[!UICONTROL 編輯批集預設集]**&#x200B;頁上使用。

請參閱[為影像集或回轉集](#creating-bsp)或[編輯批次集預設集](#edit-bsp)建立批次集預設集。

| **[!UICONTROL 預設集詳細資訊]** | 說明 |
| --- | --- |
| 預設集名稱 | 唯讀. 首次建立批集時指定的名稱。 如果必須更名預設集，則可以複製現有批集預設集並指定新名稱。 請參閱[複製現有批集預設集](#copy-bsp)。 |
| 類型 | 唯讀. 首次建立批集時指定了類型。 複製現有批集預設集不允許您更改其[!UICONTROL 類型];您必須改為建立預設集。 |
| 包括衍生資產 | 選填。要使[!DNL Dynamic Media]的IPS（映像生產系統）包含已生成或「派生」的映像，請選擇&#x200B;**[!UICONTROL 是]**（預設）。 衍生資產是使用者未直接上傳的影像。 相反地，資產是在上傳主資產時由IPS產生的。 例如，在[!DNL Dynamic Media]中上傳PDF時，IPS從PDF中的頁面產生的影像資產被視為衍生資產。 |
| 目的地資料夾 | 選填。如果您定義大量影像集或回轉集，Adobe建議您將這些集與包含資產本身的資料夾分開。 因此，請考慮建立「影像集」或「回轉集」資料夾，並將應用程式重新導向，將批集生成的集放置在此處。<br>在此情況下，請指定「Experience Manager資產」資料夾結構(`/content/dam`)中哪個資料夾已將批次集預設設為作用中。請確保已為[!DNL Dynamic Media]同步啟用該資料夾，以允許它作為目標資料夾。 請參閱[在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)的資料夾層級設定選擇性發佈。<br>如果通過資料夾的「屬性」應用預設集，則可以為多個資料夾分配指定的批集預 **[!UICONTROL 設集]**。請參閱從資產資料夾的「屬性」頁面[套用批次集預設集。](#apply-bsp-to-folders-via-properties)<br>如果您未指定資料夾，則會在與您上傳至的資產資料夾相同的資料夾中建立批次集預設產生的影像集或回轉集。 |
| **[!UICONTROL 設定命名慣例]** |  |
| 前置詞<br>或<br>尾碼 | 選填。在相應欄位中輸入前置詞、尾碼或兩者。<br>前置詞和尾碼欄位可讓您針對特定內容集使用替代的自訂檔案命名慣例來建立許多批次集預設集。在公司定義的預設命名方案有例外的情況下，此方法特別實用。<br>前置詞或尾碼會新增至您在「 **[!UICONTROL 資]** 產命名慣例」區域中定義的「 **[!UICONTROL 基本]** 名稱」。借由新增首碼或尾碼，您可確保您的影像集或回轉集完全獨立於其他資產建立。 也可進一步協助其他人識別檔案類型。 例如，要確定所使用的顏色模式，可以添加為前置詞或尾碼`rgb`或`cmyk`。<br>雖然使用批集預設集功能不需要指定集命名慣例，但最佳實務建議您使用集命名慣例。此慣例可讓您定義想要分組到一組中的命名慣例的多個元素，以協助簡化批次集建立。 |
| **[!UICONTROL 規則結果 - RegX]** |  |
| 資產命名慣例 — 符合 | 唯讀. 根據您選擇的「符合」表單選項或您輸入的原始程式碼，顯示規則運算式語法。 |
| 資產命名慣例 — 基本名稱 | 唯讀. 根據您選擇的「基本名稱」表單選項或您輸入的原始代碼顯示規則運算式語法。 |
| 序列排序 — 匹配 | 唯讀. 根據您選擇的表單選項或您輸入的原始程式碼顯示規則運算式語法。 |

## 關於將批次集預設集套用至資產資料夾 {#apply-bsp}

將批集預設集分配給一個或多個資產資料夾時，任何子資料夾都會自動從其父資料夾繼承預設集。

您可以將多個批次集預設集套用至資產資料夾。

在&#x200B;**[!UICONTROL Card]**&#x200B;視圖中，在用戶介面中指示為其分配了批處理預設的資料夾，該資料夾的名稱出現在資料夾中。

若要將批次集預設集套用至資產資料夾，請使用下列兩種方法之一：

* [從「批集預設集」頁將批集預設集應用於資產資料夾](#apply-bsp-to-folders-via-bsp-page)  — 此方法為您提供了最大的靈活性。您可以將單一預設集或多個預設集套用至單一資料夾或多個資料夾。
* [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties)  — 此方法可讓您將一或多個批次集預設集套用至單一資料夾。

最佳實務是，請確定已同步資產資料夾[!DNL Dynamic Media]，然後套用您想要的預設集。

如果您遇到下列兩種情況之一，請重新處理資料夾中的資產：

* 您想要在現有資產資料夾上執行已上傳資產的批次集預設集。
* 您之後可以編輯先前已套用至資產資料夾的現有批次集預設集。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 從「批集預設集」頁將批集預設集應用於資產資料夾 {#apply-bsp-to-folders-via-bsp-page}

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要應用於資料夾的每個批集預設集的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 將批預設集應用於資料夾]**。
1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁上，選中要應用批集預設集的每個資料夾的複選框。
1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁的右上角，選擇&#x200B;**[!UICONTROL 應用]**。

### 從資產資料夾的「屬性」頁面套用批次集預設集 {#apply-bsp-to-folders-via-properties}

1. 選取Experience Manager標誌，然後前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 導覽至您要套用一或多個批次集預設集的資料夾。
1. 在頁面上，在&#x200B;**[!UICONTROL 名稱]**&#x200B;列的左側，選擇資料夾的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，選取&#x200B;**[!UICONTROL Dynamic Media處理]**&#x200B;標籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;下，從&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉清單框中，選擇要應用的批集預設集的名稱。 上方的螢幕擷圖顯示套用至資產資料夾的兩個選取批次集預設集。

   如果&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉清單框中不存在批集預設集名稱，則表示您尚未建立任何批集預設集。 請參閱[為影像集或回轉集建立批次集預設集](#creating-bsp)。

   要刪除應用的批集預設集，請選擇預設類型右側的&#x200B;**[!UICONTROL X]**。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。

## 編輯批集預設集 {#edit-bsp}

您可以編輯已建立的現有批集預設集。 您可以變更為資產命名慣例或順序建立的任何運算式群組。 如有需要，您也可以更新目標資料夾並設定命名慣例。

不過，您無法變更預設集的名稱或預設集類型（「影像集」或「回轉集」）。 如果有必要變更預設集的名稱，請複製現有的預設集並指定新名稱。 請參閱[複製批集預設集](#copy-bsp)。

如果您編輯先前已套用至資料夾的批次集預設集，新編輯的批次集預設集只會套用至上傳至該資料夾的新資產。

如果您想要將新編輯的預設集重新套用至資料夾中的現有資產，您必須重新處理資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->如此一來，現有資產現在就可以成為影像集或回轉集的一部分，並可以新增。此外，影像集或回轉集中已包含的現有資產（根據先前使用的批次集預設集）不會遭到移除，且會如實顯示。 此案例假設他們不再根據新編輯的預設集符合資格。

**要編輯批集預設集，請執行以下操作：**

1. 選取Experience Manager標誌，然後前往「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，檢查要更改的批集預設集。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 編輯批集預設集]**。
1. 視需要編輯預設集。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的右上角，選擇&#x200B;**[!UICONTROL 保存]**。

## 複製現有批集預設集 {#copy-bsp}

您可以複製現有的批集預設集，以避免手動重新建立複雜的預設集，或者只是想更名預設集。 但您無法變更所使用的預設集類型（影像集或回轉集）。

如果您複製由資產資料夾參照的現有預設集，這些資料夾不受影響。

**複製現有批集預設集：**

1. 選取Experience Manager標誌，然後前往「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要複製的批集預設集的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL Copy]**。
1. 在&#x200B;**[!UICONTROL 複製批集預設集]**&#x200B;對話框的&#x200B;**[!UICONTROL 標題]**&#x200B;文本框中，為預設集鍵入新名稱。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 選擇&#x200B;**[!UICONTROL 複製]**。

## 關於從資料夾中刪除批集預設集 {#remove-bsp-from-folder}

當您從資料夾中移除批次集預設集時，上傳至這些資料夾的任何新資產都不會套用批次集預設集。 資料夾中已新增至影像集的現有資產，或根據套用至資料夾的批次集預設集來指定資產，繼續按原樣顯示。

如果要從資料夾中刪除&#x200B;**&#x200B;預設集，請參閱[刪除批集預設集](#delete-bsp)。

有兩種方法可用來從資料夾中移除批次集預設集。

* [通過「批集預設集」頁從資料夾中刪除批集預設集](#remove-bsp-from-folders-via-bsp-page)  — 此方法為您提供了最大的靈活性。您可以從單一資料夾或多個資料夾中移除單一預設集或多個預設集。
* [從資料夾的「屬性」頁中刪除批集預設集](#remove-bsp-from-folders-via-properties)  — 此方法僅允許從單個資料夾中刪除一個或多個批集預設集。

### 通過「批集預設集」頁從資料夾中刪除批集預設集 {#remove-bsp-from-folders-via-bsp-page}

1. 選取Experience Manager標誌，然後前往「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**」。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要從一個或多個資料夾中刪除的一個或多個批集預設集的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 從資料夾中刪除批預設集]**。

1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁上，選擇要刪除批集預設集的一個或多個資料夾。
1. 在&#x200B;**[!UICONTROL 選擇資料夾]**&#x200B;頁的右上角，選擇&#x200B;**[!UICONTROL 刪除]**。

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在&#x200B;**[!UICONTROL 移除設定檔]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 移除]**。

### 從資料夾的「屬性」頁中刪除批集預設集 {#remove-bsp-from-folders-via-properties}

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 導覽至您要移除一或多個批次集預設集的資料夾。
1. 在頁面上，在&#x200B;**[!UICONTROL 名稱]**&#x200B;列的左側，選擇資料夾的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，選擇&#x200B;**[!UICONTROL Dynamic Media處理]**。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;下，選擇預設類型右側的&#x200B;**[!UICONTROL X]**。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。

## 刪除批集預設集 {#delete-bsp}

您可以刪除批集預設集，以便從[!DNL Dynamic Media]中永久刪除它們。 也就是說，它們不再顯示在[!UICONTROL 批集預設集]頁面上，也不再顯示在資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上&#x200B;**[!UICONTROL Dynamic Media處理]**&#x200B;標籤的&#x200B;**[!UICONTROL 批集預設集]**&#x200B;下拉清單中。 因此，重新處理資料夾或在資料夾中上傳新資產時，預設集不會套用至現有資產。

如果您刪除先前已套用至一或多個資料夾的預設集，從這些資料夾中的資產建立的任何影像集或回轉集會繼續依現狀顯示。

如果要從資料夾中刪除&#x200B;*預設集，請參閱[從資料夾中刪除批集預設集](#remove-bsp-from-folder)。*

**要刪除批集預設集：**

1. 選取Experience Manager標誌，並導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**。
1. 在&#x200B;**[!UICONTROL 批集預設集]**&#x200B;頁的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;列左側，選中要刪除的一個或多個批集預設集的複選框。
1. 在工具欄中，選擇&#x200B;**[!UICONTROL 刪除批集預設集]**。

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在&#x200B;**[!UICONTROL 刪除批集預設集]**&#x200B;對話框中，選擇&#x200B;**[!UICONTROL 刪除]**。

   如果您要刪除的預設集被資產資料夾參照，請改為選取&#x200B;**[!UICONTROL 強制刪除]**。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [影像集](/help/assets/dynamic-media/image-sets.md)
* [迴轉集](/help/assets/dynamic-media/spin-sets.md)
* [在Dynamic Media中在資料夾層級設定選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果您想要進一步了解如何將單一資料夾同步至的相關資訊，請參閱主題中的「同步模式」 [!DNL Dynamic Media]。
* [在Cloud Services中建立Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想要進一步了解如何將所有資料夾同步至，請參閱主題中的「Dynamic Media同步模式」 [!DNL Dynamic Media]。

