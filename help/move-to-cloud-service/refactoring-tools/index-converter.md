---
title: 索引轉換器
description: 索引轉換器
translation-type: tm+mt
source-git-commit: adfc453729b88a9cc457783806eb7b4d69150b21
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# 索引轉換器{#index-converter}

Index Converter是一項公用程式，專為移轉客戶的索引定義而開發，以備移轉至AEM做為雲端服務。

## 簡介 {#introduction}

Index Converter可讓AEM開發人員將現有的自訂Oak索引定義移轉至AEM，做為Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>「索引轉換器」僅轉換&#x200B;*lucene*&#x200B;類型的「自訂Oak索引定義」，這些定義存在於`/apps`或`/oak:index`下。 它不會轉換為`nt:base`建立的&#x200B;*lucene*&#x200B;類型索引。

建立自訂Oak索引定義有兩種方式：

* `under /apps` （透過任何自訂內容套件）
* 位於`/oak:index`路徑下

>[!NOTE]
>請參閱[Ensure Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)以瞭解如何定義和建立Oak Definitions

## 使用索引轉換器{#using-index-converter}

>[!NOTE]
>雖然建議通過[AIO CLI插件使用Index Converter工具進行源遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)，但也可以單獨執行。

請參閱&#x200B;**[Git資源：aem-cs-source-migration-index-converter](https://git.corp.adobe.com/vavarshn/aem-cloud-service-source-migration/blob/master/packages/index-converter/README.md)**&#x200B;以瞭解如何安裝和使用外掛程式。

