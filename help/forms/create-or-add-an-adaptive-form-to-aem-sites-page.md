---
title: 如何將最適化表單新增至AEM Sites頁面？
description: 瞭解如何建立最適化表單或將其新增到您的AEM Sites頁面。 也瞭解將表單整合至您網站的好處和各種方式。
feature: Adaptive Forms, Foundation Components
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
role: User, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '3162'
ht-degree: 18%

---

# 新增自適應表單至 AEM Sites 頁面或體驗片段 {#create-or-add-an-adaptive-form-to-aem-sites-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |
| AEM as a Cloud Service  | 本文章 |

## 概觀 {#overview}

透過AEM Forms，您可以順暢地新增表單至AEM Sites頁面。 這可讓您的訪客方便填寫和提交表單，而無需離開他們所在的頁面。 這麼，他們便可毫不費力地使用網站的其他元素，同時積極與表單進行互動。

您可以使用AEM頁面編輯器快速建立多個表單並新增到您的AEM Sites頁面。 使用AEM頁面編輯器，內容作者就能利用調適型表單元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面內建立順暢的資料擷取體驗。 它也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

AEM Forms Cloud Service提供最適化表單容器和Adaptive Forms — 內嵌元件。 您可以使用調適型表單容器在AEM Sites頁面或體驗片段中建立表單，而調適型Forms — 內嵌元件可讓您新增現有的調適型表單或使用調適型Forms編輯器建立表單。

![AEM Sites頁面中的最適化表單範例](/help/forms/assets/adaptive-form-in-sites-page.png)

## 為何要使用最適化Forms核心元件在AEM Sites頁面或體驗片段中建立最適化表單？

如果您過去曾為網站建立最適化Forms基礎元件或純HTML型表單，Adobe建議您使用最適化Forms核心元件在AEM Sites頁面或體驗片段中建立最適化表單。 它可讓您使用AEM Sites頁面的各種功能，例如、版本設定、目標定位、翻譯和多網站管理員，增強最適化Forms的整體表單建立和管理體驗。 讓我們來探索其中的部分功能：

* **版本設定：** AEM Sites頁面提供[強大的版本設定功能](/help/sites-cloud/authoring/sites-console/page-versions.md)，可讓您追蹤和管理不同版本的表單。 這可讓您變更和增強表單，同時維持必要時回覆至先前版本的能力。 版本設定可確保採用受控且有條理的方式來形成開發和演化。
* **鎖定目標(與Adobe Target整合)：**&#x200B;透過AEM Sites頁面鎖定目標功能，您也可以[為不同的對象，個人化表單體驗](/help/sites-cloud/integrating/integrating-adobe-target.md)。 透過使用使用者區段和目標定位條件，您可以針對特定使用者群組量身打造表單的內容、設計或行為。 這可讓您提供個人化和相關的表單體驗，提高參與度和轉換率。
* **翻譯：** AEM Sites [與翻譯服務緊密整合](/help/sites-cloud/administering/translation/overview.md)，讓您輕鬆將表單翻譯成多種語言。 此功能可簡化本地化程式，確保全球受眾可存取您的表單。 您可以在AEM翻譯專案中有效率地管理翻譯，減少支援多語言表單所需的時間和精力。 如需翻譯的詳細資訊，請參閱考量事項一節。
* **多網站管理和即時副本：** AEM Sites提供強大的[多網站管理和即時副本功能](/help/sites-cloud/administering/msm/overview.md)，讓您在單一環境中建立和管理多個網站。 此功能現在可讓您跨不同網站重複使用表單，確保一致性並減少重複工作。 透過集中化控制及管理，您可以有效維護及更新多個網站的表單。
* **佈景主題：** AEM Sites頁面提供框架，可跨多個網頁設計和維護一致的視覺樣式。 這些會定義顏色、字型、樣式表及其他視覺元素，這些元素有助於網站的整體外觀和風格。 [您可以使用為最適化表單的AEM Sites頁面設計的主題，以節省時間和精力](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes)。
* **標籤：** AEM Sites頁面可讓您[將標籤或標籤指派給頁面、資產或其他內容](/help/implementing/developing/introduction/tagging-framework.md)。 標籤是關鍵字或中繼資料標籤，提供根據特定條件分類及組織內容的方式。 您可以指派一或多個標籤給AEM中的頁面、資產或任何其他內容專案，以改善搜尋並將資產分類。
* **鎖定和解鎖內容：** AEM Sites可讓使用者[控制AEM Sites環境中對頁面](/help/sites-cloud/authoring/page-editor/edit-content.md)的存取與修改。 頁面鎖定時，即表示頁面可免受其他使用者未經授權的變更或編輯作業。 只有已鎖定內容的使用者或指定的管理員可以解除鎖定內容以允許修改。

此外，AEM頁面編輯器中的最適化Forms使用[最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features)。 這些核心元件提供標準且更簡單的方法來樣式化和自訂元件，與[AEM Sites WCM元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)相同。


## 如何在AEM Sites頁面或AEM體驗片段中建立或新增最適化表單？ {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

您可以通過使用以下選項來充分利用此功能：

* **[建立自訂最適化表單並新增至AEM Sites頁面](#create-an-adaptive-form-in-sites-editor-or-experience-fragment)：**&#x200B;您可以使用最適化表單容器元件，從頭開始建立全新的表單，根據您的需求和設計偏好設定量身打造。

* **[建立自訂最適化表單並新增至體驗片段](#create-an-adaptive-form-in-sites-editor)：**&#x200B;您可以透過將表單新增至AEM體驗片段來延伸表單的觸及，以便在多個頁面或網站之間無縫重複使用。

* **[將最適化表單轉換為體驗片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)：**&#x200B;將新增至AEM Sites頁面的最適化表單轉換為體驗片段，以便在多個AEM Sites頁面中重複使用表單。

* **[根據核准的範本建立表單並新增至AEM Sites頁面：](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)**&#x200B;您可以使用預先核准的範本，快速建立符合您組織品牌方針和設計標準的調適型Forms。 此選項僅適用於以最適化Forms編輯器或Adaptive Forms — 內嵌元件建立的最適化Forms 。

* **[將現有表單新增至AEM Sites頁面：](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)**&#x200B;您可以輕鬆將已建立的表單整合至您的網站，讓訪客直接與表單互動。 此選項僅適用於以最適化Forms編輯器或Adaptive Forms — 內嵌元件建立的最適化Forms 。


* **將多個表單新增至AEM Sites頁面或體驗片段：**&#x200B;您可以建立多個最適化Forms或將多個最適化表單新增至AEM Sites頁面，以根據使用者的偏好和需求為其提供多個選擇。 這些可以是全新表單和現有表單的組合。 您可以多次使用&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;元件，以在AEM Sites頁面中新增最適化Forms。 您必須選取&#x200B;**[!UICONTROL Form涵蓋影格的整個寬度]**&#x200B;選項，才能在AEM Sites頁面中多次使用&#x200B;**[!UICONTROL Adaptive Forms - Embed]**&#x200B;元件。 如果未核取&#x200B;**[!UICONTROL 表單涵蓋影格]**&#x200B;的整個寬度，AEM Sites頁面僅支援一個不含iframe的最適化表單存在。 若要使用&#x200B;**[!UICONTROL 最適化Forms — 內嵌]**&#x200B;元件新增更多最適化Forms，請選取&#x200B;**[!UICONTROL 表單涵蓋影格整個寬度]**&#x200B;選項。

## 在AEM Sites頁面或AEM體驗片段中建立最適化表單的考量事項 {#consideration}

* 當您使用調適型表單容器建立或新增表單時，表單會透過 AEM Sites 翻譯流程進行翻譯和本地化。 對於每種語言，系統會產生網站頁面和相應表單的個別副本 (語言副本)，當內容作者在父頁面表單中修訂規則時，表單的所有語言副本必須進行相同的變更。 最適化表單容器也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

* 當您使用調適型表單 - 嵌入元件建立或新增表單時，表單會使用 AEM Forms 翻譯流程進行翻譯和本地化。 在這種情況下，Sites 頁面的所有語言副本中會維持和引用單一表單。 調適型表單-嵌入元件不會讓您存取 AEM Sites 頁面的各種功能，例如版本設定、目標定位、翻譯和多個網站管理員。


## 在AEM Sites頁面或AEM體驗片段中建立或新增最適化表單的需求 {#before-you-start-creating-an-adaptive-form}

開始建立最適化表單之前，請啟用最適化Forms核心元件，並將最適化Forms使用者端程式庫新增到AEM Sites頁面：

### 為您的AEM Cloud Service環境啟用最適化Forms核心元件

確保[已為您的 AEM Forms as a Cloud Service environment 環境啟用調適型表單核心元件](enable-adaptive-forms-core-components.md)。

### 新增Adaptive Forms使用者端資料庫至您的AEM Sites頁面或體驗片段

若要啟用調適型表單容器元件的完整功能，請使用部署管道將 Customheaderlibs 和 Customfooterlibs 客戶端資料庫新增至您的 AEM Sites 頁面。 若要新增資料庫：

1. 存取並原地複製您的 [AEM Cloud Service Git 存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html)。
1. 在純文字編輯器中開啟 AEM Cloud Service Git 存放庫資料夾。 例如，Microsoft 視覺效果程式碼。
1. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //Customheaderlibs.html
   
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 開啟`ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html`檔案，並將下列程式碼新增至檔案：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [執行部署管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html)，將客戶端資料庫部署到您的 AEM as a Cloud Service 環境。

### 為您的AEM Sites頁面或體驗片段啟用最適化Forms容器

若要啟用範本原則中的[!UICONTROL 調適型表單容器]元件，需執行以下步驟：

1. 開啟AEM Sites頁面或體驗片段進行編輯。 若要開啟頁面進行編輯，請選擇該頁面，然後按一下「編輯」。
1. 開啟網站或體驗片段頁面的範本。 若要開啟範本，前往[!UICONTROL 頁面資訊] ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg)>[!UICONTROL 編輯範本]。 它會在範本編輯器中開啟對應的範本。
1. 在「結構」視圖中，在選單列中按一下&#x200B;**[!UICONTROL 「原則」]**![「原則」](/help/forms/assets/Smock_FeedManagement_18_N.svg)圖示。 在「**[!UICONTROL 允許的元件]**」清單中，選取「**[!UICONTROL 調適型表單容器]**」的勾選方格 (在 **[AEM 原型專案名稱] - 調適型表單**&#x200B;下方)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## 建立自適應表單 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

您可以直接在AEM Sites頁面或體驗片段中，從頭開始建立全新的表單，根據您的需求和設計偏好設定進行量身打造。 對於單次使用的表單，建議直接編寫到AEM Sites頁面，而體驗片段則適用於需要在您網站上的多個頁面中重複使用的表單。

* [在 AEM Sites 頁面建立表單](#create-an-adaptive-form-in-sites-editor)
* [在體驗片段中建立表單](#create-an-adaptive-form-in-experience-fragment)
* [將AEM Sites頁面中的最適化表單轉換為體驗片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### 在 AEM Sites 頁面建立表單 {#create-an-adaptive-form-in-sites-editor}

您可以使用AEM頁面編輯器中的調適型表單容器元件來建立自訂表單。 元件可讓您拖放表單元件來建立表單。 表單元件是以核心元件為主。 您可以根據組織的要求輕鬆自訂這一些。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

若要在 Sites 頁面建立調適型表單：

1. 在編輯模式中開啟 AEM Sites 頁面。
1. 將&#x200B;**[!UICONTROL 調適型表單容器]**&#x200B;元件從元件瀏覽器拖放至 Sites 頁面。 這樣可在頁面上為表單建立一個空間。 您可以使用版面模式來變更容器空間的大小。
1. 將調適型表單核心拖放至容器空間，以便建立表單。
1. 新增「提交」按鈕。

接著，您[設定提交動作](#configure-submit-action-for-form)和進階屬性。

### 在體驗片段中建立表單 {#create-an-adaptive-form-in-experience-fragment}

您可以新增表單至 AEM 體驗片段來擴展表單的範圍，如此可跨多個頁面或多個網站進行無縫的重複使用。 例如，您可以在體驗片段中包含時事通訊註冊表單。這可讓您方便地在網站的多個頁面中重複使用片段，而無需重複重新建立表單。 在體驗片段內對電子報登錄檔單所做的任何更新或修改都會自動傳播到所有使用它的頁面。 這簡化了流程並確保無縫的用戶體驗，同時簡化了網站表單的管理。

若要在體驗片段中建立調適型表單：

1. 開啟體驗片段。
1. 將&#x200B;**[!UICONTROL Adaptive Forms Container]**&#x200B;元件從元件瀏覽器拖放至體驗片段。
1. 將最適化表單核心元件拖放至體驗片段中的容器空間來建立表單。
1. 新增「提交」按鈕。

接著，您[設定提交動作](#configure-submit-action-for-form)和進階屬性。

### 將AEM Sites頁面中的表單轉換為體驗片段 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

您可以將網站頁面編輯器中的現有最適化表單轉換為體驗片段，以跨多個頁面或網站重複使用表單。

若要將AEM Sites頁面中的最適化表單轉換為體驗片段：

1. 在編輯模式中開啟包含調適型表單的AEM Sites頁面(在調適型Forms容器元件中)。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 在功能表列上，選取![轉換成體驗片段圖示](/help/forms/assets/Smock_FilingCabinet_18_N.svg)轉換成體驗片段變數圖示。
   ![按一下檔案封包標誌，將AEM Sites頁面中的最適化表單轉換為體驗片段](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   會出現對話方塊，將最適化表單容器轉換為新的體驗片段或新增到現有的體驗片段
1. 在轉換為體驗片段變數對話方塊中，設定以下選項的值：

   * **動作：**&#x200B;選取以建立體驗片段或新增至現有的體驗片段。
   * **父路徑：**&#x200B;指定承載體驗片段的資料夾路徑。 選項僅適用於建立體驗片段。
   * **範本：**&#x200B;指定體驗片段範本的路徑。 如果您沒有體驗片段範本，請[建立它](/help/implementing/developing/extending/experience-fragments.md)。 該選項僅可用於將最適化表單新增到現有的體驗片段。
   * **片段標題：**&#x200B;指定體驗片段的標題。 標題可唯一識別體驗片段


## 在AEM Sites頁面或體驗片段中設定表單的提交動作 {#configure-submit-action-for-form}

提交動作讓您可選擇透過最適化表單擷取的資料目標。當使用者按一下最適化表單上的提交按鈕時會觸發。 調適型表單包含一些立即可用的提交動作。 您也可以擴充預設提交動作，以建立自己的自訂提交動作。 若要設定表單的提交動作：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 可設定提交動作的調適型表單容器對話方塊隨即開啟。
   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定最適化表單的提交動作](/help/forms/assets/adaptive-forms-container.png)
1. 根據您的要求，選取並設定提交動作。 如需提交動作的詳細資訊，請參閱[最適化表單提交動作](/help/forms/configuring-submit-actions.md)


## 為AEM Sites頁面或體驗片段中的表單設定結構描述或表單資料模型(FDM) {#configure-schema-or-data-model-for-form}

您可以使用表單資料模型(FDM)將表單連線至資料Source，以根據使用者動作傳送及接收資料。 您也可以將表單連線至JSON結構描述，以預先定義的格式接收提交的資料。 根據需求，將表單連線到JSON結構描述或表單資料模型(FDM)：

* [建立JSON結構描述並上傳至您的環境](/help/forms/adaptive-form-json-schema-form-model.md)，或
* [建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)

若要設定表單的JSON結構描述或表單資料模型(FDM)：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![按一下扳手圖示以設定最適化表單的資料模型](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. 根據您的要求，選取並設定JSON結構描述或表單資料模型(FDM)。 如需提交動作的詳細資訊，請參閱[最適化表單提交動作](/help/forms/configuring-submit-actions.md)。

   * 當您選取&#x200B;**[!UICONTROL 表單模型]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 選取表單資料模型]**&#x200B;選項來選取預先設定的表單資料模型(FDM)。
   * 當您選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項為您的表單選取JSON結構描述。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

## 在AEM Sites頁面或體驗片段中設定表單的預填服務 {#configure-prefill-service-for-form}

您可以使用預填服務，使用現有資料自動填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 您可以：

* [建立自訂預填服務](/help/forms/prepopulate-adaptive-form-fields.md)
* [使用表單資料模型預填服務](#fdm-prefill-service)

### 使用表單資料模型預填服務預先填入AEM Sites頁面或體驗片段中表單的欄位 {#fdm-prefill-service}

您可以使用表單資料模型預填服務來預先填入AEM Sites頁面中適用性表單的欄位，或使用表單資料模型或自訂預填服務的體驗片段。 表單資料模型預填服務使用已設定的表單資料模型[的](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)Get服務來擷取資料。 若要針對最適化表單使用表單資料模型預填服務：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![按一下扳手圖示以開啟最適化表單容器對話方塊，設定最適化表單的預填服務](/help/forms/assets/adaptive-forms-container.png)
1. 選取表單資料模型。 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤。 在預填服務中，選取&#x200B;**[!UICONTROL 表單資料模型預填服務]**。
1. 按一下&#x200B;**[!UICONTROL 完成]**。 您的最適化表單現在已設定為使用表單資料模型預填。 您現在可以使用[規則編輯器](rule-editor.md)來建立規則以預先填入表單的欄位。


## 將使用者重新導向至頁面，或在提交表單時顯示感謝訊息

在提交表單時，您可以將使用者重新導向至其他網頁或訊息。 若要重新導向使用者或設定感謝訊息：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟內容樹狀結構，然後選取裝載您最適化表單的&#x200B;**[!UICONTROL 最適化Forms容器]**。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。

1. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;標籤。

   * 若要設定重新導向URL，請在[送出]選項中選取&#x200B;**[!UICONTROL 重新導向至URL]**&#x200B;選項，然後瀏覽並選取AEM Sites頁面，或提供外部頁面的URL。
   * 若要設定自訂或感謝訊息，請在[送出]選項中選取&#x200B;**[!UICONTROL 顯示訊息]**&#x200B;選項，並在&#x200B;**[!UICONTROL 訊息內容]**&#x200B;方塊中提供訊息。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。


