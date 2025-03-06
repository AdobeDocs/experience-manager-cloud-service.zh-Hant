---
title: 如何使用通用編輯器建立獨立的最適化Forms？
description: 本文說明如何使用AEM製作例項中的表單建立精靈，建立最適化Forms，並將表單發佈至AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 49%

---

# 使用通用編輯器(WYSIWYG)製作獨立表單

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請將您的GitHub組織名稱和存放庫名稱從您的官方地址傳送電子郵件至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 。 例如，如果存放庫URL是https://github.com/adobe/abc，組織名稱是adobe，存放庫名稱是abc。</span>

本文會透過從表單建立精靈中選取以Edge Delivery Services為基礎的範本，引導您完成使用通用編輯器製作獨立表單的程式。 您也可以將使用Universal Editor編寫的表單發佈到AEM Edge Delivery Services。

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

開始之前，請先了解您可以使用的表單元件類型：

* [適用於AEM Forms的Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)是一組可撰寫的服務，可啟用快速開發環境，讓作者可以使用通用編輯器快速更新、發佈和啟動新表單。 通用編輯器透過簡單易用的視覺化WYSIWYG介面，簡化Adobe Edge Delivery Services的表單建立工作。

* [最適化表單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)：這些是標準化的資料擷取元件。這些元件會為您的數位註冊體驗提供自訂功能、縮短的開發時間，並降低維護成本。開發人員可以輕鬆地自訂這些元件和設計其樣式。您可以造訪 [https://aemcomponents.dev/](https://aemcomponents.dev/) 以檢視可用核心元件的實際運作 **Adobe 建議使用這些現代且可擴展的元件來開發最適化表單**。

* [最適化表單基礎元件](/help/forms/creating-adaptive-form.md)：這些是經典 (舊) 的資料擷取元件。您可以繼續使用這些元件來編輯以現有基礎元件為主的最適化表單。如果您要建立新表單，Adobe 建議使用[最適化表單核心元件以建立最適化表單](#create-an-adaptive-form-core-components)。

AEM Forms 會提供一個區塊，稱為最適化表單區塊，協助您輕鬆建立 Edge Delivery Services 表單來擷取和儲存資料。您可以[建立已預先設定最適化AEM區塊的新Forms專案](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，或[將最適化Forms區塊新增至現有的AEM網站專案](#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github存放庫工作流程](/help/edge/assets/repo-workflow.png)

## 必要條件

* [設定您的GitHub存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)以建立您的AEM環境與GitHub存放庫之間的連線。
* 如果您已使用 Edge Delivery Services，請將最新版本的[最適化表單區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)新增至您的 GitHub 存放庫。
* AEM 表單作者執行個體包括根據 Edge Delivery Services 建立的範本。請確保您的環境中安裝了[最新版本的核心元件](https://github.com/adobe/aem-core-forms-components)。
* 將 AEM Forms 作為雲端服務作者執行個體的 URL 和 GitHub 存放庫保持便於使用。

## 使用通用編輯器編寫最適化表單

透過通用編輯器，您可以使用文字欄位、核取方塊和選項按鈕等現成的元件，輕鬆建立回應式互動式獨立表單。 它提供強大的功能，例如動態規則、順暢的資料整合和自訂選項，可讓您根據確切的需求建立表單。

>[!NOTE]
>
> 您也可以[在通用編輯器中使用AEM網站範本，在Edge Delivery Services網站中製作表單並將其發佈到Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project)。

若要使用通用編輯器製作獨立最適化表單，請執行以下步驟：

1. **在AEM Forms作者執行個體上建立最適化表單**

   1. 存取您的 AEM Forms 作為雲端服務作者執行個體。
   1.  選取 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**。1. 選取&#x200B;**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**。此時會開啟精靈。
   1. 在&#x200B;**Source**&#x200B;索引標籤中，選取以Edge Delivery Services為基礎的表單範本：

      ![建立EDS Forms](/help/edge/assets/create-eds-forms.png)

   1. 按一下&#x200B;**[!UICONTROL 建立]**，即會出現&#x200B;**建立表單**&#x200B;精靈。
   1. 指定 **GitHub URL**。例如，如果您的GitHub存放庫名為`edsforms`，則位於帳戶`wkndforms`下，URL為：
      `https://github.com/wkndforms/edsforms`
   1. 按一下&#x200B;**[!UICONTROL 建立]**。

      ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

      您按一下&#x200B;**[!UICONTROL 建立]**，表單即會在通用編輯器中開啟以供編寫。

      ![編寫表單](/help/edge/assets/author-form.png)

      <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

      當您按一下&#x200B;**[!UICONTROL 建立]**&#x200B;時，表單即會在通用編輯器中開啟以供編寫。

1. **在通用編輯器中編寫表單**

   1. 開啟內容瀏覽器，然後瀏覽至&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件 (在&#x200B;**內容樹**&#x200B;中)。

      ![內容樹](/help/edge/assets/content-tree.png)

   1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增所需元件。

      ![新增元件](/help/edge/assets/add-component.png)

   1. 選取新增的最適化表單元件並使用&#x200B;**[!UICONTROL 屬性]**&#x200B;更新其屬性。

      ![開啟屬性](/help/edge/assets/component-properties.png)

      以下熒幕擷圖顯示在Universal Editor中編寫的簡單`Registration Form`表單：

      ![連絡我們表單](/help/edge/assets/contact-us.png)

      現在您可以[設定和自訂表單提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。


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

## 發佈表單

現在，按一下Universal Editor右上角的&#x200B;**[!UICONTROL 發佈]**&#x200B;按鈕，將獨立表單發佈到Edge Delivery Services。

![發佈表單](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 請參閱[發佈並部署](/help/edge/docs/forms/universal-editor/publish-forms.md)文章以瞭解如何將表單發佈到Edge Delivery Services。

以下是存取 Edge Delivery Services 上的表單的方法：

* **暫存版本 (用於測試)**：暫存版本會顯示表單未發佈的工作版本，以用於測試目的。使用下列 URL 格式在表單上線之前預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果您的專案存放庫命名為「edsforms」，位於帳戶「wkandforms」下，而您使用「主要」分支和表單作為「登錄檔單」，則分段版本URL看起來如下所示：
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **即時版本 (發佈形式)**：即時版本會顯示表單的最新發佈版本，可供終端使用者存取。使用以下 URL 格式存取表單的已發佈即時版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果您的專案存放庫命名為「edsforms」，位於帳戶「wkandforms」下，而您使用「主要」分支和表單作為「登錄檔單」，則分段版本URL看起來如下所示：
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

暫存和即時版本的 URL 結構都保持不變。但是，您看到的內容會根據內容而有所不同：

![檢視已發佈的表單](/help/edge/assets/eds-view-publish-form.png)

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
