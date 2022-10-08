---
title: AEM標籤架構
description: 標籤內容並運用AEM標籤基礎架構，以便加以分類和組織。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# AEM標籤架構 {#aem-tagging-framework}

標籤可讓內容分類和組織。 標籤可依命名空間和分類法來分類。 如需使用標籤的詳細資訊：

* 請參閱 [使用標籤](/help/sites-cloud/authoring/features/tags.md) 以取得將內容標籤為內容作者的相關資訊。
* 請參閱管理標籤，以了解管理員關於建立和管理標籤的觀點，以及已套用哪些內容標籤。

本文著重於支援在AEM中標籤的基礎架構，以及如何以開發人員的身分運用它。

## 簡介 {#introduction}

若要標籤內容並運用AEM標籤基礎結構：

* 標籤必須存在為類型的節點 [`cq:Tag`](#cq-tag-node-type) 在 [分類根節點。](#taxonomy-root-node)
* 標籤的內容節點 `NodeType` 必須包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 米辛。
* 此 [`TagID`](#tagid) 會新增至內容節點的 [`cq:tags`](#cq-tags-property) 屬性，並解析到類型的節點 [`cq:Tag`.](#cq-tag-node-type)

## cq：標籤節點類型 {#cq-tag-node-type}

標籤的聲明被捕獲到儲存庫中類型的節點中 `cq:Tag.`

* 標籤可以是簡單的字詞(例如 `sky`)或代表階層分類法(例如 `fruit/apple`，表示通用水果和更具體的蘋果)。
* 標籤以不重複 `TagID`.
* 標籤包含選用的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非 `TagID`，若存在。

標籤架構也能限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性 {#tag-characteristics}

* 節點類型為 `cq:Tag`.
* 節點名稱是 [`TagID`.](#tagid)
* 此 [`TagID`](#tagid) 一律包含 [命名空間。](#tag-namespace)
* 此 `jcr:title` 屬性（UI中顯示的標題）為選用。
* 此 `jcr:description` 屬性為選用。
* 包含子節點時，稱為 [容器標籤。](#container-tags)
* 標籤會儲存在存放庫中，位於名為 [分類根節點。](#taxonomy-root-node)

### 標記 ID {#tagid}

A `TagID` 標識解析到儲存庫中標籤節點的路徑。

通常， `TagID` 是速記 `TagID` 從命名空間開始，或者它可以是絕對的 `TagID` 從 [分類根節點。](#taxonomy-root-node)

當內容經過標籤時，如果內容尚未存在，則 [`cq:tags`](#cq-tags-property) 屬性會新增至內容節點，而 `TagID` 會新增至屬性的 `String` 陣列值。

此 `TagID` 包含a [命名空間](#tag-namespace) 接著是當地 `TagID`. [容器標籤](#container-tags) 具有子標籤，該子標籤表示分類中的分層順序。 子標籤可用來參照與任何本機標籤相同的標籤 `TagID`. 例如，將內容標籤為 `fruit` 即使是具有子標籤的容器標籤，例如 `fruit/apple` 和 `fruit/banana`.

### 分類根節點 {#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點必須 *not* 是類型的節點 `cq:Tag`.

在AEM中，基本路徑為 `/content/cq:tags` 根節點是 `cq:Folder`.

### 標籤命名空間 {#tag-namespace}

命名空間可將項目分組。 最典型的使用案例是每個網站（例如公用與內部）或每個大型應用程式（例如網站或資產）都有命名空間，但命名空間可用於各種其他需求。 使用者介面中會使用命名空間，以僅顯示適用於目前內容的標籤子集（即特定命名空間的標籤）。

標籤的命名空間是分類子樹狀結構中的第一層，也就是緊接在 [分類根節點。](#taxonomy-root-node) 命名空間是一種節點 `cq:Tag` 其父母 `cq:Tag` 節點類型。

所有標籤都有命名空間。 若未指定命名空間，則會將標籤指派給預設命名空間，也就是 `TagID` `default`，即 `/content/cq:tags/default`.  標題預設為 `Standard Tags`在這種情況下。

### 容器標籤 {#container-tags}

容器標籤是類型的節點 `cq:Tag` 包含任何數目和類型的子節點，因此可以使用自訂中繼資料增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，標示為 `fruit/apple` 被視為已加上 `fruit` 同樣，也就是搜尋只加上標籤的內容 `fruit` 也會找到標籤了的內容 `fruit/apple`.

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號(`:`)，冒號會將命名空間與標籤或子分類法分開，然後以一般斜線(`/`)。 如果標籤ID沒有冒號，表示預設命名空間。

標籤的標準且唯一位置如下所示 `/content/cq:tags`.

標籤會參考未指向 `cq:Tag` 節點被視為無效，且會被忽略。

下表顯示一些範例 `TagID`s，它們的元素，以及 `TagID` 解析至儲存庫中的絕對路徑：

| `TagID` | 命名空間 | 本機ID | 容器標籤 | 葉標籤 | 儲存庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (無) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (無) | (無) | (無) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 標籤標題的本地化 {#localization-of-tag-title}

標籤包含選用的標題字串時 `jcr:title`，則可新增屬性，將顯示的標題當地化 `jcr:title.<locale>`.

如需更多詳細資訊，請參閱：

* [不同語言的標籤，](tagging-applications.md#tags-in-different-languages) 說明如何以開發人員身分使用API
* 管理不同語言的標籤，說明如何以管理員身分使用「標籤」控制台

### 存取控制 {#access-control}

標籤存在於存放庫的 [分類根節點。](#taxonomy-root-node) 您可以在存放庫中設定適當的ACL，借此允許或拒絕作者和網站訪客在指定命名空間中建立標籤。

拒絕某些標籤或命名空間的讀取權限將控制將標籤應用於特定內容的能力。

典型做法包括：

* 允許 `tag-administrators` 組/角色寫入訪問所有命名空間(在 `/content/cq:tags`)。 此群組隨附AEM現成可用。
* 允許使用者/作者讀取應讀取之所有命名空間的存取權（大多為）。
* 允許使用者/作者撰寫存取使用者/作者應可自由定義標籤的命名空間(`add_node` 在 `/content/cq:tags/some_namespace`)

## 可標籤內容：cq：可標籤的Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包含 `cq:Taggable` mixin或 `cq:OwnerTaggable` 米辛。

此 `cq:OwnerTaggable` mixin，它繼承自 `cq:Taggable`，旨在指出內容可由擁有者/作者分類。 在AEM中，它只是 `cq:PageContent` 節點。 此 `cq:OwnerTaggable` 標籤架構不需要mixin。

>[!NOTE]
>
>建議只在匯總內容項目的頂層節點（或其上）上啟用標籤 `jcr:content` 節點)。 範例包括：
>
>* 頁面(`cq:Page`)，其中 `jcr:content`節點的類型 `cq:PageContent`，包括 `cq:Taggable` 米辛。
>* 資產(`cq:Asset`)，其中 `jcr:content/metadata` 節點總是有 `cq:Taggable` 米辛。


### 節點類型標籤法(CND) {#node-type-notation-cnd}

儲存庫中的節點類型定義以CND檔案的形式存在。 CND標籤法定義為 [JCR檔案。](https://jackrabbit.apache.org/node-type-notation.html).

AEM中包含之節點類型的基本定義如下：

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

## cq:tags屬性 {#cq-tags-property}

此 `cq:tags` 屬性為 `String` 用於儲存一或多個陣列 `TagID`是否由作者或網站訪客套用至內容時。 只有在新增至以 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 米辛。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義標籤屬性， `cq:tags`.

## 移動及合併標籤 {#moving-and-merging-tags}

以下說明使用「標籤」控制台移動或合併標籤時，儲存庫中的效果。

標籤A移動或合併至標籤B時，於 `/content/cq:tags`:

* 標籤A未刪除，且會收到 `cq:movedTo` 屬性。
   * `cq:movedTo` 指向標籤B。
   * 此屬性表示標籤A已移動或合併至標籤B。
   * 移動標籤B會據此更新此屬性。
   * 因此，標籤A會隱藏，並僅保留在存放庫中，以解析指向標籤A的內容節點中的標籤ID。
   * 標籤垃圾收集器會再次移除標籤A之類的標籤，不再將內容節點指向它們。
   * 的特殊值 `cq:movedTo` 屬性為 `nirvana`，此標籤會在標籤刪除時套用，但無法從存放庫中移除，因為存在具有的子標籤 `cq:movedTo` 必須保留。

      >[!NOTE]
      >
      >此 `cq:movedTo` 只有在符合下列任一條件時，才會將屬性新增至移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即有參考）。 或
      > 1. 標籤包含已移動的子項。

* 標籤B會建立（若是移動）並接收 `cq:backlinks` 屬性。
   * `cq:backlinks` 保留反向的參照，即保留已移至標籤B或與標籤B合併的所有標籤的清單。
   * 這主要是為了保留 `cq:movedTo` 屬性，直到標籤B移動/合併/刪除或標籤B啟動時為止，在此情況下，其所有反向連結標籤也必須啟動。

      >[!NOTE]
      >
      >此 `cq:backlinks` 只有在符合下列任一條件時，才會將屬性新增至移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即有參考）。 或
      > 1. 標籤包含已移動的子項。


閱讀 `cq:tags` 內容節點的屬性包含下列解析度：

1. 如果下沒有匹配項 `/content/cq:tags`，則不會傳回任何標籤。
1. 如果標籤具有 `cq:movedTo` 屬性集，則會遵循參考的標籤ID。
   * 只要後面的標籤具有 `cq:movedTo` 屬性。
1. 如果後面的標籤沒有 `cq:movedTo` 屬性，則會讀取標籤。

若要在移動或合併標籤時發佈變更， `cq:Tag` 節點及其所有反向連結都必須複製。 在標籤管理主控台中啟動標籤時，就會自動完成這項作業。

稍後更新頁面的 `cq:tags` 屬性會自動清除舊的參考。 觸發此動作是因為透過API解析移動的標籤會傳回目的地標籤，因而提供目的地標籤ID。
