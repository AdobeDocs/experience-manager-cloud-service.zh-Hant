---
title: 建立頁面範本
description: 範本會定義產生頁面的結構，而使用範本編輯器，建立和維護範本不再是僅限開發人員的工作
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '4551'
ht-degree: 11%

---


# 建立頁面範本 {#creating-page-templates}

建立頁面時，您必須選取範本，此範本將用作建立新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容，以及可使用的元件。

使用范 **本編輯器**，建立和維護範本不再是開發人員專屬的工作。也可以涉及一種稱為模板作 **者的權**&#x200B;力用戶。開發人員仍需要設定環境、建立用戶端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。****

範本控 **制台(Templates Console** )可讓範本作者：

* 建立新範本或複製現有範本。
* 管理模板的生命週期。

範本編 **輯器** (Template Editor)允許範本作者：

* 將元件新增至範本，並將它們置於互動式格線上。
* 預先設定元件。
* 定義哪些元件可在使用範本建立的頁面上編輯。

本檔案說明範本作 **者如何使用範本** 主控台和編輯器來建立和管理可編輯的範本。

如需可編輯範本在技術層級運作的詳細資訊，請參閱開發人員檔案頁面範本 [](/help/implementing/developing/components/templates.md) ，以取得詳細資訊。

>[!NOTE]
>
>范 **** 本編輯器不支援直接在範本層級定位。可以定位根據可編輯的範本建立的頁面，但無法定位範本本身。

## 開始之前 {#before-you-start}

>[!NOTE]
>
>管理員必須在「配置瀏覽器」中配置模板檔案 **夾** ，並應用適當的權限，模板作者才能在該資料夾中建立模板。

在您開始之前，請務必考慮建立新範本需要共同作業。 因此，會為每 [個任務指](#roles) 定「角色」。 這不會影響您實際使用範本建立頁面的方式，但會影響頁面與其範本的關聯方式。

### 角色 {#roles}

使用「模板控制台」和「模 **板編輯器** 」建立新模板時 **** ，需要在以下角色之間協作：

* **管理員**:
   * 為需要權限的模板建立新文 `admin` 件夾。
   * 這類工作通常也可由開發人員完成
* **開發人員**:
   * 重點介紹技術／內部細節
   * 需要開發環境的經驗。
   * 提供範本作者必要的資訊。
* **範本作者**:
   * 此為群組成員的特定作者 `template-authors`
      * 這會分配所需的權限和權限。
   * 可以配置元件的使用和其他需要的高級詳細資訊：
      * 一些技術知識
         * 例如，在定義路徑時使用圖樣。
      * 開發人員的技術資訊。

由於某些任務的性質（如建立資料夾），因此需要開發環境，這需要知識／經驗。

本文檔中詳述的任務將列出負責執行這些任務的角色。

## 建立和管理模板 {#creating-and-managing-templates}

建立新的可編輯範本時：

* 使用范 **本控** 制台。 這可在「工具」( **Tools** )控制台的「一 **般」(General** )部分中使用。
   * 或直接在： `https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* 可 [以為模板建立資料夾](#creating-a-template-folder-admin) （如果需要）
* [建立新範本](#creating-a-new-template-template-author)，此範本一開始會是空的
* [視需要為範本定義其他屬性](#defining-template-properties-template-author) ,
* [編輯範本](#editing-templates-template-authors) ，以定義：
   * [結構](#editing-a-template-structure-template-author) -在使用範本建立的頁面上，無法變更的預先定義內容。
   * [初始內容](#editing-a-template-initial-content-author) -可在使用範本建立之頁面上變更的預先定義內容。
   * [版面](#editing-a-template-layout-template-author) -適用於各種裝置。
   * [樣式](/help/sites-cloud/authoring/features/style-system.md) -定義要與範本及其元件一起使用的樣式。
* [啟用範本](#enabling-a-template-template-author) ，以便在建立頁面時使用
* [允許您網站](#allowing-a-template-author) 所需頁面或分支的範本
* [發佈範本](#publishing-a-template-template-author) ，使其可在發佈環境中使用

>[!NOTE]
>
>「允 **許的範本** 」通常會在網站初次設定時預先定義。

>[!CAUTION]
>
>切勿將任何需要國際化的資訊輸入到模板中。 <!-- Never enter any information that needs to be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>對於必須本地化的範本元素（例如頁首和頁尾），請運用核 [心元件的本地化功能。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/localization.html)

### 建立範本資料夾——管理員 {#creating-a-template-folder-admin}

應為您的專案建立範本資料夾，以存放專案專用的範本。 這是一項管理任務，在文檔「頁面模板」中 [有說明](/help/implementing/developing/components/templates.md#template-folders)。—>

### 建立新範本——範本作者 {#creating-a-new-template-template-author}

1. 開啟范 **本主控台** (透過工具-> **一** 般 ****)，然後導覽至所需的檔案夾。

   >[!NOTE]
   >
   >在標準AEM例項中，范 **本主控台中** ，已有全域資料夾存在。 如果當前資料夾中未找到策略和／或模板類型，則此選項將保留預設模板並充當備援。
   >
   >建議使用為專案建立的范 [本資料夾，這是最佳實務](/help/implementing/developing/components/templates.md#template-folders)。

1. 選擇 **建立**，然後選 **擇建立模板** ，以開啟嚮導。

1. 選擇「模 **板類型**」，然後選擇「 **下一步」**。

   >[!NOTE]
   >
   >範本類型是預先定義的範本版面，可視為範本的範本。 這些是由開發人員或系統管理員預先定義的。 如需詳細資訊，請參閱開發人員檔案 [頁面範本](/help/implementing/developing/components/templates.md#template-type)。—>

1. 完成范 **本詳細資訊**:

   * **範本名稱**
   * **說明**

1. 選擇 **建立**。將顯示確認資訊，選擇「 **Open** 」（開啟）開始編輯模板，或選擇「 **Done** 」（完成）返回模板控制台。

   >[!NOTE]
   >
   >當建立新範本時，在主控台中會將其標示為 **Draft** ，這表示該範本尚未可供頁面作者使用。

### 定義模板屬性——模板作者 {#defining-template-properties-template-author}

範本可以有下列屬性：

* 影像
   * 影像將用作範本 [的縮圖](#template-thumbnail-image) ，以協助選取，例如在「建立頁面」精靈中。
      * 可上傳
      * 可根據範本內容產生
* 標題
   * 用於標識模板的標題，如在「建立頁 **面」嚮導中** 。
* 說明
   * 提供範本及其使用的詳細資訊的選用說明，例如在「建立頁面」精靈中 **可看到** 。

要查看和／或編輯屬性：

1. 在「範本 **控制台**」中，選取範本。
1. 從工 **具欄中選擇** 「查看屬性」(View Properties)或快速選項以開啟對話框。
1. 您現在可以檢視或編輯範本屬性。

>[!NOTE]
>
>控制台會指出範本的狀態（草稿、啟用或停用）。

#### 範本縮圖影像 {#template-thumbnail-image}

要定義模板縮覽圖，請執行以下操作：

1. 編輯範本屬性。
1. 選擇您要上傳縮圖或是從範本內容產生縮圖。
   * 如果您想要上傳縮圖，請按一下或點選「上傳影 **像」。**
   * 如果您想要產生縮圖，請按一下或點選「產生預 **覽」**
1. 對於這兩種方法，都會顯示縮圖的預覽。
   * 如果不滿意，請按一下或點選「清 **除」** ，上傳其他影像或重新產生縮圖。
1. 當您對縮圖滿意時，按一下或點選「儲 **存並關閉」**。

### 啟用和允許範本——範本作者 {#enabling-and-allowing-a-template-template-author}

若要在建立頁面時能夠使用範本，您必須：

* [啟用範本](#enabling-a-template-template-author) ，讓範本在建立頁面時可供使用。
* [允許範本](#allowing-a-template-author) ，指定可使用範本的內容分支。

#### 啟用範本——範本作者 {#enabling-a-template-template-author}

範本可以啟用或停用，以便在「建立頁面」精靈中提供或 **無法使用** 。

>[!CAUTION]
>
>當範本啟用後，當範本作者開始進一步更新範本時，將會顯示警告。 這是為了通知使用者範本可能被參考，因此任何變更都可能會影響參考範本的頁面。

1. 在「範本 **控制台**」中，選取範本。
1. 從工 **具列中選** 擇「啟用 **」或「停用** 」，然後在確認對話方塊中再次選擇。
1. 您現在可以在建立新頁 [面時使用範本](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)，不過您可能會想 [要根據需求編輯範本](#editing-templates-template-authors) 。

>[!NOTE]
>
>控制台會指出範本的狀態（草稿、啟用或停用）。

#### 允許範本——作者 {#allowing-a-template-author}

範本可供某些頁面分支使用或無法使用。

1. 開啟 [](/help/sites-cloud/authoring/fundamentals/page-properties.md) 您要範本可用之分支之根頁面的頁面屬性。
1. 開啟「進 **階** 」標籤。
1. 在「 **範本設定** 」下 **，使用「新增」欄位** ，指定範本的路徑。

   路徑可以是明確的或使用模式。 例如：

   `/conf/<your-folder>/settings/wcm/templates/.*`

   路徑順序不相關，所有路徑都將被掃描，並檢索任何模板。

   >[!NOTE]
   >
   >如果「允 **許的模板** 」清單為空，則樹將被提升，直到找到值／清單。
   >
   >
   >請參 [閱範本可用性](/help/implementing/developing/components/templates.md#template-availability) -允許範本的原則保持不變。

1. 按一 **下「儲存** 」以儲存對頁面屬性所做的變更。

>[!NOTE]
>
>通常允許的範本會在設定時預先定義給整個網站。

### 發佈範本——範本作者 {#publishing-a-template-template-author}

當轉譯頁面時參考範本時，必須發佈已完全設定的範本，以便在發佈環境中使用。

1. 在「範本 **控制台**」中，選取範本。
1. Select **Publish** from the toolbar to open the wizard.
1. 選取 **要同時發佈的** 「內容原則」。
1. 從工 **具列選擇** 「發佈」(Publish)以完成動作。

## 編輯範本——範本作者 {#editing-templates-template-authors}

建立或編輯範本時，您可以定義多個方面。 編輯範本類似於頁面製作。

工具 **列中的** 「模式選取器」(Mode selector)可讓您選取並編輯範本的適當方面：

* [結構](#editing-a-template-structure-template-author)
* [初始內容](#editing-a-template-initial-content-author)
* [配置](#editing-a-template-layout-template-author)

![範本編輯器模式選擇器](/help/sites-cloud/authoring/assets/templates-mode.png)

雖然「頁 **面資訊** 」功能表上的「頁面原則」選 **項可讓您選** 取所需的頁面原則 [](#page-policies):

![範本編輯器頁面資訊](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>如果作者開始編輯已啟用的範本，將會顯示警告。 這是為了通知使用者範本可能被參考，因此任何變更都可能會影響參考範本的頁面。

### 範本屬性 {#template-attributes}

可以編輯模板的以下屬性：

#### 結構 {#template-structure}

添加到結構 [的元件](#editing-a-template-structure-template-author) ，不能由頁面作者從結果頁面中移動／刪除。 如果您希望頁面作者能夠將元件新增及移除至產生的頁面，則必須將段落系統新增至範本。

當元件鎖定時，您可以新增內容，頁面作者無法編輯這些內容。 您可以解除鎖定元件，以便定義「初始 [內容」](#editing-a-template-initial-content-author)。

>[!NOTE]
>
>在結構模式下，任何作為解鎖元件的父級的元件都不能移動、剪切或刪除。

#### 初始內容 {#template-initial-content}

解除鎖定元件後，您可以定 [義將複製到](#editing-a-template-initial-content-author) （從範本建立）結果頁面的初始內容。 這些解鎖的元件可在產生的頁面上編輯。

>[!NOTE]
>
>在「 **初始內容** 」模式和產生的頁面中，任何具有可存取父項（即版面容器中的元件）的解鎖元件都可以刪除。

#### 配置 {#template-layout}

使用版 [面](#editing-a-template-layout-template-author) ，您可以預先定義所需裝置格式的範本版面。**範本製作的** 「版面」模式與頁面製作的「版面 [**** 」模式功能相同](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)。

#### 頁面原則 {#template-page-policies}

[頁面原則](#page-policies) ，可將預先定義的頁面原則連接至頁面。 這些頁面原則可定義各種設計組態。

#### 樣式 {#template-styles}

樣式 [系統](/help/sites-cloud/authoring/features/style-system.md) (Style System)允許模板作者在元件的內容策略中定義樣式類，以便內容作者在編輯頁面上的元件時能夠選擇它們。 這些樣式可以替代元件的視覺變化，讓元件更具彈性。

如需詳細 [資訊，請參閱Style System](/help/sites-cloud/authoring/features/style-system.md) 檔案。

### 編輯模板——結構——模板作者 {#editing-a-template-structure-template-author}

在「 **結構** 」模式中，您可定義範本的元件和內容，並定義範本及其元件的原則。

* 在範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面刪除。
* 如果您希望頁面作者能夠新增和移除元件，請將段落系統新增至範本。
* 元件可以解除鎖定並再次鎖定，讓您定義 [初始內容](#editing-a-template-initial-content-author)。
* 定義了元件和頁面的設計策略。

![範本編輯器頁面結構](/help/sites-cloud/authoring/assets/templates-page-structure.png)

在模板編輯器的「結構」( **Structure** )模式下，可以執行一些操作，並可以執行一些功能來幫助您：

#### 新增元件 {#add-components}

有幾種機制可將元件新增至範本：

* 從側面 **板的** 「元件」瀏覽器。
* 使用範本上 **元件工具列上的「插入元件** 」(Insert Component **)選項或「拖曳元件至此** 」(Drag components here)方塊。
* 將資產(從側面板的 **Assets** 瀏覽器)直接拖曳至範本上，就地產生適當的元件。

新增後，每個元件都會標示為：

* 邊框
* 顯示元件類型的標籤
* 要在元件已解鎖時顯示的標籤

>[!NOTE]
>
>將現成可用的標題元件新增至範本時 **** ，其中會包含預設的文字 **結構**。
>
>如果您變更此項，並新增您自己的文字，則從範本建立頁面時，將會使用此更新的文字。
>
>如果您保留預設文字（結構），則標題將預設為後續頁面的名稱。

>[!NOTE]
>
>雖然不相同，但將元件和資產新增至範本與在製作頁面時的類似動作有許多 [相似之處](/help/sites-cloud/authoring/fundamentals/editing-content.md)。

#### 元件操作 {#component-actions}

將元件新增至範本後，請對元件採取動作。 每個單獨實例都有一個工具欄，允許您訪問可用操作，該工具欄取決於元件類型。

![範本元件的動作工具列](/help/sites-cloud/authoring/assets/templates-component-actions.png)

它也可以取決於所採取的操作，例如當策略與元件關聯時，設計配置表徵圖變為可用。

#### 編輯和設定 {#edit-and-configure}

透過這兩個動作，您可以將內容新增至元件。

#### 用邊框表示結構 {#border-to-indicate-structure}

在「結構」 **模式下工作** 時，橙色邊框表示當前選定的元件。 虛線也表示父元件。

#### 策略和屬性（一般） {#policy-and-properties-general}

內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

為元件建立內容策略或選擇現有策略。

![「內容策略」按鈕](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

這可讓您定義設計詳細資訊。

![內容原則](/help/sites-cloud/authoring/assets/template-content-policy.png)

配置窗口分為兩個部分。

* 在對話框的左側，可 **以選擇現有策略**，也可以選擇現有策略。
* 在對話框的右側，可以在「屬 **性」(Properties**)下設定特定於元件類型的屬性。

可用的屬性取決於所選元件。 例如，對於文本元件，屬性定義了複製和貼上選項、格式設定選項和段落樣式等選項。

##### 政策 {#policy}

內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

在 **Policy** （策略）下，您可以通過下拉清單選擇要應用於元件的現有策略。

![選取原則](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

通過選擇「選擇策略」下拉清單旁的「添加」按鈕，可以添加 **新策略** 。 然後，應在「原則標題」欄位中指 **定新標題** 。

![「添加策略」按鈕](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

使用下拉式清單旁的復 **制按鈕** ，可將「選擇原則」下拉式清單中選取的現有原則複製為新原則。 然後，應在「原則標題」欄位中指 **定新標題** 。 預設情況下，複製的策略將被標 **題為Copy of X**，其中X是複製策略的標題。

![「複製策略」按鈕](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

策略說明在策略說明欄位中是可選 **的** 。

在「其他 **範本」(Other templates also using the selected policy** )部分中，您可以輕鬆查看哪些其他範本使用「選擇原則」下拉式清單中選 **取的原則** 。

![現有策略的使用](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>如果將相同類型的多個元件新增為初始內容，則相同的原則會套用至所有元件。

##### 屬性 {#properties}

在「屬 **性** 」(Properties)標題下，可定義元件的設定。 標題包含兩個標籤：

* 主要
* 功能

###### 主要 {#main}

在「主 **要** 」(Main)頁籤上，定義了元件的最重要設定。

例如，對於影像元件，可定義允許的寬度，並啟用延遲載入。

如果設定允許多個配置，請按一下或點選「 **Add** （添加）」按鈕以添加其它配置。

![「添加」按鈕](/help/sites-cloud/authoring/assets/templates-add-button.png)

要刪除配置，請按一下或點選 **配置右側** 的「刪除」按鈕。

若要移除設定，請按一下或點選「刪 **除** 」按鈕。

![刪除按鈕](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### 功能 {#features}

「功 **能** 」(Features)頁籤允許您啟用或禁用元件的其他功能。

例如，對於影像元件，您可以定義裁切比例、允許的影像方向，以及允許上傳。

![功能標籤](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>請注意，在AEM裁切比例中，定義為 **高度／寬度**。 這與傳統的寬度／高度定義不同，而且是基於舊有相容性的原因。 如果您清楚地定義「名稱」( **Name** )，網頁製作使用者將不會察覺到任何差異，因為這是UI中顯示的內容。

>[!NOTE]
>
>[實施富格文本編輯器的元件的內容策略](/help/implementing/developing/extending/rich-text-editor.md) ，只能針對RTE通過其UI設定提供的選項定義。

#### 原則與屬性（版面容器） {#policy-and-properties-layout-container}

版面容器的原則和屬性設定與一般用途類似，但有些差異。

>[!NOTE]
>
>設定原則對於容器元件是必備的，因為它可讓您定義容器中可用的元件。

配置窗口分為兩個部分，與窗口的一般用法相同。

##### 政策 {#policy-layout}

內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

在 **Policy** （策略）下，您可以通過下拉清單選擇要應用於元件的現有策略。 此功能與一般使用視窗時的功能相同。

##### 屬性 {#properties-layout}

在「屬 **性** 」標題下，您可以選擇哪些元件適用於版面容器並定義其設定。 標題有三個標籤：

* 允許的元件
* 預設元件
* 回應式設定

###### 允許的元件 {#allowed-components}

在「允 **許的元件** 」標籤上，您可定義哪些元件可用於版面容器。

* 這些元件依其元件群組分組，可展開和收合。
* 您可以勾選整個群組，方法是勾選群組名稱，而取消勾選所有群組即可取消勾選。
* 減號表示至少選取一個項目，但並非選取群組中的所有項目。
* 可使用搜尋來依名稱篩選元件。
* 列在元件群組名稱右側的計數代表這些群組中選取的元件總數，而不考慮篩選。

![「允許的元件」頁籤](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### 預設元件 {#default-components}

在「預 **設元件** 」標籤上，您可定義哪些元件會自動與指定的媒體類型關聯，如此當作者從資產瀏覽器拖曳資產時，AEM就知道要將資產與哪個元件關聯。 請注意，只有具有放置區域的元件可用於此類配置。

按一下或點選 **「新增對應** 」，新增全新的元件和MIME類型對應。

在清單中選取元件，然後按一下或點選「 **新增類型** 」，將其他MIME類型新增至已映射的元件。按一下「 **刪除** 」圖示以移除MIME類型。

![「預設元件」頁籤](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### 回應式設定 {#responsive-settings}

在「回 **應式設定** 」標籤上，您可以設定版面容器產生格線中的欄數。

#### 解鎖和鎖定元件 {#unlock-and-lock-components}

您可以解除鎖定／鎖定元件，以定義內容是否可在「初始內容」模 **式中變** 更。

當元件已解除鎖定時：

* 邊框中顯示開啟的掛鎖指示符。
* 元件工具列會隨之調整。
* 已輸入的任何內容將不再顯示在「結 **構** 」模式。
   * 已輸入的內容會視為初始內容，且僅在「初始內容」 **模式中** 。
* 無法移動、剪切或刪除解鎖元件的父代。

![鎖定元件按鈕](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

這包括解除鎖定容器元件，以便在初始內容模式或產生的頁 **面中新增其他元件** 。如果您在解除鎖定容器之前已將元件/內容新增至容器，則這些元件/內容在「結構」模式中將不再顯示，但會以「初始內容 ******** 」模式顯示。在「 **結構模式**」中，只有容器元件本身會顯示其「允許的元 **件」清單**。

![允許的元件](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

為節省空間，版面容器不會擴充以容納允許的元件清單。 容器會變成可捲動的清單。

可配置的元件以「策略」表徵圖顯示 **** ，可以點選或按一下該表徵圖以編輯該元件的策略和屬性。

![「可配置元件」表徵圖](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### 與現有頁面的關係 {#relationship-to-existing-pages}

如果在根據範本建立頁面後更新結構，則這些頁面將反映範本的變更。 工具列中會顯示警告，提醒您此事以及確認對話方塊。

![範本正在使用的橫幅警告](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### 編輯範本——初始內容——作者 {#editing-a-template-initial-content-author}

**初始內容** (Initial Content)模式用於定義在首次根據範本建立頁面時將出現的內容。 然後頁面作者就可以編輯初始內容。

雖然在「結構 **」模式下建立的所有內容在「初始內容」中都可** 見 ****，但只能選擇和編輯已解鎖的元件。

>[!NOTE]
>
>**使用該範本** 所建立之頁面的編輯模式可考慮初始內容模式。 因此，策略不是在「初始內 **容** 」模式中定義，而是在「 [**結構** 」模式中](#editing-a-template-structure-template-author)。

* 標籤可供編輯的解鎖元件。 選取後，它們會有藍色邊框：

   ![初始內容模式](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* 解除鎖定的元件有工具列，可讓您編輯和設定內容：

   ![解鎖元件](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* 如果容器元件已解除鎖定(在「結 **構** 」模式中)，則您可以在「初始內容 **** 」模式中新增元件至容器。在「初始內 **容」模式中新增的元件** ，可在產生的頁面上移動或從中刪除。

   您可以使用「拖曳元件到此處 **」區域，或從適當容器的工具列** 中使用「插入新元件 **** 」選項來新增元件。

   ![新增元件](/help/sites-cloud/authoring/assets/templates-add-component.png)
   ![新增元件](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* 如果在根據範本建立頁面後更新範本的初始內容，則這些頁面不會受到範本中初始內容變更的影響。

>[!NOTE]
>
>初始內容是用於準備元件和頁面版面，以做為建立內容的起點。 它並非實際內容，而是維持原狀。 因此，無法翻譯初始內容。
>
>如果您需要在範本中加入可翻譯的文字，例如在頁首或頁尾中，則可使用核 [心元件的本地化功能](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/localization.html)。

### 編輯範本——版面——範本作者 {#editing-a-template-layout-template-author}

您可以為各種裝置定義範本版面。 [範本的互動式版面](/help/sites-cloud/authoring/features/responsive-layout.md) ，就像網頁製作一樣。

>[!NOTE]
>
>版面的變更會反映在「初始內 **容** 」模式中，但「結構」模式中未 **顯示變更** 。

![編輯範本版面](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### 編輯範本——頁面政策——範本作者／開發人員 {#editing-a-template-page-policy-template-author-developer}

「頁面資訊」功能表的「頁面政策」選項下會維護包含必要用戶端程 **式庫的頁面原** 則 **** 。

要訪問「頁 **面策略** 」對話框：

1. 從範本 **編輯器中**，從工具列中選 **擇頁面資訊** ，然後選 **擇頁面原則** ，以開啟對話方塊。
1. 「頁 **面原則** 」對話方塊隨即開啟，並分為兩個區段：

   * 左半部分定義頁 [面原則](#page-policies)
   * 右半部分定義頁 [面屬性](#page-properties)

   ![頁面設計](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### 頁面原則 {#page-policies}

您可以將內容原則套用至範本或結果頁面。 這定義了頁面上主要段落系統的內容原則。

![頁面原則](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* 您可以從「選擇策略」下拉式清單中 **選擇頁面的** 現有策略。

   ![原則選擇器](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

   通過選擇「選擇策略」下拉清單旁的「添加」按鈕，可以添加 **新策略** 。 然後，應在「原則標題」欄位中指 **定新標題** 。

   ![「添加策略」按鈕](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

   使用下拉式清單旁的復 **制按鈕** ，可將「選擇原則」下拉式清單中選取的現有原則複製為新原則。 然後，應在「原則標題」欄位中指 **定新標題** 。 預設情況下，複製的策略將被標 **題為Copy of X**，其中X是複製策略的標題。

   ![「複製策略」按鈕](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* 在「原則標題」欄位中定義原則 **的標題** 。 必須有原則才能擁有標題，才能在「選取原則」下拉式清單中輕鬆 **選取** 。

   ![原則標題](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* 策略說明在策略說明欄位中是可選 **的** 。
* 在「其他 **範本」(Other templates also using the selected policy** )部分中，您可以輕鬆查看哪些其他範本使用「選擇原則」下拉式清單中選 **取的原則** 。

   ![原則使用](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### 頁面內容 {#page-properties}

使用頁面屬性，您可以使用「頁面設計」對話方塊來定義所需的 **用戶端程式庫** 。 這些用戶端程式庫包括要載入範本的樣式表和javascript，以及使用該範本建立的頁面。

![頁面內容](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* 指定您要套用至使用此範本所建立之頁面的用戶端程式庫。 在「用戶端程式庫」區段的文字欄位中輸入程 **式庫的名稱** 。

   ![用戶端程式庫](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* 如果需要多個庫，請按一下「添加」按鈕為庫名稱添加其他文本欄位。

   ![「添加」按鈕](/help/sites-cloud/authoring/assets/templates-add-button.png)

   視需要為用戶端程式庫新增多個文字欄位。

* 使用拖曳控點拖曳欄位，以視需要定義程式庫的相對位置。

   ![拖曳控點](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>雖然範本作者可以在範本上指定頁面原則，但他或她需要從開發人員取得適當用戶端程式庫的詳細資訊。

### 編輯範本——初始頁面屬性——作者 {#editing-a-template-initial-page-properties-author}

使用「 **初始頁面屬性** 」選項，可以定義在建立 [結果頁面時要使用的初始頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 。

1. 從範本編輯器中，從工具 **列選擇「頁面資訊** 」，然後 **選擇「初始頁面屬性** 」以開啟對話方塊。

1. 在對話方塊中，您可以定義要套用至使用此範本建立之頁面的屬性。

   ![範本初始頁面屬性](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. 使用「完成」確認 **您的定義**。

## 最佳作法 {#best-practices}

建立範本時，您應考慮：

1. 從範本建立頁面後，範本變更的影響。

   以下列出範本上可能的不同作業，以及它們對從它們建立的頁面有何影響：

   * 結構變更：

      * 這些會立即套用至產生的頁面。
      * 訪客仍需要發佈已變更的範本，才能看到變更。
   * 變更內容原則和設計組態：

      * 這些項目會立即套用至產生的頁面。
      * 訪客需要發佈變更才能看到變更。
   * 初始內容的變更：

      * 這些僅適用於在範本變更後建立的頁面。
   * 版面的變更取決於修改的元件是否屬於：

      * 僅限結構——立即應用
      * 包含初始內容——僅限在變更後建立的頁面上

   在下列情況下，請格外小心：

   * 鎖定或解除鎖定啟用範本上的元件。
   * 這可能會產生副作用，因為現有的頁面已經在使用它。 通常：

      * 現有頁面上將遺失解除鎖定的元件（已鎖定）。
      * 鎖定元件（可編輯）將隱藏該內容，使其無法顯示在頁面上。

   >[!NOTE]
   >
   >AEM在變更不再是草稿之範本上元件的鎖定狀態時，會顯式提供警告。

1. [為您的網站特定範本](#creating-a-template-folder-admin) ，建立您自己的資料夾。
1. [從範本主控台](#publishing-a-template-template-author) ，發佈您 **的範本** 。
