---
title: 網站主題
description: 瞭解如AEM何使用網站主題來自定義網站的樣式和設計。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 網站主題 {#site-themes}

瞭解如AEM何使用網站主題來自定義網站的樣式和設計。

## 概覽 {#overview}

站AEM點主題是包含CSS、JavaScript和靜態資源的包，這些資源定義站點的樣式並AEM遵循站點主題的AEM結構。

使用站點模AEM板建立的站點允許輕鬆下載、自定義和重新部署主題。

>[!NOTE]
>
>不AEM應將網站主題與 [網AEM站模板](site-templates.md) 網AEM站主題只包含網站的樣式AEM資訊。 站AEM點模板定義站點結構和初始內容，並AEM包含站點主題，以允許 [快速建立站點。](create-site.md)

## 使用網站主題 {#using-themes}

網站主題的使用方式有兩種：

* 它們用作站點模板的一部分，在 [建立站點。](create-site.md)
* 在基於站點模板建立站點之後下載這些文檔，以便前端開發人員可以進一步定制該樣式。

>[!TIP]
>
>有關從模板建立站點和自定義其主題的過程的端到端說明，請參見 [快速建立站點行程。](/help/journey-sites/quick-site/overview.md)

## 網站主題結構 {#structure}

站點主題只是具有明確反映包內容目的的邏輯結構的包。 站點主題具有以下前端項目的典型結構。

* `src/main.ts`:JS和CSS主題的主要入口點
* `src/site`:應用於整個站點的JS和CSS檔案
* `src/components`:特定於元件的JS和CSSAEM檔案
* `src/resources`:靜態檔案，如表徵圖、徽標和字型

## 標準網站主題 {#standard-site-theme}

Adobe提供了最佳實踐參考主題，您可以將其用作建立自己主題的基礎。 [GitHub上提供標準網站主題。](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## 開發網站主題 {#developing-themes}

Adobe提AEM供網站主題生成器作為一組用於建立新網站主題的指令碼。

[Site AEM Theme Builder與GitHub上的使用文檔一起提供。](https://github.com/adobe/aem-site-theme-builder) 定制主題需要前端開發經驗。
