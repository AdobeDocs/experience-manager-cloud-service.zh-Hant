---
title: 如何產生AEM Forms的記錄檔案(DoR)？
description: 瞭解如何產生最適化Forms的記錄檔案(DoR)範本。
feature: Adaptive Forms, Foundation Components
exl-id: 16d07932-3308-4b62-8fa4-88c4e42ca7b6
role: User, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '4221'
ht-degree: 2%

---

# 為最適化表單產生記錄文件

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/creating-adaptive-form-core-components.md)，使用現代且可擴充的資料擷取[核心元件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

## 概觀 {#overview}

填寫或提交表單時，您可以以列印或檔案格式保留表單記錄。 此記錄稱為記錄檔案(DoR)。 這是一份容易列印的已提交表格。 您也可以參考記錄檔案以瞭解客戶在稍後日期填寫的資訊，或使用記錄檔案以PDF格式將表單和內容一起封存。

![記錄檔案](assets/document-of-record.png)

為了建立記錄檔案，會將XFA或Acroform型範本與透過最適化表單收集的資料合併。 您可以自動或依需求產生記錄檔案。
隨選選項可讓您指定自訂XFA或Acroform型範本，以提供記錄檔案的自訂外觀。

您可以：

* [產生以XFA為基礎的記錄檔案](#generate-an-XFA-based-document-of-record)
* [產生以Acroform為基礎的(Acrobat Form PDF)記錄檔案](#generate-an-Acroform-based-document-of-record)
* [自動生成記錄檔案](#auto-generate-a-document-of-record)

## 開始之前 {#components-to-automatically-generate-a-document-of-record}

在您開始學習並準備好記錄檔案所需的資產之前：

**基底範本：**&#x200B;在Forms Designer或Acrobat表單(AcroForm)中建立的XFA範本（XDP檔案）。 [基底範本](#base-template-of-a-document-of-record)用於指定記錄檔案的樣式和品牌資訊。 在之前將您的XFA範本（XDP檔案）上傳到您的AEM Forms執行個體

**最適化表單：**&#x200B;要產生記錄檔案的最適化表單。

## 產生以XFA為基礎的記錄檔案 {#generate-an-XFA-based-document-of-record}

將您的XFA範本（XDP檔案）上傳至您的AEM Forms執行個體。 執行以下步驟來設定最適化表單，以使用XFA範本（XDP檔案）作為記錄檔案的範本：

1. 在Experience Manager作者執行個體中，按一下&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]。**
1. 選取表單，然後按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在[內容]視窗中，選取&#x200B;**[!UICONTROL 表單模型]**。
1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤的&#x200B;**[!UICONTROL 選取自]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;或&#x200B;**[!UICONTROL 無]**。 您也可以在建立表單時選取表單模型。
1. 在[表單模型]索引標籤的[記錄檔案範本組態]區段中，選取[**關聯表單範本作為記錄檔案範本**]。 選取此選項時，會顯示電腦上可用的所有XFA範本（XDP檔案）。 選取適當的檔案。 此外，請確定最適化表單和選取的XFA範本（XDP檔案）使用的是相同結構描述（資料結構描述）。
1. 按一下&#x200B;**[!UICONTROL 完成]**

您的最適化表單現在已設定為使用XDP檔案作為記錄檔案的範本。 下一個步驟是[繫結最適化表單元件與對應的範本欄位](#bind-adaptive-form-components-with-template-fields)。

## 產生以Acroform為基礎的記錄檔案 {#generate-an-Acroform-based-document-of-record}

將Adobe Acrobat PDF (Acroform)上傳至AEM Forms執行個體。 執行以下步驟來設定最適化表單，以使用Adobe Acrobat PDF (Acroform)作為記錄檔案的範本：

1. 在Experience Manager作者執行個體中，按一下&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]。**
1. 選取表單，然後按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在[內容]視窗中，選取&#x200B;**[!UICONTROL 表單模型]**。
1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤的&#x200B;**[!UICONTROL 選取自]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;或&#x200B;**[!UICONTROL 無]**。 您也可以在建立表單時選取表單模型。
1. 在[表單模型]索引標籤的[記錄檔案範本組態]區段中，選取[**關聯表單範本作為記錄檔案範本**]。 選取此選項時，會顯示電腦上可用的所有Acrobat PDF (Acroform)。 選取適當的檔案。
1. 按一下&#x200B;**[!UICONTROL 完成]**

您的最適化表單現在已設定為使用Acroform作為記錄檔案的範本。 下一個步驟是[繫結最適化表單元件與對應的範本欄位](#bind-adaptive-form-components-with-template-fields)。

## 自動產生記錄檔案 {#auto-generate-a-document-of-record}

當調適型表單設定為自動生成記錄檔案時，每次表單變更時，其記錄檔案都會立即更新。 例如，如果欄位從現有的最適化表單中移除，則對應的欄位也會被移除，並且不會顯示在記錄檔案中。 自動產生記錄檔案還有其他許多優點。 ：

* 表單開發人員不需要手動維護資料繫結。 自動產生的記錄檔案會處理資料繫結相關更新。
* 表單開發人員不必手動隱藏標籤為從記錄檔案排除的欄位。 自動產生的記錄檔案已預先設定為排除這類欄位。
* 自動產生的記錄檔案選項可節省建立記錄檔案的表單範本所需的時間。
* 「自動產生的記錄檔案」選項可讓您使用不同的基本範本來使用不同的樣式和外觀。 這有助於為您的組織選擇記錄檔案的最佳樣式和外觀。 如果未指定樣式，系統樣式會設定為預設值。
* 自動產生的記錄檔案可確保表單中的任何變更都立即反映在記錄檔案中。

執行以下步驟來設定最適化表單以自動產生記錄檔案：

1. 在Experience Manager作者執行個體中，按一下&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]。**
1. 選取表單，然後按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在[內容]視窗中，選取&#x200B;**[!UICONTROL 表單模型]**。
1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤的&#x200B;**[!UICONTROL 選取自]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;或&#x200B;**[!UICONTROL 無]**。 您也可以在建立表單時選取表單模型。
1. 在[表單模型]索引標籤的[記錄檔案範本組態]區段中，選取[**產生記錄檔案**]。
1. 按一下&#x200B;**[!UICONTROL 完成]**

## 繫結最適化表單元件與範本欄位 {#bind-adaptive-form-components-with-template-fields}

繫結最適化表單欄位與範本欄位，以在對應的記錄檔案欄位中顯示擷取的表單資料。 若要將最適化表單元件與對應的記錄檔案範本欄位繫結：

1. 開啟最適化表單，設定為使用自訂表單範本進行編輯。

1. 選取最適化表單元件，然後按一下[開啟設定![設定](assets/Smock_Wrench_18_N.svg)]圖示。 它會開啟屬性瀏覽器。

1. 在屬性瀏覽器中，瀏覽並選取欄位。

   * （針對AcroForm範本） **[!UICONTROL 記錄檔案繫結參考欄位]**&#x200B;屬性。
   * （適用於XFA範本） **[!UICONTROL 資料模型繫結參考]**&#x200B;屬性。

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

您可以使用傳送電子郵件、Experience Manager工作流程提交動作搭配[記錄檔案步驟以及其他提交動作](configuring-submit-actions.md)來接收記錄檔案。

## 記錄檔案範本的增量更新 {#document-of-record-template-incremental-updates}

最適化表單和相應的記錄檔案範本可能會隨著時間而改變。 您可以選擇新增、移除或修改最適化表單或記錄檔案範本的欄位。

當您變更記錄檔案範本並將變更後的記錄檔案範本上傳到AEM Forms時，Adaptive Forms編輯器會自動偵測變更的繫結，並通知您需要新繫結的自適應表單元件。 它可讓您對記錄檔案範本進行增量更新。

例如，組織&#x200B;*We.Retail*&#x200B;有一個以AcroForm為基礎的記錄檔案範本&#x200B;*we-retail-invoice.pdf*。 範本看起來如下所示：

![原始範本](assets/we-retail-invoice.png)

使用範本一段時間後，組織決定將「`invoice-number`」欄位重新命名為「`bill-number`」欄位，並擷取購買者的電子郵件地址。 開發人員更新`invoice-number`欄位的名稱，並將電子郵件欄位新增至範本。 他還建立了名為&#x200B;*we-retail-invoice-v2.pdf*&#x200B;的新版範本。

![已更新範本](assets/we-retail-new-invoice.png)

開發人員會上傳並將更新後的範本套用至最適化表單。 最適化表單會自動偵測並顯示繫結已變更的欄位清單。

![繫結錯誤](assets/we-retail-binding-error.png)

表單開發人員會將最適化Forms欄位與對應的記錄檔案範本繫結。

>[!VIDEO](assets/we-retail-binding.mp4)

現在，當最適化表單被提交時，會建立一個更新的記錄檔案。

![已更新 — ](assets/we-retail-new-invoice-sent-to-customer.png)

## 使用記錄檔案時的主要考量事項 {#key-considerations-when-working-with-document-of-record}

處理最適化Forms的記錄檔案時，請牢記以下考量事項和限制。

* 記錄檔案範本不支援RTF文字。 因此，靜態最適化表單中或使用者填入的資訊中的任何RTF文字都會在記錄檔案中顯示為純文字。
* 最適化表單中的檔案片段未出現在記錄檔案中。 不過，支援最適化表單片段。
* 不支援為以XML結構描述為基礎的最適化表單產生的記錄檔案中的內容繫結。
* 當使用者請求轉譯記錄檔案時，記錄檔案的當地語系化版本是應地區設定的要求建立的。 記錄檔案本地化與最適化表單本地化同時發生。<!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

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

下表說明最適化表單元件和對應的XFA元件，以及這些元件是否出現在記錄檔案中。

### 欄位 {#fields}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>預設包含在記錄檔案範本中？</th>
   <th>備註</th>
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
   <td>日期挑選器</td>
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
   <td>草寫簽名</td>
   <td>手寫簽名</td>
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
   <td>密碼方塊</td>
   <td>密碼欄位</td>
   <td>false</td>
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
   <td>條款與條件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td> </td>
   <td>false</td>
   <td>在記錄檔案範本中無法使用。 只能透過附件在記錄檔案中使用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>備註</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表單<br /> </td>
   <td>可重複面板對應至可重複的子表單。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 最適化表單元件 | 對應的XFA元件 | 備註 |
|---|---|---|
| 影像 | 影像 | 除非使用記錄檔案設定加以排除，否則TextDraw和Image元件（無論繫結或未繫結）一律顯示在XSD型調適型表單的記錄檔案中。 |

### 表格 {#tables}

最適化Forms表格元件（例如頁首、頁尾和列）對應至對應的XFA元件。 您可以將可重複面板對應至記錄檔案中的表格。

## 記錄檔案的基礎範本 {#base-template-of-a-document-of-record}

基礎範本為記錄檔案提供樣式和外觀資訊。 它可讓您自訂自動產生之記錄檔案的預設外觀。 例如，您可以使用基礎範本在記錄檔案的頁首和頁尾中新增公司標誌和版權資訊。

基礎範本的主版頁面會作為記錄檔案範本的主版頁面。 主版頁面可以包含頁首、頁尾和頁碼等資訊，您可以將這些資訊套用至記錄檔案。 您可以使用基礎範本將此類資訊套用至記錄檔案，以自動產生記錄檔案。 使用基礎範本可讓您變更欄位的預設屬性。

在設計基礎範本時，請一律遵循[基礎範本慣例](#base-template-conventions)。

## 基礎範本慣例 {#base-template-conventions}

基礎範本用於定義記錄檔案的頁首、頁尾、樣式和外觀。 頁首和頁尾可包含公司標誌和版權文字等資訊。 基礎範本中的第一個主版頁面被複製並用作記錄檔案的主版頁面，其中包含頁首、頁尾、頁碼或應該出現在記錄檔案所有頁面上的任何其他資訊。 如果您使用的基底範本不符合基底範本慣例，則基底範本中的第一個主版頁面仍會用於「記錄檔案」範本中。 強烈建議您依照其慣例設計基礎範本，並用於自動產生記錄檔案。

**主版頁面慣例**

* 在基底範本中，將根子表單命名為`AF_METATEMPLATE`，將主版頁面命名為`AF_MASTERPAGE`。

* 位於`AF_MASTERPAGE`根子表單下名稱為`AF_METATEMPLATE`的主版頁面較適合擷取頁首、頁尾和樣式資訊。

* 如果`AF_MASTERPAGE`不存在，則會使用基底範本中存在的第一個主版頁面。

**欄位的樣式慣例**

* 若要在記錄檔案中的欄位套用樣式，基底範本提供位於`AF_FIELDSSUBFORM`根子表單下的`AF_METATEMPLATE`子表單中的欄位。

* 這些欄位的屬性會套用至記錄檔案中的欄位。 這些欄位應遵循`AF_<name of field in all caps>_XFO`命名慣例。 例如，核取方塊的欄位名稱應該是`AF_CHECKBOX_XFO`。

若要建立基礎範本，請在Forms Designer中執行下列動作。

1. 按一下&#x200B;**[!UICONTROL 檔案]** > **[!UICONTROL 新增]**。
1. 選取&#x200B;**[!UICONTROL 根據範本]**&#x200B;選項。

1. 選取&#x200B;**[!UICONTROL Forms — 記錄檔案]**&#x200B;類別。
1. 選取&#x200B;**[!UICONTROL DoR基底範本]**。
1. 按一下[下一步]&#x200B;**&#x200B;**&#x200B;並提供必要的資訊。

1. （選擇性）修改您要在記錄檔案中欄位上套用的欄位樣式和外觀。
1. 儲存表單。

您現在可以使用儲存的表單作為記錄檔案的基礎範本。 請勿修改或移除基礎範本中存在的任何指令碼。

**正在修改基底範本**

* 如果沒有在基本範本的欄位上套用任何樣式，建議從基本範本中移除這些欄位，以便自動擷取對基本範本的任何升級。
* 修改基底範本時，請勿移除、新增或修改指令碼。

請嚴格遵守上述慣例和指示，以設計基礎範本。

## 自訂記錄檔案中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

產生記錄檔案時，您可以在記錄檔案索引標籤上變更記錄檔案的品牌資訊。 「記錄檔案」索引標籤包括如標誌、外觀、版面、頁首和頁尾、免責宣告等選項，以及您是否要包含未選取的核取方塊和選項按鈕選項。

若要將您在「記錄檔案」標籤中輸入的品牌資訊當地語系化，請確定已正確設定瀏覽器的地區設定。 若要自訂記錄檔案的品牌資訊，請執行下列步驟：

1. 選取記錄檔案中的面板（根面板），然後選取![設定](assets/configure.png)。
1. 選取![多標籤](assets/dortab.png)。 記錄檔案索引標籤隨即顯示。
1. 選取呈現記錄檔案的預設範本或自訂範本。 如果您選取預設範本，記錄檔案的縮圖預覽會顯示在「範本」下拉式清單下方。
1. 根據您選取預設或自訂範本，以下某些屬性或所有屬性都會顯示在「記錄檔案」標籤中。 指定以下提及的屬性以定義記錄檔案的外觀：

   1. **基本屬性**：
      * **範本**：如果您選擇選取自訂範本，請在[!DNL AEM Forms]伺服器上瀏覽選取XDP。 如果您想使用未在[!DNL AEM Forms]伺服器上的範本，您應該先將XDP上傳到您的[!DNL AEM Forms]伺服器。
      * **強調色**：在PDF檔案或記錄中呈現標頭文字和分隔線的色彩。
      * **字型系列**：記錄檔案PDF中的文字字型系列。

        >[!NOTE]
        >
        > AEM Forms提供多種內建字型，可順暢地與PDF檔案整合。 若要檢視支援的字型清單，[請按一下這裡](/help/forms/supported-out-of-the-box-fonts.md)。

      * **包含未繫結至資料模型的表單物件**：設定屬性會包含記錄檔案中結構描述型最適化表單中未繫結的欄位。
      * **從記錄檔案排除隱藏欄位**：設定屬性可識別從記錄檔案排除的隱藏欄位。
      * **隱藏面板的描述**：設定屬性會從記錄檔案中排除面板/表格的描述。 適用於面板和表格。

      ![基本屬性](/help/forms/assets/basicpropertiesdor.png)

   2. **表單欄位屬性**：
      * **對於核取方塊與選項按鈕元件，僅顯示選取的值**：設定屬性只會顯示[!UICONTROL 記錄檔案]中核取方塊與選項按鈕的選取值。
      * **多個值的分隔符號**：您可以選擇任何分隔符號，例如逗號或分行符號，以顯示多個值。
      * **選項對齊方式**：您可以選取想要的對齊方式（水準、垂直、與調適型表單相同），以設定在[!UICONTROL 記錄檔案]上顯示的核取方塊或選項按鈕等欄位對齊方式。 根據預設，[!UICONTROL 記錄檔案]中的欄位會設定垂直對齊方式。 從DoR的[!UICONTROL 表單欄位屬性]設定屬性，會覆寫最適化表單上欄位在[!UICONTROL 專案對齊方式]中設定的屬性。 如果您選取[!UICONTROL 與適用性表單相同]選項，適用性表單作者執行個體中設定的對齊方式會用於[!UICONTROL 記錄檔案]欄位。
      * **水準對齊方式的選項數目**:You&#x200B;可以設定要在記錄檔案上顯示的水準對齊方式的選項數目。

      ![表單欄位屬性](/help/forms/assets/formfieldpropertiesdor.png)

   3. **主版頁面屬性**：
      * **標誌影像**：您可以選擇使用最適化表單的標誌影像、從DAM選擇標誌影像，或從您的電腦上傳標誌影像。
      * **表單標題**： DoR標題。
      * **標題文字**：出現在記錄檔案標題區段的文字。
      * **免責宣告標籤**：免責宣告的標籤。
      * **免責宣告**：指定記錄檔案上權利與義務範圍的文字。
      * **免責宣告文字**：免責宣告文字。

      ![主版頁面屬性](/help/forms/assets/masterpagepropertiesdor.png)

   >[!NOTE]
   >
   >如果您使用以6.3之前的Designer版本建立的調適型表單範本，為了使輔色和字型系列屬性運作，請確定根子表單下的調適型表單範本中存在下列專案：

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

1. 若要儲存品牌變更，請選取&#x200B;**[!UICONTROL 完成]**。

>[!NOTE]
> 
> 若要在記錄檔案中顯示自訂表單標題，請編輯&#x200B;**記錄檔案屬性** > **主版頁面屬性**&#x200B;中的&#x200B;**自訂表單標題**。 此自訂標題：
> 
> * 出現在產生的PDF標題中
> * 在PDF的檔案屬性中顯示為標題
> * 在PDF開啟時顯示為初始檢視標題

## 最適化表單編輯器中的記錄檔案支援 {#dor-support-in-adaptiveform}

您可以直接從最適化表單編輯器或最適化表單範本編輯器設定[!UICONTROL 記錄檔案]範本。

從最適化表單編輯器的製作例項執行以下步驟：

1. 選取「**[!UICONTROL 最適化表單容器 (根)]**」元件。
1. 按一下 ![設定圖示](/help/forms/assets/configure-icon.svg) 圖示以開啟最適化表單容器的「**[!UICONTROL 屬性]**」。
1. 開啟&#x200B;**[!UICONTROL 記錄範本檔案]**&#x200B;索引標籤，然後從下列選項中選取：
   * **[!UICONTROL 無]**：選取此選項時，不會為您的最適化表單建立[!UICONTROL 記錄檔案]範本。
   * **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]**:When選取此選項時，會使用XFA表單作為記錄檔案的範本。
   * **[!UICONTROL 產生記錄檔案]**：選取此選項時，系統會自動為您的最適化表單產生[!UICONTROL 記錄檔案]範本。

1. 選取![儲存](/help/forms/assets/check-button.png)以儲存屬性。

![記錄範本檔案支援](/help/forms/assets/dor-templatesupport.png)

>[!NOTE]
>
>使用最適化表單範本編輯器建立[!UICONTROL 記錄檔案]範本時，[!UICONTROL 記錄檔案範本]標籤下只有兩個選項可用，即[!UICONTROL 無]和[!UICONTROL 產生記錄檔案]。

## 記錄檔案中面板的表格和欄配置 {#table-and-column-layouts-for-panels-in-document-of-record}

您的調適型表單可能很長，包含多個表單欄位。 您可能不想將記錄檔案儲存為最適化表單的精確副本。 現在您可以選擇表格或欄版面配置，以將一個或多個最適化表單面板儲存在記錄檔案PDF中。

在產生記錄檔案之前，在面板的設定中，選取該面板的「記錄檔案配置」(Layout For The Document of Record)為「表格」或「欄」。 面板中的欄位會在記錄檔案中進行相應的組織。

![面板中的欄位在記錄檔案中以資料表配置呈現](assets/dortablelayout.png)

面板中的欄位在記錄檔案中以表格佈局呈現

![面板中的欄位在記錄檔案中以欄配置呈現](assets/dorcolumnlayout.png)

面板中的欄位在記錄檔案中的欄配置中轉譯

## 記錄檔案設定 {#document-of-record-settings}

記錄檔案設定可讓您選擇要包含在記錄檔案中的選項。 例如，銀行可接受表單中的姓名、年齡、社保號碼和電話號碼。 此表單會產生銀行帳號及分行詳細資訊。 您可以選擇在記錄檔案中只顯示名稱、社會安全號碼、銀行帳戶和分行詳細資訊。

記錄檔案元件的設定可在其屬性下使用。 若要存取元件的屬性，請選取該元件，然後按一下覆蓋圖中的![cmppr](assets/cmppr.png)。 屬性會列在側邊欄中，您可在其中找到下列設定。

**欄位層級設定**

* **從記錄檔案排除**：設定屬性True會從記錄檔案排除欄位。 這是名為`excludeFromDoR`的指令碼屬性。 其行為取決於若隱藏&#x200B;**表單層級屬性，則從DoR排除**&#x200B;欄位。

* **將面板顯示為表格：**&#x200B;如果面板中有少於6個欄位，則設定屬性將面板顯示為記錄檔案中的表格。 僅適用於面板。
* **從記錄檔案排除標題：**&#x200B;設定屬性會從記錄檔案排除面板/表格的標題。 僅適用於面板和表格。
* **從記錄檔案排除描述：**&#x200B;設定屬性會從記錄檔案排除面板/表格的描述。 僅適用於面板和表格。

**表單層級設定**

* **包含未繫結欄位於DoR：**&#x200B;設定屬性包含記錄檔案中結構描述型最適化表單的未繫結欄位。 預設為true。
* **若隱藏則從DoR排除欄位：**&#x200B;設定屬性以在提交表單時從記錄檔案中排除隱藏欄位。 當您在伺服器[上啟用](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)重新驗證時，伺服器會先重新計算隱藏的欄位，然後再將這些欄位從記錄檔案中排除。

## 使用自訂XCI檔案

XCI檔案可協助您設定檔案的各種屬性。 Forms as a Cloud Service有主XCI檔案。 您可以使用自訂XCI檔案來覆寫主XCI檔案中指定的一個或多個預設屬性。 例如，您可以選擇將字型內嵌到檔案中，或是為所有檔案啟用標籤屬性。 下表指定XCI選項：

| XCI選項 | 說明 |
|--- |--- |
| config/present/pdf/creator | 使用檔案資訊字典中的建立者專案來識別檔案建立者。 如需此字典的相關資訊，請參閱[PDF參考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/pdf/producer | 使用檔案資訊字典中的製作者專案來識別檔案製作者。 如需此字典的相關資訊，請參閱[PDF參考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/layout | 控制輸出是單一面板還是分頁。 |
| config/present/pdf/compression/level | 指定產生PDF檔案時要使用的壓縮程度。 |
| config/present/pdf/fontInfo/embed | 控制輸出檔案中的字型內嵌。 |
| config/present/pdf/scriptModel | 控制輸出PDF檔案中是否包含XFA特定資訊。 |
| config/present/common/data/adjustData | 控制XFA應用程式是否會在合併後調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的產生是在伺服器上完成，還是延後至使用者端。 |
| config/present/common/locale | 指定輸出檔案中使用的預設地區設定。 |
| config/present/destination | 當由目前元素包含時，指定輸出格式。 當由openAction元素包含時，會指定在互動式使用者端中開啟檔案時要執行的動作。 |
| config/present/output/type | 指定要套用至檔案的壓縮型別，或是要產生的輸出型別。 |
| config/present/common/temp/uri | 指定表單URI。 |
| config/present/common/template/base | 提供表單設計中基本的URI位置。 當此元素不存在或空白時，會使用表單設計的位置作為基礎。 |
| config/present/common/log/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/output/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟檔案時的初始頁面。 |
| config/present/script/exclude | 通知Forms as a Cloud Service要忽略哪些事件。 |
| config/present/pdf/linearized | 控制是否將輸出PDF檔案線性化。 |
| config/present/script/runScripts | 控制Forms as a Cloud Service要執行哪一組指令碼。 |
| config/present/pdf/tagged | 控制標籤在輸出PDF檔案中是否包含。 在PDF中，標籤是包含在檔案中的其他資訊，用於公開檔案的邏輯結構。 標籤有助於協助協助工具及重新格式化。 例如，頁碼可能會被標籤為成品，這樣熒幕閱讀器就不會在文字中間朗讀它。 雖然標籤讓檔案變得更實用，但它們也會增加檔案的大小，以及建立檔案的處理時間。 |
| config/present/pdf/fontInfo/alwaysEmbed | 指定內嵌在輸出檔案中的字型。 |
| config/present/pdf/fontInfo/neverEmbed | 指定不得嵌入至輸出檔案的字型。 |
| config/present/pdf/pdfa/part | 指定檔案符合的PDF/A規格版本號碼。 |
| config/present/pdf/pdfa/amd | 指定PDF/A規格的修訂等級。 |
| config/present/pdf/pdfa/conformance | 指定與PDF/A規格一致的等級。 |
| config/present/pdf/version | 指定要產生的PDF檔案版本 |
| config/present/pdf/version/map | 指定檔案的回覆字型 |

>[!NOTE]
>
> AEM Forms提供多種內建字型，可順暢地與PDF檔案整合。 若要檢視支援的字型清單，[請按一下這裡](/help/forms/supported-out-of-the-box-fonts.md)。


### 在您的Forms as a Cloud Service環境中使用自訂XCI檔案

1. 將自訂XCI檔案新增至您的開發專案。
1. 指定下列[內嵌屬性](/help/implementing/deploying/configuring-osgi.md)：

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

1. 將專案部署至您的Cloud Service環境。

### 在本機Forms as a Cloud Service開發環境中使用自訂XCI檔案

1. 上傳XCI檔案至您的本機開發環境。
1. 開啟Cloud Service SDK設定管理員。 預設URL為： <http://localhost:4502/system/console/configMgr>。
1. 找到並開啟&#x200B;**[!UICONTROL 最適化Forms和互動式通訊Web Channel]**&#x200B;設定。
1. 指定XCI檔案的路徑，然後按一下&#x200B;**[!UICONTROL 儲存]**。


## 另請參閱 {#see-also}

{{see-also}}
