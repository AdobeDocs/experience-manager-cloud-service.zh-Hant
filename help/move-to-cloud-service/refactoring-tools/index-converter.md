---
title: 索引轉換器
description: 索引轉換器
exl-id: e6a3ec6d-cc02-4f5b-8b1d-ea481d6884ca
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 索引轉換器{#index-converter}

Index Converter是一個公用程式，用於遷移客戶的「索引定義」，以準備移動到AEM作為Cloud Service。

## 簡介 {#introduction}

Index Converter可讓AEM開發人員將現有的自訂Oak索引定義移轉至AEM，作為與Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>Index Converter僅轉換&#x200B;*lucene*&#x200B;類型`/apps`或`/oak:index`下顯示的自訂Oak索引定義。 它不會轉換為`nt:base`建立的&#x200B;*lucene*&#x200B;類型索引。

建立自訂Oak索引定義的方式有兩種：

* `under /apps` （透過任何自訂內容套件）
* 直接在`/oak:index`路徑下

若已使用[確保Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，請注意「確保定義」不支援AEM作為Cloud Service，因此需先轉換為Oak索引定義，然後再移轉至與AEM作為Cloud Service相容的自訂Oak索引定義，如下所述：

* 如果屬性ignore設定為`true`，請忽略或跳過「確保定義」
* 將`jcr:primaryType`更新為`oak:QueryIndexDefinition`
* 刪除要忽略的任何屬性，如OSGi配置中所述
* 從「確保定義」中刪除子樹`/facets/jcr:content`

## 使用索引轉換器{#using-index-converter}

* 通過Adobe I/OCLI :建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用「索引轉換器」(AEM作為Adobe I/OCLI的Cloud Service程式碼重構外掛程式)。

   請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以了解如何安裝及使用外掛程式。

* 作為獨立公用程式：Index Converter也可以作為獨立實用程式執行。

   請參閱&#x200B;**[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;以了解如何使用此工具。
