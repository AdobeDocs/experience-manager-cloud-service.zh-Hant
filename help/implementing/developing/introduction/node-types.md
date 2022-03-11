---
title: 節AEM點類型
description: 基於AEMSling，使用JCR儲存庫，其中包含兩者提供的節點類型，AEM但也提供其自己的節點類型範圍。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 節AEM點類型 {#aem-node-types}

因AEM為基於Sling並使用JCR儲存庫，因此這兩種標準提供的節點類型可用於AEM:

* [JCR節點類型](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [吊掛節點類型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 提AEM供一系列自定義節點類型。 對於具有所有關聯屬性的最新清單， [使用CRXDE](/help/implementing/developing/tools/crxde.md) 瀏覽儲存庫中的以AEM下路徑：

`/jcr:system/jcr:nodeTypes`
