---
title: 在Adobe Experience Manager as a Cloud Service中使用Sling Resource Merger
description: Sling Resource Merger提供存取及合併資源的服務
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# 在 AEM as a Cloud Service 中使用 Sling Resource Merger {#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Merger提供存取及合併資源的服務。 它為兩者提供不同（差異）機制：

* 使用&#x200B;**[搜尋路徑](/help/implementing/developing/introduction/overlays.md)**&#x200B;的[資源重疊](/help/implementing/developing/introduction/overlays.md#search-paths)。

* 使用資源型別階層（透過屬性&#x200B;**）覆寫觸控式UI (**)的元件對話方塊的`cq:dialog`覆寫`sling:resourceSuperType`。

透過Sling Resource Merger，覆蓋/覆寫資源和/或屬性會與原始資源/屬性合併：

* 自訂定義內容的優先順序高於原始定義（亦即&#x200B;*覆蓋*&#x200B;或&#x200B;*覆寫*）。

* 必要時，自訂中定義的[屬性](#properties)會指示如何使用從原始內容合併的內容。

>[!CAUTION]
>
>Sling Resource Merger和相關方法只能搭配觸控式UI (這是AEM as a Cloud Service唯一可用的UI)使用。

### AEM的目標 {#goals-for-aem}

在AEM中使用Sling Resource Merger的目標為：

* 請確定未在`/libs`中進行自訂變更。
* 減少從`/libs`復寫的結構。

  使用Sling資源合併時，不建議從`/libs`複製整個結構，因為這將導致自訂中保留過多資訊（通常為`/apps`）。 當系統以任何方式升級時，不必要地複製資訊會增加發生問題的機會。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何專案。
>
>這是因為`/libs`的內容可能會在升級套用至執行個體時遭到覆寫。
>
>* 覆蓋圖依存於[搜尋路徑](/help/implementing/developing/introduction/overlays.md#search-paths)。
>
>* 覆寫不依存於搜尋路徑，它們會使用屬性`sling:resourceSuperType`來建立連線。
>
>不過，覆寫通常定義在`/apps`下，因為AEM as a Cloud Service的最佳實務是在`/apps`下定義自訂；這是因為您不得變更`/libs`下的任何專案。

### 屬性 {#properties}

資源合併器提供下列屬性：

* `sling:hideProperties` （ `String`或`String[]`）

  指定要隱藏的屬性或屬性清單。

  萬用字元`*`會隱藏所有。

* `sling:hideResource` ( `Boolean`)

  指示是否應完全隱藏資源，包括其子項。

* `sling:hideChildren` （ `String`或`String[]`）

  包含要隱藏的子節點或子節點清單。 會維護節點的屬性。

  萬用字元`*`會隱藏所有。

* `sling:orderBefore` ( `String`)

  包含同層級節點的名稱，目前節點應位於該節點的前面。

這些屬性會影響覆蓋/覆寫（通常在`/libs`中）使用對應/原始資源/屬性（來自`/apps`）的方式。

### 建立結構 {#creating-the-structure}

若要建立覆蓋或覆寫，您需要在目的地（通常為`/apps`）下以同等結構重新建立原始節點。 例如：

* 覆蓋

   * Sites主控台之導覽專案的定義（如邊欄中所示）定義於：

     `/libs/cq/core/content/nav/sites/jcr:title`

   * 若要覆蓋此節點，請建立下列節點：

     `/apps/cq/core/content/nav/sites`

     然後視需要更新屬性`jcr:title`。

* 覆寫

   * 文字控制檯之觸控式對話方塊的定義定義如下：

     `/libs/foundation/components/text/cq:dialog`

   * 若要覆寫此節點，請建立以下節點 — 例如：

     `/apps/the-project/components/text/cq:dialog`

若要建立其中一個，您只需要重新建立骨架結構。 若要簡化結構的重新建立，所有中介節點都可以是`nt:unstructured`型別（它們不必反映原始節點型別；例如，在`/libs`中）。

所以在上述覆蓋圖範例中，需要下列節點：

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
>在使用Sling Resource Merger （亦即處理標準觸控式UI時）時，不建議從`/libs`複製整個結構，因為這樣會導致`/apps`中保留太多資訊。 當系統以任何方式升級時，這可能會導致問題。

### 使用案例 {#use-cases}

這些功能與標準功能搭配使用，可讓您：

* **新增屬性**

  屬性不存在於`/libs`定義中，但在`/apps`覆蓋/覆寫中是必要的。

   1. 在`/apps`中建立對應的節點
   1. 在此節點上建立新屬性»

* **重新定義屬性（不是自動建立的屬性）**

  屬性已在`/libs`中定義，但在`/apps`覆蓋/覆寫中需要新值。

   1. 在`/apps`中建立對應的節點
   1. 在此節點上建立相符的屬性（在/ `apps`下）

      * 根據Sling資源解析器設定，屬性的優先順序將為。
      * 支援變更屬性型別。

        如果您使用的屬性型別與`/libs`中使用的屬性型別不同，則會使用您定義的屬性型別。

  >[!NOTE]
  >
  >支援變更屬性型別。

* **重新定義自動建立的屬性**

  依預設，自動建立的屬性（例如`jcr:primaryType`）不受覆蓋/覆寫約束，以確保目前在`/libs`之下的節點型別受到遵守。 若要強制覆蓋/覆寫，您必須在`/apps`中重新建立節點，明確隱藏屬性並重新定義它：

   1. 使用所需的`/apps`在`jcr:primaryType`下建立對應的節點
   1. 在該節點上建立屬性`sling:hideProperties`，其值設為自動建立屬性的值；例如`jcr:primaryType`

      這個在`/apps`下定義的屬性，現在會優先於`/libs`下定義的屬性

* **重新定義節點及其子系**

  節點及其子系已在`/libs`中定義，但在`/apps`覆蓋/覆寫中需要新設定。

   1. 結合下列動作：

      1. 隱藏節點的子系（保留節點的屬性）
      1. 重新定義屬性/屬性

* **隱藏屬性**

  屬性已在`/libs`中定義，但在`/apps`覆蓋/覆寫中並非必要。

   1. 在`/apps`中建立對應的節點
   1. 建立型別`sling:hideProperties`或`String`的屬性`String[]`。 使用此項可指定要隱藏/忽略的屬性。 也可以使用萬用字元。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子系**

  節點及其子系已在`/libs`中定義，但在`/apps`覆蓋/覆寫中並非必要。

   1. 在/apps下建立對應的節點
   1. 建立屬性`sling:hideResource`

      * 型別： `Boolean`
      * 值： `true`

* **隱藏節點的子系（同時保留節點的屬性）**

  在`/libs`中定義節點、其屬性及其子系。 `/apps`覆蓋/覆寫中需要節點及其屬性，但`/apps`覆蓋/覆寫中不需要部分或全部子節點。

   1. 在`/apps`下建立對應的節點
   1. 建立屬性`sling:hideChildren`：

      * 型別： `String[]`
      * 值：要隱藏/忽略的子節點清單（如`/libs`中所定義）

      萬用字元&amp;amp；ast；可用來隱藏/忽略所有子節點。

* **重新排序節點**

  節點及其同層級已在`/libs`中定義。 需要新位置，以便在`/apps`覆蓋/覆寫中重新建立節點，其中新位置是參照`/libs`中適當的同層級節點所定義。

   * 使用`sling:orderBefore`屬性：

      1. 在`/apps`下建立對應的節點
      1. 建立屬性`sling:orderBefore`：

         這會指定目前節點應置於之前的節點（如`/libs`）：

         * 型別： `String`
         * 值： `<before-SiblingName>`

### 從您的程式碼叫用Sling Resource Merger {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger包含兩個自訂資源提供者，一個用於覆蓋，另一個用於覆寫。 您可以使用掛接點，在程式碼中叫用這些選項：

>[!NOTE]
>
>存取資源時，建議使用適當的掛載點。
>
>這可確保叫用Sling資源合併並傳回完全合併的資源（減少必須從`/libs`復寫的結構）。

* 覆蓋：

   * 用途：根據搜尋路徑合併資源
   * 掛接點： `/mnt/overlay`
   * 使用狀況： `mount point + relative path`
   * 範例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫：

   * 用途：根據資源的超級型別合併資源
   * 掛接點： `/mnt/overide`
   * 使用狀況： `mount point + absolute path`
   * 範例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

