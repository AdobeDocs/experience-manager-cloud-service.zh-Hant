---
title: AEM節點類型
description: AEM以Sling為基礎，並使用JCR存放庫及兩者皆提供的節點類型，但AEM也提供其專屬的節點類型範圍。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# AEM節點類型 {#aem-node-types}

由於AEM以Sling為基礎，且使用JCR存放庫，因此這兩種標準提供的節點類型都可在AEM中使用：

* [JCR節點類型](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling節點類型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 AEM提供自訂節點類型的範圍。 對於具有所有關聯屬性的最新清單， [使用CRXDE](/help/implementing/developing/tools/crxde.md) 要在AEM儲存庫中瀏覽以下路徑：

`/jcr:system/jcr:nodeTypes`
