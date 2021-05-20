---
title: SPA的動態模型與元件對應
description: 本文說明Javascript SPA SDK for AEM中如何進行動態模型與元件的對應。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# SPA {#dynamic-model-to-component-mapping-for-spas}的動態模型與元件映射

本檔案說明Javascript SPA SDK for AEM中如何進行動態模型與元件的對應。

## 元件映射模組{#componentmapping-module}

`ComponentMapping`模組作為NPM包提供給前端項目。 它儲存前端元件，並為單頁應用程式將前端元件映射到AEM資源類型提供了一種方式。 這可在剖析應用程式的JSON模型時，啟用元件的動態解析。

模型中呈現的每個項目都包含顯示AEM資源類型的`:type`欄位。 裝載時，前端元件可使用從基礎庫接收的模型片段來呈現自身。

請參閱[SPA Blueprint](blueprint.md)文檔，了解有關模型解析和對模型的前端元件訪問的詳細資訊。

另請參閱npm套件：[@adobe-aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動的單頁應用程式{#model-driven-single-page-application}

運用Javascript SPA SDK for AEM的單頁應用程式是模型導向：

1. 前端元件自註冊到[元件映射儲存器](#componentmapping-module)。
1. 然後，[容器](blueprint.md#container)一旦由[模型提供者](blueprint.md#the-model-provider)提供模型，則會反覆其模型內容(`:items`)。

1. 在頁面的情況下，其子項(`:children`)首先從[元件映射](blueprint.md#componentmapping)獲取元件類，然後實例化它。

## 應用程式初始化{#app-initialization}

每個元件都會使用[`ModelProvider`](blueprint.md#the-model-provider)的功能進行擴展。 因此，初始化採用以下一般形式：

1. 每個模型提供程式都自行初始化，並監聽對與其內部元件對應的模型片段所做的更改。
1. 必須初始化[`PageModelManager`](blueprint.md#pagemodelmanager)，如[初始化流](blueprint.md)所示。

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至應用程式的前端根[容器](blueprint.md#container)元件。
1. 模型的片段最終傳播到每個單獨的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
