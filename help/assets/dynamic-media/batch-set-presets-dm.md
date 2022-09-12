---
title: 批次集預設集
description: 了解如何使用 Dynamic Media 中的批次集預設集自動建立影像集和迴轉集。
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# 關於批集預設集 {#about-bsp}

使用 **[!UICONTROL 批集預設集]** 若要在個別或使用大量擷取將資產檔案上傳至資料夾時，在影像集或回轉集中建立並組織多個資產。 您可以在排程的資產匯入工作旁邊執行預設集 [!DNL Dynamic Media]. 每個預設集都是一組唯一命名的自包含指令，定義如何使用符合預設方式中已定義命名慣例的影像來建構影像集或回轉集。

>[!IMPORTANT]
>
>您是否在中使用批次集預設集 [!DNL Dynamic Media Classic]，並從 [!DNL Dynamic Media Classic] Adobe Experience Manager as a Cloud Service? 如果是，您必須在中手動重新建立批次集預設集定義 [!DNL Adobe Experience Manager as a Cloud Service].

**最佳實務**  — 使用批集預設集時，Adobe建議使用以下工作流：

1. 建立批集預設集。 請參閱 [為影像集或回轉集建立批集預設集](#creating-bsp).
1. 建立資產資料夾或使用現有資產資料夾，並確認已同步至 [!DNL Dynamic Media]. 請參閱 [建立資料夾](/help/assets/manage-digital-assets.md#creating-folders).
1. 將批次集預設集套用至資產資料夾。 請參閱 [關於將批集預設集應用於資料夾](#apply-bsp).
1. 上傳影像至資產資料夾。 請參閱 [上傳影像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [上傳回轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)，或 [新增數位資產至Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. 影像集或回轉集會在所需資料夾中自動產生。
1. 發佈影像集或回轉集。 請參閱 [發佈Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 為影像集或回轉集建立批集預設集 {#creating-bsp}

若要建立批集預設集，您應熟悉並了解規則運算式。

理想情況下，您的公司已定義資產在集合中分組方式的命名慣例。
為協助您了解使用命名慣例的重要性，假設貴公司定義的命名慣例為 `<style>-<color>-<view>`. 而且，集的基名必須始終為 `<style>-<color>`，而設定名稱副檔名為 `-SET`. 如果您上傳的影像名為 `0123-RED-01`，則會建立名為 `0123-RED-SET`. 如果您稍後上傳影像 `0123-RED-03` 和 `0123-BLUE-01`，則 `RED-03` 影像會新增至第二個位置的集合，因為排序順序低於 `01`. 不過， `BLUE-01` 影像將是新集合的一部分，命名為 `0123-BLUE-SET`. 您會為下次資產上傳新增檔案 `0123-RED-02` 和 `0123-BLUE-02`. 每項資產將加入其各自的資產組。 此 `RED-02` 影像會在現有 `01` 和 `03` 因為排序順序。

此 **[!UICONTROL 批集預設集]** 頁面 [!DNL Dynamic Media] 可讓您建立、編輯或刪除批次集預設集，以及在資產資料夾中套用或移除批次集預設集。 您可以使用表單欄位下拉式清單來定義批次集預設集，或使用 **[!UICONTROL 原始程式碼]** 欄位，可讓您輸入規則運算式語法。

您可以建立許多批次集預設集，以涵蓋所有您需要的資產內嵌作業。

### 關於資產命名慣例

此 **[!UICONTROL 資產命名慣例]** 區域 **[!UICONTROL 批集預設集]** 「頁面」有兩個元素，您可以用來定義批次集預設集： **[!UICONTROL 符合]** 和 **[!UICONTROL 基本名稱]**. 這些元素可讓您定義命名慣例，並識別用來為其所包含集命名的慣例部分。 <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的個別命名慣例通常會從這兩個元素中的每一行使用一或多行定義。 您可以針對唯一定義使用任意數行，並將它們分組為不同的元素，例如主影像、顏色元素、替代視圖元素和色票元素。

例如，常值比對規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

### 關於序列順序

您可以選擇定義影像集或回轉集分組後，影像的顯示順序 [!DNL Dynamic Media]. 依預設，您的資產依字母順序排列。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您需要指定規則，以特定方式強制排序資產。 例如，假設您的第一個資產一律命名為 `_main` 你想跟著 `_alt1`, `_alt2`, `_alt3`等。 在這種情況下，您可以使用下列語法來建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然可以強制排序序列，但最好盡可能依靠字母數字編號來排序序列。 此外，您還可以在 [!DNL Dynamic Media] 重新排列資產的順序，或使用拖放操作在集中新增和刪除新資產。

完成建立批集預設集後，可將其應用於已建立的一個或多個資料夾。 請參閱 [關於將批集預設集應用於資料夾](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要為影像集或回轉集建立批集預設集：**

1. 選取Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在 **[!UICONTROL 批集預設集]** 頁面，在右上角附近，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立批集預設集]** 對話框， **[!UICONTROL 預設集名稱]** 文本欄位，輸入描述性名稱。 如果您稍後決定變更預設集名稱，該預設集名稱將無法編輯。

1. 在 **[!UICONTROL 預設類型]** 下拉清單，選擇 **[!UICONTROL ImageSet]** 或 **[!UICONTROL 回轉集]**. 請務必選擇正確的預設集類型；以後無法編輯。
1. 選擇 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 編輯批集預設集]** 頁面，在 **[!UICONTROL 預設集詳細資料]** 和 **[!UICONTROL 設定命名慣例]** 標題。
若要進一步了解您可使用的可編輯選項，請參閱 [預設集詳細資訊、設定命名慣例和規則結果 — RegX選項](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一或多個規則運算式群組。

   * 在 **[!UICONTROL 編輯批集預設集]** 頁面下方 **[!UICONTROL 符合]**, **[!UICONTROL 基本名稱]**，或 **[!UICONTROL 序列排序]**，選取 **[!UICONTROL 新增群組]**.
   * 此 **[!UICONTROL 符合]** 欄位為必填。 **[!UICONTROL 基本名稱]** 只有在 **[!UICONTROL 符合]** 欄位尚未使用括弧分組來指定基名。 **[!UICONTROL 序列排序]** 為選用。
   * 使用組窗體中的下拉清單和文本框，指定要用來定義影像集或回轉集資產成員命名標準的表達式組。
      * 當您選取並指定群組的運算式時，請注意實際的規則運算式語法會反映在頁面右下方的 **[!UICONTROL 規則結果 — RegX]** 標題。 若要查看右下角更新的規則運算式字串，請選取表單區域以外的任何位置。 這些規則運算式字串代表您要在搜尋中比對的模式 [!DNL Dynamic Media] 資產來建立影像集或回轉集。
      * 如果您已新增群組且想將其移除，請選取 **[!UICONTROL X]**.
   * 新增兩個或多個群組時， **[!UICONTROL 和]** 下拉清單，選擇 **[!UICONTROL 和]** 將新添加的組與添加的任何先前表達式組連接。 或者，選取 **[!UICONTROL 或]** 添加前一個表達式組和所建立新組之間的更改。 此 **[!UICONTROL 或]** 操作數由使用垂直行字元來定義 `|` 規則運算式語法本身。

1. 執行下列任一項作業：

   * 若要新增其他新群組，請在 **[!UICONTROL 符合]**, **[!UICONTROL 基本名稱]**，或 **[!UICONTROL 排序順序]**，選取 **[!UICONTROL 新增群組]**. 建立另一個規則運算式群組，如上一步所述。
   * 請參閱 **[!UICONTROL 規則結果 — RegX]** 的上界。 如果您必須變更語法，請在頁面左側的個別群組中進行編輯。
   * 如果已完成運算式群組的建立，請繼續下一個步驟。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

您現在可以將批次集預設集套用至資產資料夾。 接著，您上傳資產至該資料夾。 此工作流程會自動產生影像集或回轉集。 請參閱 [關於將批次集預設集套用至資產資料夾](#apply-bsp).

### 預設集詳細資訊、設定命名慣例和規則結果 — RegX選項 {#features-options-bsp}

這些選項可在 **[!UICONTROL 編輯批集預設集]** 頁面。

請參閱 [為影像集或回轉集建立批集預設集](#creating-bsp) 或 [編輯批集預設集](#edit-bsp).

| **[!UICONTROL 預設集詳細資訊]** | 說明 |
| --- | --- |
| 預設集名稱 | 唯讀. 首次建立批集時指定的名稱。 如果必須更名預設集，則可以複製現有批集預設集並指定新名稱。 請參閱 [複製現有批集預設集](#copy-bsp). |
| 類型 | 唯讀. 首次建立批集時指定了類型。 複製現有批集預設集不允許您更改它 [!UICONTROL 類型];您必須改為建立預設集。 |
| 包括衍生資產 | 選填。若要 [!DNL Dynamic Media]的IPS（映像生產系統）包含帶回轉集或映像集的已生成或「派生」映像，請選擇 **[!UICONTROL 是]** （預設）。 衍生資產是使用者未直接上傳的影像。 相反地，資產是在上傳主資產時由IPS產生的。 例如，IPS在PDF中的頁面上傳PDF時，從頁面產生的影像資產 [!DNL Dynamic Media]，則視為衍生資產。 |
| 目的地資料夾 | 選填。如果您定義大量影像集或回轉集，Adobe建議您將這些集與包含資產本身的資料夾分開。 因此，請考慮建立「影像集」或「回轉集」資料夾，並將應用程式重新導向，將批集生成的集放置在此處。<br>在這種情況下，請指定Experience Manager Assets資料夾結構中的哪個資料夾(`/content/dam`)的批次集預設集已啟用。 請確定已為 [!DNL Dynamic Media] 同步，允許其作為目標資料夾。 請參閱 [在Dynamic Media的資料夾層級設定選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>如果通過資料夾的應用預設集，則可以為多個資料夾分配指定的批集預設集 **[!UICONTROL 屬性]**. 請參閱 [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties).<br>如果您未指定資料夾，則會在與您上傳至的資產資料夾相同的資料夾中建立批次集預設產生的影像集或回轉集。 |
| **[!UICONTROL 設定命名慣例]** |  |
| 前置詞<br>或<br>尾碼 | 選填。在相應欄位中輸入前置詞、尾碼或兩者。<br>前置詞和尾碼欄位可讓您針對特定內容集使用替代的自訂檔案命名慣例來建立許多批次集預設集。 在公司定義的預設命名方案有例外的情況下，此方法特別實用。<br>前置詞或尾碼會新增至 **[!UICONTROL 基本名稱]** 在 **[!UICONTROL 資產命名慣例]** 的上界。 借由新增首碼或尾碼，您可確保您的影像集或回轉集完全獨立於其他資產建立。 也可進一步協助其他人識別檔案類型。 例如，若要判斷所使用的色彩模式，您可以新增為首碼或尾碼 `rgb` 或 `cmyk`.<br>雖然使用批集預設集功能不需要指定集命名慣例，但最佳實務建議您使用集命名慣例。 此慣例可讓您定義想要分組到一組中的命名慣例的多個元素，以協助簡化批次集建立。 |
| **[!UICONTROL 規則結果 - RegX]** |  |
| 資產命名慣例 — 符合 | 唯讀. 根據您選擇的「符合」表單選項或您輸入的原始程式碼，顯示規則運算式語法。 |
| 資產命名慣例 — 基本名稱 | 唯讀. 根據您選擇的「基本名稱」表單選項或您輸入的原始代碼顯示規則運算式語法。 |
| 序列排序 — 匹配 | 唯讀. 根據您選擇的表單選項或您輸入的原始程式碼顯示規則運算式語法。 |

## 關於將批次集預設集套用至資產資料夾 {#apply-bsp}

將批集預設集分配給一個或多個資產資料夾時，任何子資料夾都會自動從其父資料夾繼承預設集。

您可以將多個批次集預設集套用至資產資料夾。

為其分配了批預設的資料夾會在用戶介面中指示，而預設的名稱會出現在資料夾中的 **[!UICONTROL 卡片]** 檢視。

若要將批次集預設集套用至資產資料夾，請使用下列兩種方法之一：

* [從「批集預設集」頁將批集預設集應用於資產資料夾](#apply-bsp-to-folders-via-bsp-page)  — 此方法可提供您最大的彈性。 您可以將單一預設集或多個預設集套用至單一資料夾或多個資料夾。
* [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties)  — 此方法可讓您將一或多個批次集預設集套用至單一資料夾。

最佳實務是，請確定已同步資產資料夾 [!DNL Dynamic Media]，然後套用您想要的預設集。

如果您遇到下列兩種情況之一，請重新處理資料夾中的資產：

* 您想要在現有資產資料夾上執行已上傳資產的批次集預設集。
* 您之後可以編輯先前已套用至資產資料夾的現有批次集預設集。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 從「批集預設集」頁將批集預設集應用於資產資料夾 {#apply-bsp-to-folders-via-bsp-page}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.
1. 在 **[!UICONTROL 批集預設集]** 頁面左側 **[!UICONTROL 預設集名稱]** 欄，選中要應用於資料夾的每個批集預設集的複選框。
1. 在工具列中，選取 **[!UICONTROL 將批預設集應用於資料夾]**.
1. 在 **[!UICONTROL 選擇資料夾]** 頁，選中要應用批集預設集的每個資料夾的複選框。
1. 位於 **[!UICONTROL 選擇資料夾]** 頁面，選取 **[!UICONTROL 套用]**.

### 從資產資料夾的「屬性」頁面套用批次集預設集 {#apply-bsp-to-folders-via-properties}

1. 選取Experience Manager標誌，然後前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要套用一或多個批次集預設集的資料夾。
1. 在頁面上，位於 **[!UICONTROL 名稱]** 欄中，選擇資料夾的複選框。
1. 在工具列中，選取 **[!UICONTROL 屬性]**.
1. 在資料夾的「屬性」頁面上，選取 **[!UICONTROL Dynamic Media處理]** 標籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在 **[!UICONTROL 批集預設集]**，從 **[!UICONTROL 預設集名稱]** 下拉式清單方塊中，選取您要套用的批次集預設集名稱。 上方的螢幕擷圖顯示套用至資產資料夾的兩個選取批次集預設集。

   如果中不存在批集預設集名稱 **[!UICONTROL 預設集名稱]** 下拉清單框，表示您尚未建立任何批集預設集。 請參閱 [為影像集或回轉集建立批集預設集](#creating-bsp).

   要刪除應用的批集預設集，請選擇 **[!UICONTROL X]** 的右側。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.

## 編輯批集預設集 {#edit-bsp}

您可以編輯已建立的現有批集預設集。 您可以變更為資產命名慣例或順序建立的任何運算式群組。 如有需要，您也可以更新目標資料夾並設定命名慣例。

不過，您無法變更預設集的名稱或預設集類型（「影像集」或「回轉集」）。 如果有必要變更預設集的名稱，請複製現有的預設集並指定新名稱。 請參閱 [複製批集預設集](#copy-bsp).

如果您編輯先前已套用至資料夾的批次集預設集，新編輯的批次集預設集只會套用至上傳至該資料夾的新資產。

如果您想要將新編輯的預設集重新套用至資料夾中的現有資產，您必須重新處理資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->如此一來，現有資產現在就可以成為影像集或回轉集的一部分，並可以新增。 此外，影像集或回轉集中已包含的現有資產（根據先前使用的批次集預設集）不會遭到移除，且會如實顯示。 此案例假設他們不再根據新編輯的預設集符合資格。

**要編輯批集預設集，請執行以下操作：**

1. 選取Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.
1. 在 **[!UICONTROL 批集預設集]** 頁面左側 **[!UICONTROL 預設集名稱]** 欄，檢查要更改的批集預設集。
1. 在工具列中，選取 **[!UICONTROL 編輯批集預設集]**.
1. 視需要編輯預設集。
1. 位於 **[!UICONTROL 批集預設集]** 頁面，選取 **[!UICONTROL 儲存]**.

## 複製現有批集預設集 {#copy-bsp}

您可以複製現有的批集預設集，以避免手動重新建立複雜的預設集，或者只是想更名預設集。 但您無法變更所使用的預設集類型（影像集或回轉集）。

如果您複製由資產資料夾參照的現有預設集，這些資料夾不受影響。

**複製現有批集預設集：**

1. 選取Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.
1. 在 **[!UICONTROL 批集預設集]** 頁面左側 **[!UICONTROL 預設集名稱]** 欄，選中要複製的批集預設集的複選框。
1. 在工具列中，選取 **[!UICONTROL 複製]**.
1. 在 **[!UICONTROL 複製批集預設集]** 對話框， **[!UICONTROL 標題]** 框中，鍵入預設集的新名稱。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 選擇 **[!UICONTROL 複製]**.

## 關於從資料夾中刪除批集預設集 {#remove-bsp-from-folder}

當您從資料夾中移除批次集預設集時，上傳至這些資料夾的任何新資產都不會套用批次集預設集。 資料夾中已新增至影像集的現有資產，或根據套用至資料夾的批次集預設集來指定資產，繼續按原樣顯示。

如果您想 *刪除* 改用資料夾中的預設集，請參閱 [刪除批集預設集](#delete-bsp).

有兩種方法可用來從資料夾中移除批次集預設集。

* [通過「批集預設集」頁從資料夾中刪除批集預設集](#remove-bsp-from-folders-via-bsp-page)  — 此方法可提供您最大的彈性。 您可以從單一資料夾或多個資料夾中移除單一預設集或多個預設集。
* [從資料夾的「屬性」頁中刪除批集預設集](#remove-bsp-from-folders-via-properties)  — 此方法可讓您僅從單一資料夾中移除一或多個批次集預設集。

### 通過「批集預設集」頁從資料夾中刪除批集預設集 {#remove-bsp-from-folders-via-bsp-page}

1. 選取Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.
1. 在 **[!UICONTROL 批集預設集]** 頁面左側 **[!UICONTROL 預設集名稱]** 列中，選中要從一個或多個資料夾中刪除的一個或多個批集預設集的複選框。
1. 在工具列中，選取 **[!UICONTROL 從資料夾中刪除批預設集]**.

1. 在 **[!UICONTROL 選擇資料夾]** 頁，選擇要刪除批集預設集的一個或多個資料夾。
1. 位於 **[!UICONTROL 選擇資料夾]** 頁面，選取 **[!UICONTROL 移除]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在 **[!UICONTROL 移除設定檔]** 對話框，選擇 **[!UICONTROL 移除]**.

### 從資料夾的「屬性」頁中刪除批集預設集 {#remove-bsp-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要移除一或多個批次集預設集的資料夾。
1. 在頁面上，位於 **[!UICONTROL 名稱]** 欄中，選擇資料夾的複選框。
1. 在工具列中，選取 **[!UICONTROL 屬性]**.
1. 在資料夾的「屬性」頁上，選擇 **[!UICONTROL Dynamic Media處理]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在 **[!UICONTROL 批集預設集]**，選取 **[!UICONTROL X]** 的右側。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.

## 刪除批集預設集 {#delete-bsp}

您可以刪除批集預設集，以便從 [!DNL Dynamic Media]. 也就是說，它們不再顯示於 [!UICONTROL 批集預設集] 頁面中也不顯示 **[!UICONTROL 批集預設集]** 下拉式清單 **[!UICONTROL Dynamic Media處理]** 頁簽 **[!UICONTROL 屬性]** 頁面。 因此，重新處理資料夾或在資料夾中上傳新資產時，預設集不會套用至現有資產。

如果您刪除先前已套用至一或多個資料夾的預設集，從這些資料夾中的資產建立的任何影像集或回轉集會繼續依現狀顯示。

如果您想 *移除* 改用資料夾中的預設集，請參閱 [從資料夾中刪除批集預設集](#remove-bsp-from-folder).

**要刪除批集預設集：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設集]**.
1. 在 **[!UICONTROL 批集預設集]** 頁面左側 **[!UICONTROL 預設集名稱]** 列中，選中要刪除的一個或多個批集預設集的複選框。
1. 在工具列中，選取 **[!UICONTROL 刪除批集預設集]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在 **[!UICONTROL 刪除批集預設集]** 對話框，選擇 **[!UICONTROL 刪除]**.

   如果您要刪除的預設集被資產資料夾參照，請選取 **[!UICONTROL 強制刪除]** 。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [影像集](/help/assets/dynamic-media/image-sets.md)
>* [迴轉集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media的資料夾層級設定選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果您想要進一步了解如何將單一資料夾同步至 [!DNL Dynamic Media].
>* [在Cloud Services中建立Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想要進一步了解如何將所有資料夾同步至 [!DNL Dynamic Media].

