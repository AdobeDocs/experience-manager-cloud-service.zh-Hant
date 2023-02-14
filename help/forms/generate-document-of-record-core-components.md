---
title: 產生最適化Forms的記錄檔案
description: 說明如何為適用性Forms的記錄檔案(DoR)產生範本。
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: b0e49296344a4f52a07699a308eb0cbeef897bb9
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 1%

---

# 產生最適化Forms（核心元件）的記錄檔案

## 概觀 {#overview}

填寫或提交表單時，您可以以打印或文檔格式保存表單記錄。 此記錄稱為記錄檔案(DoR)。 這是已提交表單的可打印副本。 您也可以參考記錄檔案，了解客戶在以後填寫的資訊，或使用記錄檔案將表單和內容以PDF格式一起歸檔。

![記錄文件](assets/document-of-record.png)

若要建立記錄檔案，系統會將XFA或Acroform範本與透過最適化表單收集的資料合併。 您可以自動或按需生成記錄文檔。 隨需選項可讓您指定自訂XFA或Acroform範本，為記錄檔案提供自訂外觀。

您可以：

* [生成基於XFA的記錄文檔](#generate-an-XFA-based-document-of-record)
* [生成基於Acroform(Acrobat表單PDF)的記錄文檔](#generate-an-Acroform-based-document-of-record)
* [自動生成記錄文檔](#auto-generate-a-document-of-record)

## 開始之前 {#components-to-automatically-generate-a-document-of-record}

開始學習並準備記錄檔案所需的資產之前：

**基本模板：** 在Forms Designer或Acrobat表單(AcroForm)中建立的XFA範本（XDP檔案）。 [基礎範本](#base-template-of-a-document-of-record) 用於指定記錄文檔的樣式和品牌資訊。 先將XFA範本（XDP檔案）上傳至AEM Forms執行個體。

**適用性表單：** 要為其生成記錄文檔的最適化表單。

## 生成基於XFA的記錄文檔 {#generate-an-XFA-based-document-of-record}

上傳XFA範本（XDP檔案）至AEM Forms執行個體。 執行下列步驟來設定適用性表單，以使用XFA範本（XDP檔案）作為記錄檔案的範本：

1. 在Experience Manager製作例項中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案].**
1. 選取表單或建立最適化表單，然後按一下 **[!UICONTROL 屬性]**.
1. 在「屬性」視窗中，點選 **[!UICONTROL 表單模型]**.
1. 在  **[!UICONTROL 表單模型]** 標籤中 **[!UICONTROL 從]** 下拉式清單，選取 **[!UICONTROL 表單資料模型]**, **[!UICONTROL 結構]** 或 **[!UICONTROL 無]**. 建立表單時，也可以選取表單模型。
1. 在「表單模型」頁簽的「記錄模板配置文檔」部分中，選擇 **將表單模板與記錄模板文檔關聯**. 選取此選項時，會顯示您電腦上可用的所有XFA範本（XDP檔案）。 選取適當的檔案。 此外，請確認適用性表單和選取的XFA範本（XDP檔案）使用相同的結構描述（資料結構描述）。
1. 按一下 **[!UICONTROL 完成。]**

您的適用性表單現在已設定為使用XDP檔案作為記錄檔案的範本。 接下來的步驟是 [使用對應的範本欄位系結適用性表單元件](#bind-adaptive-form-components-with-template-fields).

## 生成基於Acroform的記錄文檔 {#generate-an-Acroform-based-document-of-record}

將Adobe AcrobatPDF(Acroform)上傳至AEM Forms執行個體。 執行下列步驟來設定適用性表單，以使用Adobe AcrobatPDF(Acroform)作為記錄檔案的範本：

1. 在Experience Manager製作例項中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案].**
1. 選取表單或 **[!UICONTROL 建立最適化表單]**，然後按一下 **[!UICONTROL 屬性]**.
1. 在「屬性」視窗中，點選 **[!UICONTROL 表單模型]**.
1. 在  **[!UICONTROL 表單模型]** 標籤中 **[!UICONTROL 從]** 下拉式清單，選取 **[!UICONTROL 表單資料模型]**, **[!UICONTROL 結構]** 或 **[!UICONTROL 無]**. 建立表單時，也可以選取表單模型。
1. 在「表單模型」頁簽的「記錄模板配置文檔」部分中，選擇 **將表單模板與記錄模板文檔關聯**. 選取此選項時，會顯示您電腦上可用的所有AcrobatPDF(Acroform)。 選取您要使用的對應表單。
1. 按一下 **[!UICONTROL 完成。]**

您的適用性表單現在已設定為使用Acroform作為記錄檔案的範本。 接下來的步驟是 [使用對應的範本欄位系結適用性表單元件](#bind-adaptive-form-components-with-template-fields).

## 自動生成記錄文檔 {#auto-generate-a-document-of-record}

當適用性表單配置為自動生成記錄文檔時，每次更改表單時，其記錄文檔都會立即更新。 例如，如果從現有的最適化表單中移除欄位，則也會移除對應欄位，且在記錄檔案中不會顯示。 自動生成記錄文檔還有許多其他優點：

* 表單開發人員不必手動維護資料綁定。 自動產生的記錄檔案會處理資料系結相關的更新。
* 表單開發人員不必手動隱藏標示為從記錄檔案中排除的欄位。 預先配置自動生成的記錄文檔以排除此類欄位。
* 自動生成的記錄文檔選項可節省為記錄文檔建立表單模板所需的時間。
* 自動生成的「記錄文檔」選項允許您使用不同的基模板來使用不同的樣式和外觀。 它有助於為貴組織的記錄檔案選擇最佳樣式和外觀。 如果未指定樣式，系統樣式將設定為預設樣式。
* 自動生成的記錄文檔可確保任何形式更改立即反映在記錄文檔中。

執行下列步驟來設定適用性表單以自動產生記錄檔案：

1. 在Experience Manager製作例項中，按一下 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案].**
1. 選取表單或建立最適化表單，然後按一下 **[!UICONTROL 屬性]**.
1. 在「屬性」視窗中，點選 **[!UICONTROL 表單模型]**.
1. 在  **[!UICONTROL 表單模型]** 標籤中 **[!UICONTROL 從]** 下拉式清單，選取 **[!UICONTROL 表單資料模型]**, **[!UICONTROL 結構]** 或 **[!UICONTROL 無]**. 建立表單時，也可以選取表單模型。
1. 在「表單模型」頁簽的「記錄模板配置文檔」部分中，選擇 **生成記錄文檔**.
1. 按一下 **[!UICONTROL 完成。]**

## 使用範本欄位系結適用性表單元件 {#bind-adaptive-form-components-with-template-fields}

將適用性表單欄位與範本欄位系結，以在對應的記錄欄位檔案中顯示擷取的表單資料。 要將適用性表單元件與記錄模板欄位的相應文檔綁定，請執行以下操作：

1. 開啟最適化表單，此表單設定為使用自訂表單範本進行編輯。

1. 選取適用性表單元件，然後按一下開啟「設定」 ![設定](assets/Smock_Wrench_18_N.svg) 表徵圖。 它會開啟屬性瀏覽器。

1. 在屬性瀏覽器中，瀏覽並選取欄位。

   * （AcroForm範本） **[!UICONTROL 記錄綁定引用欄位的文檔]** 屬性。
   * （XFA範本） **[!UICONTROL 資料模型系結參考]** 屬性。

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- 
In the following video Adaptive Form components are binded with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

您可以使用「傳送電子郵件」、「叫用AEM工作流程」、「叫用電源自動化流程」等提交動作 [提交操作](configuring-submit-actions.md) 接收記錄檔。
![影像提交動作](/help/forms/assets/submit-actions-img.png)



## 記錄文檔模板的增量更新 {#document-of-record-template-incremental-updates}

記錄模板的最適化表單和相應文檔可以隨著時間而變化。 您可以選擇將欄位添加、刪除或修改至「最適化表單」或「記錄文檔」模板。

當您對「記錄文檔」模板進行更改並將更改的「記錄文檔」模板上載到AEM Forms時，適用性Forms編輯器會自動檢測更改的綁定，並通知您需要新綁定的適用性表單元件。 它允許您對記錄文檔模板進行增量更新。

例如，組織， *We.Retail*，具有基於AcroForm的記錄文檔模板， *we-retail-invoice.pdf*. 範本如下所示：

![原始範本](assets/we-retail-invoice.png)

使用範本一段時間後，組織決定重新命名 `invoice-number` 欄位至 `bill-number` 欄位並擷取購買者的電子郵件地址。 開發人員會更新 `invoice-number` 欄位並新增電子郵件欄位至範本。 他還建立了新版的模板，稱為  *we-retail-invoice-v2.pdf*.

![更新的範本](assets/we-retail-new-invoice.png)

<!--

The developer uploads and applies to the updated template to the adaptive form. The adaptive form automatically detects and displays list of fields where binding has changed.

![Binding Error](assets/we-retail-binding-error.png)

The form developer binds Adaptive Forms fields with corresponding Document of Record template.

-->

>[!VIDEO](assets/we-retail-binding.mp4)

現在，提交適用性表單時，會產生更新的記錄檔案。

![已更新-](assets/we-retail-new-invoice-sent-to-customer.png)

## 使用記錄檔案時的主要考量 {#key-considerations-when-working-with-document-of-record}

處理適用性Forms的記錄檔案時，請記住下列考量事項和限制。

* 記錄模板文檔不支援RTF。 因此，靜態適用性表單或一般使用者填入的資訊中的任何RTF文字都會在記錄檔案中顯示為純文字。
* 最適化表單中的檔案片段不會出現在記錄檔案中。 不過，也支援最適化表單片段。
* 不支援為基於XML架構的適用性表單生成的記錄文檔中的內容綁定。
* 當用戶請求呈現記錄文檔時，將根據地區設定的要求建立記錄文檔的本地化版本。 記錄文檔的本地化與最適化表單的本地化同時發生。 <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## 最適化表單元素的對應 {#mapping-of-adaptive-form-elements}

下表說明適用性表單元件和對應的XFA元件，以及這些元件是否出現在記錄檔案中。

### 欄位 {#fields}

<table>
 <tbody>
  <tr>
   <th>適用性表單元件</th>
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
   <td>核取方塊</td>
   <td>核取方塊</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期選擇器</td>
   <td>日期/時間欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉式清單</td>
   <td>下拉式清單</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>數值方塊</td>
   <td>數值欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td>選項按鈕</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文字方塊</td>
   <td>文字欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>重設按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>提交按鈕</td>
   <td><p>電子郵件提交按鈕</p> <p>HTTP提交按鈕</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td> </td>
   <td>false</td>
   <td>在記錄文檔模板中不可用。 僅在記錄文檔中通過附件可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>適用性表單元件</th>
   <th>對應的XFA元件</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表單<br /> </td>
   <td>可重複面板對應至可重複的子表單。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 適用性表單元件 | 對應的XFA元件 | 附註 |
|---|---|---|
| 影像 | 影像 | TextDraw和Image元件（無論是綁定還是未綁定）始終出現在基於XSD的適用性表單的記錄文檔中，除非使用記錄文檔設定排除。 |
| 文字 | 文字 |

### 表格 {#tables}

適用性Forms表格元件（例如頁首、頁尾和列對應至對應的XFA元件）。 您可以將可重複的面板對應至記錄檔案中的表格。

## 記錄文檔的基礎模板 {#base-template-of-a-document-of-record}

基礎模板為記錄文檔提供樣式和外觀資訊。 它允許您自定義自動生成的記錄文檔的預設外觀。 例如，您可以使用基本模板將公司徽標添加到記錄文檔頁首中，並在文檔頁尾中添加版權資訊。

基礎模板中的首頁用作記錄文檔模板的首頁。 主版頁可以有頁首、頁尾和頁碼等資訊，您可以將這些資訊應用到記錄文檔。 您可以使用基本模板將此類資訊應用於記錄文檔，以自動生成記錄文檔。 使用基本模板可以更改欄位的預設屬性。

一律遵循 [基本範本慣例](#base-template-conventions) 設計基礎模板時。

## 基本範本慣例 {#base-template-conventions}

基本模板用於定義記錄文檔的頁眉、頁腳、樣式和外觀。 頁首和頁尾可包含公司標誌和版權文字等資訊。 基本模板中的第一個母版頁被複製並用作記錄文檔的母版頁，該母版頁包含標題、頁尾、頁碼，或應出現在記錄文檔中所有頁上的任何其他資訊。 如果使用的基礎模板不符合基礎模板約定，則基礎模板的第一個首頁仍用於記錄文檔模板中。 強烈建議您根據基本模板的慣例設計基礎模板，並將其用於自動生成記錄文檔。

**主版頁面慣例**

* 在基礎範本中，將根子表單命名為 `AF_METATEMPLATE` 而主版頁面為 `AF_MASTERPAGE`.

* 具有名稱的主版頁面 `AF_MASTERPAGE` 位於 `AF_METATEMPLATE` 偏好使用根子表單來擷取頁首、頁尾和樣式資訊。

* 若 `AF_MASTERPAGE` 不存在，則會使用基本範本中出現的第一個母版頁面。

**欄位的樣式慣例**

* 要對記錄文檔中的欄位應用樣式，基礎模板提供位於 `AF_FIELDSSUBFORM` 從下方 `AF_METATEMPLATE` 根子表單。

* 這些欄位的屬性將應用於記錄文檔中的欄位。 這些欄位應遵循 `AF_<name of field in all caps>_XFO` 命名慣例。 例如，核取方塊的欄位名稱應為 `AF_CHECKBOX_XFO`.

若要建立基礎範本，請在Forms Designer中執行下列操作。

1. 按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 新增]**.
1. 選取 **[!UICONTROL 根據範本]** 選項。

1. 選取 **[!UICONTROL Forms — 記錄檔案]** 類別。
1. 選擇 **[!UICONTROL DoR基模板]**.
1. 按一下 **[!UICONTROL 下一個]** 並提供所需資訊。

1. （可選）修改要應用於記錄文檔中欄位的欄位的樣式和外觀。
1. 儲存表單。
   ![基本屬性](/help/forms/assets/form-designer-dor-img.png)

您現在可以將保存的表單用作記錄文檔的基礎模板。 請勿修改或移除基本範本中存在的任何指令碼。

**修改基礎模板**

* 請勿對基礎範本中的欄位套用任何樣式，建議您從基礎範本中移除這些欄位，以便自動擷取對基礎範本的任何升級。
* 修改基本模板時，請勿刪除、添加或修改指令碼。

嚴格遵守上述慣例和指示設計基礎模板。

## 自定義記錄文檔中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

在生成記錄文檔時，您可以在「記錄文檔」頁簽上更改記錄文檔的品牌資訊。 「記錄文檔」頁簽包含標誌、外觀、佈局、頁眉和頁腳、免責聲明，以及是否要包括未選定的複選框和單選按鈕選項等選項。

要本地化您在「記錄文檔」頁簽中輸入的品牌資訊，請確保已適當設定瀏覽器的區域設定。 要自定義記錄文檔的品牌資訊，請執行以下步驟：

1. 在「記錄檔」中選取面板（根面板），然後點選 ![設定](assets/configure.png).
1. 點選 ![多塔布](assets/dortab.png). 此時將顯示「記錄文檔」頁簽。
1. 選擇預設模板或自定義模板以呈現記錄文檔。 如果選擇預設模板，則「記錄文檔」(Document of Record)的縮圖預覽將顯示在「模板」(Template)下拉清單下方。
1. 根據您是選擇預設模板還是自定義模板，以下部分或全部屬性將出現在「記錄文檔」頁簽中。 指定以下提及的屬性以定義記錄文檔的外觀：

   1. **基本屬性**:
      * **範本**:如果您想要選取自訂範本，請瀏覽並在您的 [!DNL AEM Forms] 伺服器。 如果您想使用的範本在 [!DNL AEM Forms] 伺服器上，您應先將XDP上傳至您的 [!DNL AEM Forms] 伺服器。
      * **重音顏色**:在記錄PDF文檔中呈現標題文本和分隔符行的顏色。
      * **字型系列**:「記錄文檔」PDF中文本的字型系列。

      * **包括未綁定到資料模型的表單對象**:設定屬性時，記錄檔案中的「基於架構的最適化表單」中的未綁定欄位。
      <!-- **Exclude hidden fields from the Document of Record**: Setting the property identifies the hidden fields for exclusion from Document of Record.-->

      * **隱藏面板的說明**:設定屬性會從記錄檔案中排除面板/表格的說明。 適用於面板和表格。
   1. **表單欄位屬性**:
      * **對於核取方塊和選項按鈕元件，僅顯示選取的值**:設定屬性時，僅會顯示中的核取方塊和選項按鈕的選取值 [!UICONTROL 記錄檔案].
      * **多個值的分隔符號**:您可以選擇任何分隔符號，例如逗號或分行符號，以顯示多個值。
      * **選項對齊**:您可以選取所需的對齊方式（水準、垂直、與最適化表單相同），以設定要顯示於的欄位對齊方式，例如核取方塊或選項按鈕 [!UICONTROL 記錄檔案]. 預設情況下，會為 [!UICONTROL 記錄檔案]. 從 [!UICONTROL 表單欄位屬性] 的DoR會覆寫 [!UICONTROL 項目對齊方式] （適用於適用性表單上的欄位）。 如果是，請選取 [!UICONTROL 與適用表單相同] 選項，則適用性表單製作例項中設定的對齊方式會用於 [!UICONTROL 記錄檔案] 欄位。
      * **水準對齊選項數**：您可以設定要在「記錄文檔」上顯示的水準對齊選項的數量。
   1. **主版頁面屬性**:
      * **標誌影像**:您可以選擇從適用性表單使用標誌影像、從DAM中選擇一個，或從電腦上傳一個。
      * **表單標題**:DoR的標題。
      * **標題文字**:出現在記錄檔案標題區段的文字。
      * **免責聲明標籤**:免責聲明標籤。
      * **免責聲明**:說明記錄檔案權利和義務範圍的文本。
      * **免責聲明文本**:免責聲明文本。
      ![主版頁面屬性](/help/forms/assets/dorpropertiesimg.png)
   >[!NOTE]
   >
   >如果您使用使用6.3之前版本的設計器建立的適用性表單模板，以便「重音顏色」和「字型系列」屬性工作，請確保根子表單下的適用性表單模板中存在以下內容：

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

1. 若要儲存品牌變更，請點選 **[!UICONTROL 完成]**.



## 記錄文檔中面板的表和列佈局 {#table-and-column-layouts-for-panels-in-document-of-record}

您的適用性表單可能會是包含數個表單欄位的冗長表單。 您可能不想將記錄檔案儲存為最適化表單的確切副本。 現在，您可以選擇表格或欄版面，以在「記錄檔案」PDF中儲存一或多個「最適化表單」面板。

在生成記錄文檔之前，在面板的設定中，選擇該面板的記錄文檔佈局作為表或列。 在記錄檔案中會據以組織面板中的欄位。

![在「記錄文檔」中以表佈局呈現的面板中的欄位](assets/dortablelayout.png)

在「記錄文檔」中以表佈局呈現的面板中的欄位

![在「記錄文檔」中以列佈局呈現的面板中的欄位](assets/dorcolumnlayout.png)

在「記錄文檔」中以列佈局呈現的面板中的欄位

## 記錄設定文檔 {#document-of-record-settings}

「記錄文檔」設定允許您選擇要包含在「記錄文檔」中的選項。 例如，銀行接受表單中的姓名、年齡、社會保障號碼和電話號碼。 此表單會生成銀行帳號和分行詳細資訊。 您可以選擇在「記錄檔案」中只顯示姓名、社會保險號碼、銀行帳戶和分行詳細資訊。

記錄文檔元件的設定可在其屬性下使用。 若要存取元件的屬性，請選取元件，然後按一下 ![cppr](assets/cmppr.png) 在覆蓋圖中。 屬性會列在側欄中，您可以在其中找到下列設定。

**欄位層級設定**

* **從記錄檔案中排除**:將屬性設定為true會從記錄文檔中排除該欄位。 這是可指令碼的屬性，名為 `excludeFromDoR`. 其行為取決於 **如果隱藏，則從DoR排除欄位** 表單層級屬性。

* **將面板顯示為表格：** 如果面板中的欄位少於6個，設定屬性會將面板顯示為「記錄檔」中的表格。 僅適用於面板。
* **從記錄檔案中排除標題：** 設定屬性會從記錄檔案中排除面板/表格的標題。 僅適用於面板和表格。
* **從記錄文檔中排除說明：** 設定屬性會從記錄檔案中排除面板/表格的說明。 僅適用於面板和表格。

**表單層級設定**

* **在DoR中包含未綁定欄位：** 設定屬性時，包括記錄文檔中基於架構的最適化表單中的未綁定欄位。 預設為true。
<!-- **Exclude fields from DoR if hidden:** Set the property to exclude the hidden fields from Document of Record at form submission. When you enable [Revalidate on server](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), the server recomputes the hidden fields before excluding those fields from the Document of Record.->>