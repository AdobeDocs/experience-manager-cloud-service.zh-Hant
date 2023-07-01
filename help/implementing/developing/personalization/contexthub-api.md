---
title: ContextHub JavaScript API參考
description: 將ContextHub元件新增至頁面後，您的指令碼即可使用ContextHub JavaScript API
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '4620'
ht-degree: 2%

---

# ContextHub JavaScript API參考 {#contexthub-javascript-api-reference}

ContextHub JavaScript API適用於您的指令碼，當 [ContextHub元件已新增至頁面](adding-contexthub.md).

## ContextHub常數 {#contexthub-constants}

ContextHub JavaScript API定義的常數值。

### 事件常數 {#event-constants}

下表列出ContextHub存放區發生的名稱事件。 另請參閱 [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| 常數 | 說明 | 值 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub的事件名稱空間 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 表示所有必要的存放區都已註冊、初始化，且可供使用 | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 表示在指定的逾時內並未初始化所有存放區 | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | 註冊存放區時引發 | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | 表示存放區已準備就緒。 註冊後會立即觸發，但JSONP存放區除外（會在擷取資料時觸發）。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | 在存放區更新其持續性時引發 | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 持續性容器名稱 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 儲存原始JSON結果的特定持續性金鑰名稱 | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | 儲存特定時間戳記，指出擷取JSON資料的時間 | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 儲存上次呼叫期間使用的JSON服務的特定URL | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | 指出ContextHub的UI是否展開 | `/_/container-expanded` |

### UI事件常數 {#ui-event-constants}

下表列出ContextHub UI中發生的事件名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | 註冊模式時引發 | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | 在模式取消註冊時引發 | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | 註冊模式轉譯器時引發 | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | 取消註冊模式轉譯器時引發 | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 在新增模式時引發 | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | 移除模式時引發 | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | 當使用者選取模式時引發 | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 註冊新模組時引發 | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | 模組取消註冊時引發 | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | 註冊模組轉譯器時引發 | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | 模組轉譯器取消註冊時引發 | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 在新增模組時引發 | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | 移除模組時引發 | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | 將UI容器新增至頁面時引發 | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | 開啟ContextHub UI時引發 | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | 當ContextHub UI摺疊時引發 | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | 修改屬性時引發 | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | 每次呈現ContextHub UI時引發（例如，在屬性變更後） | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | UI容器初始化時引發 | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | 指示作用中的UI模式 | `/_/active-ui-mode` |

## ContextHub JavaScript API參考 {#contexthub-javascript-api-reference-2}

ContextHub物件可讓您存取所有存放區。

### 函式(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

傳回所有已註冊的ContextHub存放區。

此函式沒有引數。

##### 傳回 {#returns-}

包含所有ContextHub存放區的物件。 每個存放區都是一個物件，使用與該存放區相同的名稱。

##### 範例 {#example-}

下列範例會擷取所有存放區，然後擷取地理位置存放區：

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

擷取作為JavaScript物件的存放區。

##### 參數 {#parameters-}

* **`name`：** 存放區註冊使用的名稱。

##### 傳回 {#returns-getstore-name}

代表存放區的物件。

##### 範例 {#example-getstore-name}

下列範例會擷取地理位置存放區：

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

代表ContextHub區段。 使用 `ContextHub.SegmentEngine.SegmentManager` 以取得區段。

### 函式(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

以字串值的形式傳回區段名稱。

#### getPath() {#getpath}

以字串值的形式傳回區段定義的存放庫路徑。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供對ContextHub區段的存取權。

### 函式(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

傳回在目前內容中解析的區段。 此函式沒有引數。

##### 傳回 {#returns-getresolvedsegments}

陣列 `ContextHub.SegmentEngine.Segment` 物件。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub存放區的基底類別。

### 屬性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) 物件。 使用此物件進行繫結函式以儲存事件。 如需預設值和初始化的相關資訊，請參閱 [`init(name,config)`](#init-name-config).

#### 名稱 {#name}

存放區名稱。

#### 持續性 {#persistence}

A `ContextHub.Utils.Persistence` 物件。 如需預設值和初始化的相關資訊，請參閱 [`init(name,config)`](#init-name-config).

### 函式(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree， options) {#addallitems-tree-options}

將資料物件或陣列與存放區資料合併。 物件或陣列中的每個索引鍵/值組都會新增至存放區(透過 `setItem` 函式)：

* **物件：** 索引鍵是屬性名稱。
* **陣列：** 索引鍵是陣列索引。

請注意，值可以是物件。

##### 參數 {#parameters-addallitems}

* **`tree`：** （物件或陣列）要新增至存放區的資料。
* **`options`：** （物件）傳遞至setItem函式之選項的選用物件。 如需詳細資訊，請參閱 `options` 引數： [`setItem(key,value,options)`](#setitem-key-value-options).

##### 傳回 {#returns-addallitems}

A `boolean` 值：

* 值 `true` 表示已儲存資料物件。
* 值 `false` 表示資料存放區未變更。

#### addReference(key， anotherKey) {#addreference-key-anotherkey}

建立從一個索引鍵到另一個索引鍵的參考。 索引鍵不能參照自身。

##### 參數 {#parameters-addreference}

* **`key`：** 參考的金鑰 `anotherKey`.

* **`anotherkey`：** 參考的金鑰 `key`.

##### 傳回 {#returns-addreference}

A `boolean` 值：

* 值 `true` 表示參照已新增。
* 值 `false` 表示未新增任何參考。

#### announceReadiness() {#announcereadiness}

觸發 `ready` 此商店的事件。 此函式沒有引數且未傳回任何值。

#### clean() {#clean}

從存放區移除所有資料。 函式沒有引數和傳回值。

#### getItem(key) {#getitem-key}

傳回與索引鍵相關聯的值。

##### 參數 {#parameters-getitem}

* **`key`：** （字串）要傳回值的索引鍵。

##### 傳回 {#returns-getitem}

代表索引鍵值的物件。

#### getKeys(includeInternals) {#getkeys-includeinternals}

從存放區擷取金鑰。 或者，您也可以擷取ContextHub架構內部使用的索引鍵。

##### 參數 {#parameters-getkeys}

* **`includeInternals`：** 值 `true` 結果中包含內部使用的索引鍵。 這些鍵以底線(`_`)個字元。 預設值為 `false`。

##### 傳回 {#returns-getkeys}

金鑰名稱的陣列( `string` 值)。

#### getReferences() {#getreferences}

從存放區擷取參考。

##### 傳回 {#returns-getreferences}

使用參照索引鍵作為參照索引鍵的索引的陣列：

* 參照索引鍵對應至 `key` 的引數 `addReference` 函式。
* 參照的索引鍵對應至 `anotherKey` 的引數 `addReference` 函式。

#### getTree(includeInternals) {#gettree-includeinternals}

從存放區擷取資料樹狀結構。 您可以選擇加入ContextHub架構在內部使用的索引鍵/值組。

##### 參數 {#parameters-gettree}

* `includeInternals:` 值 `true` 結果中包含內部使用的索引鍵/值配對。 此資料的索引鍵以底線(`_`)個字元。 預設值為 `false`。

##### 傳回 {#returns-gettree}

代表資料樹狀結構的物件。 鍵是物件的屬性名稱。

#### init(name， config) {#init-name-config}

初始化存放區。

* 將存放區資料設定為空白物件。
* 將存放區參考設定為空白物件。
* 此 `eventChannel` 是 `data:<name>`，其中 `<name>` 是存放區名稱。
* 此 `storeDataKey` 是 `/store/<name>`，其中 `<name>` 是存放區名稱。

##### 參數 {#parameters-init}

* **`name`：** 存放區名稱。
* **`config`：** 包含組態屬性的物件：
   * `eventDeferring`：預設值為32。
   * `eventing`：此 [ContextHub.Utils.Eventing](#contexthub-utils-eventing) 物件。 預設值為 `ContextHub.eventing` 物件使用。
   * `persistence`：此 `ContextHub.Utils.Persistence` 物件。 預設值為 `ContextHub.persistence` 物件。

#### isEventingPaused() {#iseventingpaused}

決定是否暫停此存放區的事件。

##### 傳回 {#returns-iseventingpaused}

布林值：

* `true`：事件已暫停，因此不會為此存放區觸發任何事件。
* `false`：事件不會暫停，因此會為此存放區觸發事件。

#### pauseEventing() {#pauseeventing}

暫停存放區的事件，以免觸發任何事件。 此函式不需要引數且不會傳回任何值。

#### removeItem(key， options) {#removeitem-key-options}

從存放區中移除索引鍵/值組。

移除索引鍵時，函式會觸發 `data` 事件。 事件資料包含存放區名稱、已移除的機碼名稱、已移除的值、機碼的新值(null)以及「移除」的動作型別。

或者，您也可以防止觸發 `data` 事件。

##### 參數 {#parameters-removeitem}

* **`key`：** （字串）要移除的金鑰名稱。
* **`options`：** （物件）選項的物件。 下列物件屬性有效：
   * silent：值 `true` 防止觸發 `data` 事件。 預設值為 `false`。

##### 傳回 {#returns-removeitem}

A `boolean` 值：

* 值 `true` 表示索引鍵/值配對已移除。
* 值 `false` 表示資料存放區未變更，因為在存放區中找不到索引鍵。

#### removeReference(key) {#removereference-key}

從存放區移除參考。

##### 參數 {#parameters-removereference}

* **`key`：** 要移除的索引鍵參考。 此引數對應至 `key` 的引數 `addReference` 函式。

##### 傳回 {#returns-removereference}

A `boolean` 值：

* 值 `true` 表示參照已移除。
* 值 `false` 表示金鑰無效，且存放區未變更。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重設存放區儲存資料的初始值。 或者，您也可以從存放區中移除所有其他資料。 當存放區重設時，此存放區的事件已暫停。 此函式未傳回任何值。

初始值提供於 `initialValues` 用來具現化存放區物件之設定物件的屬性。

##### 參數 {#parameters-reset}

* **`keepRemainingData`**：（布林值） true值會導致非初始資料持續存在。 若值為false，則會移除初始值以外的所有資料。

#### resolveReference(key， retry) {#resolvereference-key-retry}

擷取參照的索引鍵。 或者，您可以指定要用於解析最佳比對的反複專案數。

##### 參數 {#parameters-resolvereference}

* **`key`：** （字串）要解析參照的索引鍵。 此 `key` 引數對應至 `key` 的引數 `addReference` 函式。
* **`retry`：** （數目）要使用的反複專案數。

##### 傳回 {#returns-resolvereference}

A `string` 代表參考索引鍵的值。 如果未解析任何參照，則 `key` 引數會傳回。

#### resumeEventing() {#resumeeventing}

繼續此存放區的事件，以便觸發事件。 此函式不定義任何引數也不傳回任何值。

#### setItem(key， value， options) {#setitem-key-value-options}

將索引鍵/值配對新增至存放區。

觸發 `data` 只有在索引鍵的值不同於目前為索引鍵儲存的值時，才會發生事件。 您可以選擇避免觸發 `data` 事件。

事件資料包含商店名稱、金鑰、先前的值、新值和動作型別 `set`.

##### 參數 {#parameters-setitem}

* **`key`：** （字串）金鑰的名稱。
* **`options`：** （物件）選項的物件。 下列物件屬性有效：
   * `silent`：值 `true` 防止觸發 `data` 事件。 預設值為 `false`。
* **`value`：** （物件）要與索引鍵關聯的值。

##### 傳回 {#returns-setitem}

A `boolean` 值：

* 值 `true` 表示已儲存資料物件。
* 值 `false` 表示資料存放區未變更。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的存放區。 資料會從外部JSONP服務擷取，或選擇性地從傳回JSON資料的服務擷取。 使用指定服務詳細資料 [`init`](#init-name-config) 建立此類別的執行個體時執行函式。

存放區使用記憶體內持續性（JavaScript變數）。 存放區資料僅在頁面存留期內可用。

ContextHub.Store.JSONPStore延伸 [ContextHub.Store.Core](#contexthub-store-core) 並繼承該類別的函式。

### 函式(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig， override) {#configureservice-serviceconfig-override}

設定連線至此物件所使用JSONP服務的詳細資訊。 您可以更新或取代現有設定。 函式不會傳回任何值。

##### 參數 {#parameters-configureservice}

* **`serviceConfig`：** 包含下列屬性的物件：
   * `host`：（字串）伺服器名稱或IP位址。
   * `jsonp`：（布林值）如果值為true，表示服務是JSONP服務；否則為false。 為true時，{callback： &quot;ContextHub.Callbacks.*物件名稱*}物件已新增至service.params物件。
   * `params`：（物件）以物件屬性表示的URL引數。 引數名稱為屬性名稱，引數值為屬性值。
   * `path`：（字串）服務的路徑。
   * `port`：（數字）服務的連線埠號碼。
   * `secure`：（字串或布林值）決定用於服務URL的通訊協定：
      * `auto`: //
      * `true`： https://
      * `false`: http://
* **覆寫：** （布林值）。 值 `true` 導致現有服務設定被以下屬性取代： `serviceConfig`. 值 `false` 導致現有服務設定屬性與下列屬性合併： `serviceConfig`.

#### getRawResponse() {#getrawresponse}

傳回自上次呼叫JSONP服務後快取的原始回應。 函式不需要引數。

##### 傳回 {#returns-getrawresponse}

代表原始回應的物件。

#### getServiceDetails() {#getservicedetails}

擷取此ContextHub.Store.JSONPStore物件的服務物件。 服務物件包含建立服務URL所需的所有資訊。

##### 傳回 {#returns-getservicedetails}

具有下列屬性的物件：

* **`host`：** （字串）伺服器名稱或IP位址。
* **`jsonp`：** （布林值）值為true表示服務是JSONP服務，否則為false。 為true時，{callback： &quot;ContextHub.Callbacks.*物件名稱*}物件已新增至service.params物件。
* **`params`：** （物件）以物件屬性表示的URL引數。 引數名稱為屬性名稱，引數值為屬性值。
* **`path`：** （字串）服務的路徑。
* **`port`：** (Number)服務的連線埠號碼。
* **`secure`：** （字串或布林值）決定用於服務URL的通訊協定：
   * `auto`: //
   * `true`： https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

擷取JSONP服務的URL。

##### 參數 {#parameters-getserviceurl}

* **`resolve`：** （布林值）決定是否在URL中包含解析的引數。 值 `true` 解析的引數，以及 `false` 不會。

##### 傳回 {#returns-getserviceurl}

A `string` 代表服務URL的值。

#### init(name， config) {#init-name-config-1}

初始化 `ContextHub.Store.JSONPStore` 物件。

##### 參數 {#parameters-init-1}

* **`name`：** （字串）存放區的名稱。
* **`config`：** （物件）包含服務屬性的物件。 JSONPStore物件會使用 `service` 物件來建構JSONP服務的URL：
   * `eventDeferring`: 32.
   * `eventing`：此存放區的ContextHub.Utils.Eventing物件。 預設值為 `ContextHub.eventing` 物件。
   * `persistence`：此存放區的ContextHub.Utils.Persistence物件。 預設會使用記憶體持續性（JavaScript物件）。
   * `service`: (物件)
      * `host`：（字串）伺服器名稱或IP位址。
      * `jsonp`：（布林值）如果值為true，表示服務是JSONP服務；否則為false。 為真時， `{callback: "ContextHub.Callbacks.*Object.name*}`物件已新增至 `service.params`.
      * `params`：（物件）以物件屬性表示的URL引數。 引數名稱和值分別是物件屬性名稱和值。
      * `path`：（字串）服務的路徑。
      * `port`：（數字）服務的連線埠號碼。
      * `secure`：（字串或布林值）決定用於服務URL的通訊協定：
         * `auto`: //
         * `true`： https://
         * `false`: http://
      * `timeout`：（數字）逾時前等待JSONP服務回應的時間長度，以毫秒為單位。
         * `ttl`：呼叫JSONP服務之間的最小時間量（以毫秒為單位）。 (請參閱 [queryservice](#queryservice-reload) 函式)。

#### queryService（重新載入） {#queryservice-reload}

查詢遠端JSONP服務並快取回應。 如果自上次呼叫此函式後經過的時間少於 `config.service.ttl`，不會呼叫服務，且不會變更快取回應。 或者，您也可以強制呼叫服務。 此 `config.service.ttl`屬性是在呼叫 [init](#init-name-config) 函式來初始化存放區。

查詢完成時會觸發就緒事件。 如果未設定JSONP服務URL，函式不會執行任何動作。

##### 參數 {#parameters-queryservice}

* **`reload`：** （布林值） true值會移除快取回應，並強制呼叫JSONP服務。

#### 重設 {#reset}

重設存放區儲存資料的初始值，然後呼叫JSONP服務。 或者，您也可以從存放區中移除所有其他資料。 初始值重設時，此存放區的事件已暫停。 此函式未傳回任何值。

初始值是在用來具現化存放區物件之設定物件的initialValues屬性中提供。

##### 參數 {#parameters-reset-1}

* **`keepRemainingData`：** （布林值） true值會導致非初始資料持續存在。 若值為false，則會移除初始值以外的所有資料。

#### resolveParameter(f) {#resolveparameter-f}

解析給定的引數。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` 延伸 [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) 所以它會繼承該類別的所有函式。 不過，從JSONP服務擷取的資料會根據ContextHub持續性的設定持續保留。 (請參閱 [持續性模式：](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` 延伸 [ContextHub.Store.Core](#contexthub-store-core) 所以它會繼承該類別的所有函式。 此存放區中的資料會根據ContextHub持續性的設定而持續儲存。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` 延伸 [ContextHub.Store.Core](#contexthub-store-core) 所以它會繼承該類別的所有函式。 此存放區中的資料是使用記憶體內持續性（JavaScript物件）來持續儲存。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組轉譯器。

### 函式(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType， renderer， dontRender) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub註冊UI模組轉譯器。 註冊轉譯器後，它可用於 [建立使用者介面模組](configuring-contexthub.md#adding-a-ui-module). 請在以下情況下使用此函式： [延伸 `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) 以建立自訂UI模組轉譯器。

##### 參數 {#parameters-registerrenderer}

* **`moduleType`：** （字串） UI模組轉譯器的識別碼。 如果已使用指定的值註冊轉譯器，則在註冊此轉譯器之前會先取消註冊現有的轉譯器。
* **`renderer`：** （字串）轉譯UI模組的類別名稱。
* **`dontRender`：** （布林值）設為 `true` 以防止在註冊轉譯器後轉譯ContextHub UI。 預設值為 `false`。

##### 範例 {#example-registerrenderer}

下列範例會將轉譯器註冊為 `contexthub.browserinfo` 模組型別。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

與Cookie互動的公用程式類別。

### 函式(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists（鍵） {#exists-key}

判斷Cookie是否存在。

##### 參數 {#parameters-exists}

* **`key`：** A `String` 包含您正在測試之Cookie的金鑰。

##### 傳回 {#returns-exists}

A `boolean` true值表示Cookie存在。

##### 範例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

傳回索引鍵符合篩選器的所有Cookie。

##### 參數 {#parameters-getallitems}

* **`filter`：** （選用）比對Cookie金鑰的條件。 若要傳回所有Cookie，請勿指定任何值。 支援下列型別：
   * 字串：字串會與Cookie金鑰進行比較。
   * 陣列：陣列中的每個專案都是一個篩選器。
   * RegExp物件：物件的測試函式用於比對Cookie索引鍵。
   * 函式：測試Cookie金鑰以符合的函式。 函式必須將Cookie金鑰視為引數，如果測試確認相符，則傳回true。

##### 傳回 {#returns-getallitems}

Cookie的物件。 物件屬性是Cookie索引鍵，而索引鍵值是Cookie值。

##### 範例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

傳回Cookie值。

##### 參數 {#parameters-getitem-1}

* **`key`：** 您要其值之Cookie的金鑰。

##### 傳回 {#returns-getitem-1}

Cookie值，或 `null` 如果找不到索引鍵的Cookie。

##### 範例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

傳回符合篩選器的現有Cookie索引鍵陣列。

##### 參數 {#parameters-getkeys-1}

* **`filter`：** 符合Cookie金鑰的條件。 支援下列型別：
   * 字串：字串會與Cookie金鑰進行比較。
   * 陣列：陣列中的每個專案都是一個篩選器。
   * RegExp物件：物件的測試函式用於比對Cookie索引鍵。
   * 函式：測試Cookie金鑰以符合的函式。 函式必須以Cookie金鑰作為引數，並傳回 `true` 如果測試確認相符專案。

##### 傳回 {#returns-getkeys-1}

字串陣列，其中每個字串都是符合篩選器的Cookie索引鍵。

##### 範例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key， options) {#removeitem-key-options-1}

移除Cookie。 若要移除Cookie，值會設為空字串，而到期日會設為目前日期的前一天。

##### 參數 {#parameters-removeitem-1}

* **`key`：** A `String` 代表要移除之Cookie索引鍵的值。
* **`options`：** 包含用於設定Cookie屬性的屬性值的物件。 請參閱 [`setItem`](#setitem-key-value-options) 函式以取得資訊。 此 `expires` 屬性沒有作用。

##### 傳回 {#returns-removeitem-1}

此函式未傳回值。

##### 範例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key， value， options) {#setitem-key-value-options-1}

建立指定索引鍵和值的Cookie，並將Cookie新增至目前檔案。 或者，您可以指定設定Cookie屬性的選項。

##### 參數 {#parameters-setitem-1}

* **`key`：** 包含Cookie金鑰的字串。
* **`value`：** 包含Cookie值的字串。
* **`options`：** （選用）包含下列任何屬性以設定Cookie屬性的物件：
   * `expires`：A `date` 或 `number` 指定Cookie過期時間的值。 日期值會指定到期的絕對時間。 數字（以天為單位）會將到期時間設定為目前時間加上數字。 預設值為 `undefined`。
   * `secure`：A `boolean` 值，指定 `Secure` Cookie的屬性。 預設值為 `false`。
   * `path`：A `String` 要用作 `Path` Cookie的屬性。 預設值為 `undefined`。

##### 傳回 {#returns-setitem-1}

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

#### 消失（篩選，選項） {#vanish-filter-options}

移除符合指定篩選器的所有Cookie。 Cookie是使用 `getKeys` 函式並使用 `removeItem` 函式。

##### 參數 {#parameters-vanish}

* **`filter`：** 此 `filter` 用於呼叫中的引數 [`getKeys`](#getkeys-filter) 函式。
* **`options`：** 此 `options` 用於呼叫中的引數 [`removeItem`](#removeitem-key-options) 函式。

##### 傳回 {#returns-vanish}

此函式未傳回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

可讓您將函式繫結和解除繫結至ContextHub存放區事件。 存取 `ContextHub.Utils.Eventing` 物件(使用 [事件](#eventing) 存放區的屬性。

### 函式(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name， selector) {#off-name-selector}

從事件中取消繫結函式。

##### 參數 {#parameters-off}

* **`name`：** 此 [事件名稱](#contexthub-utils-eventing) 您正在解除繫結函式的對象。
* **`selector`：** 識別繫結的選擇器。 (請參閱 `selector` 的引數 [`on`](#on-name-handler-selector-triggerforpastevents) 和 [`once`](#once-name-handler-selector-triggerforpastevents) 函式)。

##### 傳回 {#returns-off}

此函式未傳回任何值。

#### on(name， handler， selector， triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

將函式繫結至事件。 每次發生事件時都會呼叫函式。 或者，您也可以針對過去發生的事件，在建立繫結之前呼叫函式。

##### 參數 {#parameters-on}

* **`name`：** （字串） [事件名稱](#contexthub-utils-eventing) 您要將函式繫結到哪個位置。
* **`handler`：** （函式）繫結至事件的函式。
* **`selector`：** （字串）繫結的唯一識別碼。 如果要使用，則需要選擇器來識別繫結 `off` 函式以移除繫結。
* **`triggerForPastEvents`：** （布林值）指出是否應為過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 呼叫未來事件的處理常式。 預設值為 `true`。

##### 傳回 {#returns-on}

當 `triggerForPastEvents` 引數為 `true`，此函式傳回 `boolean` 指出事件是否過去發生的值：

* `true`：此事件發生在過去，且系統會呼叫處理常式。
* `false`：此事件過去未發生。

若 `triggerForPastEvents` 是 `false`，此函式不會傳回任何值。

##### 範例 {#example-on}

下列範例會將函式繫結至地理位置存放區的資料事件。 函式會使用儲存區中latitude資料專案的值填入頁面上的元素。

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

#### once(name， handler， selector， triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

將函式繫結至事件。 函式只會在第一次發生事件時呼叫一次。 您可以選擇在建立繫結之前，為過去發生的事件呼叫函式。

##### 參數 {#parameters-once}

* **`name`：** （字串） [事件名稱](#contexthub-utils-eventing) 您要將函式繫結到哪個位置。
* **`handler`：** （函式）繫結至事件的函式。
* **`selector`：** （字串）繫結的唯一識別碼。 如果要使用，則需要選擇器來識別繫結 `off` 函式以移除繫結。
* **`triggerForPastEvents`：** （布林值）指出是否應為過去發生的事件執行處理常式。 值 `true` 呼叫過去事件的處理常式。 值 `false` 呼叫未來事件的處理常式。 預設值為 `true`。

##### 傳回 {#returns-once}

當 `triggerForPastEvents` 引數為 `true`，此函式傳回 `boolean` 指出事件是否過去發生的值：

* `true`：此事件發生在過去，且系統會呼叫處理常式。
* `false`：此事件過去未發生。

若 `triggerForPastEvents` 是 `false`，此函式不會傳回任何值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

讓物件繼承另一個物件之屬性和方法的公用程式類別。

### 函式(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child， parent) {#inherit-child-parent}

讓物件繼承另一個物件的屬性和方法。

##### 參數 {#parameters-inherit}

* **`child`：** （物件）繼承的物件。
* **`parent`：** （物件）定義繼承之屬性和方法的物件。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供將物件序列化為JSON格式和將JSON字串還原序列化為物件的函式。

### 函式(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

將字串值剖析為JSON並將其轉換為Javascript物件。

##### 參數 {#parameters-parse}

* **`data`：** JSON格式的字串值。

##### 傳回 {#returns-parse}

javascript物件。

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

#### stringify(data) {#stringify-data}

將JavaScript值和物件序列化為JSON格式的字串值。

##### 參數 {#parameters-stringify}

* **`data`：** 要序列化的值或物件。 此函式支援布林值、陣列、數字、字串和日期值。

##### 傳回 {#returns-stringify}

序列化字串值。 時間 `data` 是R `egExp` 值，此函式傳回空白物件。 時間 `data` 為函式，傳回 `undefined`.

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

此類別有助於處理要儲存或從ContextHub存放區擷取的資料物件。

### 函式(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料物件的復本，並從第二個物件新增至資料樹狀結構。 函式會傳回副本，而不會修改任何原始物件。 當兩個物件的資料樹包含相同的索引鍵時，第二個物件的值會覆寫第一個物件的值。

##### 參數 {#parameters-addallitems-1}

* **`tree`：** 複製的物件。
* **`secondTree`：** 與復本合併的物件 `tree` 物件。

##### 傳回 {#returns-addallitems-1}

包含合併資料的物件。

#### cleanup() {#cleanup}

建立物件的復本，尋找並移除資料樹狀結構中不含任何值、null值或未定義值的專案，然後傳回覆本。

##### 參數 {#parameters-cleanup}

* **`tree`：** 要清除的物件。

##### 傳回 {#returns-cleanup}

已清除的樹狀結構復本。

#### getItem() {#getitem}

從物件擷取索引鍵的值。

##### 參數 {#parameters-getitem-2}

* **`tree`：** 資料物件。
* **`key`：** 您要擷取之值的索引鍵。

##### 傳回 {#returns-getitem-2}

與索引鍵對應的值。 當索引鍵具有子索引鍵時，此函式會傳回複雜物件。 當索引鍵值的型別是 `undefined`， `null` 會傳回。

##### 範例 {#example-getitem-2}

請考量下列JavaScript物件：

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

下列範常式式碼會傳回值 `260`：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

下列範常式式碼會擷取具有子索引鍵的索引鍵的值：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

此函式傳回以下物件：

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

從物件的資料樹狀結構中擷取所有索引鍵。 或者，您只能擷取特定鍵的子系鍵值。 您也可以選擇指定擷取之索引鍵的排序順序。

##### 參數 {#parameters-getkeys-2}

* **`tree`：** 要從中擷取資料樹狀結構索引鍵的物件。
* **`parent`：** （選用）資料樹狀結構中要擷取子專案索引鍵的專案索引鍵。
* **`order`：** （選用）決定傳回索引鍵排序順序的函式。 (請參閱 [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) （在Mozilla Developer Network上）。

##### 傳回 {#returns-getkeys-2}

索引鍵陣列。

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

此 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 指令碼傳回下列陣列：

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立指定物件的復本、從資料樹狀結構中移除指定分支，並傳回修改後的復本。

##### 參數 {#parameters-removeitem-2}

* **`tree`：** 資料物件。
* **`key`：** 要移除的金鑰。

##### 傳回 {#returns-removeitem-2}

移除金鑰的原始資料物件復本。

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

以下範例指令碼會從資料樹狀結構中移除/one/two/three/four分支：

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

此函式傳回以下物件：

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

清除字串值，使其可作為索引鍵使用。 若要清除字串，此函式會執行下列動作：

* 將多個連續正斜線減少為單一斜線。
* 移除字串開頭和結尾的空格。
* 將結果分割成以斜線分隔的字串陣列。

使用結果陣列來建立可用的索引鍵。

##### 參數 {#parameters-sanitizekey}

* **`key`：** 此 `string` 以利處理。

##### 傳回 {#returns-sanitizekey}

陣列 `string` 值，其中每個字串都是 `key` 以斜線標示。 代表已清除的金鑰。 如果經過清理的陣列長度為零，此函式會傳回 `null`.

##### 範例 {#example-sanitizekey}

下列程式碼會清理字串以產生陣列 `["this", "is", "a", "path"]`，然後產生金鑰 `"/this/is/a/path"` 從陣列：

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree， key， value) {#setitem-tree-key-value}

將索引鍵/值配對新增至物件副本的資料樹狀結構。 如需資料樹狀結構的相關資訊，請參閱 [持續性。](contexthub.md#persistence)

##### 參數 {#parameters-setitem-2}

* **`tree`：** 資料物件。
* **`key`：** 要與您新增的值產生關聯的索引鍵。 索引鍵是資料樹狀結構中專案的路徑。 此函式呼叫 `ContextHub.Utils.JSON.tree.sanitize` 以在新增金鑰之前對其進行清理處理。
* **`value`：** 要新增至資料樹狀結構的值。

##### 傳回 {#returns-setitem-2}

「 」的副本 `tree` 物件，包括 `key`/ `value` 配對。

##### 範例 {#example-setitem-2}

考量下列JavaScript程式碼：

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

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

可讓您註冊商店候選者，並取得註冊的商店候選者。

### 函式(ContextHub.Utils.storeCategers) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

傳回註冊為候選商店的商店型別。 擷取特定商店型別或所有商店型別的註冊候選項。

##### 參數 {#parameters-getregisteredcandidates}

* **`storeType`：** （字串）商店型別的名稱。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 函式。

##### 傳回 {#returns-getregisteredcandidates}

存放區型別的物件。 物件屬性是存放區型別名稱，而屬性值是註冊存放區候選者的陣列。

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

從註冊的候選者中傳回存放區型別。 如果註冊了多個相同名稱的存放區型別，此函式會傳回具有最高優先順序的存放區型別。

##### 參數 {#parameters-getstorefromcandidates}

* `storeType`：（字串）候選商店的名稱。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) 函式。

##### 傳回 {#returns-getstorefromcandidates}

代表已註冊商店候選者的物件。 如果未登入要求的存放區型別，則會擲回錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

傳回註冊為候選商店的商店型別名稱。 此函式不需要引數。

##### 傳回 {#returns-getsupportedstoretypes}

字串值的陣列，其中每個字串都是用來登入存放區候選的存放區型別。 請參閱 `storeType` 的引數 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 函式。

#### registerStoreCandidate(store， storeType， priority， applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將存放區物件註冊為存放區候選。

優先順序是一個數字，可指出同名存放區的重要性。 當使用與已註冊商店候選相同的名稱註冊商店候選時，會使用具有較高優先順序的候選者。 註冊候選商店時，只有當優先順序高於同名已註冊候選商店時，才會註冊該商店。

##### 參數 {#parameters-registerstorecandidate}

* **`store`：** （物件）要註冊為商店候選者的商店物件。
* **`storeType`：** （字串）候選商店的名稱。 建立存放區候選執行個體時，需要此值。
* **`priority`：** （數字）商店候選的優先順序。
* **`applies`：** （函式）要呼叫的函式，會評估存放區在目前環境中的適用性。 函式必須傳回 `true` 是否適用，以及 `false` 否則。 預設值是傳回true的函式： `function() {return true;}`

##### 範例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
