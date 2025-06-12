---
title: SPA的元件對應動態模型
description: 本文說明在AEM的JavaScript SPA SDK中，元件對映的動態模型如何發生。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# SPA的元件對應動態模型 {#dynamic-model-to-component-mapping-for-spas}

本檔案說明適用於AEM的JavaScript SPA SDK中如何發生元件對應的動態模型。

{{ue-over-spa}}

## 元件對應模組 {#componentmapping-module}

`ComponentMapping`模組是以NPM封裝形式提供給前端專案。 它會儲存前端元件，並提供單頁應用程式將前端元件對應至AEM資源型別的方法。 模組會在剖析應用程式的JSON模型時啟用元件的動態解析。

模型中每個專案都包含公開AEM資源型別的`:type`欄位。 掛載時，前端元件可使用從基礎程式庫收到的模型片段來轉譯自身。

請參閱[SPA Blueprint](blueprint.md)檔案，以取得有關模型剖析和模型的前端元件存取權的詳細資訊。

另請參閱npm套件： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動單頁應用程式 {#model-driven-single-page-application}

使用適用於AEM的JavaScript SPA SDK的單頁應用程式是模型導向的：

1. 前端元件註冊到[元件對應存放區](#componentmapping-module)。
1. 然後[模型提供者](blueprint.md#the-model-provider)提供模型的[容器](blueprint.md#container)會反複執行其模型內容(`:items`)。

1. 如果有頁面，其子系(`:children`)會先從[元件對應](blueprint.md#componentmapping)取得元件類別，然後將其具現化。

## 應用程式初始化 {#app-initialization}

每個元件都使用[`ModelProvider`](blueprint.md#the-model-provider)的功能延伸。 因此，初始化會採用下列一般形式：

1. 每個模型提供者會自我初始化，並監聽對應到其內部元件的模型片段所做的變更。
1. 必須初始化[`PageModelManager`](blueprint.md#pagemodelmanager)，如[初始化流程](blueprint.md)所表示。

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至應用程式的前端根[Container](blueprint.md#container)元件。
1. 模型片段最後會傳播至每個個別的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
