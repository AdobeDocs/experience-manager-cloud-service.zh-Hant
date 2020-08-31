---
title: SPA的動態模型到元件映射
description: 本文說明Javascript SPA SDK for AEM中如何產生動態模型至元件的對應。
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# SPA的動態模型到元件映射 {#dynamic-model-to-component-mapping-for-spas}

本檔案說明Javascript SPA SDK for AEM中如何進行動態模型與元件對應。

## 元件映射模組 {#componentmapping-module}

該 `ComponentMapping` 模組作為NPM包提供給前端項目。 它可儲存前端元件，並為「單頁應用程式」提供將前端元件對應至AEM資源類型的方式。 如此可在剖析應用程式的JSON模型時，啟用元件的動態解析度。

模型中的每個項目都包含一個 `:type` 欄位，可顯示AEM資源類型。 當裝載時，前端元件可以使用它從基礎庫接收到的模型片段進行自身渲染。

請參閱 [SPA Blueprint](blueprint.md) （SPA藍圖）檔案，以取得模型剖析和前端元件存取模型的詳細資訊。

另請參閱npm套件： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型導向的單頁應用程式 {#model-driven-single-page-application}

「單頁應用程式」運用Javascript SPA SDK for AEM是模型導向：

1. 前端元件可自行註冊至元 [件對應商店](#componentmapping-module)。
1. 然後， [Container](blueprint.md#container)( [Model Provider)提供模型後](blueprint.md#the-model-provider)，會重複其模型內容(`:items`)。

1. 如果是頁面，其子項(`:children`)會先從「元件對應」取得元件類 [別](blueprint.md#componentmapping) ，然後執行個體化它。

## 應用程式初始化 {#app-initialization}

每個元件都會與的功能一起擴展 [`ModelProvider`](blueprint.md#the-model-provider)。 因此，初始化採用以下一般形式：

1. 每個模型提供器都自行初始化，並偵聽對與其內部元件相對應的模型段所做的更改。
1. 必 [`PageModelManager`](blueprint.md#pagemodelmanager) 須初始化為由初始化流 [表示](blueprint.md)。

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至應用程式的前 [端根](blueprint.md#container) Container元件。
1. 模型的段最終會傳播到每個單獨的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
