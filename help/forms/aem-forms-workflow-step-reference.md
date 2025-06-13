---
title: 在AEM Forms Cloud Service上，哪些工作流程步驟可用來建立工作流程或用於業務流程自動化(BPM)？
description: 以Forms為中心的工作流程可讓您快速建立最適化Forms型工作流程。 您可以使用Adobe Sign對檔案進行電子簽章、建立表單式業務流程、擷取資料並傳送至多個資料來源，以及傳送電子郵件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: 使用AEM工作流程、使用指派工作步驟、轉換至PDF/A步驟、產生記錄步驟的檔案、使用工作流程、簽署檔案步驟、產生列印輸出步驟、產生非互動式PDF輸出
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '7370'
ht-degree: 0%

---


# 使用以Forms為中心的AEM工作流程 — 步驟參考來自動化業務流程 {#forms-centric-workflow-on-osgi-step-reference}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html) |
| AEM as a Cloud Service  | 本文章 |

您使用工作流程模型。 模型可協助您定義並執行一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。 您可以[在模型中加入各種AEM工作流程步驟，以達成商業邏輯](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)。

## 以Forms為中心的步驟 {#forms-workflow-steps}

以Forms為中心的工作流程步驟，會在AEM工作流程中執行AEM Forms特定的操作。 這些步驟可讓您在OSGi上快速建立最適化Forms型Forms工作流程。 這些工作流程可用於開發基本的稽核和核准工作流程、內部和跨防火牆業務流程。 您也可以使用Forms Workflow步驟來：

* 建立業務流程、提交後工作流程以及後端工作流程，以管理註冊流程。

* 建立並指派工作給使用者或群組。

* 在AEM工作流程中使用[!DNL Adobe Sign]來傳送要簽署的檔案。

* 隨選或提交表單時產生記錄檔案。

* 將工作流程模型與各種資料來源連結，以輕鬆儲存和擷取資料。

* 使用電子郵件步驟，在動作完成和工作流程開始或完成時傳送通知電子郵件和其他附件。

>[!NOTE]
>
>如果為外部儲存體標示了工作流程模型，則對於所有Forms Workflow步驟，您只能選取變數選項來儲存或擷取資料檔案和附件。

## 指派任務步驟 {#assign-task-step}

指派工作步驟會建立工作專案，並將其指派給使用者或群組。 在指派工作的同時，元件也會為此工作指定最適化表單或非互動式PDF 。 若要接受使用者的輸入，且非互動式PDF或唯讀的最適化表單必須使用於僅供檢閱的工作流程，最適化表單為必要項。

您也可以使用元件來控制工作的行為。 例如，建立自動記錄檔案、將工作指派給特定使用者或群組、指定提交資料的路徑、指定要預先填入的資料路徑，以及指定預設動作。 「指派工作」步驟具有以下屬性：

* **[!UICONTROL 標題]**：工作的標題。 標題會顯示在AEM收件匣中。
* **[!UICONTROL 描述]**：說明在工作中執行的作業。 當您在共用開發環境中工作時，此資訊對於其他流程開發人員很有用。

* **[!UICONTROL 縮圖路徑]**：工作縮圖的路徑。 若未指定路徑，最適化表單會顯示預設縮圖，記錄檔案則會顯示預設圖示。
* **[!UICONTROL 工作流程階段]**：工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型屬性(Sidekick >頁面>頁面屬性>階段)中定義這些階段。
* **[!UICONTROL 優先順序]**：選取的優先順序會顯示在AEM收件匣中。 可用的選項為「高」、「Medium」和「低」。 預設值為Medium。
* **[!UICONTROL 到期日]**：指定在多少天或多少小時之後，工作就會標示為逾期。 如果您選取&#x200B;**[!UICONTROL 關閉]**，則不會將工作標示為逾期。 您也可以指定逾時處理常式，以便在工作逾期後執行特定工作。

* **[!UICONTROL 天]**：工作要完成的天數。 將任務指派給使用者後會計入的天數。 如果任務未完成並超過「天數」欄位中指定的天數，則選取該任務時，逾時處理常式會在到期日之後觸發。
* **[!UICONTROL 小時]**：工作要完成之前的小時數。 將任務指派給使用者後會計入小時數。 如果任務未完成並超過時數欄位中指定的時數，則如果選取它，逾時處理常式會在到期時數之後觸發。
* **[!UICONTROL 到期日之後逾時]**：選取此選項以啟用[逾時處理常式]選取欄位。
* **[!UICONTROL 逾時處理常式]**：選取指派工作步驟超過到期日時要執行的指令碼。 放置在CRX儲存庫中[apps]/fd/dashboard/scripts/timeoutHandler的指令碼可供選取。 crx-repository中不存在指定的路徑。 管理員會在使用之前建立路徑。
* **[!UICONTROL 在任務詳細資訊中反白上一個任務的動作和註解]**：選取此選項可顯示上一個在任務詳細資訊區段上採取的動作和收到的註解。
* **[!UICONTROL 型別]**：選擇工作流程啟動時要填寫的檔案型別。 您可以選擇最適化表單、唯讀最適化表單、非互動式PDF檔案。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用最適化表單]**：指定尋找輸入最適化表單的方法。 如果您從「型別」下拉式清單中選取「最適化表單」或「唯讀最適化表單」，即可使用此選項。 您可以使用提交至工作流程的最適化表單、在絕對路徑提供的表單，或在變數中的路徑提供的表單。 您可以使用字串型別的變數來指定路徑。\
  您可以將多個最適化Forms與一個工作流程建立關聯。 因此，您可以使用可用的輸入法，在執行階段指定調適型表單。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 自適應表單路徑]**：指定自適應表單的路徑。 您可以使用提交給工作流程的最適化表單（可在絕對路徑取得），或從儲存在字串資料型別變數中的路徑擷取最適化表單。
* **[!UICONTROL 使用]**&#x200B;選取輸入PDF：指定非互動式PDF檔案的路徑。 當您在「型別」欄位中選擇非互動式PDF檔案時，該欄位可供使用。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取輸入PDF。 例如，[Payload_Directory]/Workflow/PDF/credit-card.pdf。 crx-repository中不存在該路徑。 管理員會在使用之前建立路徑。 您需要啟用記錄檔案選項或表單範本式的最適化Forms ，才能使用PDF路徑選項。
* **[!UICONTROL 針對已完成的工作，將調適型表單轉譯為]**：當工作標示為完成時，您可以將調適型表單轉譯為唯讀的調適型表單或PDF檔案。 您需要啟用記錄檔案選項或表單範本式的最適化Forms，才能將最適化表單呈現為記錄檔案。
* **[!UICONTROL 已預先填入]**：下列欄位可作為工作的輸入專案：

   * **[!UICONTROL 使用]**&#x200B;選取輸入資料檔：輸入資料檔的路徑(.json、.xml、.doc或表單資料模型(FDM))。 您可以使用相對於承載的路徑來擷取輸入資料檔案，或擷取儲存在Document、XML或JSON資料型別變數中的檔案。 例如，檔案包含透過AEM收件匣應用程式為表單提交的資料。 範例路徑為[Payload_Directory]/workflow/data。
   * **[!UICONTROL 使用]**&#x200B;選取輸入附件：位置可用的附件會附加至與工作關聯的表單。 路徑可以是相對於承載或擷取儲存在檔案變數中的附件。 範例路徑為[Payload_Directory]/attachments/。 您可以指定相對於承載放置的附件，或使用檔案型別（「陣列清單」>「檔案」）變數來指定最適化表單的輸入附件。

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 要求屬性對應]**：使用要求屬性對應區段來定義要求屬性[&#128279;](work-with-form-data-model.md#bindargument)的名稱和值。 根據請求中指定的屬性名稱和值從資料來源擷取詳細資料。 您可以使用常值或String資料型別的變數來定義請求屬性值。

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 提交的資訊]**：下列欄位可作為工作的輸出位置：

   * **[!UICONTROL 使用]**&#x200B;儲存輸出資料檔：儲存資料檔(.json、.xml、.doc或表單資料模型(FDM))。 資料檔案包含透過相關表單提交的資訊。 您可以使用相對於承載的路徑來儲存輸出資料檔案，或將其儲存在Document、XML或JSON資料型別的變數中。 例如，[Payload_Directory]/Workflow/data，其中資料是檔案。
   * **[!UICONTROL 使用]**&#x200B;儲存附件：儲存工作所提供的表單附件。 您可以使用相對於承載的路徑來儲存附件，或將其儲存在Document資料型別的陣列清單中。
   * **[!UICONTROL 使用]**&#x200B;儲存記錄檔案：儲存記錄檔案檔案的路徑。 例如，[Payload_Directory]/DocumentofRecord/credit-card.pdf。 您可以使用相對於承載的路徑來儲存記錄檔案，或將其儲存在Document資料型別的變數中。 如果您選取&#x200B;**[!UICONTROL 相對於承載]**&#x200B;選項，如果路徑欄位留空，則不會產生記錄檔案。 只有在從「型別」下拉式清單中選取「最適化表單」時，才能使用此選項。

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 受指派人]** > **[!UICONTROL 指派選項]**：指定將工作指派給使用者的方法。 您可以使用「參與者選擇器」指令碼動態地將任務指派給使用者或群組，或將任務指派給特定的AEM使用者或群組。
* **[!UICONTROL 參與者選擇器]**：在[指派選項]欄位中選取&#x200B;**[!UICONTROL 動態至使用者或群組]**&#x200B;選項時，即可使用此選項。 您可以使用ECMAScript或服務來動態選取使用者或群組。 如需詳細資訊，請參閱[建立自訂Adobe Experience Manager動態參與者步驟](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&CID=RedirectAEMCommunityKautuk)。

* **[!UICONTROL 參與者]**：在&#x200B;**[!UICONTROL 參與者選擇器]**&#x200B;欄位中選取&#x200B;**[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]**&#x200B;選項時，即可使用此欄位。 欄位可讓您為RandomParticipantChooser選項選取使用者或群組。

* **[!UICONTROL 受指派人]**：在&#x200B;**[!UICONTROL 參與者選擇器]**&#x200B;欄位中選取&#x200B;**[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]**&#x200B;時，該欄位可供使用。 欄位可讓您選取字串資料型別的變數以定義受託人。

* **[!UICONTROL 引數]**：在「參與者選擇器」欄位中選取RandomParticipantChoose指令碼以外的指令碼時，該欄位可供使用。 欄位可讓您針對「參與者選擇器」欄位中所選的指令碼，提供以逗號分隔的引數清單。

* **[!UICONTROL 使用者或群組]**：工作已指派給選取的使用者或群組。 在&#x200B;**[!UICONTROL 指派選項]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 至特定使用者或群組選項]**&#x200B;時，即可使用此選項。 欄位會列出[!DNL workflow-users]群組的所有使用者和群組。\
  **[!UICONTROL 使用者或群組]**&#x200B;下拉式功能表會列出登入使用者有權存取的使用者和群組。 使用者名稱顯示取決於您是否具有該特定使用者crx-repository中&#x200B;**[!UICONTROL 使用者]**&#x200B;節點的存取許可權。

* **[!UICONTROL 傳送通知電子郵件]**：選取此選項可將電子郵件通知傳送給受指派人。 這些通知會在任務指派給使用者或群組時傳送。 您可以使用&#x200B;**[!UICONTROL 收件者電子郵件地址]**&#x200B;選項來指定擷取電子郵件地址的機制。

* **[!UICONTROL 收件者電子郵件地址]**：您可以將電子郵件地址儲存在變數中、使用常值來指定永久電子郵件地址，或使用受指派人設定檔中指定的受指派人預設電子郵件地址。 您可以使用常值或變數來指定群組的電子郵件地址。 變數選項有助於動態擷取和使用電子郵件地址。 **[!UICONTROL 使用受指派人的預設電子郵件地址]**&#x200B;選項僅適用於單一受指派人。 在這種情況下，將使用儲存在受指派人使用者設定檔中的電子郵件地址。

* **[!UICONTROL HTML電子郵件範本]**：選取通知電子郵件的電子郵件範本。 若要編輯範本，請在crx-repository中修改位於/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的檔案。
* **[!UICONTROL 允許委派給]**： AEM收件匣為登入的使用者提供將指派的工作流程委派給其他使用者的選項。 您可以委派給相同群組內的工作流程使用者，或委派給其他群組的工作流程使用者。 如果任務指派給單一使用者，並且選取了&#x200B;**[!UICONTROL 允許委派給受指派人群組]**&#x200B;成員選項，則無法將任務委派給其他使用者或群組。
* **[!UICONTROL 共用設定]**： AEM收件匣提供選項，讓其他使用者共用收件匣中的單一或所有工作：
   * 選取&#x200B;**[!UICONTROL 允許受分派者在收件匣]**&#x200B;中明確共用選項時，使用者可以在AEM收件匣中選取工作並與其他AEM使用者共用。
   * 選取&#x200B;**[!UICONTROL 允許受指派人透過收件匣共用來共用]**&#x200B;選項，且使用者共用其收件匣專案或允許其他使用者存取其收件匣專案時，只有先前提及的選項啟用的工作才會與其他使用者共用。
   * 選取&#x200B;**[!UICONTROL 允許受分派者使用「外出」設定]**&#x200B;委派時。 受指派人可以啟用將任務委派給其他使用者的選項，以及其他休假選項。 任何指派給休假使用者的新任務都會自動委派（指派）給休假設定中提到的使用者。

  它可讓其他使用者在外出時選擇受指派人工作，而無法處理受指派任務。

* **[!UICONTROL 動作]** > **[!UICONTROL 預設動作]**：現成可用的送出、儲存和重設動作。 預設會啟用所有預設動作。
* **[!UICONTROL 路由變數]**：路由變數的名稱。 路由變數會擷取使用者在AEM收件匣中選取的自訂動作。
* **[!UICONTROL 路由]**：任務可以分支至不同的路由。 在AEM收件匣中選取時，路由會傳回值，而工作流程會根據選取的路由進行分支。 您可以將路由儲存在String資料型別陣列的變數中，或選取&#x200B;**[!UICONTROL 常值]**&#x200B;以手動新增路由。

* **[!UICONTROL 路由標題]**：指定路由的標題。 它會顯示在AEM收件匣中。
* **[!UICONTROL Coral圖示]**：指定Coral圖示的HTML屬性。 Adobe CorelUI資料庫提供了一組數量龐大的觸控優先圖示。 您可以選擇並使用路由的圖示。 它會與標題一起顯示在AEM收件匣中。 如果您將路由儲存在變數中，路由會使用預設的「標籤」珊瑚圖示。
* **[!UICONTROL 允許受分派者新增註解]**：選取此選項可啟用工作的註解。 受指派人可以於任務提交時，從AEM收件匣新增註解。
* **[!UICONTROL 將註解儲存在變數中]**：將註解儲存在字串資料型別的變數中。 只有在選取&#x200B;**[!UICONTROL 允許受分派者新增註解]**&#x200B;核取方塊時，才會顯示此選項。

* **[!UICONTROL 允許受分派者將附件新增至工作]**：選取此選項以啟用工作的附件。 受指派人可以於提交任務時從AEM收件匣新增附件。 您也可以限制附件的大小上限&#x200B;**[!UICONTROL （檔案大小上限）]**。 預設大小為2 MB。

* **[!UICONTROL 使用]**&#x200B;儲存輸出工作附件：指定附件資料夾的位置。 您可以使用相對於承載的路徑或在檔案資料型別陣列的變數中儲存輸出工作附件。 只有當您選取&#x200B;**[!UICONTROL 允許受分派者將附件新增至工作]**&#x200B;核取方塊，並從&#x200B;**[!UICONTROL 表單/檔案]**&#x200B;索引標籤中的&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 最適化表單]**、**[!UICONTROL 唯讀最適化表單]**&#x200B;或&#x200B;**[!UICONTROL 非互動式PDF檔案]**，才會顯示此選項。

* **[!UICONTROL 使用自訂中繼資料]**：選取此選項可啟用自訂中繼資料欄位。 自訂中繼資料用於電子郵件範本。
* **[!UICONTROL 自訂中繼資料]**：選取電子郵件範本的自訂中繼資料。 自訂中繼資料可在crx-repository的apps/fd/dashboard/scripts/metadataScripts取得。 crx-repository中不存在指定的路徑。 管理員會在使用之前建立路徑。 您也可以使用自訂中繼資料的服務。 您也可以擴充`WorkitemUserMetadataService`介面以提供自訂中繼資料。
* **[!UICONTROL 顯示先前步驟的資料]**：選取此選項可讓受指派人檢視先前的受指派人、已對任務採取的動作、新增至任務的註解，以及已完成任務的記錄檔案（若有）。
* **[!UICONTROL 顯示後續步驟的資料]**：選取此選項可讓目前的受指派人檢視後續受指派人採取的動作及新增至工作的註解。 也可讓目前受分派者檢視已完成工作的記錄檔案（若有）。
* **[!UICONTROL 資料型別的可見性]**：依預設，受指派人可以檢視記錄檔案、受指派人、採取的動作，以及先前和後續受指派人已新增的註解。 使用資料型別可見性選項來限制受指派人可見的資料型別。

>[!NOTE]
>
>當您設定外部資料儲存的AEM工作流程模型時，將指派任務步驟儲存為草稿以及擷取指派任務步驟歷史記錄的選項會停用。 此外，收件匣中的儲存選項已停用。

## 轉換為PDF/A步驟 {#convert-pdfa}

PDF/A是一種用於長期儲存檔案內容的封存格式，其方式為嵌入字型並解壓縮檔案。 因此，PDF/A 文件通常比標準 PDF 文件大。您可以在AEM工作流程中使用&#x200B;***轉換成PDF/A***&#x200B;步驟，將PDF檔案轉換成PDF/A格式。

轉換至PDF/A步驟具有以下屬性：

**[!UICONTROL 輸入檔案]**：輸入檔案可以相對於承載、具有絕對路徑、可以作為承載提供或儲存在Document資料型別的變數中。

**[!UICONTROL 轉換選項]**：使用此屬性，可指定將PDF檔案轉換為PDF/A檔案的設定。 此標籤下可用的各種選項包括：
* **[!UICONTROL 法規遵循]**：指定輸出PDF/A檔案必須符合的標準。 它支援不同的PDF標準，例如PDF/A-1b、PDF/A-2b或PDF/A-3b。
* **[!UICONTROL 結果層級]**：將轉換輸出的結果層級指定為PassFail、Summary或Detailed。
* **[!UICONTROL 色域]**：將預先定義的色域指定為S_RGB、COATED_FOGRA27、JAPAN_COLOR_COATED或SWOP，可用於輸出PDF/A檔案。
* **[!UICONTROL 選擇性內容]**：只有在符合指定的准則集時，才允許在輸出PDF/A檔案中顯示特定圖形物件和/或註解。

**[!UICONTROL 輸出檔案]**：指定儲存輸出檔案的位置。 輸出檔案可儲存在相對於承載的位置、覆寫承載（如果承載是檔案或是Document資料型別的變數）。


## 傳送電子郵件步驟 {#send-email-step}

使用電子郵件步驟來傳送電子郵件，例如，包含記錄檔案、最適化表單<!-- , link of an interactive communication-->連結或附加PDF檔案的電子郵件。 傳送電子郵件步驟支援[HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 HTML電子郵件會迅速回應，並因應收件者的電子郵件使用者端和熒幕大小。 您可以使用HTML電子郵件範本來定義電子郵件的外觀、色彩配置和行為。

電子郵件步驟使用Day CQ Mail Service傳送電子郵件。 在使用電子郵件步驟之前，請確定已設定電子郵件服務。 預設僅支援HTTP和HTTP通訊協定。 [請連絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email)以啟用連線埠來傳送電子郵件，並為您的環境啟用SMTP通訊協定。 此限制有助於改善平台的安全性。

電子郵件步驟有下列屬性：

**[!UICONTROL 標題]**：步驟的標題可協助識別工作流程編輯器中的步驟。

**[!UICONTROL 描述]**：當您在共用開發環境中工作時，說明對於其他程式開發人員很有用。

**[!UICONTROL 電子郵件主旨]**：主旨可從工作流程中繼資料擷取、手動指定，或從儲存在變數中的值擷取。 從下列選項中選取：

* **[!UICONTROL 常值]**&#x200B;手動指定主旨。
* **[!UICONTROL 從工作流程中繼資料擷取]** — 從中繼資料屬性擷取主旨。
* **[!UICONTROL 變數]** — 從儲存在字串資料型別變數中的值擷取主旨。

**[!UICONTROL HTML電子郵件範本]**：電子郵件的HTML範本。 您可以在電子郵件範本中指定變數。 「電子郵件步驟」會擷取並顯示範本中包含的所有變數以供輸入。

**[!UICONTROL 電子郵件範本中繼資料]**：電子郵件範本變數的值可以是使用者指定的值、作者或發佈伺服器上的資產路徑、影像，或工作流程中繼資料屬性。

* **[!UICONTROL 常值]**：當您知道要指定的確切值時，請使用選項。 例如，[example@example.com](mailto:example@example.com)。

* **[!UICONTROL 工作流程中繼資料]**：當要使用的值儲存在工作流程中繼資料屬性中時，請使用選項。 選取選項後，在工作流程中繼資料選項下方的空白文字方塊中輸入中繼資料屬性名稱。 例如，emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 影像]**：使用選項將影像內嵌至電子郵件。 選取選項後，瀏覽並選擇影像。 影像選項僅適用於電子郵件範本中可用的影像標籤(&lt;img src=&quot;&#42;&quot;/>)。

**[!UICONTROL 寄件者/收件者的電子郵件地址]**：選取&#x200B;**[!UICONTROL 常值]**&#x200B;選項，以手動指定電子郵件地址，或選取&#x200B;**[!UICONTROL 從工作流程中繼資料擷取]**&#x200B;選項，以從中繼資料屬性擷取電子郵件地址。 您也可以為&#x200B;**[!UICONTROL 從工作流程中繼資料擷取]**&#x200B;選項指定中繼資料屬性陣列清單。 選取&#x200B;**[!UICONTROL 變數]**&#x200B;選項，以從字串資料型別變數中儲存的值擷取電子郵件地址。

* **[!UICONTROL 檔案附件]**：指定位置可用的資產已附加至電子郵件。 資產的路徑可以是相對於承載或絕對路徑。 範例路徑為[Payload_Directory]/attachments/。

選取&#x200B;**[!UICONTROL 變數]**&#x200B;選項，以擷取儲存在Document、XML或JSON資料型別變數中的檔案附件。

**[!UICONTROL 檔案名稱]**：電子郵件附件檔案的名稱。 「電子郵件步驟」會將附件的原始檔案名稱變更為指定的檔案名稱。 您可以手動指定名稱，或從工作流程中繼資料屬性或變數中擷取名稱。 當您知道要指定的確切值時，請使用&#x200B;**[!UICONTROL 常值]**&#x200B;選項。 使用&#x200B;**[!UICONTROL 變數]**&#x200B;選項，從儲存在字串資料型別變數中的值擷取檔案名稱。 當要使用的值儲存在工作流程中繼資料屬性中時，使用&#x200B;**[!UICONTROL 從工作流程中繼資料擷取]**&#x200B;選項。

## 產生記錄檔案步驟 {#generate-document-of-record-step}

填寫或提交表單時，您可以以列印或檔案格式保留表單記錄。 此記錄稱為記錄檔案(DoR)。 您可以使用「產生記錄檔案」步驟來建立最適化表單的唯讀或互動式PDF版本。 PDF版本包含填寫至表單的資訊以及最適化表單的版面。

記錄檔案步驟具有以下屬性：

**[!UICONTROL 使用最適化表單]**：指定尋找輸入最適化表單的方法。 您可以使用提交至工作流程的最適化表單、在絕對路徑提供的表單，或在變數中的路徑提供的表單。 您可以使用String資料型別的變數，在&#x200B;**[!UICONTROL 選取要解析的變數]**&#x200B;欄位中指定路徑。\
您可以將多個最適化Forms與一個工作流程建立關聯。 因此，您可以使用可用的輸入法，在執行階段指定調適型表單。

**[!UICONTROL 自適應表單路徑]**：指定自適應表單的路徑。 當您從&#x200B;**[!UICONTROL 使用最適化表單]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 在絕對路徑上可用]**&#x200B;選項時，該欄位可供使用。

**[!UICONTROL 選擇輸入資料，使用]**：最適化表單的輸入資料路徑。 您可以將資料保留在相對於承載的位置、指定資料的絕對路徑，或擷取儲存在Document、JSON或XML資料型別變數中的資料。 輸入資料會與最適化表單合併，以建立記錄檔案。

**[!UICONTROL 使用]**&#x200B;選取輸入附件路徑：附件的路徑。 這些附件包含在記錄檔案中。 您可以將附件保持在相對於承載的位置、指定附件的絕對路徑，或擷取儲存在「檔案」資料型別陣列中的附件。

如果您指定資料夾的路徑（例如附件），資料夾中直接可用的所有檔案都會附加至記錄檔案。 如果在指定附件路徑中直接可用的資料夾中有任何檔案可用，則這些檔案會作為附件包含在記錄檔案中。 如果在直接可用的資料夾中有任何資料夾，則會略過這些資料夾。

**[!UICONTROL 使用以下選項儲存產生的記錄檔案]**：指定保留記錄檔案檔案的位置。 您可以選擇覆寫裝載資料夾、將記錄檔案放在裝載目錄內的某個位置，或將記錄檔案儲存在「檔案」資料型別的變數中。

**[!UICONTROL 地區設定]**：指定記錄檔案的語言。 選取&#x200B;**[!UICONTROL 常值]**&#x200B;以從下拉式清單中選取地區設定，或選取&#x200B;**[!UICONTROL 變數]**&#x200B;以從字串資料型別變數中儲存的值擷取地區設定。 在變數中儲存地區設定的值時，定義地區設定代碼。 例如，指定&#x200B;**en_US**&#x200B;代表英文，指定&#x200B;**fr_FR**&#x200B;代表法文。

## 叫用DDX步驟 {#invokeddx}

檔案描述XML (DDX)是一種宣告式標籤語言，其元素代表檔案的建置組塊。 這些建置區塊包括PDF和XDP檔案以及其他元素，例如註解、書籤和樣式化文字。 DDX定義了一組作業，可套用在一或多個輸入檔案上，以產生一或多個輸出檔案。 單一DDX可用於一系列來原始檔。 您可以在AEM工作流程中使用&#x200B;***叫用DDX步驟***&#x200B;來執行各種作業，例如組譯和解譯檔案、建立和修改Acrobat和XFA Forms，以及[DDX參考檔案](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)中說明的其他作業。

叫用DDX步驟具有以下特性：

**[!UICONTROL 輸入檔案]**：用來設定輸入檔案的屬性。 此標籤下可用的各種選項包括：
* **[!UICONTROL 使用]**&#x200B;指定DDX：指定相對於承載的輸入檔案、具有絕對路徑、可作為承載提供，或儲存在Document資料型別的變數中。
* **[!UICONTROL 從承載建立對應]**：將承載資料夾下的所有檔案新增到輸入檔案的對應，以供組合器中的叫用API使用。 每個檔案的節點名稱都會作為對應中的索引鍵。
* **[!UICONTROL 輸入檔案的對應]**：選項是用來使用&#x200B;**[!UICONTROL ADD]**&#x200B;按鈕新增多個專案。 每個專案代表對應中的檔案索引鍵和檔案的來源。

**[!UICONTROL 環境選項]**：此選項是用來設定叫用API的處理設定。 此標籤下可用的各種選項包括：
* **[!UICONTROL 僅驗證]**：檢查輸入DDX檔案的有效性。
* **[!UICONTROL 發生錯誤時失敗]**：布林值，表示如果發生錯誤，叫用API服務是否失敗。 預設情況下，其值會設為False。
* **[!UICONTROL 第一個Bates數字]**：指定自動遞增的數字。 此自動遞增數字會自動顯示在每個連續頁面上。
* **[!UICONTROL 預設樣式]**：設定輸出檔案的預設樣式。

>[!NOTE]
>
>環境選項會與HTTP API保持同步。

**[!UICONTROL 輸出檔案]**：指定儲存輸出檔案的位置。 此標籤下可用的各種選項包括：
* **[!UICONTROL 將輸出儲存在承載中]**：將輸出檔案儲存在承載資料夾下，或覆寫承載，以防承載是檔案。
* **[!UICONTROL 輸出檔案的對映]**：指定每個檔案檔案明確儲存的位置，方法是在每個檔案新增一個專案。 每個專案代表檔案以及儲存檔案的位置。 如果有多個輸出檔案，則使用此選項。

## 啟動表單資料模型(FDM)服務步驟 {#invoke-form-data-model-service-step}

您可以使用[[!DNL AEM Forms] 資料整合](data-integration.md)來設定並連線至不同的資料來源。 這些資料來源可以是Web服務、REST服務、OData服務和CRM解決方案。 [!DNL AEM Forms]資料整合可讓您建立包含各種服務的表單資料模型(FDM)，以在已設定的資料庫上執行資料擷取、新增、更新作業。 您可以使用&#x200B;**[!UICONTROL 啟動資料模型服務步驟]**&#x200B;來選取表單資料模型(FDM)，並使用FDM的服務來擷取、更新或新增資料至不同的資料來源。

為說明步驟欄位的輸入，以下資料庫表格和JSON檔案為範例：

**[!UICONTROL 範例CustomerDetails資料表]**

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>值<br /> </td> 
  </tr> 
  <tr> 
   <td>名字<br /> </td> 
   <td>Sarah<br /> </td> 
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

啟動表單資料模型(FDM)服務步驟包含下列欄位，以利表單資料模型(FDM)作業：

* **[!UICONTROL 標題]**：步驟的標題。 它有助於識別工作流程編輯器中的步驟。
* **[!UICONTROL 描述]**：當您在共用開發環境中工作時，對其他程式開發人員有用的說明。

* **[!UICONTROL 表單資料模型路徑]**：瀏覽並選取伺服器上存在的表單資料模型(FDM)。

* **[!UICONTROL 錯誤與驗證]**：選項可讓您擷取錯誤訊息，並為擷取並傳送至資料來源的資料指定驗證選項。 透過這些變更，您可以確保傳遞至啟動表單資料模型(FDM)服務步驟的資料會遵守資料來源所定義的資料限制。 如需詳細資訊，請參閱[自動驗證輸入資料](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 驗證層級]**：有三種驗證類別： Basic、Full和OFF：

   * 完整：所有限制均已驗證。
   * 基本：僅限必要和空的限制
   * 關閉：不會進行驗證。

* **[!UICONTROL 失敗時終止工作流程]**：當限制驗證失敗時，工作流程會停止。

* **[!UICONTROL 在變數]**&#x200B;中儲存錯誤代碼：您可以在[字串型別變數](variable-in-aem-workflows.md)中儲存錯誤代碼。

* **[!UICONTROL 在變數]**&#x200B;中儲存錯誤訊息：您可以在[字串型別變數](variable-in-aem-workflows.md)中儲存錯誤訊息。

* **[!UICONTROL 在變數]**&#x200B;中儲存錯誤詳細資料：您可以在[JSON型別變數](variable-in-aem-workflows.md)中儲存錯誤詳細資料。

* **[!UICONTROL 服務]**：所選表單資料模型(FDM)提供的服務清單。
* **[!UICONTROL 服務的輸入]** > **[!UICONTROL 使用常值、變數或工作流程中繼資料，以及JSON檔案來提供輸入資料]**：服務可以有多個引數。 選取選項，從工作流程中繼資料屬性、JSON物件、變數取得服務引數的值，或直接在提供的文字方塊中輸入值：

   * **[!UICONTROL 常值]**：當您知道要指定的確切值時，請使用選項。 例如， srose@we.info。
   * **[!UICONTROL 變數]**：使用選項來擷取儲存在變數中的值。
   * **[!UICONTROL 從工作流程中繼資料擷取]**：當要使用的值儲存在工作流程中繼資料屬性中時，請使用選項。 例如，emailAddress。

   * **[!UICONTROL 相對於承載]**：使用選項來擷取儲存在相對於承載路徑中的檔案附件。 選取選項並指定包含檔案附件的資料夾名稱，或在文字方塊中指定檔案附件名稱。

     例如，如果CRX存放庫中的「相對於有效負載」資料夾在`attachment\attachment-folder`位置包含檔案附件，請在選取「**[!UICONTROL 相對於有效負載]**」選項後，在文字方塊中指定`attachment\attachment-folder`。

   * **[!UICONTROL JSON點標籤法]**：當要使用的值位於JSON檔案中時，請使用選項。 例如，insurance.customerDetails.emailAddress。 JSON Dot Notation選項僅在選取「從輸入JSON選項對應輸入欄位」時可用。
   * **[!UICONTROL 從輸入JSON對應輸入欄位]**：指定JSON檔案的路徑，以從JSON檔案取得某些服務引數的輸入值。 JSON檔案的路徑可以是相對於裝載、絕對路徑，也可以使用JSON或表單資料模型(FDM)型別的變數來選取輸入JSON檔案。

* **[!UICONTROL 服務的輸入]** > **[!UICONTROL 使用變數或JSON檔案提供輸入資料]**：選取選項，以從儲存在絕對路徑、相對於承載的路徑或變數中的JSON檔案取得所有引數的值。
* **[!UICONTROL 使用]**&#x200B;選取輸入JSON檔案：包含所有服務引數值的JSON檔案。 JSON檔案的路徑可以是相對於承載&#x200B;**的**&#x200B;或&#x200B;**[!UICONTROL 絕對路徑]**。 您也可以使用JSON或表單資料模型(FDM)資料型別的變數來擷取輸入JSON檔案。

* **[!UICONTROL JSON Dot Notation]**：將欄位保留空白，以使用指定JSON檔案的所有物件作為服務引數的輸入。 若要從指定的JSON檔案讀取特定JSON物件作為服務引數的輸入，請為JSON物件指定點標籤法。例如，如果您有和區段開頭所列出的JSON類似的JSON，請指定insurance.customerDetails以提供客戶的所有詳細資料作為服務的輸入。
* **[!UICONTROL 服務的輸出]** > **[!UICONTROL 對應輸出值並將輸出值寫入變數或中繼資料]**：選取選項，以將輸出值儲存為crx-repository中工作流程執行個體中繼資料節點的屬性。 指定中繼資料屬性的名稱，並選取對應的服務輸出屬性，以與中繼資料屬性對應，例如，將輸出服務傳回的phone_number與工作流程中繼資料的phone_number屬性對應。 同樣地，您可以將輸出儲存在Long資料型別的變數中。 當您選取&#x200B;**[!UICONTROL 要對映的服務輸出屬性]**&#x200B;選項的屬性時，**[!UICONTROL 將輸出儲存至]**&#x200B;選項只會填入能夠儲存所選屬性資料的變數。

* **[!UICONTROL 服務的輸出]** > **[!UICONTROL 將輸出儲存至變數或JSON檔案]**：選取選項，將輸出值儲存在JSON檔案中的絕對路徑、相對於承載的路徑或變數中。
* **[!UICONTROL 使用以下選項儲存輸出JSON檔案]**：儲存輸出JSON檔案。 輸出JSON檔案的路徑可以是相對於承載或絕對路徑。 您也可以使用JSON或表單資料模型(FDM)資料型別的變數來儲存輸出JSON檔案。



## 簽署檔案步驟 {#sign-document-step}

「簽署檔案」步驟可讓您使用[!DNL Adobe Sign]來簽署檔案。 當您使用[!DNL Adobe Sign]工作流程步驟在最適化表單上簽名時，視工作流程步驟的設定而定，此表單可以在收件者之間逐一傳遞，或同時傳送給所有收件者。 啟用[!DNL Adobe Sign]的Adaptive Forms只會在所有收件者完成簽署程式後，才提交至Experience Manager Forms伺服器。

根據預設，[!DNL Adobe Sign]排程器服務每24小時檢查（輪詢）一次收件者回應。 您可以[變更環境的預設間隔](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status)。

「簽署檔案」步驟具有以下屬性：

* **[!UICONTROL 合約名稱]**：指定合約的標題。 合約名稱會成為傳送給簽署者之電子郵件的主旨與內文的一部分。 您可以將名稱儲存在String資料型別的變數中，或選取&#x200B;**[!UICONTROL 常值]**&#x200B;以手動新增名稱。

* **[!UICONTROL 地區設定]**：指定電子郵件和驗證選項的語言。 您可以將地區設定儲存在String資料型別的變數中，或選取&#x200B;**[!UICONTROL 常值]**&#x200B;從可用選項清單中選擇地區設定。 將地區設定的值儲存在變數中時，您必須定義地區設定代碼。 例如，指定&#x200B;**[!UICONTROL en_US]**&#x200B;代表英文，指定&#x200B;**[!UICONTROL fr_FR]**&#x200B;代表法文。

* **[!UICONTROL Adobe Sign雲端設定]**：選擇[!DNL Adobe Sign]雲端設定。 如果您尚未為[!DNL AEM Forms]設定[!DNL Adobe Sign]，請參閱[將Adobe Sign與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)整合。

* **[!UICONTROL 使用]**&#x200B;選取要簽署的檔案：您可以從相對於承載的位置選擇檔案、使用承載作為檔案、指定檔案的絕對路徑，或擷取儲存在Document資料型別變數中的檔案。
* **[!UICONTROL 截止日期前的天數]**：在&#x200B;**[!UICONTROL 截止日期前的天數]**&#x200B;欄位中指定的天數沒有作業之後，檔案會標示為到期（已超過截止日期）。 檔案指派給使用者簽署後，會計入的天數。
* **[!UICONTROL 提醒電子郵件頻率]**：您可以每日或每週傳送提醒電子郵件。 一週是從檔案指派給使用者供簽署之日開始計算。
* **[!UICONTROL 簽章程式]**：您可以選擇以循序或平行順序簽署檔案。 依序由一位簽署者一次收到檔案以供簽署。 第一個簽署者完成檔案的簽署後，檔案會傳送給第二個簽署者，依此類推。 多個簽署者可同時以平行順序簽署檔案。
* **[!UICONTROL 重新導向URL]**：指定重新導向URL。 檔案簽署後，您可以將受指派人重新導向至URL。 此URL通常包含感謝訊息或進一步說明。
* **[!UICONTROL 工作流程階段]**：工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中。 您可以在模型的屬性中定義這些階段(**[!UICONTROL Sidekick]** > **[!UICONTROL 頁面]** > **[!UICONTROL 頁面屬性]** > **[!UICONTROL 階段]**)。
* **[!UICONTROL 選取收件者]**：指定選擇檔案收件者的方法。 您可以動態地將工作流程指派給使用者或群組，或手動新增收件者的詳細資訊。 當您在下拉式清單中選取手動時，您會新增收件者詳細資訊，例如電子郵件、角色和驗證方法。

  >[!NOTE]
  >
  >* 在「角色」區段中，您可以將收件者角色指定為「簽署者」、「核准者」、「接受者」、「已驗證的收件者」、「表單填寫者」及「委派者」。
  >* 如果您在「角色」選項中選取「委派者」，委派者可以將簽署任務指派給其他收件者。
  >* 如果您已設定[!DNL Adobe Sign]的驗證方法，則根據您的設定，您會選取驗證方法，例如以電話為基礎的驗證、以社交身分為基礎的驗證、以知識為基礎的驗證、以政府身分為基礎的驗證。

* **[!UICONTROL 用來選取收件者的指令碼或服務]**：只有當您在[選取收件者]欄位中選取[動態]選項時，才能使用此選項。 您可以指定ECMAScript或服務，以選擇檔案的簽署者和驗證選項。
* **[!UICONTROL 收件者詳細資料]**：只有在[選取收件者]欄位中選取[手動]選項時，才能使用選項。 指定電子郵件地址，並選擇選用的驗證機制。 在選取兩步驟驗證機制之前，請確定已針對設定的[!DNL Adobe Sign]帳戶啟用對應的驗證選項。 您可以使用String資料型別的變數來定義電子郵件、國家/地區代碼和電話號碼欄位的值。 只有當您從兩步驟驗證下拉式清單中選取「電話驗證」時，才會顯示「國家代碼」和「電話號碼」欄位。
* **[!UICONTROL 已簽署檔案]**：您可以將已簽署檔案的狀態儲存至變數。 若要新增電子簽章稽核軌跡，以提高「已簽署檔案」的安全性與合法性，您可以包含「稽核報表」。 您可以使用變數或承載資料夾來儲存已簽署的檔案。

  >[!NOTE]
  >
  > 「稽核報表」會附加至已簽署檔案的最後一頁。

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

## 產生列印輸出步驟 {#generatePrintedOutput}

此步驟會產生PCL、PostScript、ZPL、IPL、TPCL或DPL輸出，並提供表單設計和資料檔案。 資料檔會與表單設計合併，並格式化以供列印。 此步驟產生的輸出可以直接傳送到印表機或另存為檔案。 當您想要使用表單設計或來自應用程式的資料時，建議您使用此步驟。 如果您的表單設計位於網路、本機檔案系統或HTTP位置，請使用generatePrintedOutput操作。

例如，您的應用程式要求您將表單設計與資料檔案合併。 資料包含數百筆記錄。 此外，它要求將輸出傳送到支援ZPL的印表機。 表單設計和您的輸入資料都在應用程式中。 使用generatePrintedOutput作業將每個記錄與表單設計合併，並將輸出傳送到支援ZPL的印表機。

「產生列印輸出」步驟具有以下屬性：

**[!UICONTROL 輸入屬性]**

* **[!UICONTROL 使用]**&#x200B;選取範本檔案：指定範本檔案的路徑。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取範本檔案。 例如，[Payload_Directory]/Workflow/data.xml。 如果crx-repository中不存在路徑，管理員可以在使用之前建立路徑。 此外，您也可以接受裝載作為輸入資料檔案。

* **[!UICONTROL 使用]**&#x200B;選取資料檔案：指定輸入資料檔案的路徑。 您可以使用相對於承載的路徑、以絕對路徑儲存的路徑，或使用Document資料型別的變數來選取輸入資料檔案。 例如，[Payload_Directory]/Workflow/data.xml。 如果crx-repository中不存在路徑，管理員可以在使用之前建立路徑。

* **[!UICONTROL 印表機格式]**：指定未提供XDC檔案時用來產生輸出資料流的頁面描述語言的列印格式值。 如果您提供常值，請選取下列其中一個值：

   * **[!UICONTROL 色彩PCL]**：使用選項為PCL指定XDC檔案。
   * **[!UICONTROL 通用PostScript]**：使用選項為PostScript指定通用XDC檔案。
   * **[!UICONTROL ZPL 300 DPI]**：使用ZPL 300 DPI。 使用zpl300.xdc。
   * **[!UICONTROL ZPL 600 DPI]**：使用ZPL 600 DPI。 使用zpl600.xdc檔案。
   * **[!UICONTROL IPL 300 DPI]**：使用IPL 300 DPI。 使用ipl300.xdc。
   * **[!UICONTROL IPL 400 DPI]**：使用IPL 400 DPI。 使用ipl400.xdc檔案。
   * **[!UICONTROL TPCL 600 DPI]**：使用TPCL 600 DPI。 使用tpcl600.xdc檔案。
   * **[!UICONTROL PostScript Plain]**：使用選項為PostScript指定純文字XDC檔案。
   * **[!UICONTROL DPL300DPI]**：使用DPL 300 DPI。 使用dpl300.xdc。
   * **[!UICONTROL DPL400DPI]**：使用DPL 400 DPI。 使用dpl400.xdc。
   * **[!UICONTROL DPL600DPI]**：使用DPL 600 DPI。 使用dpl600.xdc。
   * **[!UICONTROL HP_PCL_5e]**：使用選項支援多個Canon裝置。


**[!UICONTROL 輸出屬性]**

* **[!UICONTROL 使用]**&#x200B;儲存輸出檔案：指定儲存輸出檔案的位置。 您可以將輸出檔案儲存在相對於承載的位置、變數中，或指定絕對位置來儲存輸出檔案。 如果crx-repository中不存在路徑，管理員可以在使用之前建立路徑。

**[!UICONTROL 進階屬性]**

* **[!UICONTROL 使用]**&#x200B;選取內容根目錄位置：內容根目錄是字串值，會指定URI、絕對參照或存放庫中的位置，以擷取表單設計所使用的相對資產。 例如，如果表單設計相對參考影像（例如`../myImage.gif`），`myImage.gif`必須位於`repository://`。 預設值為`repository://`，指向存放庫的根層級。

  當您從應用程式中挑選資產時，內容根URI路徑必須具有正確結構。 例如，如果從名為SampleApp的應用程式中挑選表單，並將表單置於`SampleApp/1.0/forms/Test.xdp`，則內容根URI必須指定為`repository://administrator@password/Applications/SampleApp/1.0/forms/`或`repository:/Applications/SampleApp/1.0/forms/` （當授權為null時）。 以這種方式指定內容根URI時，表單中所有參考資產的路徑都會針對此URI解析。

* **[!UICONTROL 使用]**&#x200B;選取XCI檔案： XCI檔案用於描述用於表單設計元素的字型和其他屬性。 您可以相對於承載將XCI檔案保留在絕對路徑上，或使用Document資料型別的變數。

* **[!UICONTROL 地區設定]**：指定用來產生PDF檔案的語言。 如果您提供常值，請從清單中選取語言或選取下列其中一個值：
   * **[!UICONTROL 要使用伺服器預設值]**：
（預設）使用[!DNL AEM Forms]伺服器上設定的地區設定。 地區設定是使用Administration Console來設定。 (請參閱[Designer說明](https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)。)

   * **[!UICONTROL 若要使用自訂值]**：
在常值方塊中輸入地區設定代碼，或選取包含地區設定代碼的字串變數。 如需支援地區設定代碼的完整清單，請參閱https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html。

* **[!UICONTROL 副本]**：指定輸出產生之副本數目的整數值。 預設值為 1。

* **[!UICONTROL 雙面列印]**：指定使用雙面或單面列印的「分頁」值。 支援PostScript和PCL的印表機使用此值。 如果您提供常值，請選取下列其中一個值：
   * **[!UICONTROL 雙面長Edge]**：使用雙面列印，並使用長邊分頁列印。
   * **[!UICONTROL 雙面短Edge]**：使用雙面列印，並使用短邊分頁列印。
   * **[!UICONTROL 單面]**：使用單面列印。

## 產生非互動式PDF輸出步驟   {#generatePDFdocuments}

1. 拖曳Sidekick中「PDF」標籤下的「產生非互動式Forms Workflow輸出」工作流程。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在[編輯元件]對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下[確定]。**&#x200B;**

### 輸入檔案 {#input-documents-3}

* **範本檔案**：指定XDP範本的位置。 這是必填欄位。

* **資料檔案**：指定必須與範本合併的資料xml的位置。

### 輸出檔案 {#output-document}

**輸出檔案**：指定產生的PDF表單的名稱。

### 其他引數 {#additional-parameters-1}

* **內容根**：指定儲存於輸入XDP範本中所用片段或影像之存放庫中的資料夾路徑。
* **地區**：指定產生的PDF表單的預設地區。
* **Acrobat版本**：指定所產生PDF表單的目標Acrobat版本。
* **線性化PDF**：指定是否要最佳化產生的PDF以供網頁檢視。
* **已標籤的PDF**：指定是否要存取產生的PDF。
* **XCI檔案**：指定XCI檔案的路徑。

## 另請參閱 {#see-also}

* [Forms中心AEM工作流程中的變數](/help/forms/variable-in-aem-workflows.md)
* [設定「外出」設定](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->