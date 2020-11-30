---
title: AEM標籤架構
description: 標籤內容並運用AEM標籤基礎架構，以便對內容進行分類和組織。
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# AEM標籤架構 {#aem-tagging-framework}

標籤可讓內容分類和組織。 標籤可以按命名空間和分類法分類。 如需使用標籤的詳細資訊：

* 如需 [](/help/sites-cloud/authoring/features/tags.md) 將內容標籤為內容作者的詳細資訊，請參閱使用標籤。
* 請參閱管理標籤，以瞭解管理員建立和管理標籤的觀點，以及已套用內容標籤的觀點。

本文著重說明在AEM中支援標籤的基礎架構，以及如何以開發人員的身分運用它。

## 簡介 {#introduction}

若要標籤內容並運用AEM標籤基礎架構：

* 標籤必須作為分類根節點下 [`cq:Tag`](#cq-tag-node-type) 的類 [型節點存在。](#taxonomy-root-node)
* 標籤的內容節點必 `NodeType` 須包含混 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 音。
* 將 [`TagID`](#tagid) 添加到內容節點的屬性 [`cq:tags`](#cq-tags-property) 中，並解析到類型的節點 [`cq:Tag`。](#cq-tag-node-type)

## cq：標籤節點類型 {#cq-tag-node-type}

標籤的聲明在儲存庫中捕獲，其類型為 `cq:Tag.`

* 標籤可以是簡單字詞(例如 `sky`)或表示階層分類法(例如 `fruit/apple`，即通用水果和更具體的蘋果)。
* 標籤由唯一標籤識 `TagID`別。
* 標籤包含可選的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非 `TagID`顯示時。

標籤框架也能夠限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性 {#tag-characteristics}

* 節點類型為 `cq:Tag`。
* 節點名稱是的元件 [`TagID`。](#tagid)
* 一律 [`TagID`](#tagid) 包含命名 [空間。](#tag-namespace)
* 屬 `jcr:title` 性（要在UI中顯示的標題）是選用的。
* 屬 `jcr:description` 性為可選。
* 包含子節點時，稱為容 [器標籤。](#container-tags)
* 標籤儲存在名為分類根節點的基本路徑下的 [儲存庫中。](#taxonomy-root-node)

### 標記 ID {#tagid}

標識 `TagID` 解析到儲存庫中標籤節點的路徑。

通常，是 `TagID` 從命名空 `TagID` 間開始的速記，也可以是從分類根節 `TagID` 點開始的 [絕對值。](#taxonomy-root-node)

標籤內容時，如果內容尚不存在，則 [`cq:tags`](#cq-tags-property) 會將屬性添加到內容節點，並 `TagID` 將其添加到屬性的 `String` 陣列值。

包含 `TagID` 一個名 [稱空間](#tag-namespace) ，後面跟著本地 `TagID`。 [容器標籤](#container-tags) ，具有子標籤，代表分類法中的階層順序。 子標籤可用來參照與任何本機標籤相同的標籤 `TagID`。 例如，允許將內 `fruit` 容標籤為子標籤（例如和）的容器標 `fruit/apple` 記 `fruit/banana`。

### 分類根節點 {#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點不 *能* 是類型的節點 `cq:Tag`。

在AEM中，基本路徑為 `/content/cq:tags` 根節點類型 `cq:Folder`。

### 標籤命名空間 {#tag-namespace}

名稱空間允許將事物分組。 最典型的使用案例是每個網站（例如公用與內部）或每個較大的應用程式（例如網站或資產）擁有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用名稱空間，僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的命名空間是分類子樹中的第一級，該子樹是緊接在分類根節點下 [的節點。](#taxonomy-root-node) namespace是父代不是節 `cq:Tag` 點類型的節 `cq:Tag` 點類型。

所有標籤都有命名空間。 如果未指定命名空間，則標籤會指派給預設命名空 `TagID` 間， `default`即： `/content/cq:tags/default`.  在這類情況下，「標 `Standard Tags`題」預設為。

### 容器標籤 {#container-tags}

容器標籤是包含任意數 `cq:Tag` 目和類型子節點的類型節點，因此可以使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，標籤為 `fruit/apple` 的內容也被視為標籤為 `fruit` 標籤，即搜索僅標籤為的內容 `fruit` 也會找到標籤為的內容 `fruit/apple`

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號(`:`)，冒號會將命名空間與標籤或子分類分類分開，然後使用正常斜線(`/`)分隔。 如果標籤ID沒有冒號，則會隱含預設命名空間。

標籤的標準且唯一位置如下 `/content/cq:tags`。

參照不指向節點的非現有路徑或路徑的標籤會 `cq:Tag` 被視為無效且被忽略。

下表顯示了一些示 `TagID`例、其元素，以及解析到儲存庫 `TagID` 中絕對路徑的方式：

| `TagID` | 命名空間 | 本機ID | 容器標籤 | 葉標籤 | 儲存庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (無) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (無) | (無) | (無) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 標籤標題的本地化 {#localization-of-tag-title}

當標籤包含可選的標題字串 `jcr:title`時，可透過新增屬性來本地化要顯示的標題 `jcr:title.<locale>`。

如需詳細資訊，請參閱：

* [「不同語言的標籤](tagging-applications.md#tags-in-different-languages) 」，說明API做為開發人員的使用
* 管理不同語言的標籤，其中說明以管理員身份使用標籤控制台

### 存取控制 {#access-control}

標籤作為分類根節點下的儲存庫 [中的節點存在。](#taxonomy-root-node) 允許或拒絕作者和站點訪客在給定名稱空間中建立標籤，可以通過在儲存庫中設定適當的ACL來實現。

拒絕某些標籤或名稱空間的讀取權限將控制將標籤應用於特定內容的能力。

典型做法包括：

* 允許對所 `tag-administrators` 有名稱空間的組／角色寫訪問(在下添加／修 `/content/cq:tags`改)。 此群組隨附AEM現成可用功能。
* 允許用戶／作者讀取對所有應該對其可讀取的名稱空間（大部分）的訪問權。
* 允許使用者／作者對使用者／作者可自由定義標籤的命名空間進行寫入存取(在`add_node` 下 `/content/cq:tags/some_namespace`)

## 可標籤內容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加至內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包含 `cq:Taggable` mixin或mixin `cq:OwnerTaggable` 。

繼承 `cq:OwnerTaggable` 自的mixin旨在 `cq:Taggable`指出內容可由擁有者／作者分類。 在AEM中，它只是節點的屬 `cq:PageContent` 性。 標籤 `cq:OwnerTaggable` 框架不需要混合素。

>[!NOTE]
>
>建議僅在匯總內容項目（或其節點）的頂層節點上啟用 `jcr:content` 標籤。 範例包括：
>
>* 節點類`cq:Page`型的頁 `jcr:content`面(), `cq:PageContent`其中包含混 `cq:Taggable` 合。
>* 節點總`cq:Asset`有混合 `jcr:content/metadata` 項的資產( `cq:Taggable` )。


### 節點類型注釋(CND) {#node-type-notation-cnd}

節點類型定義作為CND檔案存在於儲存庫中。 CND符號定義為 [JCR文檔的一部分](https://jackrabbit.apache.org/node-type-notation.html)。

AEM中包含的「節點類型」基本定義如下：

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

屬 `cq:tags` 性是一個陣列， `String` 當作者或網站訪客將一或 `TagID`多個s套用至內容時，用來儲存這些s。 僅當將屬性添加到使用mixin定義的節點時，該屬性才有 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 意義。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義標籤屬性 `cq:tags`。

## 移動和合併標籤 {#moving-and-merging-tags}

以下是使用「標籤」控制台移動或合併標籤時儲存庫中效果的說明。

當標籤A被移動或合併到標籤B時，位於 `/content/cq:tags`:

* 標籤A不會刪除並接收屬 `cq:movedTo` 性。
   * `cq:movedTo` 指向標籤B。
   * 此屬性表示標籤A已移動或合併到標籤B。
   * 移動標籤B將相應地更新此屬性。
   * 標籤A因此會隱藏，並且僅保存在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。
   * 標籤廢棄項目收集器會移除標籤A等標籤，不再有內容節點指向標籤A。
   * 屬性的特殊 `cq:movedTo` 值是 `nirvana`，在刪除標籤時應用，但無法從儲存庫中刪除，因為必須保留具有子標籤 `cq:movedTo` 的子標籤。

      >[!NOTE]
      >
      >只有 `cq:movedTo` 符合下列任一條件時，才會將屬性新增至已移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即它有參考）。 或
      > 1. 標籤中有已移動的子項。


* 標籤B會建立（在移動時）並接收屬 `cq:backlinks` 性。
   * `cq:backlinks` 將參照保持在另一個方向，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。
   * 當移動／合併／刪除標 `cq:movedTo` 簽B時，或當標籤B啟動時，這通常需要保持屬性的最新狀態，在此情況下，其所有的回溯連結標籤也必須啟動。

      >[!NOTE]
      >
      >只有 `cq:backlinks` 符合下列任一條件時，才會將屬性新增至已移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即它有參考）。 或
      > 1. 標籤中有已移動的子項。


讀取內 `cq:tags` 容節點的屬性時，會涉及下列解析度：

1. 如果下方沒有相符項目 `/content/cq:tags`，則不會傳回標籤。
1. 如果標籤有屬性 `cq:movedTo` 集，則會遵循參考的標籤ID。
   * 只要後面的標籤有屬性，就會重複此 `cq:movedTo` 步驟。
1. 如果後面的標籤沒有屬 `cq:movedTo` 性，則讀取標籤。

若要在標籤已移動或合併時發佈變更，必須復 `cq:Tag` 制節點及其所有回溯連結。 當標籤在標籤管理主控台中啟動時，會自動完成此動作。

稍後頁面屬性的更新 `cq:tags` 會自動清除舊參照。 觸發此項是因為透過API解析移動的標籤會傳回目標標籤，因此提供目標標籤ID。
