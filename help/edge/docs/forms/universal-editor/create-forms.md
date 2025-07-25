---
title: 如何建立以核心元件或 Edge Delivery Services 範本為基礎的獨立表單，並發佈至 Edge Delivery Services
description: 本文說明在表單建立精靈中，選取以核心元件為基礎或以 Edge Delivery Services 為基礎的範本來建立自適應表單的方法。您也可以將表單發佈到 AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: ht
source-wordcount: '1687'
ht-degree: 100%

---


# 從編寫到發佈：Edge Delivery Services 上的 AEM Forms

<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址發送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容須包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>

您可以使用 Adobe Experience Manager (AEM) 建立具有吸引力的動態回應式表單。其提供多種編寫方法，分別適合不同的要求和使用者專業知識等級。

本文重點介紹在 AEM 環境中編寫表單並透過 Edge Delivery Services 發佈的方法。使用以核心元件為基礎的範本建立的表單可以在 AEM 和 Edge Delivery Services 上發佈，方便靈活地進行部署。相反的，使用以 Edge Delivery Services 為基礎的範本編寫的表單只能在 Edge Delivery Services 上發佈。

![編寫和發佈自適應表單](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## 在 AEM 中編寫表單並使用 Edge Delivery Services 發佈的優點：

* **保留現有的 AEM 工作流程**：各組織可以繼續使用其既定的 AEM 工作流程和治理結構，確保內容創作的一致性與可控性。

* **增強效能**：透過 Edge Delivery Services 發佈可以加快轉譯時間，提升使用者體驗並減少頁面載入時間。

* **改善 SEO**：Edge Delivery Services 是為了傳遞獲得 Google Lighthouse 高分數的內容而設計，有助於提升搜尋引擎最佳化成效，並增加可見度。&#x200B;

* **靈活的部署選項**：使用核心元件建立的表單可以在 AEM 和 Edge Delivery Services 上發佈，方便靈活採用不同的部署策略。

## 開始之前

開始在 AEM 中編寫表單並透過 Edge Delivery Services 發佈之前，請確保滿足以下先決條件：

* 確保您已經設定 Edge Delivery Services 的 Github 存放庫。
   * 如果您沒有存放庫，請使用[預先設定自適應表單區塊的新 AEM 專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。
   * 如果您有存放庫，請將自適應表單區塊新增至現有的存放庫。詳細說明請參閱[開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)。
* 在您的 AEM 環境和 GitHub 存放庫之間建立連線。[要怎麼做？](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

引導自適應表單之設定和發佈的決策流程圖：

![Github 存放庫工作流程](/help/forms/assets/repo-workflow.png){width=auto}

## 在 AEM 中編寫表單並將其發佈到 Edge Delivery Services

請依照以下步驟在 AEM 中編寫表單並將其發佈到 Edge Delivery Services：

[&#x200B;1. 選擇範本並建立表單](#choose-a-template-and-create-the-form)

[&#x200B;2. 編寫表單](#author-the-form)

[&#x200B;3. 發佈表單](#publish-a-form)

### 選擇範本並建立表單

您可以在 AEM 執行個體上建立表單，以使用下列方式發佈到 Edge Delivery Services：

>[!BEGINTABS]

>[!TAB 以 Edge Delivery Services 為基礎的範本]

執行以下步驟來選擇範本並建立表單：

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。此時會開啟精靈。
1. 在「**來源**」索引標籤中，選取一個&#x200B;**以 Edge Delivery Services 為基礎的範本**：

   ![建立 EDS 表單](/help/edge/assets/create-eds-forms.png)

   當您選取&#x200B;**以 Edge Delivery Services 為基礎的範本**&#x200B;時，便會啟用「**[!UICONTROL 建立]**」按鈕。
1. (選擇性) 您在「**[!UICONTROL 資料來源]**」或「**[!UICONTROL 提交]**」索引標籤中可以選取資料來源或提交動作。
1. (選擇性) 在「**[!UICONTROL 傳送]**」標籤中，您可以指定表單的發佈日期或取消發佈日期。
1. 按一下「**[!UICONTROL 建立]**」，隨即出現「**建立表單**」精靈：

   1. 設定「**名稱**」和「**標題**」。
   1. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`、位於帳戶 `wkndforms` 之下，則 URL 為：
      `https://github.com/wkndforms/edsforms`

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

   在按一下「**[!UICONTROL 建立]**」時，通用編輯器中便會開啟表單供您編寫。

   ![通用編輯器的螢幕擷圖顯示正在製作表單，其中元件面板位在左側，表單版面居中，而屬性面板則在右側](/help/edge/assets/author-form.png)
1. 按一下「**[!UICONTROL 建立]**」以建立表單。現在，您可以[使用通用編輯器編寫表單](#author-the-form)。

>[!TAB 以核心元件為基礎的範本]

執行以下步驟來選擇範本並建立表單：

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。此時會開啟精靈。
1. 在「**來源**」索引標籤中，選取一個&#x200B;**以核心元件為基礎的範本**&#x200B;和&#x200B;**主題**，便會啟用「**[!UICONTROL 建立]**」按鈕。

   ![以核心元件為基礎的範本](/help/forms/assets/core-component-based-template.png)

1. (選擇性) 您在「**[!UICONTROL 資料來源]**」或「**[!UICONTROL 提交]**」索引標籤中可以選取資料來源或提交動作。
1. (選擇性) 在「**[!UICONTROL 傳送]**」標籤中，您可以指定表單的發佈日期或取消發佈日期。
1. 按一下「**[!UICONTROL 建立]**」，隨即出現「**建立表單**」精靈，以便：
   1. 指定「**名稱**」和「**標題**」。
   1. 在「**路徑**」欄位指定要儲存自適應表單的位置。

   ![建立表單精靈](/help/forms/assets/create-cc-form.png)

   按一下「**[!UICONTROL 建立]**」，即會在自適應表單編輯器中開啟表單供您編寫。

   ![自適應表單編輯器](/help/forms/assets/af-editor-form.png)

1. 按一下「**[!UICONTROL 建立]**」以建立表單。現在，您可以[使用自適應表單編輯器編寫表單](#author-the-form)。

>[!ENDTABS]

### 編寫表單

使用以 Edge Delivery Services 為基礎的範本所建立的表單，會在[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) 中開啟，以供進行編寫。但是，使用以核心元件為基礎的範本所建立的表單，會在自適應表單編輯器中開啟，以供進行編寫。

請執行下列步驟來編寫表單 (對於以 Edge Delivery Services 為基礎的範本，請使用通用編輯器；對於以核心元件為基礎的範本，則請使用自適應表單編輯器)：

>[!BEGINTABS]

>[!TAB 以 Edge Delivery Services 為基礎的範本]


1. 開啟內容瀏覽器，然後導覽至&#x200B;**內容樹**&#x200B;中的&#x200B;**[!UICONTROL 自適應表單]**&#x200B;元件。

   ![內容樹](/help/edge/assets/content-tree.png)

1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**自適應表單元件**清單新增所需元件。
   ![新增元件](/help/edge/assets/add-component.png)

   下方的螢幕擷圖顯示在通用編輯器中編寫的 `Registration Form`：

   ![通用編輯器中填寫完成的「聯絡我們」表單螢幕擷圖，顯示姓名、電子郵件、電話以及訊息的表單欄位，並具有適當的樣式和版面](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> 有關使用通用編輯器編寫自適應表單的詳細說明，[請按一下此處](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

您現在可以[設定與自訂表單提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

>[!TAB 以核心元件為基礎的範本]

1. 在「**[!UICONTROL 將元件拖曳到這裡]**」區段按一下「**插入元件**」。

   ![將元件拖曳到這裡](/help/forms/assets/drag-components-af-editor.png)

1. 從&#x200B;**自適應表單元件**&#x200B;清單中新增所需的元件。

   ![新增元件](/help/forms/assets/add-component-af.png)

下方的螢幕擷圖顯示在自適應表單編輯器中編寫的`Enrollment Form`：

![自適應表單編輯器](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> 有關以核心元件範本為基礎建立自適應表單的詳細指南，請[按一下這裡](/help/forms/creating-adaptive-form-core-components.md)。

您現在可以[設定表單提交動作](/help/forms/configure-submit-actions-core-components.md)。

>[!ENDTABS]

### 發佈表單

若要在 Edge Delivery Services 上發佈自適應表單，您必須[在 AEM](#create-an-edge-delivery-services-configuration)執行個體上建立 Edge Delivery Services 設定。

#### 建立 Edge Delivery Services 設定

執行下列步驟來建立 Edge Delivery Services 設定：

>[!BEGINTABS]
>[!TAB 以 Edge Delivery Services 為基礎的範本]


根據以 Edge Delivery Services 為基礎的範本製作的表單，會在表單的設定容器中自動建立其 Edge Delivery Services 設定。

![Edge Delivery Services 設定](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB 以核心元件為基礎的範本]

1. 在您的 AEM Forms as a Cloud Service 作者實例上，瀏覽至「**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Edge Delivery Services 設定]**」。

   ![選取 Edge Delivery Services 設定](/help/edge/assets/select-eds-conf.png)

2. 選取與表單名稱相符的資料夾。例如，如果您的表單名稱為 `enrollment-form`，請選擇資料夾 `forms/enrollment-form`，然後按一下「**[!UICONTROL 建立]** > **[!UICONTROL 設定]**」：

   ![Edge Delivery Services 設定](/help/forms/assets/create-eds-conf.png)

3. 按一下「**[!UICONTROL Edge Delivery Services 設定]**」，然後按一下「**[!UICONTROL 屬性]**」以開啟屬性：

   ![自動建立的設定](/help/forms/assets/eds-conf.png)

   隨即出現 Edge Delivery Services 設定。

4. 在 Edge Delivery Services 設定中指定以下內容：

   * **組織**：指定您的 GitHub 組織名稱。

   * **網站名稱**：指定您的 GitHub 存放庫名稱。
   * **分支**：指定分支名稱。如果使用主分支，請將文字方塊保留空白。
   * **(可選) Edge 主機**：依原樣保留 Edge 主機選項。該表單同時發佈到預覽 (.page) 和即時 (.live) 環境。
   * **(可選) 網站驗證權杖**：使用網站驗證權杖在 AEM 執行個體和 Edge Delivery Services 之間安全地驗證請求。

5. 按一下「**[!UICONTROL 儲存並關閉]**」。已建立設定。

>[!ENDTABS]

#### 存取 Edge Delivery Services 上的表單

若要存取 Edge Delivery Services 上的表單，則必須發佈該表單。執行以下步驟來發佈表單：

>[!BEGINTABS]
>[!TAB 使用通用編輯器]

1. 按一下通用編輯器右上角的「**[!UICONTROL 發佈]**」按鈕來發佈表單。

![通用編輯器的螢幕擷圖顯示發佈對話框，其中包含表單發佈選項和確認按鈕](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 請參閱「[發佈及部署](/help/edge/docs/forms/universal-editor/publish-forms.md)」一文，了解如何將表單發佈至 Edge Delivery Services。

>[!TAB 使用自適應表單編輯器]

1. 從 Experience Manager Forms 主控台瀏覽至父系資料夾，並選取要發佈的表單。

1. 按一下工具列上的「**[!UICONTROL 發佈]**」選項，查看將隨表單發佈的所有參考資產。

![在自適應表單編輯器上發佈表單](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 請參閱[在 Experience Manager Forms 中管理發佈](/help/forms/manage-publication.md)一文，以了解如何在自適應表單編輯器上發佈表單。

>[!ENDTABS]

* **暫存版本 (用於測試)**：暫存版本會顯示表單未發佈的工作版本，以用於測試目的。使用下列 URL 格式在表單上線之前預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **即時版本 (發佈形式)**：即時版本會顯示表單的最新發佈版本，可供終端使用者存取。使用以下 URL 格式存取表單的已發佈即時版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  暫存和即時版本的 URL 結構都保持不變。但是，您看到的內容會根據情境而有所不同。

對於使用以 Edge Delivery Services 為基礎和以核心元件為基礎的範本所建立的表單，以下螢幕擷圖比較其暫存和即時表單 URL 以及視覺預覽：

>[!BEGINTABS]
>[!TAB 以 Edge Delivery Services 為基礎的範本]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>影像</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>暫存版本</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="註冊表單的暫存版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>即時版本</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="註冊表單的即時版本" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB 以核心元件為基礎的範本]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>影像</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>暫存版本</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="註冊表單的暫存版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>即時版本</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="註冊表單的即時版本" style="width: 100%; height: auto;" /></td>
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
