---
title: Adobe Experience Manager as a Cloud Service的覆蓋圖
description: AEM as a Cloud Service使用覆蓋原則，可讓您擴充和自訂主控台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# AEM as a Cloud Service 中的覆蓋 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用覆蓋原則，可讓您擴充及自訂主控台和其他功能（例如頁面製作）。

覆蓋是可用於許多內容的辭彙。 在此上下文中，擴充AEM as a Cloud Service的覆蓋是指取得預先定義的功能，並將您自己的定義強加於此功能，以自訂標準功能。

在標準執行個體中，預先定義的功能儲存在`/libs`下，建議在`/apps`分支下定義您的覆蓋（自訂） （使用[搜尋路徑](#search-paths)來解析資源）。

* 觸控式使用者介面使用[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)相關覆蓋圖：

   * 方法

      * 在`/libs`下重新建構適當的`/apps`結構。

        此重新建構不需要複製1:1，因為[Sling資源合併器](/help/implementing/developing/introduction/sling-resource-merger.md)是用來互動參照所需的原始定義。 Sling Resource Merger提供的服務可存取及合併具有不同（差異）機制的資源。

      * 在`/apps`底下，進行變更。

   * 優點

      * 對`/libs`下的變更更健全。
      * 僅重新定義必要的專案。

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)和相關方法只能搭配[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)使用。 此規則表示建立具有骨架結構的覆蓋圖僅適用於已啟用觸控功能的標準使用者介面。

覆蓋圖是進行許多變更的建議方法。 例如，設定主控台，或在側面板中的資產瀏覽器中建立選取範圍類別（用於編寫頁面）。 其需求為：

* **在`/libs`分支中，*不*進行變更**
您所做的任何變更都可能遺失，因為每當升級套用至您的執行個體時，此分支很容易變更。

* 這些功能可將您的變更集中在一個位置，讓您更輕鬆地追蹤、移轉、備份變更，或視需要偵錯變更。

## 搜尋路徑 {#search-paths}

AEM使用搜尋路徑來尋找資源，會先搜尋（預設情況下）「`/apps`」分支，然後搜尋`/libs`分支。 此機制表示您在`/apps` （以及其中定義的自訂）中的覆蓋有優先順序。

對於覆蓋，傳送的資源是擷取的資源和屬性的彙總，取決於OSGi設定中定義的搜尋路徑。
