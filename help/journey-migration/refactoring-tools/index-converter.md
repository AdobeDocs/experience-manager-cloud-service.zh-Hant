---
title: 索引轉換器
description: 瞭解如何移轉索引定義，為移動至AEM as a Cloud Service做準備。
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 索引轉換器 {#index-converter}

Index Converter是專為移轉客戶的索引定義而開發的公用程式，為移轉至AEM as a Cloud Service做準備。

## 簡介 {#introduction}

索引轉換器可讓AEM開發人員將現有的自訂Oak索引定義移轉至與AEM as a Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>索引轉換器只會轉換`/apps`或`/oak:index`下出現的&#x200B;*lucene*&#x200B;型別自訂Oak索引定義。 它不會轉換為`nt:base`建立的&#x200B;*lucene*&#x200B;型別索引。

建立自訂Oak索引定義有兩個方法：

* `under /apps` （透過任何自訂內容封裝）
* 直接位於`/oak:index`路徑下

如果[確定使用了Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，請確定AEM as a Cloud Service上不支援定義。 因此，必須先將它們轉換成Oak索引定義，然後移轉至與AEM as a Cloud Service相容的自訂Oak索引定義，如以下准則所述：

* 如果屬性ignore設定為`true`，請忽略或略過確定定義
* 將`jcr:primaryType`更新為`oak:QueryIndexDefinition`
* 移除任何在OSGi設定中提到的要忽略的屬性
* 從確定定義移除子樹狀結構`/facets/jcr:content`

## 使用索引轉換器 {#using-index-converter}

* 透過Adobe I/OCLI ：Adobe建議透過`aio-cli-plugin-aem-cloud-service-migration`使用索引轉換器(Adobe I/OCLI的AEM as a Cloud Service程式碼重構外掛程式)。

  請參閱&#x200B;**[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式：Index Converter也可以作為獨立公用程式執行。

  請參閱&#x200B;**[Git資源： aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;以瞭解如何使用此工具。
