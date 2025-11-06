---
title: AEM 節點類型
description: AEM以Sling為基礎，並使用JCR存放庫和兩者都提供的節點型別，但AEM也提供它自己的節點型別範圍。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 6%

---

# AEM 節點類型 {#aem-node-types}

由於AEM是以Sling為基礎，並使用JCR存放庫，因此這兩種標準提供的節點型別都可以在AEM中使用：

* [JCR節點型別](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling節點型別](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 AEM提供一系列自訂節點型別。 針對具有所有關聯屬性的最新清單，[使用CRXDE](/help/implementing/developing/tools/crxde.md)瀏覽AEM存放庫中的下列路徑：

`/jcr:system/jcr:nodeTypes`
