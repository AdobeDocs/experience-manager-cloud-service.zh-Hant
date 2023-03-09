---
title: 如何將工作流程指派給其他使用者、傳送電子郵件、在工作流程中使用Adobe Sign?
description: 以Forms為中心的工作流程可讓您快速建立以Forms為基礎的最適化工作流程。 您可以使用Adobe Sign來電子簽署檔案、建立表單式業務流程、擷取資料並傳送至多個資料來源，以及傳送電子郵件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '7190'
ht-degree: 1%

---

# Forms導向的AEM工作流程 — 步驟參考 {#forms-centric-workflow-on-osgi-step-reference}

您可以使用工作流模型將業務邏輯轉換為自動重複性流程。 模型可協助您定義及執行一系列步驟。 您也可以定義模型屬性，例如工作流是暫時性的，還是使用多個資源。 您可以 [在模型中納入各種AEM工作流程步驟，以達成業務邏輯](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Forms中心步驟 {#forms-workflow-steps}

以Forms為中心的工作流程步驟會在AEM工作流程中執行AEM Forms專屬的操作。 這些步驟可讓您在OSGi上快速建立以Forms為中心的最適化Forms工作流程。 這些工作流可用於開發基本的審核和批准工作流、內部和跨防火牆業務流程。 您也可以使用Forms Workflow步驟：

* 建立業務流程、提交後工作流程和後端工作流程，以管理註冊流程。

* 建立任務並將其分配給用戶或組。

* 使用 [!DNL Adobe Sign] 在AEM工作流程中傳送要簽署的檔案。

* 按需或在提交表單時生成記錄文檔。

* 將工作流程模型與各種資料來源連結，以輕鬆儲存和擷取資料。

* 使用電子郵件步驟，在完成動作和在工作流程開始或完成時傳送通知電子郵件和其他附件。

>[!NOTE]
>
>如果將工作流模型標籤為外部儲存，則對於所有Forms工作流步驟，您只能選擇變數選項來儲存或檢索資料檔案和附件。


## 分配任務步驟 {#assign-task-step}

分配任務步驟將建立工作項並將其分配給用戶或組。 除了指定任務外，元件還指定任務的最適化表單或非互動式PDF。 需要「適用性表單」來接受使用者的輸入，而非互動式PDF，或只供審核工作流程使用的唯讀適用性表單。

您也可以使用元件來控制任務的行為。 例如，建立自動記錄文檔，將任務分配給特定的用戶或組，指定提交資料的路徑，指定要預先填入的資料路徑，並指定預設操作。 分配任務步驟具有以下屬性：

* **[!UICONTROL 標題]**:任務的標題。 標題會顯示在AEM收件匣中。
* **[!UICONTROL 說明]**:對任務中正在執行的操作的說明。 當您在共用開發環境中工作時，此資訊對於其他程式開發人員很實用。

* **[!UICONTROL 縮圖路徑]**:任務縮圖的路徑。 如果未指定路徑，則會為「適用性表單」預設縮圖顯示，為「記錄檔案」顯示預設圖示。
* **[!UICONTROL 工作流程階段]**:工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型的屬性中定義這些階段（Sidekick >頁面>頁面屬性>階段）。
* **[!UICONTROL 優先順序]**:選取的優先順序會顯示在AEM收件匣中。 可用選項有高、中和低。 預設值為Medium。
* **[!UICONTROL 到期日]**:指定任務標籤為過期的天數或小時數。 如果您選取 **[!UICONTROL 關閉]**，則任務永遠不會標籤為過期。 您也可以指定超時處理程式，以在任務逾期後執行特定任務。

* **[!UICONTROL 天]**:任務完成的天數。 將任務分配給用戶後計算的天數。 如果任務未完成，且越過「天」欄位中指定的天數，則如果選中，則在到期日後觸發超時處理程式。
* **[!UICONTROL 小時]**:任務完成前的小時數。 將任務分配給用戶後計算的小時數。 如果任務未完成，且越過「小時」欄位中指定的小時數，則如果選中，則在到期小時後觸發超時處理程式。
* **[!UICONTROL 到期日後超時]**:選擇此選項以啟用「逾時處理常式」選取欄位。
* **[!UICONTROL 逾時處理常式]**:選擇要在分配任務步驟跨到期日期時執行的指令碼。 放置於CRX-repository的指令碼 [app]/fd/dashboard/scripts/timeoutHandler可供選取。 crx-repository中不存在指定的路徑。 管理員在使用路徑之前會建立路徑。
* **[!UICONTROL 在「任務詳細資訊」中突出顯示最後一個任務中的操作和注釋]**:選擇此選項可顯示上次採取的操作以及在任務的任務詳細資訊部分收到的注釋。
* **[!UICONTROL 類型]**:選擇啟動工作流時要填寫的文檔類型。 您可以選擇適用性表單、唯讀適用性表單、非互動式PDF檔案。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用最適化表單]**:指定尋找輸入「最適化表單」的方法。 如果您從「類型」下拉式清單中選取「適用性表單」或「唯讀適用性表單」，即可使用此選項。 您可以使用提交至工作流程的適用性表單、絕對路徑可用，或變數中的路徑可用。 您可以使用字串類型的變數來指定路徑。\
   您可以將多個適用性Forms與工作流程建立關聯。 因此，您可以使用可用的輸入方法在執行階段中指定適用性表單。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 最適化表單路徑]**:指定最適化表單的路徑。 您可以使用提交至工作流程的適用性表單（以絕對路徑提供），或從儲存在字串資料類型變數中的路徑擷取適用性表單。
* **[!UICONTROL 使用選擇輸入PDF]**:指定非互動式PDF文檔的路徑。 在「類型」欄位中選擇非互動式PDF文檔時，該欄位可用。 您可以使用相對於有效負載的路徑、保存在絕對路徑上的路徑，或使用文檔資料類型的變數來選擇輸入PDF。 例如， [裝載目錄]/Workflow/PDF/credit-card.pdf。 crx-repository中不存在路徑。 管理員在使用路徑之前會建立路徑。 若要使用「PDF路徑」選項，您需要啟用「記錄檔案」選項，或使用基於表單範本的適用性Forms。
* **[!UICONTROL 對於完成的任務，將適用性表單呈現為]**:將任務標籤為完成時，您可以將適用性表單轉譯為唯讀適用性表單或PDF檔案。 您需要啟用「記錄檔案」選項或以表單範本為基礎的適用性Forms，才能將最適化表單轉譯為「記錄檔案」。
* **[!UICONTROL 預先填入]**:下列欄位可作為任務的輸入：

   * **[!UICONTROL 使用選擇輸入資料檔案]**:輸入資料檔案的路徑（.json、.xml、.doc或表單資料模型）。 您可以使用與裝載相關的路徑來擷取輸入資料檔案，或擷取儲存在檔案、XML或JSON資料類型變數中的檔案。 例如，檔案包含透過AEM收件匣應用程式為表單提交的資料。 範例路徑為 [裝載目錄]/workflow/data。
   * **[!UICONTROL 使用]**:該位置可用的附件將附加到與任務關聯的表單。 該路徑可以相對於裝載，或檢索儲存在文檔變數中的附件。 範例路徑為 [裝載目錄]/attachments/。 您可以指定相對於裝載放置的附件，或使用文檔類型（陣列清單>文檔）變數來指定適用性表單的輸入附件。

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 請求屬性對應]**:使用「請求屬性對應」區段來定義 [請求屬性的名稱和值](work-with-form-data-model.md#bindargument). 根據請求中指定的屬性名稱和值，從資料來源擷取詳細資料。 您可以使用常值或字串資料類型的變數來定義請求屬性值。

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 已提交的資訊]**:下列欄位作為任務的輸出位置：

   * **[!UICONTROL 使用保存輸出資料檔案]**:儲存資料檔案（.json、.xml、.doc或表單資料模型）。 資料檔案包含透過關聯表單提交的資訊。 您可以使用與裝載相對的路徑儲存輸出資料檔案，或將其儲存在檔案、XML或JSON資料類型的變數中。 例如， [裝載目錄]/Workflow/data，其中資料為檔案。
   * **[!UICONTROL 使用]**:保存任務中提供的表單附件。 您可以使用相對於裝載的路徑保存附件，或將其儲存在「文檔」資料類型的陣列清單的變數中。
   * **[!UICONTROL 使用保存記錄文檔]**:保存記錄檔案的路徑。 例如， [裝載目錄]/DocumentofRecord/credit-card.pdf。 您可以使用與裝載相關的路徑來保存記錄文檔，或將其儲存在文檔資料類型的變數中。 如果您選取 **[!UICONTROL 相對於裝載]** 選項，則如果路徑欄位為空，則不會生成記錄文檔。 只有在從「類型」下拉式清單中選取「最適化表單」時，才可使用此選項。

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 受託人]** > **[!UICONTROL 指派選項]**:指定將任務分配給用戶的方法。 您可以使用參與者選擇器指令碼將任務動態分配給用戶或組，或將任務分配給特定AEM用戶或組。
* **[!UICONTROL 參與者選擇器]**:當 **[!UICONTROL 動態地連結至使用者或群組]** 選項。 您可以使用ECMAScript或服務來動態選取使用者或群組。 如需詳細資訊，請參閱 [動態指派工作流程給使用者](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) 和 [建立自訂Adobe Experience Manager動態參與者步驟。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL 參與者]**:欄位在 **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** 選項 **[!UICONTROL 參與者選擇器]** 欄位。 欄位允許您為RandomParticipantChooser選項選擇用戶或組。

* **[!UICONTROL 受託人]**:欄位在 **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** 在 **[!UICONTROL 參與者選擇器]** 欄位。 欄位可讓您選取字串資料類型的變數，以定義受託人。

* **[!UICONTROL 引數]**:在「參與者選擇器」欄位中選擇了RandomParticipantChoose指令碼以外的指令碼時，該欄位可用。 欄位允許您為在「參與者選擇器」欄位中選擇的指令碼提供逗號分隔參數的清單。

* **[!UICONTROL 使用者或群組]**:該任務被分配給選定的用戶或組。 當 **[!UICONTROL 指定用戶或組選項]** 在 **[!UICONTROL 指派選項]** 欄位。 欄位會列出 [!DNL workflow-users] 群組。\
   此 **[!UICONTROL 使用者或群組]** 下拉式功能表會列出登入使用者可存取的使用者和群組。 使用者名稱的顯示取決於您是否擁有 **[!UICONTROL 使用者]** 該特定使用者的crx-repository中節點。

* **[!UICONTROL 傳送通知電子郵件]**:選取此選項，將電子郵件通知傳送給受託人。 將任務分配給用戶或組時，將發送這些通知。 您可以使用 **[!UICONTROL 收件者電子郵件地址]** 選項，指定擷取電子郵件地址的機制。

* **[!UICONTROL 收件者電子郵件地址]**:您可以將電子郵件地址儲存在變數中，使用常值來指定永久電子郵件地址，或使用受託人設定檔中指定之受託人的預設電子郵件地址。 您可以使用常值或變數來指定群組的電子郵件地址。 變數選項有助於動態擷取和使用電子郵件地址。 此 **[!UICONTROL 使用受託人的預設電子郵件地址]** 選項僅適用於單一受託人。 在這種情況下，會使用儲存在受分配的用戶配置檔案中的電子郵件地址。

* **[!UICONTROL HTML電子郵件範本]**:為通知電子郵件選取電子郵件範本。 若要編輯範本，請修改crx-repository中位於/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的檔案。
* **[!UICONTROL 允許委派至]**:AEM收件匣提供選項給登入的使用者，以將指派的工作流程委派給其他使用者。 您可以委派至相同群組內，或委派給其他群組的工作流程使用者。 如果將任務指派給單一使用者，且 **[!UICONTROL 允許委派給受讓人組的成員]** 選項，則無法將任務委派給其他用戶或組。
* **[!UICONTROL 共用設定]**:AEM收件匣提供可與其他使用者共用收件匣中單一或所有工作的選項：
   * 當 **[!UICONTROL 允許受託人明確在收件匣中共用]** 選項，則使用者可以在AEM收件匣中選取任務，並與其他AEM使用者共用。
   * 當 **[!UICONTROL 允許受託人透過收件匣共用來共用]** 選項，並且用戶共用其收件箱項或允許其他用戶訪問其收件箱項，則只有啟用前面提及的選項的任務才與其他用戶共用。
   * 當 **[!UICONTROL 允許受託人使用「外出」設定進行委派]** 中所有規則的URL。 受託人可以啟用將任務委派給其他用戶的選項以及其他「外出」選項。 任何指派給離職使用者的新任務都會自動委派（指派）給離職設定中提及的使用者。

   它允許其他用戶在任務不在辦公室且無法處理已分配的任務時選擇受分配的任務。

* **[!UICONTROL 動作]** > **[!UICONTROL 預設動作]**:現成可用的提交、儲存和重設動作。 預設會啟用所有預設動作。
* **[!UICONTROL 路由變數]**:路由變數的名稱。 路由變數會擷取使用者在AEM收件匣中選取的自訂動作。
* **[!UICONTROL 路由]**:任務可以分支到不同的路由。 在AEM收件匣中選取時，路由會傳回值，而工作流程會根據選取的路由分支。 您可以將路由儲存在String資料類型陣列的變數中，或選取 **[!UICONTROL 常值]** 手動添加路由。

* **[!UICONTROL 路由標題]**:指定路由的標題。 它會顯示在AEM收件匣中。
* **[!UICONTROL 珊瑚圖示]**:指定珊瑚圖示的HTML屬性。 AdobeCorelUI程式庫提供大量的觸控優先圖示。 您可以選擇並使用路由的表徵圖。 它會與標題一起顯示在AEM收件匣中。 如果將路由儲存在變數中，則路由會使用預設的「標籤」珊瑚圖示。
* **[!UICONTROL 允許受託人添加註釋]**:選擇此選項可為任務啟用注釋。 受託人可以在提交任務時從AEM收件匣中新增註解。
* **[!UICONTROL 在變數中儲存註解]**:將註解儲存在字串資料類型的變數中。 只有選取 **[!UICONTROL 允許受託人添加註釋]** 核取方塊。

* **[!UICONTROL 允許受託人向任務添加附件]**:選擇此選項可啟用任務的附件。 受託人可以在提交任務時從AEM收件匣中新增附件。 您也可以限制最大大小 **[!UICONTROL （檔案大小上限）]** 附件。 預設大小為2 MB。

* **[!UICONTROL 使用保存輸出任務附件]**:指定附件資料夾的位置。 您可以使用相對於裝載的路徑或文檔資料類型的陣列變數來保存輸出任務附件。 只有選取 **[!UICONTROL 允許受託人向任務添加附件]** 核取方塊與選取 **[!UICONTROL 適用性表單]**, **[!UICONTROL 唯讀適用性表單]**，或 **[!UICONTROL 非互動式PDF檔案]** 從 **[!UICONTROL 類型]** 下拉式清單 **[!UICONTROL 表單/檔案]** 標籤。

* **[!UICONTROL 使用自訂中繼資料]**:選取此選項以啟用自訂中繼資料欄位。 自訂中繼資料用於電子郵件範本。
* **[!UICONTROL 自訂中繼資料]**:為電子郵件範本選取自訂中繼資料。 自訂中繼資料可在crx-repository中取得，位於apps/fd/dashboard/scripts/metadataScripts。 crx-repository中不存在指定的路徑。 管理員在使用路徑之前會建立路徑。 您也可以對自訂中繼資料使用服務。 您也可以擴充 `WorkitemUserMetadataService` 提供自訂中繼資料的介面。
* **[!UICONTROL 顯示前幾個步驟的資料]**:選擇此選項可使受分配者查看以前的受分配者、已對任務採取的操作、添加到任務的注釋以及已完成任務的記錄文檔（如果可用）。
* **[!UICONTROL 顯示後續步驟的資料]**:選擇此選項可讓當前受託人查看後續受託人執行的操作和添加到任務的注釋。 它還允許當前受託人查看已完成任務的「記錄文檔」(Document of Record)（如果可用）。
* **[!UICONTROL 資料類型的可見性]**:預設情況下，受託人可以查看以前和以後受讓人添加的記錄文檔、受託人、所採取的操作和注釋。 使用資料類型的可見性選項來限制受分配者可見的資料類型。

>[!NOTE]
>
>為外部資料儲存配置AEM工作流模型時，將「分配任務」步驟另存為草稿並檢索「分配任務」步驟歷史記錄的選項將被禁用。 此外，在「收件匣」中，儲存的選項會停用。

## 轉換為PDF/步驟 {#convert-pdfa}

PDF/A是一種存檔格式，通過嵌入字型和解壓縮檔案來長期保存文檔的內容。 因此，PDF/A 文件通常比標準 PDF 文件大。您可以使用 ***轉換為PDF/A*** 步驟，將PDF檔案轉換為PDF/A格式。

轉換為PDF/A步驟具有下列屬性：

**[!UICONTROL 輸入文檔]**:輸入文檔可以相對於有效負載，具有絕對路徑，可以作為有效負載提供或儲存在文檔資料類型的變數中。

**[!UICONTROL 轉換選項]**:使用此屬性，可指定將PDF文檔轉換為PDF/A文檔的設定。 此標籤下提供的各種選項有：
* **[!UICONTROL 合規性]**:指定輸出PDF/文檔必須符合的標準。 它支援不同的PDF標準，例如PDF/A-1b、PDF/A-2b或PDF/A-3b。
* **[!UICONTROL 結果級別]**:為轉換輸出指定結果級別為PassFail、Summary或Detailed。
* **[!UICONTROL 色域]**:指定預定義的顏色空間為S_RGB、COBATED_FOGRA27、JAPAN_COLOR_COBATED或SWOP，可用於輸出PDF/A檔案。
* **[!UICONTROL 可選內容]**:僅當滿足指定的一組標準時，才允許在輸出PDF/A文檔中顯示特定圖形對象和/或注釋。

**[!UICONTROL 輸出文檔]**:指定儲存輸出檔案的位置。 輸出檔案可儲存在與裝載相關的位置、覆寫裝載（如果裝載是檔案），或儲存在Document資料類型的變數中。


## 傳送電子郵件步驟 {#send-email-step}

使用電子郵件步驟來傳送電子郵件，例如，含有記錄檔、最適化表單連結的電子郵件 <!-- , link of an interactive communication-->，或附加PDF檔案。 傳送電子郵件步驟支援 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email). HTML電子郵件具有回應性，並可適應收件者的電子郵件用戶端和螢幕大小。 您可以使用HTML電子郵件範本來定義電子郵件的外觀、色彩配置和行為。

電子郵件步驟使用Day CQ Mail Service來傳送電子郵件。 使用電子郵件步驟之前，請確定已設定電子郵件服務。 依預設，電子郵件僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email) 啟用用於發送電子郵件的埠，並為您的環境啟用SMTP協定。 限制有助於提高平台的安全性。

電子郵件步驟具有下列屬性：

**[!UICONTROL 標題]**:步驟的標題有助於識別工作流程編輯器中的步驟。

**[!UICONTROL 說明]**:當您在共用開發環境中工作時，說明對其他程式開發人員很實用。

**[!UICONTROL 電子郵件主旨]**:主題可以從工作流元資料中擷取、手動指定，或從儲存在變數中的值擷取。 從下列選項中選取：

* **[!UICONTROL 常值]** 手動指定主旨。
* **[!UICONTROL 從工作流程中繼資料擷取]**  — 從元資料屬性中檢索主題。
* **[!UICONTROL 變數]**  — 從字串資料類型變數中儲存的值擷取主旨。

**[!UICONTROL HTML電子郵件範本]**:電子郵件的HTML範本。 您可以在電子郵件範本中指定變數。 電子郵件步驟會擷取並顯示輸入項目範本中包含的所有變數。

**[!UICONTROL 電子郵件範本中繼資料]**:電子郵件範本變數的值可以是使用者指定的值、作者或發佈伺服器上資產的路徑、影像，或工作流程中繼資料屬性。

* **[!UICONTROL 常值]**:當您知道要指定的確切值時，請使用選項。 例如， [example@example.com](mailto:example@example.com).

* **[!UICONTROL 工作流程中繼資料]**:要使用的值儲存至工作流程中繼資料屬性時，請使用選項。 選取選項後，在「工作流元資料」選項下方的空白文字方塊中輸入中繼資料屬性名稱。 例如， emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 影像]**:使用選項將影像內嵌至電子郵件。 選取選項後，瀏覽並選擇影像。 影像選項僅適用於電子郵件範本中可用的影像標籤(&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>)。&#42;

**[!UICONTROL 發件人/收件人的電子郵件地址]**:選取 **[!UICONTROL 常值]** 手動指定電子郵件地址或選取 **[!UICONTROL 從工作流程中繼資料擷取]** 從中繼資料屬性擷取電子郵件地址的選項。 您也可以為 **[!UICONTROL 從工作流程中繼資料擷取]** 選項。 選取 **[!UICONTROL 變數]** 選項，從字串資料類型變數中儲存的值擷取電子郵件地址。

* **[!UICONTROL 檔案附件]**:指定位置的可用資產會附加至電子郵件。 資產的路徑可以是相對於裝載或絕對路徑。 範例路徑為 [裝載目錄]/attachments/。

選取 **[!UICONTROL 變數]** 選項，用於檢索儲存在文檔、XML或JSON資料類型變數中的檔案附件。

**[!UICONTROL 檔案名]**:電子郵件附件檔案的名稱。 「電子郵件步驟」將附件的原始檔案名更改為指定的檔案名。 可以手動指定名稱，或從工作流程中繼資料屬性或變數中擷取名稱。 使用 **[!UICONTROL 常值]** 選項。 使用 **[!UICONTROL 變數]** 選項，從字串資料類型變數中儲存的值擷取檔案名稱。 使用 **[!UICONTROL 從工作流程中繼資料擷取]** 選項。

## 生成記錄文檔步驟 {#generate-document-of-record-step}

填寫或提交表單時，您可以以打印或文檔格式保存表單記錄。 此記錄稱為記錄檔案(DoR)。 您可以使用「產生記錄檔案」步驟來建立最適化表單的唯讀或互動式PDF版本。 PDF版本包含填入表單的資訊以及最適化表單的版面。

「記錄文檔」步驟具有以下屬性：

**[!UICONTROL 使用最適化表單]**:指定尋找輸入「最適化表單」的方法。 您可以使用提交至工作流程的適用性表單、絕對路徑可用，或變數中的路徑可用。 您可以使用字串資料類型的變數來指定 **[!UICONTROL 選取要解析的變數]** 欄位。\
您可以將多個適用性Forms與工作流程建立關聯。 因此，您可以使用可用的輸入方法在執行階段中指定適用性表單。

**[!UICONTROL 最適化表單路徑]**:指定最適化表單的路徑。 選取 **[!UICONTROL 在絕對路徑中可用]** 選項 **[!UICONTROL 使用最適化表單]** 欄位。

**[!UICONTROL 使用選擇輸入資料]**:最適化表單的輸入資料路徑。 您可以將資料保留在與裝載相對的位置，指定資料的絕對路徑，或擷取儲存在檔案、JSON或XML資料類型變數中的資料。 輸入資料與最適化表單合併，以建立記錄檔案。

**[!UICONTROL 使用選擇輸入附件路徑]**:附件的路徑。 這些附件包含在記錄文檔中。 您可以將附件保留在相對於裝載的位置，指定附件的絕對路徑，或檢索儲存在Document資料類型陣列變數中的附件。

如果指定資料夾的路徑（例如附件），則資料夾中直接可用的所有檔案都將附加到記錄文檔。 如果在指定附件路徑中直接可用的資料夾中有任何檔案可用，則檔案將作為附件包含在記錄文檔中。 如果直接可用的資料夾中有任何資料夾，則會跳過這些資料夾。

**[!UICONTROL 使用以下選項保存生成的記錄文檔]**:指定保留記錄檔的位置。 您可以選擇覆蓋有效負載資料夾、將記錄文檔放置在有效負載目錄內的某個位置，或將記錄文檔儲存在文檔資料類型的變數中。

**[!UICONTROL 地區]**:指定記錄檔的語言。 選擇 **[!UICONTROL 常值]** 從下拉清單中選擇區域設定或選擇 **[!UICONTROL 變數]** 從字串資料類型變數中儲存的值檢索區域設定。 在變數中儲存地區設定值時定義地區設定代碼。 例如，指定 **en_US** 英文和 **fr_FR** 法語。

## 調用DDX步驟 {#invokeddx}

文檔描述XML(DDX)是一種聲明性標注語言，其元素表示文檔的構成塊。 這些建置區塊包括PDF和XDP檔案，以及其他元素，例如註解、書籤和已設定樣式的文字。 DDX定義一組操作，該操作可以應用於一個或多個輸入文檔以生成一個或多個輸出文檔。 單個DDX可與一系列源文檔一起使用。 您可以使用 ***調用DDX步驟*** 在AEM工作流程中執行各種作業，例如組裝分解檔案、建立和修改Acrobat和XFA Forms，以及 [DDX參考檔案](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

調用DDX步驟具有以下屬性：

**[!UICONTROL 輸入文檔]**:用於設定輸入文檔的屬性。 此標籤下提供的各種選項有：
* **[!UICONTROL 使用指定DDX]**:指定相對於有效負載的輸入文檔、具有絕對路徑、可以作為有效負載提供，或儲存在Document資料類型的變數中。
* **[!UICONTROL 從裝載建立地圖]**:將裝載資料夾下的所有文檔添加到「輸入文檔的映射」中，以便調用組合器中的API。 每個文檔的節點名稱用作映射中的鍵。
* **[!UICONTROL 輸入文檔的映射]**:選項用於使用 **[!UICONTROL 新增]** 按鈕。 每個條目表示映射中文檔的鍵和文檔的源。

**[!UICONTROL 環境選項]**:此選項可用來設定叫用API的處理設定。 此標籤下提供的各種選項有：
* **[!UICONTROL 僅驗證]**:檢查輸入DDX文檔的有效性。
* **[!UICONTROL 錯誤時失敗]**:指示調用API服務是否失敗（如果有錯誤）的布爾值。 預設情況下，其值設為False。
* **[!UICONTROL 第一個Bates數]**:指定自增加的數字。 此自增數字會自動顯示在每個連續頁面上。
* **[!UICONTROL 預設樣式]**:設定輸出檔案的預設樣式。

>[!NOTE]
>
>環境選項與HTTP API保持同步。

**[!UICONTROL 輸出文檔]**:指定儲存輸出檔案的位置。 此標籤下提供的各種選項有：
* **[!UICONTROL 在裝載中儲存輸出]**:將輸出檔案儲存在裝載資料夾下，或覆寫裝載（若有效負載是檔案）。
* **[!UICONTROL 輸出文檔的映射]**:通過為每個文檔添加一個條目，指定顯式保存每個文檔檔案的位置。 每個條目表示文檔和保存文檔的位置。 如果有多個輸出文檔，則使用此選項。

## 調用表單資料模型服務步驟 {#invoke-form-data-model-service-step}

您可以使用 [[!DNL AEM Forms] 資料整合](data-integration.md) 配置和連接到不同的資料源。 這些資料源可以是Web服務、REST服務、OData服務和CRM解決方案。 [!DNL AEM Forms] 資料整合允許您建立包含各種服務的表單資料模型，以對配置的資料庫執行資料檢索、添加和更新操作。 您可以使用 **[!UICONTROL 調用資料模型服務步驟]** 要選擇表單資料模型(FDM)，並使用FDM的服務來檢索、更新或將資料添加到不同的資料源。

為了說明步驟欄位的輸入，以下資料庫表格和JSON檔案為範例：

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

**[!UICONTROL 範例JSON檔案]**

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

「調用表單資料模型服務」步驟具有下列欄位，以便執行表單資料模型操作：

* **[!UICONTROL 標題]**:步驟的標題。 它有助於識別工作流程編輯器中的步驟。
* **[!UICONTROL 說明]**:當您在共用開發環境中工作時，此說明對其他程式開發人員很實用。

* **[!UICONTROL 表單資料模型路徑]**:瀏覽並選取伺服器上存在的表單資料模型。

* **[!UICONTROL 錯誤和驗證]**:選項可讓您擷取錯誤訊息，並指定擷取並傳送至資料來源之資料的驗證選項。 透過這些變更，您可以確保傳遞至「叫用表單資料模型服務」步驟的資料符合資料來源所定義的資料限制。 如需詳細資訊，請參閱 [輸入資料的自動驗證](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 驗證層級]**:驗證分為三類：基本、完全和關閉：

   * 完整：所有約束均經過驗證。
   * 基本：僅必需和可為空的約束
   * 關閉：未進行驗證。

* **[!UICONTROL 失敗時終止工作流]**:當限制無法驗證時，工作流程會停止。

* **[!UICONTROL 將錯誤代碼儲存在變數中]**:您可以將錯誤碼儲存在 [字串類型變數](variable-in-aem-workflows.md).

* **[!UICONTROL 將錯誤訊息儲存在變數中]**:您可以將錯誤訊息儲存在 [字串類型變數](variable-in-aem-workflows.md).

* **[!UICONTROL 在變數中儲存錯誤詳細資訊]**:您可以將錯誤詳細資料儲存在 [JSON類型變數](variable-in-aem-workflows.md).

* **[!UICONTROL 服務]**:所選表單資料模型提供的服務清單。
* **[!UICONTROL 服務輸入]** > **[!UICONTROL 使用常值、變數或工作流程中繼資料和JSON檔案提供輸入資料]**:服務可以有多個引數。 選取選項，以從工作流程中繼資料屬性、JSON物件、變數或直接在提供的文字方塊中輸入值來取得服務引數的值：

   * **[!UICONTROL 常值]**:當您知道要指定的確切值時，請使用選項。 例如， srose@we.info。
   * **[!UICONTROL 變數]**:使用選項來擷取儲存在變數中的值。
   * **[!UICONTROL 從工作流元資料中擷取]**:要使用的值儲存至工作流程中繼資料屬性時，請使用選項。 例如， emailAddress。

   * **[!UICONTROL 相對於裝載]**:使用選項可檢索儲存在相對於有效負載的路徑上的檔案附件。 選擇選項並指定包含檔案附件的資料夾名稱，或在文本框中指定檔案附件名稱。

      例如，如果CRX存放庫中的相對裝載資料夾包含位於 `attachment\attachment-folder` 位置，指定 `attachment\attachment-folder` 在 **[!UICONTROL 相對於裝載]** 選項。

   * **[!UICONTROL JSON點記號]**:當要使用的值位於JSON檔案中時，請使用選項。 例如， insurance.customerDetails.emailAddress。 只有選取了輸入JSON選項的「對應」輸入欄位時，「JSON點記號」選項才可用。
   * **[!UICONTROL 從輸入JSON對應輸入欄位]**:指定JSON檔案的路徑，以從JSON檔案取得某些服務引數的輸入值。 JSON檔案的路徑可以是相對於裝載、絕對路徑，或者您可以使用JSON或表單資料模型類型的變數來選取輸入JSON檔案。

* **[!UICONTROL 服務輸入]** > **[!UICONTROL 使用變數或JSON檔案提供輸入資料]**:選取選項，從儲存在絕對路徑、相對於裝載的路徑或變數中的JSON檔案取得所有引數的值。
* **[!UICONTROL 使用選擇輸入JSON文檔]**:包含所有服務引數值的JSON檔案。 JSON檔案的路徑可以是 **[!UICONTROL 相對於有效負載]** 或 **[!UICONTROL 絕對路徑]**. 您也可以使用JSON或表單資料模型資料類型的變數來擷取輸入JSON檔案。

* **[!UICONTROL JSON點記號]**:將欄位留空，以使用指定JSON檔案的所有物件作為服務引數的輸入。 若要從指定的JSON檔案讀取特定JSON物件，作為服務引數的輸入，請為JSON物件指定點記號，例如，如果您的JSON類似於區段開頭列出的JSON，請指定insurance.customerDetails ，以提供客戶的所有詳細資料作為服務的輸入。
* **[!UICONTROL 服務輸出]** > **[!UICONTROL 將輸出值映射並寫入變數或中繼資料]**:選取選項，將輸出值儲存為crx-repository中工作流程例項中繼資料節點的屬性。 指定元資料屬性的名稱，並選擇要與元資料屬性映射的相應服務輸出屬性，例如，將輸出服務返回的phone_number與工作流元資料的phone_number屬性映射。 同樣地，您也可以將輸出儲存在Long資料類型的變數中。 當您為 **[!UICONTROL 要映射的服務輸出屬性]** 選項，則僅會為 **[!UICONTROL 將輸出儲存至]** 選項。

* **[!UICONTROL 服務輸出]** > **[!UICONTROL 將輸出儲存至變數或JSON檔案]**:選取選項，將輸出值儲存在JSON檔案的絕對路徑、相對於裝載的路徑或變數中。
* **[!UICONTROL 使用下列選項儲存輸出JSON檔案]**:儲存輸出JSON檔案。 輸出JSON檔案的路徑可以是相對於裝載或絕對路徑。 您也可以使用JSON或表單資料模型資料類型的變數來儲存輸出JSON檔案。

## 簽署檔案步驟 {#sign-document-step}

「簽署檔案」步驟可讓您使用 [!DNL Adobe Sign] 來簽署文檔。 當您使用 [!DNL Adobe Sign] 工作流程步驟在最適化表單上簽名時，視工作流程設定步驟而定，此表單可以在簽名者之間逐一傳遞，或同時傳送給所有簽名者。啟用 [!DNL Adobe Sign] 的最適化表單只會在所有簽名者完成簽名程序後提交給 Experience Manager Forms 伺服器。

[!DNL Adobe Sign] 排程器服務預設為每 24 小時檢查 (輪詢) 簽名者回應。您可以 [變更環境的預設間隔](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

「簽署文檔」步驟具有以下屬性：

* **[!UICONTROL 協定名稱]**:指定協定的標題。 合約名稱會成為傳送給簽署者之電子郵件的主旨與內文的一部分。 您可以將名稱儲存在字串資料類型的變數中，或選取 **[!UICONTROL 常值]** 手動新增名稱。

* **[!UICONTROL 地區]**:指定電子郵件和驗證選項的語言。 您可以將地區設定儲存在字串資料類型的變數中，或選取 **[!UICONTROL 常值]** 從可用選項清單中選擇區域設定。 在變數中儲存地區設定值時，必須定義地區設定代碼。 例如，指定 **[!UICONTROL en_US]** 英文和 **[!UICONTROL fr_FR]** 法語。

* **[!UICONTROL Adobe Sign雲端設定]**:選擇 [!DNL Adobe Sign] 雲端設定。 如果您尚未設定 [!DNL Adobe Sign] for [!DNL AEM Forms]，請參閱 [將Adobe Sign與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL 選擇要使用簽名的文檔]**:您可以從相對於有效負載的位置選擇文檔、使用有效負載作為文檔、指定文檔的絕對路徑，或檢索儲存在「文檔」資料類型變數中的文檔。
* **[!UICONTROL 截止天數]**:在指定的天數內，任務上沒有任何活動，則會將檔案標示為到期（超過截止日期） **[!UICONTROL 截止天數]** 欄位。 將記錄的內容指派給使用者進行簽署後，會計算的天數。
* **[!UICONTROL 提醒電子郵件頻率]**:您可以每日或每週間隔發送提醒電子郵件。 該周從將記錄的日期指派給使用者進行簽署之日算起。
* **[!UICONTROL 簽名過程]**:您可以選擇按順序或並行順序對文檔進行簽名。 按順序，一個簽名者一次接收文檔以進行簽名。 第一個簽名者完成對文檔的簽名後，將文檔發送給第二個簽名者，以此類推。 同時，多個簽署者一次可以簽署檔案。
* **[!UICONTROL 重新導向URL]**:指定重定向URL。 簽署檔案後，您可以將受託人重新導向至URL。 此URL通常包含感謝訊息或進一步指示。
* **[!UICONTROL 工作流程階段]**:工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型的屬性中定義這些階段( **[!UICONTROL Sidekick]** > **[!UICONTROL 頁面]** > **[!UICONTROL 頁面屬性]** > **[!UICONTROL 階段]**)。
* **[!UICONTROL 選擇簽署者]**:指定為文檔選擇簽署者的方法。 您可以動態地將工作流程指派給使用者或群組，或手動新增簽署者的詳細資訊。
* **[!UICONTROL 指令碼或服務以選擇簽署者]**:只有在「選取簽署者」欄位中選取「動態」選項時，選項才可用。 您可以指定ECMAScript或服務來為文檔選擇簽名器和驗證選項。
* **[!UICONTROL 簽署者詳細資訊]**:僅當在「選擇簽名者」欄位中選擇了「手動」選項時，該選項才可用。 指定電子郵件地址並選擇可選的驗證機制。 在選擇兩步驗證機制之前，請確保為已配置的 [!DNL Adobe Sign] 帳戶。 您可以使用字串資料類型的變數來定義電子郵件、國家/地區代碼和電話號碼欄位的值。 只有在從2步驗證下拉式清單中選取「電話驗證」時，才會顯示「國家/地區代碼」和「電話號碼」欄位。

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
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## 生成打印輸出步驟 {#generatePrintedOutput}

該步驟將生成PCL、PostScript、ZPL、IPL、TPCL或DPL輸出，並提供表單設計和資料檔案。 資料檔案與表單設計合併，並格式化以便打印。 通過此步驟生成的輸出可以直接發送到打印機或另存為檔案。 當您想要使用來自應用程式的表單設計或資料時，建議您使用此步驟。 如果您的表單設計位於網路、本地檔案系統或HTTP位置，請使用generatePrintedOutput操作。

例如，您的應用程式要求您將表單設計與資料檔案合併。 資料包含數百筆記錄。 此外，它要求將輸出發送到支援ZPL的打印機。 表單設計和輸入資料位於應用程式中。 使用generatePrintedOutput操作將每個記錄與表單設計合併，並將輸出發送到支援ZPL的打印機。

「生成打印輸出」步驟具有以下屬性：

**[!UICONTROL 輸入屬性]**

* **[!UICONTROL 使用]**:指定範本檔案的路徑。 您可以使用相對於裝載的路徑、以絕對路徑保存的路徑或使用文檔資料類型的變數來選擇模板檔案。 例如， [裝載目錄]/Workflow/data.xml。 如果crx-repository中不存在路徑，管理員可以先建立路徑再使用。 此外，您也可以接受裝載作為輸入資料檔案。

* **[!UICONTROL 使用]**:指定輸入資料檔案的路徑。 您可以使用相對於有效負載的路徑、保存在絕對路徑上的路徑，或使用文檔資料類型的變數來選擇輸入資料檔案。 例如， [裝載目錄]/Workflow/data.xml。 如果crx-repository中不存在路徑，管理員可以先建立路徑再使用。

* **[!UICONTROL 打印機格式]**:「打印格式」值，指定在未提供XDC檔案時用於生成輸出流的頁面描述語言。 如果您提供常值，請選取以下其中一個值：

   * **[!UICONTROL 顏色PCL]**:使用選項為PCL指定XDC檔案。
   * **[!UICONTROL 一般PostScript]**:使用選項為PostScript指定一般XDC檔案。
   * **[!UICONTROL 300 DPI]**:使用300 DPI。 已使用zpl300.xdc。
   * **[!UICONTROL ZPL 600 DPI]**:使用600 DPI。 使用zpl600.xdc檔案。
   * **[!UICONTROL IPL 300 DPI]**:使用IPL 300 DPI。 已使用ipl300.xdc。
   * **[!UICONTROL IPL 400 DPI]**:使用IPL 400 DPI。 使用ipl400.xdc檔案。
   * **[!UICONTROL TPCL 600 DPI]**:使用TPCL 600 DPI。 使用tpcl600.xdc檔案。
   * **[!UICONTROL PostScript Plain]**:使用選項為PostScript指定純文字檔案XDC檔案。
   * **[!UICONTROL DPL300DPI]**:使用DPL 300 DPI。 已使用dpl300.xdc。
   * **[!UICONTROL DPL400DPI]**:使用DPL 400 DPI。 已使用dpl400.xdc。
   * **[!UICONTROL DPL600DPI]**:使用DPL 600 DPI。 已使用dpl600.xdc。
   * **[!UICONTROL HP_PCL_5e]**:使用選項支援多個Canon裝置。


**[!UICONTROL 輸出屬性]**

* **[!UICONTROL 使用保存輸出文檔]**:指定儲存輸出檔案的位置。 您可以將輸出檔案儲存在與裝載相對的位置、變數中，或指定儲存輸出檔案的絕對位置。 如果crx-repository中不存在路徑，管理員可以先建立路徑再使用。

**[!UICONTROL 進階屬性]**

* **[!UICONTROL 使用]**:內容根是字串值，它指定URI、絕對參照或儲存庫中的位置，以檢索表單設計使用的相對資產。 例如，如果表單設計相對參照影像，例如 `../myImage.gif`, `myImage.gif` 必須為 `repository://`. 預設值為 `repository://`，指向存放庫的根層級。

   當您從應用程式中挑選資產時，內容根URI路徑必須具有正確的結構。 例如，如果從名為SampleApp的應用程式中挑選表單，並放置在 `SampleApp/1.0/forms/Test.xdp`，內容根URI必須指定為 `repository://administrator@password/Applications/SampleApp/1.0/forms/`，或 `repository:/Applications/SampleApp/1.0/forms/` （當權限為空時）。 以此方式指定「內容根URI」時，表單中所有參考資產的路徑將會針對此URI進行解析。

* **[!UICONTROL 使用]**:XCI檔案用於描述用於表單設計元素的字型和其他屬性。 您可以保留相對於裝載、絕對路徑或使用Document資料類型變數的XCI檔案。

* **[!UICONTROL 地區]**:指定用於生成PDF文檔的語言。 如果您提供常值，請從清單中選取語言，或選取以下任一值：
   * **[!UICONTROL 使用伺服器預設值]**:（預設）使用 [!DNL AEM Forms] 伺服器。 使用管理控制台配置了「區域設定」。 (請參閱 [設計工具說明](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL 使用自訂值]**:在文字框中鍵入地區代碼，或選擇包含地區代碼的字串變數。 有關支援的區域設定代碼的完整清單，請參見https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html。

* **[!UICONTROL 復本]**:一個整數值，它指定要為輸出生成的副本數。 預設值為 1。

* **[!UICONTROL 雙面打印]**:指定是使用雙面打印還是單面打印的分頁值。 支援PostScript和PCL的打印機使用此值。 如果您提供常值，請選取以下其中一個值：
   * **[!UICONTROL 雙工長邊]**:使用長邊分頁，進行雙面打印和打印。
   * **[!UICONTROL 雙工短邊]**:使用短邊分頁進行雙面打印和打印。
   * **[!UICONTROL 單純形]**:使用單面打印。

## 生成非互動式PDF輸出步驟   {#generatePDFdocuments}

1. 將「產生非互動式PDF輸出」工作流程拖曳至Sidekick的「Forms Workflow」標籤下。
1. 按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、輸出文檔和其他參數，然後按一下 **[!UICONTROL 確定]**.

### 輸入文檔 {#input-documents-3}

* **範本檔案**:指定XDP範本的位置。 這是必填欄位。

* **資料檔案**:指定需要與模板合併的資料xml的位置。

### 輸出文檔 {#output-document}

**輸出文檔**:指定生成的PDF表單的名稱。

### 其他參數 {#additional-parameters-1}

* **內容根**:指定儲存庫中資料夾的路徑，儲存輸入XDP範本中使用的片段或影像。
* **地區**:指定生成的PDF表單的預設區域。
* **Acrobat版本**:指定所產生Acrobat表單的目標PDF版本。
* **線性化PDF**:指定是否要最佳化為Web檢視產生的PDF。
* **標籤PDF**:指定是否讓產生的PDF可供存取。
* **XCI檔案**:指定XCI檔案的路徑。
