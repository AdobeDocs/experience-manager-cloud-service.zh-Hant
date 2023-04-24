---
title: 在AEM Sites頁面中新增最適化表單（核心元件）
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: 您可以在AEM Sites頁面中使用適用性表單（核心元件）來填寫和提交表單，而不需離開AEM Sites頁面。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 2%

---

# 將適用性Forms新增至AEM Sites頁面 {#add-an-adaptive-form-to-aem-sites-page}

## 概觀 {#overview}

您可以順暢地在AEM Sites頁面中撰寫或內嵌適用性Forms，讓使用者無需離開Sites頁面即可填寫及提交表單。 它可協助使用者停留在網頁的其他元素上，同時與表單互動。

您可以選擇下列其中一種方法，在AEM Sites頁面中製作或內嵌適用性表單：

* **將表單元件拖放至適用性Forms容器元件，以建立適用性表單**:使用 [適用性Forms容器](#af-container-component) 元件，在網頁內建立托管最適化表單的空間。 您可以在此空間拖放適用性表單元件以建立表單。 例如，請觀看以下影片，了解如何使用 [!UICONTROL 適用性Forms容器] 元件：

>[!VIDEO](/help/forms/assets/formcreationbyadaptiveformcontainer.mp4)

此 [適用性表單容器](#af-container-component) 元件可讓您直接在AEM Sites編輯器中利用適用性Forms元件來建立數位註冊體驗。 此整合可為想在AEM Sites頁面中建立和管理表單的AEM Sites作者提供順暢的體驗。

* **內嵌現有的最適化表單**:此 [適用性Forms — 內嵌](#embed-existing-af) 元件可讓您輕鬆將預先存在的適用性表單整合至AEM Sites中的頁面。 例如，使用 [!UICONTROL 適用性Forms — 內嵌] 元件，如下列影片所示：

>[!VIDEO](/help/forms/assets/embednewform_embed.mp4)

這一功能增強了自適應Forms的適應性和可重用性。 此整合為客戶重複使用已建立的適用性Forms提供了便利的方式。

* **使用適用性Forms精靈建立表單**:

   使用 [適用性Forms — 內嵌](#embed-new-af) 元件，使用「表單建立」精靈從AEM Sites編輯器中建立最適化表單。 表單會儲存為外部實體。 您也可以在其他Sites頁面和獨立表單中重複使用此表單。
例如，請觀看以下影片，了解如何使用 [!UICONTROL 適用性Forms — 內嵌] 元件。

>[!VIDEO](/help/forms/assets/createnewform_embed.mp4)

### 考量 {#considerations}

您可以使用規則編輯器來新增或控制適用性表單元件的動態行為。 例如，隱藏或顯示元件。 規則編輯器無法用於非適用性表單元件。 因此，在AEM Forms容器元件中使用非最適化表單元件時，請盡量使用您的注意事項。

## 使用適用性Forms容器元件建立適用性表單 {#af-container-component}

此 [!UICONTROL 適用性表單容器] 元件可讓您使用AEM Sites編輯器中的適用性Forms元件來建立數位註冊體驗。 您可以拖放表單元件，以建立最適化表單。

### 必備條件 {#prerequisites-af-container}

+++ 啟用 **[!UICONTROL 適用性Forms容器]** 元件（在關聯模板的策略中）。

啟用 [!UICONTROL 適用性Forms容器] 元件，請執行下列步驟：
1. 前往 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯範本]
1. 按一下 [!UICONTROL 原則] ，然後選取 **核心元件範例 — 最適化表單** 核取方塊。
1. 按一下 [!UICONTROL 完成].

>[!VIDEO](/help/forms/assets/adaptiveformcontainer.mp4)

+++

+++ 在網站的頁面上包含clientlib

若要在AEM Sites頁面中使用適用性Forms元件，請使用AEM原型/Git存放庫和部署管道，將Customheaderlibs和Customfooterlibs用戶端程式庫包含至AEM Sites頁面。

1. 開啟 [AEM Forms原型或複製的Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 專案（在文字編輯器中）。 例如Visual Studio Code。
1. 導覽至 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製 `sling:resourceSuperType`. 例如，值為 `core/wcm/components/page/v3/page`.

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似結構 `ui.apps/src/main/content/jcr_root/apps` 與 `core/wcm/components/page/v3/page`.

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 新增 `customheaderlibs.html` 和 `customfooterlibs.html` 檔案。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   customfooterlibs.html用於JavaScript，而customheaderlibs.html用於CSS。

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 來部署變更。

+++

### 使用適用性Forms容器元件建立適用性表單 {#create-af-using-af-container}


若要建立最適化表單，請使用 [!UICONTROL 適用性Forms容器] 元件：

1. 在編輯模式中開啟AEM Sites頁面。
1. 從「元件」瀏覽器面板，拖放 **[!UICONTROL 適用性Forms容器]** 元件。
1. 使用適用性Forms元件建立適用性表單。
1. 儲存設定。

>[!VIDEO](/help/forms/assets/af-container.mp4)

你的表格準備好了。 當您發佈AEM Sites頁面時，它會自動發佈適用性表單及其相關的參考資產。

#### 設定最適化表單容器屬性 {#configure-additional-settings-container}

您可以自訂 [!UICONTROL 適用性表單容器] 元件。 例如，您可以設定預填服務，以載入網站頁面上具有預先填入值的適用性表單。 您可以配置「資料模型」設定，以將適用性表單與資料模型關聯。 如果您想在提交適用性表單時將資料儲存在OneDrive或SharePoint上，請配置「提交」動作的設定。 您也可以為最適化Forms新增自訂提交動作。

若要設定 **[!UICONTROL 適用性Forms容器]** 元件，按一下 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在動作列上。 此 **[!UICONTROL 編輯適用性Forms容器]** 對話框開啟。

![編輯對話方塊](/help/forms/assets/adaptiveformcontainer-editdialog.png)

在 [!UICONTROL 編輯適用性Forms容器] 對話框，可以指定以下內容。
* **基本標籤**
   * **預填服務**:您可以使用預填服務，使用現有資料自動填寫適用性表單的欄位。 使用者開啟表單時，會預填這些欄位的值。 有關預填服務的資訊，請參見 [預填最適化表單欄位](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **客戶端庫類別**:指定 [JavaScript函式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 用於運算式中，且受適用性Forms支援。
* **資料模型**:資料模型可讓您將不同資料來源的實體和服務整合至最適化表單。 選擇 **[!UICONTROL 表單資料模型]** 如果您要建立的適用性表單涉及從多個資料來源擷取和寫入資料。
   * **表單資料模型**:表單資料模型可讓適用性表單與不同的資料來源通訊。 如需設定資料來源的相關資訊，請參閱 [設定資料來源。](/help/forms/configure-data-sources.md)
   * **結構**:結構表示組織中後端系統產生或使用資料的結構。 您可以 [將結構關聯至適用性表單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) 並使用其元素將動態內容新增至最適化表單。

      >[!NOTE]
      >
      > 配置表單資料模型後，您無法更改關聯的表單模型。 但是，可以修改與表單資料模型相關聯的架構。

* **提交標籤**

   * **重新導向至 URL**

      **重新導向URL/路徑**:指定在提交動作後，適用性表單重新導向的URL或路徑。

      **提交動作**:當使用者按一下適用性表單上的「提交」按鈕時，會觸發提交動作。 您可以 [在適用性表單上設定提交動作](/help/forms/configuring-submit-actions.md). 適用性表單提供一些立即可用的提交動作：
      * 提交到REST端點
      * 傳送電子郵件
      * 使用表單資料模型提交
      * 叫用AEM工作流程
      * 提交至 SharePoint
      * 提交至 OneDrive
      * 提交到 Azure Blob 儲存體

   您也可以 [擴展預設的提交操作](custom-submit-action-form.md) 建立自訂提交動作。

* **顯示訊息**
   * **訊息內容**:使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有在您選擇顯示感謝訊息時，才可使用此選項。

## 內嵌現有的最適化表單  {#aem-container-component}

使用 **[!UICONTROL 適用性Forms — 內嵌]** 元件，您可以內嵌新的適用性表單，或在網站的頁面中內嵌現有的適用性表單。 此 [!UICONTROL 適用性Forms — 內嵌] 元件可讓您：

* [Embe現有適用性表單](#embed-new-af)

* [建立和內嵌新的最適化表單](#embed-existing-af)

### 必備條件 {#prerequisites}

+++ 啟用 **適用性Forms — 內嵌** 元件（在關聯模板的策略中）。

啟用 [!UICONTROL 適用性Forms — 內嵌] 元件，請執行下列步驟：
1. 前往 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯範本]
1. 按一下 [!UICONTROL 原則] ，然後選取 **核心內容** 核取方塊。
1. 按一下 [!UICONTROL 完成].

>[!VIDEO](/help/forms/assets/enableadaptiveform-embedtemplate.mp4)

+++

+++ 在網站的頁面上包含clientlib

當 **[!UICONTROL 表單覆蓋頁面的整個寬度時]** 選項 **[!UICONTROL 表單容器]** 配置對話框和 **使用核心元件的適用性Forms** ，則必須在您對應網站的頁面上包含clientlib。

![覆蓋Gif](/help/forms/assets/overlaycorecomponent.gif)

若要在AEM Sites頁面中使用適用性Forms元件，請使用AEM原型/Git存放庫和部署管道，將Customheaderlibs和Customfooterlibs用戶端程式庫包含至AEM Sites頁面。

1. 開啟 [AEM Forms原型或複製的Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 專案（在文字編輯器中）。 例如Visual Studio Code。
1. 導覽至 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製 `sling:resourceSuperType`. 例如，值為 `core/wcm/components/page/v3/page`.

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似結構 `ui.apps/src/main/content/jcr_root/apps` 與 `core/wcm/components/page/v3/page`.

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 新增 `customheaderlibs.html` 和 `customfooterlibs.html` 檔案。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   customfooterlibs.html用於JavaScript，而customheaderlibs.html用於CSS。

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 來部署變更。

+++

### 內嵌新的最適化表單 {#embed-new-af}

1. 在編輯模式中開啟AEM Sites頁面。
1. 從「元件」瀏覽器面板，拖放 [!UICONTROL 適用性Forms — 內嵌] 元件。
1. 按一下 **加號** 圖示，系統就會將您重新導向至表單建立精靈。

   ![適用性Forms — 內嵌元件](/help/forms/assets/aemformcontainer.png)

1. 從 [!UICONTROL 表單建立] 嚮導。
1. 此 [!UICONTROL 資產路徑] 已包含已建立適用性表單的路徑
1. 儲存設定。 適用性表單現已內嵌於頁面中。

### 內嵌現有適用性表單 {#embed-existing-af}

1. 在編輯模式中開啟AEM Sites頁面。
1. 從「元件」瀏覽器面板，拖放 [!UICONTROL 適用性Forms — 內嵌] 元件。
1. 點選 [!UICONTROL 適用性Forms — 內嵌] 元件，然後點選 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在動作列上。 此 **[!UICONTROL 編輯適用性Forms — 內嵌]** 對話框開啟。
1. 瀏覽並選取要內嵌於 [!UICONTROL 資產路徑].
1. 儲存設定。 適用性表單現已內嵌於頁面中。

#### 配置適用性表單_內嵌屬性

您可以自訂 [!UICONTROL 適用性表單 — 內嵌] 元件。 在 [!UICONTROL 編輯適用性Forms — 內嵌] 對話框，可以指定以下內容。
* **資產路徑**:瀏覽並選取要內嵌的適用性表單。 如果您從「資產」瀏覽器中拖放，則會自動填入。
* **貼文提交** :選取要在表單提交時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。
   * **顯示感謝消息**:使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有在您選擇顯示感謝訊息時，才可使用此選項。
   * **顯示感謝頁**:瀏覽並選取要在表單提交時顯示的頁面。 只有在您選擇顯示感謝頁面時，才可使用此選項。
   * **重新導向至感謝頁面**:啟用選項，將包含內嵌適用性表單的頁面取代為感謝頁面。 否則，感謝頁面會取代 [!UICONTROL 適用性Forms — 內嵌] 元件，而不會重新整理頁面的基礎網站。 只有在您選擇顯示感謝頁面時，才可使用此選項。
* **使用頁面語言**:使用AEM Sites頁面的本機區域設定，而非適用性表單。
* **將焦點置於表單上**:選取「 」，將焦點設定在最適化表單的第一個欄位上。
* **表單覆蓋框架的整個寬度**:如果勾選此選項，則不會使用iframe來轉譯表單。
* **高度**:指定容器的高度。 保留為空白以自動調整容器大小。
* **CSS用戶端程式庫**:指定CSS用戶端程式庫的路徑。

### 發佈內嵌適用性表單 {#publishing-embedded-adaptive-form}

在AEM網站頁面中發佈內嵌適用性表單時，請考量下列案例：

* 如果您是首次發佈AEM網站頁面，且其中包含內嵌的最適化表單，請發佈網站頁面和內嵌資產。
* 如果您只修改了已發佈網站頁面中的內嵌適用性表單，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的參考，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌適用性表單，請重新發佈網站頁面和內嵌資產。

### 修改內嵌適用性表單  {#modifying-embedded-adaptive-form}

要修改嵌入式適用性表單的任何配置或屬性，請執行以下操作之一。

* 在個別編輯器的適用性表單中開啟原始表單並加以修改。
* 以編輯模式從網站頁麵點選最適化表單，然後點選 **[!UICONTROL 在新視窗中編輯]**. 原始表單會以可修改的編輯模式開啟。

>[!NOTE]
>
>原始適用性表單中所做的變更會自動反映在內嵌表單中。 不過，重新發佈適用性表單或網站的頁面，以反映已發佈頁面中的變更。

### 最佳實務 {#best-practices}

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者草稿和提交內嵌表單，且可顯示在Forms Portal的「草稿」和「已提交Forms」標籤中。

[在AEM Sites頁面中，配置模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) 可讓您調整已在AEM網站頁面中建立或內嵌的適用性表單的大小。

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM網站頁面會維護最適化表單的參考。 翻譯AEM Sites頁面時，會使用 [翻譯專案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) 其他語言。

