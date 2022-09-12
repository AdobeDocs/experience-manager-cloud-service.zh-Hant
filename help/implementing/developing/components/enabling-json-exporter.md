---
title: 為元件啟用JSON匯出
description: 元件可適合根據建模器架構產生其內容的JSON匯出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 5%

---

# 為元件啟用JSON匯出 {#enabling-json-export-for-a-component}

元件可適合根據建模器架構產生其內容的JSON匯出。

## 總覽 {#overview}

JSON匯出以 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，和 [Sling模型導出器](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(本身依賴 [傑克森注釋](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這表示如果元件需要匯出JSON，則必須有Sling模型。 因此，您需要依照這兩個步驟，對任何元件啟用JSON匯出。

* [為元件定義Sling模型](#define-a-sling-model-for-the-component)
* [註解Sling模型介面](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱文章 [在AEM中開發Sling模型匯出工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Sling Model實作類別必須加上下列註解：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可以自行匯出，使用 `.model` 選取器和 `.json` 擴充功能。

此外，這會指定Sling Model類別可調整至 `ComponentExporter` 介面。

>[!NOTE]
>
>Jackson註解通常不會在Sling Model類別層級指定，而是在Model介面層級指定。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 課程來自 `com.adobe.cq.export.json` 捆綁。

### 使用多個選取器 {#multiple-selectors}

雖然不是標準使用案例，但除了 `model` 選取器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

然而，在這種情況下， `model` 選取器必須是第一個選取器，擴充功能必須是 `.json`.

## 註解Sling模型介面 {#annotate-the-sling-model-interface}

若要納入JSON匯出工具架構，模型介面應實作 `ComponentExporter` 介面(或 `ContainerExporter`，若為容器元件)。

對應的Sling模型介面(`MyComponent`)，則會使用 [傑克森注釋](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定義匯出（序列化）的方式。

需要正確注釋「模型」介面，以定義應序列化哪些方法。 預設情況下，所有遵循getter通常命名慣例的方法都將序列化，並且會從getter名稱自然導出其JSON屬性名稱。 可以使用 `@JsonIgnore` 或 `@JsonProperty` 重新命名JSON屬性。

## 範例 {#example}

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 支援JSON匯出，可作為參考使用。

如需範例，請參閱影像核心元件及其註解介面的Sling模型實作。

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
