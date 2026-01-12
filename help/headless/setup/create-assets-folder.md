---
title: 建立資產資料夾 - Headless 設定
description: 使用 AEM 內容片段模型定義內容片段的結構，這是 Headless 內容的基礎。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 95624ebf1a77dac1f535e199b660096c8efdfa76
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 81%

---

# 建立資產資料夾 - Headless 設定 {#creating-an-assets-folder}

使用 AEM 內容片段模型定義內容片段的結構，這是 Headless 內容的基礎。然後將內容片段儲存在資產資料夾中。

## 什麼是資產資料夾？ {#what-is-an-assets-folder}

[現在您已經建立內容片段模型](create-content-model.md)，它定義您未來內容片段所需的結構，您可能很想建立一些片段。

不過，您首先需要建立資產資料夾，以便在其中儲存這些資產。

資產資料夾用於[組織傳統內容資產](/help/assets/manage-digital-assets.md)，例如影像和影片，連同內容片段。

## 建立和設定Assets資料夾 {#create-and-configure-an-assets-folder}

管理員只需要偶爾建立資料夾來組織建立的內容。使用Assets主控台建立新資料夾。

建立後，您必須將[組態](/help/headless/setup/create-configuration.md)套用至資料夾。 如需詳細資訊，請參閱[將組態套用至資料夾](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)。

您可以在剛建立的資料夾中建立其他子資料夾。子資料夾將繼承父資料夾的&#x200B;**雲端設定**。但是，如果您想使用來自另一個設定的模型，可以覆寫此設定。

如果您使用的是當地語系化網站結構，則可以在新資料夾下[建立語言根](/help/assets/translate-assets.md)。

## 後續步驟 {#next-steps}

現在您已經為內容片段建立資料夾，您可以繼續進行快速入門指南的第四部分並[建立內容片段](create-content-fragment.md)。

>[!TIP]
>
>如需有關管理內容片段的完整詳細資訊，請參閱[內容片段文件](/help/sites-cloud/administering/content-fragments/overview.md)
