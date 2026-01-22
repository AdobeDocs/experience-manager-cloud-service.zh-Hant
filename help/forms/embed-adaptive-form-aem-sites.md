---
title: 如何將最適化表單新增至AEM Sites頁面？
description: 將Adaptive Forms順暢地內嵌於AEM Sites頁面或AEM外部託管的網頁中。
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: bc9fa030aeab4f2dddafc2241fade7b5d0689926
workflow-type: tm+mt
source-wordcount: '3296'
ht-degree: 5%

---

# 將最適化表單內嵌至AEM網站頁面 {#embed-an-adaptive-form-to-aem-sites-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service  | 本文章 |


## 概觀 {#overview}

AEM Forms可讓表單開發人員順暢地將最適化Forms內嵌在AEM Sites頁面或AEM外部託管的網頁中。 內嵌的最適化表單功能齊全，使用者無須離開頁面即可填寫並提交表單。 它有助於使用者停留在網頁上其他元素的內容中，同時與表單互動。 這可讓您的使用者方便地填寫和提交表單，永遠不需要離開他們所在的頁面。 此整合提供一種便利的方法，可重複使用他們已建立的最適化Forms。

您可以使用AEM頁面編輯器快速將多個表單內嵌到您的AEM Sites頁面。 使用AEM頁面編輯器，內容作者就能利用最適化Forms元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面內建立順暢的資料擷取體驗。 它也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

AEM Forms提供&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;和&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;元件。 您可以使用&#x200B;**[!UICONTROL Adaptive Forms - Embed(v2)]**&#x200B;元件新增現有的Adaptive Form或使用Adaptive Forms編輯器建立表單，同時使用&#x200B;**[!UICONTROL Adaptive Form容器]**&#x200B;在Experience Fragment或AEM Sites頁面中建立新表單。

![AEM Sites頁面中的最適化表單範例](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integrating-adobe-target.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## 如何在AEM Sites頁面或AEM體驗片段中建立或內嵌最適化表單？ {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

您可以使用以下選項來充分利用此功能：

* **[使用核准的範本建立最適化表單，並將其內嵌到AEM Sites頁面](#embed-form-using-adaptive-form-wizzard-aem-sites)：**&#x200B;您可以使用預先核准的範本，快速建立並內嵌符合您組織品牌方針和設計標準的最適化Forms。

* **[將現有表單內嵌至AEM Sites頁面](#embed-an-adaptive-form-in-sites-editor)：**&#x200B;您可以輕鬆將已建立的表單整合至您的網站，讓訪客直接與表單互動。

* **[將內嵌的最適化表單轉換為體驗片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)：**&#x200B;將新增至AEM Sites頁面的內嵌的最適化表單轉換為體驗片段，以便在多個AEM Sites頁面上重複使用表單。

* **[建立自訂最適化表單並新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment)：**&#x200B;您可以使用&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;元件，從頭開始建立全新的表單，根據您的需求和設計偏好設定量身打造。

* **[建立自訂最適化表單並新增至體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor)：**&#x200B;您可以透過將表單新增至AEM體驗片段來延伸表單的觸及，以便在多個頁面或網站之間無縫重複使用。

* **將多個表單新增至AEM Sites頁面或體驗片段：**&#x200B;您可以建立多個最適化Forms或將多個最適化表單新增至AEM Sites頁面，以根據使用者的偏好和需求為其提供多個選擇。 您可以使用AEM頁面編輯器快速將多個表單內嵌到您的AEM Sites頁面。 您可以多次使用&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;元件，以在AEM Sites頁面中新增最適化Forms。 您必須選取&#x200B;**[!UICONTROL Form涵蓋影格的整個寬度]**&#x200B;選項，才能在AEM Sites頁面中多次使用&#x200B;**[!UICONTROL Adaptive Forms - Embed]**&#x200B;元件。 如果未核取&#x200B;**[!UICONTROL 表單涵蓋影格]**&#x200B;的整個寬度，AEM Sites頁面僅支援一個不含iframe的最適化表單存在。 若要使用&#x200B;**[!UICONTROL 最適化Forms — 內嵌]**&#x200B;元件新增更多最適化Forms，請選取&#x200B;**[!UICONTROL 表單涵蓋影格整個寬度]**&#x200B;選項。

## 將最適化表單嵌入到AEM Sites頁面或AEM體驗片段的考量事項 {#consideration}

* 當您使用&#x200B;**[!UICONTROL 最適化Forms - Embed(v2)]**&#x200B;元件建立或新增表單時，表單會使用AEM Forms翻譯流程進行翻譯和本地化。 在這種情況下，Sites 頁面的所有語言副本中會維持和引用單一表單。 **[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;元件不提供對AEM Sites頁面的各種功能的存取權，例如，版本設定、目標定位、翻譯和多網站管理員。

* 當您使用&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;建立表單時，表單會透過AEM Sites翻譯流程進行翻譯和本地化。 對於每種語言，系統會產生網站頁面和相應表單的個別副本 (語言副本)，當內容作者在父頁面表單中修訂規則時，表單的所有語言副本必須進行相同的變更。 **[!UICONTROL 最適化表單容器]**&#x200B;也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。


## 在AEM Sites頁面或AEM體驗片段中內嵌最適化表單的需求 {#before-you-start-embedding-an-adaptive-form}

開始使用&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;內嵌新的最適化表單或現有的最適化表單之前，請啟用&#x200B;**最適化Forms核心元件**&#x200B;並將&#x200B;**最適化Forms使用者端資料庫**&#x200B;新增到AEM Sites頁面：

<!--### Enable Adaptive Forms Core Components for your AEM Cloud Service environment

Install the latest far to enable Adaptive Forms Core Components for your AEM Cloud Service environment.-->

### 新增Adaptive Forms使用者端資料庫至您的AEM Sites頁面或體驗片段

在&#x200B;**[!UICONTROL 表單容器]**&#x200B;設定對話方塊中選取&#x200B;**[!UICONTROL 當表單涵蓋整個頁面寬度]**&#x200B;選項，並使用使用核心元件的調適型Forms時，必須在您對應的網站頁面上包含使用者端資料庫。

![當選取表單涵蓋整個頁面寬度選項，且使用具有核心元件的最適化表單時](/help/forms/assets/overlaycorecomponent.gif)

**案例1：使用個別網站頁面元件**

使用部署管道將&#x200B;**Customheaderlibs**&#x200B;和&#x200B;**Customfooterlibs**&#x200B;使用者端資料庫新增到您的AEM Sites頁面。 若要新增使用者端程式庫：

1. 存取並原地複製您的 [AEM Cloud Service Git 存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html)。
2. 在純文字編輯器中開啟 AEM Cloud Service Git 存放庫資料夾。 例如，Microsoft® Visual Code。
3. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

4. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

5. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

6. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

7. [執行部署管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html)，將客戶端資料庫部署到您的 AEM as a Cloud Service 環境。

>[!NOTE]
>
> 只有在所有表單都需要自訂函式使用者端程式庫時，才對該程式庫進行硬式編碼。 針對因表單型別而異的程式庫，請透過範本頁面原則將其新增，如下節所述。

**案例2：使用相同的Sites頁面元件**

在用來建立含有表單之頁面的範本的頁面原則中，包含執行階段使用者端程式庫或自訂函式程式庫。

1. 開啟AEM Sites頁面或體驗片段進行編輯。 若要開啟頁面進行編輯，請選取頁面，然後按一下[編輯]。****
2. 開啟網站或體驗片段頁面的範本。 若要開啟範本，前往&#x200B;**[!UICONTROL 頁面資訊]** ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg)>**[!UICONTROL 編輯範本]**。 它會在範本編輯器中開啟對應的範本。
3. 移至範本的&#x200B;**[!UICONTROL 頁面資訊]** ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg)區段，並選取&#x200B;**[!UICONTROL 頁面原則]**&#x200B;選項。 這會開啟AEM Sites範本的屬性，您可在此定義自訂函式或執行階段使用者端程式庫。
4. 按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;索引標籤中的&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，以新增自訂函式庫或執行階段程式庫。
5. 按一下&#x200B;**[完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### 啟用最適化Forms — 為您的AEM Sites頁面或體驗片段內嵌(v2)

若要在範本的原則中啟用&#x200B;**[!UICONTROL Adaptive Forms - Embed(v2)]**&#x200B;元件，請執行下列步驟：

1. 開啟AEM Sites頁面或體驗片段進行編輯。 若要開啟頁面進行編輯，請選取頁面，然後按一下[編輯]。****
1. 開啟網站或體驗片段頁面的範本。 若要開啟範本，前往&#x200B;**[!UICONTROL 頁面資訊]** ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg)>**[!UICONTROL 編輯範本]**。 它會在範本編輯器中開啟對應的範本。
1. 在「結構」視圖中，在選單列中按一下&#x200B;**[!UICONTROL 「原則」]**![「原則」](/help/forms/assets/Smock_FeedManagement_18_N.svg)圖示。 在&#x200B;**[!UICONTROL 允許的元件]**&#x200B;清單中，選取&#x200B;**[!UICONTROL AEM原型專案名稱]** — 最適化表單&#x200B;**[下的]最適化Forms — 內嵌(v2)**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

## 使用最適化Forms - Embed(v2)元件內嵌最適化表單 {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

使用&#x200B;**[!UICONTROL 最適化Forms - Embed(v2)]**&#x200B;元件，使用表單建立精靈直接在AEM Sites編輯器中建立最適化表單。 產生的表單會儲存為外部實體，以供在其他Sites頁面和獨立表單中重複使用。 您可以直接在AEM Sites頁面或體驗片段中，從頭開始內嵌全新的表單，根據您的需求和設計偏好設定進行量身打造。 對於單次使用的表單，建議直接編寫到AEM Sites頁面，而體驗片段則適用於必須在您網站上的多個頁面中重複使用的表單。

您可以使用&#x200B;**[!UICONTROL 最適化Forms - Embed(v2)]**&#x200B;輕鬆內嵌新表單。  例如，想像將新的聯絡人表單合併到AEM Sites頁面或AEM體驗片段中。 對AEM Sites頁面或體驗片段中的連絡人表單所做的任何更新或修改都會自動套用至部署該表單的所有頁面。 這可簡化網站表單的管理，確保順暢的使用者體驗，同時簡化整體程式。

使用&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**，您可以：

* [在AEM Sites頁面中使用「最適化Forms精靈」內嵌新表單](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [在體驗片段中使用Adaptive Forms精靈嵌入新表單](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [將現有的最適化表單內嵌到AEM Sites頁面中](#embed-an-adaptive-form-in-sites-editor)
* [將現有表單嵌入體驗片段中](#embed-an-adaptive-form-in-experience-fragment)
* [將AEM Sites頁面中的最適化表單轉換為體驗片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### 在AEM Sites頁面中使用「最適化Forms精靈」內嵌新表單 {#embed-form-using-adaptive-form-wizzard-aem-sites}

將新表單內嵌至AEM Sites頁面的步驟如下：

1. 在編輯模式中開啟 AEM Sites 頁面。
1. 從元件瀏覽器面板中，將&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;元件拖放到頁面上。
1. 按一下&#x200B;**加號**&#x200B;圖示，系統會將您重新導向表單建立精靈。

   ![最適化Forms — 內嵌元件](/help/forms/assets/aemformcontainer.png)

1. 從&#x200B;**[!UICONTROL 表單建立]**精靈建立新的最適化表單。
**[!UICONTROL 資產路徑]**&#x200B;已包含已建立的最適化表單的路徑
1. 儲存設定。 最適化表單現在內嵌在頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

接下來，您可以使用表單建立精靈[設定提交動作](/help/forms/configuring-submit-actions.md)和內嵌式最適化表單的進階屬性。


### 在體驗片段中使用Adaptive Forms精靈嵌入新表單 {#embed-form-using-adaptive-form-wizzard-experience-fragment}

將新表單內嵌至體驗片段的步驟如下：

1. 在編輯模式中開啟體驗片段。
1. 從元件瀏覽器面板中，將&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;元件拖放到頁面上。
1. 按一下&#x200B;**加號**&#x200B;圖示，系統會將您重新導向表單建立精靈。

   ![最適化Forms — 內嵌元件](/help/forms/assets/aemformcontainer.png)

1. 從&#x200B;**[!UICONTROL 表單建立]**精靈建立新的最適化表單。
**[!UICONTROL 資產路徑]**&#x200B;已包含已建立的最適化表單的路徑
1. 儲存設定。 最適化表單現在內嵌在體驗片段中。

接下來，您可以使用表單建立精靈[設定提交動作](/help/forms/configuring-submit-actions.md)和內嵌式最適化表單的進階屬性。

### 將現有的最適化表單內嵌到AEM Sites頁面中 {#embed-an-adaptive-form-in-sites-editor}

透過&#x200B;**[!UICONTROL 最適化Forms - Embed(v2)]**&#x200B;元件，您可以輕鬆將既存的最適化表單整合到AEM Sites內的頁面中。 此功能大幅增強最適化Forms的適應性和可重複使用性，為客戶提供重複使用他們已建立之表單的便利方式。 例如，想像將連絡人表單合併到AEM Sites頁面，而不需要多次重新建立表單。

若要將現有的最適化表單內嵌在網站頁面中：

1. 在編輯模式中開啟 AEM Sites 頁面。
1. 將&#x200B;**[!UICONTROL Adaptive Forms - Embed(v2)]**&#x200B;元件從元件瀏覽器拖放至Sites頁面。
1. 在Sites頁面中選取&#x200B;**[!UICONTROL Adaptive Forms - Embed]**&#x200B;元件，然後在動作列上選取![Adaptive Form Container屬性](/help/forms/assets/configure-icon.svg)。 **[!UICONTROL 編輯最適化Forms — 內嵌(v2)]**&#x200B;對話方塊開啟。
1. 瀏覽並選取最適化表單，以內嵌於&#x200B;**[!UICONTROL 資產路徑]**。
1. 儲存設定。 最適化表單現在內嵌在頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

接下來，您可以使用表單建立精靈[設定提交動作](/help/forms/configuring-submit-actions.md)和內嵌式最適化表單的進階屬性。

### 將現有的最適化表單嵌入體驗片段中 {#embed-an-adaptive-form-in-experience-fragment}

您也可以將表單內嵌至AEM體驗片段，以擴充表單的協助工具。 若要將最適化表單嵌入體驗片段：

1. 在編輯模式中開啟體驗片段。
1. 將&#x200B;**[!UICONTROL Adaptive Forms - Embed(v2)]**&#x200B;元件從元件瀏覽器拖放至體驗片段。
1. 選取體驗片段中的&#x200B;**[!UICONTROL Adaptive Forms - Embed]**&#x200B;元件，然後在動作列上選取![Adaptive Form Container屬性](/help/forms/assets/configure-icon.svg)。 **[!UICONTROL 編輯最適化Forms — 內嵌(v2)]**&#x200B;對話方塊開啟。
1. 瀏覽並選取最適化表單，以內嵌於&#x200B;**[!UICONTROL 資產路徑]**。
1. 儲存設定。 最適化表單現在內嵌於體驗片段中。

接下來，您可以使用表單建立精靈[設定提交動作](/help/forms/configuring-submit-actions.md)和內嵌式最適化表單的進階屬性。

### 將AEM Sites頁面中的表單轉換為體驗片段 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

您可以將網站頁面編輯器中的現有最適化表單轉換為體驗片段，以跨多個頁面或網站重複使用表單。

若要將AEM Sites頁面中的最適化表單轉換為體驗片段：

1. 在編輯模式中開啟包含調適型表單的AEM Sites頁面(在調適型Forms容器元件中)。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 在功能表列上，選取![轉換成體驗片段變數圖示](/help/forms/assets/Smock_FilingCabinet_18_N.svg)轉換成體驗片段變數圖示。

   ![按一下檔案封包標誌，將AEM Sites頁面中的最適化表單轉換為體驗片段](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   會出現對話方塊，將最適化表單容器轉換為新的體驗片段或新增到現有的體驗片段。

1. 在&#x200B;**[!UICONTROL 轉換成體驗片段]**&#x200B;變化對話方塊中，設定下列選項的值：

   * **動作：**&#x200B;選取以建立體驗片段或新增至現有的體驗片段。
   * **父路徑：**&#x200B;指定承載體驗片段的資料夾路徑。 選項僅適用於建立新的體驗片段。
   * **範本：**&#x200B;指定體驗片段範本的路徑。 如果您沒有體驗片段範本，請[建立它](/help/implementing/developing/extending/experience-fragments.md)。 該選項僅可用於將最適化表單新增到現有的體驗片段。
   * **片段標題：**&#x200B;指定體驗片段的標題。 標題可唯一識別體驗片段。
   * **片段標籤：**&#x200B;指定體驗片段的標籤。 標籤可唯一識別體驗片段的類別。

## 設定最適化表單內嵌(v2)屬性

您可以自訂&#x200B;**[!UICONTROL 最適化表單 — 內嵌(v2)]**&#x200B;元件的進階設定。 在「**[!UICONTROL 編輯最適化Forms — 內嵌]**」對話方塊中，您可以指定下列專案：

* **資產路徑**：瀏覽並選取要內嵌的最適化表單。 如果您從Assets瀏覽器中將其刪除，則會自動填入。
* **發佈提交** ：選取要在提交表單時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。
   * **顯示感謝訊息**：使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有當您選擇顯示感謝訊息時，才能使用此選項。
   * **顯示感謝頁面**：瀏覽並選取要在表單提交時顯示的頁面。 只有當您選擇顯示感謝頁面時，才能使用此選項。
   * **重新導向以感謝您的頁面**：啟用選項，以感謝頁面取代包含內嵌最適化表單的頁面。 否則，感謝頁面會取代&#x200B;**[!UICONTROL 最適化Forms — 內嵌(v2)]**&#x200B;元件中的最適化表單，而不會重新整理頁面上的基礎網站。 只有當您選擇顯示感謝頁面時，才能使用此選項。
   * **感謝訊息**：成功提交表單後，熒幕上會顯示簡短的確認或確認。
   * **感謝頁面**：瀏覽並選取成功提交表單後要顯示的頁面。

* **使用頁面語言**：使用AEM Sites頁面的本機，而非最適化表單的區域設定。 此選項僅適用於最適化表單(Foundation)。
* **將焦點設定在表單**：選取此選項可將焦點設定在調適型表單的第一個欄位。 此選項僅適用於最適化表單(Foundation)。
* **佈景主題**：選取定義最適化表單元件樣式的主題。 樣式包含外觀屬性，例如字型樣式、背景顏色、尺寸和對齊。 此選項僅適用於最適化表單(Foundation)。

  >[!NOTE]
  >
  > 您只能針對最適化表單(Foundation)使用&#x200B;**使用頁面語言**、**設定表單**&#x200B;和&#x200B;**主題**&#x200B;選項。

* **表單涵蓋影格的整個寬度**：
內嵌框架(iframe)是HTML元素，可將最適化表單載入AEM Sites頁面。

   * 如果勾選&#x200B;**[!UICONTROL 表單涵蓋影格]**&#x200B;的整個寬度，則最適化表單會佔據其所在容器的整個寬度。 在此情況下，不會使用iframe來呈現表單。 最適化表單的版面配置和設計可適應容器的整個寬度，使其回應速度更快，並能夠調整到不同的熒幕大小。 此選項可讓您將多個最適化Forms內嵌在AEM Sites頁面中。

     >[!NOTE]
     >
     > 若要在AEM Sites頁面中內嵌多個表單，請選取「**[!UICONTROL 表單涵蓋影格的整個寬度]**」核取方塊。

   * 如果未核取&#x200B;**[!UICONTROL 表單涵蓋影格]**&#x200B;的整個寬度，則最適化表單不會涵蓋容器的整個寬度。 而是使用iframe來呈現表單，其不可延伸超過特定寬度。 當最適化表單具有明確的邊界，且必須在容器內與其旁的其他AEM元件共存時，此方法就相當實用。 如果未核取此選項，則僅允許在AEM Sites頁面中嵌入一個不含iframe的最適化Forms。

     >[!NOTE]
     >
     > AEM Sites頁面僅支援一個不含iframe的最適化表單。 若要使用&#x200B;**[!UICONTROL 最適化Forms — 內嵌]**&#x200B;元件新增更多最適化Forms，請選取&#x200B;**[!UICONTROL 表單涵蓋影格整個寬度]**&#x200B;選項。

* **高度**：指定容器的高度。 保留空白以自動調整容器大小。
* **CSS使用者端資料庫**：指定CSS使用者端資料庫的路徑。

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## 發佈內嵌式最適化表單 {#publishing-embedded-adaptive-form}

讓我們考慮下列在AEM網站頁面中發佈內嵌式最適化表單的情況：

* 如果您是第一次發佈AEM網站頁面，且其中包含內嵌的最適化表單，請發佈網站頁面和內嵌資產。
* 如果您只修改已發佈網站頁面中內嵌的最適化表單，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的引用，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌的最適化表單，請重新發佈網站頁面和內嵌資產。

## 修改內嵌的最適化表單  {#modifying-embedded-adaptive-form}

若要修改內嵌調適型表單的任何設定或屬性，請執行下列任一項作業。

* 在個別編輯器中以最適化表單開啟原始表單，並加以修改。
* 在編輯模式中，從網站頁面內選取最適化表單，然後在新視窗中選取&#x200B;**[!UICONTROL 編輯]**。 原始表單會以您可以修改的編輯模式開啟。

>[!NOTE]
>
>在原始最適化表單中所做的變更會自動反映在內嵌表單中。 不過，請重新發佈最適化表單或網站頁面，以反映已發佈頁面中的變更。

## 最佳做法 {#best-practices}

在AEM網站頁面中內嵌最適化Forms時，請記住下列幾點：

* 內嵌表單中不包含原始表單的頁首和頁尾。
* 使用者草稿和提交內嵌表單受到支援，並可在Forms Portal的草稿和已提交的Forms標籤中看到。
* 在原始表單上設定的提交動作會保留在內嵌表單中。
* 如果您已針對原始表單設定Adobe Analytics，則會在Adobe Analytics中擷取內嵌表單的分析資料。 但是，它不會出現在Forms Analytics報告中。

## 另請參閱 {#see-also}

* [建立以核心元件為基礎的獨立最適化Forms](/help/forms/creating-adaptive-form-core-components.md)
* [直接在AEM Sites頁面中建立以核心元件為基礎的最適化表單](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
