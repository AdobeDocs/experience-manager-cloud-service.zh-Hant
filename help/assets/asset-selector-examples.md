---
title: 適用於  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的資產選擇器
description: 根據需求使用Asset Selector來自訂的範例。
role: Admin, User
exl-id: 7a393a96-f2a2-4a25-922c-577271cafc57
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 54%

---


# 使用資產選擇器屬性的範例 {#usage-examples}

您可以在&#x200B;**index.html**&#x200B;檔案中定義資產選擇器[屬性](/help/assets/asset-selector-properties.md)，以自訂應用程式中的資產選擇器顯示。

## 範例 1：邊欄視圖中的資產選擇器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果AssetSelector `rail`的值設為`false`或未在屬性中提及，預設會在強制回應檢視中顯示Asset Selector。 `acvConfig`屬性允許一些深入設定，例如拖放。 請造訪[啟用或停用拖放](asset-selector-customization.md#enable-disable-drag-and-drop)，以瞭解`acvConfig`屬性的使用方式。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

## 範例 2：中繼資料彈出視窗

使用各種屬性定義您要使用資訊圖示檢視的資產中繼資料。資訊彈出視窗提供有關資產或資料夾的資訊集合，包括資產的標題、尺寸、修改日期、位置和說明。在下面的範例中，各種屬性用於顯示資產的中繼資料，例如，`repo:path`屬性指定資產的位置<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->。

![metadata-popover-example](assets/metadata-popover.png)

## 範例 3：邊欄視圖中的自訂篩選器屬性

除了多面向搜尋之外，Assets Selector可讓您自訂各種屬性，以將搜尋從[!DNL Adobe Experience Manager]縮小為[!DNL Cloud Service]應用程式。 新增下列程式碼，在您的應用程式中新增自訂的搜尋篩選器。 在下面的範例中，`Type Filter`在影像、文件或影片中篩選資產類型，或為搜尋新增篩選器類型的搜尋。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->


>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [資產選擇器上傳](/help/assets/asset-selector-upload.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
