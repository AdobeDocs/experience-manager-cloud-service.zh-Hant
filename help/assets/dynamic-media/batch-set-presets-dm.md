---
title: 大量集預設集
description: 瞭解如何使用Dynamic Media中的批次集預設集自動建立影像集和迴轉集。
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '3480'
ht-degree: 1%

---

# 關於批次集預設集 {#about-bsp}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

當您個別或大量擷取將資產檔案上傳至資料夾時，可使用&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;在影像集或迴轉集中建立及組織多個資產。 您可以讓預設集與您排程在[!DNL Dynamic Media]中的資產匯入工作一起執行。 每個預設集都是一組名稱唯一、內含的指示，定義如何使用符合預設集中定義的命名慣例的影像來建構影像集或迴轉集。

>[!IMPORTANT]
>
>您是否在[!DNL Dynamic Media Classic]中使用批次集預設集，並從[!DNL Dynamic Media Classic]移轉至Adobe Experience Manager as a Cloud Service？ 若是如此，您必須在[!DNL Adobe Experience Manager as a Cloud Service]內手動重新建立批次集預設集定義。

**最佳實務** — 使用批次集預設集時，Adobe建議使用下列工作流程：

1. 建立批次集預設集。 請參閱[為影像集或迴轉集建立批次集預設集](#creating-bsp)。
1. 建立資產資料夾或使用現有的資產資料夾，並確保它已同步至[!DNL Dynamic Media]。 請參閱[建立資料夾](/help/assets/manage-digital-assets.md#creating-folders)。
1. 將批次集預設集套用至資產資料夾。 請參閱[關於將批次集預設集套用至資料夾](#apply-bsp)。
1. 將影像上傳至資產資料夾。 請參閱[上傳影像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)、[上傳迴轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)或[新增數位資產至Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager)。
1. 影像集或迴轉集會在所需的資料夾中自動產生。
1. 發佈影像集或迴轉集。 請參閱[發佈Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 為影像集或迴轉集建立批次集預設集 {#creating-bsp}

若要建立批次集預設集，最好熟悉並瞭解規則運算式。

理想情況下，貴公司已針對資產在集合中的分組方式定義命名慣例。
為協助您瞭解使用命名慣例的重要性，假設貴公司定義的命名慣例為`<style>-<color>-<view>`。 而且，集合的基底名稱必須一律為`<style>-<color>`，集合名稱副檔名為`-SET`。 如果您上傳名為`0123-RED-01`的影像，則會建立名為`0123-RED-SET`的集合。 如果您稍後上傳影像`0123-RED-03`和`0123-BLUE-01`，則會在第二個位置將`RED-03`影像新增到影像集，因為其排序低於`01`。 不過，`BLUE-01`影像會是一個名為`0123-BLUE-SET`的新集合的一部分。 在下次上傳資產時，您新增檔案`0123-RED-02`和`0123-BLUE-02`。 每個資產都會新增至其個別的集合。 由於排序順序，`RED-02`影像將會在現有`01`和`03`影像之間自動排序。

[!DNL Dynamic Media]中的&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面可讓您建立、編輯或刪除批次集預設集，以及將批次集預設集套用至資產資料夾或從資產資料夾中移除批次集預設集。 您可以使用表單欄位下拉式清單來定義批次集預設集，或是使用&#x200B;**[!UICONTROL 原始程式碼]**&#x200B;欄位，讓您輸入規則運算式語法。

您可以建立許多批次集預設集，以涵蓋所需的所有資產擷取作業。

### 關於資產命名慣例

**[!UICONTROL 批次集預設集]**&#x200B;頁面上的&#x200B;**[!UICONTROL 資產命名慣例]**&#x200B;區域有兩個可用來定義批次集預設集的元素： **[!UICONTROL 符合]**&#x200B;和&#x200B;**[!UICONTROL 基本名稱]**。 這些元素可讓您定義命名慣例，並識別用於命名包含這些元素的集的慣例部分。<!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的個別命名慣例通常使用來自這兩個元素中每個元素的一或多行定義。 您可以針對唯一的定義使用儘可能多的線條，並將它們分組為不同的元素，例如「主影像」、「顏色」元素、「替代檢視」元素和「色票」元素。

例如，常值比對規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

### 關於序列順序

您可以選擇定義影像集或迴轉集分組到[!DNL Dynamic Media]後影像的顯示順序。 根據預設，您的資產會依字母數字排序。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您可以指定規則，在必要時以特定方式強制排序資產。 例如，假設您的第一個資產一律名為`_main`，您希望它後面有`_alt1`、`_alt2`、`_alt3`等。 在這種情況下，您可以使用以下語法建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然強制排序序列是可行的，但最好儘可能依賴字母數字編號來排序序列。 此外，您可以在[!DNL Dynamic Media]中使用影像集或迴轉集編輯器工具，重新排列資產的順序順序，或使用拖放操作新增和刪除集合中的新資產。

當您完成建立批次集預設集時，可將其套用至您已建立的一或多個資料夾。 請參閱[關於將批次集預設集套用至資料夾](#apply-bsp)。

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**若要建立影像集或迴轉集的批次集預設集：**

1. 選取Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立批次集預設集]**&#x200B;對話方塊的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;文字欄位中，輸入描述性名稱。 如果您稍後決定變更預設集名稱，則無法編輯預設集名稱。

1. 在&#x200B;**[!UICONTROL 預設集型別]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 影像集]**&#x200B;或&#x200B;**[!UICONTROL 迴轉集]**。 請確定您選擇正確的預設集型別；之後將無法編輯。
1. 選取「**[!UICONTROL 建立]**」。
1. 在&#x200B;**[!UICONTROL 編輯批次集預設集]**&#x200B;頁面的右側，在&#x200B;**[!UICONTROL 預設集詳細資料]**&#x200B;和&#x200B;**[!UICONTROL 設定命名慣例]**標題下設定您想要的可編輯選項。
若要深入瞭解您可用的可編輯選項，請參閱[預設集詳細資訊、設定命名慣例和規則結果 — RegX選項](#features-options-bsp)。

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一或多個規則運算式群組。

   * 在&#x200B;**[!UICONTROL 編輯批次集預設集]**&#x200B;頁面的左側，在&#x200B;**[!UICONTROL 符合]**、**[!UICONTROL 基本名稱]**&#x200B;或&#x200B;**[!UICONTROL 序列順序]**&#x200B;下，選取&#x200B;**[!UICONTROL 新增群組]**。
   * **[!UICONTROL 符合]**&#x200B;欄位為必填。 只有在&#x200B;**[!UICONTROL Match]**&#x200B;欄位尚未使用括弧群組指定基底名稱時，**[!UICONTROL 基底名稱]**&#x200B;才為必要。 **[!UICONTROL 順序順序]**&#x200B;是選擇性的。
   * 使用群組表單中的下拉式清單和文字方塊，指定您要用來定義影像集或迴轉集資產成員命名條件的運算式群組。
      * 當您選取並指定群組的運算式時，請注意，實際的規則運算式語法會反映在頁面右下角附近，**[!UICONTROL 規則結果 — RegX]**&#x200B;標題下。 若要檢視更新於右下角的規則運算式字串，請選取表單區域之外的任意位置。 這些規則運算式字串代表您在搜尋[!DNL Dynamic Media]個資產以建立影像集或迴轉集時要比對的模式。
      * 如果您已新增群組且想要移除它，請選取&#x200B;**[!UICONTROL X]**。
   * 當您新增兩個或更多群組時，請在&#x200B;**[!UICONTROL And]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL And]**，以將新新增的群組與您之前新增的任何運算式群組連結。 或者，選取&#x200B;**[!UICONTROL 或]**，在先前的運算式群組與您建立的新群組之間新增替代。 **[!UICONTROL Or]**&#x200B;運算元是在規則運算式語法本身中使用垂直行字元`|`來定義。

1. 執行下列任一項作業：

   * 若要新增另一個群組，請在&#x200B;**[!UICONTROL 符合]**、**[!UICONTROL 基本名稱]**&#x200B;或&#x200B;**[!UICONTROL 排序順序]**&#x200B;下選取&#x200B;**[!UICONTROL 新增群組]**。 建立另一個規則運算式群組，就像在上一步中所做的那樣。
   * 檢閱&#x200B;**[!UICONTROL 規則結果 — RegX]**&#x200B;區域中的規則運算式語法。 如果您必須變更語法，請在頁面左側的個別群組中執行編輯。
   * 如果您已完成建立運算式群組，請繼續進行下一個步驟。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。

您現在可以將批次集預設集套用至資產資料夾。 接著，將資產上傳至該資料夾。 此工作流程會自動產生影像集或迴轉集。 請參閱[關於將批次集預設集套用至資產資料夾](#apply-bsp)。

### 預設集詳細資訊、設定命名慣例和規則結果 — RegX選項 {#features-options-bsp}

當您建立或編輯批次集預設集時，這些選項可在&#x200B;**[!UICONTROL 編輯批次集預設集]**&#x200B;頁面上使用。

請參閱[為影像集或迴轉集建立批次集預設集](#creating-bsp)或[編輯批次集預設集](#edit-bsp)。

| **[!UICONTROL 預設集詳細資料]** | 描述 |
| --- | --- |
| 預設集名稱 | 唯讀。 您第一次建立批次集時所指定的名稱。 如果您必須重新命名預設集，您可以複製現有的批次集預設集並指定新名稱。 請參閱[複製現有的批次集預設集](#copy-bsp)。 |
| 類型 | 唯讀。 當您初次建立批次集時指定了型別。 複製現有的批次集預設集無法讓您變更其[!UICONTROL 型別]；您必須改為建立預設集。 |
| 包括衍生資產 | 選擇性。若要讓[!DNL Dynamic Media]的IPS （影像生產系統）包含使用您的迴轉集或影像集產生或「衍生」的影像，請選取&#x200B;**[!UICONTROL 是]** （預設）。 衍生資產是使用者未直接上傳的影像。 而是在上傳主要資產時，由IPS產生資產。 例如，在[!DNL Dynamic Media]中上傳PDF時，IPS從PDF中的頁面產生的影像資產會視為衍生資產。 |
| 目的地資料夾 | 選擇性。如果您定義大量影像集或迴轉集，Adobe建議您將這些影像集與包含資產本身的資料夾分開。 因此，請考慮建立「影像集」或「迴轉集」資料夾，並將應用程式重新導向，以在此放置批次集產生的集合。<br>在這種情況下，請指定Experience Manager Assets資料夾結構(`/content/dam`)中的哪個資料夾已啟用批次集預設集。 請確定資料夾已啟用[!DNL Dynamic Media]同步處理，以允許它作為目的地資料夾。 請參閱[在Dynamic Media中設定資料夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)。<br>如果透過資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;套用預設集，則可以為多個資料夾指派指定的批次集預設集。 請參閱[從資產資料夾的「屬性」頁面](#apply-bsp-to-folders-via-properties)套用批次集預設集。<br>如果您未指定資料夾，批次集預設集產生的影像集或迴轉集會建立在與您上傳至的資產資料夾相同的資料夾中。 |
| **[!UICONTROL 設定命名慣例]** |  |
| 前置詞<br>或<br>後置詞 | 選擇性。在個別欄位中輸入字首、字尾或兩者。<br>字首與字尾欄位可讓您使用特定內容集的替代自訂檔案命名慣例，建立許多批次集預設集。 在公司定義的預設命名配置有例外的情況下，此方法特別有用。<br>前置詞或尾碼已新增至您在&#x200B;**[!UICONTROL 資產命名慣例]**&#x200B;區域中定義的&#x200B;**[!UICONTROL 基底名稱]**。 新增首碼或尾碼可確保您的影像集或迴轉集是獨立於其他資產以獨佔方式建立的。 它也可以進一步協助其他人識別檔案型別。 例如，若要判斷所使用的色彩模式，您可以新增做為字首或字尾`rgb`或`cmyk`。<br>雖然使用批次集預設集功能不需要指定集合命名慣例，但最佳實務建議您使用集合命名慣例。 此作法可讓您定義要分組在集合中的命名慣例元素，以協助簡化批次集合的建立。 |
| **[!UICONTROL 規則結果 — RegX]** |  |
| 資產命名慣例 — 相符 | 唯讀。 根據您選擇的「符合」表單選項或您輸入的原始程式碼顯示規則運算式語法。 |
| 資產命名慣例 — 基本名稱 | 唯讀。 根據您選擇的「基本名稱」表單選項或您輸入的原始程式碼顯示規則運算式語法。 |
| 序列順序 — 相符 | 唯讀。 根據您選擇的表單選項或您輸入的原始程式碼顯示規則運算式語法。 |

## 關於將批次集預設集套用至資產資料夾 {#apply-bsp}

將批次集預設集指派給一個或多個資產資料夾時，任何子資料夾都會自動從其父資料夾繼承預設集。

您可以將多個批次集預設集套用至資產資料夾。

在&#x200B;**[!UICONTROL 卡片]**&#x200B;檢視中，資料夾內所顯示預設集名稱的使用者介面中，會指出已指派批次預設集的資料夾。

若要將批次集預設集套用至資產資料夾，請使用下列兩種方法之一：

* [從批次集預設集頁面將批次集預設集套用至資產資料夾](#apply-bsp-to-folders-via-bsp-page) — 此方法為您提供最大的彈性。 您可以將單一預設集或多個預設集套用至單一資料夾或多個資料夾。
* [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties) — 此方法可讓您將一個或多個批次集預設集套用至單一資料夾。

最佳做法是確認資產資料夾已同步[!DNL Dynamic Media]，然後套用您想要的預設集。

如果您遇到以下兩種情況之一，請重新處理資料夾中的資產：

* 您想要對已上傳資產的現有資產資料夾執行批次集預設集。
* 您稍後會編輯先前套用至資產資料夾的現有批次集預設集。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 從批次集預設集頁面將批次集預設集套用至資產資料夾 {#apply-bsp-to-folders-via-bsp-page}

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄的左側，選取您要套用至資料夾的每個批次集預設集核取方塊。
1. 在工具列中選取&#x200B;**[!UICONTROL 套用批次預設集至資料夾]**。
1. 在&#x200B;**[!UICONTROL 選取資料夾]**&#x200B;頁面上，選取要套用批次集預設集的每個資料夾的核取方塊。
1. 在&#x200B;**[!UICONTROL 選取資料夾]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 套用]**。

### 從資產資料夾的「屬性」頁面套用批次集預設集 {#apply-bsp-to-folders-via-properties}

1. 選取Experience Manager標誌，並前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 導覽至您要套用一或多個批次集預設集的資料夾。
1. 在頁面的&#x200B;**[!UICONTROL Name]**&#x200B;欄左側，選取資料夾的核取方塊。
1. 在工具列中選取&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的「屬性」頁面上，選取「**[!UICONTROL 動態媒體處理]**」標籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;下，從&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉式清單方塊中，選取您要套用的批次集預設集名稱。 上方的熒幕擷圖顯示套用至資產資料夾的兩個所選批次集預設集。

   如果&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;下拉式清單方塊中沒有批次集預設集名稱，表示您尚未建立任何批次集預設集。 請參閱[為影像集或迴轉集建立批次集預設集](#creating-bsp)。

   若要移除套用的批次集預設集，請選取預設集型別右側的&#x200B;**[!UICONTROL X]**。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。

## 編輯批次集預設集 {#edit-bsp}

您可以編輯已建立的現有批次集預設集。 您可以變更任何您為資產命名慣例或序列順序建立的運算式群組。 如有需要，您也可以更新目的地資料夾並設定命名慣例。

但是，您無法變更預設集的名稱或預設集型別（「影像集」或「迴轉集」）。 如果必須變更預設集的名稱，請複製現有預設集並指定新名稱。 請參閱[複製批次集預設集](#copy-bsp)。

如果您編輯先前套用至資料夾的批次集預設集，新編輯的批次集預設集只會套用至上傳至該資料夾的新資產。

如果您要將新編輯的預設集重新套用至資料夾中的現有資產，則必須重新處理資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->如此一來，現有資產將符合影像集或迴轉集的一部分資格並加入。 此外，已包含於影像集或迴轉集的現有資產（根據先前使用的批次集預設集）並未移除，而是按原樣顯示。 此情境假設他們不再符合新編輯的預設集的資格。

**若要編輯批次集預設集：**

1. 選取Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄的左側，檢查您要變更的批次集預設集。
1. 在工具列中選取&#x200B;**[!UICONTROL 編輯批次集預設集]**。
1. 視需要編輯預設集。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。

## 複製現有的批次集預設集 {#copy-bsp}

您可以複製現有的批次集預設集，以避免手動重新建立複雜的預設集，或您只是想重新命名預設集。 不過，您無法變更所使用的預設集型別（影像集或迴轉集）。

如果您複製資產資料夾所參照的現有預設集，這些資料夾將不受影響。

**複製現有的批次集預設集：**

1. 選取Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄的左側，選取您要複製的批次集預設集核取方塊。
1. 在工具列中選取&#x200B;**[!UICONTROL 複製]**。
1. 在「**[!UICONTROL 複製批次集預設集]**」對話方塊的「**[!UICONTROL 標題]**」文字方塊中，輸入預設集的新名稱。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 選取&#x200B;**[!UICONTROL 複製]**。

## 關於從資料夾中移除批次集預設集 {#remove-bsp-from-folder}

當您從資料夾中移除批次集預設集時，您上傳到這些資料夾的任何新資產都不會套用批次集預設集。 資料夾中已新增至影像集的現有資產，或根據套用至資料夾的批次集預設集以列印集為基礎的現有資產 — 繼續按原樣顯示。

如果您想要&#x200B;*從資料夾刪除*&#x200B;預設集，請參閱[刪除批次集預設集](#delete-bsp)。

您可以使用兩種方法從資料夾中移除批次集預設集。

* [透過批次集預設集頁面](#remove-bsp-from-folders-via-bsp-page)從資料夾中移除批次集預設集 — 此方法為您提供最大的彈性。 您可以從單一資料夾或多個資料夾中移除單一預設集或多個預設集。
* [從資料夾的[內容]頁面移除批次集預設集](#remove-bsp-from-folders-via-properties) — 此方法可讓您僅從單一資料夾移除一或多個批次集預設集。

### 透過「批次集預設集」頁面，從資料夾中移除批次集預設集 {#remove-bsp-from-folders-via-bsp-page}

1. 選取Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄的左側，選取一或多個批次集預設集的核取方塊，以從一或多個資料夾中移除這些預設集。
1. 在工具列中選取&#x200B;**[!UICONTROL 從資料夾移除批次預設集]**。

1. 在&#x200B;**[!UICONTROL 選取資料夾]**&#x200B;頁面上，選取一或多個要移除批次集預設集的資料夾。
1. 在&#x200B;**[!UICONTROL 選取資料夾]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 移除]**。

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在&#x200B;**[!UICONTROL 移除設定檔]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 移除]**。

### 從資料夾的「屬性」頁面移除批次集預設集 {#remove-bsp-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 導覽至您要移除一或多個批次集預設集的資料夾。
1. 在頁面的&#x200B;**[!UICONTROL Name]**&#x200B;欄左側，選取資料夾的核取方塊。
1. 在工具列中選取&#x200B;**[!UICONTROL 屬性]**。
1. 在資料夾的[內容]頁面上，選取[**[!UICONTROL 動態媒體處理]**]。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;下，選取預設集型別右側的&#x200B;**[!UICONTROL X]**。

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**。

## 刪除批次集預設集 {#delete-bsp}

您可以刪除批次集預設集，以從[!DNL Dynamic Media]中永久移除它們。 也就是說，這些預設集不再顯示在[!UICONTROL 批次集預設集]頁面上，也不會顯示在資料夾&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面上&#x200B;**[!UICONTROL Dynamic Media處理]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;下拉式清單中。 因此，在資料夾重新處理或新資產上傳至資料夾時，預設集不會套用至現有資產。

如果您刪除先前套用至一或多個資料夾的預設集，則從這些資料夾中的資產建立的任何影像集或迴轉集都會繼續按原樣顯示。

如果您想要&#x200B;*從資料夾移除*&#x200B;預設集，請參閱[從資料夾移除批次集預設集](#remove-bsp-from-folder)。

**若要刪除批次集預設集：**

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 批次集預設集]**。
1. 在&#x200B;**[!UICONTROL 批次集預設集]**&#x200B;頁面的&#x200B;**[!UICONTROL 預設集名稱]**&#x200B;欄的左側，選取一或多個要刪除的批次集預設集核取方塊。
1. 在工具列中選取&#x200B;**[!UICONTROL 刪除批次集預設集]**。

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在&#x200B;**[!UICONTROL 刪除批次集預設集]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 刪除]**。

   如果您要刪除的預設集已由資產資料夾參考，請改為選取「強制刪除」****。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [影像集](/help/assets/dynamic-media/image-sets.md)
>* [迴轉集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media中設定資料夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) — 如果您想深入瞭解將單一資料夾同步至[!DNL Dynamic Media]的相關資訊，請參閱主題中的「同步模式」。
>* [在Cloud Services中建立Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) — 如果您想深入瞭解將所有資料夾同步至[!DNL Dynamic Media]，請參閱主題中的「Dynamic Media同步模式」。
