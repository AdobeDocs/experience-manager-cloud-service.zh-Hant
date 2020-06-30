---
title: Adobe Experience Manager雲端服務的覆蓋
description: AEM as a Cloud Service使用覆蓋原則，讓您擴充和自訂控制台和其他功能
translation-type: tm+mt
source-git-commit: e9fa89753289563edd59e3d75413c90efe3ff0b2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---


# AEM中的覆蓋作為雲端服務 {#overlays-in-aem}

Adobe Experience Manager做為雲端服務，使用覆蓋原則來擴充和自訂控制台和其他功能（例如頁面製作）。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Overlay是可在許多內容中使用的詞語。 在此內容中（將AEM延伸為雲端服務），覆蓋表示您會取用預先定義的功能，並將您自己的定義加入該功能（以自訂標準功能）。

在標準例項中，預先定義的功能 `/libs` 保留在下方，建議在分支下定義覆蓋（自訂） `/apps` 。 AEM使用搜尋路徑來尋找資源，先搜尋 `/apps` 分支，然 `/libs` 後搜尋 [分支(搜尋路徑可設定](#configuring-the-search-paths))。 此機制表示您的覆蓋（及其中定義的自訂）將具有優先順序。

* 啟用觸控功能的UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-related覆蓋：

   * 方法

      * 在下重建適 `/libs` 當的結構 `/apps`。

         這不需要1:1復本， [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 可用來交叉參考所需的原始定義。 Sling Resource Merger提供服務，透過差異(differencing)機制存取和合併資源。

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

* 您 ***不得在分支中&#x200B;*進`/libs`**行更改。您所做的任何更改都可能丟失，因為此分支在您執行以下操作時都會面臨更改：

   * 升級至您的實例
   * 套用修補程式
   * 安裝功能套件

* 他們將您的變更集中在一個位置； 讓您更輕鬆地追蹤、移轉、備份和／或除錯變更。

## 設定搜尋路徑 {#configuring-the-search-paths}

對於覆蓋，所傳送的資源是所檢索的資源和屬性的匯總，具體取決於可定義的搜索路徑：

* The resource **Resolver Search Path** as defined in the [OSGi configuration for the](/help/implementing/deploying/configuring-osgi.md) Apache Sling Resource Resolver Factory ****.

   * 搜索路徑的自頂向下順序指示其各自的優先順序。
   * 在標準安裝中，主要預設值 `/apps`為 `/libs` - `/apps` 因此，內容的優先順序比 `/libs` (即覆蓋 ** )高。

* 兩個服務用戶需要對指令碼儲存位置的JCR：讀取訪問。 這些使用者包括： components-search-service(由com.day.cq.wcm.coreto存取／快取元件使用)和sling-scripting（由org.apache.sling.servlets.resolver用來尋找servlet）。
* 還必鬚根據指令碼的放置位置配置以下配置（在此示例中，位於/etc、/libs或/apps下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後，還必須配置Servlet解析程式（在本示例中，還要添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->