---
title: 基於OSGi的以Forms為中心的工作流
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用 [!DNL AEM Forms] 自動並快速構建審核和批准、啟動文檔服務的工作流
seo-description: Use [!DNL AEM Forms] Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 1%

---


# 基於OSGi的以Forms為中心的工作流{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企業從成百上千個表單、各種後端系統以及線上或離線資料源中收集資料。 他們還擁有一組動態的用戶來對資料做出決策，這涉及到反複的審核和批准過程。

除了針對內部和外部受眾的審核和批准工作流外，大型組織和企業還具有重複性任務。 例如，將PDF文檔轉換為其他格式。 手動完成這些任務時，需要耗費大量時間和資源。 企業還有法律要求對文檔和存檔表單資料進行數字簽名，以便以後以預定義格式使用。

## OSGi中以Forms為中心的工作流簡介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使AEM用工作流快速構建基於Forms的自適應工作流。 這些工作流可用於審查和批准、業務流程流、啟動文檔服務、與Adobe Sign簽名工作流整合以及類似操作。 例如，信用卡申請處理、員工離職審批工作流、將表單另存為PDF單據。 此外，這些工作流可以在組織內或跨網路防火牆使用。

在OSGi上，使用以Forms為中心的工作流，您可以快速構建和部署OSGi堆棧上各種任務的工作流，而無需在JEE堆棧上安裝完整的進程管理功能。 工作流的開發和管理使用熟悉的工作AEM流和收件箱AEM功能。 工作流構成了自動化跨多個軟體系統、網路、部門甚至組織的真實業務流程的基礎。

設定後，這些工作流可以手動觸發以完成定義的流程或在用戶提交表單時以寫程式方式運行 <!-- or [correspondence management](cm-overview.md) letter-->。 <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

基於OSGi的以Forms為中心的工作流擴展 [收件箱AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) 並為工作流編輯器提AEM供額外元件（步驟） [!DNL AEM Forms] — 以中心為中心的工作流。 <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

全部 [!DNL AEM Forms] 工作流步驟支援使用變數。 變數允許工作流步驟在運行時保留和傳遞跨步驟的元資料。 您可以建立不同類型的變數來儲存不同類型的資料。 您還可以建立變數集合（陣列）來儲存相關、相同類型資料的多個實例。 通常，當需要根據變數所包含的值做出決策或儲存在以後流程中需要的資訊時，您會使用變數或變數集合。 有關在這些以Forms為中心的工作流元件中使用變數的詳細資訊（步驟），請參見 [以Forms為中心的OSGi工作流 — 步驟參考](aem-forms-workflow-step-reference.md)。 有關建立和管理變數的資訊，請參見 [工作流中的AEM變數](variable-in-aem-workflows.md)。

下圖描述了在OSGi上建立、運行和監視以Forms為中心的工作流的端到端過程。

![工作流簡介](assets/introduction-to-aem-forms-workflow.jpg)

## 開始之前 {#before-you-start}

* 工作流是真實世界業務流程的表示。 讓您的實際業務流程和業務流程參與者清單保持就緒狀態。 另外，在開始建立工作流之前，請保持宣傳資料(自適應Forms、PDF文檔等)的就緒性。
* 工作流可以具有多個階段。 這些階段顯示在「收件箱」AEM中，並幫助報告工作流的進度。 將業務流程分為邏輯階段。
* 您可以配置工作流的分配任AEM務步驟，以向用戶或受分配者發送電子郵件通知。 所以， [啟用電子郵件通知](#configure-email-service)。
* 工作流還可以使用Adobe符號進行數字簽名。 如果您計畫在工作流中使用Adobe Sign, [配置Adobe Sign [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 在工作流中使用。

## 建立工作流模型 {#create-a-workflow-model}

工作流模型由業務流程的邏輯和流程組成。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以根據需要擴展包含參數和指令碼的工作流步驟，以提供更多功能和控制。 [!DNL AEM Forms] 除了現成可用的步驟AEM外，還提供了幾個步驟。 有關和的詳細AEM清單 [!DNL AEM Forms] 步驟，請參閱 [工作AEM流步驟參考](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) 和 [以Forms為中心的OSGi工作流 — 步驟參考](aem-forms-workflow.md)。

提AEM供直觀的用戶介面，以使用提供的工作流步驟建立工作流模型。 有關建立工作流模型的逐步說明，請參閱 [建立工作流模型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows)。 以下示例提供了逐步說明，用於為審批和複查工作流建立工作流模型：

>[!NOTE]
>
>必須是工作流編輯器組的成員才能建立或編輯工作流模型。

### 為審批和複查工作流建立模型 {#create-a-model-for-an-approval-and-review-workflow}

審批和審核工作流是針對需要人工干預才能做出決策的任務。 下面的示例為由前台銀行代理填寫的抵押貸款申請建立工作流模型。 申請填寫後，即發送審批。 隨後，核准的申請將發給申請人，請其使用Adobe Sign進行電子簽名。

該示例作為附加在下面的包提供。 使用包管理器導入並安裝示例。 您還可以執行以下步驟為應用程式手動建立工作流模型：

該示例建立由前台銀行代理填寫的抵押申請的工作流模型。 填寫完申請後，將發送審批。 稍後，將批准的應用程式發送給客戶，以便使用Adobe Sign進行電子簽名。 可以使用包管理器導入和安裝示例。

[取得檔案](assets/example-mortgage-loan-application.zip)

1. 開啟「工作流模型」控制台。 預設URL為 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 選擇 **建立**，則 **建立模型**。 將出現「添加工作流模型」對話框。
1. 輸入 **標題** 和 **名稱** （可選）。 例如，抵押貸款申請。 點擊 **完成**。
1. 選擇新建立的工作流模型並點擊 **編輯**。 現在，您可以添加工作流步驟來構建業務邏輯。 首次建立工作流模型時，它包含：

   * 步驟：流開始和流結束。 這些步驟表示工作流的開始和結束。 這些步驟是必需的，不能編輯或刪除。
   * 名為步驟1的「參與者」步驟示例。 此步驟配置為將工作項分配給管理員用戶。 刪除此步驟。

1. 啟用電子郵件通知。 您可以在OSGi上配置以Forms為中心的工作流，以向用戶或受分配者發送電子郵件通知。 執行以下配置以啟用電子郵件通知：

   1. 轉到AEM配置管理器 `https://[server]:[port]/system/console/configMgr`。
   1. 開啟 **[!UICONTROL 第CQ天郵件服務]** 配置。 為 **[!UICONTROL SMTP伺服器主機名]**。 **[!UICONTROL SMTP伺服器埠，]** 和 **[!UICONTROL &quot;發件人&quot;地址]** 的子菜單。 按一下「**[!UICONTROL 儲存]**」。
   1. 開啟 **[!UICONTROL 第CQ天連結外部化程式]** 配置。 在 **[!UICONTROL 域]** 欄位，指定本地、作者和發佈實例的實際主機名/IP地址和埠號。 按一下「**[!UICONTROL 儲存]**」。

1. 建立工作流階段。 工作流可以具有多個階段。 這些階段顯示在工AEM作流的收件箱和報告進度中。

   要定義舞台，請點擊 ![資訊圓](assets/info-circle.png) 表徵圖以開啟工作流模型屬性，開啟 **階段** 頁籤，為工作流模型添加階段，然後按一下 **保存並關閉**。 對於抵押申請示例，請建立階段：貸款申請、貸款申請狀態、待簽檔案和已簽貸款檔案。

1. 拖放 **分配任務** 步驟瀏覽到工作流模型。 將其作為模型的第一步。

   分配任務元件將由工作流建立的任務分配給用戶或組。 在分配任務的同時，可以使用元件為任務指定自適應表單或非互動式PDF。 需要自適應表單來接受來自用戶的輸入，非互動式PDF或只讀自適應表單用於僅查看工作流。

   也可以使用步驟來控制任務的行為。 例如，建立自動記錄文檔，將任務分配給特定用戶或組、已提交資料的路徑、要預填充的資料路徑以及預設操作。 有關分配任務步驟選項的詳細資訊，請參閱 [以Forms為中心的OSGi工作流 — 步驟參考](aem-forms-workflow.md) 的子菜單。

   ![工作流編輯器](assets/workflow-editor.png)

   對於抵押申請實例，將分配任務步驟配置為在任務完成後使用只讀自適應表單並顯示PDF文檔。 此外，選擇允許審批貸款請求的用戶組。 在 **操作** 頁籤 **提交** 的雙曲餘切值。 建立 **已採取的操作** 字串資料類型的變數，並將該變數指定為 **路由變數**。 例如，actionTaked。 另外，添加「批准」和「拒絕」路由。 路由在收件箱中顯示為單獨的操作(按AEM鈕)。 工作流根據用戶點擊的操作（按鈕）選擇分支。

   您可以導入示例包，該示例包可在節的開頭下載，以用於為例如抵押申請配置的分配任務步驟的所有欄位的完整值集。

1. 將「或拆分」元件從步驟瀏覽器拖放到工作流模型。 「或拆分」(OR Split)在工作流中建立一個拆分，之後只有一個分支處於活動狀態。 此步驟使您能夠將條件處理路徑引入工作流。 根據需要將工作流步驟添加到每個分支。

   可以使用規則定義、ECMA指令碼或外部指令碼為分支定義路由表達式。

   使用表達式編輯器為Branch 1和Branch 2建立路由表達式。 這些路由表達式有助於根據收件箱中的用戶操作選擇AEM分支。

   **分支1的路由表達式**

   用戶點擊時 **批准** 在收AEM件箱中，Branch 1被激活。

   ![OR拆分示例](assets/orsplit_branch1_active_new.png)

   **分支2的路由表達式**

   用戶點擊時 **拒絕** 在收AEM件箱中，將激活Branch 2。

   ![OR拆分示例](assets/orsplit_branch2_active_new.png)

   有關使用變數建立路由表達式的資訊，請參見 [變數 [!DNL AEM Forms] 工作流](variable-in-aem-workflows.md)。

1. 添加其他工作流步驟以構建業務邏輯。

   對於抵押示例，將生成記錄文檔、兩個分配任務步驟和一個簽名文檔步驟添加到模型的分支1中，如下圖所示。 一個分配任務步驟是顯示和發送 **要簽署貸款檔案** 另一個分配任務元件 **顯示簽名文檔**。 另外，將分配任務元件添加到分支2。 當用戶點擊收件箱中的拒絕時，將激AEM活它。

   對於為例如抵押申請配置的分配任務步驟、記錄文檔步驟和簽名文檔步驟的所有欄位的完整值集，請導入示例包，該示例包可在本節的開頭下載。

   工作流模型已就緒。 您可以通過各種方法啟動工作流。 有關詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流](#launch)。

   ![工作流編輯器 — 抵押](assets/workflow-editor-mortgage.png)

## 建立以Forms為中心的工作流應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流關聯的自適應表單。 當應用程式通過收件箱提交時，它將啟動關聯的工作流。 將Forms工作流作為應用程式在收件箱AEM和 [!DNL AEM Forms] 應用程式，執行以下操作建立工作流應用程式：

>[!NOTE]
>
>您必須是fd-administrator組的成員才能建立和管理工作流應用程式。

1. 在您的AEM作者實例上，轉到 ![工具–1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流應用程式]** 和水龍頭 **[!UICONTROL 建立]**。
1. 在「建立工作流應用程式」窗口中，為以下欄位提供輸入，並抽取 **建立**。 將建立新應用程式，並在「工作流應用程式」螢幕中列出。

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>標題在收件箱中可AEM見，並幫助用戶選擇應用程式。 保持描述性。 例如，儲蓄帳戶開戶應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名稱 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字元和下划線以外的所有字元都用連字元替換。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>說明在收件箱中AEM可見。 在說明欄位中提供有關應用程式的詳細資訊。 例如，應用程式的目的。<br /> </td>
  </tr>
  <tr>
   <td>自適應窗體</td>
   <td><p>指定自適應表單的路徑。 當用戶啟動應用程式時，將顯示指定的自適應表單。</p> <p><strong>注釋</strong>:工作流應用程式不支援超過一頁或需要在AppleiPad上滾動的表單和PDF文檔。 當在AppleiPad上開啟應用程式，並且自適應表單或PDF文檔長於頁面時，表單欄位和第二頁的內容將丟失。</p> </td>
  </tr>
  <tr>
   <td>存取群組</td>
   <td><p>選擇組。 該應用程式在「收AEM件箱」中僅對選定組的成員可見。 訪問組選項使 [!DNL workflow-users] 可供選擇的組。 </p> <br /> </td>
  </tr>
  <tr>
   <td>預填服務</td>
   <td>選擇 <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">預填充服務</a> 的子菜單。<br /> </td>
  </tr>
  <tr>
   <td>工作流程模型</td>
   <td>選擇 <a href="aem-forms-workflow.md#create-a-workflow-model">工作流模型</a> 的雙曲餘切值。 工作流模型由業務流程的邏輯和流程組成。 </td>
  </tr>
  <tr>
   <td>資料檔案路徑</td>
   <td>指定crx-repository中資料檔案的路徑。 該路徑相對於Adaptive Form負載，並包含資料檔案的名稱。 始終包括檔案的完整名稱（包括副檔名）（如果適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路徑</td>
   <td>指定crx-repository中附件資料夾的路徑。 附件路徑相對於負載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>記錄文件路徑</td>
   <td>指定crx-repository中記錄檔案的文檔路徑。 該路徑與Adaptive Form負載位置相關。 始終包括檔案的完整名稱（包括副檔名）（如果適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以Forms為中心的工作流 {#launch}

您可以通過以下方式啟動或觸發以Forms為中心的工作流：

* [從收件箱提交應AEM用程式](#inbox)
* [提交申請 [!DNL AEM Forms] 應用](#afa)

* [提交自適應表單](#af)
* [使用監視資料夾](#watched)

* [提交互動式通信或信函](#letter)

### 從收件箱提交應AEM用程式 {#inbox}

您建立的工作流應用程式可以作為收件箱中的應用程式使用。 屬於 [!DNL workflow-users] 組可以填寫和提交觸發關聯工作流的應用程式。 有關使用收件箱AEM提交應用程式和管理任務的資訊，請參閱 [在收件箱中管理Forms應用程式AEM和任務](manage-applications-inbox.md)。

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and allows you to make changes to the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### 提交自適應表單 {#af}

您可以配置自適應表單的提交操作，以便在提交自適應表單時啟動工作流。 自適應Forms提供 **調用工AEM作流** 提交操作以在提交自適應表單時啟動工作流。 有關提交操作的詳細資訊，請參閱 [配置提交操作](configuring-submit-actions.md)。 通過 [!DNL AEM Forms] app，啟用同步 [!DNL AEM Forms] 自適應表單屬性中的應用。

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Tap **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Tap **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### 清除工作流實例 {#purge-workflow-instances}

最大限度地減少工作流實例的數量會提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。 有關詳細資訊，請參見 [定期清除工作流實例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html) 清除工作流實例
