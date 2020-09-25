---
title: 設定ContextHub
description: 瞭解如何設定內容中樞。
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 0%

---


# 設定ContextHub {#configuring-contexthub}

ContextHub是儲存、控制和呈現上下文資料的架構。 如需ContextHub的詳細資訊，請參閱 [ContextHub開發人員概觀](contexthub.md)。

您可以設定ContextHub工具列，以控制它是否出現在「預覽」模式中、建立ContextHub儲存區，以及新增UI模組。

## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

設定Adobe Granite ContextHub OSGi服務，在您的頁面上顯示或 [隱藏ContextHub](/help/sites-cloud/authoring/personalization/targeted-content.md) UI。 此服務的PID是 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服務，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) ，或在儲存庫中使用JCR節點：

* **Web控制台：** 若要顯示UI，請選取「顯示UI」屬性。 若要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 若要顯示UI，請將布林屬 `com.adobe.granite.contexthub.show_ui` 性設為 `true`。 若要隱藏UI，請將屬性設為 `false`。

當顯示ContextHub UI時，它只會出現在AEM作者例項的頁面上。 UI不會顯示在發佈例項的頁面上。

## 添加ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

在「預覽」模式下配置ContextHub工具列中顯示的UI模式和模組：

* UI模式：相關模組組
* 模組：可從商店公開內容資料並讓作者控制內容的Widget

UI模式會以一系列圖示的形式出現在工具列的左側。 選取後，UI模式的模組會出現在右側。

![ContextHub工具列](assets/contexthub-toolbar.png)

圖示是 [Coral UI圖示庫的參考](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)。

### 新增UI模式 {#adding-a-ui-mode}

新增UI模式至群組相關的ContextHub模組。 當您建立UI模式時，您會提供顯示在ContextHub工具列中的標題和圖示。

1. 在Experience Manager邊欄上，按一下或點選「工具>網站>內容中樞」。
1. 按一下或點選預設的「設定容器」。
1. 按一下或點選「內容中樞設定」。
1. 按一下或點選「建立」按鈕，然後按一下或點選「內容中樞UI模式」。

   ![新增UI模式](assets/contexthub-ui-mode.png)

1. 提供下列屬性的值：

   * UI模式標題：識別UI模式的標題
   * 模式圖示：例如，要使 [用的Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) (Coral UI)選擇器 `coral-Icon--user`
   * 啟用：選擇以在ContextHub工具列中顯示UI模式

1. 按一下或點選「儲存」。

### 添加UI模組 {#adding-a-ui-module}

將ContextHub UI模組新增至UI模式，以便顯示在ContextHub工具列中，以預覽頁面內容。 當您新增UI模組時，您會建立已在ContextHub中註冊的模組類型例項。 要添加UI模組，您必須知道關聯模組類型的名稱。

AEM提供基本UI模組類型以及數種範例UI模組類型，您可依此類型建立UI模組。 下表提供每個表格的簡要說明。 如需開發自訂UI模組的詳細資訊，請參 [閱建立ContextHub UI模組](extending-contexthub.md#creating-contexthub-ui-module-types)。

UI模組屬性包括詳細配置，您可以在其中為模組特定屬性提供值。 您提供JSON格式的詳細設定。 表格中的「模組類型」欄提供每個UI模組類型所需JSON程式碼的相關資訊連結。

| 模組類型 | 說明 | 存放 |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 通用UI模組類型 | 在UI模組屬性中配置 |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | 顯示瀏覽器的相關資訊 | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | 顯示用戶端的經緯度，以及地圖上的位置。 可讓您變更位置。 | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | 顯示裝置的螢幕方向（橫向或縱向） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | 顯示頁面標籤的統計資料 | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | 顯示當前用戶的配置檔案資訊，包括 `authorizableID`和 `displayName` 和 `familyName`。 您可以更改和的 `displayName` 值 `familyName`。 | `profile` |

1. 在Experience Manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選您要新增UI模組的「設定容器」。
1. 按一下或輸入您要新增UI模組的ContextHub設定。
1. 按一下或點選您要新增UI模組的UI模式。
1. 按一下或點選「建立」按鈕，然後按一下或點選「ContextHub UI Module（一般）」。

   ![ContextHub UI模組](assets/contexthub-ui-module.png)

1. 提供下列屬性的值：

   * UI模組標題：識別UI模組的標題
   * 模組類型：模組類型
   * 啟用：選擇以在ContextHub工具列中顯示UI模組

1. （可選）若要覆寫預設商店設定，請輸入JSON物件以設定UI模組。
1. 按一下或點選「儲存」。

## 建立ContextHub商店 {#creating-a-contexthub-store}

建立內容中樞儲存區，以保存使用者資料並視需要存取資料。 ContextHub儲存區是以註冊的儲存區候選項為基礎。 當您建立商店時，需要註冊商店候選者的storeType值。 (請參 [閱建立自訂商店候選](extending-contexthub.md#creating-custom-store-candidates)。)

### 詳細的商店設定 {#detailed-store-configuration}

在配置儲存時，Detail Configuration屬性允許您為儲存特定屬性提供值。 該值基於儲存 `config` 器函式的參 `init` 數。 因此，是否需要提供此值和值的格式取決於儲存。

「詳細資料設定」屬性的值是JSON格 `config` 式的物件。

### 商店候選人範例 {#sample-store-candidates}

AEM提供下列範例商店候選者，供您建立商店的基礎。

| 商店類型 | 說明 |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | 儲存已解決和未解析的ContextHub區段。 自動從ContextHub SegmentManager中擷取區段 |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [granite.emulator](sample-stores.md#granite-emulators-sample-store-candidate) | 定義多個設備的屬性和功能，並檢測當前客戶端設備 |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | 儲存目前使用者的描述檔資料 |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | 儲存用戶端的相關資訊，例如裝置資訊、瀏覽器類型和視窗方向 |

1. 在Experience Manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選預設設定容器。
1. 按一下或點選「Contexthub Configuration」（內容圖布組態）
1. 若要新增商店，請按一下或點選「建立」圖示，然後按一下或點選「ContextHub商店設定」。

   ![ContextHub儲存區設定](assets/contexthub-store-configuration.png)

1. 提供基本配置屬性的值，然後按一下或點選「下一步」:

   * **配置標題：** 識別商店的標題
   * **商店類型：** 要作為儲存基礎的儲存候選項的storeType屬性的值
   * **必要：** 選擇
   * **啟用：** 選擇以啟用商店

1. （可選）若要覆寫預設的商店設定，請在「詳細設定(JSON)」方塊中輸入JSON物件。
1. 按一下或點選「儲存」。

## 範例：使用JSONP服務  {#example-using-a-jsonp-service}

此範例說明如何設定儲存區並在UI模組中顯示資料。 在此範例中，jsontest.com網站的MD5服務會用作商店的資料來源。 服務會傳回指定字串的MD5雜湊代碼，格式為JSON。

配置contexthub.generic-jsonp儲存器，以便儲存服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`。 服務返回UI模組中顯示的以下資料：

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp儲存 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp範例儲存候選項可讓您從傳回JSON資料的JSONP服務或web service擷取資料。 對於此商店候選項，請使用商店配置來提供要使用的JSONP服務的詳細資訊。

Javascript [類的init](contexthub-api.md#init-name-config) 函式定義一個對 `ContextHub.Store.JSONPStore``config` 像，用於初始化此儲存候選項。 對 `config` 像包含 `service` 包含JSONP服務詳細資訊的對象。 若要設定商店，請以JSON格 `service` 式提供物件作為「詳細資料設定」屬性的值。

要保存jsontest.com站點的MD5服務中的資料，請使用以下屬性 [建立ContextHub儲存](#creating-a-contexthub-store) :

* **配置標題：** md5
* **商店類型：** contexthub.generic-jsonp
* **必要：** 選擇
* **啟用：** 選擇
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

將UI模組新增至ContextHub工具列，以顯示儲存在範例md5商店的資料。 在此範例中，contexthub.base模組用來產生下列UI模組：

![ContextHub MD5商店](assets/contexthub-md5-store.png)

使用「添 [](#adding-a-ui-module) 加UI模組」中的過程將UI模組添加到現有UI模式，如「角色UI模式」示例。 對於UI模組，請使用下列屬性值：

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

## 除錯ContextHub {#debugging-contexthub}

ContextHub的除錯模式可啟用，以允許疑難排解。 除錯模式可以透過ContextHub組態或CRXDE來啟用。

### 透過設定 {#via-the-configuration}

編輯ContextHub的設定並勾選「除錯」選 **項**

1. 在邊欄中按一下或點選「工 **具>網站> ContextHub」**
1. 按一下或點選預設的「設 **定容器」**
1. 選取「 **ContextHub設定」** ，然後按一下或點選「編 **輯選取的元素」**
1. 按一下或點選「 **除錯** 」，然後按一下或點選「儲 **存」**

### 透過CRXDE {#via-crxde}

使用CRXDE Lite將屬性設 `debug` 為 **true** :

* `/conf/global/settings/cloudsettings` 或
* `/conf/<site>/settings/cloudsettings`

### 記錄ContextHub的調試消息 {#logging-debug-messages-for-contexthub}

設定Adobe Granite ContextHub OSGi服務(PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`)，以記錄詳細的除錯訊息，這些訊息在開發時很有用。

要配置服務，您可以使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md) ，或在儲存庫中使用JCR節點：

* Web控制台：要記錄調試消息，請選擇Debug屬性。
* JCR節點：要記錄調試消息，請將布爾 `com.adobe.granite.contexthub.debug` 屬性設定為 `true`。

### 靜默模式 {#silent-mode}

靜默模式會隱藏所有調試資訊。 與一般除錯選項（可針對每個ContextHub配置獨立設定）不同，silent模式是全域設定，取代ContextHub組態層級上的任何除錯設定。

這對您的發佈例項非常有用，因為您完全不需要任何除錯資訊。 因為它是全域設定，所以會透過OSGi啟用。

1. 開啟 **Adobe Experience Manager Web Console設定** : `http://<host>:<port>/system/console/configMgr`
1. 搜尋 **Adobe Granite ContextHub**
1. 按一下 **Adobe Granite ContextHub組態** ，以編輯其屬性
1. 選中「靜默模 **式」選項** ，然後按一下「 **保存」**

## 停用ContextHub {#disabling-contexthub}

ContextHub可停用，以防止它載入js/css並初始化。 要禁用ContextHub，有兩個選項：

* 編輯ContextHub的設定並勾選「停用ContextHub」 **選項**

   1. 在邊欄中按一下或點選「工 **具>網站> ContextHub」**
   1. 按一下或點選預設的「設 **定容器」**
   1. 選取「 **ContextHub設定」** ，然後按一下或點選「編 **輯選取的元素」**
   1. 按一下或點選「 **停用ContextHub」** ，然後按一下或點選「 **儲存」**

或

* 使用CRXDE Lite將屬性設 `disabled` 為 **true** , `/conf/global/settings/cloudsettings/<configName>/contexthub`
