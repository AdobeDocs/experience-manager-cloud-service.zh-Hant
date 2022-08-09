---
title: '如何將工作流分配給其他用戶、發送電子郵件、在工作流中使用Adobe Sign? '
description: 以Forms為中心的工作流允許您快速構建基於Forms的自適應工作流。 您可以使用Adobe Sign對文檔進行電子簽名、建立基於表單的業務流程、檢索資料並將資料發送到多個資料源以及發送電子郵件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: ebd7942cfaa7717d68ad039f3e0301cb52cbcec7
workflow-type: tm+mt
source-wordcount: '6098'
ht-degree: 1%

---

# 以Forms為AEM中心的工作流 — 步驟參考 {#forms-centric-workflow-on-osgi-step-reference}

您可以使用工作流模型將業務邏輯轉換為自動化的重複流程。 模型可幫助您定義和執行一系列步驟。 您還可以定義模型屬性，如工作流是瞬態的還是使用多個資源。 你可以 [在模AEM型中包括各種工作流步驟以實現業務邏輯](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem)。

## 以Forms為中心的步驟 {#forms-workflow-steps}

以Forms為中心的工作流步驟在工作流中執行特定於AEM FormsAEM的操作。 這些步驟使您能夠在OSGi上快速構建基於自適應Forms的以Forms為中心的工作流。 這些工作流可用於開發基本的審核和批准工作流、內部和跨防火牆的業務流程。 您還可以使用Forms Workflow步驟：

* 建立業務流程、提交後工作流和後端工作流以管理註冊流程。

* 建立任務並將其分配給用戶或組。

* 使用 [!DNL Adobe Sign] 的子AEM菜單。

* 按需或按表單提交生成記錄文檔。

* 將工作流模型與各種資料源連接以便輕鬆保存和檢索資料。

* 使用電子郵件步驟可以在完成操作以及工作流開始或完成時發送通知電子郵件和其他附件。

>[!NOTE]
>
>如果為外部儲存標籤了工作流模型，則對於所有Forms工作流步驟，您只能選擇變數選項來儲存或檢索資料檔案和附件。


## 分配任務步驟 {#assign-task-step}

分配任務步驟將建立工作項並將其分配給用戶或組。 除了分配任務外，元件還為任務指定自適應表單或非交互PDF。 需要自適應表單來接受來自用戶的輸入，非互動式PDF或只讀自適應表單用於僅查看工作流。

也可以使用元件來控制任務的行為。 例如，建立自動記錄文檔，將任務分配給特定用戶或組，指定提交資料的路徑，指定要預填充的資料路徑，以及指定預設操作。 「分配任務」步驟具有以下屬性：

* **[!UICONTROL 標題]**:任務的標題。 標題顯示在收件箱AEM中。
* **[!UICONTROL 說明]**:對任務中正在執行的操作的說明。 當您在共用開發環境中工作時，此資訊對其他流程開發人員非常有用。

* **[!UICONTROL 縮略圖路徑]**:任務縮略圖的路徑。 如果未指定路徑，則顯示自適應表單預設縮略圖，並顯示記錄文檔的預設表徵圖。
* **[!UICONTROL 工作流階段]**:工作流可以具有多個階段。 這些階段顯示在收件箱AEM中。 可以在模型的屬性（「邊」>「頁面」>「頁面屬性」>「階段」）中定義這些階段。
* **[!UICONTROL 優先順序]**:選定優先順序顯示在收AEM件箱中。 可用選項有「高」、「中」和「低」。 預設值為「中」。
* **[!UICONTROL 到期日]**:指定任務標籤為逾期的天數或小時數。 如果選擇 **[!UICONTROL 關閉]**，則任務永遠不會被標籤為過期。 您還可以指定超時處理程式以在任務過期後執行特定任務。

* **[!UICONTROL 天數]**:任務完成前的天數。 在將任務分配給用戶後計算天數。 如果任務未完成，並且超過「天數」欄位中指定的天數，則如果選中，則在到期日期之後觸發超時處理程式。
* **[!UICONTROL 小時]**:任務完成前的小時數。 在將任務分配給用戶後計算小時數。 如果任務未完成，並且超過「小時數」欄位中指定的小時數，則如果選中，則在到期小時後觸發超時處理程式。
* **[!UICONTROL 到期日後超時]**:選擇此選項以啟用超時處理程式選擇欄位。
* **[!UICONTROL 超時處理程式]**:選擇當分配任務步驟超過到期日期時要執行的指令碼。 放置在CRX儲存庫中的指令碼 [應用]/fd/dashboard/scripts/timeoutHandler可供選擇。 crx-repository中不存在指定的路徑。 管理員在使用路徑之前建立路徑。
* **[!UICONTROL 突出顯示任務詳細資訊中最後一個任務中的操作和注釋]**:選擇此選項可顯示在任務的任務詳細資訊部分上執行的最後操作和收到的注釋。
* **[!UICONTROL 類型]**:選擇啟動工作流時要填寫的文檔類型。 您可以選擇「自適應表單」、只讀自適應表單、非互動式PDF文檔。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用自適應窗體]**:指定定位輸入自適應表單的方法。 如果從「類型」(Type)下拉清單中選擇「自適應表單」(Adaptive Form)或「只讀自適應表單」(Read-only Adaptive Form)，則此選項可用。 可以使用提交到工作流的自適應表單，該表單可以在絕對路徑上使用，也可以在變數的路徑上使用。 可以使用字串類型的變數指定路徑。\
   可以將多個AdaptiveForms與工作流關聯。 因此，可以使用可用的輸入方法在運行時指定自適應表單。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 自適應窗體路徑]**:指定「自適應表單」的路徑。 可以使用提交到工作流的自適應表單（可以在絕對路徑中使用），或從儲存在字串資料類型變數中的路徑檢索自適應表單。
* **[!UICONTROL 選擇輸入PDF]**:指定非互動式PDF文檔的路徑。 在「類型」(Type)欄位中選擇非互動式PDF文檔時，該欄位可用。 可以使用相對於負載的路徑、保存在絕對路徑上的路徑或使用「文檔」資料類型的變數來選擇輸入PDF。 比如說， [負載目錄]/Workflow/PDF/credit-card.pdf。 crx-repository中不存在路徑。 管理員在使用路徑之前建立路徑。 您需要啟用「記錄文檔」選項或基於表單模板的「自適應Forms」來使用「PDF路徑」選項。
* **[!UICONTROL 對於已完成的任務，將自適應表單渲染為]**:當任務標籤為完成時，可將自適應表單呈現為只讀自適應表單或PDF文檔。 您需要啟用「記錄文檔」選項或基於表單模板的「自適應Forms」來將「自適應表單」呈現為「記錄文檔」。
* **[!UICONTROL 預填充]**:下面列出的下列欄位是任務的輸入：

   * **[!UICONTROL 使用]**:輸入資料檔案（.json、.xml、.doc或表單資料模型）的路徑。 可以使用相對於負載的路徑檢索輸入資料檔案，或檢索儲存在文檔、XML或JSON資料類型變數中的檔案。 例如，檔案包含通過收件箱應用程式為表單提交AEM的資料。 示例路徑是 [負載目錄]/workflow/data。
   * **[!UICONTROL 使用]**:在該位置可用的附件將附加到與任務關聯的表單。 該路徑可以相對於有效載荷或檢索儲存在文檔變數中的附件。 示例路徑是 [負載目錄]/attachments/。 您可以指定相對於負載放置的附件，或使用文檔類型（「陣列清單」>「文檔」）變數為「自適應表單」指定輸入附件。

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 請求屬性映射]**:使用「請求屬性映射」部分定義 [請求屬性的名稱和值](work-with-form-data-model.md#bindargument)。 根據請求中指定的屬性名稱和值從資料源檢索詳細資訊。 可以使用字面值或字串資料類型的變數定義請求屬性值。

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 已提交資訊]**:下面列出的下列欄位用作任務的輸出位置：

   * **[!UICONTROL 使用保存輸出資料檔案]**:保存資料檔案（.json、.xml、.doc或表單資料模型）。 資料檔案包含通過關聯表單提交的資訊。 可以使用相對於負載的路徑保存輸出資料檔案，或將其儲存在Document、XML或JSON資料類型的變數中。 比如說， [負載目錄]/Workflow/data，其中資料是檔案。
   * **[!UICONTROL 使用]**:保存任務中提供的表單附件。 可以使用與負載相關的路徑保存附件，或將其儲存在「文檔」資料類型的陣列清單的變數中。
   * **[!UICONTROL 使用保存記錄文檔]**:保存記錄文檔的路徑。 比如說， [負載目錄]/DocumentofRecord/credit-card.pdf。 可以使用相對於負載的路徑保存「記錄文檔」，或將其儲存在「文檔」資料類型的變數中。 如果選擇 **[!UICONTROL 相對於負載]** 選項，如果路徑欄位為空，則不生成記錄文檔。 僅當從「類型」(Type)下拉清單中選擇「自適應表單」(Adaptive Form)時，此選項才可用。

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 受分配人]** > **[!UICONTROL 分配選項]**:指定將任務分配給用戶的方法。 您可以使用「參與者選擇器」指令碼將任務動態分配給用戶或組，或將任務分配給AEM特定用戶或組。
* **[!UICONTROL 參與者選擇器]**:當 **[!UICONTROL 動態到用戶或組]** 選項。 可以使用ECMAScript或服務動態選擇用戶或組。 有關詳細資訊，請參見 [將工作流動態分配給用戶](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) 和 [建立自定義Adobe Experience Manager動態參與者步驟。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL 參與者]**:當 **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** 的子菜單。 **[!UICONTROL 參與者選擇器]** 的子菜單。 該欄位允許您為RandomParticipantChooser選項選擇用戶或組。

* **[!UICONTROL 受分配人]**:當 **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** 中 **[!UICONTROL 參與者選擇器]** 的子菜單。 該欄位允許您選擇字串資料類型的變數來定義工作負責人。

* **[!UICONTROL 參數]**:當在「參與者選擇器」欄位中選擇了RandomParticipantChoose指令碼以外的指令碼時，此欄位可用。 該欄位允許您為在「參與者選擇器」欄位中選擇的指令碼提供以逗號分隔的參數清單。

* **[!UICONTROL 用戶或組]**:該任務已分配給選定的用戶或組。 當 **[!UICONTROL 到特定用戶或組選項]** 中 **[!UICONTROL 分配選項]** 的子菜單。 該欄位列出了 [!DNL workflow-users] 組。\
   的 **[!UICONTROL 用戶或組]** 下拉菜單列出了登錄用戶有權訪問的用戶和組。 用戶名顯示取決於您是否對 **[!UICONTROL 用戶]** crx-repository中的節點。

* **[!UICONTROL 發送通知電子郵件]**:選擇此選項可向受分配人發送電子郵件通知。 當將任務分配給用戶或組時，會發送這些通知。 您可以使用 **[!UICONTROL 收件人電子郵件地址]** 的子菜單。

* **[!UICONTROL 收件人電子郵件地址]**:您可以將電子郵件地址儲存在變數中，使用文字指定永久電子郵件地址，或使用在受分配人配置檔案中指定的受分配人的預設電子郵件地址。 可以使用文字或變數指定組的電子郵件地址。 變數選項在動態檢索和使用電子郵件地址時非常有用。 的 **[!UICONTROL 使用受分配人的預設電子郵件地址]** 選項僅適用於單個工作負責人。 在這種情況下，使用儲存在受分配者用戶配置檔案中的電子郵件地址。

* **[!UICONTROL HTML電子郵件模板]**:為通知電子郵件選擇電子郵件模板。 要編輯模板，請修改crx-repository中/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt上的檔案。
* **[!UICONTROL 允許委派到]**:收AEM件箱為已登錄用戶提供了一個選項，可將分配的工作流委託給其他用戶。 您可以委託同一組內或委託給另一組的工作流用戶。 如果任務已分配給單個用戶， **[!UICONTROL 允許委派給受分配組的成員]** 選項，則無法將任務委託給其他用戶或組。
* **[!UICONTROL 共用設定]**:「收AEM件箱」提供了與其他用戶共用收件箱中單個或所有任務的選項：
   * 當 **[!UICONTROL 允許受分配人在收件箱中顯式共用]** 選項，用戶可以在收件箱中選擇任AEM務，並與其他用戶AEM共用。
   * 當 **[!UICONTROL 允許受分配人通過收件箱共用共用]** 選項，並且用戶共用其收件箱項或允許其他用戶訪問其收件箱項，只有啟用了先前提及的選項的任務才與其他用戶共用。
   * 當 **[!UICONTROL 允許受分配人使用「外出」設定委派]** 的子菜單。 受分配人可以啟用將任務委派給其他用戶的選項以及其他「外出」選項。 分配給外出用戶的任何新任務都自動被委派（分配）到外出設定中提到的用戶。

   它允許其他用戶在外出時選擇受分配者任務，並且無法處理已分配的任務。

* **[!UICONTROL 操作]** > **[!UICONTROL 預設操作]**:現成的「提交」、「保存」和「重置」操作可用。 預設情況下，所有預設操作都處於啟用狀態。
* **[!UICONTROL 路由變數]**:路由變數的名稱。 路由變數捕獲用戶在收件箱中選擇的自定AEM義操作。
* **[!UICONTROL 路由]**:任務可以分支到不同的路由。 當在「收件箱」AEM中選中時，該路由將返回一個值，並基於所選路由返回工作流分支。 可以將路由儲存在字串資料類型的陣列變數中，或選擇 **[!UICONTROL 文字]** 以手動添加路由。

* **[!UICONTROL 路由標題]**:指定路由的標題。 它顯示在收件箱AEM中。
* **[!UICONTROL 珊瑚表徵圖]**:指定珊瑚表徵圖的HTML屬性。 AdobeCorelUI庫提供大量的觸摸優先表徵圖。 您可以選擇並使用路由表徵圖。 它與「收件箱」中的標題一起AEM顯示。 如果將路由儲存在變數中，則路由使用預設的「標籤」珊瑚表徵圖。
* **[!UICONTROL 允許受分配人添加註釋]**:選擇此選項可為任務啟用注釋。 任務提交時，受分配人可AEM以在收件箱內添加註釋。
* **[!UICONTROL 在變數中保存注釋]**:將注釋保存在字串資料類型的變數中。 僅當選擇 **[!UICONTROL 允許受分配人添加註釋]** 複選框。

* **[!UICONTROL 允許受分配人向任務添加附件]**:選擇此選項可為任務啟用附件。 任務提交時，受分配人可AEM以從收件箱中添加附件。 也可以限制最大大小 **[!UICONTROL （最大檔案大小）]** 附件。 預設大小為2 MB。

* **[!UICONTROL 使用保存輸出任務附件]**:指定附件資料夾的位置。 可以使用相對於負載的路徑或文檔資料類型陣列的變數來保存輸出任務附件。 僅當選擇 **[!UICONTROL 允許受分配人向任務添加附件]** 複選框，選擇 **[!UICONTROL 自適應窗體]**。 **[!UICONTROL 只讀自適應窗體]**&#x200B;或 **[!UICONTROL 非互動式PDF文檔]** 從 **[!UICONTROL 類型]** 下拉清單 **[!UICONTROL 窗體/文檔]** 頁籤。

* **[!UICONTROL 使用自定義元資料]**:選擇此選項以啟用自定義元資料欄位。 自定義元資料用於電子郵件模板。
* **[!UICONTROL 自定義元資料]**:為電子郵件模板選擇自定義元資料。 自定義元資料可在apps/fd/dashboard/scripts/metadataScripts的crx-repository中使用。 crx-repository中不存在指定的路徑。 管理員在使用路徑之前建立路徑。 您還可以為自定義元資料使用服務。 也可以擴展 `WorkitemUserMetadataService` 提供自定義元資料的介面。
* **[!UICONTROL 顯示前一步中的資料]**:選擇此選項可使任務負責人查看以前的任務負責人、已對任務採取的操作、添加到任務的注釋以及已完成任務的記錄文檔（如果可用）。
* **[!UICONTROL 顯示後續步驟中的資料]**:選擇此選項可使當前受分配人查看後續受分配人所採取的操作和添加到任務的注釋。 它還允許當前受分配人查看已完成任務的「記錄文檔」(Document of Record)（如果可用）。
* **[!UICONTROL 資料類型的可見性]**:預設情況下，受分配人可以查看「記錄文檔」、受分配人、採取的操作以及先前和後續受分配人已添加的注釋。 使用資料類型的可見性選項限制受分配方可見的資料類型。

>[!NOTE]
>
>在為外部資料儲存配置工作流模型時，將「分配任務」步驟另存為草稿並檢索「分配任務」步驟歷史記錄的選項AEM將被禁用。 此外，在「收件箱」中，禁用了保存選項。

## 轉換為PDF/步驟 {#convert-pdfa}

PDF/A是一種存檔格式，用於通過嵌入字型和解壓縮檔案來長期保存文檔的內容。 因此，PDF/A文檔通常比標準PDF文檔大。 您可以使用 ***轉換為PDF/A*** 的上界AEM。

轉換為PDF/A步驟具有以下屬性：

**[!UICONTROL 輸入文檔]**:輸入文檔可以相對於有效載荷，具有絕對路徑，可以作為有效載荷提供或儲存在文檔資料類型的變數中。

**[!UICONTROL 轉換選項]**:使用此屬性，指定將PDF文檔轉換為PDF/A文檔的設定。 此頁籤下提供的各種選項包括：
* **[!UICONTROL 合規性]**:指定輸出PDF/A文檔必須遵守的標準。
* **[!UICONTROL 結果級別]**:指定轉換輸出的結果級別為PassFail、Summary或Detailed。
* **[!UICONTROL 顏色空間]**:指定用於輸出PDF/A檔案的預定義顏色空間。
* **[!UICONTROL 可選內容]**:僅當滿足指定的一組標準時，才允許在輸出PDF/A文檔中顯示特定圖形對象和/或注釋。

**[!UICONTROL 輸出文檔]**:指定保存輸出檔案的位置。 輸出檔案可以保存在與負載相關的位置，如果負載是檔案，則覆蓋負載，或保存在「文檔」資料類型的變數中。


## 發送電子郵件步驟 {#send-email-step}

使用電子郵件步驟發送電子郵件，例如帶有「記錄文檔」的電子郵件，以及自適應表單的連結 <!-- , link of an interactive communication-->或附加的PDF文檔。 「發送電子郵件」步驟支援 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 HTML電子郵件能夠響應並適應收件人的電子郵件客戶端和螢幕大小。 您可以使用HTML電子郵件模板來定義電子郵件的外觀、顏色方案和行為。

電子郵件步驟使用「第CQ天郵件服務」發送電子郵件。 使用電子郵件步驟之前，請確保已配置電子郵件服務。 預設情況下，電子郵件僅支援HTTP和HTTP協定。 [聯繫支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email) 啟用用於發送電子郵件的埠，並啟用環境的SMTP協定。 該限制有助於提高平台的安全性。

電子郵件步驟具有以下屬性：

**[!UICONTROL 標題]**:該步驟的標題有助於在工作流編輯器中確定該步驟。

**[!UICONTROL 說明]**:在共用開發環境中工作時，說明對其他流程開發人員非常有用。

**[!UICONTROL 電子郵件主題]**:可以從工作流元資料中檢索主題，手動指定或從變數中儲存的值中檢索主題。 從以下選項中選擇：

* **[!UICONTROL 文字]** 手動指定主題。
* **[!UICONTROL 從工作流元資料中檢索]**  — 從元資料屬性中檢索主題。
* **[!UICONTROL 變數]**  — 從字串資料類型變數中儲存的值中檢索主題。

**[!UICONTROL HTML電子郵件模板]**:HTML電子郵件模板。 可以在電子郵件模板中指定變數。 電子郵件步驟提取並顯示輸入模板中包含的所有變數。

**[!UICONTROL 電子郵件模板元資料]**:電子郵件模板變數的值可以是用戶指定的值、作者或發佈伺服器上資產的路徑、影像或工作流元資料屬性。

* **[!UICONTROL 文字]**:當知道要指定的精確值時，使用該選項。 比如說， [example@example.com](mailto:example@example.com)。

* **[!UICONTROL 工作流元資料]**:當要使用的值保存在工作流元資料屬性中時，請使用該選項。 選擇該選項後，在「工作流元資料」選項下的空文本框中輸入元資料屬性名稱。 例如， emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 影像]**:使用該選項將影像嵌入到電子郵件中。 選擇該選項後，瀏覽並選擇影像。 影像選項僅適用於電子郵件模板中可用的影像標籤(&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>)。&#42;

**[!UICONTROL 發件人/收件人的電子郵件地址]**:選擇 **[!UICONTROL 文字]** 選項，以手動指定電子郵件地址或選擇 **[!UICONTROL 從工作流元資料中檢索]** 選項從元資料屬性中檢索電子郵件地址。 您還可以為 **[!UICONTROL 從工作流元資料中檢索]** 的雙曲餘切值。 選擇 **[!UICONTROL 變數]** 選項，從字串資料類型變數中儲存的值檢索電子郵件地址。

* **[!UICONTROL 檔案附件]**:在指定位置可用的資產將附加到電子郵件。 資產的路徑可以是相對於有效負載的路徑或絕對路徑的路徑。 示例路徑是 [負載目錄]/attachments/。

選擇 **[!UICONTROL 變數]** 選項，以檢索儲存在文檔、XML或JSON資料類型變數中的檔案附件。

**[!UICONTROL 檔案名]**:電子郵件附件檔案的名稱。 「電子郵件步驟」將附件的原始檔案名更改為指定的檔案名。 可以手動指定名稱或從工作流元資料屬性或變數中檢索名稱。 使用 **[!UICONTROL 文字]** 的子菜單。 使用 **[!UICONTROL 變數]** 選項，從字串資料類型的變數中儲存的值檢索檔案名。 使用 **[!UICONTROL 從工作流元資料中檢索]** 選項。

## 生成記錄文檔步驟 {#generate-document-of-record-step}

填寫或提交表單時，您可以以打印或文檔格式保留表單記錄。 此記錄稱為記錄文檔(DoR)。 您可以使用「生成記錄文檔」步驟建立自適應表單的只讀或互動式PDF版本。 PDF版本包含填入表單的資訊以及「自適應表單」的佈局。

「記錄文檔」步驟具有以下屬性：

**[!UICONTROL 使用自適應窗體]**:指定定位輸入自適應表單的方法。 可以使用提交到工作流的自適應表單，該表單可以在絕對路徑上使用，也可以在變數的路徑上使用。 可以使用字串資料類型的變數指定 **[!UICONTROL 選擇要解析的變數]** 的子菜單。\
可以將多個AdaptiveForms與工作流關聯。 因此，可以使用可用的輸入方法在運行時指定自適應表單。

**[!UICONTROL 自適應窗體路徑]**:指定「自適應表單」的路徑。 選擇 **[!UICONTROL 在絕對路徑上可用]** 的 **[!UICONTROL 使用自適應窗體]** 的子菜單。

**[!UICONTROL 使用]**:自適應表單的輸入資料路徑。 您可以將資料保留在相對於負載的位置，指定資料的絕對路徑，或檢索儲存在文檔、JSON或XML資料類型變數中的資料。 輸入資料與自適應表單合併以建立記錄文檔。

**[!UICONTROL 使用]**:附件的路徑。 這些附件包含在記錄文檔中。 您可以將附件保留在相對於負載的位置，指定附件的絕對路徑，或檢索儲存在文檔資料類型陣列變數中的附件。

如果指定資料夾的路徑（例如，附件），則資料夾中直接可用的所有檔案都將附加到「記錄文檔」。 如果資料夾中有檔案直接位於指定的附件路徑中，則這些檔案將作為附件包含在「記錄文檔」中。 如果直接可用的資料夾中有任何資料夾，則跳過這些資料夾。

**[!UICONTROL 使用以下選項保存生成的記錄文檔]**:指定保留「記錄文檔」檔案的位置。 您可以選擇覆蓋負載資料夾、將「記錄文檔」(Document of Record)放置在負載目錄中的某個位置，或將「記錄文檔」(Document of Record)儲存在「文檔」(Document)資料類型的變數中。

**[!UICONTROL 區域設定]**:指定記錄文檔的語言。 選擇 **[!UICONTROL 文字]** 從下拉清單中選擇區域設定，或選擇 **[!UICONTROL 變數]** 從字串資料類型變數中儲存的值中檢索區域設定。 在變數中儲存區域設定值時，必須定義區域設定代碼。 例如，指定 **en_US** 英語和 **fr_FR** 法語。

## 調用DDX步驟 {#invokeddx}

文檔描述XML(DDX)是聲明性標籤語言，其元素表示文檔的構建塊。 這些構造塊包括PDF和XDP文檔，以及諸如注釋、書籤和樣式文本等其他元素。 DDX定義一組操作，這些操作可以應用於一個或多個輸入文檔以生成一個或多個輸出文檔。  單個DDX可與一系列源文檔一起使用。 您可以使用 ***調用DDX步驟*** 在工AEM作流中執行各種操作，如「匯編拆卸文檔」、「建立和修改Acrobat」和XFAForms，以及中介紹的其他操作 [DDX參考文檔](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)。

調用DDX步驟具有以下屬性：

**[!UICONTROL 輸入文檔]**:用於設定輸入文檔的屬性。 此頁籤下提供的各種選項包括：
* **[!UICONTROL 指定DDX使用]**:指定相對於負載的輸入文檔、具有絕對路徑、可以作為負載提供或儲存在文檔資料類型的變數中。
* **[!UICONTROL 從負載建立映射]**:將有效負載資料夾下的所有文檔添加到匯編器中調用API的「輸入文檔」映射中。 每個文檔的節點名稱用作映射中的鍵。
* **[!UICONTROL 輸入文檔的映射]**:選項用於使用 **[!UICONTROL 添加]** 按鈕 每個條目都表示映射中文檔的鍵和文檔的源。

**[!UICONTROL 環境選項]**:此選項用於設定調用API的處理設定。 此頁籤下提供的各種選項包括：
* **[!UICONTROL 僅驗證]**:檢查輸入DDX文檔的有效性。
* **[!UICONTROL 錯誤時失敗]**:檢查調用API服務是否失敗（如果出現錯誤）。 預設情況下，其值設定為False。
* **[!UICONTROL 第一個Bates數]**:指定自增量的數字。 此自增量數字將自動顯示在每個連續頁面上。
* **[!UICONTROL 預設樣式]**:設定輸出檔案的預設樣式。

>[!NOTE]
>
>環境選項與HTTP API保持同步。

**[!UICONTROL 輸出文檔]**:指定保存輸出檔案的位置。 此頁籤下提供的各種選項包括：
* **[!UICONTROL 在負載中保存輸出]**:將輸出文檔保存在負載資料夾下，或覆蓋負載，以防負載是檔案。
* **[!UICONTROL 輸出文檔的映射]**:通過為每個文檔添加一個條目，指定顯式保存每個文檔檔案的位置。 每個條目都表示文檔和保存文檔的位置。 如果有多個輸出文檔，則使用此選項。

## 調用表單資料模型服務步驟 {#invoke-form-data-model-service-step}

您可以使用 [[!DNL AEM Forms] 資料整合](data-integration.md) 配置和連接到不同的資料源。 這些資料源可以是Web服務、REST服務、OData服務和CRM解決方案。 [!DNL AEM Forms] 資料整合允許您建立包含各種服務的表單資料模型，以對配置的資料庫執行資料檢索、添加和更新操作。 您可以使用 **[!UICONTROL 調用資料模型服務步驟]** 選擇表單資料模型(FDM)，並使用FDM的服務來檢索、更新或向不同資料源添加資料。

要解釋步驟欄位的輸入，以下資料庫表和JSON檔案將用作示例：

**[!UICONTROL CustomerDetails表示例]**

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>值<br /> </td> 
  </tr> 
  <tr> 
   <td>名字<br /> </td> 
   <td>莎拉<br /> </td> 
  </tr> 
  <tr> 
   <td>姓氏</td> 
   <td>玫瑰</td> 
  </tr> 
  <tr> 
   <td>客戶ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>電子郵件地址<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL 示例JSON檔案]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

「調用表單資料模型服務」步驟包含下列欄位，以便於表單資料模型操作：

* **[!UICONTROL 標題]**:步驟的標題。 它有助於確定工作流編輯器中的步驟。
* **[!UICONTROL 說明]**:在共用開發環境中工作時，對其他流程開發者有用的說明。

* **[!UICONTROL 表單資料模型路徑]**:瀏覽並選擇伺服器上存在的表單資料模型。

* **[!UICONTROL 錯誤和驗證]**:該選項允許您捕獲錯誤消息並為檢索到併發送到資料源的資料指定驗證選項。 通過這些更改，您可以確保傳遞到「調用表單資料模型服務」步驟的資料遵守由資料源定義的資料約束。 有關詳細資訊，請參閱 [輸入資料的自動驗證](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 驗證級別]**:驗證分為三類：基本、完全和關閉：

   * 滿：驗證了所有約束。
   * 基本：僅必需和可空的約束
   * 關閉：不進行驗證。

* **[!UICONTROL 失敗時終止工作流]**:當約束無法驗證時，將停止工作流。

* **[!UICONTROL 在變數中儲存錯誤代碼]**:可以將錯誤代碼儲存在 [字串類型變數](variable-in-aem-workflows.md)。

* **[!UICONTROL 在變數中儲存錯誤消息]**:您可以在 [字串類型變數](variable-in-aem-workflows.md)。

* **[!UICONTROL 在變數中儲存錯誤詳細資訊]**:您可以將錯誤詳細資訊儲存在 [JSON類型變數](variable-in-aem-workflows.md)。

* **[!UICONTROL 服務]**:所選表單資料模型提供的服務清單。
* **[!UICONTROL 服務輸入]** > **[!UICONTROL 使用文本、變數或工作流元資料和JSON檔案提供輸入資料]**:服務可以具有多個參數。 選擇該選項以從工作流元資料屬性、JSON對象、變數中獲取服務參數的值，或直接在提供的文本框中輸入值：

   * **[!UICONTROL 文字]**:當知道要指定的精確值時，使用該選項。 例如，srose@we.info。
   * **[!UICONTROL 變數]**:使用該選項檢索儲存在變數中的值。
   * **[!UICONTROL 從工作流元資料中檢索]**:當要使用的值保存在工作流元資料屬性中時，請使用該選項。 例如， emailAddress。

   * **[!UICONTROL 相對於負載]**:使用此選項檢索保存在相對於負載的路徑上的檔案附件。 選擇該選項並指定包含檔案附件的資料夾名稱或在文本框中指定檔案附件名稱。

      例如，如果CRX儲存庫中的「相對負載」資料夾包含位於 `attachment\attachment-folder` 位置，指定 `attachment\attachment-folder` 的子菜單。 **[!UICONTROL 相對於負載]** 的雙曲餘切值。

   * **[!UICONTROL JSON點符號]**:當要使用的值在JSON檔案中時，請使用該選項。 例如， insurance.customerDetails.emailAddress。 僅當從輸入JSON選項中選擇了「映射」輸入欄位時，JSON點表示法選項才可用。
   * **[!UICONTROL 從輸入JSON映射輸入欄位]**:指定JSON檔案的路徑，以從JSON檔案獲取某些服務參數的輸入值。 JSON檔案的路徑可以是相對於負載、絕對路徑的路徑，也可以使用JSON或窗體資料模型類型的變數選擇輸入JSON文檔。

* **[!UICONTROL 服務輸入]** > **[!UICONTROL 使用變數或JSON檔案提供輸入資料]**:選擇該選項可從保存在絕對路徑、相對於負載的路徑或變數中的JSON檔案中獲取所有參數的值。
* **[!UICONTROL 使用選擇輸入JSON文檔]**:包含所有服務參數值的JSON檔案。 JSON檔案的路徑可以是 **[!UICONTROL 相對於負載]** 或 **[!UICONTROL 絕對路徑]**。 您還可以使用JSON或表單資料模型資料類型的變數檢索輸入JSON文檔。

* **[!UICONTROL JSON點符號]**:將該欄位留空，以將指定JSON檔案的所有對象用作服務參數的輸入。 要從指定的JSON檔案中讀取特定JSON對象作為服務參數的輸入，請為JSON對象指定點符號，例如，如果JSON與節開頭列出的JSON類似，請指定insuran.customerDetails以提供客戶的所有詳細資訊作為服務的輸入。
* **[!UICONTROL 服務產出]** > **[!UICONTROL 將輸出值映射到變數或元資料]**:選擇該選項可將輸出值另存為crx-repository中工作流實例元資料節點的屬性。 指定元資料屬性的名稱並選擇要與元資料屬性映射的相應服務輸出屬性，例如，將輸出服務返回的phonenumber與工作流元資料的phonenumber屬性進行映射。 同樣，可以將輸出儲存在Long資料類型的變數中。 為 **[!UICONTROL 要映射的服務輸出屬性]** 選項，只為 **[!UICONTROL 將輸出保存到]** 的雙曲餘切值。

* **[!UICONTROL 服務產出]** > **[!UICONTROL 將輸出保存到變數或JSON檔案]**:選擇該選項可將輸出值保存在JSON檔案中的絕對路徑、相對於負載的路徑或變數中。
* **[!UICONTROL 使用以下選項保存輸出JSON文檔]**:保存輸出JSON檔案。 輸出JSON檔案的路徑可以是相對於負載的路徑或絕對路徑。 您還可以使用JSON或表單資料模型資料類型的變數保存輸出JSON檔案。

## 簽署文檔步驟 {#sign-document-step}

「簽名文檔」(Sign Document)步驟使您能夠 [!DNL Adobe Sign] 來簽署文檔。 當您使用 [!DNL Adobe Sign] 工作流程步驟在最適化表單上簽名時，視工作流程設定步驟而定，此表單可以在簽名者之間逐一傳遞，或同時傳送給所有簽名者。啟用 [!DNL Adobe Sign] 的最適化表單只會在所有簽名者完成簽名程序後提交給 Experience Manager Forms 伺服器。

[!DNL Adobe Sign] 排程器服務預設為每 24 小時檢查 (輪詢) 簽名者回應。你可以 [更改環境的預設間隔](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status)。

「簽名文檔」步驟具有以下屬性：

* **[!UICONTROL 協定名稱]**:指定協定的標題。 協定名稱將成為發送到簽名者的電子郵件的主題和正文文本的一部分。 可以將名稱儲存在字串資料類型的變數中，或選擇 **[!UICONTROL 文字]** 以手動添加名稱。

* **[!UICONTROL 區域設定]**:指定電子郵件和驗證選項的語言。 可以將區域設定儲存在字串資料類型的變數中，或選擇 **[!UICONTROL 文字]** 選項。 在變數中儲存區域設定值時，必須定義區域設定代碼。 例如，指定 **[!UICONTROL en_US]** 英語和 **[!UICONTROL fr_FR]** 法語。

* **[!UICONTROL Adobe Sign雲配置]**:選擇 [!DNL Adobe Sign] 雲配置。 如果尚未配置 [!DNL Adobe Sign] 為 [!DNL AEM Forms]，請參閱 [將Adobe Sign與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)。

* **[!UICONTROL 選擇要使用簽名的文檔]**:可以從相對於負載的位置選擇文檔，將負載用作文檔，指定文檔的絕對路徑，或檢索儲存在「文檔」資料類型變數中的文檔。
* **[!UICONTROL 截止日期]**:在任務中指定的天數內沒有活動後，文檔將標籤為到期（已過期） **[!UICONTROL 截止日期]** 的子菜單。 在將記錄的天數分配給用戶進行簽名後計算。
* **[!UICONTROL 提醒電子郵件頻率]**:您可以按每日或每週間隔發送提醒電子郵件。 從將文檔指定給用戶進行簽名之日起計算周。
* **[!UICONTROL 簽名過程]**:您可以選擇按順序或並行順序對文檔進行簽名。 按順序，一個簽名者每次接收文檔以進行簽名。 第一簽名者完成對文檔的簽名後，將文檔發送給第二簽名者等。 同時，多個簽名者可以一次對文檔進行簽名。
* **[!UICONTROL 重定向URL]**:指定重定向URL。 在文檔簽名後，您可以將受分配人重定向到URL。 通常，此URL包含感謝信或進一步說明。
* **[!UICONTROL 工作流階段]**:工作流可以具有多個階段。 這些階段顯示在收件箱AEM中。 可以在模型的屬性中定義這些階段( **[!UICONTROL 側腳]** > **[!UICONTROL 頁面]** > **[!UICONTROL 頁面屬性]** > **[!UICONTROL 階段]**)。
* **[!UICONTROL 選擇簽名者]**:指定為文檔選擇簽名者的方法。 您可以動態將工作流分配給用戶或組，或手動添加簽名者的詳細資訊。
* **[!UICONTROL 指令碼或服務以選擇簽名者]**:僅當在「選擇簽名者」(Select Signers)欄位中選擇了「動態」(Dynamically)選項時，此選項才可用。 可以指定ECMAScript或服務來為文檔選擇簽名器和驗證選項。
* **[!UICONTROL 簽名者詳細資訊]**:僅當在「選擇簽名者」(Select Signers)欄位中選擇了「手動」(Manual)選項時，此選項才可用。 指定電子郵件地址並選擇可選的驗證機制。 在選擇兩步驗證機制之前，請確保已配置的驗證選項已啟用 [!DNL Adobe Sign] 帳戶。 可以使用字串資料類型的變數來定義「電子郵件」、「國家/地區代碼」和「電話號碼」欄位的值。 僅當從2步驗證下拉清單中選擇電話驗證時，才會顯示「國家/地區代碼」和「電話號碼」欄位。

<!-- 

## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).

### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.

### Generate Printed Output Step {#generatePrintedOutput}

The step generates a PCL, PostScript, ZPL, IPL, TPCL, or DPL output given a form design and data file. The data file is merged with the form design and formatted for printing. The output generated by this step can be sent directly to a printer or saved as file. It is recommended that you use this step when you want to use form designs or data from an application. If your form designs or form designs are located on the network, local file system, or HTTP location, use the generatePrintedOutput operation operation.

For example, your application requires that you merge a form design with a data file. The data contains hundreds of records. In addition, it requires the output is sent to a printer that supports ZPL. The form design and your input data are located in an application. Use the generatePrintedOutput operation to merge each record with a form design and send the output to a printer that supports ZPL.

The Generate Printed Output step has the following properties:

**[!UICONTROL Input properties]**

* **[!UICONTROL Select template file using]**: Specify the path of the template file. You can select the template file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it. Moreover, you can also accept payload as the input data file.

* **[!UICONTROL Select data document using]**: Specify the path of a input data file. You can select the input data file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it.

* **[!UICONTROL Printer Format]**: A Print Format value that specifies the page description language to use, when an XDC file is not provided, to generate the output stream. If you provide a literal value, select one of these values:

  * **[!UICONTROL Custom PCL]**: Use the option to specify a custom XDC file for PCL.
  * **[!UICONTROL Custom PostScript]**: Use the option to specify a custom XDC file for PostScript.
  * **[!UICONTROL Custom ZPL]**: Use the option to specify a custom XDC file file for ZPL.
  * **[!UICONTROL Generic Color PCL (5c)]**: Use a generic color PCL (5c).
  * **[!UICONTROL Generic PostScript Level3]**: Use generic PostScript Level 3.
  * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. The zpl300.xdc is used.
  * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. The zpl600.xdc file is used.
  * **[!UICONTROL Custom IPL]**: Use the option to specify a custom XDC file for IPL.
  * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. The ipl300.xdc is used.
  * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. The ipl400.xdc file is used.
  * **[!UICONTROL Custom TPCL]**: Use the option to specify a custom XDC file for TPCL.
  * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. The tpcl305.xdc file is used.
  * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. The tpcl600.xdc file is used.
  * **[!UICONTROL Custom DPL]**: Use the option to specify a custom XDC file DPL.
  * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. The dpl300.xdc file is used.
  * **[!UICONTROL DPL406DPI]**: Use DPL 400 DPI. The dpl406.xdc is used.
  * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. The dpl600.xdc is used.

**[!UICONTROL Output Properties]**

* **[!UICONTROL Save output document using]**: Specify the location to save the output file. You can save the output file at an location  which is relative to the payload, in a variable, or specify an absolute location to save the output file. If the path does not exist in crx-repository, an administrator can create the path before using it.

**[!UICONTROL Advanced Properties]**

* **[!UICONTROL Select Content Root location using]**: Content root is a string value that specifies the URI, absolute reference, or location in the repository to retrieve relative assets used by the form design. For example, if the form design references an image relatively, such as ../myImage.gif, myImage.gif must be located at repository://. The default value is repository://, which points to the root level of the repository.

  When you pick an asset from your application, the Content Root URI path must have the correct structure. For example, if a form is picked from an application named SampleApp, and is placed at SampleApp/1.0/forms/Test.xdp, the Content Root URI must be specified as repository://administrator@password/Applications/SampleApp/1.0/forms/, or repository:/Applications/SampleApp/1.0/forms/ (when authority is null). When the Content Root URI is specified this way, the paths of all of the referenced assets in the form will be resolved against this URI.

* **[!UICONTROL Select XCI file using]**: XCI files are used to describe fonts and other properties that are used for form design elements. You can keep an XCI file relative to the payload, at an absolute path, or using a variable of Document data type.

* **[!UICONTROL Locale]**: Specifies the language used for generating the PDF document. If you provide a literal value, select a language from the list or select one of these values:
  * **[!UICONTROL To use server default]**:
    (Default) Use the Locale setting configured on the [!DNL AEM Forms] Server. The Locale setting is configured using Administration Console. (See [Designer Help](http://www.adobe.com/go/learn_aemforms_designer_65).)

  * **[!UICONTROL To use custom value]**:
    Type the Locale code in the literal box or select a string variable containing the locale code. For a complete list of supported locale codes, see http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]**: An integer value that specifies the number of copies to generate for the output. The default value is 1.

* **[!UICONTROL Duplex Printing]**:  A Pagination value that specifies whether to use two-sided or single-sided printing. Printers that support PostScript and PCL use this value.If you provide a literal value, select one of these values:
    * **[!UICONTROL Duplex Long Edge]**: Use two-sided printing and print using long-edge pagination. 
    * **[!UICONTROL Duplex Short Edge]**: Use two-sided printing and print using short-edge pagination. 
    * **[!UICONTROL Simplex]**: Use single-sided printing.
    
    -->
