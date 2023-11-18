---
title: 設定 ContextHub
description: 瞭解如何設定Context Hub，此架構用於儲存、操控和呈現內容資料。
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 1%

---

# 設定 ContextHub {#configuring-contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 如需ContextHub的詳細資訊，請參閱 [ContextHub開發人員概觀](contexthub.md).

您可以設定ContextHub工具列來控制它是否出現在預覽模式中、建立ContextHub存放區以及新增UI模組。

## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

設定AdobeGranite ContextHub OSGi服務以顯示或隱藏 [ContextHub UI](/help/sites-cloud/authoring/personalization/targeted-content.md) 在您的頁面上。 此服務的PID為 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

若要設定服務，您可以使用 [網頁主控台](/help/implementing/deploying/configuring-osgi.md) 或使用存放庫中的JCR節點：

* **Web主控台：** 若要顯示UI，請選取「顯示UI」屬性。 若要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 若要顯示UI，請設定布林值 `com.adobe.granite.contexthub.show_ui` 屬性至 `true`. 若要隱藏UI，請將屬性設為 `false`.

顯示ContextHub UI時，它只會顯示在AEM作者執行個體的頁面上。 UI未出現在發佈執行個體的頁面上。

## 新增ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

在「預覽」模式下設定ContextHub工具列中出現的UI模式和模組：

* UI模式：相關模組群組
* 模組：從存放區公開內容資料並允許作者操控內容的Widget

UI模式會在工具列左側顯示為一系列圖示。 選取後，UI模式的模組會顯示在右側。

![contexthub工具列](assets/contexthub-toolbar.png)

圖示是來自的參照 [Coral UI圖示程式庫](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### 新增UI模式 {#adding-a-ui-mode}

新增UI模式至群組相關的ContextHub模組。 建立UI模式時，您會提供顯示在ContextHub工具列中的標題和圖示。

1. 在Experience Manager邊欄中，選取「工具>網站>內容中心」。
1. 選取預設的「組態容器」。
1. 選取Context Hub組態。
1. 選取「建立」按鈕，然後選取「Context Hub UI模式」。

   ![新增UI模式](assets/contexthub-ui-mode.png)

1. 提供下列屬性的值：

   * UI模式標題：識別UI模式的標題
   * 模式圖示：的選取器 [Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 以使用 `coral-Icon--user`
   * 啟用：選取此選項可在ContextHub工具列中顯示UI模式

1. 選取儲存。

### 新增使用者介面模組 {#adding-a-ui-module}

將ContextHub UI模組新增至UI模式，使其顯示在ContextHub工具列中以預覽頁面內容。 新增UI模組時，您會建立已向ContextHub註冊的模組型別例項。 若要新增UI模組，您必須知道關聯模組型別的名稱。

AEM提供基礎UI模組型別以及數個範例UI模組型別，您可以依據這些型別建立UI模組。 下表提供每個專案的簡短說明。 如需有關開發自訂UI模組的資訊，請參閱 [建立ContextHub UI模組](extending-contexthub.md#creating-contexthub-ui-module-types).

UI模組屬性包含詳細設定，您可以在其中提供模組特定屬性的值。 您可以提供JSON格式的詳細資料設定。 表格中的模組型別欄提供每個UI模組型別所需JSON程式碼相關資訊的連結。

| 模組型別 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 通用UI模組型別 | 在UI模組屬性中設定 |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | 顯示瀏覽器的相關資訊 | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | 顯示使用者端的經緯度，以及地圖上的位置。 可讓您變更位置。 | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | 顯示裝置的熒幕方向（橫向或縱向） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | 顯示頁面標籤的相關統計資料 | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | 顯示目前使用者的設定檔資訊，包括 `authorizableID`， `displayName` 和 `familyName`. 您可以變更以下專案的值： `displayName` 和 `familyName`. | `profile` |

1. 在Experience Manager邊欄中，選取「工具>網站> ContextHub」。
1. 選取要新增UI模組的設定容器。
1. 按一下或輸入您要新增UI模組的ContextHub組態。
1. 選取要新增UI模組的UI模式。
1. 選取「建立」按鈕，然後選取「ContextHub UI模組（一般）」。

   ![contexthub UI模組](assets/contexthub-ui-module.png)

1. 提供下列屬性的值：

   * UI模組標題：識別UI模組的標題
   * 模組型別：模組型別
   * 啟用：選取以在ContextHub工具列中顯示UI模組

1. （選用）若要覆寫預設存放區設定，請輸入JSON物件以設定UI模組。
1. 選取儲存。

## 建立ContextHub存放區 {#creating-a-contexthub-store}

建立Context Hub存放區以儲存使用者資料，並視需要存取資料。 ContextHub存放區是以已註冊的存放區候選專案為基礎。 當您建立存放區時，您需要存放區候選專案註冊所在的storeType值。 (請參閱 [建立自訂商店候選者](extending-contexthub.md#creating-custom-store-candidates).)

### 詳細存放區設定 {#detailed-store-configuration}

當您設定存放區時，Detail Configuration屬性可讓您提供存放區特定屬性的值。 此值以下列專案為基礎 `config` 商店的引數 `init` 函式。 因此，您是否需提供此值，以及值的格式取決於存放區。

「詳細資料組態」屬性的值為 `config` json格式的物件。

### 範例商店候選者 {#sample-store-candidates}

AEM提供下列範例商店候選者，您可以據以建立商店。

| 存放區型別 | 說明 |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | 儲存已解析和未解析的ContextHub區段。 自動從ContextHub SegmentManager擷取區段 |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | 定義數個裝置的屬性和功能，並偵測目前的使用者端裝置 |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | 儲存目前使用者的設定檔資料 |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | 儲存使用者端的相關資訊，例如裝置資訊、瀏覽器型別和視窗方向 |

1. 在Experience Manager邊欄中，選取「工具>網站> ContextHub」。
1. 選取預設設定容器。
1. 選取Contexthub設定
1. 若要新增存放區，請選取「建立」圖示，然後選取「ContextHub存放區設定」。

   ![ContextHub存放區設定](assets/contexthub-store-configuration.png)

1. 提供基本組態屬性的值，然後選取[下一步]：

   * **設定標題：** 識別存放區的標題
   * **存放區型別：** 作為存放區基礎之存放區候選專案的storeType屬性值
   * **必填：** 選取
   * **已啟用：** 選取以啟用存放區

1. （選用）若要覆寫預設存放區設定，請在「詳細資料設定(JSON)」方塊中輸入JSON物件。
1. 選取儲存。

## 範例：使用JSONP服務  {#example-using-a-jsonp-service}

此範例說明如何設定存放區並在UI模組中顯示資料。 在此範例中，jsontest.com網站的MD5服務會作為存放區的資料來源。 此服務會傳回指定字串的MD5雜湊代碼，格式為JSON。

contexthub.generic-jsonp存放區已設定為儲存服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. 此服務會傳回以下資料，這些資料會顯示在UI模組中：

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp存放區 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp範例存放區候選專案可讓您從JSONP服務或傳回JSON資料的Web服務擷取資料。 對於此存放區候選專案，請使用存放區設定來提供有關要使用的JSONP服務的詳細資訊。

此 [init](contexthub-api.md#init-name-config) 的功能 `ContextHub.Store.JSONPStore` JavaScript類別定義 `config` 初始化此存放區候選的物件。 此 `config` 物件包含 `service` 物件，其中包含有關JSONP服務的詳細資訊。 若要設定商店，您需提供 `service` JSON格式的物件，作為詳細資料設定的屬性值。

若要儲存jsontest.com網站MD5服務的資料，請使用下列程式 [建立ContextHub存放區](#creating-a-contexthub-store) 使用下列屬性：

* **設定標題：** md5
* **存放區型別：** contexthub.generic-jsonp
* **必填：** 選取
* **已啟用：** 選取
* **詳細資料組態 (JSON):**

  ```javascript
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### 新增md5資料的UI模組 {#adding-a-ui-module-for-the-md-data}

將UI模組新增至ContextHub工具列，以顯示儲存在範例md5存放區中的資料。 在此範例中，contexthub.base模組用於產生下列UI模組：

![ContextHub MD5存放區](assets/contexthub-md5-store.png)

請遵循下列步驟： [新增使用者介面模組](#adding-a-ui-module) 將UI模組新增至現有UI模式，例如範例Persona UI模式。 對於UI模組，請使用以下屬性值：

* **UI模組標題：** MD5
* **模組型別：** contexthub.base
* **詳細資料組態 (JSON):**

  ```javascript
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Conversion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## 偵錯ContextHub {#debugging-contexthub}

可以啟用ContextHub的偵錯模式，以進行疑難排解。 偵錯模式可以透過ContextHub設定或透過CRXDE啟用。

### 透過設定 {#via-the-configuration}

編輯ContextHub的設定並核取選項 **偵錯**

1. 在邊欄中選取 **「工具」>「網站」>「ContextHub」**
1. 選取預設值 **設定容器**
1. 選取 **ContextHub設定** 並選取 **編輯選取的元素**
1. 選取 **偵錯** 並選取 **儲存**

### 透過CRXDE {#via-crxde}

使用CRXDE Lite設定屬性 `debug` 至 **true** 在：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<site>/settings/cloudsettings`

### 記錄ContextHub的偵錯訊息 {#logging-debug-messages-for-contexthub}

設定AdobeGranite ContextHub OSGi服務(PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`)以記錄詳細的偵錯訊息，這些訊息在開發時相當實用。

若要設定服務，您可以使用 [網頁主控台](/help/implementing/deploying/configuring-osgi.md) 或使用存放庫中的JCR節點：

* Web主控台：若要記錄「除錯」訊息，請選取「除錯」屬性。
* JCR節點：若要記錄偵錯訊息，請設定布林值 `com.adobe.granite.contexthub.debug` 屬性至 `true`.

### 無訊息模式 {#silent-mode}

無訊息模式會隱藏所有偵錯資訊。 與一般偵錯選項不同（可針對每個ContextHub組態個別設定），無訊息模式是全域設定，其優先於ContextHub組態層級上的任何偵錯設定。

這對於您根本不想要任何偵錯資訊的發佈執行個體非常有用。 由於這是全域設定，因此會透過OSGi啟用。

1. 開啟 **Adobe Experience Manager Web主控台設定** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜尋 **AdobeGranite ContextHub**
1. 按一下設定 **AdobeGranite ContextHub** 以編輯其屬性
1. 核取選項 **無訊息模式** 並按一下 **儲存**

## 正在停用ContextHub {#disabling-contexthub}

可以停用ContextHub以防止其載入js/css和初始化。 有兩個選項可停用ContextHub：

* 編輯ContextHub的設定並核取選項 **停用ContextHub**

   1. 在邊欄中選取 **「工具」>「網站」>「ContextHub」**
   1. 選取預設值 **設定容器**
   1. 選取 **ContextHub設定** 並選取 **編輯選取的元素**
   1. 選取 **停用ContextHub** 並選取 **儲存**

或

* 使用CRXDE Lite設定屬性 `disabled` 至 **true** 在 `/conf/global/settings/cloudsettings/<configName>/contexthub`
