---
title: Adobe Experience Manager作為Cloud Service的覆蓋
description: AEM as aCloud Service使用覆蓋原則，可讓您擴充及自訂主控台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 1%

---

# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager as aCloud Service使用覆蓋原則，可讓您擴充及自訂主控台和其他功能（例如頁面編寫）。

覆蓋是可在許多內容中使用的詞語。 在此內容中(將AEM延伸為Cloud Service)，覆蓋表示您會取用預先定義的功能，並將您自己的定義加以覆寫（以自訂標準功能）。

在標準例項中，預先定義的功能保存在`/libs`下，建議您使用`/apps`分支下定義覆蓋（自訂）（使用[搜尋路徑](#search-paths)來解析資源）。

* 觸控式UI使用[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相關覆蓋：

   * 方法

      * 在`/apps`下重建相應的`/libs`結構。

         這不需要1:1副本，因為[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)用來交叉參考所需的原始定義。 Sling Resource Merger通過差異（差異）機制提供存取和合併資源的服務。

      * 在`/apps`下進行任何更改。
   * 優勢

      * 對`/libs`下的變更更穩健。
      * 只重新定義實際需要的。


>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)及相關方法只能搭配[Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)使用。 這表示以骨架結構建立覆蓋圖僅適用於標準觸控式UI。

覆蓋是許多變更的建議方法，例如設定主控台或在側面板的資產瀏覽器中建立選取類別（用於製作頁面時）。 這些參數為：

* 您&#x200B;***不得*&#x200B;在`/libs`分支&#x200B;**中進行變更
您所做的任何變更都可能會遺失，因為每當將升級套用至您的執行個體時，此分支就會面臨變更的責任。

* 他們將你的變更集中在一個位置；讓您更輕鬆地視需要追蹤、移轉、備份和/或除錯變更。

## 搜尋路徑 {#search-paths}

AEM使用搜尋路徑來尋找資源，先搜尋`/apps`分支，再搜尋`/libs`分支（預設）。 此機制表示您的`/apps`中覆蓋（以及該處定義的自訂）將具有優先順序。

針對覆蓋，傳送的資源是所擷取資源和屬性的匯總，視OSGi設定中定義的搜尋路徑而定。
