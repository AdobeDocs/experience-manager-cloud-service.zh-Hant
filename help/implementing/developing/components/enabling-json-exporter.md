---
title: 為元件啟用 JSON 匯出
description: 元件可調整為根據模組化架構產生其內容的JSON匯出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 9%

---

# 為元件啟用 JSON 匯出 {#enabling-json-export-for-a-component}

元件可調整為根據模組化架構產生其內容的JSON匯出。

## 概觀 {#overview}

JSON匯出是根據 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，並在上 [Sling模型匯出工具](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(本身依賴 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這表示元件必須具有Sling模型（若元件必須匯出JSON）。 因此，請依照這兩個步驟，在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](#define-a-sling-model-for-the-component)
* [為Sling模型介面加上註釋](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱文章 [在AEM中開發Sling模型匯出工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Sling模型實作類別必須使用以下專案註釋：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可自行匯出，並使用 `.model` 選擇器和 `.json` 副檔名。

此外，這會指定Sling模型類別可以調整到 `ComponentExporter` 介面。

>[!NOTE]
>
>Jackson註解通常不會在Sling模型類別層級指定，而是在「模型」介面層級指定。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 類別來自 `com.adobe.cq.export.json` 套件組合。

### 使用多個選擇器 {#multiple-selectors}

雖然這不是標準使用案例，但除了以下設定外，您也可以設定多個選取器： `model` 選擇器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但在這種情況下， `model` 選取器必須是第一個選取器，而擴充功能必須是 `.json`.

## 為Sling模型介面加上註釋 {#annotate-the-sling-model-interface}

若要JSON匯出程式架構列入考量，模型介面應實作 `ComponentExporter` 介面(或 `ContainerExporter`（例如容器元件）。

對應的Sling模型介面(`MyComponent`)之後會使用進行註解 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定義應如何匯出（序列化）。

模型介面必須正確加上註解，以定義應該序列化哪些方法。 依預設，所有遵守getter一般命名慣例的方法都會序列化，且會從getter名稱自然衍生其JSON屬性名稱。 這可以使用防止或覆寫 `@JsonIgnore` 或 `@JsonProperty` 重新命名JSON屬性。

## 範例 {#example}

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 支援JSON匯出，可作為參考使用。

如需範例，請參閱影像核心元件的Sling模型實作及其附註介面。

## 相關檔案 {#related-documentation}

* [內容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
