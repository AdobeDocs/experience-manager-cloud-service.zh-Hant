---
title: 延伸 ContextHub
description: 當提供的ContextHub存放區和模組不符合您的解決方案需求時，定義這些新的型別
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 延伸 ContextHub {#extending-contexthub}

當提供的ContextHub存放區和模組不符合您的解決方案需求時，請定義這些新型別。

## 建立自訂商店候選者 {#creating-custom-store-candidates}

ContextHub存放區是從已登入的存放區候選專案建立的。 若要建立自訂商店，您必須建立並註冊商店候選商店。

包含建立及登入存放區候選程式碼的javascript檔案必須包含在[使用者端程式庫資料夾](/help/implementing/developing/introduction/clientlibs.md)中。 資料夾的類別必須符合以下模式：

```xml
contexthub.store.[storeType]
```

類別的`storeType`部分為登入商店候選者的`storeType`。 （請參閱[註冊ContextHub存放區候選專案](#registering-a-contexthub-store-candidate)）。 例如，對於`contexthub.mystore`的storeType，使用者端程式庫資料夾的類別必須是`contexthub.store.contexthub.mystore`。

### 建立ContextHub存放區候選專案 {#creating-a-contexthub-store-candidate}

若要建立候選商店，請使用[`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent)函式來擴充其中一個基本商店：

* [&#39;ContextHub.Store.PersistedStore&#39;](contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPStore&#39;](contexthub-api.md#contexthub-store-persistedjsonpstore)

每個基底存放區都會擴充[`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core)存放區。

下列範例會建立`ContextHub.Store.PersistedStore`存放區候選的最簡單延伸模組：

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店候選者將定義其他功能或覆寫商店的初始設定。 有數個[範例商店候選者](sample-stores.md)安裝在`/libs/granite/contexthub/components/stores`下的存放庫中。

### 註冊ContextHub存放區候選專案 {#registering-a-contexthub-store-candidate}

註冊存放區候選項，以將其與ContextHub架構整合，並啟用從中建立存放區的功能。 若要登入存放區候選專案，請使用[`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)類別的`ContextHub.Utils.storeCandidates`函式。

註冊候選商店時，需提供該商店型別的名稱。 從候選者建立存放區時，您可以使用存放區型別來識別它所依據的候選者。

當您註冊候選商店時，請指出其優先順序。 當使用與已登入的候選商店相同的候選商店型別登入候選商店時，會使用具有較高優先順序的候選商店。 因此，您可以使用新的實作來覆寫現有的商店候選者。

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選者，而且優先順序可以設定為`0`，但如果您有興趣，可以瞭解更多進階註冊[，這可讓您根據javascript條件(](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies))和候選者優先順序，選擇少數幾個商店實作之一。`applies`

## 建立ContextHub UI模組型別 {#creating-contexthub-ui-module-types}

當與ContextHub[一起安裝的](sample-modules.md)模組不符合您的需求時，請建立自訂UI模組型別。 若要建立UI模組型別，請擴充`ContextHub.UI.BaseModuleRenderer`類別，然後向`ContextHub.UI`註冊，以建立UI模組轉譯器。

若要建立UI模組轉譯器，請建立包含轉譯UI模組的邏輯的`Class`物件。 您的類別至少必須執行下列動作：

* 擴充`ContextHub.UI.BaseModuleRenderer`類別。 此類別是所有UI模組轉譯器的基本實施。 `Class`物件定義名為`extend`的屬性，您可用來將此類別命名為要擴充的類別。
* 提供預設設定。 建立`defaultConfig`屬性。 此屬性是物件，其中包含為[`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) UI模組定義的屬性，以及您需要的任何其他屬性。

`ContextHub.UI.BaseModuleRenderer`的來源位於`/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`。  若要註冊轉譯器，請使用[`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)類別的`ContextHub.UI`方法。 您必須提供模組型別的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自動執行的匿名函式中建立並註冊轉譯器類別。 下列範例是以`contexthub.browserinfo` UI模組的原始程式碼為基礎。 此UI模組是`ContextHub.UI.BaseModuleRenderer`類別的簡單擴充。

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

包含建立及登入轉譯器之程式碼的javascript檔案必須包含在[使用者端程式庫資料夾](/help/implementing/developing/introduction/clientlibs.md)中。 資料夾的類別必須符合以下模式：

```javascript
contexthub.module.[moduleType]
```

類別的`[moduleType]`部分是模組轉譯器登入的`moduleType`。 例如，對於`moduleType`的`contexthub.browserinfo`，使用者端資料庫資料夾的類別必須是`contexthub.module.contexthub.browserinfo`。
