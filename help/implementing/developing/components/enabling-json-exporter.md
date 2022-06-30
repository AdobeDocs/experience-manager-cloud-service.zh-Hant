---
title: 為元件啟用JSON導出
description: 元件可適於基於建模器框架生成其內容的JSON導出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 5%

---

# 為元件啟用JSON導出 {#enabling-json-export-for-a-component}

元件可適於基於建模器框架生成其內容的JSON導出。

## 概觀 {#overview}

JSON導出基於 [吊具模型](https://sling.apache.org/documentation/bundles/models.html)的 [Sling模型導出器](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(它本身依賴 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這意味著如果元件需要導出JSON，則它必須具有Sling模型。 因此，您需要執行這兩個步驟，才能在任何元件上啟用JSON導出。

* [為元件定義吊具模型](#define-a-sling-model-for-the-component)
* [注釋Sling模型介面](#annotate-the-sling-model-interface)

## 為元件定義吊具模型 {#define-a-sling-model-for-the-component}

首先必須為元件定義「吊索模型」。

>[!NOTE]
>
>有關使用Sling模型的示例，請參閱文章 [發展中國Sling模AEM式](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)。

Sling Model實現類必須用下列內容進行注釋：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保使用 `.model` 選擇器和 `.json` 擴展。

此外，它指定Sling Model類可以適配到 `ComponentExporter` 。

>[!NOTE]
>
>Jackson批注通常不在Sling Model類級別指定，而是在Model介面級別指定。 這是為了確保將JSON導出視為元件API的一部分。

>[!NOTE]
>
>的 `ExporterConstants` 和 `ComponentExporter` 課來自 `com.adobe.cq.export.json` 捆綁。

### 使用多個選擇器 {#multiple-selectors}

雖然不是標準使用情形，但除了配置 `model` 選擇器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但在這種情況下 `model` 選擇器必須是第一個選擇器，副檔名必須是 `.json`。

## 注釋Sling模型介面 {#annotate-the-sling-model-interface}

要由JSON導出器框架考慮，模型介面應實現 `ComponentExporter` 介面(或 `ContainerExporter`，例如容器元件)。

相應的Sling模型介面(`MyComponent`)，然後使用 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 定義如何導出（序列化）。

需要對「模型」介面進行正確注釋，以定義應序列化哪些方法。 預設情況下，將序列化所有遵守getter通常命名約定的方法，並將自然從getter名稱中派生其JSON屬性名稱。 可以使用 `@JsonIgnore` 或 `@JsonProperty` 更名JSON屬性。

## 範例 {#example}

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 支援JSON導出，可用作引用。

例如，請參閱影像核心元件及其注釋介面的Sling模型實現。

## 相關文檔 {#related-documentation}

有關詳細資訊，請參閱：

* [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用內容片段創作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
