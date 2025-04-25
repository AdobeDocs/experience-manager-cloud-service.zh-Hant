---
title: 如何根據核心元件或Edge Delivery Services範本建立獨立表單，並在Edge Delivery Services上發佈
description: 本文說明如何在表單建立精靈中選取核心元件或Edge Delivery Services型範本，以建立最適化Forms。 您也可以將表單發佈到 AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: bcf8f9e5273819eaee09875ec81251fe4330701c
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 26%

---


# 從製作到發佈：Edge Delivery Services上的AEM Forms

<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址發送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容須包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>

Adobe Experience Manager (AEM)可讓您建立吸引人、回應式且動態的表單。 它提供多種編寫方法，每種方法都適合不同的需求和使用者專業知識水準&#x200B;。

本文主要介紹在AEM環境中撰寫表單，並透過Edge Delivery Services發佈表單的方法。 使用核心元件式範本建立的Forms可發佈在AEM和Edge Delivery Services上，提供部署彈性。 相反地，使用Edge Delivery Services範本撰寫的表單只能在Edge Delivery Services上發佈&#x200B;。

![製作及發佈最適化表單](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## 在AEM中製作表單及使用Edge Delivery Services發佈的優點：

* **保留現有的AEM工作流程**：組織可以繼續使用其已建立的AEM工作流程和治理結構，以確保內容建立的一致性和控制力&#x200B;。

* **增強效能**：透過Edge Delivery Services發佈可加快轉譯時間、改善使用者體驗並縮短頁面載入時間。&#x200B;

* **改善的SEO**： Edge Delivery Services的設計目的是提供具有高Google Lighthouse分數的內容，這可以導致更優異的搜尋引擎最佳化及提升可見度&#x200B;。

* **彈性的部署選項**：使用核心元件建置的Forms可發佈在AEM和Edge Delivery Services上，提供部署策略的彈性&#x200B;。

## 開始之前

開始在AEM中編寫表單並透過Edge Delivery Services發佈之前，請確定符合下列必要條件：

* 確保您已為Edge Delivery Services設定Github存放庫。
   * 如果您沒有存放庫，請[新的AEM專案已預先設定最適化Forms區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。
   * 如果您有存放庫，請新增最適化Forms區塊至您現有的存放庫。 [AEM Forms的Edge Delivery Services快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)中提供詳細指示。
* 在您的AEM環境和GitHub存放庫之間建立連線。 [如何操作？](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

<!--A decision flow diagram to guide the setup and publishing of Adaptive Forms:

![Github Repository Workflow](/help/edge/assets/repo-workflow.png){width=auto}-->

## 在AEM中製作表單並將其發佈到Edge Delivery Services

請依照下列步驟在AEM中撰寫表單，並在Edge Delivery Services上發佈：

[1.選擇樣版並建立表單](#choose-a-template-and-create-the-form)

[2.撰寫表單](#author-the-form)

[3.建立Edge Delivery Services設定](#create-an-edge-delivery-services-configuration)

[4.發佈表單](#publish-a-form)

[5.存取Edge Delivery Services上的表單](#access-the-form-on-edge-delivery-services)

### 選擇範本並建立表單

您可以在AEM例項上建立表單，以使用發佈至Edge Delivery Services：

* Edge Delivery Services範本
* 核心元件型範本

執行以下步驟來選擇範本並建立表單：

1. 登入AEM Forms as a Cloud Service作者例項。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**」。此時會開啟精靈。
1. 選取範本。 您可以選取下列其中一項：
   * 以Edge Delivery Services為基礎的範本&#x200B;****

     在&#x200B;**Source**&#x200B;索引標籤中，選取&#x200B;**Edge Delivery Services範本**：

     ![建立 EDS 表單](/help/edge/assets/create-eds-forms.png)

     當您選取&#x200B;**Edge Delivery Services範本**&#x200B;時，**[!UICONTROL 建立]**&#x200B;按鈕已啟用。

      * 核心元件型範本的&#x200B;****

     在&#x200B;**Source**&#x200B;索引標籤中，選取&#x200B;**以核心元件為基礎的範本**&#x200B;和&#x200B;**佈景主題**，已啟用&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕：

     ![以核心元件為基礎的範本](/help/forms/assets/core-component-based-template.png)

1. (選用) 您在「**[!UICONTROL 資料來源]**」或「**[!UICONTROL 提交]**」標籤中可以選取資料來源或提交動作。
1. (選用) 在「**[!UICONTROL 傳送]**」標籤中，您可以指定表單的發佈日期或取消發佈日期。
1. 按一下「**[!UICONTROL 建立]**」，系統就會針對下列專案顯示「**建立表單**」精靈：

   * **Edge Delivery Services範本式表單**

      1. 設定「**名稱**」和「**標題**」。
      2. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`、位於帳戶 `wkndforms` 之下，則 URL 為：
         `https://github.com/wkndforms/edsforms`

         ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

         當您按一下「**[!UICONTROL 建立]**」時，通用編輯器中便會開啟表單供您製作。

         ![製作表單](/help/edge/assets/author-form.png)

   * **以核心元件範本為基礎的表單**

      1. 設定「**名稱**」和「**標題**」。
      1. 在&#x200B;**路徑**&#x200B;欄位中指定最適化表單的儲存位置。

         ![建立表單精靈](/help/forms/assets/create-cc-form.png)

         當您按一下&#x200B;**[!UICONTROL 建立]**&#x200B;時，表單會在最適化表單編輯器中開啟以進行編寫。

         ![最適化表單編輯器](/help/forms/assets/af-editor-form.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以建立表單。 現在，您可以使用通用編輯器或調適型表單編輯器來編寫表單。

### 撰寫表單

使用Edge Delivery Services範本建立的表單會在[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)中開啟以進行編寫。 不過，使用核心元件式範本建立的表單會在最適化表單編輯器中開啟以進行編寫。

執行以下步驟來使用Edge Delivery Services範本的通用編輯器或核心元件範本的調適型表單編輯器製作表單：

>[!BEGINTABS]

>[!TAB Edge Delivery Services範本]


1. 開啟內容瀏覽器，然後導覽至&#x200B;**內容樹**&#x200B;中的&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件。

   ![內容樹](/help/edge/assets/content-tree.png)

1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**清單新增所需元件。
   ![新增元件](/help/edge/assets/add-component.png)

   底下熒幕擷圖顯示通用編輯器中編寫的`Registration Form`：

   ![聯絡我們表單](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> 如需使用通用編輯器製作最適化表單的詳細指示，[請按一下這裡](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

您現在可以[設定與自訂表單的提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

>[!TAB 核心元件型範本]

1. 在&#x200B;**將元件拖曳到這裡**&#x200B;區段中，按一下&#x200B;**[!UICONTROL 插入元件]**。

   ![將元件拖曳到這裡](/help/forms/assets/drag-components-af-editor.png)

1. 從&#x200B;**最適化表單元件**&#x200B;清單新增所需的元件。

   ![新增元件](/help/forms/assets/add-component-af.png)

底下熒幕擷圖顯示最適化表單編輯器中編寫的`Enrollment Form`：

![最適化表單編輯器](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> 如需根據核心元件範本建立最適化表單的詳細指引，[請按一下這裡](/help/forms/creating-adaptive-form-core-components.md)。

現在您可以[設定表單](/help/forms/configure-submit-actions-core-components.md)的提交動作。

>[!ENDTABS]

### 建立Edge Delivery Services設定

若要在Edge Delivery Services上發佈調適型表單，您需要在AEM執行個體上建立Edge Delivery Services設定。 執行以下步驟來建立Edge Delivery Services設定：

>[!BEGINTABS]
>[!TAB 針對使用Edge Delivery Services範本建立的表單]


在表單的設定容器中，會自動建立以Edge Delivery Services為基礎之範本的表單之Edge Delivery Services設定。

![Edge Delivery Services設定](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB 針對使用核心元件型範本建立的表單]

1. 在您的 AEM Forms 作為雲端服務作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Edge Delivery Services 設定]**。

   ![選取Edge Delivery Services設定](/help/edge/assets/select-eds-conf.png)

1. 選取與表單名稱相符的資料夾。例如，如果您的表單名為`enrollment-form`，請選擇資料夾`forms/enrollment-form`並按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 設定]**：

   ![Edge Delivery Services設定](/help/forms/assets/create-eds-conf.png)

1. 按一下&#x200B;**[!UICONTROL Edge Delivery Services設定]**，然後按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;以開啟屬性：

   ![自動建立的組態](/help/forms/assets/eds-conf.png)

   Edge Delivery Services設定隨即顯示。

1. 在Edge Delivery Services設定中指定下列專案：

   * **組織**：指定您的GitHub組織名稱。

   * **網站名稱**：指定您的GitHub存放庫名稱。
   * **分支**：指定分支名稱。 如果使用主要分支，請將文字方塊保留空白。
   * **（選用） Edge主機**：保留Edge主機選項。 表單會發佈到預覽(.page)和即時(.live)環境。
   * **（選擇性）網站驗證Token**：使用網站驗證Token，在您的AEM執行個體與Edge Delivery Services之間安全地驗證請求。

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。設定已建立。

>[!ENDTABS]

### 發佈表單

若要在Edge Delivery Services上存取表單，必須發佈表單。

執行以下步驟以發佈表單：

>[!BEGINTABS]
>在通用編輯器上[!TAB ]

1. 按一下通用編輯器右上角的&#x200B;**[!UICONTROL 發佈]**&#x200B;按鈕以發佈表單。

![發佈表單](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 若要了解如何將表單發佈至 Edge Delivery Services，請參閱「[發佈及部署](/help/edge/docs/forms/universal-editor/publish-forms.md)」一文。

>在最適化表單編輯器上[!TAB ]

1. 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要發佈的表單。

1. 按一下工具列中的「發佈&#x200B;****」選項，檢視所有將隨表單發佈的參考資產。

![在最適化表單編輯器上發佈表單](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 請參閱[在Experience Manager Forms中管理發布](/help/forms/manage-publication.md)一文，瞭解如何在最適化表單編輯器中發佈表單。

>[!ENDTABS]

## 存取Edge Delivery Services上的表單

* **暫存版本 (用於測試)**：暫存版本會顯示表單未發佈的工作版本，以用於測試目的。使用下列 URL 格式在表單上線之前預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **即時版本 (發佈形式)**：即時版本會顯示表單的最新發佈版本，可供終端使用者存取。使用以下 URL 格式存取表單的已發佈即時版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  暫存和即時版本的 URL 結構都保持不變。不過，您看到的內容會因內容而異。

以下熒幕擷取畫面會比較各階段和即時表單URL，以及使用Edge Delivery Services範本和核心元件範本建立之表單的視覺化預覽：

>[!BEGINTABS]
>[!TAB 存取使用Edge Delivery Services範本建立的表單]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>影像</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>分段版本</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="登錄檔單的階段版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>即時版本</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="登錄檔單的即時版本" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB 存取使用核心元件範本建立的表單]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>影像</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>分段版本</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="登錄檔單的階段化版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>即時版本</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="登錄檔單的即時版本" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## 疑難排解

載入表單時是否遇到問題？以下是一些常見問題以及修正的方法：

* **表單 URL**：仔細確認您表單的 URL 尾端並未包括副檔名 &quot;.html&quot;。Edge Deliver Service 不需要此副檔名。

* **AEM 作者 UR** L：確保 `fstab.yaml` 檔案中所列的 AEM 作者 URL 格式正確。它應包括下列詳細資料：

   * 正確的 GitHub 所有者
   * 正確的存放庫名稱
   * 您用於 Edge Delivery Services 的特定分支

## 開始建立表單

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
