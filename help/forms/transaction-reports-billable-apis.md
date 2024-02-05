---
title: 交易報表可記帳API
description: 作為交易入帳的所有API清單
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a1a87a27d73d7472ec02de37621123bbdd3876b4
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 4%

---

# 交易報表可記帳API {#transaction-reports-billable-apis}

AEM Forms提供多個API來提交表單、處理檔案和轉譯檔案。 有些API是以交易入帳，其他則可供自由使用。 本檔案提供在交易報表中作為交易入帳的所有API清單。 以下是一些使用計費API的常見案例：

* 提交最適化表單
* 將檔案從一種格式轉換為另一種格式
* 平面化動態PDF檔案
* 產生記錄檔案(使用Forms服務或輸出服務)
* 將互動式PDF檔案與另一個PDF檔案合併
* 使用AEM Workflow的指派工作步驟和通訊API步驟

帳單API不考慮頁數、檔案或表單的長度，或轉譯檔案的最終格式。 交易報表將交易分為兩個類別：「Forms已提交」和「檔案已呈現」。

* **Forms已提交：** 若從使用AEM Forms建立的任何型別的表單提交資料，且資料已提交至任何資料儲存庫或資料庫，則視為表單提交。 例如，提交最適化表單或表單集會視為已提交的表單。 如果表單集有5個表單，在提交表單集時，交易報告服務將其計為5個提交。

* **已轉譯的檔案：** 透過結合範本和資料來產生檔案、以數位方式簽署或認證檔案、使用檔案服務的計費檔案服務API，或將檔案從一種格式轉換為另一種格式，均被視為檔案已呈現。

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="表單提交追蹤器"
>abstract="透過整合檢視輕鬆追蹤表單提交的總計數，或深入瞭解執行個體特定的詳細資訊。 使用直覺式長條圖來識別趨勢、比較例項，並快速做出明智的決策。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="表單轉換追蹤器"
>abstract="輕鬆掌握表單轉換的總數摘要，或探索每個AEM Forms執行個體的詳細資訊。 易讀的橫條圖有助於找出趨勢、比較例項，以及做出快速、明智的決策。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="表單產生的平均持續時間"
>abstract="圖表說明建立表單所用的平均時間。 圖表上的每個長條代表特定表單，長條的高度代表該時間範圍內建立表單所用的平均持續時間。 分析此圖表可協助使用者瞭解不同期間或不同內容中表單建立的效率和速度，進而瞭解可能的改善專案。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="建立表單的平均持續時間"
>abstract="圖形顯示建立和發佈表單所需的平均時間，從開啟表單進行編輯的初始日期開始計算。 每個長條會對應至表單的特定時間範圍，長條高度會指出從表單開發開始到最終完成及發佈所花費的平均時間。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="新增Forms追蹤器"
>abstract="圖表會提供特定時段內新建立表單的數量或頻率的相關資訊。 圖表上的每個長條代表不同的測量單位，例如日、周或月。 每個長條的高度表示在該特定間隔內建立的新表單的數量或頻率。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="已發佈Forms追蹤器"
>abstract="圖表提供特定時段內已成功發佈之表單的數量或頻率的相關資訊。 這可讓您瞭解表單發佈在一段時間內的趨勢、模式或變數，有助於監控生產力、識別尖峰發佈期間，或評估表單發佈程式中變更的成功程度。"

<!-- 
>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Form Fragments Tracker"
>abstract="This graph helps you see how many form fragments people use in their forms. It gives you a sense of how popular or common these reusable parts are in form building."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Average Duration for Form Fragments Creation"
>abstract= "The graph displays the average time taken to create a form fragment, measured from the initial day the form fragment was opened for editing. Each bar corresponds to a specific time frame for a form fragment, with the bar height indicating the average time taken from the start of form fragment development to its finalization and publication."


<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## 可記帳檔案服務API {#billable-document-services-apis}

### 產生PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>從範本產生PDF檔案，並將資料合併到其中。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>將XDP檔案或PDF檔案轉換為支援的檔案型別。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### 輸出服務 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>合併資料和範本以建立一組PDF檔案。</td>
   <td>已處理的文件</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (PrintedOutputOptions)</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>將一組XDP和PDF檔案轉換為一組PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### DocAssurance服務 {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>此API可讓您保護檔案的安全。 您可以使用API來簽署、認證、讀取器延伸或加密PDF檔案。</td>
   <td>已處理的文件</td>
   <td>只對secureDocument的簽署和認證操作收費。</td>
  </tr>
 </tbody>
</table>

### 記錄檔案(DOR)服務 {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">轉譯</a></td>
   <td>叫用指定的轉譯方法，以使用提供的引數產生記錄檔案。</td>
   <td>使用Forms服務處理的檔案</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### 組合器服務 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">叫用</a></td>
   <td>在指定的輸入檔案上執行DDX，並傳回包含結果檔案的物件</td>
   <td>已處理的文件</td>
   <td>下列作業不會作為交易入帳：
    <ul>
     <li>建立套件或投資組合</li>
     <li>拼接多個XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">叫用</a></td>
   <td>在指定的輸入檔案上執行DDX，並傳回包含結果檔案的物件</td>
   <td>已處理的文件</td>
   <td>PDF Generator、Forms和輸出服務支援的所有輸入檔案格式，組合器服務都支援所有這些格式作為輸出檔案格式。 </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>使用指定的選項將指定的檔案轉換為PDF/A。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

當您執行下列一或多個作業時，叫用API的使用量會計為交易：

1. 從非PDF格式轉換成PDF格式。 <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. 從PDF格式轉換為PDF/A格式。
1. 從PDF格式轉換為非PDF格式。 範例包括從PDF到影像格式的轉換或從PDF到文字格式的轉換。


>[!NOTE]
>
>* 組合器服務的叫用API可以在內部根據輸入呼叫另一個服務的計費的API。 因此，叫用API可計為無、單一或多個交易。 計算交易數取決於輸入和叫用的內部API。
>* 使用組合器服務產生的單一PDF檔案可計為無、單一或多個交易。 計算的交易數取決於提供的代碼。
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## 可記帳資料擷取API {#billable-data-capture-apis}

所有最適化表單的提交事件都會入帳為交易。 依預設，PDF表單的提交不會作為交易入帳。 使用提供的 [交易錄製器API](record-transaction-custom-implementation.md) 將PDF forms提交記錄為交易。

### 最適化表單 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交最適化表單</td>
   <td>提交最適化表單以設定提交動作。 </td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>單一或兩個交易的成功提交帳戶。 計算交易數取決於用於提交的提交動作型別。 例如，透過電子郵件傳送PDF時，提交動作會計算兩個交易計數。 一個交易用於表單提交，另一個交易用於使用記錄檔案(DOR)服務產生的PDF。 </li>
     <li>在最適化表單（最適化表單集）中使用最適化表單時，只會計算單一交易。 在最適化表單中可以有任意數量的最適化表單。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## 計費表單中心的AEM工作流程 {#billable--form-centric-aem-workflows}

以「表單為中心的AEM工作流程」的指定作業與檔案服務步驟會作為異動入帳。 如果工作流程步驟將交易入帳，但工作流程無法完成，則不會迴轉交易計數。

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### 以表單為中心的AEM工作流程 {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交指派工作步驟</td>
   <td>已提交的表單</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>提交工作流程應用程式起點 </td>
   <td>已提交的表單</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 將可記帳API記錄為自訂程式碼的交易 {#recording-billable-apis-as-transactions-for-custom-code}

提交PDF表單、使用代理程式UI預覽互動式通訊、使用非標準表單提交和自訂實施等動作不會計為交易。 AEM Forms提供API來記錄此類動作，例如交易。 您可以從自訂實施呼叫API至 [記錄交易](/help/forms/record-transaction-custom-implementation.md).

## 相關文章 {#related-articles}

* [記錄自訂實作的交易](/help/forms/record-transaction-custom-implementation.md)
