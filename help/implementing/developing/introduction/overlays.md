---
title: Adobe Experience Manager雲端服務的覆蓋
description: AEM as a Cloud Service使用覆蓋原則，讓您擴充和自訂控制台和其他功能
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager做為雲端服務，使用覆蓋原則來擴充和自訂控制台和其他功能（例如頁面製作）。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Overlay是可在許多內容中使用的詞語。 在此內容中（將AEM延伸為雲端服務），覆蓋表示您會取用預先定義的功能，並將您自己的定義加入該功能（以自訂標準功能）。

在標準例項中，預先定義的功能保存在`/libs`下，建議在`/apps`分支下定義覆蓋（自訂）（使用[搜尋路徑](#search-paths)解析資源）。

* 啟用觸控的UI使用[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相關覆蓋：

   * 方法

      * 在`/apps`下重建適當的`/libs`結構。

         這不需要1:1復本，因為[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)用來交叉參考所需的原始定義。 Sling Resource Merger提供服務，透過差異(differencing)機制存取和合併資源。

      * 在`/apps`下進行任何更改。
   * 優勢

      * 對`/libs`下的變更更更穩健。
      * 只重新定義實際需要的內容。


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)和相關方法只能與[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)一起使用。 這表示建立具有骨架結構的覆蓋僅適用於標準的觸控式使用者介面。

Overlays是許多變更的建議方法，例如在側面板中設定控制台或建立選取類別至資產瀏覽器（用於製作頁面）。 它們的要求如下：

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* ***不得*&#x200B;在`/libs`分支&#x200B;**中進行變更
您所做的任何變更都可能會遺失，因為此分支會在每次套用升級至您的實例時，都會面臨變更。

* 他們將您的變更集中在一個位置；讓您更輕鬆地追蹤、移轉、備份和／或除錯變更。

## 搜索路徑{#search-paths}

AEM使用搜尋路徑來尋找資源，先搜尋`/apps`分支，再搜尋`/libs`分支（依預設）。 這種機制表示您的覆蓋在`/apps`（及在其中定義的自訂）中具有優先順序。

對於覆蓋，所傳送的資源是所擷取的資源和屬性的匯總，具體取決於OSGi配置中定義的搜索路徑。

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->