---
title: ContextHub Javascript API參考資料
description: 將ContextHub元件新增至頁面時，您的指令碼即可使用ContextHub Javascript API
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 2%

---

# ContextHub Javascript API參考資料{#contexthub-javascript-api-reference}

將[ContextHub元件新增至頁面](adding-contexthub.md)時，您的指令碼即可使用ContextHub Javascript API。

## ContextHub常數{#contexthub-constants}

ContextHub Javascript API定義的常數值。

### 事件常數{#event-constants}

下表列出ContextHub儲存區發生的名稱事件。 另請參閱[ContextHub.Utils.Eventing](#contexthub-utils-eventing)。

| 常數 | 說明 | 值 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub的事件命名空間 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 指示所有必需儲存庫都已註冊、初始化並準備好使用 | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 指出並非所有儲存都已在指定逾時內初始化 | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | 在註冊商店時引發 | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | 指出存放區已準備就緒。 註冊後會立即觸發，但JSONP商店除外，擷取資料時會在此觸發)。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | 商店更新其持續性時引發 | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 永續性容器名稱 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 儲儲存存原始JSON結果的特定永續性金鑰名稱 | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | 儲存指出JSON資料擷取時的特定時間戳記 | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 儲存上次呼叫期間使用的JSON服務特定URL | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | 指出ContextHub的UI是否已展開 | `/_/container-expanded` |

### UI事件常數{#ui-event-constants}

下表列出ContextHub UI發生的事件名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | 註冊模式時引發 | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | 未註冊模式時引發 | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | 註冊模式轉譯器時引發 | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | 未註冊模式轉譯器時引發 | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 新增模式時引發 | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | 移除模式時引發 | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | 使用者選取模式時觸發 | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 註冊新模組時引發 | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | 未註冊模組時引發 | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | 註冊模組轉譯器時引發 | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | 未註冊模組轉譯器時引發 | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 新增模組時引發 | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | 移除模組時觸發 | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | 將UI容器新增至頁面時引發 | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | 開啟ContextHub UI時觸發 | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | 折疊ContextHub UI時觸發 | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | 修改屬性時觸發 | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | 每次轉譯ContextHub UI時（例如在屬性變更後）觸發 | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | 初始化UI容器時觸發 | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | 指示活動UI模式 | `/_/active-ui-mode` |

## ContextHub Javascript API參考資料{#contexthub-javascript-api-reference-2}

ContextHub物件可讓您存取所有存放區。

### 函式(ContextHub){#functions-contexthub}

#### getAllStores() {#getallstores}

傳回所有已註冊的ContextHub存放區。

此函式沒有參數。

##### 傳回{#returns-}

包含所有ContextHub存放區的物件。 每個商店都是一個使用與商店相同名稱的對象。

##### 範例 {#example-}

下列範例會擷取所有商店，然後擷取地理位置商店：

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name){#getstore-name}

以Javascript物件擷取商店。

##### 參數 {#parameters-}

* **`name`:** 註冊商店的名稱。

##### 傳回{#returns-getstore-name}

代表存放區的物件。

##### 範例 {#example-getstore-name}

下列範例會擷取地理位置存放區：

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

代表ContextHub區段。 使用`ContextHub.SegmentEngine.SegmentManager`取得區段。

### 函式(ContextHub.ContextEngine.Segment){#functions-contexthub-contextengine-segment}

#### getName() {#getname}

以字串值傳回區段名稱。

#### getPath() {#getpath}

以字串值傳回區段定義的存放庫路徑。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供ContextHub區段的存取權。

### 函式(ContextHub.SegmentEngine.SegmentManager){#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

傳回在目前內容中解析的區段。 此函式沒有參數。

##### 傳回{#returns-getresolvedsegments}

`ContextHub.SegmentEngine.Segment`物件的陣列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub儲存庫的基類。

### 屬性(ContextHub.Store.Core){#properties-contexthub-store-core}

#### 事件 {#eventing}

[`ContextHub.Utils.Eventing`](#contexthub-utils-eventing)物件。 使用此對象來綁定函式以儲存事件。 有關預設值和初始化的資訊，請參見[`init(name,config)`](#init-name-config)。

#### 名稱 {#name}

商店的名稱。

#### 持續性 {#persistence}

`ContextHub.Utils.Persistence`物件。 有關預設值和初始化的資訊，請參見[`init(name,config)`](#init-name-config)。

### 函式(ContextHub.Store.Core){#functions-contexthub-store-core}

#### addAllItems(tree, options){#addallitems-tree-options}

將資料對象或陣列與儲存資料合併。 對象或陣列中的每個鍵/值對都添加到儲存（通過`setItem`函式）:

* **物件：** 索引鍵為屬性名稱。
* **陣列：** 鍵是陣列索引。

請注意，值可以是物件。

##### 參數 {#parameters-addallitems}

* **`tree`:** （物件或陣列）要新增至存放區的資料。
* **`options`:** （物件）傳遞至setItem函式的選項物件。有關資訊，請參閱[`setItem(key,value,options)`](#setitem-key-value-options)的`options`參數。

##### 傳回{#returns-addallitems}

`boolean`值：

* 值`true`表示已儲存資料對象。
* 值`false`表示資料儲存區未更改。

#### addReference(key, anotherKey){#addreference-key-anotherkey}

建立從一個鍵到另一個鍵的引用。 鍵無法引用本身。

##### 參數 {#parameters-addreference}

* **`key`:** 參考的鍵 `anotherKey`。

* **`anotherkey`:** 參考的索引鍵 `key`。

##### 傳回{#returns-addreference}

`boolean`值：

* 值`true`表示已添加引用。
* 值`false`表示未添加任何引用。

#### announceReadiness() {#announcereadiness}

觸發此商店的`ready`事件。 此函式沒有參數且未傳回值。

#### clean() {#clean}

從儲存中移除所有資料。 函式沒有參數，也沒有傳回值。

#### getItem(key){#getitem-key}

傳回與索引鍵相關聯的值。

##### 參數 {#parameters-getitem}

* **`key`:** （字串）要傳回值的索引鍵。

##### 傳回{#returns-getitem}

代表索引鍵值的物件。

#### getKeys(includeInternals){#getkeys-includeinternals}

從商店中擷取金鑰。 您可以選擇擷取ContextHub架構內部使用的索引鍵。

##### 參數 {#parameters-getkeys}

* **`includeInternals`:** 的值包 `true` 含內部使用的索引鍵。這些鍵以下划線(`_`)字元開頭。 預設值為 `false`.

##### 傳回{#returns-getkeys}

鍵名稱的陣列（`string`值）。

#### getReferences() {#getreferences}

從商店中檢索引用。

##### 傳回{#returns-getreferences}

使用引用鍵作為引用鍵索引的陣列：

* 引用鍵與`addReference`函式的`key`參數對應。
* 引用的鍵與`addReference`函式的`anotherKey`參數對應。

#### getTree(includeInternals){#gettree-includeinternals}

從儲存中檢索資料樹。 您可以選擇包含ContextHub架構內部使用的索引鍵/值組。

##### 參數 {#parameters-gettree}

* `includeInternals:` 的值包含 `true` 結果中內部使用的索引鍵/值組。此資料的鍵以下划線(`_`)字元開頭。 預設值為 `false`.

##### 傳回{#returns-gettree}

表示資料樹的對象。 鍵是對象的屬性名稱。

#### init(name, config){#init-name-config}

初始化儲存。

* 將儲存資料設定為空對象。
* 設定對空對象的儲存引用。
* `eventChannel`為`data:<name>`，其中`<name>`為商店名稱。
* `storeDataKey`為`/store/<name>`，其中`<name>`為商店名稱。

##### 參數 {#parameters-init}

* **`name`:** 商店名稱。
* **`config`:** 包含設定屬性的物件：
   * `eventDeferring`:預設值為32。
   * `eventing`:此存 [放區的ContextHub.Utils.](#contexthub-utils-eventing) Eventingobject 。預設值為`ContextHub.eventing`物件使用的。
   * `persistence`:此 `ContextHub.Utils.Persistence` 儲存的對象。預設值為`ContextHub.persistence`物件。

#### isEventingPaused() {#iseventingpaused}

判斷是否暫停此商店的事件。

##### 傳回{#returns-iseventingpaused}

布林值：

* `true`:事件已暫停，因此不會為此存放區觸發任何事件。
* `false`:事件不會暫停，因此會針對此存放區觸發事件。

#### pauseEventing() {#pauseeventing}

暫停儲存的事件，以便不觸發任何事件。 此函式不需要參數且不傳回值。

#### removeItem(key, options){#removeitem-key-options}

從存放區移除金鑰/值組。

移除金鑰時，函式會觸發`data`事件。 事件資料包括儲存名稱、已移除的金鑰名稱、已移除的值、金鑰的新值(null)，以及「remove」的動作類型。

您可以選擇防止`data`事件的觸發。

##### 參數 {#parameters-removeitem}

* **`key`:** （字串）要移除的金鑰名稱。
* **`options`:** （物件）選項的物件。以下對象屬性有效：
   * 靜默：值`true`可防止觸發`data`事件。 預設值為 `false`.

##### 傳回{#returns-removeitem}

`boolean`值：

* 值`true`表示已移除索引鍵/值組。
* 值`false`表示資料儲存區未更改，因為在儲存區中找不到密鑰。

#### removeReference(key){#removereference-key}

從儲存中刪除引用。

##### 參數 {#parameters-removereference}

* **`key`:** 要移除的鍵參考。此參數與`addReference`函式的`key`參數對應。

##### 傳回{#returns-removereference}

`boolean`值：

* 值`true`表示已刪除引用。
* 值`false`表示密鑰無效且儲存不變。

#### reset(keepRemainingData){#reset-keepremainingdata}

重設儲存的持續資料的初始值。 您可以選擇從存放區移除所有其他資料。 重設存放區時，此存放區的事件會暫停。 此函式不會傳回任何值。

初始值提供在用於實例化儲存對象的配置對象的`initialValues`屬性中。

##### 參數 {#parameters-reset}

* **`keepRemainingData`**:（布林值）true值會導致非初始資料持續存在。值為false會移除除初始值以外的所有資料。

#### resolveReference(key, retry){#resolvereference-key-retry}

擷取參考的金鑰。 或者，您可以指定用於解析最佳匹配的迭代次數。

##### 參數 {#parameters-resolvereference}

* **`key`:** （字串）要解析引用的鍵。此`key`參數與`addReference`函式的`key`參數對應。
* **`retry`:** （數量）要使用的迭代次數。

##### 傳回{#returns-resolvereference}

代表引用鍵的`string`值。 如果未解析任何引用，則返回`key`參數的值。

#### resumeEventing() {#resumeeventing}

繼續此存放區的事件，以觸發事件。 此函式不定義參數，也不傳回值。

#### setItem(key, value, options){#setitem-key-value-options}

將索引鍵/值組新增至商店。

僅當鍵的值與當前為鍵儲存的值不同時，才觸發`data`事件。 您可以選擇性地防止`data`事件的觸發。

事件資料包括儲存名稱、索引鍵、先前值、新值，以及`set`的動作類型。

##### 參數 {#parameters-setitem}

* **`key`:** （字串）索引鍵的名稱。
* **`options`:** （物件）選項的物件。以下對象屬性有效：
   * `silent`:值可防止 `true` 觸發事件的 `data` 情況。預設值為 `false`.
* **`value`:** （物件）要與索引鍵關聯的值。

##### 傳回{#returns-setitem}

`boolean`值：

* 值`true`表示已儲存資料對象。
* 值`false`表示資料儲存區未更改。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的商店。 資料會從外部JSONP服務中擷取，或選擇性地從傳回JSON資料的服務中擷取。 建立此類的實例時，使用[`init`](#init-name-config)函式指定服務詳細資訊。

存放區會使用記憶體中的持續時間（Javascript變數）。 儲存資料僅在頁面存留期期間可用。

ContextHub.Store.JSONPStore延伸[ContextHub.Store.Core](#contexthub-store-core)並繼承該類別的函式。

### 函式(ContextHub.Store.JSONPStore){#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override){#configureservice-serviceconfig-override}

配置用於連接到此對象使用的JSONP服務的詳細資訊。 您可以更新或取代現有設定。 函式不會傳回任何值。

##### 參數 {#parameters-configureservice}

* **`serviceConfig`:** 包含下列屬性的物件：
   * `host`:（字串）伺服器名稱或IP位址。
   * `jsonp`:（布林值）值true表示服務是JSONP服務，否則為false。若為true，則{callback:&quot;ContextHub.回呼。*Object.name*}物件已新增至service.params物件。
   * `params`:（物件）URL參數以物件屬性表示。參數名稱是屬性名稱，參數值是屬性值。
   * `path`:（字串）服務的路徑。
   * `port`:（數字）服務的埠號。
   * `secure`:（字串或布林值）決定要用於服務URL的通訊協定：
      * `auto`:/
      * `true`:https://
      * `false`: http://
* **override:** （布林值）。值`true`會導致現有服務配置被`serviceConfig`的屬性替換。 值`false`會導致現有服務配置屬性與屬性`serviceConfig`合併。

#### getRawResponse() {#getrawresponse}

傳回自上次呼叫JSONP服務以來所快取的原始回應。 函式不需要參數。

##### 傳回{#returns-getrawresponse}

代表原始回應的物件。

#### getServiceDetails() {#getservicedetails}

檢索此ContextHub.Store.JSONPStore對象的服務對象。 服務物件包含建立服務URL所需的所有資訊。

##### 傳回{#returns-getservicedetails}

具有下列屬性的物件：

* **`host`:** （字串）伺服器名稱或IP位址。
* **`jsonp`:** （布林值）true值表示服務是JSONP服務，否則為false。若為true，則{callback:&quot;ContextHub.回呼。*Object.name*}物件已新增至service.params物件。
* **`params`:** （物件）URL參數以物件屬性表示。參數名稱是屬性名稱，參數值是屬性值。
* **`path`:** （字串）服務的路徑。
* **`port`:** （數字）服務的埠號。
* **`secure`:** （字串或布林值）決定要用於服務URL的通訊協定：
   * `auto`:/
   * `true`:https://
   * `false`:http://

#### getServiceURL(resolve){#getserviceurl-resolve}

擷取JSONP服務的URL。

##### 參數 {#parameters-getserviceurl}

* **`resolve`:** （布林值）判斷是否要在URL中包含已解析的參數。值`true`解析參數，而`false`解析參數則不。

##### 傳回{#returns-getserviceurl}

代表服務URL的`string`值。

#### init(name, config){#init-name-config-1}

初始化`ContextHub.Store.JSONPStore`對象。

##### 參數 {#parameters-init-1}

* **`name`:** （字串）商店的名稱。
* **`config`:** （物件）包含service屬性的物件。JSONPStore物件使用`service`物件的屬性來建構JSONP服務的URL:
   * `eventDeferring`:32.
   * `eventing`:此儲存區的ContextHub.Utils.Eventing物件。預設值為`ContextHub.eventing`物件。
   * `persistence`:此儲存的ContextHub.Utils.Persistence物件。預設會使用記憶體持續性（Javascript物件）。
   * `service`: (物件)
      * `host`:（字串）伺服器名稱或IP位址。
      * `jsonp`:（布林值）值true表示服務是JSONP服務，否則為false。若為true，則會將`{callback: "ContextHub.Callbacks.*Object.name*}`物件新增至`service.params`。
      * `params`:（物件）URL參數以物件屬性表示。參數名稱和值分別是對象屬性名稱和值。
      * `path`:（字串）服務的路徑。
      * `port`:（數字）服務的埠號。
      * `secure`:（字串或布林值）決定要用於服務URL的通訊協定：
         * `auto`:/
         * `true`:https://
         * `false`:http://
      * `timeout`:（數字）等待JSONP服務在超時前響應的時間長度（以毫秒為單位）。
         * `ttl`:在兩次JSONP服務呼叫之間傳遞的最小時間量（毫秒）。（請參閱[queryService](#queryservice-reload)函式）。

#### queryService(reload){#queryservice-reload}

查詢遠程JSONP服務並快取響應。 如果自上次調用此函式以來的時間小於`config.service.ttl`值，則不會調用該服務，並且快取響應不會更改。 您可以視需要強制呼叫服務。 呼叫[init](#init-name-config)函式初始化儲存時設定`config.service.ttl`屬性。

查詢完成時觸發就緒事件。 如果未設定JSONP服務URL，函式則不會執行任何動作。

##### 參數 {#parameters-queryservice}

* **`reload`:** （布林值）true值會移除快取回應，並強制呼叫JSONP服務。

#### 重設 {#reset}

重設儲存區持續資料的初始值，然後呼叫JSONP服務。 您可以選擇從存放區移除所有其他資料。 初始值重設時，此存放區的事件會暫停。 此函式不會傳回任何值。

初始值會提供在用於實例化儲存對象的配置對象的initialValues屬性中。

##### 參數 {#parameters-reset-1}

* **`keepRemainingData`:** （布林值）true值會導致非初始資料持續存在。值為false會移除除初始值以外的所有資料。

#### resolveParameter(f){#resolveparameter-f}

解析給定參數。

## ContextHub.Store.PerisentJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` extends  [ContextHub.Store.](#contexthub-store-jsonpstore) JSONPStoreso會繼承該類的所有函式。不過，從JSONP服務擷取的資料會根據ContextHub持續性的設定而持續保存。 （請參閱[持久模式：](adding-contexthub.md#persistence-modes)）

## ContextHub.Store.PerisentStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` extends  [ContextHub.Store.](#contexthub-store-core) Coreso會繼承該類的所有函式。此存放區中的資料會根據ContextHub持續性的設定而保存。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` extends  [ContextHub.Store.](#contexthub-store-core) Coreso會繼承該類的所有函式。此存放區中的資料會使用記憶體中的持續性（Javascript物件）來保存。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組轉譯器。

### 函式(ContextHub.UI){#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender){#registerrenderer-moduletype-renderer-dontrender}

向ContextHub註冊UI模組轉譯器。 註冊轉譯器後，可將其用於[建立UI模組](configuring-contexthub.md#adding-a-ui-module)。 當您是[延伸`ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types)時，請使用此函式來建立自訂UI模組轉譯器。

##### 參數 {#parameters-registerrenderer}

* **`moduleType`:** （字串）UI模組轉譯器的識別碼。如果已使用指定值註冊了渲染器，則在註冊此渲染器之前，將先註冊現有的渲染器。
* **`renderer`:** （字串）轉譯UI模組的類別名稱。
* **`dontRender`:** （布林值）設 `true` 為，以防止在註冊轉譯器後轉譯ContextHub UI。預設值為 `false`.

##### 範例 {#example-registerrenderer}

下面的示例將渲染器註冊為`contexthub.browserinfo`模組類型。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

與Cookie互動的公用程式類別。

### 函式(ContextHub.Utils.Cookie){#functions-contexthub-utils-cookie}

#### exists(key){#exists-key}

判斷Cookie是否存在。

##### 參數 {#parameters-exists}

* **`key`:** 包 `String` 含您要測試之Cookie之索引鍵的。

##### 傳回{#returns-exists}

`boolean`值true表示Cookie存在。

##### 範例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter){#getallitems-filter}

傳回所有具有符合篩選器之索引鍵的Cookie。

##### 參數 {#parameters-getallitems}

* **`filter`:** （選用）Cookie索引鍵相符的條件。若要傳回所有Cookie，請指定任何值。 支援下列類型：
   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp物件：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰是否相符的函式。 如果測試確認相符，函式必須將Cookie金鑰當作參數，並傳回true。

##### 傳回{#returns-getallitems}

Cookie的物件。 物件屬性是Cookie索引鍵，而索引鍵值是Cookie值。

##### 範例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key){#getitem-key-1}

傳回Cookie值。

##### 參數 {#parameters-getitem-1}

* **`key`:** 您要其值的Cookie金鑰。

##### 傳回{#returns-getitem-1}

Cookie值；若找不到金鑰的Cookie，則為`null`。

##### 範例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter){#getkeys-filter}

傳回符合篩選器之現有Cookie的索引鍵陣列。

##### 參數 {#parameters-getkeys-1}

* **`filter`:** 比對Cookie金鑰的條件。支援下列類型：
   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp物件：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰是否相符的函式。 如果測試確認相符，函式必須將Cookie金鑰當作參數，並傳回`true`。

##### 傳回{#returns-getkeys-1}

字串的陣列，其中每個字串是符合篩選條件之Cookie的索引鍵。

##### 範例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options){#removeitem-key-options-1}

移除Cookie。 若要移除Cookie，值會設為空字串，而到期日會設為目前日期的前一天。

##### 參數 {#parameters-removeitem-1}

* **`key`:** 代 `String` 表要移除之Cookie索引鍵的值。
* **`options`:** 包含用於設定Cookie屬性之屬性值的物件。如需詳細資訊，請參閱[`setItem`](#setitem-key-value-options)函式。 `expires`屬性無效。

##### 傳回{#returns-removeitem-1}

此函式不會傳回值。

##### 範例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options){#setitem-key-value-options-1}

建立指定索引鍵和值的Cookie，並將Cookie新增至目前的檔案。 您可以選擇指定用以設定Cookie屬性的選項。

##### 參數 {#parameters-setitem-1}

* **`key`:** 包含Cookie索引鍵的字串。
* **`value`:** 包含Cookie值的字串。
* **`options`:** （選用）包含下列任何設定Cookie屬性屬性的屬性的物件：
   * `expires`:指 `date` 定 `number` Cookie過期時間的或值。日期值指定到期的絕對時間。 數字（以天為單位）會將到期時間設為目前時間加上數字。 預設值為 `undefined`.
   * `secure`:指 `boolean` 定Cookie屬 `Secure` 性的值。預設值為 `false`.
   * `path`:用 `String` 作Cookie屬 `Path` 性的值。預設值為 `undefined`.

##### 傳回{#returns-setitem-1}

具有設定值的Cookie。

##### 範例 {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 消失（篩選，選項）{#vanish-filter-options}

移除符合指定篩選器的所有Cookie。 使用`getKeys`函式來比對Cookie，並使用`removeItem`函式來移除。

##### 參數 {#parameters-vanish}

* **`filter`:** 在 `filter` 呼叫函式時使用的引 [`getKeys`](#getkeys-filter) 數。
* **`options`:** 在 `options` 呼叫函式時使用的引 [`removeItem`](#removeitem-key-options) 數。

##### 傳回{#returns-vanish}

此函式不會傳回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

可讓您將函式系結和解除系結至ContextHub儲存事件。 使用儲存的[eventing](#eventing)屬性訪問儲存的`ContextHub.Utils.Eventing`對象。

### 函式(ContextHub.Utils.Eventing){#functions-contexthub-utils-eventing}

#### off(name, selector){#off-name-selector}

從事件中取消綁定函式。

##### 參數 {#parameters-off}

* **`name`:** 您要 [解除](#contexthub-utils-eventing) 函式系結的事件名稱。
* **`selector`:** 識別系結的選取器。（請參閱[`on`](#on-name-handler-selector-triggerforpastevents)和[`once`](#once-name-handler-selector-triggerforpastevents)函式的`selector`參數）。

##### 傳回{#returns-off}

此函式不會傳回任何值。

#### on(name, handler, selector, triggerForPastEvents){#on-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 每次發生事件時都會呼叫函式。 可選地，在建立綁定之前，可以為過去發生的事件調用函式。

##### 參數 {#parameters-on}

* **`name`:** （字串）您 [要系](#contexthub-utils-eventing) 結函式的事件名稱。
* **`handler`:** （函式）要系結至事件的函式。
* **`selector`:** （字串）系結的唯一識別碼。如果要使用`off`函式來刪除綁定，則需要選擇器來標識綁定。
* **`triggerForPastEvents`:** （布林值）指出是否應針對過去發生的事件執行處理常式。`true`值會呼叫過去事件的處理常式。 值`false`將調用將來事件的處理程式。 預設值為 `true`.

##### 傳回{#returns-on}

當`triggerForPastEvents`引數為`true`時，此函式會傳回`boolean`值，指出事件是否發生在過去：

* `true`:事件在過去發生，將呼叫處理常式。
* `false`:事件過去未發生。

如果`triggerForPastEvents`為`false`，則此函式不返回值。

##### 範例 {#example-on}

以下範例將函式系結至地理位置存放區的資料事件。 函式會以商店中緯度資料項目的值填入頁面上的元素。

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents){#once-name-handler-selector-triggerforpastevents}

將函式綁定到事件。 對於事件的首次出現，函式只會呼叫一次。 或者，可以在建立綁定之前，為過去發生的事件調用函式。

##### 參數 {#parameters-once}

* **`name`:** （字串）您 [要系](#contexthub-utils-eventing) 結函式的事件名稱。
* **`handler`:** （函式）要系結至事件的函式。
* **`selector`:** （字串）系結的唯一識別碼。如果要使用`off`函式來刪除綁定，則需要選擇器來標識綁定。
* **`triggerForPastEvents`:** （布林值）指出是否應針對過去發生的事件執行處理常式。`true`值會呼叫過去事件的處理常式。 值`false`將調用將來事件的處理程式。 預設值為 `true`.

##### 傳回{#returns-once}

當`triggerForPastEvents`引數為`true`時，此函式會傳回`boolean`值，指出事件是否發生在過去：

* `true`:事件在過去發生，將呼叫處理常式。
* `false`:事件過去未發生。

如果`triggerForPastEvents`為`false`，則此函式不返回值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

允許對象繼承另一個對象的屬性和方法的實用程式類。

### 函式(ContextHub.Utils.inheritation){#functions-contexthub-utils-inheritance}

#### inherit(child, parent){#inherit-child-parent}

使對象繼承另一個對象的屬性和方法。

##### 參數 {#parameters-inherit}

* **`child`:** （物件）繼承的物件。
* **`parent`:** （物件）定義繼承的屬性和方法的物件。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供將物件序列化為JSON格式，以及將JSON字串反序列化為物件的函式。

### 函式(ContextHub.Utils.JSON){#functions-contexthub-utils-json}

#### parse(data){#parse-data}

將字串值剖析為JSON，並將其轉換為Javascript物件。

##### 參數 {#parameters-parse}

* **`data`:** JSON格式的字串值。

##### 傳回{#returns-parse}

Javascript物件。

##### 範例 {#example-parse}

程式碼：

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

傳回下列物件：

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data){#stringify-data}

將Javascript值和物件序列化為JSON格式的字串值。

##### 參數 {#parameters-stringify}

* **`data`:** 要序列化的值或物件。此函式支援布林值、陣列、數字、字串和日期值。

##### 傳回{#returns-stringify}

序列化字串值。 當`data`為R `egExp`值時，此函式返回空對象。 當`data`為函式時，返回`undefined`。

##### 範例 {#example-stringify}

下列程式碼：

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

傳回：

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此類便於操作要儲存或從ContextHub儲存中檢索的資料對象。

### 函式(ContextHub.Utils.JSON.tree){#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料對象的副本，並從第二個對象添加到資料樹中。 函式返回副本，不修改任何一個原始對象。 當兩個對象的資料樹包含相同的鍵時，第二對象的值覆蓋第一對象的值。

##### 參數 {#parameters-addallitems-1}

* **`tree`:** 複製的物件。
* **`secondTree`:** 與物件復本合併的物 `tree` 件。

##### 傳回{#returns-addallitems-1}

包含合併資料的物件。

#### cleanup() {#cleanup}

建立對象的副本，查找並刪除資料樹中不包含值、空值或未定義的項，並返回副本。

##### 參數 {#parameters-cleanup}

* **`tree`:** 要清除的物件。

##### 傳回{#returns-cleanup}

已清理的樹的副本。

#### getItem() {#getitem}

從物件中擷取金鑰的值。

##### 參數 {#parameters-getitem-2}

* **`tree`:** 資料物件。
* **`key`:** 您要擷取之值的索引鍵。

##### 傳回{#returns-getitem-2}

與索引鍵對應的值。 當索引鍵具有子索引鍵時，此函式會傳回複雜物件。 當鍵的值類型為`undefined`時，會傳回`null`。

##### 範例 {#example-getitem-2}

請考量下列Javascript物件：

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

下列范常式式碼會傳回值`260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

下列范常式式碼會擷取具有子項之索引鍵的值：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

函式會傳回下列物件：

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

從對象的資料樹中檢索所有鍵。 或者，您只能檢索特定鍵子項的鍵。 您也可以選擇指定擷取索引鍵的排序順序。

##### 參數 {#parameters-getkeys-2}

* **`tree`:** 要從中擷取資料樹索引鍵的物件。
* **`parent`:** （選用）您要擷取子項索引鍵之資料樹中項目的索引鍵。
* **`order`:** （選用）決定傳回索引鍵排序順序的函式。（請參閱Mozilla開發人員網路上的[`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)。）

##### 傳回{#returns-getkeys-2}

鍵的陣列。

##### 範例 {#example-getkeys-2}

請考量下列物件：

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

`ContextHub.Utils.JSON.tree.getKeys(myObject);`指令碼返回以下陣列：

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立給定對象的副本，從資料樹中刪除指定的分支，並返回修改的副本。

##### 參數 {#parameters-removeitem-2}

* **`tree`:** 資料物件。
* **`key`:** 要移除的金鑰。

##### 傳回{#returns-removeitem-2}

已移除鍵的原始資料物件復本。

##### 範例 {#example-removeitem-2}

請考量下列物件：

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

以下示例指令碼從資料樹中刪除/one/two/three/four分支：

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

函式會傳回下列物件：

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key){#sanitizekey-key}

清除字串值，以便用作索引鍵。 若要處理字串，此函式會執行下列動作：

* 將多個連續正斜線減少為單斜線。
* 從字串的開頭和結尾移除空格。
* 將結果分割為由斜線標定的字串陣列。

使用產生的陣列建立可用密鑰。

##### 參數 {#parameters-sanitizekey}

* **`key`:** 處理 `string` 方式。

##### 傳回{#returns-sanitizekey}

`string`值的陣列，其中每個字串是由斜線標定的`key`部分。 代表已淨化的金鑰。 如果清理的陣列長度為零，則此函式將返回`null`。

##### 範例 {#example-sanitizekey}

以下代碼清理字串以生成陣列`["this", "is", "a", "path"]`，然後從陣列生成鍵`"/this/is/a/path"`:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value){#setitem-tree-key-value}

將索引鍵/值組新增至物件復本的資料樹。 有關資料樹的資訊，請參閱[持久性。](contexthub.md#persistence)

##### 參數 {#parameters-setitem-2}

* **`tree`:** 資料物件。
* **`key`:** 與要新增的值相關聯的鍵。索引鍵是資料樹中項目的路徑。 此函式會呼叫`ContextHub.Utils.JSON.tree.sanitize`以在新增索引鍵前處理索引鍵。
* **`value`:** 要新增至資料樹的值。

##### 傳回{#returns-setitem-2}

包含`key`/ `value`對的`tree`對的副本。

##### 範例 {#example-setitem-2}

請考量下列Javascript程式碼：

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandiates {#contexthub-utils-storecandidates}

使您可以註冊儲存候選項，並獲取註冊的儲存候選項。

### 函式(ContextHub.Utils.storeCandiates){#functions-contexthub-utils-storecandidates}

#### getRegisteredCandiates(storeType){#getregisteredcandidates-storetype}

返回註冊為儲存候選項的儲存類型。 檢索特定儲存類型或所有儲存類型的註冊候選。

##### 參數 {#parameters-getregisteredcandidates}

* **`storeType`:** （字串）商店類型的名稱。請參閱[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)函式的`storeType`參數。

##### 傳回{#returns-getregisteredcandidates}

儲存類型的物件。 對象屬性是儲存類型名稱，而屬性值是已註冊儲存候選項的陣列。

#### getStoreFromCandipats(storeType){#getstorefromcandidates-storetype}

從註冊候選項返回儲存類型。 如果註冊了多個同名的儲存類型，則函式將返回具有最高優先順序的儲存類型。

##### 參數 {#parameters-getstorefromcandidates}

* `storeType`:（字串）商店候選名稱。請參閱[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies)函式的`storeType`參數。

##### 傳回{#returns-getstorefromcandidates}

表示註冊儲存候選項的對象。 如果未註冊請求的儲存類型，則會引發錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

返回註冊為儲存候選項的儲存類型的名稱。 此函式不需要參數。

##### 傳回{#returns-getsupportedstoretypes}

字串值的陣列，其中每個字串是註冊儲存候選項的儲存類型。 請參閱[`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)函式的`storeType`參數。

#### registerStoreCanditad(store, storeType, priority, applies){#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將儲存對象註冊為儲存候選項。

優先順序是指出同名商店重要性的數字。 當使用與已註冊的儲存候選相同的名稱註冊儲存候選時，使用優先順序較高的候選。 當註冊儲存候選時，僅當優先順序高於同名註冊儲存候選時，才註冊儲存。

##### 參數 {#parameters-registerstorecandidate}

* **`store`:** （物件）要註冊為儲存候選項的儲存物件。
* **`storeType`:** （字串）商店候選名稱。建立商店候選項的例項時，需要此值。
* **`priority`:** （數字）儲存候選項的優先順序。
* **`applies`:** （函式）要叫用的函式，用於評估儲存區在目前環境中的適用性。如果儲存適用，函式必須返回`true`，否則必須返回`false`。 預設值是傳回true的函式：`function() {return true;}`

##### 範例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
