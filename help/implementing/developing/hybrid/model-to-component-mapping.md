---
title: SPA的動態模型至元件對應
description: 本文說明適用於AEM的JavaScript SPA SDK中元件對映的動態模型如何發生。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# SPA的動態模型至元件對應 {#dynamic-model-to-component-mapping-for-spas}

本檔案說明在AEM適用的JavaScript SPA SDK中元件對映的動態模型如何發生。

## 元件對應模組 {#componentmapping-module}

此 `ComponentMapping` 模組會以NPM封裝的形式提供給前端專案。 它儲存前端元件，並提供單頁應用程式將前端元件對應到AEM資源型別的方法。 模組會在剖析應用程式的JSON模型時啟用元件的動態解析。

模型中每個專案都包含 `:type` 公開AEM資源型別的欄位。 掛載時，前端元件可使用從基礎程式庫收到的模型片段來轉譯自身。

另請參閱 [SPA Blueprint](blueprint.md) 檔案，以取得有關模型剖析和模型的前端元件存取權的詳細資訊。

另請參閱npm套件： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動單頁應用程式 {#model-driven-single-page-application}

使用AEM適用的JavaScript SPA SDK的單頁應用程式是模型導向的：

1. 前端元件向 [元件對應存放區](#componentmapping-module).
1. 然後 [容器](blueprint.md#container)，一旦由提供模型 [模型提供者](blueprint.md#the-model-provider)，反複執行其模型內容(`:items`)。

1. 如果有頁面，其子項(`:children`)首先從取得元件類別 [元件對應](blueprint.md#componentmapping) 然後將其例項化。

## 應用程式初始化 {#app-initialization}

每個元件都可藉由以下功能擴展： [`ModelProvider`](blueprint.md#the-model-provider). 因此，初始化會採用下列一般形式：

1. 每個模型提供者會自我初始化，並監聽對應到其內部元件的模型片段所做的變更。
1. 此 [`PageModelManager`](blueprint.md#pagemodelmanager) 必須初始化，如以下所示 [初始化流程](blueprint.md).

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型傳遞至前端根 [容器](blueprint.md#container) 應用程式的元件。
1. 模型片段最後會傳播至每個個別的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
