---
title: 生成適應性Forms的記錄文檔
description: 說明如何為Adaptive Forms的記錄文檔(DoR)生成模板。
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: f75636c1b964c9edbc3e1dee937f3807e194c311
workflow-type: tm+mt
source-wordcount: '3678'
ht-degree: 2%

---

# 生成適應性Forms的記錄文檔

## 概覽 {#overview}

填寫或提交表單時，您可以以打印或文檔格式保留表單記錄。 此記錄稱為記錄文檔(DoR)。 它是已提交表單的打印友好副本。 您還可以參考記錄文檔，瞭解客戶在以後填寫的資訊，或使用記錄文檔以PDF格式將表單和內容一起存檔。

![記錄文件](assets/document-of-record.png)

要建立「記錄文檔」，將基於XFA或Acroform的模板與通過自適應表單收集的資料合併。 您可以自動或按需生成記錄文檔。
按需選項允許您指定基於自定義XFA或Acroform的模板，以為記錄文檔提供自定義外觀。

您可以：

* [生成基於XFA的記錄文檔](#generate-an-XFA-based-document-of-record)
* [生成基於頂層的(Acrobat表單PDF)記錄文檔](#generate-an-Acroform-based-document-of-record)
* [自動生成記錄文檔](#auto-generate-a-document-of-record)

## 開始之前 {#components-to-automatically-generate-a-document-of-record}

在開始學習並準備記錄文檔所需的資產之前：

**基本模板：** 在Forms設計器或Acrobat窗體(AcroForm)中建立的XFA模板（XDP檔案）。 [基本模板](#base-template-of-a-document-of-record) 用於為記錄文檔指定樣式和品牌資訊。 將XFA模板（XDP檔案）上載到AEM Forms實例之前

**自適應窗體：** 要為其生成記錄文檔的自適應表單。

## 生成基於XFA的記錄文檔 {#generate-an-XFA-based-document-of-record}

將XFA模板（XDP檔案）上載到您的AEM Forms實例。 執行以下步驟，將自適應表單配置為將XFA模板（XDP檔案）用作記錄文檔的模板：

1. 在Experience Manager作者實例中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]。**
1. 選擇表單，然後按一下 **[!UICONTROL 屬性]**。
1. 在「屬性」窗口中，按一下 **[!UICONTROL 窗體模型]**。
1. 在  **[!UICONTROL 窗體模型]** 的 **[!UICONTROL 從中選擇]** 下拉，選擇 **[!UICONTROL 架構]** 或 **[!UICONTROL 無]**。 建立表單時，也可選取表單模型。
1. 在「表單模型」頁籤的「記錄模板配置文檔」部分，選擇 **將表單模板與記錄模板文檔關聯**。 選擇此選項時，將顯示電腦上所有可用的XFA模板（XDP檔案）。 選擇相應的檔案。 另外，確保將同一模式（資料模式）用於自適應表單和選定的XFA模板（XDP檔案）。
1. 按一下 **[!UICONTROL 搞定。]**

現在，您的自適應表單已配置為將XDP檔案用作記錄文檔的模板。 下一步是 [使用相應的模板欄位綁定自適應表單元件](#bind-adaptive-form-components-with-template-fields)。

## 生成基於頂層的記錄文檔 {#generate-an-Acroform-based-document-of-record}

將您的Adobe AcrobatPDF(Acroform)上載到您的AEM Forms實例。 執行以下步驟，將自適應表單配置為將Adobe AcrobatPDF(Acroform)用作記錄文檔的模板：

1. 在Experience Manager作者實例中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]。**
1. 選擇表單，然後按一下 **[!UICONTROL 屬性]**。
1. 在「屬性」窗口中，按一下 **[!UICONTROL 窗體模型]**。
1. 在  **[!UICONTROL 窗體模型]** 的 **[!UICONTROL 從中選擇]** 下拉，選擇 **[!UICONTROL 架構]** 或 **[!UICONTROL 無]**。 建立表單時，也可選取表單模型。
1. 在「表單模型」頁籤的「記錄模板配置文檔」部分，選擇 **將表單模板與記錄模板文檔關聯**。 選擇此選項時，將顯示電腦上所有可用的AcrobatPDF（頂框）。 選擇相應的檔案。
1. 按一下 **[!UICONTROL 搞定。]**

您的自適應表單現在配置為將Acroform用作記錄文檔的模板。 下一步是 [使用相應的模板欄位綁定自適應表單元件](#bind-adaptive-form-components-with-template-fields)。

## 自動生成記錄文檔 {#auto-generate-a-document-of-record}

當自適應表單配置為自動生成記錄文檔時，每次更改表單時，其記錄文檔會立即更新。 例如，如果從現有自適應表單中刪除了欄位，則相應的欄位也會被刪除，並且在「記錄文檔」中不可見。 自動生成記錄文檔還有許多其他優點。 :

* 表單開發人員不必手動維護資料綁定。 自動生成的記錄文檔會處理與資料綁定相關的更新。
* 表單開發人員不必手動隱藏標籤為從記錄文檔中排除的欄位。 自動生成的記錄文檔已預先配置為排除此類欄位。
* 自動生成的「記錄文檔」選項可節省為「記錄文檔」建立表單模板所需的時間。
* 自動生成的「記錄文檔」(Document of Record)選項允許您使用不同的基本模板使用不同的造型和外觀。 它有助於為組織的「記錄文檔」選擇最佳樣式和外觀。 如果未指定樣式，則系統樣式將設定為預設樣式。
* 自動生成的記錄文檔可確保表單上的任何更改立即反映在記錄文檔中。

執行以下步驟來配置自適應表單以自動生成記錄文檔：

1. 在Experience Manager作者實例中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]。**
1. 選擇表單，然後按一下 **[!UICONTROL 屬性]**。
1. 在「屬性」窗口中，按一下 **[!UICONTROL 窗體模型]**。
1. 在  **[!UICONTROL 窗體模型]** 的 **[!UICONTROL 從中選擇]** 下拉，選擇 **[!UICONTROL 架構]** 或 **[!UICONTROL 無]**。 建立表單時，也可選取表單模型。
1. 在「表單模型」頁籤的「記錄模板配置文檔」部分，選擇 **生成記錄文檔**。
1. 按一下 **[!UICONTROL 搞定。]**

## 使用模板欄位綁定自適應表單元件 {#bind-adaptive-form-components-with-template-fields}

將「自適應表單」欄位與模板欄位綁定，以在相應的「記錄欄位文檔」中顯示捕獲的表單資料。 要將Adaptive Form元件與記錄模板欄位的相應文檔綁定，請執行以下操作：

1. 開啟「自適應表單」，該表單配置為使用自定義表單模板進行編輯。

1. 選擇一個Adaptive Form元件，然後按一下開啟「配置」 ![配置](assets/Smock_Wrench_18_N.svg) 表徵圖 它開啟屬性瀏覽器。

1. 在屬性瀏覽器中，瀏覽並選擇一個欄位。

   * （對於AcroForm模板） **[!UICONTROL 記錄綁定引用的文檔欄位]** 屬性。
   * （對於XFA模板） **[!UICONTROL 資料模型綁定引用]** 屬性。

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- 
In the following video Adaptive Form components are binded with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

您可以將「發送電子郵件」、「Experience Manager工作流」提交操作與 [記錄步驟的文檔和其他提交操作](configuring-submit-actions.md) 接收記錄文檔。

## 記錄文檔模板的增量更新 {#document-of-record-template-incremental-updates}

記錄模板的自適應形式和相應文檔可以在一段時間內演化。 您可以選擇將欄位添加、刪除或修改到「自適應表單」或「記錄文檔」模板。

當您對「記錄文檔」模板進行更改並將更改的「記錄文檔」模板上載到AEM Forms時，Adaptive Detior會自動檢測更改的綁定，並通知您需要新綁定的自適應表單元件。 它允許您對記錄文檔模板進行增量更新。

例如，組織， *We.Retail*，具有基於AcroForm的記錄文檔模板， *we-retail-invoice.pdf*。 模板如下所示：

![原始模板](assets/we-retail-invoice.png)

使用模板一段時間後，組織決定更名 `invoice-number` 欄位 `bill-number` 並捕獲買家的電子郵件地址。 開發人員更新 `invoice-number` 欄位，並向模板中添加一個電子郵件欄位。 他還建立了一個新版本的模板  *we-retail-invoice-v2.pdf*。

![更新的模板](assets/we-retail-new-invoice.png)

開發人員將上載並應用於更新的模板到自適應表單。 自適應表單自動檢測並顯示綁定已更改的欄位清單。

![綁定錯誤](assets/we-retail-binding-error.png)

表單開發者將Adaptive Forms欄位與相應的「記錄文檔」模板綁定。
>[!VIDEO](assets/we-retail-binding.mp4)

現在，在提交自適應表單時，將建立更新的記錄文檔。

![已更新-](assets/we-retail-new-invoice-sent-to-customer.png)

## 使用記錄文檔時的主要注意事項 {#key-considerations-when-working-with-document-of-record}

在處理適應性Forms的記錄文檔時，請記住以下考慮事項和限制。

* 記錄模板的文檔不支援RTF。 因此，靜態自適應表單或最終用戶填寫的資訊中的任何富文本都顯示為「記錄文檔」中的純文字檔案。
* 自適應表單中的文檔片段不會出現在記錄文檔中。 但是，支援自適應表單片段。
* 不支援為基於XML架構的自適應表單生成的記錄文檔中的內容綁定。
* 當用戶請求呈現記錄文檔時，將根據區域設定的要求建立記錄文檔的本地化版本。 記錄文檔的定位與自適應表單的定位同時進行。 <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## 自適應表單元素的映射 {#mapping-of-adaptive-form-elements}

下表介紹了Adaptive Form元件和相應的XFA元件，以及這些元件是否出現在「記錄文檔」中。

### 欄位 {#fields}

<table>
 <tbody>
  <tr>
   <th>自適應表單元件</th>
   <th>對應的XFA元件</th>
   <th>預設包含在記錄模板文檔中？</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>按鈕</td>
   <td>按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>複選框</td>
   <td>核取方塊</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期選取器</td>
   <td>日期/時間欄位</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉清單</td>
   <td>下拉式清單</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>簽名Scribble</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>數字框</td>
   <td>數字欄位</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>密碼框</td>
   <td>密碼欄位</td>
   <td>假</td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td>選項按鈕</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文字欄位</td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>重設按鈕</td>
   <td>假</td>
   <td> </td>
  </tr>
  <tr>
   <td>「提交」按鈕</td>
   <td><p>電子郵件提交按鈕</p> <p>HTTP提交按鈕</p> </td>
   <td>假</td>
   <td> </td>
  </tr>
  <tr>
   <td>條款和條件</td>
   <td> </td>
   <td>真</td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td> </td>
   <td>假</td>
   <td>記錄文檔模板中不可用。 僅通過附件在記錄文檔中可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>自適應表單元件</th>
   <th>對應的XFA元件</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子窗體<br /> </td>
   <td>可重複面板映射到可重複子窗體。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 自適應表單元件 | 對應的XFA元件 | 附註 |
|---|---|---|
| 影像 | 影像 | TextDraw和Image元件（無論綁定還是未綁定）始終出現在基於XSD的自適應表單的「記錄文檔」中，除非使用「記錄文檔」設定排除。 |
| 文字 | 文字 |

### 表 {#tables}

自適應Forms表元件（如頁眉、頁腳和行映射）映射到相應的XFA元件。 您可以將可重複面板映射到記錄文檔中的表。

## 記錄文檔的基本模板 {#base-template-of-a-document-of-record}

基本模板為「記錄文檔」提供樣式和外觀資訊。 它允許您自定義自動生成的記錄文檔的預設外觀。 例如，您可以使用基本模板將公司徽標添加到「記錄文檔」頁腳的頁眉和版權資訊中。

基本模板中的母版頁用作「記錄文檔」模板的母版頁。 母版頁可以包含可應用於「記錄文檔」的頁眉、頁腳和頁碼等資訊。 您可以使用基本模板將此類資訊應用於記錄文檔，以自動生成記錄文檔。 使用基本模板可更改欄位的預設屬性。

始終遵循 [基本模板約定](#base-template-conventions) 設計基模板。

## 基本模板約定 {#base-template-conventions}

基本模板用於定義「記錄文檔」的頁眉、頁腳、樣式和外觀。 頁眉和頁腳可以包括公司徽標和版權文本等資訊。 基本模板中的第一個母版頁被複製並用作「記錄文檔」的母版頁，該母版頁包含頁眉、頁腳、頁碼或應出現在「記錄文檔」中所有頁面的任何其他資訊。 如果使用的基本模板不符合基本模板約定，則基本模板的第一個母版頁仍用於「記錄文檔」模板。 強烈建議您根據基本模板的約定設計基本模板，並將其用於自動生成記錄文檔。

**母版頁約定**

* 在基本模板中，將根子表單命名為 `AF_METATEMPLATE` 母版頁 `AF_MASTERPAGE`。

* 具有名稱的母版頁 `AF_MASTERPAGE` 位於 `AF_METATEMPLATE` 根子表單是提取頁眉、頁腳和樣式資訊的首選。

* 如果 `AF_MASTERPAGE` 缺少，則使用基模板中存在的第一母版頁。

**域的樣式約定**

* 要對「記錄文檔」中的欄位應用樣式，基本模板將提供位於 `AF_FIELDSSUBFORM` 從 `AF_METATEMPLATE` 根子窗體。

* 這些欄位的屬性將應用於「記錄文檔」中的欄位。 這些欄位應跟在 `AF_<name of field in all caps>_XFO` 命名約定。 例如，複選框的欄位名應為 `AF_CHECKBOX_XFO`。

要建立基本模板，請在Forms設計器中執行以下操作。

1. 按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 新建]**。
1. 選擇 **[!UICONTROL 基於模板]** 的雙曲餘切值。

1. 選擇 **[!UICONTROL Forms — 記錄文檔]** 的子菜單。
1. 選擇 **[!UICONTROL DoR基本模板]**。
1. 按一下 **[!UICONTROL 下一個]** 提供所需資訊。

1. （可選）修改要應用於記錄文檔中欄位的欄位的樣式和外觀。
1. 保存窗體。

現在，您可以將保存的表單用作記錄文檔的基本模板。 不要修改或刪除基本模板中存在的任何指令碼。

**修改基本模板**

* 如果不對基本模板中的欄位應用任何樣式，則建議從基本模板中刪除這些欄位，以便自動提取對基本模板的任何升級。
* 修改基本模板時，不要刪除、添加或修改指令碼。

嚴格遵循上述約定和說明設計基本模板。

## 自定義記錄文檔中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

在生成記錄文檔時，您可以在「記錄文檔」頁籤上更改「記錄文檔」的品牌資訊。 「記錄文檔」頁籤包括徽標、外觀、佈局、頁眉和頁腳、免責聲明，以及是否要包括未選定的複選框和單選按鈕選項等選項。

要本地化您在「記錄文檔」頁籤中輸入的品牌資訊，請確保正確設定瀏覽器的區域設定。 要自定義記錄文檔的品牌資訊，請執行以下步驟：

1. 在「記錄文檔」中選擇一個面板（根面板），然後點擊 ![配置](assets/configure.png)。
1. 點擊 ![多拉](assets/dortab.png)。 此時將顯示「記錄文檔」頁籤。
1. 選擇預設模板或自定義模板以呈現記錄文檔。 如果選擇預設模板，則「記錄文檔」(Document of Record)的縮覽圖預覽會顯示在「模板」(Template)下拉菜單下方。

   ![品牌模板](assets/brandingtemplate.png)

   如果選擇選擇自定義模板，請瀏覽您的 [!DNL AEM Forms] 伺服器。 如果要使用尚未在上的模板 [!DNL AEM Forms] 伺服器，您應首先將XDP上載到 [!DNL AEM Forms] 伺服器。

1. 根據您是選擇預設模板還是自定義模板，「記錄文檔」頁籤中將顯示以下部分或全部屬性。 相應地指定以下項：

   * **徽標影像**:您可以選擇使用「自適應表單」中的徽標影像，從DAM中選擇一個，或從電腦上載一個。
   * **表單標題**
   * **頁首文字**
   * **免責聲明標籤**
   * **免責聲明**
   * **免責聲明文字**
   * **強調色**:在文檔或記錄PDF中呈現標題文本和分隔線的顏色
   * **字型系列**:記錄文檔中文本的字型系列PDF
   * **對於複選框和單選按鈕元件，只顯示所選值**
   * **所選多個值的分隔符號**
   * **包括未綁定到資料模型的表單對象**
   * **從記錄文檔中排除隱藏欄位**
   * **隱藏面板描述**

   >[!NOTE]
   >
   >如果使用使用6.3之前版本的Designer建立的Adaptive Form模板來使用「強調顏色」和「字型系列」屬性，請確保在根子表單下的Adaptive Form模板中存在以下內容：

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. 要保存品牌更改，請點擊「完成」。

## 記錄文檔中面板的表和列佈局 {#table-and-column-layouts-for-panels-in-document-of-record}

「自適應表單」可能是一個包含多個表單域的長表單。 您可能不想將「記錄文檔」保存為「自適應表單」的精確副本。 現在，您可以選擇表或列佈局，以在「記錄文檔」PDF中保存一個或多個「自適應表單」面板。

在生成記錄文檔之前，在面板的設定中，選擇該面板的記錄文檔的佈局作為表或列。 面板中的欄位在「記錄文檔」中相應地組織。

![在「記錄文檔」的表佈局中呈現的面板中的欄位](assets/dortablelayout.png)

在「記錄文檔」的表佈局中呈現的面板中的欄位

![在「記錄文檔」的列佈局中呈現的面板中的欄位](assets/dorcolumnlayout.png)

在「記錄文檔」的列佈局中呈現的面板中的欄位

## 記錄設定的文檔 {#document-of-record-settings}

「記錄文檔」設定允許您選擇要包括在「記錄文檔」中的選項。 例如，銀行接受表單中的姓名、年齡、社會保險號碼和電話號碼。 表單生成銀行帳號和分行詳細資訊。 您可以選擇在「記錄文檔」中僅顯示姓名、社會保險編號、銀行帳戶和分支詳細資訊。

「記錄文檔」元件的設定可在其屬性下使用。 要訪問元件的屬性，請選擇該元件並按一下 ![招商](assets/cmppr.png) 的上界。 這些屬性列在提要欄中，您可以在其中找到以下設定。

**欄位級別設定**

* **從記錄文檔中排除**:將屬性設定為true會從記錄文檔中排除該欄位。 這是名為的可指令碼的屬性 `excludeFromDoR`。 它的行為取決於 **如果隱藏，則從DoR中排除欄位** 窗體級別屬性。

* **以表格形式顯示面板：** 如果面板中的欄位少於6個，則將屬性設定為「記錄文檔」中的表格顯示面板。 僅適用於面板。
* **從記錄文檔中排除標題：** 設定屬性不包括「記錄文檔」中的面板/表的標題。 僅適用於面板和表。
* **從記錄文檔中排除說明：** 設定屬性不包括「記錄文檔」中對面板/表的說明。 僅適用於面板和表。

**表單級別設定**

* **在DoR中包括未綁定欄位：** 設定屬性包括記錄文檔中基於模式的自適應表單中的未綁定欄位。 預設情況下為true。
* **如果隱藏，則從DoR中排除欄位：** 設定屬性將覆蓋「從記錄文檔中排除」欄位級別屬性的行為（如果不為true）。 如果在提交表單時隱藏欄位，則如果屬性設定為true，則這些欄位將從「記錄文檔」中排除，前提是未設定「從記錄文檔中排除」屬性。

## 使用自定義XCI檔案

>[!NOTE]
>
> 此功能在預發行渠道中可用。 請參閱 [預發行渠道文檔](/help/release-notes/prerelease.md#enable-prerelease) 的子菜單。

XCI檔案可幫助您設定文檔的各種屬性。 Formsas a Cloud Service有主XCI檔案。 可以使用自定義XCI檔案覆蓋在主XCI檔案中指定的一個或多個預設屬性。 例如，您可以選擇將字型嵌入文檔或為所有文檔啟用標籤屬性。 下表指定了XCI選項：

| XCI選項 | 說明 |
|--- |--- |
| 配置/呈現/pdf/建立者 | 使用「文檔資訊」字典中的「建立者」條目標識文檔建立者。 有關此詞典的資訊，請參閱 [PDF參考指南](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/pdf_reference_archives/PDFReference.pdf)。 |
| 配置/存在/pdf/製作者 | 使用「文檔資訊」字典中的「製作者」條目標識文檔製作者。 有關此詞典的資訊，請參閱 [PDF參考指南](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/pdf_reference_archives/PDFReference.pdf)。 |
| 配置/現在/佈局 | 控制輸出是單個面板還是分頁。 |
| 配置/存在/pdf/壓縮/級別 | 指定生成PDF文檔時要使用的壓縮程度。 |
| config/present/pdf/fontInfo/embed | 控制輸出文檔中的字型嵌入。 |
| config/present/pdf/script模型 | 控制是否將XFA特定資訊包含在輸出PDF文檔中。 |
| config/present/common/data/adjustData | 控制XFA應用程式是否在合併後調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的生成是在伺服器上完成還是延遲到客戶端。 |
| 配置/現在/常用/區域設定 | 指定在輸出文檔中使用的預設區域設定。 |
| 配置/存在/目標 | 當當前元素包含時，指定輸出格式。 當openAction元素包含時，指定在互動式客戶端中開啟文檔時要執行的操作。 |
| 配置/存在/輸出/類型 | 指定要應用於檔案的壓縮類型或要生成的輸出類型。 |
| 配置/當前/常/溫/uri | 指定窗體URI。 |
| 配置/現在/常用/模板/基本 | 為窗體設計中的URI提供基本位置。 當此元素不存在或為空時，窗體設計的位置將用作基礎。 |
| 配置/存在/公用/日誌/收件人 | 控制日誌資料或輸出資料寫入的位置。 |
| 配置/提供/輸出/到 | 控制日誌資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟文檔時的初始頁面。 |
| 配置/現在/指令碼/排除 | 通知Formsas a Cloud Service要忽略哪些事件。 |
| 配置/現在/pdf/線性化 | 控制輸出PDF文檔是否線性化。 |
| config/present/script/runScripts | 控制Formsas a Cloud Service執行的指令碼集。 |
| 配置/呈現/pdf/加標籤 | 控制將標籤包含到輸出PDF文檔中。 在PDF的上下文中，標籤是文檔中包含的用於公開文檔邏輯結構的附加資訊。 標籤有助於輔助輔助工具和重新格式化。 例如，頁碼可以被標籤為項目，以便螢幕閱讀器不會在文本的中間清晰它。 儘管標籤使文檔更有用，但它們也增加了文檔的大小和建立文檔的處理時間。 |
| config/present/pdf/fontInfo/alwaysEmbed | 指定嵌入到輸出文檔中的字型。 |
| config/present/pdf/fontInfo/neverEmbed | 指定永遠不能嵌入到輸出文檔中的字型。 |
| 配置/呈現/pdf/pdfa/部件 | 指定文檔所遵循的PDF/A規範的版本號。 |
| config/present/pdf/pdfa/amd | 指定PDF/A規範的修改級別。 |
| 配置/提供/pdf/pdfa/符合性 | 指定符合PDF/A規格的級別。 |
| 配置/提供/pdf/版本 | 指定要生成的PDF文檔的版本 |
| 配置/現在/pdf/版本/地圖 | 指定文檔的回退字型 |

### 在您的Formsas a Cloud Service環境中使用自定義XCI檔案

1. 將自定義XCI檔案添加到開發項目。
1. 指定以下內容 [inline屬性](/help/implementing/deploying/configuring-osgi.md):

   ```JSON
    {
     "xciFilePath": "[path of XCI file]"
    }
   ```

   例如，

   ```JSON
    {
     "xciFilePath": "/content/dam/formsanddocuments/customMinionProBoldAndTagged.xci"
    }
   ```

1. 將項目部署到您的Cloud Service環境。

### 在本地Formsas a Cloud Service開發環境中使用自定義XCI檔案

1. 將XCI檔案上載到本地開發環境。
1. 開啟Cloud ServiceSDK配置管理器。 預設URL為： <http://localhost:4502/system/console/configMgr>。
1. 查找並開啟 **[!UICONTROL 自適應Forms與交互通信Web通道]** 配置。
1. 指定XCI檔案的路徑，然後按一下 **[!UICONTROL 保存]**。
