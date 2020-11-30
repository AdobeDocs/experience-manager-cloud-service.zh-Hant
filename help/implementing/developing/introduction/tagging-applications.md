---
title: 建立標籤至AEM應用程式
description: 以程式設計方式在自訂AEM應用程式中處理標籤或擴充標籤
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# 建立標籤至AEM應用程式 {#building-tagging-into-aem-applications}

為了以程式設計方式處理自訂AEM應用程式中的標籤或擴充標籤，本檔案說明

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](tagging-framework.md)

有關標籤的相關資訊：

* 如需 [](/help/sites-cloud/authoring/features/tags.md) 將內容標籤為內容作者的詳細資訊，請參閱使用標籤。
* 請參閱管理標籤，以瞭解管理員建立和管理標籤的觀點，以及已套用內容標籤的觀點。

## 標籤API概述 {#overview-of-the-tagging-api}

在AEM中實作標 [記架構](tagging-framework.md) ，可讓您使用JCR API管理標籤和標籤內容。 `TagManager` 確保在字串陣列屬性中輸入的 `cq:tags` 標籤不會重複，它會移除指 `TagID`向非現有標籤的標籤，以及移 `TagID`動或合併標籤的更新。 `TagManager` 使用JCR觀察偵聽器來恢復任何不正確的更改。 主要類別位於com.day.cq.ta [ting](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) package:

* `JcrTagManagerFactory` -返回基於JCR的實施 `TagManager`。 這是標籤API的參考實作。
* `TagManager` -允許依路徑和名稱來解析和建立標籤。
* `Tag` -定義標籤對象。

### 取得JCR架構的TagManager {#getting-a-jcr-based-tagmanager}

要檢索實 `TagManager` 例，您需要JCR並 `Session` 調用 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling內容中，您也可以調整以 `TagManager` 下項目 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 檢索標籤對象 {#retrieving-a-tag-object}

可 `Tag` 以通過解析現有標 `TagManager`記或建立新標籤來檢索：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

若是JCR架構的實作(對應 `Tags` 至JCR `Nodes`)，若您擁有資源(例如 `adaptTo``/content/cq:tags/default/my/tag`)，則可直接使用Sling&#39;s機制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從資 *源* （非節點）轉換 *，但標籤可以同* 時轉換為節點和資源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>無法直接 `Node` 自 `Tag` 動調整，因 `Node` 為不實作Sling `Adaptable.adaptTo(Class)` 方法。

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
>有效 `RangeIterator` 使用方式為：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標籤 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以將複製服務(`Replicator`)與標籤一起使用，因為標籤類型 `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 標籤廢棄項目收集器 {#the-tag-garbage-collector}

標籤廢棄項目收集器是一種後台服務，可清除隱藏和未使用的標籤。 隱藏和未使用的標籤是下 `/content/cq:tags` 面具有屬 `cq:movedTo` 性的標籤，不用於內容節點。 他們的數字是零。 通過使用此延遲刪除過程，內容節點(即屬性 `cq:tags` )不必作為移動或合併操作的一部分進行更新。 屬性中的參 `cq:tags` 照在更新屬性時會自動 `cq:tags` 更新，例如透過頁面屬性對話方塊。

標籤廢棄項目收集器依預設每天執行一次。 This can be configured at:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋會搜 `TagID` 尋屬性設為並遵循 `cq:movedTo` s `TagID` 的標籤的 `cq:movedTo``TagID`屬性。
* 搜尋標籤標題只會搜尋沒有屬性的標 `cq:movedTo` 記。

## 不同語言的標籤 {#tags-in-different-languages}

標籤可 `title` 以定義為不同的語言。 然後，語言敏感屬性會新增至標籤節點。 此屬性的格式 `jcr:title.<locale>`為，例如 `jcr:title.fr` 用於法語翻譯。 `<locale>` 必須是小寫的ISO地區設定字串，並使用底線(`_`)取代連字型大小／破折號(`-`)，例如： `de_ch`.

例如，當Animals **** 標籤新增至 **Products** 頁面時，值 `stockphotography:animals` 會新增至節點 `cq:tags` 的屬性 `/content/wknd/en/products/jcr:content`。 轉換是從標籤節點引用的。

伺服器端API有本地化的 `title`相關方法：

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

在AEM中，語言可從頁面語言或使用者語言取得。

對於標籤，本地化取決於上下文，因 `titles` 為標籤可以以頁面語言、用戶語言或任何其他語言顯示。

### 將新語言添加到「編輯標籤」對話框 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何將新語言（例如芬蘭文）新增至「標籤編輯」 **對話方塊** :

1. 在 **CRXDE**&#x200B;中，編輯節點的多 `languages` 值屬性 `/content/cq:tags`。
1. 添加 `fi_fi`代表芬蘭語地區設定，並保存更改。

現在，在「標籤」控制台中編輯標籤時，芬蘭文可在頁面屬性的標籤對話方塊和「編 **輯標籤** 」對話方 **塊中使用** 。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，例如，它必須以節點的形式提供 `/libs/wcm/core/resources/languages`。
