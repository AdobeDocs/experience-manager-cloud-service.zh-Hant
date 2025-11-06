---
title: AEM 標記框架
description: 標籤內容，並使用AEM標籤基礎結構來分類及組織內容。
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# AEM標籤架構 {#aem-tagging-framework}

標籤可讓內容分類並整理。 標籤可以依名稱空間和分類法來分類。 如需使用標籤的詳細資訊：

* 請參閱[使用標籤](/help/sites-cloud/authoring/sites-console/tags.md)，以取得將內容標籤為內容作者的相關資訊。
* 請參閱管理標籤，以取得管理員對於建立和管理標籤以及已對哪些內容套用標籤的觀點。

本文主要說明在AEM中支援標籤的基本架構，以及如何以開發人員身分使用。

## 簡介 {#introduction}

若要標籤內容並使用AEM標籤基礎結構：

* 標籤必須以[`cq:Tag`](#cq-tag-node-type)分類根節點[下型別](#taxonomy-root-node)的節點存在。
* 標籤的內容節點的`NodeType`必須包含[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* [`TagID`](#tagid)已新增至內容節點的[`cq:tags`](#cq-tags-property)屬性，並解析為型別[`cq:Tag`](#cq-tag-node-type)的節點。

## cq:Tag節點型別 {#cq-tag-node-type}

標籤宣告是在型別`cq:Tag.`的節點的儲存庫中擷取的

* 標籤可以是簡單的單字（例如，`sky`），或代表階層式分類法（例如，`fruit/apple`，表示一般水果和更具體的蘋果）。
* 標籤由唯一的`TagID`識別。
* 標籤具有可選的中繼資訊，例如標題、當地語系化的標題和說明。 當出現時，標題應該顯示在使用者介面中，而非`TagID`。

標籤架構也限製作者和網站訪客只能使用特定的預先定義標籤。

### 標籤特性 {#tag-characteristics}

* 節點型別為`cq:Tag`。
* 節點名稱是[`TagID`](#tagid)的元件。
* [`TagID`](#tagid)一律包含[名稱空間](#tag-namespace)。
* `jcr:title`屬性（顯示在UI中的標題）是選用的。
* `jcr:description`屬性是選用的。
* 包含子節點時，會稱為[容器標籤](#container-tags)。
* 標籤儲存在稱為[分類根節點](#taxonomy-root-node)的基底路徑下方的儲存庫中。

### 標記 ID {#tagid}

`TagID`會識別解析成存放庫中的標籤節點的路徑。

一般而言，`TagID`是以名稱空間開頭的速記`TagID`，或者可以是從`TagID`分類根節點[開始的絕對](#taxonomy-root-node)。

標籤內容時，如果內容尚不存在，[`cq:tags`](#cq-tags-property)屬性會新增至內容節點，而`TagID`會新增至屬性的`String`陣列值。

`TagID`包含[名稱空間](#tag-namespace)，後面接著本機`TagID`。 [容器標籤](#container-tags)的子標籤代表分類法中的階層順序。 子標籤可用於參照與任何本機`TagID`相同的標籤。 例如，允許使用`fruit`標籤內容，即使它是具有子標籤的容器標籤，例如`fruit/apple`和`fruit/banana`。

### 分類根節點 {#taxonomy-root-node}

分類根節點是存放庫中所有標籤的基本路徑。 分類根節點必須&#x200B;*不是*&#x200B;是型別`cq:Tag`的節點。

在AEM中，基底路徑為`/content/cq:tags`，而根節點的型別為`cq:Folder`。

### 標籤名稱空間 {#tag-namespace}

名稱空間可讓您將專案分組。 最典型的使用案例是每個網站或大型應用程式(例如網站或Assets)都有一個名稱空間（例如公用與內部），但名稱空間可用於各種其他需求。 在使用者介面中使用名稱空間，以僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的名稱空間是分類子樹狀結構中的第一個層級，它是[分類根節點](#taxonomy-root-node)正下方的節點。 名稱空間是型別`cq:Tag`的節點，其父系不是`cq:Tag`節點型別。

所有標籤都有名稱空間。 如果未指定名稱空間，則會將標籤指派給預設名稱空間`TagID` `default`，即`/content/cq:tags/default`。 在這種情況下，標題會預設為`Standard Tags`。

### 容器標籤 {#container-tags}

容器標籤是型別`cq:Tag`的節點，包含任何數目和型別的子節點，因此可以使用自訂中繼資料增強標籤模型。

此外，分類法中的容器標籤（或超級標籤）可作為所有子標籤的彙總。 例如，以`fruit/apple`標籤的內容也被視為以`fruit`標籤。 也就是說，搜尋以`fruit`標籤的內容也會找到以`fruit/apple`標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號(`:`)，冒號會將名稱空間與標籤或子分類分開，然後以一般斜線(`/`)分隔。 如果標籤ID沒有冒號，則會隱含預設名稱空間。

標籤的標準及唯一位置低於`/content/cq:tags`。

參照不存在的路徑或不指向`cq:Tag`節點的路徑的標籤會被視為無效並被忽略。

下表顯示一些範例`TagID`、其元素，以及`TagID`如何解析成存放庫中的絕對路徑：

| `TagID` | 命名空間 | 本機ID | 容器標籤 | 分葉標籤 | 存放庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`，`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | （無） | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | （無） | （無） | （無） | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### 標籤標題本地化 {#localization-of-tag-title}

當標籤包含選擇性標題字串`jcr:title`時，可以新增屬性`jcr:title.<locale>`來本地化顯示的標題。

如需詳細資訊，請參閱下列內容：

* 不同語言的[標籤](tagging-applications.md#tags-in-different-languages)說明開發人員如何使用API
* 管理不同語言的標籤，說明以管理員身分使用「標籤」主控台

### 存取控制 {#access-control}

標籤在[分類根節點](#taxonomy-root-node)下的儲存庫中作為節點存在。 若要允許或拒絕作者和網站訪客在指定的名稱空間中建立標籤，可在存放庫中設定適當的ACL。

拒絕某些標籤或名稱空間的讀取許可權會控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許`tag-administrators`群組/角色對所有名稱空間的寫入存取權（在`/content/cq:tags`下新增/修改）。 此群組隨附AEM立即可用。
* 允許使用者/作者讀取他們應可讀取的所有名稱空間（幾乎全部）。
* 允許使用者/作者寫入存取那些標籤應該可由使用者/作者自由定義的名稱空間（`add_node`下的`/content/cq:tags/some_namespace`）

## 可標籤的內容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

若要讓應用程式開發人員將標籤附加至內容型別，節點的註冊([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必須包含`cq:Taggable` mixin或`cq:OwnerTaggable` mixin。

繼承自`cq:OwnerTaggable`的`cq:Taggable` mixin旨在表示內容可由擁有者/作者分類。 在AEM中，它只是`cq:PageContent`節點的屬性。 標籤架構不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建議僅在彙總內容專案的頂層節點（或其`jcr:content`節點）上啟用標籤。 例如：
>
>* `cq:Page`節點為`jcr:content`型別（包含`cq:PageContent` mixin）的頁面(`cq:Taggable`)。
>* Assets (`cq:Asset`)，其中`jcr:content/metadata`節點一律有`cq:Taggable` mixin。

### 節點型別標籤法(CND) {#node-type-notation-cnd}

節點型別定義以CND檔案的形式存在於存放庫中。 CND標籤法定義為[JCR檔案](https://jackrabbit.apache.org/jcr/node-type-notation.html)的一部分。

AEM中包含之節點型別的基本定義如下：

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

`cq:tags`屬性是`String`陣列，用來儲存作者或網站訪客套用至內容的一或多個`TagID`。 屬性只有在新增至使用[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin定義的節點時才有意義。

>[!NOTE]
>
>若要使用AEM標籤功能，自訂開發的應用程式不應定義`cq:tags`以外的標籤屬性。

## 移動和合併標籤 {#moving-and-merging-tags}

以下說明使用「標籤」主控台移動或合併標籤時，在存放庫中所產生的效果。

將標籤A移動或合併到`/content/cq:tags`下的標籤B中時：

* 標籤A未刪除並接收`cq:movedTo`屬性。
   * `cq:movedTo`指向標籤B。
   * 此屬性表示標籤A已移動或合併到標籤B中。
   * 移動標籤B會相應地更新此屬性。
   * 因此，標籤A會隱藏，並僅保留在存放庫中，以便解析指向標籤A的內容節點中的標籤ID。
   * 標籤記憶體回收行程會移除標籤A，如此一來，內容節點便不再指向這些標籤。
   * `cq:movedTo`屬性的特殊值為`nirvana`，此特殊值會在標籤刪除時套用，但無法從存放庫中移除，因為必須保留具有`cq:movedTo`的子標籤。

     >[!NOTE]
     >
     >只有在符合下列任一條件時，`cq:movedTo`屬性才會新增至移動或合併的標籤：
     >
     > 1. 標籤用於內容中（表示它有參考）。 或者
     > 1. 標籤具有已移動的子系。
     >
* 標籤B已建立（如果有移動）並接收`cq:backlinks`屬性。
   * `cq:backlinks`會將參照保持在另一個方向。 也就是說，它會保留所有已移至標籤B或與標籤B合併的標籤清單。
   * 若要在移動/合併/刪除標籤B時或啟用標籤B時保持`cq:movedTo`屬性為最新狀態（在此情況下，也必須啟用其所有反向連結標籤），則此功能為最常所需。

     >[!NOTE]
     >
     >只有在符合下列任一條件時，`cq:backlinks`屬性才會新增至移動或合併的標籤：
     >
     > 1. 標籤用於內容中（表示它有參考），或
     > 1. 標籤具有已移動的子系。

讀取內容節點的`cq:tags`屬性涉及下列解析度：

1. 如果`/content/cq:tags`下沒有相符專案，則不會傳回任何標籤。
1. 如果標籤已設定`cq:movedTo`屬性，則會接著參考的標籤ID。
   * 只要後續的標籤具有`cq:movedTo`屬性，就會重複此步驟。
1. 如果追蹤的標籤沒有`cq:movedTo`屬性，則會讀取標籤。

若要在標籤移動或合併時發佈變更，必須復寫`cq:Tag`節點及其所有反向連結。 在標籤管理控制檯中啟動標籤時，會自動完成此復寫。

稍後更新頁面的`cq:tags`屬性會自動清除舊參考。 會觸發清除，因為透過API解析移動的標籤會傳回目的地標籤，因此會提供目的地標籤ID。
