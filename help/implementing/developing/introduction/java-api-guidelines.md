---
title: Java API准則
description: AEM建立在豐富的開放原始碼軟體堆疊上，可公開許多Java API供使用。
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Java API准則{#java-api-guidelines}

Adobe Experience Manager(AEM)建立在豐富的開放原始碼軟體堆疊上，可公開許多Java API供開發期間使用。

AEM是以下列四個主要Java API集為基礎，依偏好設定的遞減順序建立。

1. **Adobe Experience Manager(AEM)** -產品抽象化，例如頁面、資產、工作流程等。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST和資源型抽象化，例如資源、值地圖和HTTP請求。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** -資料和內容抽象化，例如節點、屬性和工作階段。
1. **[OSGi(Apache Felix)](https://felix.apache.org)** - OSGi應用程式容器抽象化，例如服務和(OSGi)元件。

如果AEM提供API，則偏好它，而非Sling、JCR和OSGi。 如果AEM不提供API，則偏好Sling，而非JCR和OSGi。

如需這些准則的詳細資訊，請參閱檔案[瞭解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
