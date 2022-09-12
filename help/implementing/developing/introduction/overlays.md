---
title: Adobe Experience Manager as a Cloud Service覆蓋
description: AEM as a Cloud Service使用覆蓋原則，可讓您擴充及自訂主控台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用覆蓋原則，可讓您擴充及自訂主控台和其他功能（例如頁面製作）。

覆蓋是可在許多內容中使用的詞語。 在此內容中(擴充AEMas a Cloud Service)，覆蓋表示取用預先定義的功能，並將您自己的定義加以取代（以自訂標準功能）。

在標準例項中，預先定義的功能會保留在 `/libs` 建議您在 `/apps` 分支(使用 [搜尋路徑](#search-paths) 以解析資源)。

* 觸控式UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相關覆蓋：

   * 方法

      * 重建適當 `/libs` 結構 `/apps`.

         這不需要1:1復本，因為 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 用於交叉參考所需的原始定義。 Sling Resource Merger通過差異（差異）機制提供存取和合併資源的服務。

      * 在 `/apps`.
   * 優點

      * 更強大，可執行 `/libs`.
      * 只重新定義實際需要的。


>[!CAUTION]
>
>此 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 相關方法只能與 [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 這表示以骨架結構建立覆蓋圖僅適用於標準觸控式UI。

覆蓋是許多變更的建議方法，例如設定主控台或在側面板的資產瀏覽器中建立選取類別（用於製作頁面時）。 這些參數為：

* 您 ***不能* 在 `/libs` 分支&#x200B;**您所做的任何變更都可能會遺失，因為每當將升級套用至您的執行個體時，此分支就會面臨變更的責任。

* 他們將你的變更集中在一個位置；讓您更輕鬆地視需要追蹤、移轉、備份和/或除錯變更。

## 搜尋路徑 {#search-paths}

AEM使用搜尋路徑來尋找資源，搜尋（依預設）先 `/apps` 分支，然後 `/libs` 分支。 此機制表示您的覆蓋 `/apps` （以及那裡定義的自訂）將具有優先順序。

針對覆蓋，傳送的資源是所擷取資源和屬性的匯總，視OSGi設定中定義的搜尋路徑而定。
