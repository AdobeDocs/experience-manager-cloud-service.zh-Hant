---
title: AEM標籤架構
description: 標籤內容並運用AEM標籤基礎架構，以便對內容進行分類和組織。
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# AEM標籤框架{#aem-tagging-framework}

標籤可讓內容分類和組織。 標籤可以按命名空間和分類法分類。 如需使用標籤的詳細資訊：

* 如需將內容標籤為內容作者的詳細資訊，請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md)。
* 請參閱管理標籤，以瞭解管理員建立和管理標籤的觀點，以及已套用內容標籤的觀點。

本文著重說明在AEM中支援標籤的基礎架構，以及如何以開發人員的身分運用它。

## 簡介 {#introduction}

若要標籤內容並運用AEM標籤基礎架構：

* 標籤必須作為[分類根節點下[`cq:Tag`](#cq-tag-node-type)類型的節點存在。](#taxonomy-root-node)
* 標籤的內容節點的`NodeType`必須包含[`cq:Taggable`](#taggable-content-cq-taggable-mixin)混音。
* 將[`TagID`](#tagid)添加到內容節點的[`cq:tags`](#cq-tags-property)屬性，並解析到類型[`cq:Tag`的節點。](#cq-tag-node-type)

## cq：標籤節點類型{#cq-tag-node-type}

標籤的聲明在`cq:Tag.`類型的節點中在儲存庫中捕獲

* 標籤可以是簡單字詞(例如`sky`)或表示階層分類(例如`fruit/apple`，表示一般水果和更特定的蘋果)。
* 標籤由唯一`TagID`識別。
* 標籤包含可選的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非`TagID`（若有）。

標籤框架也能夠限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性{#tag-characteristics}

* 節點類型為`cq:Tag`。
* 節點名稱是[`TagID`的元件。](#tagid)
* [`TagID`](#tagid)一律包含[namespace。](#tag-namespace)
* `jcr:title`屬性（要在UI中顯示的標題）為選用。
* `jcr:description`屬性是可選的。
* 包含子節點時，稱為[容器標籤。](#container-tags)
* 標籤儲存在名為[分類根節點的基本路徑下的儲存庫中。](#taxonomy-root-node)

### 標記 ID {#tagid}

`TagID`標識解析到儲存庫中標籤節點的路徑。

通常，`TagID`是從命名空間開始的速記`TagID`，或者可以是從[分類根節點開始的絕對`TagID`。](#taxonomy-root-node)

當標籤內容時，如果該內容尚不存在，則[`cq:tags`](#cq-tags-property)屬性將添加到內容節點中，而`TagID`將添加到屬性的`String`陣列值中。

`TagID`由[namespace](#tag-namespace)組成，後面接著本機`TagID`。 [容器](#container-tags) 標語子標籤，代表分類法中的階層順序。子標籤可用於引用與任何本地`TagID`相同的標籤。 例如，允許使用`fruit`標籤內容，即使它是具有子標籤的容器標籤，例如`fruit/apple`和`fruit/banana`。

### 分類根節點{#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點必須&#x200B;*not*&#x200B;是類型`cq:Tag`的節點。

在AEM中，基本路徑為`/content/cq:tags`，根節點的類型為`cq:Folder`。

### 標籤命名空間{#tag-namespace}

名稱空間允許將事物分組。 最典型的使用案例是每個網站（例如公用與內部）或每個較大的應用程式（例如網站或資產）擁有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用名稱空間，僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的命名空間是分類子樹中的第一級，該子樹是緊接在[分類根節點下方的節點。](#taxonomy-root-node) namespace是父代不是節 `cq:Tag` 點類型的節 `cq:Tag` 點類型。

所有標籤都有命名空間。 如果未指定命名空間，則標籤會指派給預設命名空間，即`TagID` `default`，亦即。`/content/cq:tags/default`。  在這種情況下，「標題」預設為`Standard Tags`。

### 容器標籤{#container-tags}

容器標籤是`cq:Tag`類型的節點，包含任意數目和類型的子節點，因此可以使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，使用`fruit/apple`標籤的內容也被視為使用`fruit`標籤，即，搜尋僅使用`fruit`標籤的內容也會找到使用`fruit/apple`標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號(`:`)，冒號會將命名空間與標籤或子分類分類分開，然後使用正常斜槓(`/`)分隔。 如果標籤ID沒有冒號，則會隱含預設命名空間。

標籤的標準和唯一位置在`/content/cq:tags`以下。

引用不指向`cq:Tag`節點的非現有路徑或路徑的標籤被視為無效，並被忽略。

下表顯示了一些示例`TagID`s、其元素，以及`TagID`如何解析為儲存庫中的絕對路徑：

| `TagID` | 命名空間 | 本機ID | 容器標籤 | 葉標籤 | 儲存庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (無) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (無) | (無) | (無) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 標籤標題的本地化{#localization-of-tag-title}

當標籤包含可選的標題字串`jcr:title`時，可以通過添加屬性`jcr:title.<locale>`來本地化要顯示的標題。

如需詳細資訊，請參閱：

* [不同語言的標](tagging-applications.md#tags-in-different-languages) 簽，說明API做為開發人員的使用
* 管理不同語言的標籤，其中說明以管理員身份使用標籤控制台

### 存取控制 {#access-control}

標籤在[分類根節點下作為儲存庫中的節點存在。](#taxonomy-root-node) 允許或拒絕作者和站點訪客在給定名稱空間中建立標籤，可以通過在儲存庫中設定適當的ACL來實現。

拒絕某些標籤或名稱空間的讀取權限將控制將標籤應用於特定內容的能力。

典型做法包括：

* 允許對所有名稱空間（在`/content/cq:tags`下添加／修改）的`tag-administrators`組／角色寫訪問。 此群組隨附AEM現成可用功能。
* 允許用戶／作者讀取對所有應該對其可讀取的名稱空間（大部分）的訪問權。
* 允許用戶／作者對用戶／作者可自由定義標籤的名稱空間進行寫入訪問（`/content/cq:tags/some_namespace`下的`add_node`）

## 可標籤內容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包括`cq:Taggable`混合或`cq:OwnerTaggable`混合。

`cq:OwnerTaggable` mixin繼承自`cq:Taggable`，其目的是指出內容可由擁有者／作者分類。 在AEM中，它只是`cq:PageContent`節點的屬性。 標籤框架不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建議僅在匯總內容項的頂層節點（或其`jcr:content`節點）上啟用標籤。 範例包括：
>
>* 其中`jcr:content`節點類型`cq:PageContent`的頁面(`cq:Page`)，其中包含`cq:Taggable`混音。
>* `jcr:content/metadata`節點一律具有`cq:Taggable`混音的資產(`cq:Asset`)。


### 節點類型標籤(CND){#node-type-notation-cnd}

節點類型定義作為CND檔案存在於儲存庫中。 CND符號定義為[JCR文檔的一部分。](https://jackrabbit.apache.org/node-type-notation.html)。

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

## cq:tags屬性{#cq-tags-property}

`cq:tags`屬性是`String`陣列，用於在作者或網站訪客將`TagID`套用至內容時儲存一或多個&lt;a2/>。 該屬性僅在添加到以[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin定義的節點時有意義。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義`cq:tags`以外的標籤屬性。

## 移動和合併標籤{#moving-and-merging-tags}

以下是使用「標籤」控制台移動或合併標籤時儲存庫中效果的說明。

將標籤A移動或合併到`/content/cq:tags`下的標籤B時：

* 標籤A未刪除，並接收`cq:movedTo`屬性。
   * `cq:movedTo` 指向標籤B。
   * 此屬性表示標籤A已移動或合併到標籤B。
   * 移動標籤B將相應地更新此屬性。
   * 標籤A因此會隱藏，並且僅保存在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。
   * 標籤廢棄項目收集器會移除標籤A等標籤，不再有內容節點指向標籤A。
   * `cq:movedTo`屬性的特殊值是`nirvana`，該值在標籤刪除時應用，但無法從儲存庫中刪除，因為必須保留具有`cq:movedTo`的子標籤。

      >[!NOTE]
      >
      >`cq:movedTo`屬性只會在符合下列任一條件時，新增至已移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即它有參考）。 或
      > 1. 標籤中有已移動的子項。


* 標籤B已建立（在移動的情況下）並接收`cq:backlinks`屬性。
   * `cq:backlinks` 將參照保持在另一個方向，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。
   * 當標籤B被移動／合併／刪除或標籤B被激活時，這通常是保持`cq:movedTo`屬性保持最新的必需項，在這種情況下，其所有的回溯標籤也必須被激活。

      >[!NOTE]
      >
      >`cq:backlinks`屬性只會在符合下列任一條件時，新增至已移動或合併的標籤：
      >
      > 1. 標籤用於內容（亦即它有參考）。 或
      > 1. 標籤中有已移動的子項。


讀取內容節點的`cq:tags`屬性涉及以下解析度：

1. 如果`/content/cq:tags`下沒有相符項目，則不會傳回任何標籤。
1. 如果標籤具有`cq:movedTo`屬性集，則會遵循參考的標籤ID。
   * 只要後面的標籤有`cq:movedTo`屬性，就會重複此步驟。
1. 如果後面的標籤沒有`cq:movedTo`屬性，則會讀取標籤。

要在標籤已移動或合併時發佈更改，必須複製`cq:Tag`節點及其所有回鏈。 當標籤在標籤管理主控台中啟動時，會自動完成此動作。

稍後對頁面`cq:tags`屬性的更新會自動清除舊參照。 觸發此項是因為透過API解析移動的標籤會傳回目標標籤，因此提供目標標籤ID。
