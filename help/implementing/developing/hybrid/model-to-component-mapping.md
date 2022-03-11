---
title: 動態模型到元件的映SPA射
description: 本文介紹在的Javascript SDK中如何進行動態模型到組SPA件的映AEM射。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 動態模型到元件的映SPA射 {#dynamic-model-to-component-mapping-for-spas}

本文檔介紹在的Javascript SDK中如何進行動態模型到組SPA件的映AEM射。

## 元件映射模組 {#componentmapping-module}

的 `ComponentMapping` 模組作為NPM包提供到前端項目。 它儲存前端元件，並為單頁應用程式將前端元件映射到資源類型提供AEM了方法。 這樣，在分析應用程式的JSON模型時，就可以動態解析元件。

模型中存在的每個項都包含 `:type` 顯示資源類AEM型的欄位。 裝載後，前端元件可以使用它從基礎庫接收到的模型片段來呈現自己。

請參閱 [藍SPA圖](blueprint.md) 的子菜單。

另請參見npm包： [@adobe/aem-spa元件映射](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動的單頁應用程式 {#model-driven-single-page-application}

使用Javascript SDKSPA的單頁應AEM用程式由模型驅動：

1. 前端元件自行註冊到 [元件映射儲存](#componentmapping-module)。
1. 然後 [容器](blueprint.md#container)，一旦由 [模型提供程式](blueprint.md#the-model-provider)，對模型內容進行迭代(`:items`)。

1. 對於頁面，其子代(`:children`)首先從 [元件映射](blueprint.md#componentmapping) 然後實例化它。

## 應用程式初始化 {#app-initialization}

每個元件都使用 [`ModelProvider`](blueprint.md#the-model-provider)。 因此，初始化採用以下一般形式：

1. 每個模型提供器都初始化自身並偵聽對與其內部元件對應的模型段所做的更改。
1. 的 [`PageModelManager`](blueprint.md#pagemodelmanager) 必須初始化為由表示 [初始化流](blueprint.md)。

1. 一旦儲存，頁面模型管理器將返回應用的完整模型。
1. 然後，此模型將傳遞給前端根 [容器](blueprint.md#container) 元件。
1. 模型的各部分最終傳播到每個單獨的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
