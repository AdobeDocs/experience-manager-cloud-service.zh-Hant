---
title: 自訂主控台
description: 瞭解AEM為自訂編寫執行個體的主控台所提供的不同選項。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# 自訂主控台 {#customizing-consoles}

AEM提供自訂主控台的選項(以及 [頁面製作功能](/help/implementing/developing/extending/page-authoring.md))。

## Clientlibs {#clientlibs}

Clientlibs可讓您擴充預設實作以提供新功能，同時重複使用標準函式、物件和方法。 使用clientlibs自訂時，您可以在下建立您自己的clientlib `/apps.` 例如，它可以儲存自訂元件所需的程式碼。

如需有關clientlibs的詳細資訊，請參閱檔案 [在AEMas a Cloud Service上使用使用者端資料庫。](/help/implementing/developing/introduction/clientlibs.md)

## 覆蓋 {#overlays}

覆蓋是以節點定義為基礎，可讓您覆蓋下找到的標準功能 `/libs` 使用您自己的自訂功能，位於 `/apps`. 建立覆蓋時，不需要原始影像的1:1復本，因為 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 允許繼承。

覆蓋可以用在許多方法來擴充AEM主控台。 以下各節提供幾個範例。

如需覆蓋圖的詳細資訊，請參閱檔案 [Adobe Experience Manager as a Cloud Service的覆蓋圖。](/help/implementing/developing/introduction/overlays.md)

>[!TIP]
>
>如果您對自訂編寫體驗的選項感興趣，請參閱檔案 [自訂頁面製作。](/help/implementing/developing/extending/page-authoring.md)

## 自訂主控台的預設檢視 {#customizing-the-default-view-for-a-console}

您可以自訂主控台的預設檢視（欄、卡片、清單）：

* 您可以在下方覆蓋所需專案來重新排序檢視：

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 第一個專案是預設值。

   * 可用的節點與可用的檢視選項相關：

      * `column`
      * `card`
      * `list`

* 例如，在清單的覆蓋中：

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 定義下列屬性：

      * **名稱**: `sling:orderBefore`
      * **型別**： `String`
      * **值**: `column`

### 將動作新增至工具列 {#add-a-new-action-to-the-toolbar}

您可以建置自己的元件，並包含自訂動作對應的使用者端程式庫。

* 例如，您可能想要建立 **提升至社群媒體** 動作時間：

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * 接著，即可將此連線至主控台上的工具列專案：

   * `/apps/<yourProject>/admin/ext/launches`

   * 例如，在選擇模式中：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 將工具列動作限制在特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

您可以使用自訂演算條件來覆蓋標準動作，並強加演算之前必須滿足的特定條件。

例如，您可能想要建立元件，以根據群組控制演算條件：

* `/apps/myapp/components/renderconditions/group`

若要將這些套用至 **建立網站** 在網站主控台上的動作：

* `/libs/wcm/core/content/sites`

1. 建立覆蓋：

   * `/apps/wcm/core/content/sites`

1. 然後新增動作的轉譯條件：

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

使用此節點上的屬性，您可以定義 `groups` 有權執行特定動作，例如 `administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-list-view}

若要自訂清單檢視中的欄：

1. 覆蓋可用欄的清單。

   * 在節點上：

     `/apps/wcm/core/content/common/availablecolumns`

1. 新增欄或移除現有欄。

如果要插入其他資料，您必須撰寫 [pageinprovider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 與 `pageInfoProviderType` 屬性。

>[!NOTE]
>
>此功能已針對文字欄位欄位進行最佳化。 對於其他資料型別，可以覆蓋 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 在 `/apps`.

### 篩選資源 {#filtering-resources}

使用主控台時，使用者通常必須從資源（例如頁面、元件或資產）中進行選取。 這可採取清單的形式，作者必須從中選擇專案。

為了使清單保持合理的大小以及與使用案例相關，可以自訂述詞的形式實施篩選器。 請參閱檔案[自訂頁面製作](/help/implementing/developing/extending/page-authoring.md#filtering-resources) 以取得詳細資訊。
