---
title: 網站主題
description: 瞭解如何使用AEM網站主題來自訂網站的樣式和設計。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
source-git-commit: a77c31ebfce01834325bfdb806793dcd8ba169d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 網站主題 {#site-themes}

瞭解如何使用AEM網站主題來自訂網站的樣式和設計。

## 概觀 {#overview}

AEM站台主題是包含CSS、JavaScript和靜態資源的套件，這些資源定義您的AEM站台樣式並符合AEM站台主題的結構。

使用AEM網站範本建立的網站可輕鬆下載、自訂和重新部署主題。

>[!NOTE]
>
>不應混淆AEM網站主題 [AEM網站範本。](site-templates.md) AEM網站主題僅包含AEM網站的樣式資訊。 AEM網站範本定義網站結構和初始內容，並包含AEM網站主題，以便 [快速建立網站。](create-site.md)

## 使用網站主題 {#using-themes}

網站主題有兩種不同的使用方式：

* 當符合下列條件時，它們會作為網站範本的一部分用來定義樣式 [建立網站。](create-site.md)
* 它們會在根據網站範本建立網站後下載，以便前端開發人員可以進一步自訂樣式。

>[!TIP]
>
>從範本建立網站並自訂其主題的程式的端對端說明可在以下網址找到： [快速網站建立歷程。](/help/journey-sites/quick-site/overview.md)

## 網站主題結構 {#structure}

網站主題只是具有邏輯結構的套件，可清楚反映套件內容的用途。 網站主題具有下列典型的前端專案結構。

* `src/main.ts`：JS &amp; CSS主題的主要進入點
* `src/site`：套用至整個網站的JS &amp; CSS檔案
* `src/components`：AEM元件專屬的JS &amp; CSS檔案
* `src/resources`：圖示、標誌和字型等靜態檔案

## 標準網站主題 {#standard-site-theme}

Adobe提供最佳做法參考主題，您可以依據此主題建立自己的主題。 [GitHub提供標準網站主題](https://github.com/adobe/aem-site-template-standard/tree/main/theme).

## 開發網站主題 {#developing-themes}

Adobe提供AEM網站主題產生器，作為建立新網站主題的一組指令碼。

[GitHub上提供AEM網站主題產生器與使用檔案。](https://github.com/adobe/aem-site-theme-builder) 自訂主題需要前端開發經驗。
