---
title: Adobe Experience Manager as a Cloud Service的覆蓋圖
description: AEMas a Cloud Service會使用覆蓋原則，讓您擴充和自訂主控台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 2%

---

# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用覆蓋原則，可讓您擴充和自訂主控台和其他功能（例如頁面製作）。

覆蓋是可用於許多內容的字詞。 在此上下文中，延伸AEMas a Cloud Service的覆蓋是指取得預先定義的功能，並將您自己的定義強加於此功能，以自訂標準功能。

在標準例項中，預先定義的功能位於 `/libs` 而且建議您在下定義覆蓋（自訂） `/apps` 分支(使用 [搜尋路徑](#search-paths) 以解決資源)。

* 觸控式使用者介面會使用 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)相關覆蓋圖：

   * 方法

      * 重新建構適當的 `/libs` 結構於 `/apps`.

        此重新建構不需要1:1的復本，因為 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 用於互動參照所需的原始定義。 Sling Resource Merger提供的服務可存取及合併具有不同（差異）機制的資源。

      * 下 `/apps`，進行變更。

   * 優點

      * 更健全，可適應以下變更 `/libs`.
      * 僅重新定義必要的專案。

>[!CAUTION]
>
>此 [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 並且相關方法只能用於 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 此規則表示建立具有骨架結構的覆蓋圖僅適用於標準觸控式使用者介面。

覆蓋圖是進行許多變更的建議方法。 例如，設定主控台，或是在側面板中的資產瀏覽器中建立選取範圍類別（用於編寫頁面）。 需有下列變數：

* **在 `/libs` 分支， *不要* 進行變更**
您所做的任何變更都可能遺失，因為每當升級套用至您的執行個體時，此分支很容易變更。

* 它們會將您的變更集中在一個位置，讓您更輕鬆地追蹤、移轉、備份變更，或視需要偵錯變更。

## 搜尋路徑 {#search-paths}

AEM使用搜尋路徑來尋找資源，先搜尋（預設為） `/apps` 分支，然後 `/libs` 分支。 此機制表示您的覆蓋位於 `/apps` （以及此處定義的自訂專案）具有優先順序。

對於覆蓋，傳遞的資源是擷取的資源和屬性的彙總，取決於OSGi設定中定義的搜尋路徑。
