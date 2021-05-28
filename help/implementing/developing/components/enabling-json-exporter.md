---
title: 為元件啟用JSON匯出
description: 元件可適合根據建模器架構產生其內容的JSON匯出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# 為元件{#enabling-json-export-for-a-component}啟用JSON匯出

元件可適合根據建模器架構產生其內容的JSON匯出。

## 概覽 {#overview}

JSON匯出以[Sling Models](https://sling.apache.org/documentation/bundles/models.html)和[Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130)架構（本身需仰賴[Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)）為基礎。

這表示如果元件需要匯出JSON，則必須有Sling模型。 因此，您需要依照這兩個步驟，對任何元件啟用JSON匯出。

* [為元件定義Sling模型](#define-a-sling-model-for-the-component)
* [註解Sling模型介面](#annotate-the-sling-model-interface)

## 為元件{#define-a-sling-model-for-the-component}定義Sling模型

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱[在AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)中開發Sling模型匯出工具一文。

Sling Model實作類別必須加上下列註解：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保使用`.model`選取器和`.json`擴充功能，自行匯出元件。

此外，還指定Sling Model類別可調整至`ComponentExporter`介面。

>[!NOTE]
>
>Jackson註解通常不會在Sling Model類別層級指定，而是在Model介面層級指定。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>`ExporterConstants`和`ComponentExporter`類來自`com.adobe.cq.export.json`套件組合。

### 使用多個選擇器{#multiple-selectors}

雖然不是標準使用案例，但除了`model`選取器外，還可以設定多個選取器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但在此情況下，`model`選擇器必須是第一個選擇器，且副檔名必須為`.json`。

## 註解Sling模型介面{#annotate-the-sling-model-interface}

若要由JSON匯出器架構考慮，模型介面應實作`ComponentExporter`介面（若是容器元件，則為`ContainerExporter`）。

然後會使用[Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)來註解對應的Sling模型介面(`MyComponent`)，以定義應如何匯出（序列化）。

需要正確注釋「模型」介面，以定義應序列化哪些方法。 預設情況下，所有遵循getter通常命名慣例的方法都將序列化，並且會從getter名稱自然導出其JSON屬性名稱。 使用`@JsonIgnore`或`@JsonProperty`來重新命名JSON屬性，可以防止或覆寫此錯誤。

## 範例 {#example}

[核心元](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 件支援JSON匯出，且可作為參考使用。

如需範例，請參閱影像核心元件及其註解介面的Sling模型實作。

## 相關檔案{#related-documentation}

如需詳細資訊，請參閱：

* [資產使用手冊中的內容片段](/help/assets/content-fragments/content-fragments.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 元件和內 [容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
