---
title: 在Adobe Experience Manager中使用Sling Resource Merger做為Cloud Service
description: Sling Resource Merger提供存取和合併資源的服務
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 2%

---

# 在 AEM as a Cloud Service 中使用 Sling Resource Merger {#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Merger提供存取和合併資源的服務。 它為以下兩者提供差異（差異）機制：

* **[](/help/implementing/developing/introduction/overlays.md)** 使用搜尋路徑覆 [蓋資源](/help/implementing/developing/introduction/overlays.md#search-paths)。

* **** 使用資源類型階層（透過屬性）覆寫觸控式UI(`cq:dialog`)的元件對話 `sling:resourceSuperType`方塊。

透過Sling Resource Merger，覆蓋/覆寫資源和/或屬性會與原始資源/屬性合併：

* 自訂定義的內容具有比原始定義更高的優先順序（即&#x200B;*覆蓋*&#x200B;或&#x200B;*覆蓋*）。

* 如有必要，在自訂中定義的[屬性](#properties)會指出如何使用從原始合併的內容。

<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Sling Resource Merger及相關方法只能搭配觸控式UI使用(這是AEM as a Cloud Service唯一可用的UI)。

### AEM的目標{#goals-for-aem}

在AEM中使用Sling Resource Merger的目標為：

* 確保未在`/libs`中進行自定義更改。
* 減少從`/libs`複製的結構。

   使用Sling Resource Merger時，不建議從`/libs`複製整個結構，因為這會導致自訂中保留太多資訊（通常為`/apps`）。 以任何方式升級系統時，重複資訊會不必要地增加出現問題的機會。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為每當將升級應用到您的實例時，`/libs`的內容都可能被覆蓋。
>
>* 覆蓋圖取決於[搜尋路徑](/help/implementing/developing/introduction/overlays.md#search-paths)。
   >
   >
* 覆蓋不依賴於搜索路徑，它們使用屬性`sling:resourceSuperType`建立連接。
>
>
不過，覆寫通常定義在`/apps`下，因為在AEM as aCloud Service中，最佳作法是在`/apps`下定義自訂；這是因為您不得變更`/libs`下的任何項目。

### 屬性 {#properties}

資源合併提供以下屬性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隱藏的屬性或屬性清單。

   萬用字元`*`會隱藏全部。

* `sling:hideResource` ( `Boolean`)

   指出是否應完全隱藏資源，包括其子項。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隱藏的子節點或子節點清單。 節點的屬性將會保留。

   萬用字元`*`會隱藏全部。

* `sling:orderBefore` ( `String`)

   包含當前節點應位於前面的同級節點的名稱。

這些屬性會影響覆蓋/覆寫（通常在`/apps`中）使用對應/原始資源/屬性的方式（來自`/libs`）。

### 建立結構{#creating-the-structure}

若要建立覆蓋或覆寫，您必須在目的地（通常為`/apps`）下，以等同的結構重新建立原始節點。 例如：

* 覆蓋

   * 如邊欄中所示，Sites主控台的導覽項目定義如下：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 若要覆蓋，請建立下列節點：

      `/apps/cq/core/content/nav/sites`

      然後視需要更新屬性`jcr:title`。

* 覆寫

   * Texts控制台的觸控式對話方塊的定義，定義於：

      `/libs/foundation/components/text/cq:dialog`

   * 若要覆寫此值，請建立下列節點，例如：

      `/apps/the-project/components/text/cq:dialog`

要建立其中任一項，您只需重新建立骨架結構。 為了簡化結構的重建，所有中間節點都可以是`nt:unstructured`類型(它們不必反映原始節點類型；例如，在`/libs`中。

因此，在上述覆蓋範例中，需要下列節點：

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>使用Sling Resource Merger時（即處理標準的觸控式UI時），不建議從`/libs`複製整個結構，因為這會導致`/apps`中保留太多資訊。 這在系統以任何方式升級時都可能造成問題。

### 使用案例{#use-cases}

這些功能與標準功能結合，可讓您：

* **新增屬性**

   屬性不存在於`/libs`定義中，但是在`/apps`覆蓋/覆蓋中是必要的。

   1. 在`/apps`內建立對應節點
   1. 在此節點上建立新屬性「

* **重定義屬性（非自動建立的屬性）**

   該屬性在`/libs`中定義，但在`/apps`覆蓋/覆蓋中需要新值。

   1. 在`/apps`內建立對應節點
   1. 在此節點上建立相符的屬性（在/ `apps`底下）

      * 屬性的優先順序會以Sling資源解析器設定為基礎。
      * 支援變更屬性類型。

         如果您使用的屬性類型與`/libs`中使用的屬性類型不同，則將使用您定義的屬性類型。
   >[!NOTE]
   >
   >支援變更屬性類型。

* **重定義自動建立的屬性**

   依預設，自動建立的屬性（例如`jcr:primaryType`）不受覆蓋/覆寫的限制，以確保目前`/libs`下的節點類型可接受。 要施加覆蓋/覆蓋，必須在`/apps`中重新建立節點，顯式隱藏該屬性並重定義該屬性：

   1. 使用所需的`jcr:primaryType`在`/apps`下建立對應節點
   1. 在該節點上建立屬性`sling:hideProperties`，並將值設為自動建立屬性的值；例如`jcr:primaryType`

      此屬性（在`/apps`下定義）現在比在`/libs`下定義的屬性具有優先順序

* **重新定義節點及其子節點**

   節點及其子項在`/libs`中定義，但在`/apps`覆蓋/覆蓋中需要新配置。

   1. 結合下列動作：

      1. 隱藏節點的子項（保留節點的屬性）
      1. 重定義屬性/屬性

* **隱藏屬性**

   該屬性在`/libs`中定義，但在`/apps`覆蓋/覆蓋中不是必要屬性。

   1. 在`/apps`內建立對應節點
   1. 建立`String`或`String[]`類型的屬性`sling:hideProperties`。 使用它指定要隱藏/忽略的屬性。 您也可以使用萬用字元。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子代**

   節點及其子項在`/libs`中定義，但在`/apps`覆蓋/覆蓋中不是必需的。

   1. 在/apps下建立對應節點
   1. 建立屬性`sling:hideResource`

      * 類型: `Boolean`
      * 值: `true`

* **隱藏節點的子項（同時保留節點的屬性）**

   在`/libs`中定義節點、其屬性及其子項。 在`/apps`覆蓋/覆蓋中需要節點及其屬性，但在`/apps`覆蓋/覆蓋中不需要部分或全部子節點。

   1. 在`/apps`下建立對應的節點
   1. 建立屬性`sling:hideChildren`:

      * 類型: `String[]`
      * 值：要隱藏/忽略的子節點清單（如`/libs`中定義）

      通配符&amp;ast;可用於隱藏/忽略所有子節點。


* **重新排序節點**

   節點及其同級在`/libs`中定義。 需要新位置，因此會在`/apps`覆蓋/覆蓋中重新建立節點，其中新位置是在參考`/libs`中適當的同層節點時定義。

   * 使用`sling:orderBefore`屬性：

      1. 在`/apps`下建立對應的節點
      1. 建立屬性`sling:orderBefore`:

         這指定了當前節點應放在以下位置之前的節點（如`/libs`中）:

         * 類型: `String`
         * 值: `<before-SiblingName>`

### 從您的程式碼{#invoking-the-sling-resource-merger-from-your-code}叫用Sling Resource Merger

Sling Resource Merger包含兩個自訂資源提供者：一個用於覆蓋，另一個用於覆寫。 您可以使用裝載點在您的代碼中叫用其中的每一項：

>[!NOTE]
>
>訪問資源時，建議使用適當的裝載點。
>
>這可確保叫用Sling Resource Merger並傳回完全合併的資源（減少需要從`/libs`複製的結構）。

* 覆蓋:

   * 目的：根據資源的搜索路徑合併資源
   * 裝載點：`/mnt/overlay`
   * 用法：`mount point + relative path`
   * 範例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫:

   * 目的：根據資源的超類型合併資源
   * 裝載點：`/mnt/overide`
   * 用法：`mount point + absolute path`
   * 範例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

<!--
### Example of Usage {#example-of-usage}

Some examples are covered:

* Overlay:

    * [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
    * [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)

* Override:

    * [Configuring your Page Properties](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
-->
