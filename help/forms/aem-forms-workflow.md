---
title: 如何使用AEM Forms進行商務程式自動化(BPM)？
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms工作流程自動化並快速建立業務流程工作流程。 例如，檢閱和核准、PDF產生、Adobe Sign工作流程。
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f0fec4a9-b214-4931-bf09-5898b082481e
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2489'
ht-degree: 1%

---

# OSGi上以Forms為中心的工作流程 {#forms-centric-workflow-on-osgi}

![英雄影像](do-not-localize/header.png)

企業會從數以百計的表單、各種後端系統以及線上或離線資料來源收集資料。 此外也有一組動態的使用者來對資料做出決策，其中涉及反複的稽核和核准流程。

除了針對內部和外部對象的檢閱和核准工作流程，大型組織和企業還會有重複性的任務。 例如，將PDF檔案轉換為另一種格式。 手動完成時，這些工作會佔用大量時間和資源。 企業也有對檔案和封存表單資料進行數位簽署的法律要求，以供日後以預先定義的格式使用。

## OSGi上Forms中心工作流程簡介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM工作流程快速建立最適化Forms型工作流程。 這些工作流程可用於審查和核准、業務流程流程、啟動檔案服務、與Adobe Sign簽名工作流程整合以及類似操作。 例如，信用卡申請處理、員工休假核准工作流程、將表單儲存為PDF檔案。 此外，這些工作流程也可在組織內或跨網路防火牆使用。

透過OSGi上的Forms工作流程，您可以在OSGi棧疊上快速建置和部署各種工作的工作流程，而不需要在JEE棧疊上安裝完整的流程管理功能。 工作流程的開發和管理使用熟悉的AEM工作流程和AEM收件匣功能。 工作流程構成了自動化跨越多個軟體系統、網路、部門甚至組織的真實業務流程的基礎。

設定之後，這些工作流程就可以手動觸發，以完成定義的程式，或在使用者提交表單<!-- or [correspondence management](cm-overview.md) letter-->時以程式設計方式執行。<!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

OSGi上的Forms導向工作流程延伸[AEM收件匣](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html?lang=zh-Hant#authoring)，並為AEM工作流程編輯器提供額外元件（步驟），以新增對[!DNL AEM Forms]導向工作流程的支援。<!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=zh-Hant#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

所有[!DNL AEM Forms]工作流程步驟都支援使用變數。 變數可讓工作流程步驟在執行階段跨步驟保留和傳遞中繼資料。 您可以建立不同型別的變數來儲存不同型別的資料。 您也可以建立變數集合（陣列），以儲存多個相關、相同型別資料的執行個體。 通常情況下，當您需要根據變數或變數集合持有的值來做出決定，或儲存您稍後在程式中需要的資訊時，會使用變數或變數集合。 如需有關在這些以Forms為中心的工作流程元件（步驟）中使用變數的詳細資訊，請參閱[在OSGi上以Forms為中心的工作流程 — 步驟參考](aem-forms-workflow-step-reference.md)。 如需建立和管理變數的詳細資訊，請參閱[AEM工作流程中的變數](variable-in-aem-workflows.md)。

下圖說明在OSGi上建立、執行和監視Forms工作流程的端對端程式。

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 適用性和使用案例

### 保險

## AEM Forms是否支援保險核准工作流程？

可以。AEM Forms支援以工作流程為基礎的稽核和核准，作為保險流程的一部分，啟用調整者稽核、經理核准和重新工作回圈。

## AEM Forms是否支援保險的製造商檢查程式流程？

可以。AEM Forms工作流程可設定為支援製作者 — 檢查者模式，確保資料輸入與核准角色之間的職責分離。

## AEM Forms是否可追蹤保險索賠或申請的狀態？

可以。AEM Forms工作流程可讓保險公司追蹤業務流程不同階段的表單提交和處理狀態。

## AEM Forms是否支援包銷工作流程？

是，且具有工作流程與整合。 AEM Forms支援工作流程導向的流程和後端整合，好讓應用程式資料可流入承保和決策系統。

## AEM Forms是否支援保險流程的稽核軌跡？

可以。AEM Forms透過工作流程歷史記錄、存取控制項和系統記錄支援稽核能力，可協助保險公司滿足內部和外部稽核需求。

## 開始之前 {#before-you-start}

* 工作流程是真實世界業務流程的表示法。 讓您的真實商業程式與商業程式參與者清單隨時待命。 此外，在開始建立工作流程之前，請準備好附屬資料(最適化Forms、PDF檔案等)。
* 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並有助於報告工作流程的進度。 將您的業務流程劃分為邏輯階段。
* 您可以設定AEM工作流程的指派工作步驟，以傳送電子郵件通知給使用者或受指派人。 因此，[啟用電子郵件通知](#configure-email-service)。
* 工作流程也可以使用Adobe sign進行數位簽名。 如果您打算在工作流程中使用Adobe Sign，請先為[設定 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)的Adobe Sign，然後再在工作流程中使用。

## 建立工作流程模型 {#create-a-workflow-model}

工作流程模型包含商務處理的邏輯與流程。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以利用引數和指令碼擴充工作流程步驟，以視需要提供更多功能與控制。 除了開箱即用的AEM步驟外，[!DNL AEM Forms]還提供一些步驟。 如需AEM和[!DNL AEM Forms]步驟的詳細清單，請參閱[AEM工作流程步驟參考](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=zh-Hant#extending-aem)和[OSGi上的Forms導向工作流程 — 步驟參考](aem-forms-workflow.md)。

AEM提供直覺式使用者介面，讓您使用提供的工作流程步驟建立工作流程模型。 如需建立工作流程模型的逐步指示，請參閱[建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html?lang=zh-Hant#workflows)。 下列範例提供逐步指示，讓您為核准與複查工作流程建立工作流程模型：

>[!NOTE]
>
>您必須是工作流程編輯器群組的成員，才能建立或編輯工作流程模型。

### 建立核准和稽核工作流程的模型 {#create-a-model-for-an-approval-and-review-workflow}

核准和稽核工作流程適用於需要人為干預才能做出決定的任務。 下列範例會建立由前台銀行代理商填寫的按揭貸款申請的工作流程模型。 填妥應用程式後，就會傳送以進行核准。 稍後，核准的申請會使用Adobe Sign傳送給申請人以索取電子簽章。

此範例可作為以下附加的套件提供。 使用封裝管理員匯入並安裝範例。 您也可以執行下列步驟，手動建立應用程式的工作流程模型：

此範例會建立工作流程模型，作為前台銀行代理商填寫的貸款應用程式。 填寫後，將傳送申請以供核准。 稍後，核准的應用程式會傳送給客戶，以供使用Adobe Sign進行電子簽章。 您可以使用封裝管理員匯入及安裝範例。

[取得檔案](assets/example-mortgage-loan-application.zip)

1. 開啟「工作流程模型」主控台。 預設URL為`https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 選取&#x200B;**建立**，然後選取&#x200B;**建立模型**。 「新增工作流程模型」對話方塊隨即顯示。
1. 輸入&#x200B;**Title**&#x200B;和&#x200B;**Name** （選擇性）。 例如，抵押貸款應用程式。 選取「**完成**」。
1. 選取已建立的工作流程模型，並選取&#x200B;**編輯**。 現在，您可以新增工作流程步驟以建立商業邏輯。 第一次建立工作流程模型時，模型會包含：

   * 步驟：流程開始與流程結束。 這些步驟代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯或移除。
   * 名為步驟1的範例參與者步驟。 此步驟已設定為將工作專案指派給管理員使用者。 移除此步驟。

1. 啟用電子郵件通知。 您可以在OSGi上設定以Forms為中心的工作流程，以傳送電子郵件通知給使用者或受指派人。 執行以下設定以啟用電子郵件通知：

   1. 前往`https://[server]:[port]/system/console/configMgr`的AEM設定管理員。
   1. 開啟&#x200B;**[!UICONTROL 天CQ郵件服務]**&#x200B;設定。 指定&#x200B;**[!UICONTROL SMTP伺服器主機名稱]**、**[!UICONTROL SMTP伺服器連線埠]**&#x200B;和&#x200B;**[!UICONTROL 「寄件者」位址]**&#x200B;欄位的值。 按一下&#x200B;**[!UICONTROL 儲存]**。
   1. 開啟&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;設定。 在&#x200B;**[!UICONTROL 網域]**&#x200B;欄位中，指定本機、作者和發佈執行個體的實際主機名稱/IP位址和連線埠號碼。 按一下&#x200B;**[!UICONTROL 儲存]**。

1. 建立工作流程階段。 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並報告工作流程的進度。

   若要定義階段，請選取![資訊圈](assets/info-circle.png)圖示以開啟工作流程模型屬性，開啟&#x200B;**階段**&#x200B;標籤，為工作流程模型新增階段，然後選取&#x200B;**儲存並關閉**。 以按揭申請為例，建立階段：貸款請求、貸款請求狀態、要簽署的檔案和已簽署的貸款檔案。

1. 將&#x200B;**指派任務**&#x200B;步驟瀏覽器拖放至工作流程模型。 使其成為模型的第一步。

   指派任務元件會指派由工作流程建立的任務給使用者或群組。 除了指派工作之外，您也可以使用元件，為該工作指定最適化表單或非互動式PDF。 若要接受使用者的輸入，且非互動式PDF或唯讀的最適化表單必須使用於僅供檢閱的工作流程，最適化表單為必要項。

   您也可以使用步驟來控制工作的行為。 例如，建立自動記錄檔案、將任務指派給特定使用者或群組、提交資料的路徑、要預先填入的資料路徑以及預設動作。 如需指派工作步驟選項的詳細資訊，請參閱OSGi上的[Forms導向工作流程 — 步驟參考](aem-forms-workflow.md)檔案。

   ![工作流程編輯器](assets/workflow-editor.png)

   以按揭應用程式為例，設定指派工作步驟以使用唯讀調適型表單，並在工作完成後顯示PDF檔案。 此外，選取允許核准貸款請求的使用者群組。 在&#x200B;**動作**&#x200B;索引標籤上，停用&#x200B;**提交**&#x200B;選項。 建立String資料型別的&#x200B;**actionTaken**&#x200B;變數，並將變數指定為&#x200B;**路由變數**。 例如，actionTaken。 此外，請新增核准與拒絕路由。 路由會在AEM收件匣中顯示為個別的動作（按鈕）。 工作流程會根據使用者點選的動作（按鈕）選取分支。

   您可以為設定的指派工作步驟的所有欄位（例如，抵押應用程式）匯入範例套件（可在區段開頭下載）。

1. 將OR拆分元件從步驟瀏覽器拖放至工作流程模型。 「OR分割」會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您將條件式處理路徑匯入工作流程中。 您可以視需要將工作流程步驟新增到每個分支。

   您可以使用規則定義、ECMA命令檔或外部命令檔來定義分支的路由表示式。

   使用運算式編輯器為Branch 1和Branch 2建立路由運算式。 這些路由運算式可協助您根據AEM收件匣中的使用者動作選擇分支。

   分支1 **的**&#x200B;路由運算式

   當使用者在AEM收件匣中點選&#x200B;**核准**&#x200B;時，分支1會啟用。

   ![OR分割範例](assets/orsplit_branch1_active_new.png)

   分支2 **的**&#x200B;路由運算式

   當使用者在AEM收件匣中點選&#x200B;**Reject**&#x200B;時，分支2就會啟動。

   ![OR分割範例](assets/orsplit_branch2_active_new.png)

   如需有關使用變數建立路由運算式的資訊，請參閱[工作流程 [!DNL AEM Forms] 中的](variable-in-aem-workflows.md)變數。

1. 新增其他工作流程步驟以建置商業邏輯。

   在抵押範例中，新增產生「記錄檔案」、兩個指派工作步驟，以及一個簽署檔案步驟至模型的「分支1」，如下圖所示。 一個指派工作步驟是顯示並傳送&#x200B;**要簽署的貸款檔案給申請者**，另一個指派工作元件是&#x200B;**以顯示已簽署的檔案**。 此外，新增指派工作元件至分支2。 當使用者點選AEM收件匣中的拒絕時，它會啟動。

   針對指派任務步驟、「記錄檔案」步驟及已設定的簽署檔案步驟（例如，抵押應用程式）的所有欄位之完整值集，匯入範例套件，可於本節開頭下載。

   工作流程模型已準備就緒。 您可以透過各種方法啟動工作流程。 如需詳細資訊，請參閱[在OSGi上啟動Forms中心的工作流程](#launch)。

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## 建立以Forms為中心的工作流程應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流程關聯的最適化表單。 透過「收件匣」提交應用程式時，它會啟動相關的工作流程。 若要讓Forms工作流程可作為AEM收件匣和[!DNL AEM Forms]應用程式中的應用程式，請執行以下動作以建立工作流程應用程式：

>[!NOTE]
>
>您必須是fd-administrator群組的成員，才能建立和管理工作流程應用程式。

1. 在您的AEM作者執行個體上，前往![工具–1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流程應用程式]**，然後點選&#x200B;**[!UICONTROL 建立]**。
1. 在[建立工作流程應用程式]視窗中，提供下列欄位的輸入，並點選&#x200B;**建立**。 隨即建立新應用程式，並列在「工作流程應用程式」畫面中。

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>標題會顯示在AEM收件匣中，並協助使用者選擇應用程式。 保持其描述性。 例如，儲蓄帳戶開立應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名稱 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字型大小和底線以外的所有字元都會取代為連字型大小。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>說明會顯示在AEM收件匣中。 在說明欄位中提供應用程式的詳細資訊。 例如，應用程式的用途。<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td><p>指定自適應表單的路徑。 當使用者啟動應用程式時，會顯示指定的調適型表單。</p> <p><strong>注意</strong>：工作流程應用程式不支援超過一頁的表單和PDF檔案，或需要在Apple iPad上捲動。 在Apple iPad上開啟應用程式，且最適化表單或PDF檔案超過一頁時，第二頁的表單欄位和內容會遺失。</p> </td>
  </tr>
  <tr>
   <td>存取群組</td>
   <td><p>選取群組。 只有選取群組的成員才能在AEM收件匣中看到應用程式。 存取群組選項可讓[!DNL workflow-users]群組的所有群組都可供選取。 </p> <br /> </td>
  </tr>
  <tr>
   <td>預填服務</td>
   <td>為最適化表單選取<a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">預填服務</a>。<br /> </td>
  </tr>
  <tr>
   <td>工作流程模型</td>
   <td>選取應用程式的<a href="aem-forms-workflow.md#create-a-workflow-model">工作流程模型</a>。 工作流程模型包含業務處理的邏輯與流程。 </td>
  </tr>
  <tr>
   <td>資料檔案路徑</td>
   <td>指定crx-repository中資料檔案的路徑。 此路徑是相對於最適化表單承載的，並包含資料檔案的名稱。 一律包括檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路徑</td>
   <td>指定crx-repository中附件資料夾的路徑。 附件路徑相對於承載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>記錄文件路徑</td>
   <td>指定crx-repository中記錄檔案的路徑。 此路徑是相對於最適化表單裝載位置。 一律包括檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以Forms為中心的工作流程 {#launch}

您可以透過以下方式啟動或觸發以Forms為中心的工作流程：

* [從AEM收件匣提交應用程式](#inbox)
* [從 [!DNL AEM Forms] 應用程式提交應用程式](#afa)

* [提交最適化表單](#af)
* [使用watched資料夾](#watched)

* [提互動動式通訊或信件](#letter)

### 從AEM收件匣提交應用程式 {#inbox}

您建立的工作流程應用程式可在「收件匣」中作為應用程式使用。 屬於[!DNL workflow-users]群組成員的使用者可以填寫並提交觸發相關工作流程的應用程式。

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and lets you change the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### 提交最適化表單 {#af}

您可以設定最適化表單的提交動作，以在提交最適化表單時啟動工作流程。 最適化Forms提供&#x200B;**叫用AEM工作流程**&#x200B;提交動作，以在提交最適化表單時啟動工作流程。 如需提交動作的詳細資訊，請參閱[設定提交動作](configuring-submit-actions.md)。 若要透過[!DNL AEM Forms]應用程式提交最適化表單，請在最適化表單屬性中啟用與[!DNL AEM Forms]應用程式同步。

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Select **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

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

1. Select **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

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
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### 清除工作流程例項 {#purge-workflow-instances}

將工作流程例項的數目降至最低會提升工作流程引擎的效能，因此您可以定期從儲存庫中清除已完成或執行中的工作流程例項。 如需詳細資訊，請參閱[定期清除工作流程執行個體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=zh-Hant)清除工作流程執行個體
