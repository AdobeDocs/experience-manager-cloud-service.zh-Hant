---
title: 為元件啟用JSON匯出
description: 元件可以根據建模器架構來產生其內容的JSON匯出。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 4%

---


# 為元件啟用JSON匯出 {#enabling-json-export-for-a-component}

元件可以根據建模器架構來產生其內容的JSON匯出。

## 概覽 {#overview}

JSON Export是以 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，以及 [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) framework(本身需仰賴 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))為基礎。

這表示如果元件需要匯出JSON，它必須有Sling Model。 因此，您必須依照這兩個步驟，在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](#define-a-sling-model-for-the-component)
* [註解Sling Model介面](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling Model。

>[!NOTE]
>
>如需使用Sling Models的範例，請參閱 [Developing Sling Model Exporers in AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)。

Sling Model實作類別必須加上下列註解：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保使用選擇器和擴充功能，自行導 `.model` 出組 `.json` 件。

此外，這會指定Sling Model類別可適用於介 `ComponentExporter` 面。

>[!NOTE]
>
>Jackson註解通常不會在Sling Model類別層級指定，而是在Model介面層級指定。 這是為了確保JSON匯出被視為元件API的一部分。

>[!NOTE]
>
>這 `ExporterConstants` 些 `ComponentExporter` 課程和課 `com.adobe.cq.export.json` 程。

### 使用多個選擇器 {#multiple-selectors}

雖然不是標準使用案例，但除了選擇器外，您仍可設定多個選擇 `model` 器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但是，在這種情況下，選 `model` 擇器必須是第一個選擇器，而副檔名必須是 `.json`。

## 註解Sling Model Interface {#annotate-the-sling-model-interface}

若要讓JSON匯出器架構考慮，Model介面應實 `ComponentExporter` 作介面( `ContainerExporter`若是容器元件)。

然後，對應的Sling Model介面(`MyComponent`)會使用 [Jackson Annotations加上註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) ，以定義如何匯出（序列化）。

Model介面需要正確加上註解，以定義應序列化哪些方法。 依預設，所有遵循getter通常命名慣例的方法都會序列化，並會自然從getter名稱衍生其JSON屬性名稱。 使用或重新命名JSON屬性 `@JsonIgnore` 時， `@JsonProperty` 可防止或覆寫此動作。

## 範例 {#example}

[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 支援JSON匯出，可當做參考使用。

如需範例，請參閱Image Core Component及其註解介面的Sling Model實作。

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* [資產使用指南中的內容片段](/help/assets/content-fragments/content-fragments.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和內容 [片段元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
