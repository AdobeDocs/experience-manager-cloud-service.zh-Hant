---
title: 創作簡介自適應Forms
seo-title: Introduction to authoring Adaptive Forms
description: AEM Forms為創作AdaptiveForms提供了易於使用但功能強大的介面。 它提供了許多可用於生成表單的元件和工具。
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


# 自適應Forms編輯器 {#introduction-to-authoring-adaptive-forms}

## 概覽 {#overview}

自適應Forms允許您建立具有吸引力、響應性、動態性和適應性的表單。 [!DNL AEM Forms] 提供了直觀的用戶介面和開箱即用的元件，用於建立和使用AdaptiveForms。 您可以選擇基於表單模型或模式或不使用表單模型建立自適應表單。 必須仔細選擇不僅適合您的要求，而且擴展您現有的基礎設施投資和資產的表單模式。 您可以從以下選項中進行選擇以建立自適應表單：

<!-- * **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source. -->

* **使用XDP表單模板**
如果您在基於XFA或XDP的表單中進行投資，則它是理想的表單模型。 它提供了將基於XFA的表單轉換為自適應Forms的直接方法。 任何現有的XFA規則都保留在關聯的自適應Forms中。 生成的自適應Forms支援XFA構造，如驗證、事件、屬性和模式。

* **使用XML架構定義(XSD)或JSON架構**
XML和JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 創作自適應Forms時，模式的元素將可用於內容瀏覽器的「資料模型對象」頁籤中。

* **使用無或沒有表單模型**
使用此選項建立的自適應Forms不使用任何窗體模型。 從這些表單生成的資料XML具有帶欄位和相應值的扁平結構。

<!--  For more information about creating an Adaptive Form, see [Creating an Adaptive Form](creating-adaptive-form.md). -->

## 自適應表單創作UI {#adaptive-form-authoring-ui}

用於創作自適應Forms的觸控優化UI是直觀的，它提供：

* 拖放功能
* 標準表單元件
* 整合的資產儲存庫

在建立新的或編輯現有的自適應表單時，可使用以下UI元素：

* [側欄](#sidebar)
* [頁面工具欄](#page-toolbar)
* [元件工具欄](#component-toolbar)
* [「自適應表單」頁](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### 側欄 {#sidebar}

提要欄允許您

* 搜索、查看和使用數字資產管AEM理(DAM)儲存庫中的資產。
* 請參閱表單內容，如面板、元件、欄位和佈局。
* 在窗體上添加元件。
* 編輯元件屬性。

![側欄](assets/sidebar-comps.png)

**答：** 內容瀏覽器 **B** 屬性瀏覽器 **C.** 資產瀏覽器 **D** 元件瀏覽器

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

邊欄包括以下瀏覽器：

* **內容瀏覽器**
在內容瀏覽器中，您可以看到：

   * **窗體對象**
顯示窗體的對象層次結構。 作者可以在「表單對象樹」中按一下該元素來導航到特定的表單元件。 作者可以搜索對象，並從此樹中重新排列對象。

   * **資料模型對象**
用於查看表單模型層次結構。
它允許您在自適應表單上拖放表單模型元素。 添加的元素在保留其原始屬性的同時自動轉換為表單元件。 當表單使用XML架構、JSON架構或XDP模板時，可以看到資料模型對象。

* **屬性瀏覽器**

   用於編輯元件的屬性。 屬性會根據元件更改。 要查看「自適應表單」容器的屬性：

   選擇元件，然後點擊 ![欄位級](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL 自適應窗體容器]**，然後按一下 ![屬性](assets/Smock_Wrench_18_N.svg)。

* **資產瀏覽器**

   隔離不同類型的內容，如影像、文檔、頁面、電影等。

* **元件瀏覽器**

   包括可用於構建自適應表單的元件。 您可以將元件從拖動到「自適應表單」上以添加表單元素，並根據要求配置添加的元素。 下表介紹了元件瀏覽器中列出的元件。

<table>
 <tbody>
  <tr>
   <th><strong>元件</strong></th>
   <th><strong>功能</strong></th>
  </tr>
  <tr>
   <td>Adobe Sign 區塊</td>
   <td>使用Adobe Sign簽名時，為要填充的欄位添加帶佔位符的文本塊。</td>
  </tr>
  <tr>
   <td>按鈕</td>
   <td>添加一個按鈕，您可以將其配置為執行操作，如保存、重置、下一步、上一步等。</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>使用GooglereCAPTCHA服務添加驗證碼驗證。</td>
  </tr>
  <tr>
   <td>圖表</td>
   <td>添加一個圖表，可在Adaptive Forms和文檔中使用，以便在可重複面板和表行中直觀地表示二維資料。</td>
  </tr>
  <tr>
   <td>複選框</td>
   <td>添加複選框。</td>
  </tr>
  <tr>
   <td>資料輸入欄位</td>
   <td>使用表單中的「日期輸入欄位」元件，讓客戶在三個框中分別填寫日、月和年。 可以定制元件的外觀，並更改日期格式。 例如，您可以讓客戶以MM/DD/YYYY或DD/MM/YYYY格式輸入日期。</td>
  </tr>
  <tr>
   <td>日期選取器</td>
   <td>添加日曆欄位以選擇日期。</td>
  </tr>
  <tr>
   <td>文件片段</td>
   <td>允許您添加可重用的對應元件。</td>
  </tr>
  <tr>
   <td>文件片段群組</td>
   <td>允許您添加相關文檔片段組，這些文檔片段可以作為單個單元在字母模板中使用。</td>
  </tr>
  <tr>
   <td>下拉清單</td>
   <td>添加下拉清單 — 單選或多選</td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td><p>添加欄位以捕獲電子郵件地址。 預設情況下，電子郵件元件使用以下規則運算式驗證電子郵件地址。</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td><p>添加一個按鈕，允許用戶瀏覽支援文檔並將其附加到表單。</p> <p><strong>注： </strong>「檔案附件」元件支援為Adobe Sign啟用的Adaptive Forms中預定義的一組檔案格式。 有關詳細資訊，請參見 <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">支援的檔案格式</a>。</p> </td>
  </tr>
  <tr>
   <td>檔案附件清單</td>
   <td>添加一個欄位，列出使用「檔案附件」元件上載的所有附件。</td>
  </tr>
  <tr>
   <td>頁尾<br /> </td>
   <td>添加通常包括公司徽標、表單標題和摘要的頁眉。<br /> </td>
  </tr>
  <tr>
   <td>頁首</td>
   <td>添加通常包含版權資訊的頁腳和指向其他頁面的連結。 </td>
  </tr>
  <tr>
   <td>影像</td>
   <td>讓您插入影像。</td>
  </tr>
  <tr>
   <td>影像選擇</td>
   <td>允許您的客戶選擇要提供資訊的影像。 您可以使用資訊為客戶提供個性化服務。</td>
  </tr>
  <tr>
   <td>下一個按鈕</td>
   <td>添加按鈕以導航到窗體中的下一個面板。</td>
  </tr>
  <tr>
   <td>數字框</td>
   <td>添加用於捕獲數字值的欄位</td>
  </tr>
  <tr>
   <td>數值步進器</td>
   <td>在窗體中使用數字步進器，讓客戶輸入數字值，客戶可以根據預定義的步驟增加或減少數值。</td>
  </tr>
  <tr>
   <td>面板</td>
   <td><p>添加面板或子面板。</p> <p>也可以使用 <span class="uicontrol">添加子面板</code> 按鈕 同樣，可以使用 <span class="uicontrol">添加面板工具欄</code> 按鈕 可以使用「編輯面板」對話框配置面板工具欄的位置。</code></code></p> </td>
  </tr>
  <tr>
   <td>密碼框</td>
   <td>添加用於捕獲密碼的欄位。</td>
  </tr>
  <tr>
   <td>「上一個」按鈕</td>
   <td>添加用戶需要返回上一頁或面板的按鈕。</td>
  </tr>
  <tr>
   <td>單選按鈕</td>
   <td>添加單選按鈕。</td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>添加按鈕以重置表單域。</td>
  </tr>
  <tr>
   <td>儲存按鈕</td>
   <td>添加按鈕以保存表單資料。</td>
  </tr>
  <tr>
   <td>Scribble簽名</td>
   <td>添加用於捕獲手寫簽名的欄位。</td>
  </tr>
  <tr>
   <td>分隔符號</td>
   <td>啟用窗體中面板的可視隔離。</td>
  </tr>
  <tr>
   <td>簽章步驟</td>
   <td>顯示表單中提供的資訊以及用戶驗證和簽名表單的簽名欄位。</td>
  </tr>
  <tr>
   <td>文字</td>
   <td>允許您指定靜態文本。</td>
  </tr>
  <tr>
   <td>提交按鈕</td>
   <td>添加提交按鈕以將表單提交到配置的提交操作。</td>
  </tr>
  <tr>
   <td>摘要步驟</td>
   <td>提交表單並顯示提交表單後作者指定的摘要文本。 </td>
  </tr>
  <tr>
   <td>切換</td>
   <td>添加執行切換或啟用/禁用操作的交換機。 在Switch元件中不能添加兩個以上的選項。 由於交換機只能有兩個值：「開啟」或「關閉」，不適用強制。 不管用戶輸入如何，至少保存一個值。 <br /> </td>
  </tr>
  <tr>
   <td>表格</td>
   <td>新增表格以整理行和欄中的資料。 </td>
  </tr>
  <tr>
   <td>電話</td>
   <td><p>添加欄位以捕獲電話號碼。 電話元件允許作者配置以下電話號碼類型之一。 每種類型都與用於驗證的預設規則運算式相關聯。</p>
    <ul>
     <li>類型國際由驗證者 <code>^[+][0-9]{0,14}$</code>。</li>
     <li>類型USPhoneNumber由驗證者 <code>{'+1 ('999') '999-9999}</code>。</li>
     <li>類型UKPhoneNumber由驗證者 <code>text{'+'99 999 999 9999}</code>。</li>
     <li>類型自定義不提供預設驗證模式。 它採用上一個選定電話號碼類型的值。 您也可以指定自己的自定義驗證模式。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>條款和條件<br /> </td>
   <td>添加一個欄位，作者可以使用該欄位指定在填寫表單之前用戶要查看的條款和條件。</td>
  </tr>
  <tr>
   <td>文本框 </td>
   <td><p>添加一個文本框，用戶可以在其中指定所需資訊。 </p> <p>預設情況下，「文本框」元件只接受純文字檔案。 您可以啟用文本框元件來接受富格文本。 啟用富格文本的文本元件提供了添加頁眉、更改字元樣式（粗體、斜體、下划線字元）、建立有序清單和未排序清單、更改文本背景和文本顏色以及添加超連結的選項。 要為文本框啟用RTF，請啟用<strong> 允許富格文本</strong> 的子菜單。</p> </td>
  </tr>
  <tr>
   <td>標題</td>
   <td>指定自適應表單的標題。</td>
  </tr>
  <tr>
   <td>驗證步驟</td>
   <td><p>添加一個佔位符以顯示已填充的表單以供用戶驗證。</p> <p><strong>注釋</strong>:包含Verify元件的Adaptive Form不支援匿名用戶。 此外，建議不要在自適應表單片段中使用「驗證」元件。</p> </td>
  </tr>
 </tbody>
</table>

### 頁面工具欄 {#page-toolbar}

頂部的頁面工具欄提供了一些選項，可用於預覽表單、更改表單屬性和編輯表單佈局。 在建立表單時，可以預覽該表單，並相應地進行更改。 在頁面工具欄中，您會看到：

* **切換側面板** ![切換側面板](assets/Smock_RailLeft_18_N.svg):用於顯示或隱藏邊欄。

* **頁面資訊** ![主題選項](assets/Smock_Properties_18_N.svg):用於查看頁面屬性、發佈/取消發佈表單、啟動表單工作流，以及在標準UI中開啟表單。

* **模擬器** ![尺](assets/Smock_Devices_18_N.svg):讓您模擬不同顯示尺寸（如平板電腦和手機）的表格外觀。

* **編輯**:允許您選擇其它模式，如： **[!UICONTROL 編輯]**。 **[!UICONTROL 樣式]**。 **[!UICONTROL 開發人員]**, **[!UICONTROL 設計]**。

   * **編輯**:用於編輯窗體及其元件的屬性。 例如，添加元件、刪除影像並指定必需欄位。
   * **樣式**:允許您設定窗體元件外觀的樣式。 例如，在樣式模式下，可以選擇面板並指定其背景顏色。

   * **開發人員**:允許開發人員：

      * 查看由哪些形式構成。
      * 調試在何處和何時發生的情況，這反過來有助於解決問題。

      * **設計**. 用於啟用或禁用自定義元件或未列在提要欄中的現成元件。

* **預覽**:用於預覽發佈表單時窗體的外觀。

### 元件工具欄 {#component-toolbar}

![觸摸UI中的元件工具欄](assets/component-toolbar.png)

選擇元件時，將看到一個工具欄，可以使用它。 您可以獲取剪切、貼上、移動和指定元件屬性的選項。 您的選項包括：

答：**配置**:點擊 **[!UICONTROL 配置]**，元件屬性在邊欄中可見。 通過配置這些屬性，您可以定制資料捕獲體驗。 可以更改元件的元素名稱，在元件的「標題」欄位中指定標籤文本。 元素名稱用於捕獲用戶使用元件輸入的值。 在元件屬性中，指定元件的行為並管理用戶輸入。 在提要欄中配置屬性以捕獲用戶資料，並使用它進行進一步處理。 Adaptive Form容器的屬性允許您指定客戶端庫、佈局、主題、記錄文檔設定、保存設定、提交設定和元資料設定。

B **複製**:可以使用複製選項複製元件並將其貼上到窗體中的其他位置。 貼上元件時，貼上的元件將獲取新的元素名稱，但保留複製元件的屬性。

C.**剪切**:在「自適應表單」中，可使用剪切選項將元件從一個位置移動到另一個位置。

D **刪除**:用於從表單中刪除元件。

E. **插入**:用於在選定元件上方插入元件。

F. **貼上**:允許您使用上述選項貼上剪切或複製的元件。

G. **編輯規則**:用於開啟規則編輯器。 有關詳細資訊， <!-- see [Rule Editor](rule-editor.md). -->

H **組**:如果要剪切、複製或貼上多個元件，則允許您選擇多個元件。

我。 **父級**:用於選擇元件的父項。 例如，文本欄位位於子節內，子節位於節內。 該節位於指南根面板中，而「自適應表單」容器是指南根面板的父級。 對於元件，您可以看到所有選項，這些選項都按自下而上的層次排序。

例如，如果您點擊 **[!UICONTROL 父級]** 在文本框中，您可以看到：

* 分節
* 章節
* guideRootPanel
* 自適應窗體容器

J **其他**:提供更多選項以使用所選元件。

* 查看SOM表達式
* 將面板另存為片段（僅適用於面板）
* 添加子面板（僅適用於面板）
* 添加面板工具欄（僅適用於面板）
* 更換（不適用於面板）

### 「自適應表單」頁 {#af-page}

「自適應表單」頁是實際表單。 它與任何其它WCM頁面一樣， `cq:Page` 元件。 下圖顯示了典型自適應表單的內容結構。

![自適應表單WCM頁的內容結構](assets/afstructure.png)

內容結構通常包含以下主要元件：

* **指南容器**:自適應表單的根，標籤為 **[!UICONTROL 自適應表單的開始]** 的子菜單。 在此元件中，可以指定：

   * *自適應表單的移動佈局*:定義移動設備上窗體的外觀。
   * *「謝謝」頁*:定義提交表單後用戶重定向的頁面。
   * *提交操作*:定義用戶提交表單後在伺服器上處理表單的方式。
   * *造型*:指定用於自定義窗體外觀的CSS檔案的路徑。

* **rootPanel:** 自適應表單的根面板。 它可以包含項目節點下的子面板。 包括根面板的每個面板都可以具有與其相關聯的佈局。 該面板的佈局指示了如何佈置該形式。 例如，在折疊面板佈局中，其項目以折疊式步驟佈置。

* **工具欄：** 「自適應表單」容器具有與表單全局的關聯全局工具欄。 可以使用 **[!UICONTROL 添加工具欄]** 編輯欄中的操作，允許作者添加操作，如提交、保存、重置等。

* **資產：** 此節點包含用於表單創作的附加資訊。 例如，表單模型詳細資訊、本地化詳細資訊等。
