---
title: 網站範本
description: 瞭解如AEM何使用站點模板來預定義站點結構和初始內容，以便您快速建立站點。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# 網站範本 {#site-templates}

瞭解如AEM何使用站點模板來預定義站點結構和初始內容，以便您快速建立站點。

## 概覽 {#overview}

使用預定義的結構可以方便地根據一組現有標準快速部署新站點。 站點模板是將基本站點內容合併為方便、可重用的包的一種方法。

站點模板通常包含基本站點內容和結構以及站點樣式資訊，稱為 [網站主題，](site-themes.md) 快速啟動新站點。 管理員選擇站點模板，該模板是站點的基礎 [在站點建立過程中。](create-site.md)

模板功能強大，因為它們可重複使用，而且可自定義。 而且，由於您可以在安裝中使用多AEM個模板，因此您可以靈活地建立不同的站點以滿足各種業務需求。

>[!NOTE]
>
>站AEM點模板不應與 [的子菜單。](/help/sites-cloud/authoring/features/templates.md) 站點模板定義站點的總體結構。 頁面模板定義單個頁面的結構和初始內容。
>
>站AEM點模板不應與 [的AEM子菜單。](site-themes.md) 網AEM站主題只包含網站的樣式AEM資訊。 站AEM點模板定義站點結構和初始內容，並AEM包含站點主題，以允許 [快速建立站點。](create-site.md)

## 將站點模板添加到AEM {#adding}

可以向中添加多AEM個模板，然後這些模板可用於 [建立站點。](create-site.md)

1. 登錄創AEM作環境並導航至站點控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 點擊或按一下 **建立** 在螢幕右上角，從下拉菜單中選擇 **來自模板的站點**。

   ![從模板建立站點](../assets/create-site-from-template.png)

1. 在「建立站點」嚮導中，點擊或按一下 **導入** 在左欄的頂部。

   ![網站建立嚮導](../assets/site-creation-wizard.png)

1. 在檔案瀏覽器中，找到要使用的模板，然後點擊或按一下 **上載**。

1. 上載後，它將顯示在可用模板清單中。

您的模板已上載，可用於 [建立新站點。](create-site.md)

選擇現有模板時，會在右列中顯示有關模板的資訊。

![選取範本](../assets/select-site-template.png)

## 站點模板結構 {#structure}

站點模板只是具有明確反映包內容目的的邏輯結構的包。 站點模板具有以下結構。

* `files`:包含UI工具包、文XD件或其他檔案的資料夾
* `previews`:包含網站模板螢幕截圖的資料夾
* `site`:為此模板建立的每個站點複製的內容的內容包，如頁面模板、頁面等。
* `theme`:源 [網站主題](site-themes.md) 修改站點的外觀，包括CSS、JavaScript等。

## 標準站點模板 {#standard-site-template}

Adobe提供了最佳實踐參考模板，您可以將其用作建立自己模板的基礎。 [GitHub上提供標準站點模板。](https://github.com/adobe/aem-site-template-standard)

[標準站點模板的最新版本](https://github.com/adobe/aem-site-template-standard/releases) 可以直接下載和使用 [建立新站點。](create-site.md)

## 開發站點模板 {#developing-templates}

Adobe將站點AEM模板生成器和站點模板生成器作為一組用於建立新站點模板的指令碼。

[Site AEM Template Builder與GitHub上的使用文檔一起提供。](https://github.com/adobe/aem-site-template-builder) 定制IP和IP [網站主題](site-themes.md) 定AEM制站點結構和內容需要開發人員知識。
