---
title: 將標記內建至 AEM 應用程式中
description: 以程式設計方式處理自訂AEM應用程式內的標籤或擴展標籤
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 將標記內建至 AEM 應用程式中 {#building-tagging-into-aem-applications}

為了以程式設計方式使用自訂AEM應用程式中的標籤或擴展標籤，本檔案說明如何使用

* [標籤API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

會與

* [標籤框架](tagging-framework.md)

有關標籤的相關資訊：

* 請參閱[使用標籤](/help/sites-cloud/authoring/sites-console/tags.md)，以取得將內容標籤為內容作者的相關資訊。
* 請參閱管理標籤，以取得管理員對於建立和管理標籤以及已對哪些內容套用標籤的觀點。

## 標籤API的總覽 {#overview-of-the-tagging-api}

AEM中[標籤架構](tagging-framework.md)的實作允許使用JCR API管理標籤和標籤內容。 `TagManager`確保在`cq:tags`字串陣列屬性上作為值輸入的標籤不會重複，它會移除指向非現有標籤的`TagID`，並更新已移動或合併標籤的`TagID`。 `TagManager`使用JCR觀察接聽程式來回覆任何不正確的變更。 主要類別位於[com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)封裝中：

* `JcrTagManagerFactory` — 傳回`TagManager`的JCR型實作。 此版本為「標籤API」的參考實作。
* `TagManager` — 允許依路徑和名稱解析及建立標籤。
* `Tag` — 定義標籤物件。

### 取得JCR型TagManager {#getting-a-jcr-based-tagmanager}

若要擷取`TagManager`執行個體，您必須有JCR `Session`並且呼叫`getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般Sling內容中，您也可以從`TagManager`調整`ResourceResolver`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

可透過`Tag`透過解析現有標籤或建立標籤來擷取`TagManager`：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於將`Tags`對應到JCR `Nodes`的JCR型實作，如果您有資源（例如`adaptTo`），可以直接使用Sling的`/content/cq:tags/default/my/tag`機制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從&#x200B;*資源（非節點）轉換*，但標籤可同時轉換節點和資源&#x200B;*到*：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>無法直接從`Node`調整為`Tag`，因為`Node`未實作Sling `Adaptable.adaptTo(Class)`方法。

### 取得和設定標籤 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜尋標籤 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>要使用的有效`RangeIterator`為：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標記 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以使用具有標籤的復寫服務(`Replicator`)，因為標籤的型別為`nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 標籤記憶體回收器 {#the-tag-garbage-collector}

標籤記憶體回收行程是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤是`/content/cq:tags`底下的標籤，具有`cq:movedTo`屬性，而且未用於內容節點。 它們的計數為零。 透過使用這個延遲刪除程式，內容節點（即`cq:tags`屬性）不必隨著移動或合併操作而更新。 更新`cq:tags`屬性時（例如，透過頁面屬性對話方塊），`cq:tags`屬性中的參考會自動更新。

標籤記憶體回收行程預設為每天執行一次。 這可在以下位置設定：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的工作方式如下：

* 搜尋`TagID`會搜尋屬性`cq:movedTo`設定為`TagID`並遵循`cq:movedTo` `TagID`的標籤。
* 搜尋標籤標題只會搜尋沒有`cq:movedTo`屬性的標籤。

## 不同語言的標籤 {#tags-in-different-languages}

標籤`title`可以不同的語言定義。 然後，區分語言的屬性會新增至標籤節點。 這個屬性的格式為`jcr:title.<locale>`，例如，法文翻譯為`jcr:title.fr`。 `<locale>`必須是小寫的ISO地區設定字串，並使用底線(`_`)而非連字型大小/破折號(`-`)，例如： `de_ch`。

例如，將&#x200B;**Animals**&#x200B;標籤新增至&#x200B;**Products**&#x200B;頁面時，值`stockphotography:animals`會新增至節點`cq:tags`的屬性`/content/wknd/en/products/jcr:content`。 將從標籤節點引用翻譯。

伺服器端API已本地化`title`相關方法：

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

在AEM中，可以從頁面語言或使用者語言取得語言。

對於標籤，本地化取決於內容，因為標籤`titles`可以頁面語言、使用者語言或任何其他語言顯示。

### 新增語言至編輯標籤對話方塊 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何新增語言（例如，芬蘭文）至&#x200B;**標籤編輯**&#x200B;對話方塊：

1. 在&#x200B;**CRXDE**&#x200B;中，編輯節點`languages`的多值屬性`/content/cq:tags`。
1. 新增`fi_fi` （代表芬蘭語言環境）並儲存變更。

在&#x200B;**標籤**&#x200B;主控台中編輯標籤時，現在可以在頁面屬性的標籤對話方塊和&#x200B;**編輯標籤**&#x200B;對話方塊中使用芬蘭文。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一。 也就是說，它必須能做為`/libs/wcm/core/resources/languages`以下的節點。
