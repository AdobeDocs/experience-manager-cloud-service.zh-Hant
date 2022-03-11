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

# 關於批集預設 {#about-bsp}

使用 **[!UICONTROL 批集預設]** 在將資產檔案單獨或使用批量攝取上載到資料夾時，在映像集或旋轉集中建立和組織多個資產。 您可以在計畫的資產導入作業旁邊運行預設運行 [!DNL Dynamic Media]。 每個預設都是唯一命名的、自包含的指令集，它定義如何使用與預設配方中定義的命名約定相匹配的影像構造影像集或旋轉集。

>[!IMPORTANT]
>
>是否在中使用批集預設 [!DNL Dynamic Media Classic]，從 [!DNL Dynamic Media Classic] Adobe Experience Manager as a Cloud Service? 如果是，則必須在中手動重新建立批集預設定義 [!DNL Adobe Experience Manager as a Cloud Service]。

**最佳實踐**  — 使用批集預設時Adobe建議使用以下工作流：

1. 建立批集預設。 請參閱 [為影像集或旋轉集建立批集預設](#creating-bsp)。
1. 建立資產資料夾或使用現有資產資料夾，並確保它已同步到 [!DNL Dynamic Media]。 請參閱 [建立資料夾](/help/assets/manage-digital-assets.md#creating-folders)。
1. 將批集預設應用於資產資料夾。 請參閱 [關於將批集預設應用到資料夾](#apply-bsp)。
1. 將影像上載到資產資料夾。 請參閱 [上載映像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)。 [上載旋轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或 [將數字資產添加到Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 影像集或旋轉集將在所需資料夾中自動生成。
1. 發佈映像集或旋轉集。 請參閱 [發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 為影像集或旋轉集建立批集預設 {#creating-bsp}

要建立批集預設，您最好對規則運算式有一些熟悉和瞭解。

理想情況下，您的公司已經定義了資產在集合中分組的命名約定。
為幫助您瞭解使用命名約定的重要性，假設您公司定義的命名約定是 `<style>-<color>-<view>`。 並且，集的基名必須始終為 `<style>-<color>`，並且集名副檔名為 `-SET`。 如果上載名為 `0123-RED-01`，然後建立名為 `0123-RED-SET`。 如果以後上載影像 `0123-RED-03` 和 `0123-BLUE-01`，則 `RED-03` 影像將添加到第二個位置的集合中，因為它的排序比 `01`。 然而， `BLUE-01` 影像將是名為 `0123-BLUE-SET`。 對於下次資產上載，您會添加檔案 `0123-RED-02` 和 `0123-BLUE-02`。 每項資產將加入其各自的資產組。 的 `RED-02` 影像將在現有影像之間自動排序 `01` 和 `03` 因為排序順序。

的 **[!UICONTROL 批集預設]** 頁面 [!DNL Dynamic Media] 允許您建立、編輯或刪除批集預設，以及將批集預設應用於資產資料夾或從資產資料夾中移除。 您可以使用表單域下拉清單定義批集預設或使用 **[!UICONTROL 原始代碼]** 欄位，用於鍵入規則運算式語法。

您可以建立許多批集預設，以覆蓋所需的所有資產攝取作業。

### 關於資產命名約定

的 **[!UICONTROL 資產命名約定]** 的上界 **[!UICONTROL 批集預設]** 頁面有兩個可用於定義批集預設的元素： **[!UICONTROL 匹配]** 和 **[!UICONTROL 基本名稱]**。 這些元素允許您定義命名約定並標識用於命名包含它們的集的約定部分。 <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的單個命名約定通常使用這兩個元素中每個元素的一行或多行定義。 您可以使用任意多行進行唯一定義，並將它們分組為不同的元素，如主影像、顏色元素、替代視圖元素和色板元素。

例如，文本匹配規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

### 關於序列排序

您可以選擇定義在影像集或旋轉集分組後顯示影像的順序 [!DNL Dynamic Media]。 預設情況下，資產按字母數字順序排列。 但是，可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您可以指定規則以某種方式強制對資產進行排序（如有必要）。 例如，假設您的第一個資產始終被命名 `_main` 你希望跟著 `_alt1`。 `_alt2`。 `_alt3`等等。 在這些情況下，可以使用以下語法建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然可以強制排序序列，但最好依靠字母數字編號來排序。 此外，還可在中使用影像集或旋轉集編輯器工具 [!DNL Dynamic Media] 來重新排列資產的順序，或使用拖放操作在集中添加和刪除新資產。

建立完批集預設後，將其應用於已建立的一個或多個資料夾。 請參閱 [關於將批集預設應用到資料夾](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**要為影像集或旋轉集建立批集預設：**

1. 選擇Experience Manager徽標並轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。

   ![bsp建立1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在 **[!UICONTROL 批集預設]** 頁面，靠近右上角，選擇 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立批集預設]** 對話框 **[!UICONTROL 預設名稱]** 文本欄位，輸入描述性名稱。 如果以後決定更改預設名稱，則該預設名稱不可編輯。

1. 在 **[!UICONTROL 預設類型]** 下拉清單，選擇 **[!UICONTROL 影像集]** 或 **[!UICONTROL 旋轉集]**。 確保選擇正確的預設類型；以後不可編輯。
1. 選擇 **[!UICONTROL 建立]**。
1. 論權利 **[!UICONTROL 編輯批集預設]** 的子菜單。 **[!UICONTROL 預設詳細資訊]** 和 **[!UICONTROL 設定命名約定]** 標題。
要瞭解有關可用的可編輯選項的詳細資訊，請參閱 [預設詳細資訊、設定命名約定和規則結果 — RegX選項](#features-options-bsp)。

   ![bsp建立4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一個或多個規則運算式組。

   * 左側 **[!UICONTROL 編輯批集預設]** 頁，下 **[!UICONTROL 匹配]**。 **[!UICONTROL 基本名稱]**&#x200B;或 **[!UICONTROL 序列排序]**&#x200B;選中 **[!UICONTROL 添加組]**。
   * 的 **[!UICONTROL 匹配]** 欄位。 **[!UICONTROL 基本名稱]** 只有在 **[!UICONTROL 匹配]** 欄位尚未使用括弧分組指定基名。 **[!UICONTROL 序列排序]** 為可選項。
   * 使用組窗體中的下拉清單和文本框，指定要用於定義影像集或旋轉集資產成員命名標準的表達式組。
      * 在為組選擇和指定表達式時，請注意實際規則運算式語法反映在頁面右下角的 **[!UICONTROL 規則結果 — RegX]** 的子菜單。 要查看在右下角更新的規則運算式字串，請選擇窗體區域外的任何位置。 這些規則運算式字串表示在搜索時要匹配的模式 [!DNL Dynamic Media] 用於建立映像集或旋轉集的資產。
      * 如果已添加組並要刪除它，請選擇 **[!UICONTROL X]**。
   * 添加兩個或多個組時， **[!UICONTROL 和]** 下拉清單，選擇 **[!UICONTROL 和]** 將新添加的組與添加的任何先前表達式組連接。 或，選擇 **[!UICONTROL 或]** 添加上一個表達式組和您建立的新組之間的更改。 的 **[!UICONTROL 或]** 操作數由使用垂直行字元定義 `|` 在規則運算式語法本身中。

1. 執行下列操作之一：

   * 要添加另一個新組，請在 **[!UICONTROL 匹配]**。 **[!UICONTROL 基本名稱]**&#x200B;或 **[!UICONTROL 排序順序]**&#x200B;選中 **[!UICONTROL 添加組]**。 建立另一個規則運算式組，如上一步中所做的那樣。
   * 查看中的規則運算式語法 **[!UICONTROL 規則結果 — RegX]** 的子菜單。 如果必須更改語法，請在頁面左側的相應組中進行編輯。
   * 如果已完成建立表達式組，請繼續執行下一步。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]**。

您現在可以將批集預設應用於資產資料夾。 然後，將資產上載到該資料夾。 此工作流導致自動生成映像集或旋轉集。 請參閱 [關於將批集預設應用到資產資料夾](#apply-bsp)。

### 預設詳細資訊、設定命名約定和規則結果 — RegX選項 {#features-options-bsp}

這些選項在 **[!UICONTROL 編輯批集預設]** 的子菜單。

請參閱 [為影像集或旋轉集建立批集預設](#creating-bsp) 或 [編輯批集預設](#edit-bsp)。

| **[!UICONTROL 預設集詳細資訊]** | 說明 |
| --- | --- |
| 預設集名稱 | 唯讀. 首次建立批集時指定的名稱。 如果必須更名預設，則可以複製現有批集預設並指定新名稱。 請參閱 [複製現有批集預設](#copy-bsp)。 |
| 類型 | 唯讀. 首次建立批集時指定了類型。 複製現有批集預設不允許您更改其 [!UICONTROL 類型];您必須改為建立預設。 |
| 包括衍生資產 | 選填。要 [!DNL Dynamic Media]&#39;s IPS（映像生成系統）包含已生成或「派生」的映像以及您的旋轉集或映像集，請選擇 **[!UICONTROL 是]** （預設）。 派生資產是用戶未直接上載的映像。 而是在上載主資產時由IPS生成資產。 例如，在PDF中上載PDF時，IPS從頁面生成的影像資產 [!DNL Dynamic Media]，被視為衍生資產。 |
| 目的地資料夾 | 選填。如果定義了大量影像集或旋轉集，Adobe建議將這些集與包含資產本身的資料夾分開。 因此，請考慮建立「映像集」或「旋轉集」資料夾，並將應用程式重定向到此處放置批處理集生成的集。<br>在這種情況下，指定Experience Manager Assets資料夾結構中的資料夾(`/content/dam`)已激活批處理集預設。 確保為 [!DNL Dynamic Media] 同步以允許它作為目標資料夾。 請參閱 [在Dynamic Media的資料夾級別配置選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)。<br>如果通過資料夾的方式應用預設，則多個資料夾可以為其分配給定批集預設 **[!UICONTROL 屬性]**。 請參閱 [從資產資料夾的「屬性」頁應用批集預設](#apply-bsp-to-folders-via-properties)。<br>如果未指定資料夾，則批處理集將在上載到的資產資料夾的同一資料夾中建立預設生成的影像集或旋轉集。 |
| **[!UICONTROL 設定命名慣例]** |  |
| 前置詞<br>或<br>尾碼 | 選填。在相應欄位中輸入前置詞、尾碼或兩者。<br>前置詞和尾碼欄位允許您使用特定內容集的備用自定義檔案命名約定建立許多批集預設。 在公司定義的預設命名方案存在異常時，此方法尤其有用。<br>前置詞或尾碼添加到 **[!UICONTROL 基本名稱]** 定義 **[!UICONTROL 資產命名約定]** 的子菜單。 通過添加前置詞或尾碼，可確保僅建立映像集或旋轉集，而不與其他資產獨立。 它還可進一步幫助其他人識別檔案類型。 例如，要確定使用的顏色模式，可以添加為前置詞或尾碼 `rgb` 或 `cmyk`。<br>雖然使用批處理集預設功能不需要指定集命名約定，但最佳實踐建議您使用集命名約定。 通過此練習，您可以定義想要在一個集合中分組的命名約定的任意多個元素，以幫助簡化批集建立。 |
| **[!UICONTROL 規則結果 - RegX]** |  |
| 資產命名約定 — 匹配 | 唯讀. 根據您選擇的「匹配」表單選項或輸入的原始代碼顯示規則運算式語法。 |
| 資產命名約定 — 基本名稱 | 唯讀. 根據您選擇的「基本名稱」表單選項或輸入的原始代碼顯示規則運算式語法。 |
| 順序 — 匹配 | 唯讀. 根據您選擇的表單選項或輸入的原始代碼顯示規則運算式語法。 |

## 關於將批集預設應用到資產資料夾 {#apply-bsp}

將批集預設分配給一個或多個資產資料夾時，任何子資料夾都會自動從其父資料夾繼承預設。

您可以將多個批集預設應用於資產資料夾。

在用戶介面中指示分配了批預置的資料夾，該預置的名稱出現在資料夾中，位於 **[!UICONTROL 卡]** 的子菜單。

要將批集預設應用於資產資料夾，請使用以下兩種方法之一：

* [將批集預設應用於「批集預設」頁中的資產資料夾](#apply-bsp-to-folders-via-bsp-page)  — 此方法為您提供了最大的靈活性。 可以將單個預設或多個預設應用於單個資料夾或多個資料夾。
* [從資產資料夾的「屬性」頁應用批集預設](#apply-bsp-to-folders-via-properties)  — 此方法允許您將一個或多個批集預設應用於單個資料夾。

作為最佳做法，請確保資產資料夾已同步 [!DNL Dynamic Media]，然後應用所需的預設。

如果您遇到以下兩種情況之一，請重新處理資料夾中的資產：

* 要在已上載資產的現有資產資料夾中運行批處理集預設。
* 稍後，您將編輯以前應用於資產資料夾的現有批集預設。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 將批集預設應用於「批集預設」頁中的資產資料夾 {#apply-bsp-to-folders-via-bsp-page}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。
1. 在 **[!UICONTROL 批集預設]** 頁，位於 **[!UICONTROL 預設名稱]** 列中，選中要應用於資料夾的每個批集預設的複選框。
1. 在工具欄中，選擇 **[!UICONTROL 將批預設應用於資料夾]**。
1. 在 **[!UICONTROL 選擇資料夾]** 頁中，選擇要應用批集預設的每個資料夾的複選框。
1. 在右上角 **[!UICONTROL 選擇資料夾]** ，選擇 **[!UICONTROL 應用]**。

### 從資產資料夾的「屬性」頁應用批集預設 {#apply-bsp-to-folders-via-properties}

1. 選擇Experience Manager徽標並轉到 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 導航到要應用一個或多個批集預設的資料夾。
1. 在頁面的左側 **[!UICONTROL 名稱]** 的子菜單。
1. 在工具欄中，選擇 **[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，選擇 **[!UICONTROL Dynamic Media加工]** 頁籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 下 **[!UICONTROL 批集預設]**，也請參見Wiki頁。 **[!UICONTROL 預設名稱]** 下拉清單框中，選擇要應用的批集預設的名稱。 上面的螢幕快照顯示了應用到資產資料夾的兩個選定的批集預設。

   如果中不存在批處理集預設名稱 **[!UICONTROL 預設名稱]** 下拉清單框，這意味著您尚未建立任何批集預設。 請參閱 [為影像集或旋轉集建立批集預設](#creating-bsp)。

   要刪除應用的批集預設，請選擇 **[!UICONTROL X]** 的子菜單。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存並關閉]**。

## 編輯批集預設 {#edit-bsp}

您可以編輯已建立的現有批集預設。 您可以更改為資產命名約定或順序建立的任何表達式組。 如果需要，還可以更新目標資料夾並設定命名約定。

但是，不能更改預設的名稱或預設類型（「影像集」或「旋轉集」）。 如果需要更改預設的名稱，請複製現有預設並指定新名稱。 請參閱 [複製批集預設](#copy-bsp)。

如果編輯以前應用於資料夾的批集預設，則新編輯的批集預設將僅應用於上載到該資料夾的新資產。

如果希望將新編輯的預設重新應用於資料夾中的現有資產，則必須重新處理該資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->這樣，現有資產現在將有資格成為映像集或旋轉集的一部分並添加。 此外，不會刪除已包含在影像集或旋轉集中的現有資產，並按原樣顯示。 此方案假定它們不再基於新編輯的預設進行限定。

**編輯批集預設：**

1. 選擇Experience Manager徽標並轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。
1. 在 **[!UICONTROL 批集預設]** 頁，位於 **[!UICONTROL 預設名稱]** 列，檢查要更改的批集預設。
1. 在工具欄中，選擇 **[!UICONTROL 編輯批集預設]**。
1. 根據需要編輯預設。
1. 在右上角 **[!UICONTROL 批集預設]** ，選擇 **[!UICONTROL 保存]**。

## 複製現有批集預設 {#copy-bsp}

您可以複製現有批集預設，以避免手動重新建立複雜的預設，或者只是要更名預設。 但是，不能更改使用的預設類型（「影像集」或「旋轉集」）。

如果複製由資產資料夾引用的現有預設，則這些資料夾不會受到影響。

**複製現有批集預設：**

1. 選擇Experience Manager徽標並轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。
1. 在 **[!UICONTROL 批集預設]** 頁，位於 **[!UICONTROL 預設名稱]** 列中，選擇要複製的批集預設的複選框。
1. 在工具欄中，選擇 **[!UICONTROL 複製]**。
1. 在 **[!UICONTROL 複製批集預設]** 對話框 **[!UICONTROL 標題]** 框中，鍵入預設的新名稱。

   ![bsp copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 選擇 **[!UICONTROL 複製]**。

## 關於從資料夾中刪除批集預設 {#remove-bsp-from-folder}

從資料夾中刪除批集預設時，您上載到這些資料夾的任何新資產都沒有將批集預設應用於這些資產。 資料夾中已添加到影像集或基於批集的、已應用於資料夾的預設的現有資產 — 繼續顯示原樣。

如果你想 *刪除* 從資料夾中預置，請參閱 [刪除批集預設](#delete-bsp)。

有兩種方法可用於從資料夾中刪除批集預設。

* [通過「批集預設」頁從資料夾中刪除批集預設](#remove-bsp-from-folders-via-bsp-page)  — 此方法為您提供了最大的靈活性。 可以從單個資料夾或多個資料夾中刪除單個預設或多個預設。
* [從資料夾的「屬性」頁中刪除批集預設](#remove-bsp-from-folders-via-properties)  — 此方法允許您僅從單個資料夾中刪除一個或多個批集預設。

### 通過「批集預設」頁從資料夾中刪除批集預設 {#remove-bsp-from-folders-via-bsp-page}

1. 選擇Experience Manager徽標並轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。
1. 在 **[!UICONTROL 批集預設]** 頁，位於 **[!UICONTROL 預設名稱]** 列中，選中要從一個或多個資料夾中刪除的一個或多個批集預設的複選框。
1. 在工具欄中，選擇 **[!UICONTROL 從資料夾中刪除批預設]**。

1. 在 **[!UICONTROL 選擇資料夾]** 的子菜單。
1. 在右上角 **[!UICONTROL 選擇資料夾]** ，選擇 **[!UICONTROL 刪除]**。

   ![bsp從資料夾中刪除3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在 **[!UICONTROL 刪除配置檔案]** 對話框，選擇 **[!UICONTROL 刪除]**。

### 從資料夾的「屬性」頁中刪除批集預設 {#remove-bsp-from-folders-via-properties}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 導航到要刪除一個或多個批集預設的資料夾。
1. 在頁面的左側 **[!UICONTROL 名稱]** 的子菜單。
1. 在工具欄中，選擇 **[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，選擇 **[!UICONTROL Dynamic Media加工]**。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 下 **[!UICONTROL 批集預設]**&#x200B;選中 **[!UICONTROL X]** 的子菜單。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存並關閉]**。

## 刪除批集預設 {#delete-bsp}

您可以刪除批集預設，以永久從 [!DNL Dynamic Media]。 就是說，他們不再在 [!UICONTROL 批集預設] 頁面中也未顯示 **[!UICONTROL 批集預設]** 下拉清單 **[!UICONTROL Dynamic Media加工]** 的 **[!UICONTROL 屬性]** 的子菜單。 因此，預置不會應用於資料夾重新處理中的現有資產，或者當新資產上載到資料夾中時。

如果刪除以前應用於一個或多個資料夾的預設，則從這些資料夾中的資產建立的任何影像集或旋轉集將繼續按原樣顯示。

如果你想 *刪除* 從資料夾中預置，請參閱 [從資料夾中刪除批集預設](#remove-bsp-from-folder)。

**要刪除批集預設：**

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批集預設]**。
1. 在 **[!UICONTROL 批集預設]** 頁，位於 **[!UICONTROL 預設名稱]** 列中，選中要刪除的一個或多個批集預設的複選框。
1. 在工具欄中，選擇 **[!UICONTROL 刪除批集預設]**。

   ![bsp delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在 **[!UICONTROL 刪除批集預設]** 對話框，選擇 **[!UICONTROL 刪除]**。

   如果要刪除的預設被資產資料夾引用，請選擇 **[!UICONTROL 強制刪除]** 的雙曲餘切值。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [影像集](/help/assets/dynamic-media/image-sets.md)
>* [迴轉集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media的資料夾級別配置選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果要瞭解有關將單個資料夾同步到的詳細資訊，請參閱主題中的「同步模式」 [!DNL Dynamic Media]。
>* [在Cloud Services中建立Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想瞭解有關將所有資料夾同步到的詳細資訊，請參閱主題中的「Dynamic Media同步模式」 [!DNL Dynamic Media]。

