---
title: 在AEM應用程式中建立標籤
description: 以程式設計方式使用標籤，或在自訂AEM應用程式中擴充標籤
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在AEM應用程式中建立標籤 {#building-tagging-into-aem-applications}

為了以程式設計方式使用自訂AEM應用程式中的標籤或擴充標籤，本檔案說明的使用

* [標籤API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](tagging-framework.md)

有關標籤的相關資訊：

* 如需將內容標籤為內容作者的相關資訊，請參閱[使用標籤](/help/sites-cloud/authoring/features/tags.md) 。
* 請參閱管理標籤，以了解管理員關於建立和管理標籤的觀點，以及已套用哪些內容標籤。

## 標籤API概觀 {#overview-of-the-tagging-api}

在AEM中實作[標籤架構](tagging-framework.md)可使用JCR API管理標籤和標籤內容。 `TagManager` 確保在字串陣列屬性上輸入 `cq:tags` 為值的標籤不會重複，它會移 `TagID`除指向非現有標籤的標籤，以及移 `TagID`動或合併標籤的更新。`TagManager` 使用JCR觀察接聽程式來回復任何不正確的變更。主類位於[com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)包中：

* `JcrTagManagerFactory`  — 傳回以JCR為基礎的實作 `TagManager`。這是標籤API的參考實作。
* `TagManager`  — 可依路徑和名稱解析及建立標籤。
* `Tag`  — 定義標籤物件。

### 取得JCR型TagManager {#getting-a-jcr-based-tagmanager}

若要擷取`TagManager`例項，您需要有JCR `Session`並呼叫`getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般的Sling內容中，您也可以從`ResourceResolver`調整為`TagManager`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

透過`TagManager`可解析現有標籤或建立新標籤來擷取`Tag`:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於以JCR為基礎的實作（將`Tags`對應至JCR `Nodes`），如果您有資源（例如`/content/cq:tags/default/my/tag`），則可直接使用Sling的`adaptTo`機制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從&#x200B;*資源（而非節點）轉換*，但標籤可以同時從節點和資源&#x200B;*轉換為*:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>無法直接從`Node`調整為`Tag`，因為`Node`不實作Sling `Adaptable.adaptTo(Class)`方法。

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
>使用的有效`RangeIterator`為：
>
>`com.day.cq.commons.RangeIterator`

### Deleting Tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以將複製服務(`Replicator`)與標籤一起使用，因為標籤的類型為`nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 標籤垃圾收集器 {#the-tag-garbage-collector}

標籤垃圾收集器是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤是位於`/content/cq:tags`下方的標籤，其具有`cq:movedTo`屬性，且不用於內容節點。 他們的數為零。 使用此延遲刪除程式，內容節點（即`cq:tags`屬性）不必隨著移動或合併操作而更新。 更新`cq:tags`屬性時，`cq:tags`屬性中的參照會自動更新，例如透過頁面屬性對話方塊。

標籤垃圾收集器預設會每天執行一次。 這可在下列位置進行設定：

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Tag Search and Tag Listing {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋`TagID`會搜尋將屬性`cq:movedTo`設為`TagID`並貫穿`cq:movedTo` `TagID`s的標籤。
* 搜尋標籤標題只會搜尋沒有`cq:movedTo`屬性的標籤。

## 不同語言中的標籤 {#tags-in-different-languages}

標籤`title`可以用不同語言定義。 接著，會將語言敏感屬性新增至標籤節點。 此屬性的格式為`jcr:title.<locale>`，例如`jcr:title.fr`，以取得法文翻譯。 `<locale>` 必須是小寫的ISO地區字串，並使用底線(`_`)，而非連字型大小/破折號(`-`)，例如： `de_ch`.

例如，當&#x200B;**Animals**&#x200B;標籤添加到&#x200B;**Products**&#x200B;頁面時，值`stockphotography:animals`將添加到節點`/content/wknd/en/products/jcr:content`的屬性`cq:tags`中。 轉譯會從標籤節點參考。

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

在AEM中，語言可從頁面語言或使用者語言取得。

對於標籤，本地化取決於上下文，因為標籤`titles`可以以頁面語言、用戶語言或任何其他語言顯示。

### 將新語言添加到編輯標籤對話框 {#adding-a-new-language-to-the-edit-tag-dialog}

以下過程說明如何向&#x200B;**標籤編輯**&#x200B;對話框添加新語言（如芬蘭語）:

1. 在&#x200B;**CRXDE**&#x200B;中，編輯節點`/content/cq:tags`的多值屬性`languages`。
1. 添加`fi_fi`（代表芬蘭語地區）並保存更改。

現在，在&#x200B;**標籤**&#x200B;主控台中編輯標籤時，頁面屬性的標籤對話方塊和&#x200B;**編輯標籤**&#x200B;對話方塊中都可使用芬蘭文。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，亦即，它必須是`/libs/wcm/core/resources/languages`下方的節點。
