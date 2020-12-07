---
title: AEM節點類型
description: AEM是以Sling為基礎，並使用JCR儲存庫及兩者皆提供的節點類型，但AEM也提供其專屬的節點類型範圍。
translation-type: tm+mt
source-git-commit: 020cebfa714c098f032df963b7105503c741e748
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# AEM Node Types {#aem-node-types}

由於AEM是以Sling為基礎，並使用JCR儲存庫，因此這兩種標準提供的節點類型都可用於AEM:

* [JCR節點類型](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling Node Types](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除了這些。 AEM提供一系列自訂節點類型。 對於具有所有關聯屬性的最新清單，[使用CRXDE](/help/implementing/developing/tools/crxde.md)瀏覽AEM儲存庫中的下列路徑：

`/jcr:system/jcr:nodeTypes`
