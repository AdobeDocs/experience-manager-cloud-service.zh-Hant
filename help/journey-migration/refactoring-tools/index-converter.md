---
title: 索引轉換器
description: 索引轉換器
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 索引轉換器 {#index-converter}

Index Converter是一個公用程式，用於遷移客戶的「索引定義」，以準備遷移到AEMas a Cloud Service。

## 簡介 {#introduction}

Index Converter可讓AEM開發人員將現有的自訂Oak索引定義移轉至AEMas a Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>僅索引轉換器轉換 *lucene* 類型自訂Oak索引定義，存在於 `/apps` 或 `/oak:index`. 它不會轉換 *lucene* 鍵入為建立的索引 `nt:base`.

建立自訂Oak索引定義的方式有兩種：

* `under /apps` （透過任何自訂內容套件）
* 直接在 `/oak:index` 路徑

若 [確保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 已使用，請注意「確保定義」不受AEMas a Cloud Service支援，因此需先轉換為Oak索引定義，然後再移轉至與AEMas a Cloud Service相容的自訂Oak索引定義，如下所述：

* 如果屬性忽略設定為 `true`，忽略或略過「確保定義」
* 更新 `jcr:primaryType` to `oak:QueryIndexDefinition`
* 刪除要忽略的任何屬性，如OSGi配置中所述
* 移除子樹 `/facets/jcr:content` 從確保定義

## 使用索引轉換器 {#using-index-converter}

* 通過Adobe I/OCLI :建議使用「索引轉換器」，方法是 `aio-cli-plugin-aem-cloud-service-migration` (AEMas a Cloud Service程式碼重構Adobe I/OCLI的外掛程式)。

   請參閱 **[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 了解如何安裝及使用外掛程式。

* 作為獨立公用程式：Index Converter也可以作為獨立實用程式執行。

   請參閱 **[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** 了解如何使用此工具。
