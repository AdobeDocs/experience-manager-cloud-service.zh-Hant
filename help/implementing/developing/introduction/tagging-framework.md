---
title: AEM 標記框架
description: 標籤內容，並使用AEM標籤基礎結構來分類及組織內容。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# AEM標籤架構 {#aem-tagging-framework}

標籤可讓內容分類並整理。 標籤可以依名稱空間和分類法來分類。 如需使用標籤的詳細資訊：

* 另請參閱 [使用標籤](/help/sites-cloud/authoring/features/tags.md) 有關將內容標籤為內容作者的資訊。
* 請參閱管理標籤，以取得管理員對於建立和管理標籤以及已對哪些內容套用標籤的觀點。

本文主要介紹在AEM中支援標籤的基本架構，以及如何作為開發人員使用它。

## 簡介 {#introduction}

若要標籤內容並使用AEM標籤基礎架構：

* 標籤必須存在為型別的節點 [`cq:Tag`](#cq-tag-node-type) 在 [分類根節點。](#taxonomy-root-node)
* 標籤的內容節點 `NodeType` 必須包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* 此 [`TagID`](#tagid) 會新增至內容節點的 [`cq:tags`](#cq-tags-property) 屬性並解析為型別的節點 [`cq:Tag`.](#cq-tag-node-type)

## cq：Tag節點型別 {#cq-tag-node-type}

標籤的宣告會擷取到儲存庫中的型別節點中 `cq:Tag.`

* 標籤可以是一個簡單的單字(例如， `sky`)或代表階層式分類法(例如， `fruit/apple`，代表類屬水果和更具體的蘋果)。
* 標籤由唯一的 `TagID`.
* 標籤具有可選的中繼資訊，例如標題、當地語系化的標題和說明。 標題應顯示在使用者介面中，而非 `TagID`，當出現時。

標籤架構也限製作者和網站訪客只能使用特定的預先定義標籤。

### 標籤特性 {#tag-characteristics}

* 節點型別為 `cq:Tag`.
* 節點名稱是 [`TagID`.](#tagid)
* 此 [`TagID`](#tagid) 一律包含 [名稱空間。](#tag-namespace)
* 此 `jcr:title` 屬性（要在UI中顯示的標題）為選用。
* 此 `jcr:description` 屬性為選用。
* 包含子節點時，稱為 [容器標籤。](#container-tags)
* 標籤儲存在存放庫中，位於名為的基本路徑下方 [分類根節點。](#taxonomy-root-node)

### 標記 ID {#tagid}

A `TagID` 會識別解析成存放庫中的標籤節點的路徑。

通常 `TagID` 是速記 `TagID` 從名稱空間開始，或者可以是絕對的 `TagID` 從 [分類根節點。](#taxonomy-root-node)

標籤內容時，如果內容尚不存在， [`cq:tags`](#cq-tags-property) 屬性會新增至內容節點，且 `TagID` 會新增至屬性的 `String` 陣列值。

此 `TagID` 由下列專案組成： [名稱空間](#tag-namespace) 後面跟著本機 `TagID`. [容器標籤](#container-tags) 具有代表分類法中階層順序的子標籤。 子標籤可用於參照與任何本機標籤相同的標籤 `TagID`. 例如，使用標籤內容 `fruit` 即使容器標籤具有子標籤(例如 `fruit/apple` 和 `fruit/banana`.

### 分類根節點 {#taxonomy-root-node}

分類根節點是存放庫中所有標籤的基本路徑。 分類根節點必須 *非* 為型別節點 `cq:Tag`.

在AEM中，基底路徑為 `/content/cq:tags` 並且根節點的型別為 `cq:Folder`.

### 標籤名稱空間 {#tag-namespace}

名稱空間可讓您將專案分組。 最典型的使用案例是每個網站或大型應用程式（例如網站或資產）都有一個名稱空間（例如公開與內部），但名稱空間可用於各種其他需求。 在使用者介面中使用名稱空間，以僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的名稱空間是分類子樹狀結構中的第一個層級，也就是緊接在 [分類根節點。](#taxonomy-root-node) 名稱空間是型別的節點 `cq:Tag` 其父項不是 `cq:Tag` 節點型別。

所有標籤都有名稱空間。 如果未指定名稱空間，則會將標籤指派給預設名稱空間，也就是 `TagID` `default`，也就是 `/content/cq:tags/default`. 標題預設為 `Standard Tags`在這種情況下。

### 容器標籤 {#container-tags}

容器標籤是型別的節點 `cq:Tag` 包含任何數量及型別的子節點，可利用自訂中繼資料增強標籤模型。

此外，分類法中的容器標籤（或超級標籤）可作為所有子標籤的彙總。 例如，內容標籤為 `fruit/apple` 視為已標籤 `fruit`也一樣。 也就是說，搜尋標籤有 `fruit` 也會找到標籤了的內容 `fruit/apple`.

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號(`:`)時，冒號會將名稱空間與標籤或子分類法分開，然後再以一般斜線(`/`)。 如果標籤ID沒有冒號，則會隱含預設名稱空間。

以下為標準且唯一的標籤位置 `/content/cq:tags`.

標籤會參照不存在的路徑，或不指向 `cq:Tag` 節點會視為無效，並予以忽略。

下表顯示一些範例 `TagID`s、其元素，以及如何 `TagID` 解析為存放庫中的絕對路徑：

| `TagID` | 命名空間 | 本機ID | 容器標籤 | 分葉標籤 | 存放庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`，`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | （無） | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | （無） | （無） | （無） | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 標籤標題本地化 {#localization-of-tag-title}

當標籤包含選用標題字串時 `jcr:title`，即可新增屬性，將標題當地語系化以供顯示 `jcr:title.<locale>`.

如需詳細資訊，請參閱下列內容：

* [不同語言的標籤](tagging-applications.md#tags-in-different-languages) 說明開發人員如何使用API
* 管理不同語言的標籤，說明以管理員身分使用「標籤」主控台

### 存取控制 {#access-control}

標籤會作為節點存在於下的存放庫中 [分類根節點。](#taxonomy-root-node) 若要允許或拒絕作者和網站訪客在指定的名稱空間中建立標籤，可在存放庫中設定適當的ACL。

拒絕某些標籤或名稱空間的讀取許可權會控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許 `tag-administrators` 對所有名稱空間的群組/角色寫入存取權(新增/修改 `/content/cq:tags`)。 此群組隨附AEM立即可用。
* 允許使用者/作者讀取他們應可讀取的所有名稱空間（幾乎全部）。
* 允許使用者/作者寫入存取這些名稱空間的許可權，標籤應該可由使用者/作者自由定義(`add_node` 在 `/content/cq:tags/some_namespace`)

## 可標籤的內容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

若要讓應用程式開發人員將標籤附加至內容型別，則節點的註冊([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必須包含 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin。

此 `cq:OwnerTaggable` mixin，繼承自 `cq:Taggable`，表示內容可由擁有者/作者分類。 在AEM中，它只是 `cq:PageContent` 節點。 此 `cq:OwnerTaggable` 標籤框架不需要mixin。

>[!NOTE]
>
>建議僅在彙總內容專案的頂層節點（或其節點）上啟用標籤 `jcr:content` 節點)。 例如：
>
>* 頁面(`cq:Page`)其中 `jcr:content`節點屬於型別 `cq:PageContent`，包括 `cq:Taggable` mixin。
>* 資產(`cq:Asset`)其中 `jcr:content/metadata` 節點一律具有 `cq:Taggable` mixin。

### 節點型別標籤法(CND) {#node-type-notation-cnd}

節點型別定義以CND檔案的形式存在於存放庫中。 CND標籤法定義為 [JCR檔案](https://jackrabbit.apache.org/jcr/node-type-notation.html).

AEM中包含的「節點型別」的基本定義如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq：tags屬性 {#cq-tags-property}

此 `cq:tags` 屬性是 `String` 用來儲存一或多個的陣列 `TagID`當作者或網站訪客將變數套用至內容時。 屬性只有在新增至使用定義的節點時才有意義 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。

>[!NOTE]
>
>若要使用AEM標籤功能，自訂開發的應用程式不應定義以外的標籤屬性 `cq:tags`.

## 移動和合併標籤 {#moving-and-merging-tags}

以下說明使用「標籤」主控台移動或合併標籤時，在存放庫中所產生的效果。

將標籤A移動或合併到以下標籤B時 `/content/cq:tags`：

* 標籤A未刪除並接收 `cq:movedTo` 屬性。
   * `cq:movedTo` 指向標籤B。
   * 此屬性表示標籤A已移動或合併到標籤B中。
   * 移動標籤B會相應地更新此屬性。
   * 因此，標籤A會隱藏，並僅保留在存放庫中，以便解析指向標籤A的內容節點中的標籤ID。
   * 標籤記憶體回收行程會移除標籤A，如此一來，內容節點便不再指向這些標籤。
   * 的特殊值 `cq:movedTo` 屬性為 `nirvana`，此專案會在刪除標籤時套用，但無法從存放庫中移除，因為有子標籤具有 `cq:movedTo` 必須保留該值。

     >[!NOTE]
     >
     >此 `cq:movedTo` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
     >
     > 1. 標籤用於內容中（表示它有參考）。 或
     > 1. 標籤具有已移動的子系。
     >
* 標籤B已建立（如果有移動）並接收 `cq:backlinks` 屬性。
   * `cq:backlinks` 使參照保持在另一個方向。 也就是說，它會保留所有已移至標籤B或與標籤B合併的標籤清單。
   * 此功能大部分需要保留 `cq:movedTo` 屬性為最新的標籤B移動/合併/刪除或標籤B啟動時，其所有反向連結標籤也必須啟動。

     >[!NOTE]
     >
     >此 `cq:backlinks` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
     >
     > 1. 標籤用於內容中（表示它有參考），或
     > 1. 標籤具有已移動的子系。

讀取 `cq:tags` 內容節點的屬性涉及以下解析度：

1. 如果底下沒有相符專案 `/content/cq:tags`，不會傳回任何標籤。
1. 如果標籤具有 `cq:movedTo` 屬性集，會接著參考的標籤ID。
   * 只要後續的標籤具有 `cq:movedTo` 屬性。
1. 如果追蹤的標籤沒有 `cq:movedTo` 屬性，則會讀取標籤。

若要在移動或合併標籤時發佈變更， `cq:Tag` 節點及其所有反向連結都必須複製。 在標籤管理控制檯中啟動標籤時，會自動完成此復寫。

稍後對頁面的 `cq:tags` 屬性會自動清除舊參照。 會觸發清除，因為透過API解析移動的標籤會傳回目的地標籤，因此會提供目的地標籤ID。
