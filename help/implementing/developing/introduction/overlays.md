---
title: Adobe Experience Manager雲端服務的覆蓋
description: AEM as a Cloud Service使用覆蓋原則，讓您擴充和自訂控制台和其他功能
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# AEM中的覆蓋作為雲端服務 {#overlays-in-aem}

Adobe Experience Manager做為雲端服務，使用覆蓋原則來擴充和自訂控制台和其他功能（例如頁面製作）。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Overlay是可在許多內容中使用的詞語。 在此內容中（將AEM延伸為雲端服務），覆蓋表示您會取用預先定義的功能，並將您自己的定義加入該功能（以自訂標準功能）。

在標準例項中，預先定義的功能會保留 `/libs` 在下方，建議您在分支下定義覆蓋（自訂） `/apps` (使用搜尋 [路徑](#search-paths) ，解決資源)。

* 啟用觸控功能的UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-related覆蓋：

   * 方法

      * 在下重建適 `/libs` 當的結構 `/apps`。

         這不需要1:1復本，因為 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 可用來交叉參考所需的原始定義。 Sling Resource Merger提供服務，透過差異(differencing)機制存取和合併資源。

      * 在下進行任何更改 `/apps`。
   * 優勢

      * 更強穩地處理下方的變更 `/libs`。
      * 只重新定義實際需要的內容。


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Sling Resource Merger [(](/help/implementing/developing/introduction/sling-resource-merger.md) Sling資源合併)及相關方法只能與 [Granite一起使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 這表示建立具有骨架結構的覆蓋僅適用於標準的觸控式使用者介面。

Overlays是許多變更的建議方法，例如在側面板中設定控制台或建立選取類別至資產瀏覽器（用於製作頁面）。 它們的要求如下：

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* 您不 ***得在分支中&#x200B;*進行更改。您所做的`/libs`**任何更改都可能丟失，因為此分支在應用到實例的升級時都需要進行更改。

* 他們將您的變更集中在一個位置； 讓您更輕鬆地追蹤、移轉、備份和／或除錯變更。

## 搜尋路徑 {#search-paths}

AEM使用搜尋路徑來尋找資源，先搜尋（依預設） `/apps` 分支，再搜尋 `/libs` 分支。 這種機制表示您的覆蓋( `/apps` 以及在其中定義的自訂)將具有優先順序。

對於覆蓋，所傳送的資源是所擷取的資源和屬性的匯總，具體取決於OSGi配置中定義的搜索路徑。

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->