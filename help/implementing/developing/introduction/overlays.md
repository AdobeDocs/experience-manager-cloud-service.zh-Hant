---
title: Adobe Experience Manager as a Cloud Service
description: AEMas a Cloud Service使用疊加原則，允許您擴展和定制控制台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 1%

---

# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用疊加原則，允許您擴展和定制控制台和其他功能（例如頁面創作）。

Overlay是可在許多上下文中使用的術語。 在此上下文(擴展AEMas a Cloud Service)中，疊加意味著採用預定義的功能並將您自己的定義強加到該功能之上（以自定義標準功能）。

在標準實例中，預定義功能保留在 `/libs` 建議在以下位置定義覆蓋（自定義） `/apps` 分支(使用 [搜索路徑](#search-paths) 解析資源)。

* 啟用觸摸的UI使用 [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相關疊加：

   * 方法

      * 重建適當的 `/libs` 結構 `/apps`。

         這不需要1:1的拷貝，因為 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 用於交叉引用所需的原始定義。 Sling資源合併通過差異（差異）機制提供訪問和合併資源的服務。

      * 在下進行任何更改 `/apps`。
   * 優勢

      * 對以下項的更改更加穩健 `/libs`。
      * 只重新定義實際需要的內容。


>[!CAUTION]
>
>的 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 相關方法只能與 [花崗岩](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)。 這意味著建立具有骨架結構的覆蓋僅適用於標準的啟用觸摸的UI。

重疊是許多更改的推薦方法，例如配置控制台或在側面板中的資產瀏覽器中建立選擇類別（在創作頁面時使用）。 它們要求為：

* 你 ***不能* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能丟失，因為只要將升級應用到實例，此分支就會發生更改。

* 他們把你的改變集中在一個地方；使您能夠根據需要更輕鬆地跟蹤、遷移、備份和/或調試更改。

## 搜索路徑 {#search-paths}

使AEM用搜索路徑查找資源，首先搜索 `/apps` 分支，然後 `/libs` 分支。 此機構表示您的重疊 `/apps` （以及在其中定義的自定義項）將具有優先順序。

對於覆蓋所交付的資源是所檢索的資源和屬性的集合，這取決於在OSGi配置中定義的搜索路徑。
