---
title: 如何使用通用編輯器根據Edge Delivery Services範本建立獨立表單？
description: 本文說明如何在表單建立精靈中選取以Edge Delivery Services為基礎的範本，使用通用編輯器建立表單。 您也可以將表單發佈至AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 979aad24ebbd0ef1d4d1fc92d402fca20bc27a44
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 83%

---

# 在通用編輯器中建立獨立表單的逐步指南

<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址發送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容須包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>

本文會透過從「表單建立精靈」中選取以Edge Delivery Services為基礎的範本，引導您使用通用編輯器來建立和編寫獨立表單。 您也可以透過通用編輯器，將製作好的表單發佈至 AEM Edge Delivery Services。

AEM Forms 會提供一個稱為「最適化表單區塊」的區塊，協助您輕鬆建立 Edge Delivery Services 表單來擷取和儲存資料。您可以[建立使用最適化表單區塊預先設定的全新 AEM 專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，或者[將最適化表單區塊新增至現有的 AEM Site 專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github 存放庫工作流程](/help/edge/assets/repo-workflow.png)

## 必要條件

* [設定您的 GitHub 存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，在您的 AEM 環境與 GitHub 存放庫之間建立連線。
* 如果您已使用 Edge Delivery Services，請將最新版本的[最適化表單區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)新增至您的 GitHub 存放庫。
* AEM 表單作者執行個體包括根據 Edge Delivery Services 建立的範本。請確保您的環境中安裝了[最新版本的核心元件](https://github.com/adobe/aem-core-forms-components)。
* 將 AEM Forms 作為雲端服務作者執行個體的 URL 和 GitHub 存放庫保持便於使用。

## 在通用編輯器中處理表單

藉助通用編輯器，您可以使用已建立的元件 (例如文字欄位、核取方塊和選項按鈕)，輕鬆建立回應式及互動式的獨立表單。它提供強大的功能，例如動態規則、順暢的資料整合和自訂選項，可讓您根據確切的需求建立表單。 您也可以將表單發佈至AEM Edge Delivery Services。 您可以在通用編輯器中對表單執行下列動作：
* [建立表單](#create-a-form)
* [撰寫表單](#author-a-form)
* [發佈表單](#publish-a-form)
* [管理表單](#manage-a-form)

>[!NOTE]
>
> 您也可以[使用通用編輯器中的 Edge Delivery Services 網站範本，於 AEM Site 中製作表單，並將其發佈至 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project)。


### 建立表單

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**」。此時會開啟精靈。
1. 在「**來源**」索引標籤中，選取以 Edge Delivery Services 為基礎的表單範本：

   ![建立 EDS 表單](/help/edge/assets/create-eds-forms.png)


   當您選取 Edge Delivery Services 的範本時，便會啟用「**[!UICONTROL 建立]**」按鈕。
1. (選用) 您在「**[!UICONTROL 資料來源]**」或「**[!UICONTROL 提交]**」標籤中可以選取資料來源或提交動作。
1. （選擇性）在&#x200B;**[!UICONTROL 傳遞]**&#x200B;索引標籤中，您可以指定表單的發佈或取消發佈日期。

1. 按一下「**[!UICONTROL 建立]**」，便會出現「**建立表單**」精靈。
1. 設定「**名稱**」和「**標題**」。
1. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`、位於帳戶 `wkndforms` 之下，則 URL 為：
   `https://github.com/wkndforms/edsforms`
1. 按一下「**[!UICONTROL 建立]**」。

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

   按一下「**[!UICONTROL 建立]**」，通用編輯器中便會開啟表單供您製作。

   ![製作表單](/help/edge/assets/author-form.png)

   <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

   當您按一下「**[!UICONTROL 建立]**」時，通用編輯器中便會開啟表單供您製作。

### 撰寫表單

1. 開啟內容瀏覽器，然後導覽至&#x200B;**內容樹**&#x200B;中的&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件。

   ![內容樹](/help/edge/assets/content-tree.png)

1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增所需元件。

   ![新增元件](/help/edge/assets/add-component.png)

1. 選取新增的最適化表單元件，然後使用「**[!UICONTROL 屬性]**」更新其屬性。

   ![開啟屬性](/help/edge/assets/component-properties.png)

   下方的螢幕擷圖顯示在通用編輯器中製作的簡單 `Registration Form` 表單：

   ![聯絡我們表單](/help/edge/assets/contact-us.png)

   您現在可以[設定與自訂表單提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

### 發佈表單

現在，按一下通用編輯器右上角的「**[!UICONTROL 發佈]**」按鈕，即可將獨立表單發佈至 Edge Delivery Services。

![發佈表單](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 若要了解如何將表單發佈至 Edge Delivery Services，請參閱「[發佈及部署](/help/edge/docs/forms/universal-editor/publish-forms.md)」一文。

以下是存取 Edge Delivery Services 上的表單的方法：

* **暫存版本 (用於測試)**：暫存版本會顯示表單未發佈的工作版本，以用於測試目的。使用下列 URL 格式在表單上線之前預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，若您的專案存放庫名稱為「edsforms」、位於帳戶「wkndforms」之下，並且您使用的是「main」分支和「Registration Form」表單，則暫存版本 URL 會如下所示：
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **即時版本 (發佈形式)**：即時版本會顯示表單的最新發佈版本，可供終端使用者存取。使用以下 URL 格式存取表單的已發佈即時版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，若您的專案存放庫名稱為「edsforms」、位於帳戶「wkndforms」之下，並且您使用的是「main」分支和「Registration Form」表單，則暫存版本 URL 會如下所示：
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

暫存和即時版本的 URL 結構都保持不變。但是，您看到的內容會根據內容而有所不同：

![檢視已發佈的表單](/help/edge/assets/eds-view-publish-form.png)

### 管理表單

您可以透過 AEM Forms 使用者介面執行多項表單操作。

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

1. 選取表單，然後工具列便會顯示您可以對所選表單執行的操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>編輯</p> </td>
   <td><p>以編輯模式開啟表單。<br /><br /> </p> </td>
  </tr>
    <tr>
   <td><p>屬性</p> </td>
   <td><p>您可以選擇修改表單屬性。<br /> <br /> </p> </td>
  </tr>
  <td><p>複製</p> </td>
   <td><p> 您可以選擇複製表單並將其貼上至所需位置。<br /><br /> </p> </td>
  </tr>
   <tr>
   <td><p>預覽</p> </td>
   <td><p>您可以選擇以 HTML 格式預覽表單，或是將 XML 檔案中的資料與表單合併來執行自訂預覽。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載所選表單。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始評論/管理評論</p> </td>
   <td><p>能啟動和管理所選表單的評論。<br /><br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈所選表單。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除所選表單。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>比較</p> </td>
   <td><p>比較兩種不同的表單以進行預覽。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 疑難排解

載入表單時是否遇到問題？以下是一些常見問題以及修正的方法：

* **表單 URL**：仔細確認您表單的 URL 尾端並未包括副檔名 &quot;.html&quot;。Edge Deliver Service 不需要此副檔名。

* **AEM 作者 UR** L：確保 `fstab.yaml` 檔案中所列的 AEM 作者 URL 格式正確。它應包括下列詳細資料：

   * 正確的 GitHub 所有者
   * 正確的存放庫名稱
   * 您用於 Edge Delivery Services 的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 開始建立表單

{{universal-editor-see-also}}
