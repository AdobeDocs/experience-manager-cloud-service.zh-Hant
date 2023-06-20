---
title: 在Adobe Experience Manager as a Cloud Service中使用Sling Resource Merger
description: Sling Resource Merger提供存取和合併資源的服務
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 2%

---

# 在 AEM as a Cloud Service 中使用 Sling Resource Merger {#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Merger提供存取和合併資源的服務。 它為兩者提供不同的（差異）機制：

* **[覆蓋](/help/implementing/developing/introduction/overlays.md)** 資源使用 [搜尋路徑](/help/implementing/developing/introduction/overlays.md#search-paths).

* **覆寫** 觸控式UI的元件對話方塊數量(`cq:dialog`)，使用資源型別階層(透過屬性 `sling:resourceSuperType`)。

透過Sling Resource Merger，覆蓋/覆寫資源和/或屬性會與原始資源/屬性合併：

* 自訂定義的內容優先順序高於原始定義(亦即 *覆蓋* 或 *覆寫* it)。

* 必要時， [屬性](#properties) 在自訂中定義，指示如何使用從原始內容合併的內容。

>[!CAUTION]
>
>Sling資源合併器和相關方法只能與觸控式UI (這是AEMas a Cloud Service唯一可用的UI)一起使用。

### AEM的目標 {#goals-for-aem}

在AEM中使用Sling Resource Merger的目標為：

* 確保不會在中進行自訂變更 `/libs`.
* 減少復寫來源的結構 `/libs`.

  使用Sling Resource Merger時，不建議從複製整個結構 `/libs` 因為這會導致自訂中保留太多資訊(通常是 `/apps`)。 當系統以任何方式升級時，不必要地複製資訊會增加發生問題的機會。

>[!CAUTION]
>
>您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
>
>這是因為 `/libs` 升級可隨時套用至您的執行個體而遭到覆寫。
>
>* 覆蓋圖相依於 [搜尋路徑](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* 覆寫與搜尋路徑無關，而是使用屬性 `sling:resourceSuperType` 以建立連線。
>
>不過，覆寫通常定義於 `/apps`，因為AEMas a Cloud Service的最佳實務是定義下的自訂 `/apps`；這是因為您不得變更下的任何專案 `/libs`.

### 屬性 {#properties}

資源合併器提供下列屬性：

* `sling:hideProperties` ( `String` 或 `String[]`)

  指定要隱藏的屬性或屬性清單。

  萬用字 `*` 隱藏所有。

* `sling:hideResource` ( `Boolean`)

  指出資源是否應該完全隱藏，包括其子項。

* `sling:hideChildren` ( `String` 或 `String[]`)

  包含要隱藏的子節點或子節點清單。 會維護節點的屬性。

  萬用字 `*` 隱藏所有。

* `sling:orderBefore` ( `String`)

  包含同層級節點的名稱，目前節點應位於該節點的前面。

這些屬性會影響對應/原始資源/屬性(來自 `/libs`)由覆蓋/覆寫使用(通常用於 `/apps`)。

### 建立結構 {#creating-the-structure}

若要建立覆蓋或覆寫，您需要在目的地底下重新建立具有對等結構的原始節點(通常是 `/apps`)。 例如：

* 覆蓋

   * Sites主控台的導覽專案定義（如邊欄中所示）的定義定義位於：

     `/libs/cq/core/content/nav/sites/jcr:title`

   * 若要覆蓋此節點，請建立下列節點：

     `/apps/cq/core/content/nav/sites`

     然後更新屬性 `jcr:title` 視需要。

* 覆寫

   * 文字主控台的觸控式對話方塊的定義定義如下：

     `/libs/foundation/components/text/cq:dialog`

   * 若要覆寫此節點，請建立下列節點 — 例如：

     `/apps/the-project/components/text/cq:dialog`

若要建立其中任何一個，您只需要重新建立骨架結構。 若要簡化重新建立結構，所有中間節點都可以是型別 `nt:unstructured` (它們不必反映原始節點型別；例如，在 `/libs`)。

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
>使用Sling Resource Merger時（即處理標準觸控式UI時），不建議從複製整個結構 `/libs` 因為這會導致太多資訊保留在 `/apps`. 以任何方式升級系統時，這可能會導致問題。

### 使用案例 {#use-cases}

這些功能搭配標準功能，可讓您：

* **新增屬性**

  屬性不存在於 `/libs` 定義，但在 `/apps` 覆蓋/覆寫。

   1. 在中建立對應的節點 `/apps`
   1. 在此節點上建立新屬性»

* **重新定義屬性（非自動建立的屬性）**

  屬性定義於 `/libs`，但中需要新值 `/apps` 覆蓋/覆寫。

   1. 在中建立對應的節點 `/apps`
   1. 在此節點上建立相符的屬性（在/底下） `apps`)

      * 根據Sling Resource Resolver設定，屬性會有優先順序。
      * 支援變更屬性型別。

        如果您使用的屬性型別與中使用的不同 `/libs`，則會使用您定義的屬性型別。

  >[!NOTE]
  >
  >支援變更屬性型別。

* **重新定義自動建立的屬性**

  依預設，自動建立的屬性(例如 `jcr:primaryType`)不受覆蓋/覆寫約束，以確保目前位於下的節點型別 `/libs` 已遵守。 若要強制覆蓋/覆寫，您必須在中重新建立節點 `/apps`，明確隱藏屬性並重新定義：

   1. 在下方建立對應的節點 `/apps` 搭配所需的 `jcr:primaryType`
   1. 建立屬性 `sling:hideProperties` 在該節點上，將值設定為自動建立屬性的值；例如， `jcr:primaryType`

      此屬性，在下定義 `/apps`，現在會優先於下定義者 `/libs`

* **重新定義節點及其子系**

  節點及其子系定義於 `/libs`，但中需要新設定 `/apps` 覆蓋/覆寫。

   1. 結合下列動作：

      1. 隱藏節點的子系（保留節點的屬性）
      1. 重新定義屬性/屬性

* **隱藏屬性**

  屬性定義於 `/libs`，但不需要 `/apps` 覆蓋/覆寫。

   1. 在中建立對應的節點 `/apps`
   1. 建立屬性 `sling:hideProperties` 型別 `String` 或 `String[]`. 使用此選項可指定要隱藏/忽略的屬性。 也可以使用萬用字元。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子系**

  節點及其子系定義於 `/libs`，但不需要 `/apps` 覆蓋/覆寫。

   1. 在/apps下建立對應的節點
   1. 建立屬性 `sling:hideResource`

      * 類型: `Boolean`
      * 值: `true`

* **隱藏節點的子系（同時保留節點的屬性）**

  節點、其屬性及其子系定義於 `/libs`. 節點及其屬性需要在 `/apps` 覆蓋/覆寫，但部分或全部子節點在中並非必要 `/apps` 覆蓋/覆寫。

   1. 在下方建立對應的節點 `/apps`
   1. 建立屬性 `sling:hideChildren`：

      * 類型: `String[]`
      * 值：子節點的清單（如中所定義）。 `/libs`)以隱藏/忽略

      萬用字元&amp;ast；可用來隱藏/忽略所有子節點。

* **重新排序節點**

  節點及其同層級定義於 `/libs`. 需要新位置，才能在中重新建立節點 `/apps` 覆蓋/覆寫，其中新位置是參照中適當的同層級節點來定義 `/libs`.

   * 使用 `sling:orderBefore` 屬性：

      1. 在下方建立對應的節點 `/apps`
      1. 建立屬性 `sling:orderBefore`：

         這會指定節點(如 `/libs`)，而目前節點應放置在下列位置之前：

         * 類型: `String`
         * 值: `<before-SiblingName>`

### 從您的程式碼叫用Sling資源合併器 {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger包含兩個自訂資源提供者 — 一個用於覆蓋，另一個用於覆蓋。 您可以使用掛接點，在程式碼中叫用下列各項：

>[!NOTE]
>
>存取資源時，建議使用適當的掛載點。
>
>這可確保叫用Sling資源合併器並傳回完全合併的資源(減少需要複製的結構 `/libs`)。

* 覆蓋:

   * 用途：根據搜尋路徑合併資源
   * 掛接點： `/mnt/overlay`
   * 使用狀況： `mount point + relative path`
   * 範例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫:

   * 用途：根據資源的超級型別合併資源
   * 掛接點： `/mnt/overide`
   * 使用狀況： `mount point + absolute path`
   * 範例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

