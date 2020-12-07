---
title: 索引轉換器
description: 索引轉換器
translation-type: tm+mt
source-git-commit: 21bd9392d913369a5e8e0ebd9badbbe30fd4bba3
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 索引轉換器{#index-converter}

Index Converter是一項公用程式，專為移轉客戶的索引定義而開發，以備移轉至AEM做為雲端服務。

## 簡介 {#introduction}

Index Converter可讓AEM開發人員將現有的自訂Oak索引定義移轉至AEM，做為Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>「索引轉換器」僅轉換&#x200B;*lucene*&#x200B;類型`/apps`或`/oak:index`下的「自訂Oak索引定義」。 它不會轉換為`nt:base`建立的&#x200B;*lucene*&#x200B;類型索引。

## 使用索引轉換器{#using-index-converter}

請參閱&#x200B;**[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以瞭解如何安裝和使用外掛程式。

