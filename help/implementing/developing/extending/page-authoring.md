---
title: 自訂頁面製作
description: 瞭解AEMas a Cloud Service提供自訂頁面製作功能的機制。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---


# 自訂頁面製作 {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service提供的機制可讓您自訂頁面製作功能(以及 [主控台](/help/implementing/developing/extending/consoles.md))。

## Clientlibs {#clientlibs}

Clientlibs可讓您擴充預設實作以啟用新功能，同時重複使用標準函式、物件和方法。

自訂時，您可以在下建立自己的clientlib `/apps.` 新clientlib必須：

* 取決於編寫clientlib `cq.authoring.editor.sites.page`.
* 成為適當的一部分 `cq.authoring.editor.sites.page.hook` 類別。

如需有關clientlibs的詳細資訊，請參閱檔案 [在AEMas a Cloud Service上使用使用者端資料庫。](/help/implementing/developing/introduction/clientlibs.md)

## 覆蓋 {#overlays}

覆蓋是以節點定義為基礎，可讓您覆蓋中的標準功能 `/libs` 透過您自己的自訂功能，於 `/apps`.

建立覆蓋圖時，不需要原始影像的1:1復本，因為 [sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 允許繼承。

如需詳細資訊，請參閱 [JS檔案集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

如需覆蓋圖的詳細資訊，請參閱檔案 [Adobe Experience Manager as a Cloud Service的覆蓋圖。](/help/implementing/developing/introduction/overlays.md)

## 加入新圖層（模式） {#add-new-layer-mode}

編輯頁面時，會有多種方式 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 可用。 這些模式的實作方式 [圖層](/help/implementing/developing/introduction/ui-structure.md#layer). 這些功能可讓使用者存取相同頁面內容的不同功能型別。 標準AEM模式包括「編輯」、「配置」、「開發人員」、「時間扭曲」、「即時副本狀態」和「鎖定目標」。

### 圖層範例：即時副本狀態 {#layer-example-live-copy-status}

標準AEM例項提供MSM層。 這會存取與以下專案相關的資料： [多站台管理](/help/sites-cloud/administering/msm/overview.md) 並在圖層中反白顯示。

若要檢視其實際運作情況，您可以編輯 [WKND範例內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 並選取 **即時副本狀態** 模式。

您可以在下列位置找到MSM圖層定義（以供參考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

此範例套件顯示如何為MSM檢視建立圖層（模式）。

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## 新增選擇類別至資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種型別/類別的資產（例如影像和檔案）。 您也可以依這些資產類別篩選資產。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一個範例套件，說明如何將群組新增至資產尋找器。 此範例連線到 [閃爍](https://www.flickr.com)的公開資料流，並在側面板中顯示。

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## 篩選資源 {#filtering-resources}

編寫頁面時，使用者通常必須從清單中的資源中進行選取。

為了將清單保持在合理的大小並與使用案例相關，可以以自訂述詞的形式實施篩選器。 例如，如果 `pathbrowser` Granite元件是用來讓使用者選取特定資源的路徑，可依下列方式篩選顯示的路徑：

* 實作自訂述詞 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) 介面。
* 指定述詞的名稱，並在使用時參照該名稱 `pathbrowser`.

如需建立自訂述詞的詳細資訊，請參閱 [本文章。](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## 將動作新增至元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件通常都有工具列，可讓您存取可對該元件執行的一系列動作。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一個範例套件，說明如何建立自訂工具列動作來轉譯元件。

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準的 AEM 配置中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` 儲存各種可用編輯器的定義。

1. 編輯器與可以使用的每個資源型別（如元件中所示）之間存在連線：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性: `editorType`

           定義為該元件觸發就地編輯時，所使用的內嵌編輯器型別；例如， `text`， `textimage`， `image`， `title`.

1. 編輯器的其他設定詳細資料可使用 `config` 包含設定和的節點 `plugin` 節點，以包含必要的外掛程式設定詳細資訊。


以下範例是為影像元件的影像裁切外掛程式定義外觀比例。

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
>AEM裁切比例，由設定 `ratio` 屬性，定義為 **高度/寬度**. 這與常見的寬度/高度定義不同，這樣做是出於舊版相容性的原因。 只要您定義 `name` 屬性中會清楚顯示，因為這是UI中顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

若要實作新的就地編輯器（在您的clientlib中）：

1. 實作：

   * `setUp`
   * `tearDown`

1. 註冊編輯器（包括建構函式）：

   * `editor.register`

1. 提供編輯器與可以使用的每個資源型別（如元件中）之間的連線。

#### 建立新就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一個範例套件，說明如何在AEM中建立就地編輯器。

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## 新增新頁面動作 {#add-a-new-page-action}

若要在頁面工具列中新增頁面動作，例如 **返回網站** （主控台）動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一個範例套件，說明如何建立自訂標題列動作以跳回網站主控台。

您可以在此頁面找到程式碼： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## 自訂啟用請求工作流程 {#customizing-the-request-for-activation-workflow}

現成的工作流程、 **請求啟用**：

* 當內容作者時，會自動出現在適當的選單上 **沒有** 適當的復寫許可權，但 **有** DAM使用者和作者的成員資格。

* 否則，不會顯示任何內容，因為已移除復寫許可權。

若要在發生此類啟動時具有自訂行為，您可以覆蓋 **請求啟用** 工作流程：

1. 在 `/apps` 覆蓋 **網站** 精靈 `/libs/wcm/core/content/common/managepublicationwizard`

   * 這本身會覆寫的共同例項 `/libs/cq/gui/content/common/managepublicationwizard`.

1. 視需要更新工作流程模型和相關設定/指令碼。
1. 移除「 」的許可權 `replicate` 所有相關頁面的所有適當使用者執行的動作。 若要在任何使用者時將此工作流程作為預設動作觸發，請嘗試發佈（或復寫）頁面。
