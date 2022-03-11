---
title: 建立站點
description: 瞭解如何使用站AEM點模板來建立站點，以定義站點的樣式和結構。
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 建立站點 {#creating-site}

瞭解如何使AEM用站點模板建立站點以定義站點的樣式和結構。

## 概覽 {#overview}

在內容作者可以建立包含內容的頁面之前，必須先建立網站。 通常由定義站點AEM初始結構的管理員執行。 使用站點模板可快速、靈活地建立站點。

「快AEM速站點建立」工具允許非開發人員使用站點模板從頭快速建立新站點。

建立網站後，「快速建立網站」工具還可以快速定制網站的主題和樣式AEM（JavaScript、CSS和靜態資源）。 這樣，前端開發人員就可以與內容建立者分AEM開工作，並與內容建立者並行。 管AEM理員只需下載網站主題，並將其提供給前端開發人員，後者使用他們喜愛的工具定制網站主題，然後將更改提交到AEM代碼儲存庫，然後進行部署。

本文檔重點介紹使用快速站點建立工具建立站點。 如果您想要概述網站建立和自定義工作流，請參閱 [快速AEM建立站點](/help/journey-sites/quick-site/overview.md)

## 規劃站點結構 {#structure}

請花時間提前考慮您的站點的目的和計畫內容。 這將推動您如何設計站點結構。 良好的站點結構支援站點訪問者的輕鬆導航和內容發現，並支援AEM各種功能，如 [多站點管理和翻譯。](/help/sites-cloud/administering/msm-and-translation.md)

>[!TIP]
>
>[WKND參考站點](https://wknd.site) 提供全面功能性戶外體驗品牌網站的最佳實踐實施。 瀏覽它，瞭解構建良好的站AEM點的結構。

## 網站範本 {#site-templates}

由於站點結構對站點的成功非常重要，因此使用預定義的結構可以方便地根據一組現有標準快速部署新站點。 站點模板是將基本站點內容合併為方便、可重用的包的一種方法。

網站模板通常包含基本網站內容和結構以及網站樣式資訊，以便快速啟動新網站。 模板功能強大，因為它們可重複使用，而且可自定義。 而且，由於您可以在安裝中使用多AEM個模板，因此您可以靈活地建立不同的站點以滿足各種業務需求。

>[!TIP]
>
>有關站點模板的詳細資訊，請查看 [站點模板](site-templates.md) 文章。

>[!NOTE]
>
>站點模板不與頁面模板混淆。 站點模板定義站點的總體結構。 頁面模板定義單個頁面的結構和初始內容。

## 建立站點 {#create-site}

使用模板建立站點非常簡單。

1. 登錄創AEM作環境並導航至站點控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 點擊或按一下 **建立** 在螢幕右上角，從下拉菜單中選擇 **來自模板的站點**。

   ![從模板建立站點](../assets/create-site-from-template.png)

1. 在「建立站點」嚮導中，點擊或按一下左面板中的現有模板，或按一下 **導入** 在左欄的頂部，導入新模板。

   ![網站建立嚮導](../assets/site-creation-wizard.png)

   1. 如果選擇導入，請在檔案瀏覽器中找到要使用的模板，然後點擊或按一下 **上載**。

   1. 上載後，它將顯示在可用模板清單中。

1. 選擇模板時，會在右列中顯示有關模板的資訊。 選擇所需模板後，點擊或按一下 **下一個**。

   ![選取範本](../assets/select-site-template.png)

1. 提供網站標題。 如果省略，則可以提供或將從標題生成站點名稱。

   * 網站標題顯示在瀏覽器標題欄中。
   * 站點名稱成為URL的一部分。
   * 站點名稱必須符合 [頁AEM面命名約定。](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)

1. 點擊或按一下 **建立** 並且該站點是從站點模板建立的。

   ![新站點的詳細資訊](../assets/create-site-details.png)

1. 在出現的確認對話框中，點擊或按一下 **完成**。

   ![成功對話](../assets/success.png)

1. 在站點控制台中，新站點是可見的，可導航以瀏覽其模板定義的基本結構。

   ![新站點結構](../assets/new-site.png)

內容作者現在可以開始創作！

## 站點自定義 {#site-customization}

如果您的站點需要在可用模板之外進行自定義，則您有許多選項。

* 如果網站結構或初始內容需要調整， [可以自定義站點模板以滿足您的要求。](site-templates.md)
* 如果需要調整網站的樣式， [網站主題可以下載和定制。](/help/journey-sites/quick-site/overview.md)
* 如果需要調整站點功能， [該站點可以完全自定義。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

任何定制都應在開發團隊的支援下進行。
