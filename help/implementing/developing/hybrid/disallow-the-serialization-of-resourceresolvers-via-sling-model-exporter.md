---
title: 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers
description: 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 5%

---

# 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling模型匯出工具功能允許將Sling模型物件序列化為JSON格式。 此功能廣泛使用，因為它可讓SPA （單頁應用程式）輕鬆從AEM存取資料。 在實施端，會使用Jacson資料庫資料庫來序列化這些物件。

序列化是遞回作業。 從「根物件」開始，它會遞回地反複執行所有合格的物件，並將它們及其子件序列化。 您可以找到要在哪些欄位中序列化的說明 [本文](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

此方法會將所有型別的物件序列化為JSON，自然也可以序列化Sling `ResourceResolver` 物件（如果序列化規則涵蓋此物件）。 這是有問題的，因為 `ResourceResolver` 服務（因此也是代表它的服務物件）包含潛在的敏感資訊，這些資訊不應公開。 例如：

* 使用者ID
* 要解析相對路徑的搜尋路徑
* 此 `propertyMap`.

特別敏感的是 `propertyMap` (請參閱的API檔案： [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--))，因為是內部資料結構，可用於多種用途，例如快取與 `ResourceResolver`. 序列化這些專案可能會洩露實作詳細資料，並可能對安全性造成影響，因為資料會公開，終端使用者無法讀取和存取。 基於這個原因 `ResourceResolvers` 不應序列化為JSON。

Adobe計畫停用序列化 `ResourceResolvers` 採用兩步驟方法：

1. 從AEMas a Cloud Service發行說14697開始，每當 `ResourceResolver` 序列化AEM會記錄警告訊息。 建議所有客戶檢查其應用程式記錄檔中是否有這些記錄陳述式，並據此調整程式碼基底。
1. 稍後，Adobe會停用JSON格式的ResourceResolvers序列化。

## 實作 {#implementation}

警告訊息同時記錄在AEMas a Cloud Service和本機AEM SDK執行個體中，看起來像這樣：

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

此日誌訊息表示在序列化程式期間 `/content/…/page` 至JSON a `ResourceResolver` 已序列化。 透過請求 `/content/../page.model.json` 您可以檢查 `ResourceResolver` 會顯示，並使用它來識別實際觸發此行為的Sling模型類別。


>[!NOTE]
>
>已驗證AEM核心元件不會受此問題影響。

## 請求的動作 {#requested-action}

Adobe要求其所有客戶檢查其應用程式記錄和程式碼庫，以檢視他們是否受到此問題的影響，並在必要時變更自訂應用程式，以便不再顯示此警告訊息。

我們假設在大多數情況下，這些必要的變更是直接進行的，例如 `ResourceResolver` json輸出中完全不需要物件，因為前端應用程式通常不需要其中包含的資訊。 這表示在大多數情況下，應該足以排除 `ResourceResolver` 物件，不被Jackson考慮(請參閱 [規則](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not))。

如果Sling模型受到此問題影響但未變更，會明確停用的 `ResourceResolver` 物件(由當作第2個步驟的Adobe執行)將強制執行JSON輸出中的變更。
