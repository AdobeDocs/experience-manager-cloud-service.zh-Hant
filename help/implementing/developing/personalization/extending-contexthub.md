---
title: 擴充ContextHub
description: 定義新類型的ContextHub儲存和模組（當提供的儲存和模組不符合您的解決方案要求時）
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# 擴充ContextHub {#extending-contexthub}

定義新類型的ContextHub儲存空間和模組，但提供的儲存空間和模組不符合您的解決方案需求。

## 建立自訂商店候選者 {#creating-custom-store-candidates}

ContextHub儲存區是從註冊的儲存區候選來建立。 若要建立自訂商店，您必須建立並註冊商店申請人。

包含建立和註冊商店候選項之程式碼的javascript檔案必須包含在用戶端程 [式庫資料夾中](/help/implementing/developing/introduction/clientlibs.md)。 資料夾的類別必須符合下列模式：

```xml
contexthub.store.[storeType]
```

類別 `storeType` 的一部分是註冊商 `storeType` 店候選人的部分。 (請參 [閱註冊ContextHub商店候選項](#registering-a-contexthub-store-candidate))。 例如，對於storeType的 `contexthub.mystore`，用戶端程式庫資料夾的類別必須 `contexthub.store.contexthub.mystore`。

### 建立ContextHub商店候選項 {#creating-a-contexthub-store-candidate}

要建立儲存候選項，請使用 [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) 函式擴展其中一個基本儲存：

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

請注意，每個基本儲存都擴展了 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 儲存。

下面的示例建立儲存候選項的最簡 `ContextHub.Store.PersistedStore` 擴展：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店申請人將會定義其他函式或覆寫商店的初始設定。 下面 [的儲存庫中安裝了幾個](sample-stores.md) sample store候選項 `/libs/granite/contexthub/components/stores`。

### 註冊ContextHub商店候選項 {#registering-a-contexthub-store-candidate}

註冊商店候選者，將其與ContextHub架構整合，並讓商店從中建立。 要註冊儲存候選項，請使 [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 用類的功 `ContextHub.Utils.storeCandidates` 能。

當您註冊商店候選者時，會提供商店類型的名稱。 從候選商建立商店時，您會使用商店類型來識別其所依據的候選商。

當您註冊商店候選人時，請指出其優先順序。 當使用與已註冊的儲存候選者相同的儲存類型註冊儲存候選者時，使用優先順序較高的候選者。 因此，您可以使用新實作來覆寫現有的商店申請人。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選項，而且優先順序可設為 `0`，但如果您有興趣，則可瞭解更多進階註冊，這可讓您根據javascript條件( [](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)`applies`)和候選項優先順序來選擇少數的商店實作。

## 建立ContextHub UI模組類型 {#creating-contexthub-ui-module-types}

當隨ContextHub安裝的UI模組類型不 [符合您的要求時](sample-modules.md) ，請建立自訂UI模組類型。 若要建立UI模組類型，請擴充類別，然後將其註冊，以建立 `ContextHub.UI.BaseModuleRenderer` 新的UI模組轉譯器 `ContextHub.UI`。

若要建立UI模組轉譯器，請建立 `Class` 包含轉譯UI模組邏輯的物件。 至少，您的類別必須執行下列動作：

* 擴充課 `ContextHub.UI.BaseModuleRenderer` 程。 此類別是所有UI模組轉譯器的基本實作。 對 `Class` 像定義一個名為的屬 `extend` 性，用於將此類命名為正在擴展的類。
* 提供預設設定。 建立屬 `defaultConfig` 性。 此屬性是一個對象，其中包含為 [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI模組定義的屬性以及您需要的任何其他屬性。

源位 `ContextHub.UI.BaseModuleRenderer` 於 `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`。  要註冊渲染器，請使 [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 用類的方 `ContextHub.UI` 法。 您需要提供模組類型的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自行執行的匿名函式中建立並註冊渲染器類。 以下範例以 `contexthub.browserinfo` UI模組的原始碼為基礎。 此UI模組是類別的簡單擴充 `ContextHub.UI.BaseModuleRenderer` 功能。

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

包含建立和註冊轉譯器的程式碼的javascript檔案必須包含在用戶端程 [式庫資料夾中](/help/implementing/developing/introduction/clientlibs.md)。 資料夾的類別必須符合下列模式：

```javascript
contexthub.module.[moduleType]
```

類 `[moduleType]` 別的一部分是模組 `moduleType` 渲染器註冊時使用的。 例如，對於 `moduleType` 的 `contexthub.browserinfo`，客戶端庫資料夾的類別必須為 `contexthub.module.contexthub.browserinfo`。
