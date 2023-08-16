---
title: 自訂主控台
description: 了解 AEM 提供哪些不同的選項，讓您可自訂編寫執行個體的主控台。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: ht
source-wordcount: '548'
ht-degree: 100%

---


# 自訂主控台 {#customizing-consoles}

AEM 會提供選項，讓您自訂編寫執行個體的主控台 (以及[頁面編寫功能](/help/implementing/developing/extending/page-authoring.md))。

## Clientlibs {#clientlibs}

Clientlib 可讓您擴充預設實作以提供新功能，同時會重複使用標準函數、物件和方法。使用 clientlibs 進行自訂時，您可以在 `/apps.` 下面建立自己的 clientlib，例如，clientlib 可以為您的自訂元件保留所需的程式碼。

如需有關 clientlibs 的更多詳細資料，請參閱文件[「在 AEM as a Cloud Service 上使用用戶端資料庫」。](/help/implementing/developing/introduction/clientlibs.md)

## 覆蓋 {#overlays}

覆蓋會根據節點定義，並可讓您覆蓋在 `/libs` 下面發現的標準功能，以及覆蓋在 `/apps` 下面您自己的自訂功能。建立覆蓋時，不需要按原件 1：1 複製，因為 [Sling 資源合併](/help/implementing/developing/introduction/sling-resource-merger.md)允許繼承。

覆蓋可用於多種方式，以擴充您的 AEM 主控台。以下章節會提供幾個範例。

如需有關覆蓋的更多資訊，請參閱文件[「適用於 Adobe Experience Manager as a Cloud Service 的覆蓋」。](/help/implementing/developing/introduction/overlays.md)

>[!TIP]
>
>如果您有興趣了解有哪些自訂編寫體驗的選項，請參閱文件[「自訂頁面編寫」。](/help/implementing/developing/extending/page-authoring.md)

## 自訂主控台的預設檢視 {#customizing-the-default-view-for-a-console}

您可以自訂主控台的預設檢視 (欄、卡片、清單)：

* 若要重新排序檢視，只要將所需條目覆蓋在以下位置：

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 第一個條目為預設條目。

   * 可用的節點和可用的檢視選項相互關聯：

      * `column`
      * `card`
      * `list`

* 例如，在清單的覆蓋中：

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 定義以下屬性：

      * **名稱**：`sling:orderBefore`
      * **類型**：`String`
      * **值**：`column`

### 將新動作新增到工具列 {#add-a-new-action-to-the-toolbar}

您可以建置自己的元件並包含相對應的用戶端資料庫，以用於自訂動作。

* 例如，您可能想要在以下建立一個&#x200B;**推廣到社交媒體**&#x200B;動作：

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * 然後，這可以連接至主控台上的工具列項目：

   * `/apps/<yourProject>/admin/ext/launches`

   * 例如，在選擇模式下：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 將工具列動作限制為特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

您可以使用自訂的轉譯條件來覆蓋標準動作，並在轉譯前強制實行必須滿足的特定條件。

例如，您可能想要建立元件，以根據群組控制轉譯條件：

* `/apps/myapp/components/renderconditions/group`

若要將這些套用到 Sites 主控台上的「**建立網站**」動作：

* `/libs/wcm/core/content/sites`

1. 建立覆蓋：

   * `/apps/wcm/core/content/sites`

1. 然後新增動作的轉譯條件：

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

使用此節點上的屬性，您可以定義被准許執行特定動作的 `groups`；例如，`administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-list-view}

若要自訂清單檢視中的欄：

1. 覆蓋可用欄的清單。

   * 在節點上：

     `/apps/wcm/core/content/common/availablecolumns`

1. 新增欄或移除現有的欄。

如果您要插入額外的資料，您需要撰寫 [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 和 `pageInfoProviderType` 屬性。

>[!NOTE]
>
>本功能會針對文字欄位的欄進行最佳化。若為其他資料類型，有可能覆蓋 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` (在 `/apps` 中)。

### 篩選資源 {#filtering-resources}

使用主控台時，使用者經常必須從頁面、元件或資產等資源中進行選取。這可能會採取清單的形式，作者必須從中選擇一個項目。

為了維持清單的合理大小並，同時也維持與案例相關，可以實施自訂述詞形式的篩選器。如需詳細資料，請參閱文件「[自訂頁面編寫](/help/implementing/developing/extending/page-authoring.md#filtering-resources)」。
