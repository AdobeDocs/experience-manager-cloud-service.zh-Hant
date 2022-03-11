---
title: 配置ContextHub
description: 瞭解如何配置上下文中心。
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 0%

---

# 配置ContextHub {#configuring-contexthub}

ContextHub是用於儲存、操作和呈現上下文資料的框架。 有關ContextHub的詳細資訊，請參閱 [ContextHub開發人員概述](contexthub.md)。

您可以配置ContextHub工具欄以控制它是否出現在「預覽」模式、建立ContextHub儲存以及添加UI模組。

## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

配置AdobeGranite ContextHub OSGi服務以顯示或隱藏 [上下文集線器UI](/help/sites-cloud/authoring/personalization/targeted-content.md) 在你的網頁上。 此服務的PID為 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服務，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) 或在儲存庫中使用JCR節點：

* **Web控制台：** 要顯示UI，請選擇「顯示UI」屬性。 要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 要顯示UI，請設定布爾值 `com.adobe.granite.contexthub.show_ui` 屬性 `true`。 要隱藏UI，請將屬性設定為 `false`。

當顯示ContextHub UI時，它只出現在作者實例AEM的頁面上。 UI不出現在發佈實例的頁面上。

## 添加ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

在預覽模式下配置ContextHub工具欄中顯示的UI模式和模組：

* UI模式：相關模組組
* 模組：用於從儲存中公開上下文資料並使作者能夠處理上下文的小部件

UI模式在工具欄左側顯示為一系列表徵圖。 選中後，UI模式的模組將顯示在右側。

![ContextHub工具欄](assets/contexthub-toolbar.png)

表徵圖是 [Coral UI表徵圖庫](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 添加UI模式 {#adding-a-ui-mode}

將UI模式添加到與ContextHub模組相關的組。 建立UI模式時，將提供顯示在ContextHub工具欄中的標題和表徵圖。

1. 在Experience Manager導軌上，按一下或點擊「工具」>「站點」>「上下文集線器」。
1. 按一下或點擊預設配置容器。
1. 按一下或點擊「Context Hub Configuration（上下文集線器配置）」。
1. 按一下或點擊「Create（建立）」按鈕，然後按一下或點擊「Context Hub UI Mode（上下文中心UI模式）」。

   ![添加UI模式](assets/contexthub-ui-mode.png)

1. 為以下屬性提供值：

   * UI模式標題：標識UI模式的標題
   * 模式表徵圖：選擇器 [Coral UI表徵圖](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 例如 `coral-Icon--user`
   * 已啟用：選擇以在ContextHub工具欄中顯示UI模式

1. 按一下或點擊「保存」。

### 添加UI模組 {#adding-a-ui-module}

將ContextHub UI模組添加到UI模式，以便它顯示在用於預覽頁面內容的ContextHub工具欄中。 添加UI模組時，將建立在ContextHub中註冊的模組類型實例。 要添加UI模組，必須知道關聯模組類型的名稱。

提AEM供基本UI模組類型以及幾種示例UI模組類型，您可以在這些類型上基於UI模組。 下表對每個選項提供了簡要說明。 有關開發自定義UI模組的資訊，請參見 [建立ContextHub UI模組](extending-contexthub.md#creating-contexthub-ui-module-types)。

UI模組屬性包括詳細配置，您可以在其中為模組特定的屬性提供值。 您以JSON格式提供詳細配置。 表中的「模組類型」列提供了指向每個UI模組類型所需JSON代碼資訊的連結。

| 模組類型 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 通用UI模組類型 | 在UI模組屬性中配置 |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | 顯示有關瀏覽器的資訊 | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | `datetime` |
| [contexthub.位置](sample-modules.md#contexthub-location-ui-module-type) | 顯示客戶端的經緯度以及地圖上的位置。 允許您更改位置。 | `geolocation` |
| [contexthub.screen orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | 顯示設備的螢幕方向（橫向或縱向） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | 顯示有關頁標籤的統計資訊 | `tagcloud` |
| [花崗岩/輪廓](sample-modules.md#granite-profile-ui-module-type) | 顯示當前用戶的配置檔案資訊，包括 `authorizableID`。 `displayName` 和 `familyName`。 您可以更改 `displayName` 和 `familyName`。 | `profile` |

1. 在Experience Manager欄上，按一下或按一下「工具」>「站點」>「上下文集線」。
1. 按一下或點擊要添加UI模組的配置容器。
1. 按一下或鍵入要添加UI模組的ContextHub配置。
1. 按一下或點擊要添加UI模組的UI模式。
1. 按一下或點擊「Create（建立）」按鈕，然後按一下或點擊「ContextHub UI Module（一般）」。

   ![ContextHub UI模組](assets/contexthub-ui-module.png)

1. 為以下屬性提供值：

   * UI模組標題：標識UI模組的標題
   * 模組類型：模組類型
   * 已啟用：選擇以在ContextHub工具欄中顯示UI模組

1. （可選）要覆蓋預設儲存配置，請輸入JSON對象以配置UI模組。
1. 按一下或點擊「保存」。

## 建立ContextHub儲存 {#creating-a-contexthub-store}

建立上下文中心儲存以保留用戶資料並根據需要訪問資料。 ContextHub儲存基於註冊的儲存候選。 建立儲存區時，需要註冊儲存區候選區的storeType值。 (請參閱 [建立自定義儲存候選](extending-contexthub.md#creating-custom-store-candidates)。)

### 詳細儲存配置 {#detailed-store-configuration}

配置儲存時，「詳細資訊配置」屬性允許您提供特定於儲存的屬性的值。 該值基於 `config` 儲存的參數 `init` 的子菜單。 因此，是否需要提供此值和值的格式取決於儲存。

Detail Configuration屬性的值是 `config` JSON格式的對象。

### 樣例儲存候選 {#sample-store-candidates}

提AEM供以下樣例儲存候選項，您可以在其上建立儲存。

| 儲存類型 | 說明 |
|---|---|
| [aem分割](sample-stores.md#aem-segmentation-sample-store-candidate) | 儲存已解析和未解析的ContextHub段。 自動從ContextHub SegmentManager檢索段 |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [花崗岩。模擬器](sample-stores.md#granite-emulators-sample-store-candidate) | 定義多個設備的屬性和功能，並檢測當前客戶端設備 |
| [花崗岩/輪廓](sample-stores.md#granite-profile-sample-store-candidate) | 儲存當前用戶的配置檔案資料 |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | 儲存有關客戶端的資訊，如設備資訊、瀏覽器類型和窗口方向 |

1. 在Experience Manager欄上，按一下或按一下「工具」>「站點」>「上下文集線」。
1. 按一下或點擊預設配置容器。
1. 按一下或點擊「Contexthub Configuration（上下文配置）」
1. 要添加儲存，請按一下或點擊「建立」表徵圖，然後按一下或點擊「上下文集線器儲存配置」。

   ![ContextHub儲存配置](assets/contexthub-store-configuration.png)

1. 提供基本配置屬性的值，然後按一下或點擊「下一步」：

   * **配置標題：** 標識儲存的標題
   * **儲存類型：** 要作為儲存基礎的儲存候選的storeType屬性的值
   * **必需：** 選擇
   * **已啟用：** 選擇以啟用儲存

1. （可選）要覆蓋預設儲存配置，請在「詳細配置(JSON)」框中輸入JSON對象。
1. 按一下或點擊「保存」。

## 示例：使用JSONP服務  {#example-using-a-jsonp-service}

此示例說明如何配置儲存並在UI模組中顯示資料。 在本示例中，jsontest.com站點的MD5服務用作儲存的資料源。 服務以JSON格式返回給定字串的MD5哈希代碼。

配置contexthub.generic-jsonp儲存，以便它儲存用於服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服務返回UI模組中顯示的以下資料：

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp儲存 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp示例儲存候選項使您能夠從返回JSON資料的JSONP服務或Web服務中檢索資料。 對於此儲存候選，請使用儲存配置來提供有關要使用的JSONP服務的詳細資訊。

的 [初始化](contexthub-api.md#init-name-config) 函式 `ContextHub.Store.JSONPStore` Javascript類定義 `config` 初始化此儲存候選項的對象。 的 `config` 對象包含 `service` 包含有關JSONP服務的詳細資訊的對象。 要配置儲存，請提供 `service` JSON格式的對象，作為Detail Configuration屬性的值。

要保存jsontest.com站點的MD5服務中的資料，請使用中的過程 [建立ContextHub儲存](#creating-a-contexthub-store) 使用以下屬性：

* **配置標題：** md5
* **儲存類型：** contexthub.generic.jsonp
* **必需：** 選擇
* **已啟用：** 選擇
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

### 為md5資料添加UI模組 {#adding-a-ui-module-for-the-md-data}

將UI模組添加到ContextHub工具欄，以顯示儲存在示例md5儲存中的資料。 在本示例中，contexthub.base模組用於生成以下UI模組：

![ContextHub MD5儲存](assets/contexthub-md5-store.png)

使用中的過程 [添加UI模組](#adding-a-ui-module) 將UI模組添加到現有UI模式，如「Persona UI模式」示例。 對於UI模組，請使用以下屬性值：

* **UI模組標題：** MD5
* **模組類型：** contexthub.base
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

## 調試ContextHub {#debugging-contexthub}

可以啟用ContextHub的調試模式，以允許進行故障排除。 可以通過ContextHub配置或通過CRXDE啟用調試模式。

### 通過配置 {#via-the-configuration}

編輯ContextHub的配置並檢查選項 **調試**

1. 在滑軌中按一下或點擊 **「工具」>「站點」>「上下文中心」**
1. 按一下或點擊預設 **配置容器**
1. 選擇 **ContextHub配置** 點擊 **編輯選定元素**
1. 按一下或點擊 **調試** 點擊 **保存**

### 通過CRXDE {#via-crxde}

使用CRXDE Lite設定屬性 `debug` 至 **真** 下：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<site>/settings/cloudsettings`

### 記錄ContextHub的調試消息 {#logging-debug-messages-for-contexthub}

配置AdobeGranite ContextHub OSGi服務(PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`)記錄詳細的調試消息，這些消息在開發時非常有用。

要配置服務，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) 或在儲存庫中使用JCR節點：

* Web控制台：要記錄調試消息，請選擇「調試」屬性。
* JCR節點：要記錄調試消息，請設定布爾值 `com.adobe.granite.contexthub.debug` 屬性 `true`。

### 靜默模式 {#silent-mode}

靜默模式會隱藏所有調試資訊。 與普通調試選項不同，靜默模式是全局設定，它取代了ContextHub配置級別上的任何調試設定。

這對您的發佈實例非常有用，因為您根本不需要任何調試資訊。 因為它是全局設定，所以通過OSGi啟用它。

1. 開啟 **Adobe Experience ManagerWeb控制台配置** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **Adobe花崗岩上下文樞紐**
1. 按一下配置 **Adobe花崗岩上下文樞紐** 編輯其屬性
1. 選中選項 **靜默模式** 按一下 **保存**

## 禁用ContextHub {#disabling-contexthub}

可以禁用ContextHub，以阻止它載入js/css和初始化。 禁用ContextHub有兩種選項：

* 編輯ContextHub的配置並檢查選項 **禁用ContextHub**

   1. 在滑軌中按一下或點擊 **「工具」>「站點」>「上下文中心」**
   1. 按一下或點擊預設 **配置容器**
   1. 選擇 **ContextHub配置** 點擊 **編輯選定元素**
   1. 按一下或點擊 **禁用ContextHub** 點擊 **保存**

或

* 使用CRXDE Lite設定屬性 `disabled` 至 **真** 在 `/conf/global/settings/cloudsettings/<configName>/contexthub`
