---
title: 自訂頁面編寫
description: 了解 AEM as a Cloud Service 提供用來自訂頁面編寫功能的機制。
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 85%

---

# 自訂頁面編寫 {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service 會提供一些機制，讓您自訂編寫執行個體的頁面編寫功能 (以及[主控台](/help/implementing/developing/extending/consoles.md))。

## Clientlibs {#clientlibs}

Clientlib 讓您可擴充預設實作以啟用新功能，同時會重複使用標準函數、物件和方法。

進行自訂時，您可以在 `/apps.` 下面建立自己的 clientlib。新的 clientlib 必須：

* 依賴編寫 clientlib `cq.authoring.editor.sites.page`。
* 屬於適當的 `cq.authoring.editor.sites.page.hook` 類別的一部分。

請參閱[在AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md)上使用使用者端資料庫。

## 覆蓋 {#overlays}

覆蓋會根據節點定義，並可讓您覆蓋 `/libs` 中的標準功能和 `/apps` 中您自己的自訂功能。

建立覆蓋時，不需要1:1原始復本，因為[sling資源合併器](/help/implementing/developing/introduction/sling-resource-merger.md)允許繼承。

如需詳細資訊，請參閱[JS檔案集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)。

如需重疊的詳細資訊，請參閱[Adobe Experience Manager as a Cloud Service的重疊](/help/implementing/developing/introduction/overlays.md)。

## 新增「新圖層」(模式) {#add-new-layer-mode}

當您編輯頁面時，有各種[模式](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes)可使用。這些模式會使用[圖層](/help/implementing/developing/introduction/ui-structure.md#layer)實作。這些可容許存取相同頁面內容的不同功能類型。標準 AEM 模式包括編輯、版面、開發人員、時間扭曲、Live Copy 狀態和目標定位。

### 圖層範例：Live Copy 狀態 {#layer-example-live-copy-status}

標準 AEM 執行個體會提供 MSM 圖層。這會存取和[多網站管理](/help/sites-cloud/administering/msm/overview.md)相關的資料並在圖層中將其醒目顯示。

若要查看其實際效果，您可以編輯 [WKND 範例內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md)中的任何語言副本，並選取 **Live Copy 狀態**&#x200B;模式。

您可以在以下位置找到 MSM 圖層定義 (僅供參考)：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

這是一個範例套件，顯示如何建立 MSM 檢視的圖層 (模式)。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)上找到此頁面的程式碼。

## 將新選擇類別新增到資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種類型/類別的資產 (例如影像和文件)。還可以依這些資產類別篩選資產。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一種範例套件，會顯示如何將群組新增到資產尋找器。此範例會連接到 [Flickr](https://www.flickr.com) 的公用串流並在側邊面板中顯示它們。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)上找到此頁面的程式碼。

## 篩選資源 {#filtering-resources}

在編寫頁面時，使用者必須經常從清單上的資源中進行選取。

若要將清單保持為合理的大小並且和使用案例相關，可以以自訂述詞的形式實作篩選器。例如，如果將 `pathbrowser`Granite 元件用於讓使用者可選取特定資源的路徑，則可以透過以下方式篩選顯示的路徑：

* 透過實作 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) 介面實作自訂述詞。
* 指定述詞的名稱，並在使用 `pathbrowser` 時參照該名稱。

如需建立自訂述詞的詳細資訊，請參閱[本文章](/help/implementing/developing/introduction/query-builder-custom-predicate.md)。

## 將新動作新增到元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件通常都會有一個工具列，可用以存取對該元件可以採取的一系列動作。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一種範例套件，會顯示如何建立可轉譯元件的自訂工具列動作。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)上找到此頁面的程式碼。

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準的 AEM 安裝中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` 會保存各種可用編輯器的定義。

1. 編輯器和可以使用它的每種資源類型 (如在元件中) 之間有連結：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性：`editorType`

           定義觸發該元件的就地編輯時所使用的內聯編輯器的類型；例如，`text`、`textimage`、`image`、`title`。

1. 使用包含設定的 `config` 節點和 `plugin` 節點可設定編輯器的其他設定詳細資料，以包含必要的外掛程式設定的詳細資料。


以下是為影像元件的影像裁切外掛程式定義外觀比例的範例。

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>AEM 裁切比例 (由 `ratio` 屬性設定) 的定義為&#x200B;**高度/寬度比**。這和寬度/高度比的傳統定義不同，並且是由於舊有相容性的原因完成的。如果您清楚定義了 `name` 屬性，編寫的使用者並不會看出任何差異，因為這即是 UI 中所顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

若要實作新的就地編輯器 (在您的 clientlib 裡面)：

1. 實作：

   * `setUp`
   * `tearDown`

1. 註冊編輯器 (包括建構函式)：

   * `editor.register`

1. 提供編輯器和可以使用它的每種資源類型 (如在元件中) 之間的連結：

#### 用於建立新的就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一種範例套件，會顯示如何在 AEM 中建立就地編輯器。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)上找到此頁面的程式碼。

## 新增「新頁面動作」。 {#add-a-new-page-action}

若要在頁面工具列中新增頁面動作，例如&#x200B;**返回網站** （主控台）動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一種範例套件，會顯示如何建立自訂標頭列動作以跳回 Sites 主控台。

您可以在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)上找到此頁面的程式碼。

## 自訂要求啟動工作流程 {#customizing-the-request-for-activation-workflow}

此現成可用的工作流程，**要求啟動**：

* 會在內容作者&#x200B;**不具有**&#x200B;適當的複製權時自動顯示在適當的選單上，但&#x200B;**確實具有** DAM 使用者和作者的成員資格。

* 不然的話，由於已移除複製權，因此不會顯示任何內容。

若要在這類啟動上自訂行為，您可以覆蓋「**要求啟動**」工作流程：

1. 在 `/apps` 中，覆蓋 **Sites** 精靈 `/libs/wcm/core/content/common/managepublicationwizard`

   * 這本身就覆寫了 `/libs/cq/gui/content/common/managepublicationwizard` 的通用執行個體。

1. 根據需要更新工作流程模式和相關的設定/指令碼。
1. 將所有適當的使用者對所有相關頁面的 `replicate` 動作的權利移除。預設動作為任何使用者試圖發佈 (或複製) 頁面時即會觸發此工作流程。
