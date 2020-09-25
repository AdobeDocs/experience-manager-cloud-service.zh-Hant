---
title: ContextHub Javascript API參考
description: 當ContextHub元件已新增至頁面時，指令碼可使用ContextHub Javascript API
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 1%

---


# ContextHub Javascript API參考 {#contexthub-javascript-api-reference}

當ContextHub元件已新增至頁面時，指令碼 [可使用ContextHub Javascript API](adding-contexthub.md)。

## ContextHub常數 {#contexthub-constants}

ContextHub Javascript API所定義的常數值。

### 事件常數 {#event-constants}

下表列出了ContextHub Stores發生的名稱事件。 另請參閱 [ContextHub.Utils.Eventing](#contexthub-utils-eventing)。

| 常數 | 說明 | 值 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub的事件命名空間 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 指示所有必需儲存都已註冊、初始化並準備使用 | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 表示並非所有儲存都在指定超時內初始化 | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | 在註冊商店時引發 | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | 指出商店已準備就緒。 註冊後會立即觸發，但JSONP儲存區除外，當擷取資料時會觸發)。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | 當商店更新其永續性時引發 | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 永續性容器名稱 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 儲儲存存原始JSON結果的特定永續性金鑰名稱 | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | 儲存指示擷取JSON資料時的特定時間戳記 | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 儲存上次呼叫期間使用之JSON服務的特定URL | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | 指出ContextHub的UI是否已展開 | `/_/container-expanded` |

### UI事件常數 {#ui-event-constants}

下表列出ContextHub UI發生的事件名稱。

| **常數** | **說明** | **值** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | 註冊模式時引發 | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | 未註冊模式時引發 | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | 在註冊模式轉換器時引發 | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | 當模式轉換器未註冊時引發 | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 新增模式時引發 | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | 移除模式時引發 | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | 當使用者選取模式時引發 | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 註冊新模組時引發 | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | 未註冊模組時引發 | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | 在註冊模組轉譯器時引發 | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | 在未註冊模組渲染器時引發 | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 新增模組時引發 | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | 移除模組時引發 | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | 將UI容器新增至頁面時引發 | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | 開啟ContextHub UI時引發 | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | 在收合ContextHub UI時引發 | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | 修改屬性時引發 | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | 每次轉譯ContextHub UI時引發（例如在屬性變更後） | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | 初始化UI容器時引發 | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | 指示活動的UI模式 | `/_/active-ui-mode` |

## ContextHub Javascript API參考 {#contexthub-javascript-api-reference-2}

ContextHub物件可讓您存取所有商店。

### 函式(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

傳回所有已註冊的ContextHub儲存區。

此函式沒有參數。

##### 退貨 {#returns-}

包含所有ContextHub儲存的對象。 每個商店都是使用與商店相同名稱的物件。

##### 範例 {#example-}

下面的示例檢索所有儲存，然後檢索地理位置儲存：

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

將商店擷取為Javascript物件。

##### 參數 {#parameters-}

* **`name`:** 註冊商店的名稱。

##### 退貨 {#returns-getstore-name}

表示儲存的對象。

##### 範例 {#example-getstore-name}

下面的示例檢索地理位置儲存：

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

代表ContextHub區段。 使用以 `ContextHub.SegmentEngine.SegmentManager` 取得區段。

### 函式(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

傳回區段名稱為字串值。

#### getPath() {#getpath}

傳回區段定義的儲存庫路徑，作為字串值。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

提供ContextHub區段的存取權。

### 函式(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

傳回在目前內容中解析的區段。 此函式沒有參數。

##### 退貨 {#returns-getresolvedsegments}

物件數 `ContextHub.SegmentEngine.Segment` 組。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub的基類。

### 屬性(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 事件 {#eventing}

物 [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) 件。 使用此物件來系結函式以儲存事件。 有關預設值和初始化的資訊，請參見 [`init(name,config)`](#init-name-config)。

#### 名稱 {#name}

商店名稱。

#### 持久性 {#persistence}

物 `ContextHub.Utils.Persistence` 件。 有關預設值和初始化的資訊，請參見 [`init(name,config)`](#init-name-config)。

### 函式(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

合併資料對象或陣列與儲存資料。 對象或陣列中的每個鍵／值對都添加到儲存中(通過函 `setItem` 數):

* **物件：** 鍵是屬性名稱。
* **陣列：** 鍵是陣列索引。

請注意，值可以是物件。

##### 參數 {#parameters-addallitems}

* **`tree`:** （物件或陣列）要新增至儲存區的資料。
* **`options`:** （物件）傳遞至setItem函式的選項選項物件。 有關資訊，請參 `options` 見的參 [`setItem(key,value,options)`](#setitem-key-value-options)數。

##### 退貨 {#returns-addallitems}

值 `boolean` :

* 值表示 `true` 已儲存資料對象。
* 值表示 `false` 資料儲存區未變更。

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

建立從一個鍵到另一個鍵的引用。 鍵不能參照自身。

##### 參數 {#parameters-addreference}

* **`key`:** 引用的鍵 `anotherKey`。

* **`anotherkey`:** 參考的索引鍵 `key`。

##### 退貨 {#returns-addreference}

值 `boolean` :

* 值表示 `true` 已添加引用。
* 值表示 `false` 未添加任何引用。

#### announceReadiness() {#announcereadiness}

觸發此 `ready` 商店的事件。 此函式沒有參數，也不返回值。

#### clean() {#clean}

從商店移除所有資料。 函式沒有參數，也沒有返回值。

#### getItem(key) {#getitem-key}

傳回與索引鍵相關聯的值。

##### 參數 {#parameters-getitem}

* **`key`:** （字串）要傳回值的索引鍵。

##### 退貨 {#returns-getitem}

表示鍵值的對象。

#### getKeys(includeInternals) {#getkeys-includeinternals}

從商店擷取金鑰。 或者，您可以檢索ContextHub框架內部使用的鍵。

##### 參數 {#parameters-getkeys}

* **`includeInternals`:** 值包括 `true` 結果中內部使用的鍵。 這些鍵以下划線(`_`)字元開頭。 預設值為 `false`。

##### 退貨 {#returns-getkeys}

索引鍵名稱（值） `string` 的陣列。

#### getReferences() {#getreferences}

從儲存中檢索引用。

##### 退貨 {#returns-getreferences}

使用引用鍵作為引用鍵索引的陣列：

* 引用鍵與函 `key` 數的參數相 `addReference` 對應。
* 引用的鍵與函 `anotherKey` 數的參數相 `addReference` 對應。

#### getTree(includeInternals) {#gettree-includeinternals}

從儲存中檢索資料樹。 或者，您可以包含ContextHub架構內部使用的索引鍵／值配對。

##### 參數 {#parameters-gettree}

* `includeInternals:` 值包括 `true` 結果中內部使用的鍵／值對。 此資料的索引鍵以底線(`_`)字元開頭。 預設值為 `false`。

##### 退貨 {#returns-gettree}

表示資料樹的對象。 鍵是對象的屬性名稱。

#### init(name, config) {#init-name-config}

初始化儲存。

* 將儲存資料設定為空對象。
* 設定空對象的儲存引用。
* 是 `eventChannel` ，其 `data:<name>`中 `<name>` 是商店名稱。
* 是 `storeDataKey` ，其 `/store/<name>`中 `<name>` 是商店名稱。

##### 參數 {#parameters-init}

* **`name`:** 商店名稱。
* **`config`:** 包含配置屬性的對象：
   * `eventDeferring`:預設值為32。
   * `eventing`:此存 [儲的ContextHub.Utils.Eventing](#contexthub-utils-eventing) 對象。 預設值是對象 `ContextHub.eventing` 所使用的。
   * `persistence`:此存 `ContextHub.Utils.Persistence` 儲的對象。 預設值是對 `ContextHub.persistence` 像。

#### isEventingPaused() {#iseventingpaused}

判斷是否暫停此商店的事件。

##### 退貨 {#returns-iseventingpaused}

布林值：

* `true`:事件會暫停，因此不會觸發此商店的事件。
* `false`:事件不會暫停，因此會觸發此商店的事件。

#### pauseEventing() {#pauseeventing}

暫停商店的事件，以便不觸發任何事件。 此函式不需要參數，也不返回值。

#### removeItem(key, options) {#removeitem-key-options}

從商店移除金鑰／值配對。

移除索引鍵時，函式會觸發事 `data` 件。 事件資料包括商店名稱、已移除的金鑰名稱、已移除的值、金鑰的新值(null)，以及動作類型「remove」。

（可選）您可以防止觸發事 `data` 件。

##### 參數 {#parameters-removeitem}

* **`key`:** （字串）要移除的索引鍵名稱。
* **`options`:** （物件）選項的物件。 以下對象屬性有效：
   * silent:值可避 `true` 免觸發事 `data` 件。 預設值為 `false`。

##### 退貨 {#returns-removeitem}

值 `boolean` :

* 值表示 `true` 已刪除鍵／值對。
* 值表示 `false` 資料儲存區未變更，因為在儲存區中找不到金鑰。

#### removeReference(key) {#removereference-key}

從商店移除參考。

##### 參數 {#parameters-removereference}

* **`key`:** 要刪除的鍵引用。 此參數與函 `key` 數的參 `addReference` 數。

##### 退貨 {#returns-removereference}

值 `boolean` :

* 值表示 `true` 已刪除該引用。
* 值表 `false` 示索引鍵無效，且商店不變。

#### reset(keepRemainingData) {#reset-keepremainingdata}

重設商店持續資料的初始值。 或者，您可以從商店移除所有其他資料。 重設商店時，會暫停此商店的事件。 此函式不返回值。

初始值提供在用 `initialValues` 於實例化儲存對象的config對象的屬性中。

##### 參數 {#parameters-reset}

* **`keepRemainingData`**:（布林值）若值為true，則會保留非初始資料。 值false會移除除初始值以外的所有資料。

#### resolveReference(key, retry) {#resolvereference-key-retry}

檢索引用的鍵。 或者，您可以指定用於解析最佳匹配的迭代次數。

##### 參數 {#parameters-resolvereference}

* **`key`:** （字串）要解析引用的鍵。 此 `key` 參數與函 `key` 數的參數相 `addReference` 對應。
* **`retry`:** （數量）要使用的小版本數。

##### 退貨 {#returns-resolvereference}

代 `string` 表引用鍵的值。 如果未解析引用，則返回參 `key` 數的值。

#### resumeEventing() {#resumeeventing}

繼續此商店的事件，以觸發事件。 此函式不定義任何參數，也不返回值。

#### setItem(key, value, options) {#setitem-key-value-options}

新增金鑰／值配對至商店。

只有在 `data` 索引鍵的值與目前儲存的索引鍵值不同時，才會觸發事件。 您可以選擇性地防止事件的觸 `data` 發。

事件資料包括商店名稱、金鑰、上一個值、新值和動作類型 `set`。

##### 參數 {#parameters-setitem}

* **`key`:** （字串）金鑰的名稱。
* **`options`:** （物件）選項的物件。 以下對象屬性有效：
   * `silent`:值可避 `true` 免觸發事 `data` 件。 預設值為 `false`。
* **`value`:** （物件）與索引鍵關聯的值。

##### 退貨 {#returns-setitem}

值 `boolean` :

* 值表示 `true` 已儲存資料對象。
* 值表示 `false` 資料儲存區未變更。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

包含JSON資料的商店。 資料會從外部JSONP服務中擷取，或選擇性地從傳回JSON資料的服務中擷取。 建立此類的實例時， [`init`](#init-name-config) 使用函式指定服務詳細資訊。

商店使用記憶體內永續性（Javascript變數）。 只有在頁面的存留期間，才能使用儲存資料。

ContextHub.Store.JSONPStore擴充 [了ContextHub.Store.Core](#contexthub-store-core) ，並繼承了該類的功能。

### 函式(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

配置用於連接到此對象使用的JSONP服務的詳細資訊。 您可以更新或替換現有配置。 函式不返回值。

##### 參數 {#parameters-configureservice}

* **`serviceConfig`:** 包含下列屬性的物件：
   * `host`:（字串）伺服器名稱或IP位址。
   * `jsonp`:（布爾值）值為true表示服務是JSONP服務，否則為false。 若為true，則為{callback:&quot;ContextHub.Callbacks.*Object.name*}物件會新增至service.params物件。
   * `params`:（物件）URL參數，表示為物件屬性。 參數名稱是屬性名稱，參數值是屬性值。
   * `path`:（字串）服務的路徑。
   * `port`:（編號）服務的埠號。
   * `secure`:（字串或布林值）決定用於服務URL的通訊協定：
      * `auto`: //
      * `true`:https://
      * `false`: http://
* **覆蓋：** （布林值）。 值使現 `true` 有服務配置被的屬性替換 `serviceConfig`。 值使現 `false` 有服務配置屬性與的屬性合併 `serviceConfig`。

#### getRawResponse() {#getrawresponse}

傳回自上次呼叫JSONP服務後快取的原始回應。 函式不需要參數。

##### 退貨 {#returns-getrawresponse}

表示原始回應的物件。

#### getServiceDetails() {#getservicedetails}

擷取此ContextHub.Store.JSONPStore物件的服務物件。 服務對象包含建立服務URL所需的所有資訊。

##### 退貨 {#returns-getservicedetails}

具有以下屬性的對象：

* **`host`:** （字串）伺服器名稱或IP位址。
* **`jsonp`:** （布爾值）值為true表示服務是JSONP服務，否則為false。 若為true，則為{callback:&quot;ContextHub.Callbacks.*Object.name*}物件會新增至service.params物件。
* **`params`:** （物件）URL參數，表示為物件屬性。 參數名稱是屬性名稱，參數值是屬性值。
* **`path`:** （字串）服務的路徑。
* **`port`:** （編號）服務的埠號。
* **`secure`:** （字串或布林值）決定用於服務URL的通訊協定：
   * `auto`: //
   * `true`:https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

擷取JSONP服務的URL。

##### 參數 {#parameters-getserviceurl}

* **`resolve`:** （布林值）判斷是否在URL中包含已解析的參數。 解析參 `true` 數的值， `false` 則否。

##### 退貨 {#returns-getserviceurl}

代 `string` 表服務URL的值。

#### init(name, config) {#init-name-config-1}

初始化 `ContextHub.Store.JSONPStore` 對象。

##### 參數 {#parameters-init-1}

* **`name`:** （字串）商店名稱。
* **`config`:** （對象）包含service屬性的對象。 JSONPStore物件使用物件的 `service` 屬性來建構JSONP服務的URL:
   * `eventDeferring`: 32.
   * `eventing`:此商店的ContextHub.Utils.Eventing物件。 預設值是對 `ContextHub.eventing` 像。
   * `persistence`:此儲存的ContextHub.Utils.Persistence對象。 依預設，會使用記憶體永續性（Javascript物件）。
   * `service`: (物件)
      * `host`:（字串）伺服器名稱或IP位址。
      * `jsonp`:（布爾值）值為true表示服務是JSONP服務，否則為false。 如果為true，則 `{callback: "ContextHub.Callbacks.*Object.name*}`將對象添加到 `service.params`。
      * `params`:（物件）URL參數，表示為物件屬性。 參數名稱和值分別是對象屬性名稱和值。
      * `path`:（字串）服務的路徑。
      * `port`:（編號）服務的埠號。
      * `secure`:（字串或布林值）決定用於服務URL的通訊協定：
         * `auto`: //
         * `true`:https://
         * `false`: http://
      * `timeout`:（數量）等待JSONP服務在超時前響應的時間（以毫秒為單位）。
         * `ttl`:在呼叫JSONP服務之間傳遞的最小時間（以毫秒為單位）。 (請參 [閱queryService](#queryservice-reload) 函式)。

#### queryService(reload) {#queryservice-reload}

查詢遠程JSONP服務並快取響應。 如果自上次呼叫此函式以來的時間量小於值 `config.service.ttl`，則不會呼叫服務，且快取回應不會變更。 或者，您可以強制呼叫服務。 調 `config.service.ttl`用init函式初始化存 [儲時](#init-name-config) ，將設定屬性。

在查詢完成時觸發ready事件。 如果未設定JSONP服務URL，則函式將不執行任何操作。

##### 參數 {#parameters-queryservice}

* **`reload`:** （布爾值）值true會移除快取的回應，並強制呼叫JSONP服務。

#### 重設 {#reset}

重設商店持續資料的初始值，然後呼叫JSONP服務。 或者，您可以從商店移除所有其他資料。 在重設初始值時，會暫停此商店的事件。 此函式不返回值。

初始值會提供在用於執行個體化商店物件之config物件的initialValues屬性中。

##### 參數 {#parameters-reset-1}

* **`keepRemainingData`:** （布林值）若值為true，則會保留非初始資料。 值false會移除除初始值以外的所有資料。

#### resolveParameter(f) {#resolveparameter-f}

解析給定參數。

## ContextHub.Store.PeristedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` 擴充 [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) ，讓它繼承該類別的所有功能。 但是，從JSONP服務中檢索的資料會根據ContextHub持久性的配置進行保存。 (請參 [閱永續模式：](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PeristedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` 擴充 [ContextHub.Store.Core](#contexthub-store-core) ，以繼承該類別的所有功能。 此儲存中的資料會根據ContextHub持久性的配置進行保存。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` 擴充 [ContextHub.Store.Core](#contexthub-store-core) ，以繼承該類別的所有功能。 此儲存區中的資料會使用記憶體內持久性（Javascript物件）來保存。

## ContextHub.UI {#contexthub-ui}

管理UI模組和UI模組轉譯器。

### 函式(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

向ContextHub註冊UI模組轉換器。 在註冊轉譯器後，它可用來建立 [UI模組](configuring-contexthub.md#adding-a-ui-module)。 當您擴充功能以建立自 [訂UI `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) 模組轉譯器時，請使用此函式。

##### 參數 {#parameters-registerrenderer}

* **`moduleType`:** （字串）UI模組轉譯器的識別碼。 如果已使用指定值註冊了渲染器，則在註冊此渲染器之前會先取消註冊現有渲染器。
* **`renderer`:** （字串）轉譯UI模組的類別名稱。
* **`dontRender`:** （布林值）設 `true` 定為防止在註冊轉譯器後轉譯ContextHub UI。 預設值為 `false`。

##### 範例 {#example-registerrenderer}

下面的示例將渲染器註冊為模 `contexthub.browserinfo` 塊類型。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

與Cookie互動的公用程式類別。

### 函式(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

判斷Cookie是否存在。

##### 參數 {#parameters-exists}

* **`key`:** 包 `String` 含您測試之Cookie之金鑰的A。

##### 退貨 {#returns-exists}

值 `boolean` 為true表示Cookie存在。

##### 範例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

傳回所有具有符合篩選條件之索引鍵的Cookie。

##### 參數 {#parameters-getallitems}

* **`filter`:** （選用）符合Cookie金鑰的條件。 若要傳回所有Cookie，請指定無值。 支援下列類型：
   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp對象：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰符合的函式。 函式必須將Cookie金鑰當作參數，並在測試確認相符時傳回true。

##### 退貨 {#returns-getallitems}

Cookie的物件。 物件屬性是Cookie金鑰，而金鑰值是Cookie值。

##### 範例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

傳回Cookie值。

##### 參數 {#parameters-getitem-1}

* **`key`:** 您要其值的Cookie金鑰。

##### 退貨 {#returns-getitem-1}

Cookie值，或是 `null` 找不到該金鑰的Cookie。

##### 範例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

傳回符合篩選條件之現有Cookie的索引鍵陣列。

##### 參數 {#parameters-getkeys-1}

* **`filter`:** 符合Cookie金鑰的條件。 支援下列類型：
   * 字串：字串會與Cookie金鑰比較。
   * 陣列：陣列中的每個項目都是篩選器。
   * RegExp對象：物件的測試函式可用來比對Cookie金鑰。
   * 函式：測試Cookie金鑰符合的函式。 如果測試確認符合，函式必須將Cookie金鑰 `true` 當做參數並傳回。

##### 退貨 {#returns-getkeys-1}

字串陣列，其中每個字串是符合篩選條件之Cookie的索引鍵。

##### 範例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

移除Cookie。 若要移除Cookie，此值會設為空字串，到期日會設為目前日期的前一天。

##### 參數 {#parameters-removeitem-1}

* **`key`:** 代 `String` 表要移除之Cookie之金鑰的值。
* **`options`:** 包含用於配置Cookie屬性的屬性值的對象。 如需詳細 [`setItem`](#setitem-key-value-options) 資訊，請參閱函式。 該屬 `expires` 性沒有作用。

##### 退貨 {#returns-removeitem-1}

此函式不會傳回值。

##### 範例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

建立指定金鑰和值的Cookie，並將Cookie新增至目前檔案。 或者，您可以指定設定Cookie屬性的選項。

##### 參數 {#parameters-setitem-1}

* **`key`:** 包含Cookie索引鍵的字串。
* **`value`:** 包含Cookie值的字串。
* **`options`:** （可選）包含下列任何屬性的物件，可設定Cookie屬性：
   * `expires`:指定 `date` Cookie到 `number` 期時間的或值。 日期值指定到期的絕對時間。 數字（以天為單位）會將到期時間設定為目前時間加上數字。 預設值為 `undefined`。
   * `secure`:指 `boolean` 定Cookie屬性 `Secure` 的值。 預設值為 `false`。
   * `path`:用 `String` 作Cookie屬性 `Path` 的值。 預設值為 `undefined`。

##### 退貨 {#returns-setitem-1}

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

#### 消失（濾鏡，選項） {#vanish-filter-options}

移除所有符合指定篩選的Cookie。 Cookie會使用函式進行 `getKeys` 比對，並使用函式 `removeItem` 移除。

##### 參數 {#parameters-vanish}

* **`filter`:** 在 `filter` 函式調用中使用的 [`getKeys`](#getkeys-filter) 參數。
* **`options`:** 在 `options` 函式調用中使用的 [`removeItem`](#removeitem-key-options) 參數。

##### 退貨 {#returns-vanish}

此函式不會傳回值。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

可讓您將函式系結並解除系結至ContextHub儲存事件。 使 `ContextHub.Utils.Eventing` 用商店的事件屬 [性](#eventing) ，存取商店的物件。

### 函式(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

將函式與事件解除系結。

##### 參數 {#parameters-off}

* **`name`:** 您 [要解除函式系結的事件名稱](#contexthub-utils-eventing) 。
* **`selector`:** 識別系結的選擇器。 (請參 `selector` 閱和函式 [`on`](#on-name-handler-selector-triggerforpastevents) 的 [`once`](#once-name-handler-selector-triggerforpastevents) 參數)。

##### 退貨 {#returns-off}

此函式不返回值。

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

將函式系結至事件。 每次發生事件時都會呼叫函式。 或者，在建立系結之前，可針對過去發生的事件呼叫函式。

##### 參數 {#parameters-on}

* **`name`:** （字串）您 [要系結函式之事](#contexthub-utils-eventing) 件的名稱。
* **`handler`:** （函式）要綁定到事件的函式。
* **`selector`:** （字串）系結的唯一識別碼。 如果要使用函式來移除系結，則需要選 `off` 取器來識別系結。
* **`triggerForPastEvents`:** （布林值）指出是否應針對過去發生的事件執行處理常式。 呼叫過去事 `true` 件的處理常式的值。 值：調用 `false` 未來事件的處理常式。 預設值為 `true`。

##### 退貨 {#returns-on}

當引 `triggerForPastEvents` 數為 `true`時，此函式會傳回一個值， `boolean` 指出事件是否發生在過去：

* `true`:事件發生在過去，將呼叫處理常式。
* `false`:事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，則此函式不返回值。

##### 範例 {#example-on}

下面的示例將函式綁定到地理位置儲存的資料事件。 函式會在頁面上填入來自商店的緯度資料項目值。

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

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

將函式系結至事件。 對於事件的首次出現，該函式只被調用一次。 或者，在建立系結之前，可針對過去發生的事件呼叫函式。

##### 參數 {#parameters-once}

* **`name`:** （字串）您 [要系結函式之事](#contexthub-utils-eventing) 件的名稱。
* **`handler`:** （函式）要綁定到事件的函式。
* **`selector`:** （字串）系結的唯一識別碼。 如果要使用函式來移除系結，則需要選 `off` 取器來識別系結。
* **`triggerForPastEvents`:** （布林值）指出是否應針對過去發生的事件執行處理常式。 呼叫過去事 `true` 件的處理常式的值。 值：調用 `false` 未來事件的處理常式。 預設值為 `true`。

##### 退貨 {#returns-once}

當引 `triggerForPastEvents` 數為 `true`時，此函式會傳回一個值， `boolean` 指出事件是否發生在過去：

* `true`:事件發生在過去，將呼叫處理常式。
* `false`:事件過去未發生。

如果 `triggerForPastEvents` 是 `false`，則此函式不返回值。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

一種實用程式類，它使對象能夠繼承另一個對象的屬性和方法。

### 函式(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

使對象繼承另一個對象的屬性和方法。

##### 參數 {#parameters-inherit}

* **`child`:** （對象）繼承的對象。
* **`parent`:** （對象）定義繼承的屬性和方法的對象。

## ContextHub.Utils.JSON {#contexthub-utils-json}

提供將物件序列化為JSON格式，以及將JSON字串反序列化為物件的函式。

### 函式(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

將字串值解析為JSON，並將其轉換為javascript物件。

##### 參數 {#parameters-parse}

* **`data`:** JSON格式的字串值。

##### 退貨 {#returns-parse}

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

#### stringify(data) {#stringify-data}

將Javascript值和物件序列化為JSON格式的字串值。

##### 參數 {#parameters-stringify}

* **`data`:** 要序列化的值或對象。 此函式支援布林值、陣列、數字、字串和日期值。

##### 退貨 {#returns-stringify}

序列化字串值。 當 `data` 是R值時，此函 `egExp` 數會傳回空物件。 如果 `data` 是函式，則返回 `undefined`。

##### 範例 {#example-stringify}

下列程式碼：

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

退貨：

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

此類有助於處理要儲存或從ContextHub儲存中檢索的資料對象。

### 函式(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

建立資料對象的副本，並從第二個對象添加資料樹。 該函式返回副本，但不修改任一原始對象。 當兩個對象的資料樹包含相同的鍵時，第二對象的值覆蓋第一對象的值。

##### 參數 {#parameters-addallitems-1}

* **`tree`:** 所複製的對象。
* **`secondTree`:** 與對象副本合併的對 `tree` 像。

##### 退貨 {#returns-addallitems-1}

包含合併資料的對象。

#### cleanup() {#cleanup}

建立對象的副本，查找並刪除資料樹中不含值、空值或未定義值的項，並返回副本。

##### 參數 {#parameters-cleanup}

* **`tree`:** 要清理的物件。

##### 退貨 {#returns-cleanup}

已清理的樹副本。

#### getItem() {#getitem}

從對象中檢索鍵的值。

##### 參數 {#parameters-getitem-2}

* **`tree`:** 資料物件。
* **`key`:** 要檢索的值的鍵。

##### 退貨 {#returns-getitem-2}

與鍵對應的值。 當密鑰具有子密鑰時，此函式返回複雜對象。 當鍵值的類型為時， `undefined`將 `null` 返回。

##### 範例 {#example-getitem-2}

請考慮下列Javascript物件：

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

下列范常式式碼會傳回值 `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

以下示例代碼檢索具有子鍵的鍵的值：

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

函式返回以下對象：

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

從對象的資料樹中檢索所有鍵。 或者，您只能檢索特定鍵子代的鍵。 您也可以選擇指定所擷取索引鍵的排序順序。

##### 參數 {#parameters-getkeys-2}

* **`tree`:** 要從中檢索資料樹鍵的對象。
* **`parent`:** （可選）要檢索子項索引鍵的資料樹中項目的索引鍵。
* **`order`:** （可選）決定傳回索引鍵排序順序的函式。 (請參 [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 閱Mozilla Developer Network。)

##### 退貨 {#returns-getkeys-2}

按鍵陣列。

##### 範例 {#example-getkeys-2}

請考慮下列物件：

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

腳 `ContextHub.Utils.JSON.tree.getKeys(myObject);` 本返回以下陣列：

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

建立給定對象的副本，從資料樹中刪除指定的分支，並返回修改的副本。

##### 參數 {#parameters-removeitem-2}

* **`tree`:** 資料物件。
* **`key`:** 要移除的鍵。

##### 退貨 {#returns-removeitem-2}

已移除索引鍵的原始資料物件的副本。

##### 範例 {#example-removeitem-2}

請考慮下列物件：

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

函式返回以下對象：

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

清理字串值，以便用作索引鍵。 要清理字串，此函式將執行以下操作：

* 將多個連續的正斜線減為單斜線。
* 從字串的開頭和結尾移去空格。
* 將結果分割為一系列以斜線分隔的字串。

使用合成的陣列建立可用密鑰。

##### 參數 {#parameters-sanitizekey}

* **`key`:** 淨化 `string` 環境。

##### 退貨 {#returns-sanitizekey}

一組值 `string` ，其中每個字串是由斜線 `key` 劃分的部分。 代表已淨化的索引鍵。 如果已淨化的陣列長度為零，則此函式會返回 `null`。

##### 範例 {#example-sanitizekey}

下列程式碼會清理字串以產生陣列 `["this", "is", "a", "path"]`，然後從陣列 `"/this/is/a/path"` 產生索引鍵：

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

將鍵／值對添加到對象副本的資料樹中。 有關資料樹的資訊，請參 [閱持久性。](contexthub.md#persistence)

##### 參數 {#parameters-setitem-2}

* **`tree`:** 資料物件。
* **`key`:** 要與要添加的值關聯的鍵。 關鍵字是資料樹中項的路徑。 此函式會呼 `ContextHub.Utils.JSON.tree.sanitize` 叫在新增索引鍵之前先加以淨化。
* **`value`:** 要添加到資料樹中的值。

##### 退貨 {#returns-setitem-2}

包含該對 `tree` 像／對的對 `key`像副 `value` 本。

##### 範例 {#example-setitem-2}

請考慮下列Javascript程式碼：

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

## ContextHub.Utils.storeCandites {#contexthub-utils-storecandidates}

可讓您註冊商店候選人，並取得已註冊的商店候選人。

### 函式(ContextHub.Utils.storeCandites) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCapponitals(storeType) {#getregisteredcandidates-storetype}

傳回已註冊為商店候選者的商店類型。 擷取特定商店類型或所有商店類型的已註冊候選者。

##### 參數 {#parameters-getregisteredcandidates}

* **`storeType`:** （字串）商店類型的名稱。 請參閱 `storeType` 函式的參 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 數。

##### 退貨 {#returns-getregisteredcandidates}

儲存類型的對象。 對象屬性是儲存類型名稱，屬性值是已註冊的儲存候選項的陣列。

#### getStoreFromCapponitals(storeType) {#getstorefromcandidates-storetype}

從已註冊的候選者傳回商店類型。 如果註冊了多個同名的儲存類型，則函式返回優先順序最高的儲存類型。

##### 參數 {#parameters-getstorefromcandidates}

* `storeType`:（字串）商店候選者的名稱。 請參閱 `storeType` 函式的參 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) 數。

##### 退貨 {#returns-getstorefromcandidates}

表示已註冊儲存候選對象的對象。 如果請求的商店類型未註冊，則會擲回錯誤。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

傳回已註冊為商店候選者的商店類型名稱。 此函式不需要參數。

##### 退貨 {#returns-getsupportedstoretypes}

字串值的陣列，其中每個字串是註冊商店候選者的商店類型。 請參閱 `storeType` 函式的參 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) 數。

#### registerStoreCanditade(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

使用名稱和優先順序將儲存對象註冊為儲存候選對象。

優先順序是指出同名商店重要性的數字。 當使用與已註冊的商店候選者相同的名稱註冊商店候選者時，使用優先順序較高的候選者。 在註冊商店候選者時，只有當優先順序高於同名的已註冊商店候選者時，才註冊商店。

##### 參數 {#parameters-registerstorecandidate}

* **`store`:** （對象）要註冊為儲存候選的儲存對象。
* **`storeType`:** （字串）商店候選者的名稱。 建立商店候選項的例項時，需要此值。
* **`priority`:** （數字）商店候選人的優先順序。
* **`applies`:** （函式）用於調用的函式，用於評估儲存在當前環境中的適用性。 如果儲存適 `true` 用，則必須返回函式，否 `false` 則。 預設值是傳回true的函式： `function() {return true;}`

##### 範例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
