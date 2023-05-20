---
title: 在AEM Sites頁中添加或建立自適應表單（核心元件）
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: 您可以在AEM Sites頁中使用自適應表單（核心元件）來填寫和提交表單，而無需離開AEM Sites頁。
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 1d5641dd07cc68dade247fe30bb57663872e5560
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 2%

---

# 使用AEM Sites編輯器建立或添加自適應表單 {#add-an-adaptive-form-to-aem-sites-page}

您可以無縫地在AEM Sites頁面中編寫或嵌入Adaptive Forms，以便您的用戶無需離開「站點」頁面即可填寫和提交表單。 它幫助用戶保持在網頁的其它元素的上下文中，並同時與表單交互。

您可以選擇以下方法之一來建立自適應表單或將自適應表單添加到AEM Sites頁：

* **使用自適應Forms容器元件建立自適應窗體**:的 [自適應窗體容器](#af-container-component) 元件允許您直接在AEM Sites編輯器中利用自適應Forms元件構建數字註冊體驗。 這一整合為希望在其AEM Sites頁面中建立和管理表單的AEM Sites作者提供了無縫體驗。

* **添加現有自適應表單**:的 [自適應Forms — 嵌入(v2)](#embed-existing-af) 元件允許您輕鬆地將預先存在的自適應表單添加到AEM Sites內的頁面中。 該特徵增強了自適應Forms的適應性和可重用性。 此整合為客戶重新使用他們已建立的自適應Forms提供了一種方便的方法。

* **使用自適應Forms嚮導建立表單**:使用 [自適應Forms — 嵌入(v2)](#embed-new-af) 元件，使用「建立表單」嚮導從AEM Sites編輯器中建立自適應表單。 窗體另存為外部實體。 您也可以在其他「站點」頁面和獨立表單中重複使用此表單。

* **在AEM Sites頁中添加多個自適應Forms**:要在AEM Sites頁中添加多個自適應Forms，請使用AEM Forms容器元件 —  [自適應Forms — 嵌入(v2)](#embed-new-af) 和 [自適應窗體容器](#af-container-component)。 在這種情況下，您需要在AEM Sites頁中將多個自適應表單作為div添加，您可以使用自適應表單容器元件。

可以使用規則編輯器添加或控制自適應表單元件的動態行為。 例如，隱藏或顯示元件。 規則編輯器不可用於非自適應表單元件。 因此，在使用AEM Forms集裝箱元件中的非自適應表單元件時，請使用您的勤勉。

## 使用自適應Forms容器元件建立自適應窗體 {#af-container-component}

的 [!UICONTROL 自適應窗體容器] 元件允許在AEM Sites編輯器中使用自適應Forms元件構建數字註冊體驗。 可以通過拖放表單元件來建立自適應表單。

### 必備條件 {#prerequisites-af-container}

+++ 啟用 **[!UICONTROL 自適應Forms集裝箱]** 元件。

啟用 [!UICONTROL 自適應Forms集裝箱] 的子模組，請執行以下步驟：

1. 轉到 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯模板]
1. 按一下 [!UICONTROL 策略] 的 **[!UICONTROL 自適應Forms集裝箱]**  複選框 **[原型AEM項目名稱]  — 自適應窗體**。
1. 按一下 **[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ 將AdaptiveForms客戶端庫包括到AEM Sites頁

要在AEM Sites頁中使用自適應Forms元件，請使用Archetype/Git儲存庫和部署管道將Customheaderlibs和Customfooterlibs客戶端庫包AEM括到AEM Sites頁。

1. 開啟 [AEM Forms原型或克隆的Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 在文本編輯器中。 例如，Visual Studio代碼。
1. 導覽至 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製的值 `sling:resourceSuperType`。 例如，值為 `core/wcm/components/page/v3/page`。

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似結構 `ui.apps/src/main/content/jcr_root/apps` 相同 `core/wcm/components/page/v3/page`。

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 添加 `customheaderlibs.html` 和 `customfooterlibs.html` 的子菜單。

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

   customfooterlibs.html用於JavaScript,customheaderlibs.html用於css。

1. [運行管線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署更改。

+++

### 使用自適應Forms容器元件建立自適應窗體 {#create-af-using-af-container}


使用 [!UICONTROL 自適應Forms集裝箱] 元件：

1. 以編輯模式開啟AEM Sites頁面。
1. 在「元件」瀏覽器面板中，拖放 **[!UICONTROL 自適應Forms集裝箱]** 元件。
1. 使用自適應Forms元件建立自適應窗體。
1. 保存設定。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

你的表格準備好了。 當您發佈AEM Sites頁面時，它會自動發佈自適應表單及其關聯的引用資產。

#### 配置自適應表單容器屬性 {#configure-additional-settings-container}

可以自定義 [!UICONTROL 自適應窗體容器] 元件。 例如，

* 您可以配置預填充服務，以在站點的頁面上載入具有預填充值的自適應表單。
* 可以配置「資料模型」設定，以將「自適應表單」與資料源關聯。
* 您可以配置提交操作，以便在提交表單時發送Microsoft® OneDrive、Microsoft® OneDrive或其他資料源上的資料。 您還可以為自適應Forms建立和選擇自定義提交操作。

設定 **[!UICONTROL 自適應Forms集裝箱]** 元件，按一下 ![設定表徵圖](/help/forms/assets/Smock_Wrench_18_N.svg) 按鈕。 的 **[!UICONTROL 編輯自適應Forms容器]** 對話框。

![編輯對話框](/help/forms/assets/adaptiveformcontainer-editdialog.png)

在 [!UICONTROL 編輯自適應Forms容器] 對話框，可以指定以下內容。
* **基本標籤**
   * **預填充服務**:可以使用預填充服務使用現有資料自動填充自適應表單的欄位。 當用戶開啟表單時，這些欄位的值將預先填充。 有關預填服務的資訊，請參見 [預填充自適應表單域](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **客戶端庫類別**:指定 [JavaScript函式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 在表達式中使用且受Adaptive Forms支援。
* **資料模型**:資料模型允許您將不同資料源中的實體和服務整合到自適應表單。 選擇 **[!UICONTROL 窗體資料模型]** 如果要建立的自適應表單涉及從多個資料源讀取資料和將資料寫入多個資料源。
   * **窗體資料模型**:表單資料模型允許自適應表單與不同的資料源通信。 有關配置資料源的資訊，請參見 [配置資料源。](/help/forms/configure-data-sources.md)
   * **架構**:架構表示組織中後端系統生成或使用資料的結構。 你可以 [將模式與自適應表單關聯](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) 並使用其元素將動態內容添加到自適應表單。

      >[!NOTE]
      >
      > 配置表單資料模型後，無法更改關聯的表單模型。 但是，可以修改與表單資料模型關聯的架構。

* **提交頁籤**

   * **重新導向至 URL**
      * **重定向URL/路徑**:指定在提交後自適應表單重定向到的URL或路徑。

      * **提交操作**:當用戶按一下自適應表單上的「提交」按鈕時，將觸發提交操作。 你可以 [在Adaptive Form上配置提交操作](/help/forms/configuring-submit-actions.md)。 自適應表單提供了以下現成的提交操作：
         * 提交到REST終結點
         * 傳送電子郵件
         * 使用表單資料模型提交
         * 調用工AEM作流
         * 提交至 SharePoint
         * 提交至 OneDrive
         * 提交到 Azure Blob 儲存體

   您也可以 [擴展預設提交操作](custom-submit-action-form.md) 建立您自己的自定義提交操作。

* **顯示訊息**
   * **消息內容**:使用富格文本編輯器編寫消息，以便在提交表單時顯示。 此選項僅在您選擇顯示感謝信時可用。

## 嵌入自適應表單  {#aem-container-component}

使用 **[!UICONTROL 自適應Forms — 嵌入(V2)]** 元件，您可以在網站的頁面中嵌入新的Adaptive Form，或嵌入現有的Adaptive Form。 的 [!UICONTROL 自適應Forms — 嵌入(v2)] 元件允許您：

* [添加現有自適應表單](#embed-new-af)

* [建立並添加新的自適應表單](#embed-existing-af)

### 必備條件 {#prerequisites}

+++ 啟用 **自適應Forms — 嵌入** 元件。

啟用 [!UICONTROL 自適應Forms — 嵌入(v2)] 的子模組，請執行以下步驟：

1. 轉到 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯模板]

1. 按一下 [!UICONTROL 策略] 的 **[!UICONTROL 自適應表單 — 嵌入(v2)]** 複選框 **[!UICONTROL [原型AEM項目名稱] -Forms]** 組
1. 按一下 **[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ 將AdaptiveForms客戶端庫包括到AEM Sites頁

當 **[!UICONTROL 當表單覆蓋頁面的整個寬度時]** 的子菜單。 **[!UICONTROL 窗體容器]** 配置對話框和 **使用核心元件的自適應Forms** ，則必須在相應站點的頁面上包含客戶端。

![覆蓋Gif](/help/forms/assets/overlaycorecomponent.gif)

要在AEM Sites頁中使用自適應Forms元件，請包括 `Customheaderlibs` 和 `Customfooterlibs` 使用Archetype/Git儲存庫和部AEM署管道將客戶端庫連接到AEM Sites頁。

1. 開啟 [AEM Forms原型或克隆的Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 在文本編輯器中。 例如，Visual Studio代碼。
1. 導覽至 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製的值 `sling:resourceSuperType`。 例如，值為 `core/wcm/components/page/v3/page`。

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似結構 `ui.apps/src/main/content/jcr_root/apps` 相同 `core/wcm/components/page/v3/page`。

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 添加 `customheaderlibs.html` 和 `customfooterlibs.html` 的子菜單。

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

   的 `customfooterlibs.html` 用於JavaScript和 `customheaderlibs.html` 的下界。

1. [運行管線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署更改。

+++

### 將現有的自適應表單添加到AEM Sites頁 {#embed-existing-af}

1. 以編輯模式開啟AEM Sites頁面。
1. 在「元件」瀏覽器面板中，拖放 [!UICONTROL 自適應Forms — 嵌入] 元件。
1. 點擊 [!UICONTROL 自適應Forms — 嵌入] 「站點」頁中的元件，然後點擊 ![設定表徵圖](/help/forms/assets/Smock_Wrench_18_N.svg) 按鈕。 的 **[!UICONTROL 編輯自適應Forms — 嵌入]** 對話框。
1. 瀏覽並選擇要嵌入到 [!UICONTROL 資產路徑]。
1. 保存設定。 「自適應表單」現在嵌入到頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### 建立並將新的自適應表單添加到AEM Sites頁 {#embed-new-af}

1. 以編輯模式開啟AEM Sites頁面。
1. 在「元件」瀏覽器面板中，拖放 [!UICONTROL 自適應Forms — 嵌入(v2)] 元件。
1. 按一下 **加** 表徵圖，您將被重定向到窗體建立嚮導。

   ![自適應Forms — 嵌入元件](/help/forms/assets/aemformcontainer.png)

1. 從 [!UICONTROL 窗體建立] 的子菜單。
1. 的 [!UICONTROL 資產路徑] 已包括已建立的自適應表單的路徑
1. 保存設定。 「自適應表單」現在嵌入到頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### 配置自適應表單 — 嵌入(v2)屬性 {#configure-adaptive-form-embed}

可以自定義 [!UICONTROL 自適應表單 — 嵌入(v2)] 元件。 在 [!UICONTROL 編輯自適應Forms — 嵌入(v2)] 對話框，可以指定以下內容。

* **資產路徑**:瀏覽並選擇要嵌入的自適應表單。 如果從「資產」瀏覽器中刪除它，則會自動填充它。
* **提交後** :選擇要在表單提交時觸發的操作。 您可以選擇顯示感謝信或感謝頁。
   * **顯示感謝信**:使用富格文本編輯器編寫消息，以便在提交表單時顯示。 此選項僅在您選擇顯示感謝信時可用。
   * **顯示「感謝」頁**:瀏覽並選擇要在表單提交時顯示的頁面。 此選項僅在您選擇顯示感謝頁時可用。
   * **重定向至「感謝」頁**:啟用此選項可將包含嵌入式自適應表單的頁面替換為感謝頁。 否則，感謝頁將替換 [!UICONTROL 自適應Forms — 嵌入] 元件，而不刷新頁面的基礎站點。 此選項僅在您選擇顯示感謝頁時可用。
* **使用頁面語言**:使用AEM Sites頁的本地語言環境，而不是自適應窗體。
* **將焦點設定在窗體上**:選擇以在「自適應表單」的第一個欄位上設定焦點。
* **窗體覆蓋框架的整個寬度**:如果選中，則不使用iframe來呈現表單。
* **高度**:指定容器的高度。 將其留空，以自動調整容器大小。
* **CSS客戶端庫**:指定CSS客戶端庫的路徑。

### 使用Adaptive Form - Embed(v2)元件發佈添加的自適應Forms  {#publish-embedded-adaptive-form}

請考慮以下方案，使用 **[!UICONTROL 自適應表單 — 嵌入(v2)]** 元件：

* 首次發佈AEM Sites頁面時，添加到「站點」頁面的表單將自動發佈。
* 修改添加到已發佈的「站點」頁面的自適應表單時，請手動發佈相應的自適應Forms。
* 修改「站點」頁面和相應的「自適應Forms」時，重新發佈「站點」頁面和添加到「站點」頁面的所有「自適應Forms」。

### 使用Adaptive Form - Embed(v2)元件修改添加的自適應Forms  {#modifying-embedded-adaptive-form}

要修改自適應表單的任何配置或屬性，請執行以下操作之一：

* 在相應編輯器的「自適應表單」中開啟原始表單並修改它們。
* 在編輯模式下從網站頁中按一下「Adaptive Form（自適應表單）」 ，然後按一下 **[!UICONTROL 在新窗口中編輯]**。 原始窗體在可修改的編輯模式下開啟。

## 更改添加到AEM Sites頁的自適應表單的佈局 {#change-layout-af-aem-sites-page}

在AEM Sites版 [佈局模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) 允許您調整建立或添加到AEM Sites頁面的自適應表單的大小。

![AF佈局支援](/help/forms/assets/afsite-layoutsupport.gif)

「站AEM點」頁維護對「自適應表單」的引用。 當您翻譯AEM Sites頁面時，它會使用 [翻譯項目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) 換成其他語言。

## 最佳做法 {#best-practices}

* 原始表單中的頁眉和頁腳不包括在嵌入表單中。
* 在Forms門戶的「草稿」和「已提交的Forms」頁籤中，支援和可以看到嵌入表單的用戶草稿和提交。