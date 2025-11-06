---
title: 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers
description: 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 5%

---

# 禁止透過 Sling 模型匯出工具序列化 ResourceResolvers {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling模型匯出工具功能允許將Sling模型物件序列化為JSON格式。 此功能廣泛使用，因為它可讓SPA （單頁應用程式）輕鬆存取AEM中的資料。 實施方面，Jackson Databind資料庫是用來序列化這些物件。

序列化是遞回作業。 從「根物件」開始，它會遞回循環遍歷所有合格的物件，並將它們及其子件序列化。 您可以在文章[Jackson — 決定哪些欄位要序列化/還原序列化](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)中找到哪些欄位的描述。

此方法會將所有型別的物件序列化為JSON。 自然地，它也可以序列化Sling `ResourceResolver`物件（如果序列化規則涵蓋此物件）。 這是問題所在，因為`ResourceResolver`服務（因此也是代表它的服務物件）包含潛在的敏感資訊，這些資訊不應公開。 例如：

* 使用者ID
* 要解析相對路徑的搜尋路徑
* `propertyMap`

特別敏感的是`propertyMap` （請參閱[`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)的API檔案），因為這是內部資料結構，可用於許多用途，例如快取與`ResourceResolver`共用相同生命週期的物件。 序列化這些可能會洩露實作詳細資料，並可能對安全性造成影響，因為資料會公開，一般使用者應該無法讀取和存取。 因此，不應將`ResourceResolvers`序列化為JSON。

Adobe計畫以兩步驟方式停用`ResourceResolvers`的序列化：

1. 從AEM as a Cloud Service發行說14697開始，每當`ResourceResolver`序列化時，AEM都會記錄警告訊息。 建議所有客戶檢查其應用程式記錄檔中是否有這些記錄陳述式，並據此調整程式碼基底。
1. Adobe稍後會停用`ResourceResolver`的JSON序列化功能。

## 實施 {#implementation}

警告訊息同時記錄在AEM as a Cloud Service和本機AEM SDK執行個體中，看起來像這樣：

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

此記錄訊息表示在將`/content/…/page`序列化為JSON的程式中，`ResourceResolver`已經序列化。 透過請求`/content/../page.model.json`，您可以檢查`ResourceResolver`的欄位顯示位置，並藉此識別實際觸發此行為的Sling模型類別。


>[!NOTE]
>
>[AEM核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/introduction)已驗證不受此問題影響。

## 請求的動作 {#requested-action}

Adobe要求所有客戶檢查其應用程式記錄和程式碼基底，檢視他們是否受此問題影響，並在必要時變更自訂應用程式，使此警告訊息不再出現在記錄中。

我們假設在大多數情況下，這些必要的變更是直接的。 JSON輸出中完全不需要`ResourceResolver`物件，因為包含在該處的資訊通常不是前端應用程式所必需的，這表示在大多數情況下，應該足以排除Jackson不會考慮`ResourceResolver`物件（請參閱[規則](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)）。

如果Sling模型受到此問題影響但未變更，則明確停用`ResourceResolver`物件的序列化(作為第二個步驟由Adobe執行)將會強制在JSON輸出中進行變更。
