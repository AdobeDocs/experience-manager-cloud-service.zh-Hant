---
title: 網站主題
description: 瞭解如何使用AEM網站主題來自訂網站風格和設計，供具有發佈傳送的傳統AEM製作專案使用。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 9efba01add46c09e9839da6bb96b138d48018e54
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 9%

---


# 網站主題 {#site-themes}

{{traditional-aem}}

瞭解如何使用AEM網站主題來自訂網站風格和設計，供具有發佈傳送的傳統AEM製作專案使用。

## 概觀 {#overview}

AEM網站主題是包含CSS、JavaScript和靜態資源的套件，可定義AEM網站的樣式並符合AEM網站主題的結構。

使用AEM網站範本建立的網站，可輕鬆下載、自訂和重新部署具有[發佈傳遞的傳統AEM製作專案的主題。](/help/sites-cloud/authoring/author-publish.md)

>[!NOTE]
>
>不應混淆AEM網站主題與[AEM網站範本](site-templates.md)。 AEM網站主題僅包含AEM網站的樣式資訊。 AEM網站範本定義網站結構和初始內容，並包含AEM網站主題，以允許[快速建立網站。](create-site.md)

## 使用網站主題 {#using-themes}

網站主題有兩種不同的使用方式：

* 在[建立網站時，它們會作為網站範本的一部分用來定義樣式。](create-site.md)
* 它們會在根據網站範本建立網站後下載，以便前端開發人員可以進一步自訂樣式。

>[!TIP]
>
>您可以在[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)中找到從範本建立網站並自訂其主題的程式的端對端說明。

## 網站主題結構 {#structure}

網站主題只是具有邏輯結構的套件，其明確反映套件內容的目的。 對於典型的前端專案，Adobe建議在網站主題中使用下列結構：

* `src/theme.ts`：JS &amp; CSS 主題的主要入口點
* `src/site`：套用至整個網站的 JS 和 CSS 檔案
* `src/components`：AEM 元件特定的 JS 和 CSS 檔案
* `src/resources`：圖示、標誌和字體等靜態檔案

視特定專案需求而定，只要主要進入點`src/theme.ts`被保留，您的主題結構可能會有所不同。

## 標準網站主題 {#standard-site-theme}

Adobe提供最佳做法參考主題，您可以根據此主題建立自己的主題。 [標準網站主題可在GitHub上取得。](https://github.com/adobe/aem-site-template-standard/tree/main/theme)

## 開發網站主題 {#developing-themes}

Adobe提供AEM網站主題產生器，作為一組用於建立新網站主題的指令碼。

[GitHub上提供AEM網站主題產生器與使用檔案。](https://github.com/adobe/aem-site-theme-builder)自訂主題需要前端開發體驗。
