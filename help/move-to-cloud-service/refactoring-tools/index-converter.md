---
title: 索引轉換器
description: 索引轉換器
translation-type: tm+mt
source-git-commit: 1117f03b2eff37f8b25726c3dc60d5a3fe98a5d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 索引轉換器{#index-converter}

Index Converter是一項公用程式，專為移轉客戶的「索引定義」而開發，以備移轉至AEM做為雲端服務。

## 簡介 {#introduction}

Index Converter可讓AEM開發人員將現有的自訂Oak Index定義移轉至AEM，做為Cloud Service相容的自訂Oak Index定義。

>[!NOTE]
>「索引轉換器」僅轉換&#x200B;*lucene*&#x200B;類型的「自訂Oak索引定義」，這些定義存在於`/apps`或`/oak:index`下。 它不會轉換為`nt:base`建立的&#x200B;*lucene*&#x200B;類型索引。

建立自訂Oak索引定義有兩種方式：

* `under /apps` （透過任何自訂內容套件）
* 位於`/oak:index`路徑下

如果使用[Ensure Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，請注意，AEM上不支援「Ensure Definitions as a Cloud Service」（確保定義為雲端服務），因此必須先轉換為Oak Index Definitions，然後必須移轉為自訂Oak Index Definitions，這些定義與A AS相容，如下方針：

* 如果屬性ignore設定為`true`，則忽略或跳過「確保定義」
* 將`jcr:primaryType`更新為`oak:QueryIndexDefinition`
* 刪除OSGi配置中提及的要忽略的所有屬性
* 從「確保定義」中刪除子樹`/facets/jcr:content`

## 使用索引轉換器{#using-index-converter}

* 通過Adobe I/O CLI :建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用「索引轉換器」（AEM為Adobe I/O CLI的雲端服務程式碼重構外掛程式）。

請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以瞭解如何安裝和使用外掛程式。

* 作為獨立實用程式：Index Converter也可以作為獨立實用程式執行。

請參閱&#x200B;**[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;以瞭解如何使用此工具。



