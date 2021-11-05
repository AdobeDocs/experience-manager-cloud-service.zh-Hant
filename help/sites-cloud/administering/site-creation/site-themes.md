---
title: 網站主題
description: 了解如何使用AEM網站主題來自訂網站的樣式和設計。
feature: Administering
role: Admin
source-git-commit: 9e7ad4a640f1783be5aed75e01e860b647662f52
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---


# 網站主題 {#site-themes}

了解如何使用AEM網站主題來自訂網站的樣式和設計。

>[!CAUTION]
>
>快速網站建立工具目前是技術預覽。 除非經Adobe支援同意，否則可供測試及評估之用，且非供生產使用。

## 概覽 {#overview}

AEM網站主題是包含CSS、JavaScript和靜態資源的套件，可定義AEM網站的樣式並符合AEM網站主題的結構。

使用AEM網站範本建立的網站可輕鬆下載、自訂和重新部署主題。

>[!NOTE]
>
>AEM網站主題不應與 [AEM網站範本。](site-templates.md) AEM網站主題僅包含AEM網站的樣式資訊。 AEM網站範本會定義網站結構和初始內容，並包含AEM網站主題，以便 [快速建立網站。](create-site.md)

## 使用網站主題 {#using-themes}

網站主題的使用方式有兩種：

* 當 [建立網站。](create-site.md)
* 系統會在根據網站範本建立網站後下載這些範本，讓前端開發人員可進一步自訂樣式。

>[!TIP]
>
>從範本建立網站及自訂其主題的程式的端對端說明，位於 [快速網站建立歷程。](/help/journey-sites/quick-site/overview.md)

## 網站主題結構 {#structure}

網站主題只是包，其邏輯結構可清楚反映包內容的目的。 網站主題具有前端專案的典型結構。

* `src/main.ts`:JS和CSS主題的主要入口點
* `src/site`:套用至整個網站的JS和CSS檔案
* `src/components`:AEM元件專用的JS和CSS檔案
* `src/resources`:靜態檔案，例如圖示、標誌和字型

## 標準網站主題 {#standard-site-theme}

Adobe提供最佳實務參考主題，您可以此作為建立自己主題的基礎。 [GitHub提供標準網站主題。](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## 開發網站主題 {#developing-themes}

Adobe提供和AEM網站主題產生器，作為建立新網站主題的一組指令碼。

[您可在GitHub上取得AEM網站主題產生器及使用說明檔案。](https://github.com/adobe/aem-site-theme-builder) 自訂主題需要前端開發體驗。
