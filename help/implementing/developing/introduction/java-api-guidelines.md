---
title: Java API准則
description: AEM建置在豐富的開放原始碼軟體堆疊上，可公開許多Java API以供使用。
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Java API指南{#java-api-guidelines}

Adobe Experience Manager(AEM)建置在豐富的開放原始碼軟體堆疊上，可公開許多Java API，以便在開發期間使用。

AEM是以下四個主要Java API集建置，依優先順序遞減。

1. **[Adobe Experience Manager(AEM)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/index.html)**  — 產品抽象化，例如頁面、資產、工作流程等。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和資源型抽象化，例如資源、值映射和HTTP要求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  — 資料和內容抽象化，例如節點、屬性和工作階段。
1. **[OSGi(Apache Felix)](https://felix.apache.org)**  - OSGi應用程式容器抽象化，例如服務和(OSGi)元件。

如果AEM提供API，則偏好使用它，而非Sling、JCR和OSGi。 如果AEM未提供API，則偏好Sling，而非JCR和OSGi。

如需這些准則的詳細資訊，請參閱檔案[了解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
