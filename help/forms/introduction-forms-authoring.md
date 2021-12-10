---
title: 製作適用性Forms簡介
seo-title: Introduction to authoring Adaptive Forms
description: AEM Forms提供簡單易用且功能強大的介面，可編寫適用性Forms。 它提供許多元件和工具，供您用來建立表單。
seo-description: AEM Forms provide easy-to-use yet powerful interface for authoring Adaptive Forms. It provides a host of components and tools that you can use to build forms.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
topic-tags: author, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 3%

---


# 適用性Forms編輯器 {#introduction-to-authoring-adaptive-forms}

## 概覽 {#overview}

適用性Forms可讓您建立吸引人、回應式、動態且最適化的表單。 [!DNL AEM Forms] 提供直覺式使用者介面和現成可用的元件，供您建立及使用適用性Forms。 您可以選擇根據表單模型或架構建立適用性表單，或不使用表單模型。 必須仔細選擇不僅符合您要求而且擴展您現有基礎設施投資和資產的表單模型。 您可以從下列選項中選擇以建立最適化表單：

<!-- * **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source. -->

* **使用XDP表單範本**
如果您對XFA或XDP表單有投資，則此表單是理想的表單模型。 它提供將XFA型表單轉換為最適化Forms的直接方式。 任何現有的XFA規則都會保留在相關聯的適用性Forms中。 產生的適用性Forms支援XFA結構，例如驗證、事件、屬性和模式。

* **使用XML結構定義(XSD)或JSON結構**
XML和JSON結構代表組織內的後端系統產生或使用資料的結構。 您可以將結構與適用性表單建立關聯，並使用其元素將動態內容新增至適用性表單。 製作最適化Forms時，架構的元素將可用於內容瀏覽器的「資料模型物件」標籤。

* **無或不使用表單模型**
使用此選項建立的適用性Forms不使用任何表單模型。 從這種表單生成的資料XML具有帶有欄位和相應值的扁平結構。

<!--  For more information about creating an Adaptive Form, see [Creating an Adaptive Form](creating-adaptive-form.md). -->

## 適用性表單製作UI {#adaptive-form-authoring-ui}

製作最適化Forms的觸控最佳化UI直覺式，並提供：

* 拖放功能
* 標準表單元件
* 整合的資產存放庫

建立新表單或編輯現有的適用性表單時，您會使用下列UI元素：

* [側欄](#sidebar)
* [頁面工具列](#page-toolbar)
* [元件工具列](#component-toolbar)
* [適用性表單頁面](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### 側欄 {#sidebar}

側欄可讓您

* 在AEM數位資產管理(DAM)存放庫中搜尋、檢視及使用資產。
* 請參閱表單內容，例如面板、元件、欄位和版面。
* 在表單上新增元件。
* 編輯元件屬性。

![側欄](assets/sidebar-comps.png)

**答：** 內容瀏覽器 **B.** 屬性瀏覽器 **C.** 資產瀏覽器 **D.** 元件瀏覽器

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

側欄包含下列瀏覽器：

* **內容瀏覽器**
在內容瀏覽器中，您會看到：

   * **表單物件**
顯示表單的對象層次結構。 作者可在「表單物件樹」中點選該元素，以導覽至特定表單元件。 作者可以搜尋物件，並從此樹狀結構重新排列。

   * **資料模型物件**
可讓您查看表單模型階層。
它可讓您在最適化表單上拖放表單模型元素。 新增的元素會自動轉換為表單元件，同時保留其原始屬性。 表單使用XML結構、JSON結構或XDP範本時，您可以看到資料模型物件。

* **屬性瀏覽器**

   可讓您編輯元件的屬性。 屬性會根據元件而變更。 若要查看適用性表單容器的屬性：

   選取元件，然後點選 ![欄位層級](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL 適用性表單容器]**，然後點選 ![屬性](assets/Smock_Wrench_18_N.svg).

* **資產瀏覽器**

   隔離不同類型的內容，例如影像、檔案、頁面、電影等。

* **元件瀏覽器**

   包括可用於建立最適化表單的元件。 您可以將元件從拖曳至適用性表單上，以新增表單元素，並依需求設定新增的元素。 下表說明元件瀏覽器中列出的元件。

<table>
 <tbody>
  <tr>
   <th><strong>元件</strong></th>
   <th><strong>功能</strong></th>
  </tr>
  <tr>
   <td>Adobe Sign 區塊</td>
   <td>新增文字區塊，其中包含使用Adobe Sign簽署時要填入欄位的預留位置。</td>
  </tr>
  <tr>
   <td>按鈕</td>
   <td>新增按鈕，您可以設定此按鈕以執行動作，例如儲存、重設、下一步、前一步等。</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>使用Google reCAPTCHA服務新增驗證碼。</td>
  </tr>
  <tr>
   <td>圖表</td>
   <td>新增圖表，供您在適用性Forms和檔案中使用，以可重複面板和表格列中的二維資料以視覺化方式呈現。</td>
  </tr>
  <tr>
   <td>核取方塊</td>
   <td>新增核取方塊。</td>
  </tr>
  <tr>
   <td>資料輸入欄位</td>
   <td>在表單中使用「日期輸入欄位」元件，讓客戶在三個方塊中分別填寫日、月和年。 您可以自訂元件的外觀和風格，並變更日期格式。 例如，您可以讓客戶輸入日期，格式為YYYY/MM/DD或DD/MM/YYYY。</td>
  </tr>
  <tr>
   <td>日期選擇器</td>
   <td>新增日曆欄位以挑選日期。</td>
  </tr>
  <tr>
   <td>文件片段</td>
   <td>可讓您新增可重複使用的通信元件。</td>
  </tr>
  <tr>
   <td>文件片段群組</td>
   <td>可讓您新增相關檔案片段群組，這些片段可作為單一單位用於信函範本中。</td>
  </tr>
  <tr>
   <td>下拉式清單</td>
   <td>新增下拉式清單 — 單選或多選</td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td><p>新增欄位以擷取電子郵件地址。 依預設，電子郵件元件會使用下列規則運算式來驗證電子郵件地址。</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td><p>添加一個按鈕，允許用戶瀏覽支援文檔並將其附加到表單。</p> <p><strong>注意： </strong>檔案附件元件支援針對Adobe Sign啟用的適用性Forms中預先定義的一組檔案格式。 如需詳細資訊，請參閱 <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">支援的檔案格式</a>.</p> </td>
  </tr>
  <tr>
   <td>檔案附件清單</td>
   <td>新增欄位，列出使用檔案附件元件上傳的所有附件。</td>
  </tr>
  <tr>
   <td>頁尾<br /> </td>
   <td>新增頁面標題，其中通常包含公司標誌、表單標題和摘要。<br /> </td>
  </tr>
  <tr>
   <td>頁首</td>
   <td>新增頁尾，其中通常包含版權資訊和其他頁面的連結。 </td>
  </tr>
  <tr>
   <td>影像</td>
   <td>讓您插入影像。</td>
  </tr>
  <tr>
   <td>影像選擇</td>
   <td>可讓客戶選取要提供資訊的影像。 您可以使用資訊為客戶提供個人化服務。</td>
  </tr>
  <tr>
   <td>下一個按鈕</td>
   <td>新增按鈕，以導覽至表單中的下一個面板。</td>
  </tr>
  <tr>
   <td>數值方塊</td>
   <td>新增擷取數值的欄位</td>
  </tr>
  <tr>
   <td>數值步進器</td>
   <td>使用窗體中的Numeric Stepper，讓客戶輸入一個數值，客戶可以根據預定義的步驟來增加或減少該值。</td>
  </tr>
  <tr>
   <td>面板</td>
   <td><p>新增面板或子面板。</p> <p>您也可以使用 <span class="uicontrol">添加子面板</code> 按鈕。 同樣地，您也可以使用 <span class="uicontrol">添加面板工具欄</code> 按鈕。 您可以使用「編輯面板」對話框配置面板工具欄的位置。</code></code></p> </td>
  </tr>
  <tr>
   <td>密碼框</td>
   <td>新增用於擷取密碼的欄位。</td>
  </tr>
  <tr>
   <td>上一個按鈕</td>
   <td>新增使用者返回上一頁或面板所需的按鈕。</td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td>添加單選按鈕。</td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>新增按鈕以重設表單欄位。</td>
  </tr>
  <tr>
   <td>儲存按鈕</td>
   <td>新增按鈕以儲存表單資料。</td>
  </tr>
  <tr>
   <td>手寫簽名</td>
   <td>新增擷取手寫簽名的欄位。</td>
  </tr>
  <tr>
   <td>分隔符號</td>
   <td>啟用表單中面板的視覺隔離。</td>
  </tr>
  <tr>
   <td>簽章步驟</td>
   <td>顯示表單中提供的資訊以及用戶驗證和簽名表單的簽名欄位。</td>
  </tr>
  <tr>
   <td>文字</td>
   <td>可讓您指定靜態文字。</td>
  </tr>
  <tr>
   <td>提交按鈕</td>
   <td>新增提交按鈕，將表單提交至設定的提交動作。</td>
  </tr>
  <tr>
   <td>摘要步驟</td>
   <td>提交表單並顯示作者在提交表單後指定的摘要文字。 </td>
  </tr>
  <tr>
   <td>切換</td>
   <td>添加執行切換或啟用/禁用操作的開關。 不能在Switch元件中添加兩個以上的選項。 由於交換機只能有兩個值：「開啟」或「關閉」，不適用強制項。 無論用戶輸入如何，都保存至少一個值。 <br /> </td>
  </tr>
  <tr>
   <td>表格</td>
   <td>新增表格以整理行和欄中的資料。 </td>
  </tr>
  <tr>
   <td>電話</td>
   <td><p>新增欄位以擷取電話號碼。 電話元件允許作者配置以下電話號碼類型之一。 每個類型都與驗證的預設規則運算式相關聯。</p>
    <ul>
     <li>「國際」類型通過 <code>^[+][0-9]{0,14}$</code>.</li>
     <li>類型USPhoneNumber由驗證 <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>類型UKPhoneNumber由驗證 <code>text{'+'99 999 999 9999}</code>.</li>
     <li>類型自訂不提供預設驗證模式。 它使用上次選擇的電話號碼類型的值。 您也可以指定自己的自訂驗證模式。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>條款和條件<br /> </td>
   <td>新增欄位，供作者在填寫表單前，用來指定使用者要檢閱的條款與條件。</td>
  </tr>
  <tr>
   <td>文字方塊 </td>
   <td><p>新增文字方塊，使用者可在其中指定所需資訊。 </p> <p>預設情況下，文本框元件僅接受純文字檔案。 您可以啟用文本框元件以接受RTF。 啟用RTF的文字元件提供可新增標題、變更字元樣式（粗體、斜體、加上字元底線）、建立有序和無序清單、變更文字背景和文字顏色，以及新增超連結的選項。 若要啟用文字方塊的RTF文字，請啟用<strong> 允許RTF文字</strong> 選項（在元件屬性中）。</p> </td>
  </tr>
  <tr>
   <td>標題</td>
   <td>指定適用性表單的標題。</td>
  </tr>
  <tr>
   <td>驗證步驟</td>
   <td><p>新增預留位置以顯示填入的表單供使用者驗證。</p> <p><strong>附註</strong>:包含驗證元件的適用性表單不支援匿名使用者。 此外，不建議在適用性表單片段中使用驗證元件。</p> </td>
  </tr>
 </tbody>
</table>

### 頁面工具列 {#page-toolbar}

頂端的頁面工具列提供可讓您預覽表單、變更表單屬性及編輯表單版面的選項。 您可以在製作表單時加以預覽，並據此進行變更。 在頁面工具列中，您會看到：

* **切換側面板** ![切換側面板](assets/Smock_RailLeft_18_N.svg):讓您顯示或隱藏側欄。

* **頁面資訊** ![主題選項](assets/Smock_Properties_18_N.svg):可讓您檢視頁面屬性、發佈/取消發佈表單、啟動表單工作流程，以及在傳統UI中開啟表單。

* **模擬器** ![尺標](assets/Smock_Devices_18_N.svg):可讓您針對不同的顯示大小（例如平板電腦和手機）模擬表單的外觀。

* **編輯**:可讓您選取其他模式，例如： **[!UICONTROL 編輯]**, **[!UICONTROL 樣式]**, **[!UICONTROL 開發人員]**，和 **[!UICONTROL 設計]**.

   * **編輯**:可讓您編輯表單及其元件的屬性。 例如，新增元件、拖放影像並指定必填欄位。
   * **樣式**:可讓您設定表單元件外觀的樣式。 例如，在樣式模式中，您可以選取面板並指定其背景顏色。

   * **開發人員**:讓開發人員：

      * 探索表單的組成。
      * 對發生在何處和何時的情況進行除錯，進而有助於解決問題。

      * **設計**. 可讓您啟用或停用自訂元件，或側邊欄中未列出的現成元件。

* **預覽**:可讓您預覽表單發佈時的外觀。

### 元件工具列 {#component-toolbar}

![觸控式UI中的元件工具列](assets/component-toolbar.png)

選取元件時，您會看到工具列可讓您使用它。 您可以獲得剪切、貼上、移動和指定元件屬性的選項。 您的選項為：

答：**設定**:當您點選 **[!UICONTROL 設定]**，元件屬性會顯示在側邊欄中。 設定這些屬性可讓您自訂資料擷取體驗。 您可以變更元件的元素名稱，在元件的「標題」欄位中指定標籤文字。 元素名稱可讓您擷取使用者使用元件輸入的值。 在元件屬性中，您可以指定元件的行為，並管理使用者輸入。 在側欄中設定屬性以擷取使用者資料，並用於進一步處理。 「最適化表單」容器的屬性可讓您指定用戶端程式庫、配置、主題、記錄檔案設定、儲存設定、提交設定和中繼資料設定。

B.**複製**:您可以使用複製選項來複製元件，並貼到表單中的其他位置。 貼上元件時，貼上的元件會獲得新的元素名稱，但會保留複製元件的屬性。

C.**剪下**:在「適用性表單」中，可以使用剪切選項將元件從一個位置移動到另一個位置。

D. **刪除**:可讓您從表單中刪除元件。

E. **插入**:可讓您在選取的元件上方插入元件。

F. **貼上**:可讓您使用上述選項來貼上您剪下或複製的元件。

G. **編輯規則**:可讓您開啟規則編輯器。 如需詳細資訊， <!-- see [Rule Editor](rule-editor.md). -->

H. **群組**:如果您想要剪下、複製或貼上多個元件，可讓您選取多個元件。

我。 **父級**:可讓您選取元件的父項。 例如，文字欄位位於區段中的子區段內，而子區段位於區段中。 區段位於指南根面板中，而適用性表單容器是指南根面板的父級。 對於元件，您可以看到所有選項，層次由下而上。

例如，如果您點選 **[!UICONTROL 父級]** 若為文字方塊，您會看到：

* 子區段
* 章節
* guideRootPanel
* 適用性表單容器

J. **其他**:提供更多選項以使用所選元件。

* 查看SOM表達式
* 將面板儲存為片段（僅適用於面板）
* 新增子面板（僅適用於面板）
* 新增面板工具列（僅適用於面板）
* 更換（不適用於面板）

### 適用性表單頁面 {#af-page}

適用性表單頁面是實際表單。 就像任何其他以WCM為模型的WCM頁面 `cq:Page` 元件。 下圖顯示典型自適性表單的內容結構。

![適用性表單WCM頁面的內容結構](assets/afstructure.png)

內容結構通常包含下列主要元件：

* **guideContainer**:適用性表單的根目錄，標示為 **[!UICONTROL 適用性表單開始]** 在適用性表單UI中。 在此元件中，您可以指定：

   * *最適化表單的行動版面*:定義行動裝置上表單的外觀。
   * *感謝頁面*:定義提交表單後，使用者被重新導向的頁面。
   * *提交動作*:定義當用戶提交表單後，如何在伺服器上處理表單。
   * *樣式*:指定用於自訂表單外觀的CSS檔案路徑。

* **rootPanel:** 適用性表單的根面板。 它可包含項目節點下的子面板。 每個面板（包括根面板）都可以有與其相關聯的版面。 面板的佈局指定如何佈置表單。 例如，在折疊式功能表版面中，其項目會排列為折疊式功能表步驟。

* **工具列：** 適用性表單容器具有與表單全域相關聯的全域工具列。 可使用 **[!UICONTROL 新增工具列]** 動作，可讓作者新增動作，例如提交、儲存、重設等。

* **資產：** 此節點包含用於表單編寫的其他資訊。 例如，表單模型詳細資訊、本地化詳細資訊等。
