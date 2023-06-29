---
title: 索引轉換器
description: 索引轉換器
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%

---

# 索引轉換器 {#index-converter}

Index Converter是開發的公用程式，用來移轉客戶的索引定義，為移轉到AEMas a Cloud Service做準備。

## 簡介 {#introduction}

索引轉換器可讓AEM開發人員將現有的自訂Oak索引定義移轉至AEMas a Cloud Service相容的自訂Oak索引定義。

>[!NOTE]
>僅索引轉換工具 *lucene* 輸入自訂Oak索引定義，這些定義位於 `/apps` 或 `/oak:index`. 它不會轉換 *lucene* 為建立的型別索引 `nt:base`.

建立自訂Oak索引定義有兩個方法：

* `under /apps` （透過任何自訂內容套件）
* 直接在 `/oak:index` 路徑

若 [確保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 使用，請確定AEMas a Cloud Service上不支援定義。 因此，必須先將它們轉換為Oak索引定義，然後移轉至與AEMas a Cloud Service相容的自訂Oak索引定義，如下所述：

* 如果屬性忽略設為 `true`，忽略或略過確保定義
* 更新 `jcr:primaryType` 至 `oak:QueryIndexDefinition`
* 移除任何要忽略的屬性，如OSGi設定中所述
* 移除子樹狀結構 `/facets/jcr:content` 從確認定義

## 使用索引轉換器 {#using-index-converter}

* 透過Adobe I/OCLI ：建議透過以下方式使用索引轉換器： `aio-cli-plugin-aem-cloud-service-migration` (Adobe I/OCLI的AEMas a Cloud Service程式碼重構外掛程式)。

  另請參閱 **[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： Index Converter也可以作為獨立公用程式執行。

  另請參閱 **[Git資源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** 以瞭解如何使用此工具。
