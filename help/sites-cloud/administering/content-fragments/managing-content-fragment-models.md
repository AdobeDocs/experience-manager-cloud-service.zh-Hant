---
title: 管理內容片段模型
description: 瞭解如何管理內容片段模型；這些模型可作為您在AEM中內容片段的基礎，讓您建立結構化內容以用於Headless傳送或頁面編寫。
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: f94f75c2-12fa-47c0-a71b-327f4210077d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 3%

---

# 管理內容片段模型 {#managing-content-fragment-models}

您可以從內容片段主控台管理內容片段模型，然後[開啟編輯器](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)以定義結構。

Adobe Experience Manager (AEM) as a Cloud Service中的內容片段模型定義[內容片段](/help/sites-cloud/administering/content-fragments/overview.md)的內容結構。 然後，這些片段就可以用作Headless內容或頁面編寫的基礎。

>[!NOTE]
>
>此頁面涵蓋（僅）顯示內容片段模式的控制檯區段。 如需其他面板，請參閱：
>
>* [管理內容片段](/help/sites-cloud/administering/content-fragments/managing.md)
>* [在內容片段主控台中檢視和管理Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

>[!NOTE]
>
>內容片段儲存為&#x200B;**Assets**。 內容片段模型主要是從&#x200B;**內容片段**&#x200B;主控台進行管理，但也可以從[Assets](/help/assets/content-fragments/content-fragments-managing.md)主控台以及選項[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) （可從&#x200B;**工具** - **一般**&#x200B;使用）進行管理。

## 如何使用內容片段模型 {#how-to-work-with-content-fragment-models}

作為快速概覽，若要使用內容片段模型，您：

1. [為您的執行個體啟用內容片段模型功能](/help/sites-cloud/administering/content-fragments/setup.md)
1. [建立](#creating-a-content-fragment-model)您的內容片段模式。
   * 此時您也可以&#x200B;**啟用**&#x200B;模型（供建立內容片段時使用）。
1. [定義](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#defining-your-content-fragment-model)您模型的結構。
1. [啟用您的內容片段模型](#enabling-a-content-fragment-model) （如果尚未完成）。
1. [藉由設定](#allowing-content-fragment-models-assets-folder)原則&#x200B;**，在必要的Assets資料夾**&#x200B;上允許您的內容片段模型。

## 在主控台中內容片段模式的基本結構和處理 {#basic-structure-handling-content-fragment-models-console}

您可以使用[內容片段主控台](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)最左側的面板，選取&#x200B;**內容片段模式**&#x200B;作為資源型別來檢視、瀏覽及管理：

![內容片段主控台 — 導覽](/help/sites-cloud/administering/content-fragments/assets/cf-console-models-navigation.png)

這將開啟內容片段模型的檢視：

![內容片段主控台 — 管理內容片段模型](assets/cf-managing-content-fragment-models.png)

您可以看到有三個主要區域：

* 頂端工具列
   * 提供標準AEM功能
   * 顯示您的IMS組織
   * 提供各種[動作](#actions-unselected)，當您選取一或多個模型時，這些動作可[變更](#actions-selected-content-fragment-models)
* 左側面板
   * 顯示所有組態的[路徑](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)列示為資料夾
   * 您可以在此隱藏或顯示資料夾樹狀結構
   * 您可以選取樹狀結構的特定資料夾
   * 這可以調整大小以顯示巢狀資料夾（子設定）
   * 除了內容片段模型之外，您也可以檢視[內容片段](/help/sites-cloud/administering/content-fragments/managing.md)或[Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)；您也可以壓縮或展開面板的連結
* 主要/右側面板 — 從這裡，您可以：
   * 檢視在所選資料夾下儲存的所有內容片段模型清單：
      * 所選資料夾的內容片段模型和所有子資料夾都會顯示：
         * 階層連結會指出位置，也可用來變更位置：
      * [顯示有關每個模型的資訊](#information-content-fragment-models)
         * [您可以選取要顯示哪些欄](#select-columns-console)
      * [內容片段模型的各種資訊欄位](#information-content-fragment-models)會提供連結；視欄位而定，這些連結可以：
         * 在編輯器中開啟適當的模型
         * 顯示設定路徑的相關資訊
         * 顯示模型狀態的相關資訊
      * [某些其他資訊欄位](#information-content-fragments)關於內容片段模型可用於[快速篩選](#fast-filtering)：
         * 在欄中選取值，該值會立即套用為篩選器
         * **Modified By**、**Published By**&#x200B;和&#x200B;**Status**&#x200B;資料行支援快速篩選。
      * 在欄標題上使用滑鼠游標時，下拉式動作選擇器和寬度滑桿隨即顯示。 這些功能可讓您：
         * 排序 — 以遞增或遞減方式選取適當的動作
這會根據該欄排序整個表格。 排序功能只適用於適當的欄。
         * 調整欄大小 — 使用動作或寬度滑桿
      * 選取一個或多個模型以進一步執行[動作](#actions-selected-content-fragment-models)
   * 開啟[篩選器面板](#filter-content-fragment-models)
   * 您可以在此主控台中使用一組[鍵盤快速鍵](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md)

## 提供的有關您的內容片段模式的資訊 {#information-content-fragment-models}

主控台的主/右側面板（表格檢視）提供一系列有關您的內容片段模式的資訊。 有些專案也會提供進一步動作和/或資訊的直接連結：

* **名稱**
   * 提供在編輯器中開啟模型的連結。
* **已鎖定** （掛鎖圖示）
   * 當模型鎖定時，會以掛鎖圖示表示。
* **路徑**
   * 提供路徑作為連結，以在主控台中開啟設定。
將游標停留在資料夾名稱上將顯示 JCR 路徑。
* **狀態**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)
* **復寫狀態**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)。
* **預覽**
   * 僅供參考。
* **修改於**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)。
* **修改者**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)。
* **標籤**
   * 僅供參考。
   * 開啟對話方塊，顯示與模型相關的所有標籤。
   * 可用於[快速篩選](#fast-filtering)。
* **發佈於**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)。
* **發佈者**
   * 僅供參考。
   * 可用於[快速篩選](#fast-filtering)。
* **由**&#x200B;使用
   * 開啟對話方塊，其中列出以模式為基礎的內容片段。 清單提供可讓您直接開啟片段的連結。

## 模型屬性 {#model-properties}

當您選取特定模型時，會顯示該模型的屬性（如[建立模型](#creating-a-content-fragment-model)時所定義）。 如果模型不是&#x200B;**鎖定**，則可以更新某些專案。 您也可以使用資訊圖示（在模型&#x200B;**Title**&#x200B;旁）來開啟及關閉此資訊面板。

![內容片段主控台 — 所選內容片段模式的資訊](assets/cf-managing-content-fragment-models-selected.png)

* **[路徑](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)**
* **[狀態](#enabling-a-content-fragment-model)**
* **標題**
* **標籤**
* **說明**
* **[預覽URL模式](/help/sites-cloud/administering/content-fragments/preview.md#preview-url-pattern)**

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## 動作 {#actions}

選取資料夾（在左側面板中）後，您就可以直接或選取特定模型後，使用一系列動作：

* 可以從主控台[直接使用各種動作](#actions-unselected)
* 您可以[選取一或多個內容片段模型以顯示適當的動作](#actions-selected-content-fragment)

### 動作（未選取） {#actions-unselected}

在選取資料夾後，但未選取特定內容片段模式時，可以從主控台使用某些動作：

* **[建立](#creating-a-content-fragment-model)**&#x200B;新的（空白）模型

### 內容片段控制檯中內容片段模型的動作 {#actions-selected-content-fragment-models}

選取特定模型會開啟一個工具列，其焦點是該模型可用的動作。 您也可以選取多個模型 — 可用的動作會相應調整。

* **[編輯](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)**&#x200B;以定義您的內容片段模式。
* **[發佈](#publishing-a-content-fragment-model)**&#x200B;和&#x200B;**[取消發佈](#unpublishing-a-content-fragment-model)**&#x200B;到[發佈](/help/implementing/cloud-manager/manage-environments.md#environment-types)或[預覽](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)層。
* **鎖定**/**解除鎖定**&#x200B;以控制是否允許使用者修改模型。
* **複製**&#x200B;您的模型。
* **[啟用](#enabling-a-content-fragment-model)**/**[停用](#disabling-a-content-fragment-model)**&#x200B;以控制是否允許使用者根據此模型建立內容片段。

選取單一模型也會在右側面板中顯示[模型屬性](#properties)。

## 選取主控台中顯示的欄 {#select-columns-console}

與其他主控台一樣，您可以設定可見且可動作的欄：

![內容片段主控台 — 資料行設定](assets/cf-managing-console-column-icon.png)

這會顯示您可以隱藏或顯示的欄清單：

![內容片段主控台 — 資料行設定](assets/cf-managing-content-fragment-models-column-selection.png)

## 篩選內容片段模型 {#filter-content-fragment-models}

「篩選器」面板提供：

* 述詞選擇；
   * 包括狀態列位、標籤、使用者等
   * 可以選取並組合一個或多個述詞來建立篩選器

<!--
* the opportunity to **Save** your filter
* the option to retrieve a saved search filter for reuse
-->

選取後，會顯示&#x200B;**篩選依據**&#x200B;選項（在主面板頂端）。 可以從那裡取消選取它們。 例如：

![內容片段主控台 — 篩選內容片段模型](assets/cf-managing-content-fragment-models-filter.png)

### 快速篩選 {#fast-filtering}

您也可以按一下清單中的特定欄值來選取述詞。 您可以選取一或多個值來組合述詞。

例如，在&#x200B;**狀態**&#x200B;欄中選取&#x200B;**已啟用**。 選取後，將顯示為篩選述詞，清單將據此篩選。

>[!NOTE]
>
>僅支援&#x200B;**狀態**、**修改者**、**標籤**&#x200B;和&#x200B;**發佈者**&#x200B;資料行的快速篩選。

>[!NOTE]
>
>快速篩選的運作方式與主控台中的[內容片段](/help/sites-cloud/administering/content-fragments/managing.md#fast-filtering)相同。

## 建立內容片段模型 {#creating-a-content-fragment-model}

1. 導覽至適合您[組態或子組態](/help/sites-cloud/administering/content-fragments/setup.md)的資料夾。
1. 使用&#x200B;**建立**&#x200B;開啟對話方塊。

   >[!CAUTION]
   >
   >**Create**&#x200B;選項僅供使用：
   >
   >* 如果已啟用[使用內容片段模型](/help/sites-cloud/administering/content-fragments/setup.md)
   >* 當您選取要建立模型的資料夾時。

1. 選取組態的&#x200B;**路徑**&#x200B;並指定&#x200B;**名稱**。

   >[!NOTE]
   >
   >設定會自動填入目前的設定（您目前所在的資料夾）。
   >
   >您也可以按一下資料夾圖示來變更設定。

   您也可以定義各種屬性：

   * **標題**
如果您先輸入&#x200B;**Title**，則會從該標題產生&#x200B;**Name**。
   * **描述**
   * **啟用模型**&#x200B;以[啟用模型](#enabling-disabling-a-content-fragment-model)

   >[!NOTE]
   >
   >如需完整詳細資訊，請參閱[內容片段模式 — 屬性](#model-properties)。

   ![標題和說明](assets/cf-managing-content-fragment-models-create.png)

1. 使用「**建立**」來儲存空模型，或選擇「**建立並開啟**」。

### 啟用內容片段模型 {#enabling-a-content-fragment-model}

建立模型後，必須將其啟用，以便：

* 可在建立內容片段時選擇。
* 可在內容片段模型中參考。
* 可供GraphQL使用，因此會產生結構描述。

您可以&#x200B;**啟用**&#x200B;模型：

* 建立新模型時
   * 對話方塊中會顯示一個選項。
* 模型已特別停用&#x200B;**時**
   * 選取必要的「模型」時，頂端工具列中會顯示&#x200B;**啟用**&#x200B;動作。

### 停用內容片段模型 {#disabling-a-content-fragment-model}

也可以停用模型，以便：

* 此模型無法再用來建立&#x200B;*新的*&#x200B;內容片段。
* 但是：
   * GraphQL結構描述會持續產生，且仍可查詢（以避免影響JSON API）。
   * 您仍可以從GraphQL端點查詢及傳回任何以模型為基礎的內容片段。
* 該模型無法再參考，但現有參考將保持不變，並且仍可以從GraphQL端點查詢和返回。

若要停用標示為&#x200B;**已啟用**&#x200B;的模型，您可以使用下列專案中的&#x200B;**停用**&#x200B;選項：

* 當選取所需的「模型」時，頂部工具列。

## 允許資產資料夾中的內容片段模型 {#allowing-content-fragment-models-assets-folder}

若要實作內容控管，您可以在Assets資料夾上設定&#x200B;**原則**，以控制允許在該資料夾中建立片段的內容片段模型。

>[!NOTE]
>
>此機制類似於[允許在頁面的進階屬性中，為頁面及其子頁面設定頁面範本](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author)。

若要為&#x200B;**允許的內容片段模型**&#x200B;設定&#x200B;**原則**：

1. 瀏覽並開啟必要的Assets資料夾的&#x200B;**屬性**。

1. 開啟&#x200B;**原則**&#x200B;標籤，您可以在其中設定：

   * **繼承自`<folder>`**

     建立新的子資料夾時，會自動繼承原則；如果子資料夾需要允許與父資料夾不同的模型，則可以重新設定原則（並中斷繼承）。

   * **允許的內容片段模型（依路徑**）

     可允許多個模型。

   * **允許的內容片段模型（依標籤）**

     可允許多個模型。

   ![內容片段模型原則](assets/cf-cfmodels-policy-assets-folder.png)

1. **儲存**&#x200B;任何變更。

允許用於資料夾的內容片段模型的解析如下：

* **允許的內容片段模型**&#x200B;的&#x200B;**原則**。
* 如果空白，請嘗試使用繼承規則來決定原則。
* 如果繼承鏈結未傳遞結果，請檢視該資料夾的&#x200B;**雲端服務**&#x200B;設定（也請先直接再透過繼承）。
* 如果以上所有內容均未提供任何結果，則該資料夾不允許使用模型。

## 刪除內容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>刪除內容片段模型可能會影響相依片段。

若要刪除內容片段模型：

1. 導覽至並選取您的內容片段模式。 您可以選取多個模型。

1. 從工具列選取&#x200B;**刪除**。

   >[!NOTE]
   >
   >如果參照模型，則會發出警告，以便您採取適當的動作。

## 發佈內容片段模型 {#publishing-a-content-fragment-model}

發佈任何相依內容片段時/之前，需要發佈內容片段模型。

若要發佈內容片段模型：

1. 導覽至並選取您的內容片段模式。 您可以選取多個模型。

1. 從工具列選取&#x200B;**發佈**。

1. 在[發佈]對話方塊中，選取&#x200B;**目的地**：

   * **發佈服務**
   * **預覽服務**

1. 將啟動發佈所選模型及其參照的工作流程。 然後，已發佈狀態會顯示在主控台中。

## 取消發佈內容片段模型 {#unpublishing-a-content-fragment-model}

如果內容片段模型未由任何片段參考，則可取消發佈這些模型。

若要取消發佈內容片段模型：

1. 導覽至並選取您的內容片段模式。
主控台會指出發佈狀態。

1. 從工具列選取&#x200B;**取消發佈**。

1. 在取消發佈對話方塊中，選取&#x200B;**目的地**：

   * **發佈服務**
   * **預覽服務**

1. 將啟動取消發佈所選模型及其參照的工作流程。 然後，主控台中會顯示未發佈狀態。

如果您嘗試取消發佈一個或多個片段目前使用的模型，則會顯示錯誤警告。 此訊息建議您檢查[參考](/help/sites-cloud/authoring/basic-handling.md#references)面板以進一步調查：

## 鎖定的內容片段模型 {#locked-content-fragment-models}

此功能可讓您控制模型是否可以更新，但也為已發佈的內容片段模型提供控管。

### 挑戰 {#the-challenge}

* 內容片段模型決定AEM中GraphQL查詢的結構描述。

   * AEM GraphQL結構描述會在建立內容片段模型後立即建立，且可同時存在於製作和發佈環境中。

   * 發佈上的結構描述最為關鍵，因為它們為JSON格式的內容片段內容的即時傳送奠定了基礎。

* 修改內容片段模型或編輯內容片段模型時，可能會出現問題。 這表示結構描述變更，進而可能影響現有的GraphQL查詢。

* 將新欄位新增到內容片段模式通常不應有任何有害影響。 但是，修改現有資料欄位（例如，其名稱）或刪除欄位定義時，將會在請求這些欄位時中斷現有GraphQL查詢。

### 需求 {#the-requirements}

* 讓使用者瞭解在編輯已用於即時內容傳送的模型（即已發佈的模型）時的風險。

* 此外，也可避免非預期的變更。

如果修改後的模型重新發佈，則其中任何一個條件都可能中斷查詢。

### 解決方案 {#the-solution}

為了解決這些問題，內容片段模型在發佈後立即在作者上&#x200B;*鎖定*&#x200B;為唯讀模式。 **已鎖定**&#x200B;表示此狀態。

當模型為&#x200B;**鎖定** （在「唯讀」模式中）時，您可以檢視模型的內容和結構，但無法進行編輯。

您可以從主控台或模型編輯器管理&#x200B;**已鎖定的**&#x200B;模型：

* 主控台

  從主控台，您可以使用工具列中的&#x200B;**解除鎖定**&#x200B;和&#x200B;**鎖定**&#x200B;動作來管理唯讀模式。

   * 您可以&#x200B;**解鎖**&#x200B;模型以啟用編輯。

     如果您選取&#x200B;**解除鎖定**，會顯示警告，而且您必須確認&#x200B;**解除鎖定**&#x200B;動作。

     然後您可以開啟模型以進行編輯。

   * 您之後也可以&#x200B;**鎖定**&#x200B;模型。
   * 重新發佈模型會立即將其傳回&#x200B;**鎖定** （唯讀）模式。

* 模型編輯器

   * 當您開啟已鎖定的模型時，系統會警告您，並顯示三個動作： **取消**、**檢視唯讀**、**編輯**。

   * 若您選取&#x200B;**檢視唯讀**，即可檢視模型的內容和結構。

   * 如果您選取&#x200B;**編輯**，您可以編輯並儲存您的更新：

     ![編輯 — 鎖定的內容片段模型](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     >頂端可能仍會顯示警告，但此時模型已由現有內容片段使用。

   * **取消**&#x200B;會帶您返回主控台。
