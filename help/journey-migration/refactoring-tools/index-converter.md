---
title: 索引轉換器
description: 索引轉換器
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# 索引轉換器 {#index-converter}

Index Converter是為遷移客戶的索引定義而開發的實用程式，用於準備遷移到AEMas a Cloud Service。

## 簡介 {#introduction}

索引轉換器使開AEM發人員能夠將現有的自定義Oak索引定義遷AEM移到as a Cloud Service相容的自定義Oak索引定義。

>[!NOTE]
>僅索引轉換器轉換 *苜蓿* 類型下存在的自定義橡樹索引定義 `/apps` 或 `/oak:index`。 它不會轉換 *苜蓿* 為建立的類型索引 `nt:base`。

建立自定義Oak索引定義有兩種方法：

* `under /apps` （通過任何自定義內容包）
* 直接 `/oak:index` 路徑

如果 [確保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 已使用，請注意，確保定義在AEMas a Cloud Service上不受支援，因此需要先將其轉換為Oak索引定義，然後需要遷移到與as a Cloud Service相容的自定義Oak索引定義，如下面的指AEM南所述：

* 如果屬性ignore設定為 `true`、忽略或跳過「確保定義」
* 更新 `jcr:primaryType` 至 `oak:QueryIndexDefinition`
* 刪除OSGi配置中提到的要忽略的所有屬性
* 刪除子樹 `/facets/jcr:content` 從確保定義

## 使用索引轉換器 {#using-index-converter}

* 通過Adobe I/OCLI :建議使用索引轉換器， `aio-cli-plugin-aem-cloud-service-migration` (AEMAdobe I/OCLI的as a Cloud Service代碼重構插件)。

   請參閱 **[Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝和使用插件。

* 作為獨立實用程式：索引轉換器也可以作為獨立實用程式執行。

   請參閱 **[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** 瞭解如何使用此工具。
