---
title: 建立頁面範本
description: 範本會定義結果頁面的結構，且使用範本編輯器，建立和維護範本不再是開發人員專屬的工作
exl-id: 4c9dbf26-5852-45ab-b521-9f051c153b2e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '4524'
ht-degree: 9%

---

# 建立頁面範本 {#creating-page-templates}

建立頁面時，您必須選取範本，作為建立新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容以及可以使用的元件。

使用范 **本編輯器**，建立和維護範本不再是開發人員專屬的工作。也可以涉及一種稱為模板作 **者的權**&#x200B;力用戶。開發人員仍需要設定環境、建立用戶端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。****

此 **範本主控台** 可讓範本作者：

* 建立新範本或複製現有範本。
* 管理範本的生命週期。

此 **範本編輯器** 可讓範本作者：

* 將元件新增至範本，並將其放置在回應式格線上。
* 預先設定元件。
* 定義在使用範本建立的頁面上可編輯哪些元件。

本檔案說明如何 **範本作者** 可使用範本主控台和編輯器來建立和管理可編輯的範本。

如需如何在技術層面使用可編輯範本的詳細資訊，請參閱開發人員檔案 [頁面範本](/help/implementing/developing/components/templates.md) 以取得詳細資訊。

>[!NOTE]
>
>范 **** 本編輯器不支援直接在範本層級定位。可以定位根據可編輯範本建立的頁面，但無法定位範本本身。

## 在您開始之前 {#before-you-start}

>[!NOTE]
>
>管理員必須在中設定範本資料夾 **設定瀏覽器** 並套用適當的許可權，然後範本作者才能在該資料夾中建立範本。

開始之前，請務必考慮到建立範本需要共同作業。 因此， [角色](#roles) 會針對每項任務指定。 這不會影響您實際使用範本來建立頁面的方式，但會影響頁面與其範本的關聯方式。

### 角色 {#roles}

使用「模板控制台」和「模 **板編輯器** 」建立新模板時 **** ，需要在以下角色之間協作：

* **管理員**：
   * 建立新的範本資料夾需要 `admin` 權利。
   * 這類工作通常也可以由開發人員完成
* **開發人員**：
   * 著重於技術/內部細節
   * 需要開發環境的經驗。
   * 為範本作者提供必要資訊。
* **範本作者**：
   * 此為群組成員的特定作者 `template-authors`
      * 這會配置所需的許可權和許可權。
   * 可以設定元件和其他高階詳細資訊的使用，這些需要：
      * 一些技術知識
         * 例如，在定義路徑時使用模式。
      * 來自開發人員的技術資訊。

由於某些工作的性質（例如建立資料夾），需要開發環境，而這需要知識/經驗。

本檔案中詳細列出的任務以及負責執行這些任務的角色。

## 建立和管理範本 {#creating-and-managing-templates}

建立可編輯的範本時，您可以：

* 使用 **範本** 主控台。 這可在以下位置取得： **一般** 的區段 **工具** 主控台。
   * 或直接存取： `https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* 可以 [建立範本的資料夾](#creating-a-template-folder-admin) 如有需要
* [建立新範本](#creating-a-new-template-template-author)，一開始會是空的
* [定義其他屬性](#defining-template-properties-template-author) 範本（如有需要）
* [編輯範本](#editing-templates-template-authors) 若要定義：
   * [結構](#editing-a-template-structure-template-author)  — 使用範本建立的頁面上無法變更的預定義內容。
   * [初始內容](#editing-a-template-initial-content-author)  — 可在使用範本建立的頁面上變更的預定義內容。
   * [版面](#editing-a-template-layout-template-author)  — 適用於一系列裝置。
   * [樣式](/help/sites-cloud/authoring/page-editor/style-system.md)  — 定義要與範本及其元件搭配使用的樣式。
* [啟用範本](#enabling-a-template-template-author) 建立頁面時使用
* [允許範本](#allowing-a-template-author) 適用於您的網站所需頁面或分支
* [發佈範本](#publishing-a-template-template-author) 以使其可在發佈環境中使用

>[!NOTE]
>
>此 **允許的範本** 通常會在最初設定您的網站時預先定義。

>[!TIP]
>
>切勿在範本中輸入任何必須國際化的資訊。 <!-- Never enter any information that must be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>針對必須本地化的範本元素（例如頁首和頁尾），請使用 [核心元件的本地化功能。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html)

### 建立範本資料夾 — 管理員 {#creating-a-template-folder-admin}

您應該為專案建立範本資料夾，以儲存專案特定的範本。 這是一項管理員任務，詳見檔案 [頁面範本](/help/implementing/developing/components/templates.md#template-folders).

### 建立新範本 — 範本作者 {#creating-a-new-template-template-author}

1. 開啟 **範本主控台** (方式 **工具>** **一般**)然後導覽至所需的資料夾。

   >[!NOTE]
   >
   >在標準AEM執行個體中 **全域** 資料夾已存在於範本主控台中。 此檔案會保留預設範本，並在目前資料夾中找不到原則及/或範本型別時，做為遞補內容。
   >
   >建議最佳實務使用 [為您的專案建立的範本資料夾](/help/implementing/developing/components/templates.md#template-folders).

1. 選取 **建立**，後接 **建立範本** 以開啟精靈。

1. 選取 **範本型別**，然後選取 **下一個**.

   >[!NOTE]
   >
   >範本型別是預先定義的範本配置，可視為範本的範本。 這些是由開發人員或系統管理員預先定義的。 如需詳細資訊，請參閱開發人員檔案 [頁面範本](/help/implementing/developing/components/templates.md#template-type).—>

1. 完成 **範本詳細資訊**：

   * **範本名稱**
   * **說明**

1. 選擇 **建立**。隨即顯示確認訊息，請選取 **開啟** 以開始編輯範本或 **完成** 以返回範本主控台。

   >[!NOTE]
   >
   >建立新範本時，會將其標籤為 **草稿** 在主控台中，這表示頁面作者還不能使用它。

>[!NOTE]
>
>範本是簡化頁面建立工作流程的強大工具。 然而，太多的範本會讓作者不知所措，並使頁面建立變得混亂。 一個好的經驗法則是將範本數保持在100以下。
>
>由於潛在的效能影響，Adobe不建議使用超過1000個範本。

### 定義範本屬性 — 範本作者 {#defining-template-properties-template-author}

範本可以有下列屬性：

* 影像
   * 要當做影像使用 [範本的縮圖](#template-thumbnail-image) 以輔助選取，例如「建立頁面」精靈中的選取。
      * 可以上傳
      * 可根據範本內容產生
* 標題
   * 用於識別範本的標題，例如 **建立頁面** 精靈。
* 說明
   * 選用的說明，可提供範本及其用途的詳細資訊，例如 **建立頁面** 精靈。

若要檢視和/或編輯屬性：

1. 在 **範本主控台**，選取範本。
1. 從工 **具欄中選擇** 「查看屬性」(View Properties)或快速選項以開啟對話框。
1. 您現在可以檢視或編輯範本屬性。

>[!NOTE]
>
>主控台中會指出範本的狀態（草稿、已啟用或已停用）。

#### 範本縮圖影像 {#template-thumbnail-image}

若要定義範本縮圖：

1. 編輯範本屬性。
1. 選擇您要上傳縮圖，還是從範本內容產生縮圖。
   * 如果要上傳縮圖，請選取 **上傳影像**
   * 如果您要產生縮圖，請選取 **產生預覽**
1. 對於這兩種方法，都會顯示縮圖的預覽。
   * 如果不滿意，請選取 **清除** 上傳另一個影像或重新產生縮圖。
1. 如果您對縮圖感到滿意，請選取 **儲存並關閉**.

### 啟用和允許範本 — 範本作者 {#enabling-and-allowing-a-template-template-author}

若要在建立頁面時使用範本，您需要：

* [啟用範本](#enabling-a-template-template-author) 以使其可在建立頁面時使用。
* [允許範本](#allowing-a-template-author) 以指定可使用範本的內容分支。

#### 啟用範本 — 範本作者 {#enabling-a-template-template-author}

您可啟用或停用範本，使其可在以下位置使用或無法使用： **建立頁面** 精靈。

>[!CAUTION]
>
>啟用範本後，當範本作者開始進一步更新範本時，會顯示警告。 這是為了通知使用者可能會參考範本，所以任何變更都可能影響參考範本的頁面。

1. 在 **範本主控台**，選取範本。
1. 選取 **啟用** 或 **停用** ，然後在確認對話方塊中再次開啟。
1. 您現在可以在以下情況下使用範本： [建立頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)，但您可能希望 [編輯範本](#editing-templates-template-authors) 根據您的需求。

>[!NOTE]
>
>主控台中會指出範本的狀態（草稿、已啟用或已停用）。

#### 允許範本 — 作者 {#allowing-a-template-author}

範本可以供某些頁面分支使用或無法使用。

1. 開啟 [頁面屬性](/help/sites-cloud/authoring/sites-console/page-properties.md) 用於您希望範本可用的分支根頁面。
1. 開啟 **進階** 標籤。
1. 在「 **範本設定** 」下 **，使用「新增」欄位** ，指定範本的路徑。

   路徑可以是明確的或使用模式。 例如：

   `/conf/<your-folder>/settings/wcm/templates/.*`

   路徑的順序不相關。 會掃描所有路徑並擷取任何範本。

   >[!NOTE]
   >
   >如果 **允許的範本** 清單留空，然後樹狀結構會遞增，直到找到值/清單為止。
   >
   >
   >另請參閱 [範本可用性](/help/implementing/developing/components/templates.md#template-availability)  — 允許範本的原則保持不變。

1. 按一下 **儲存** 以儲存對頁面屬性所做的變更。

>[!NOTE]
>
>通常會在設定您的網站時，為您整個網站預先定義允許的範本。

### 發佈範本 — 範本作者 {#publishing-a-template-template-author}

由於範本在轉譯頁面時為參考狀態，因此必須發佈已完整設定的範本，才能用於發佈環境。

1. 在 **範本主控台**，選取範本。
1. 選取 **發佈** 以開啟精靈。
1. 選取 **內容原則** 將一同發佈。
1. 選取 **發佈** 工具列以完成動作。

## 編輯範本 — 範本作者 {#editing-templates-template-authors}

建立或編輯範本時，您可以定義多個方面。 編輯範本類似於頁面製作。

此 **模式** 工具列中的選取器可讓您選取並編輯範本的適當方面：

* [結構](#editing-a-template-structure-template-author)
* [初始內容](#editing-a-template-initial-content-author)
* [版面配置](#editing-a-template-layout-template-author)

![範本編輯器模式選擇器](/help/sites-cloud/authoring/assets/templates-mode.png)

當 **頁面原則** 上的選項 **頁面資訊** 功能表可讓您 [選取所需的頁面原則](#page-policies)：

![範本編輯器頁面資訊](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>如果作者開始編輯已啟用的範本，則會顯示警告。 這是為了通知使用者可能會參考範本，所以任何變更都可能影響參考範本的頁面。

### 範本屬性 {#template-attributes}

可以編輯範本的下列屬性：

#### 結構 {#template-structure}

新增至的元件 [結構](#editing-a-template-structure-template-author) 頁面作者無法從結果頁面中移動/移除。 如果您希望頁面作者能夠在產生的頁面中新增和移除元件，則需將段落系統新增至範本。

鎖定元件後，您可以新增頁面作者無法編輯的內容。 您可以解鎖元件，讓您 [初始內容](#editing-a-template-initial-content-author).

>[!NOTE]
>
>在結構模式中，任何作為已解鎖元件之父件的元件都無法移動、剪下或刪除。

#### 初始內容 {#template-initial-content}

解鎖元件後，您可以定義 [初始內容](#editing-a-template-initial-content-author) 這些頁面會複製到使用範本建立的結果頁面上。 您可以在產生的頁面上編輯這些已解鎖的元件。

>[!NOTE]
>
>在 **初始內容** 模式，以及在結果頁面上，可以刪除任何具有可存取父項的已解鎖元件（即配置容器內的元件）。

#### 版面配置 {#template-layout}

使用版 [面](#editing-a-template-layout-template-author) ，您可以預先定義所需裝置格式的範本版面。**範本製作的** 「版面」模式與頁面製作的「版面 [**** 」模式功能相同](/help/sites-cloud/authoring/page-editor/responsive-layout.md#defining-layouts-layout-mode)。

#### 頁面原則 {#template-page-policies}

[頁面原則](#page-policies) 可以將預先定義的頁面原則連線至頁面。 這些頁面原則會定義各種設計配置。

#### 樣式 {#template-styles}

樣式系統可讓範本作者在元件的內容原則中定義樣式類別，讓內容作者在編輯頁面上的元件時能夠選取這些類別。 這些樣式可作為元件的替代視覺變體，使其更靈活。

請參閱 [樣式系統檔案](/help/sites-cloud/authoring/page-editor/style-system.md) 以取得詳細資訊。

### 編輯範本 — 結構 — 範本作者 {#editing-a-template-structure-template-author}

在 **結構** 模式您可以定義範本的元件和內容，並為範本及其元件定義原則。

* 範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面中刪除。
* 如果您希望頁面作者能夠新增和移除元件，請新增段落系統至範本。
* 元件可解除鎖定並重新鎖定，以允許您定義 [初始內容](#editing-a-template-initial-content-author).
* 元件和頁面的設計原則已定義。

![範本編輯器頁面結構](/help/sites-cloud/authoring/assets/templates-page-structure.png)

您可以在中執行數個動作 **結構** 範本編輯器的模式和數個功能可協助您：

#### 新增元件 {#add-components}

將元件新增至範本的機制有幾種：

* 從 **元件** 側面板中的瀏覽器。
* 使用範本上 **元件工具列上的「插入元件** 」(Insert Component **)選項或「拖曳元件至此** 」(Drag components here)方塊。
* 透過拖曳資產(從 **資產** （例如側面板中的瀏覽器）直接在範本上原地產生適當的元件。

新增後，每個元件都會標示：

* 邊框
* 顯示元件型別的標籤
* 解鎖元件時顯示的標籤

>[!NOTE]
>
>將現成可用的標題元件新增至範本時 **** ，其中會包含預設的文字 **結構**。
>
>如果您變更此專案，並新增您自己的文字，則從範本建立頁面時，會使用此更新的文字。
>
>如果您保留預設文字（結構），則標題將預設為後續頁面的名稱。

>[!NOTE]
>
>將元件和資產新增至範本時，雖然不盡相同，但與類似動作有許多相似之處， [頁面製作。](/help/sites-cloud/authoring/page-editor/edit-content.md)

#### 元件動作 {#component-actions}

將元件新增至範本後，請對元件執行動作。 每個個別例項都有可讓您存取可用動作的工具列，工具列視元件型別而定。

![範本元件的動作工具列](/help/sites-cloud/authoring/assets/templates-component-actions.png)

也可以取決於所採取的動作，例如當原則已與元件相關聯時，則設計設定圖示會變為可用。

#### 編輯和設定 {#edit-and-configure}

透過這兩個動作，您可以將內容新增至元件。

#### 指示結構的邊框 {#border-to-indicate-structure}

使用時 **結構** 模式橘色邊框表示目前選取的元件。 虛線也表示父元件。

#### 原則與屬性（一般） {#policy-and-properties-general}

內容（或設計）原則會定義元件的設計屬性。 例如，可用的元件或最小/最大尺寸。 這些適用於範本（以及使用範本建立的頁面）。

為元件建立內容原則，或選取現有的原則。

![內容原則按鈕](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

這可讓您定義設計詳細資訊。

![內容原則](/help/sites-cloud/authoring/assets/template-content-policy.png)

設定視窗分為兩個部分。

* 在對話方塊的左側，在 **原則**，您可以選取現有原則或選取現有原則。
* 對話方塊右側下方的 **屬性**&#x200B;時，您可以設定元件型別的特定屬性。

可用的屬性取決於所選的元件。 例如，對於文字元件，屬性會定義複製和貼上選項、格式選項和段落樣式等選項。

##### 政策 {#policy}

內容（或設計）原則會定義元件的設計屬性。 例如，可用的元件或最小/最大尺寸。 這些適用於範本（以及使用範本建立的頁面）。

在 **原則** 您可以透過下拉式清單，選取要套用至元件的現有原則。

![選取原則](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

選取「 」旁邊的「新增」按鈕，即可新增一項原則。 **選取原則** 下拉式清單。 在中提供新標題 **原則標題** 欄位。

![「新增原則」按鈕](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

中選取的現有原則 **選取原則** 下拉式清單可使用下拉式清單旁的複製按鈕來復製為新原則。 在中提供新標題 **原則標題** 欄位。 依預設，複製的原則標題為 **X的副本**，其中X是複製原則的標題。

![「複製原則」按鈕](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

原則說明是選擇性的，可在 **原則說明** 欄位。

在 **其他範本也使用選取的原則** 區段，您可以輕鬆檢視其他哪些範本使用在區段中選取的原則 **選取原則** 下拉式清單。

![使用現有原則](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>如果將相同型別的多個元件新增為初始內容，則相同原則會套用至所有元件。

##### 屬性 {#properties}

在 **屬性** 標題您可以定義元件的設定。 標題有兩個標籤：

* 主要
* 功能

###### 主要 {#main}

在 **主要** 標籤中，會定義元件最重要的設定。

例如，對於影像元件，可定義允許的寬度並啟用延遲載入。

如果設定允許多項組態，請選取 **新增** 按鈕以新增其他設定。

![新增按鈕](/help/sites-cloud/authoring/assets/templates-add-button.png)

若要移除組態，請選取 **刪除** 按鈕位於設定的右側。

若要移除組態，請選取 **刪除** 按鈕。

![刪除按鈕](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### 功能 {#features}

此 **功能** 索引標籤可讓您啟用或停用元件的其他功能。

例如，對於影像元件，您可以定義裁切比例、允許的影像定向以及是否允許上傳。

![功能標籤](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>在AEM中，裁切比例定義為 **高度/寬度**. 這和寬度/高度比的傳統定義不同，並且是由於舊有相容性的原因完成的。只要您定義「 」，頁面編寫使用者就不會察覺到任何差異 **名稱** 很清楚，因為這是UI中顯示的內容。

>[!NOTE]
>
>[實作RTF編輯器的元件的內容原則](/help/implementing/developing/extending/rich-text-editor.md) 只能為RTE透過其UI設定提供的選項定義。

#### 原則和屬性（配置容器） {#policy-and-properties-layout-container}

配置容器的原則與屬性設定與一般使用方式類似，但有一些差異。

>[!NOTE]
>
>容器元件必須設定原則，因為它可讓您定義容器中可用的元件。

設定視窗分為兩個部分，就像視窗的一般使用方式一樣。

##### 政策 {#policy-layout}

內容（或設計）原則會定義元件的設計屬性。 例如，可用的元件或最小/最大尺寸。 這些適用於範本（以及使用範本建立的頁面）。

在 **原則** 您可以透過下拉式清單選取要套用至元件的現有原則。 其運作方式與視窗的一般使用方式相同。

##### 屬性 {#properties-layout}

在 **屬性** 標題您可以選擇哪些元件可用於版面容器並定義其設定。 標題有三個索引標籤：

* 已允許的元件
* 預設元件
* 回應式設定

###### 已允許的元件 {#allowed-components}

在 **允許的元件** 索引標籤中，您可定義哪些元件適用於配置容器。

* 元件會依其元件群組分組，這些群組可展開和摺疊。
* 勾選群組名稱即可選取整個群組，取消勾選可取消選取所有群組。
* 減號表示至少選取了一個群組中的專案，但並未選取所有專案。
* 搜尋可依名稱篩選元件。
* 無論篩選條件為何，元件群組名稱右側所列的計數代表這些群組中選取的元件總數。

![允許的元件索引標籤](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### 預設元件 {#default-components}

在 **預設元件** 索引標籤上，您可定義哪些元件會自動與指定媒體型別建立關聯，這樣當作者從資產瀏覽器拖曳資產時，AEM就能知道要與哪個元件建立關聯。 只有具備拖放區域的元件才適用於此類設定。

選取 **新增對應** 新增全新的元件和MIME型別對應。

在清單中選取元件，然後選取 **新增型別** 將其他MIME型別新增至已對應的元件。 按一下「 **刪除** 」圖示以移除MIME類型。

![預設元件索引標籤](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### 回應式設定 {#responsive-settings}

在 **回應式設定** 索引標籤您可以配置配置配置容器之產生格線中的欄數。

#### 解鎖和鎖定元件 {#unlock-and-lock-components}

您可以解鎖/鎖定元件，以定義內容是否可用於變更 **初始內容** 模式。

解鎖元件後：

* 開啟的掛鎖指示器會顯示在邊框中。
* 元件工具列會據此調整。
* 任何已輸入的內容將不會再顯示於 **結構** 模式。
   * 已輸入的內容會視為初始內容，且只會顯示在 **初始內容** 模式。
* 無法移動、剪下或刪除已解鎖元件的父件。

![鎖定元件按鈕](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

這包括解除鎖定容器元件，以便在初始內容模式或產生的頁 **面中新增其他元件** 。如果您在解除鎖定容器之前已將元件/內容新增至容器，則在中時，不再顯示這些元件/內容。 **結構** 模式，但顯示於 **初始內容** 模式。 在 **結構模式**，則只會顯示容器元件本身及其清單： **允許的元件**.

![允許的元件](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

為了節省空間，配置容器不會為了容納允許的元件清單而增大。 容器會變成可捲動清單。

可配置的元件以「策略」表徵圖顯示 **** ，可以點選或按一下該表徵圖以編輯該元件的策略和屬性。

![「可設定的元件」圖示](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### 與現有頁面的關係 {#relationship-to-existing-pages}

如果在根據範本建立頁面後更新結構，則這些頁面將反映範本的變更。 工具列中會顯示警告訊息，提醒您這個事實以及確認對話方塊。

![正在使用範本的橫幅警告](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### 編輯範本 — 初始內容 — 作者 {#editing-a-template-initial-content-author}

**初始內容** 模式是用來定義首次根據範本建立頁面時顯示的內容。 然後，頁面作者可以編輯初始內容。

雖然在「結構 **」模式下建立的所有內容在「初始內容」中都可** 見 ****，但只能選擇和編輯已解鎖的元件。

>[!NOTE]
>
>**初始內容** 模式可視為使用該範本建立之頁面的編輯模式。 因此，原則未定義於 **初始內容** 模式，但不是在 [**結構** 模式](#editing-a-template-structure-template-author).

* 可編輯的已解除鎖定元件會加上標籤。 選取時，它們具有藍色邊框：

  ![初始內容模式](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* 已解鎖的元件有可讓您編輯及設定內容的工具列：

  ![已解除鎖定的元件](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* 如果容器元件已解除鎖定(在「結 **構** 」模式中)，則您可以在「初始內容 **** 」模式中新增元件至容器。在「初始內 **容」模式中新增的元件** ，可在產生的頁面上移動或從中刪除。

  您可以使用「拖曳元件到此處 **」區域，或從適當容器的工具列** 中使用「插入新元件 **** 」選項來新增元件。

  ![新增元件](/help/sites-cloud/authoring/assets/templates-add-component.png)
  ![新增元件](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* 如果在根據範本建立頁面後更新範本的初始內容，則範本中初始內容的變更不會影響這些頁面。

>[!NOTE]
>
>初始內容旨在準備元件和作為建立內容起點的頁面配置。 此並非意圖讓實際內容維持原狀。 因此，初始內容無法翻譯。
>
>如果您需要在範本中加入可翻譯的文字（例如頁首或頁尾），您可使用 [核心元件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html).

### 編輯範本 — 版面 — 範本作者 {#editing-a-template-layout-template-author}

您可以為一系列裝置定義範本配置。 [回應式版面](/help/sites-cloud/authoring/page-editor/responsive-layout.md) 適用於範本的運作方式與頁面製作相同。

>[!NOTE]
>
>配置變更會反映在 **初始內容** 模式，但看不到任何變更 **結構** 模式。

![編輯範本配置](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### 編輯範本 — 頁面原則 — 範本作者/開發人員 {#editing-a-template-page-policy-template-author-developer}

「頁面資訊」功能表的「頁面政策」選項下會維護包含必要用戶端程 **式庫的頁面原** 則 **** 。

若要存取 **頁面原則** 對話方塊：

1. 從 **範本編輯器**，選取 **頁面資訊** 從工具列，然後 **頁面原則** 以開啟對話方塊。
1. 此 **頁面原則** 對話方塊隨即開啟，並分成兩個區段：

   * 左半部會定義 [頁面原則](#page-policies)
   * 右半部分定義 [頁面屬性](#page-properties)

   ![頁面設計](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### 頁面原則 {#page-policies}

您可以將內容原則套用至範本或結果頁面。 這會定義頁面上主要段落系統的內容原則。

![頁面原則](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* 您可以從以下位置為頁面選取現有的原則： **選取原則** 下拉式清單。

  ![原則選擇器](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

  選取「 」旁邊的「新增」按鈕，即可新增一項原則。 **選取原則** 下拉式清單。 在中提供新標題 **原則標題** 欄位。

  ![「新增原則」按鈕](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

  中選取的現有原則 **選取原則** 下拉式清單可使用下拉式清單旁的複製按鈕來復製為新原則。 在中提供新標題 **原則標題** 欄位。 依預設，複製的原則標題為 **X的副本**，其中X是複製原則的標題。

  ![「複製原則」按鈕](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* 在中定義原則的標題 **原則標題** 欄位。 原則必須有標題，這樣才能輕鬆地在 **選取原則** 下拉式清單。

  ![原則標題](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* 原則說明是選擇性的，可在 **原則說明** 欄位。
* 在 **其他範本也使用選取的原則** 區段，您可以輕鬆檢視其他哪些範本使用在區段中選取的原則 **選取原則** 下拉式清單。

  ![原則使用情況](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### 頁面屬性 {#page-properties}

使用頁面屬性，您可以使用來定義所需的使用者端程式庫 **頁面設計** 對話方塊。 這些使用者端程式庫包含要與範本及使用該範本建立的頁面一起載入的樣式表和JavaScript。

![頁面內容](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* 指定您要套用至使用此範本建立之頁面的使用者端程式庫。 在的文字欄位中輸入程式庫名稱 **使用者端資源庫** 區段。

  ![使用者端程式庫](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* 如果需要多個程式庫，請按一下「新增」按鈕，為程式庫名稱新增其他文字欄位。

  ![新增按鈕](/help/sites-cloud/authoring/assets/templates-add-button.png)

  視需要為您的使用者端資料庫新增任意數目的文字欄位。

* 使用拖曳控點來拖曳欄位，視需要定義物件庫的相對位置。

  ![拖曳控點](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>雖然範本作者可以在範本上指定頁面原則，但他們必須向開發人員取得適當使用者端程式庫的詳細資料。

### 編輯範本 — 初始頁面屬性 — 作者 {#editing-a-template-initial-page-properties-author}

使用 **初始頁面屬性** 選項，您可以定義 [頁面屬性](/help/sites-cloud/authoring/sites-console/page-properties.md) 建立結果頁面時使用。

1. 在範本編輯器中，選取 **頁面資訊** 從工具列，然後 **初始頁面屬性** 以開啟對話方塊。

1. 在對話方塊中，您可以定義要套用至使用此範本建立的頁面的屬性。

   ![範本初始頁面屬性](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. 透過確認您的定義 **完成**.

## 最佳做法 {#best-practices}

建立範本時，您應考慮：

1. 從該範本建立頁面後，變更對範本的影響。

   以下是範本上可能進行的不同操作清單，以及這些操作如何影響根據範本建立的頁面：

   * 結構的變更：

      * 這些會立即套用至產生的頁面。
      * 訪客仍需發佈已變更的範本，才能看到變更。

   * 內容原則和設計設定的變更：

      * 這些會立即套用至產生的頁面。
      * 訪客需要發佈變更才能檢視變更。

   * 初始內容的變更：

      * 這些僅適用於範本變更後建立的頁面。

   * 配置圖變更取決於修改的元件是否屬於下列專案：

      * 僅限結構 — 立即套用
      * 包含初始內容 — 僅適用於變更後建立的頁面

   發生下列情況時請特別小心：

   * 在啟用的範本上鎖定或解除鎖定元件。
   * 這會產生副作用，因為現有頁面已可使用它。 通常：

      * 現有頁面上遺失解除鎖定元件（已鎖定）。
      * 鎖定元件（可編輯的）將會隱藏該內容，使其無法在頁面上顯示。

   >[!NOTE]
   >
   >變更不再是草稿之範本上元件的鎖定狀態時，AEM會發出明確警告。

1. [建立您自己的資料夾](#creating-a-template-folder-admin) 您網站專屬範本的URL。
1. [發佈您的範本](#publishing-a-template-template-author) 從 **範本** 主控台。
