---
title: 網站範本
description: 瞭解如何使用AEM網站範本來預先定義網站結構和初始內容，以便您快速建立網站。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 19%

---

# 網站範本 {#site-templates}

瞭解如何使用AEM網站範本來預先定義網站結構和初始內容，以便您快速建立網站。

## 概觀 {#overview}

使用預先定義的結構很方便，可根據一組現有標準快速部署新網站。 網站範本是一種將基本網站內容結合成方便且可重複使用之封裝的方法。

網站範本通常包含基本網站內容與結構和網站樣式資訊，稱為 [網站主題，](site-themes.md) 快速啟動新網站。 管理員選取站台範本作為站台基礎 [在場地建立過程中。](create-site.md)

範本可重複使用且可自訂，因此功能強大。 由於您可以在AEM安裝中使用多個範本，因此可以彈性地建立不同的網站以符合各種業務需求。

>[!NOTE]
>
>不應混淆AEM網站範本 [頁面範本](/help/sites-cloud/authoring/sites-console/templates.md). 網站範本定義網站的整體結構。 頁面範本定義單一頁面的結構和初始內容。
>
>不應混淆AEM網站範本 [AEM網站主題](site-themes.md). AEM網站主題僅包含AEM網站的樣式資訊。 AEM網站範本定義網站結構和初始內容，並包含要允許的AEM網站主題 [快速網站建立](create-site.md).

## 新增網站範本至AEM {#adding}

您可以將多個範本新增至AEM，然後將其用於 [建立網站](create-site.md).

1. 登入您的 AEM 製作環境並導覽至 Sites 主控台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 選取畫面右上角的「**建立**」並從下拉式清單選取「**來自範本的網站**」。

   ![從範本建立網站](../assets/create-site-from-template.png)

1. 在「建立網站」精靈中，選取左欄頂端的「**匯入**」。

   ![網站建立精靈](../assets/site-creation-wizard.png)

1. 在檔案瀏覽器中，找到您要使用的範本，然後選取 **上傳**.

1. 上傳後，範本就會顯示在可用範本清單中。

您的範本會上傳並用於 [建立新網站](create-site.md).

選取現有範本時，它會在右欄中顯示範本的相關資訊。

![選取範本](../assets/select-site-template.png)

## 網站範本結構 {#structure}

網站範本只是具有邏輯結構的套件，可清楚反映套件內容的用途。 網站範本具有下列結構。

* `files`：包含 UI 套件、XD 檔案及可能有其他檔案的資料夾
* `previews`：包含網站範本螢幕擷圖的資料夾
* `site`：使用這個範本建立的每個網站的複製內容之內容包，例如頁面範本、各個頁面等。
* `theme`：的來源 [網站主題](site-themes.md) 修改網站外觀，包括CSS、JavaScript等。

## 標準網站範本 {#standard-site-template}

Adobe提供最佳實務參考範本，您可以依據此範本建立自己的範本。 [GitHub提供標準網站範本。](https://github.com/adobe/aem-site-template-standard)

[最新版本的標準網站範本](https://github.com/adobe/aem-site-template-standard/releases) 可下載並直接用於 [建立新網站](create-site.md).

## 開發網站範本 {#developing-templates}

Adobe提供和AEM網站範本產生器，作為一組用於建立新網站範本的指令碼。

[GitHub上提供AEM網站範本產生器與使用檔案](https://github.com/adobe/aem-site-template-builder). 需有前端開發人員經驗才能自訂 [網站主題](site-themes.md) 自訂網站結構和內容需要AEM開發人員知識。
