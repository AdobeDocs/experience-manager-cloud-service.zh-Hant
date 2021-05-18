---
title: Java API准則
description: 建AEM立在多樣化的開放原始碼軟體堆疊上，可公開許多Java API供使用。
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: cbcc20e75e4a0cb6d0e060039f4945ff4a85ff5c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Java API准則{#java-api-guidelines}

Adobe Experience Manager(AEM)以豐富的開放原始碼軟體堆疊為基礎，可公開許多Java API供開發期間使用。

以下AEM4個主要Java API集為基礎，依偏好設定的遞減順序建立。

1. **[Adobe Experience ManagerAEM()](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html)** -產品抽象化，例如頁面、資產、工作流程等。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和資源型抽象化，例如資源、值地圖和HTTP請求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** -資料和內容抽象化，例如節點、屬性和工作階段。
1. **[OSGi(Apache Felix)](https://felix.apache.org)** - OSGi應用程式容器抽象化，例如服務和(OSGi)元件。

如果API是由提供AEM，則偏好使用它，而非Sling、JCR和OSGi。 如AEM果不提供API，則偏好Sling而非JCR和OSGi。

如需這些准則的詳細資訊，請參閱檔案[瞭解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
