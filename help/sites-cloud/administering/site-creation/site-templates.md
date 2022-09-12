---
title: 網站範本
description: 了解如何使用AEM網站範本預先定義網站結構和初始內容，以便快速建立網站。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# 網站範本 {#site-templates}

了解如何使用AEM網站範本預先定義網站結構和初始內容，以便快速建立網站。

## 總覽 {#overview}

有預先定義的結構可方便您根據一組現有標準快速部署新網站。 網站範本是將基本網站內容結合為方便且可重複使用套件的方式。

網站範本通常包含基本網站內容和結構，以及網站樣式資訊，稱為 [網站主題，](site-themes.md) 快速啟動新網站。 管理員選擇要作為站點基礎的網站模板 [在網站建立過程中。](create-site.md)

範本功能強大，因為可重複使用且可自訂。 由於AEM安裝中提供多個範本，因此您可以彈性建立不同的網站，以符合各種業務需求。

>[!NOTE]
>
>AEM網站範本不應與 [頁面範本。](/help/sites-cloud/authoring/features/templates.md) 網站範本會定義網站的整體結構。 頁面範本會定義個別頁面的結構和初始內容。
>
>AEM網站範本不應與 [AEM網站主題。](site-themes.md) AEM網站主題僅包含AEM網站的樣式資訊。 AEM網站範本會定義網站結構和初始內容，並包含AEM網站主題，以便 [快速建立網站。](create-site.md)

## 新增網站範本至AEM {#adding}

您可以將多個範本新增至AEM，然後再用於 [建立網站。](create-site.md)

1. 登入AEM製作環境，並導覽至Sites主控台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 點選或按一下 **建立** 在畫面右上方，從下拉式功能表中選取 **範本網站**.

   ![從範本建立網站](../assets/create-site-from-template.png)

1. 在「建立網站」精靈，點選或按一下 **匯入** 在左欄頂端。

   ![站點建立嚮導](../assets/site-creation-wizard.png)

1. 在檔案瀏覽器中，找到您要使用的範本，然後點選或按一下 **上傳**.

1. 上傳後，它會顯示在可用範本清單中。

您的範本已上傳，並可用於 [建立新網站。](create-site.md)

選取現有範本時，會在右側欄中顯示範本的相關資訊。

![選取範本](../assets/select-site-template.png)

## 網站範本結構 {#structure}

網站範本只是包，其邏輯結構可清楚反映包內容的用途。 網站範本的結構如下。

* `files`:包含UI套件、XD檔案和其他檔案的資料夾
* `previews`:包含網站範本螢幕擷取畫面的資料夾
* `site`:針對從此範本建立的每個網站（如頁面範本、頁面等）所複製的內容套件。
* `theme`:來源 [網站主題](site-themes.md) 修改網站外觀，包括CSS、JavaScript等。

## 標準網站範本 {#standard-site-template}

Adobe提供最佳實務參考範本，您可以此為基礎建立自己的範本。 [GitHub提供標準網站範本。](https://github.com/adobe/aem-site-template-standard)

[標準網站範本的最新版本](https://github.com/adobe/aem-site-template-standard/releases) 可下載，並直接用於 [建立新網站。](create-site.md)

## 開發網站範本 {#developing-templates}

Adobe提供和AEM網站範本產生器，作為建立新網站範本的一組指令碼。

[您可在GitHub上取得AEM網站範本產生器及使用說明檔案。](https://github.com/adobe/aem-site-template-builder) 自訂 [網站主題](site-themes.md) 而AEM開發人員在自訂網站結構和內容時需具備相關知識。
