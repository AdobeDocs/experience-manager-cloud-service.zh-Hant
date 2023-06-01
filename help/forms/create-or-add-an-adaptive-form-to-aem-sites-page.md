---
title: 建立或新增最適化表單至AEM Sites頁面
description: 瞭解如何輕鬆地建立最適化表單或順暢地將最適化表單新增到您的AEM Sites頁面。 瞭解將動態和可自訂表單整合至網站的分步技巧和最佳實務，最佳化您的數位體驗以發揮最大影響力。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# 建立或新增最適化表單至AEM Sites頁面 {#create-or-add-an-adaptive-form-to-aem-sites-page}

有了AEM Forms，您可以將最適化表單順暢地整合到網頁中。 這可讓您的訪客方便地填寫和提交表單，而不會離開他們所在的頁面。 如此一來，他們可以輕鬆地與網站的其他元素保持互動，同時主動與表單互動。

您可以充分利用此功能，利用下列選項：

* **新增自訂表單：** 從頭開始建立全新的表單，根據您的需求和設計偏好量身打造。

* **增強體驗片段：** 透過將表單新增到AEM體驗片段來擴展表單的覆蓋面，允許多個頁面或網站無縫重複使用。

* **利用核准的範本：** 運用預先核准的範本，快速建立符合貴組織品牌指導方針和設計標準的表單。

* **新增現有表單：** 輕鬆將您已建立的表單整合至網站，讓訪客可直接與他們互動。

* **新增多個表單：**  將多個表單新增至一個頁面，以根據使用者的偏好和需求為其提供多個選擇。 這些可以是全新表單和現有表單的組合。

您可以使用AEM Sites編輯器快速建立多個表單並新增到您的AEM Sites頁面。 使用AEM Sites編輯器，內容作者就能利用調適型表單元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面中建立順暢的資料擷取體驗。 它也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

## 目標

* 瞭解如何使用AEM Sites編輯器和體驗片段建立最適化表單
* 瞭解如何為AEM Sites頁面新增的最適化表單設定版面和主題，以及
* 使用AEM Sites編輯器和體驗片段建立最適化表單


## 考量事項 {#consideration}

AEM Forms提供最適化表單容器和最適化Forms — 內嵌元件。 您可以使用調適型表單容器在體驗片段或AEM Sites頁面中建立並新增表單，而調適型Forms — 內嵌元件可讓您新增現有調適型表單或使用調適型Forms編輯器建立新表單。

當您使用最適化表單容器建立或新增表單時，表單會透過AEM Sites翻譯流程進行翻譯和本地化。 對於每種語言，都會產生網站頁面和對應表單的個別副本（語言副本），當內容作者在父頁面的表單中修改規則時，必須在表單的所有語言副本中進行相同的變更。 最適化表單容器也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

使用最適化表單內嵌元件建立或新增表單時，系統會使用AEM Forms翻譯流程翻譯及本地化表單。 在此情況下，會維護單一表單，並在Sites頁面的所有語言副本中參照。 最適化表單內嵌元件不提供對AEM Sites頁面的各種功能（如版本設定、目標定位、翻譯和多網站管理員）的存取權。


## 開始之前 {#before-you-start}

+++  為您的環境啟用最適化Forms核心元件

確保 [已針對您的AEM Formsas a Cloud Service環境啟用最適化Forms核心元件](enable-adaptive-forms-core-components.md).

+++

+++ 啟用**[!UICONTROL 最適化Forms容器]

若要啟用 [!UICONTROL 最適化Forms容器] 元件執行範本原則中的下列步驟：

1. 開啟AEM Sites頁面進行編輯。 若要開啟頁面進行編輯，請選取頁面，然後按一下編輯。
1. 開啟Sites頁面的範本。 若要開啟範本，請前往 [!UICONTROL 頁面資訊] ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL 編輯範本]. 它會在範本編輯器中開啟對應的範本。
1. 在「結構」檢視中，按一下 **[!UICONTROL 原則]** ![原則](/help/forms/assets/Smock_FeedManagement_18_N.svg) 圖示來識別。 在 **[!UICONTROL 允許的元件]** 清單並選取 **[!UICONTROL 最適化Forms容器]**  核取方塊於 **[AEM原型專案名稱]  — 最適化表單**.
1. 按一下 **[!UICONTROL 完成]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  將Adaptive Forms使用者端程式庫新增至AEM Sites頁面

若要啟用最適化Forms容器元件的完整功能，請使用部署管道將Customheaderlibs和Customfooterlibs使用者端程式庫新增到AEM Sites頁面。 若要新增程式庫：

1. 存取並複製您的 [AEM Cloud Service Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. 在計畫文字編輯器中開啟AEM Cloud Service Git存放庫資料夾。 例如，Microsoft Visual Code。
1. 開啟 `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` 檔案進行編輯，並記下值 `sling:resourceSuperType`. 例如，記下值 `core/wcm/components/page/v3/page`.


   ![sling資源](/help/forms/assets/slingresource.png)

1. 導覽至 `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` 和建立與上一步中所述相同的資料夾結構。 例如，如果值與上一步中的範例類似，則最終節點結構為 `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 建立 `customheaderlibs.html` 和 `customfooterlibs.html` 以上一步建立的節點結構建立檔案，並將以下內容新增至檔案：

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

1. [執行部署管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 將使用者端程式庫部署至您的AEMas a Cloud Service環境。

+++

## 建立最適化表單 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

您可以直接在AEM網站頁面或體驗片段中，從頭開始建立全新的表單，根據您的需求和設計偏好設定進行量身打造。 對於單次使用的表單，建議直接製作到AEM網站頁面，而體驗片段則適用於需要在您網站上的多個頁面中重複使用的表單。

* [在AEM Sites頁面中建立表單](#create-an-adaptive-form-in-sites-editor)
* [在體驗片段中建立表單](#create-an-adaptive-form-in-experience-fragment)

### 在AEM Sites頁面中建立表單 {#create-an-adaptive-form-in-sites-editor}

您可以使用AEM Sites編輯器中的調適型表單容器元件來建立自訂表單。 元件可讓您拖放表單元件來建立表單。 表單元件以核心元件為基礎。 您可以根據貴組織的需求，輕鬆自訂這些專案。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

若要在Sites頁面中建立最適化表單：

1. 在編輯模式下開啟AEM Sites頁面。
1. 拖放 **[!UICONTROL 最適化Forms容器]** 元件從「元件瀏覽器」移至「網站」頁面。 它會在頁面上為表單建立空間。 您可以使用版面模式來變更容器空間的大小。
1. 將最適化表單核心元件拖放至容器空間以建立表單。
1. 新增「提交」按鈕。

接下來，您設定「提交」動作和進階屬性。

### 在體驗片段中建立表單 {#create-an-adaptive-form-in-experience-fragment}

您可以將表單新增至AEM體驗片段以擴大表單的覆蓋範圍，好讓多個頁面或網站順暢地重複使用。 例如，您可以在體驗片段中包含Newsletter登錄檔單。 這可讓您方便地在網站的多個頁面中重複使用片段，而無需重複重新建立表單。 在體驗片段內對Newsletter登錄檔單所做的任何更新或修改都會自動傳播到所有使用它的頁面。 這能簡化程式，並確保順暢的使用者體驗，同時簡化網站表單的管理。

若要在體驗片段中建立最適化表單：

## 變更最適化表單的版面 {#change-layout-of-an-adaptive-form}

在AEM Sites頁面中，使用 [版面模式](/help/sites-cloud/authoring/features/responsive-layout.md) 調整新增至AEM Sites頁面的最適化表單容器元件大小。
