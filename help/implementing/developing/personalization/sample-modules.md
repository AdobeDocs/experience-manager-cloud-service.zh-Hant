---
title: ContextHub UI模組型別範例
description: ContextHub提供數個範例UI模組，供您在解決方案中使用
exl-id: 31ff4444-8d96-4817-9676-ea5ad36dcda5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# ContextHub UI模組型別範例 {#sample-contexthub-ui-module-types}

ContextHub提供數個範例UI模組，供您在解決方案中使用。 下列資訊已提供：

* UI模組的主要功能。
* 在何處尋找原始程式碼，以方便您開啟它以供學習。
* 如何設定UI模組。

如需有關將UI模組新增至ContextHub的資訊，請參閱 [新增使用者介面模組](configuring-contexthub.md#adding-a-ui-module). 如需有關開發UI模組的資訊，請參閱 [建立ContextHub UI模組型別](extending-contexthub.md#creating-contexthub-ui-module-types).

## contexthub.base UI模組型別 {#contexthub-base-ui-module-type}

contexthub.base UI模組型別是其他所有UI模組型別的基底型別。 因此，它為呈現存放區資料提供了一般功能。

下列功能可供使用：

* **標題和圖示：** 指定UI模組的標題和圖示。 可使用URL或從Coral UI圖示資料庫參照圖示。
* **儲存資料：** 識別一或多個要擷取資料的存放區。
* **內容：** 指定UI模組在ContextHub工具列中顯示的內容。
* **彈出視窗內容：** 指定點選或點選UI模組時彈出視窗中顯示的內容。
* **全熒幕模式：** 控制是否允許全熒幕模式。

原始碼位於 `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.

### 設定 {#configuration}

使用JSON格式的JavaScript物件來設定contexthub.base UI模組。 納入以下任何屬性以設定UI模組功能：

* **影像：** 要顯示為圖示之影像的URL。
* **圖示：** 的名稱 [Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 類別。 如果您同時指定圖示和影像屬性的值，則會使用影像。
* **標題：** UI模組的標題。 當指標暫停在UI模組圖示上方時，標題就會顯示。
* **全熒幕：** 布林值，指出UI模組是否支援全熒幕模式。 使用 `true` 以支援全熒幕和 `false` 以防止全熒幕模式。
* **範本：** A [Handlebars](https://handlebarsjs.com/) 指定要在ContextHub工具列中轉譯之內容的範本。 最多使用兩個 `<p>` 標籤之間。
* **storeMapping：** 金鑰/存放區對應。 使用把手範本中的索引鍵來存取相關聯的ContextHub存放區資料。
* **清單：** 按一下UI模組時顯示在彈出視窗中的專案陣列。 如果您包含此專案，請勿包含poverTemplate。 值是一個物件陣列，內含下列索引鍵：
   * title：為此專案顯示的文字
   * 影像： （選用）應在左側顯示的影像URL
   * 圖示： （選用）應在左側顯示的CUI圖示類別；如果已指定影像，則會忽略此類別
   * selected： （選用）布林值，指定此專案是否應顯示為selected (true=selected)。 依預設，選取的專案會以粗體字型顯示。 使用 `listType` 屬性來設定其他外觀（請參閱下文）。
* **listType：** 用於彈出視窗清單專案的樣式。 使用下列其中一個值：
   * 核取記號
   * 核取方塊
   * 無線電
* **popoverTemplate：** Handlebars範本，指定在按一下UI模組時，於彈出視窗中轉譯的內容。 如果您包含此專案，請勿包含 `list` 個專案。

### 範例 {#example}

以下範例會設定c`ontexthub.base` 用於從顯示資訊的UI模組 [contexthub.emulators](sample-stores.md#granite-emulators-sample-store-candidate) 商店。 此 `template` 專案會示範如何使用下列鍵從存放區取得資料 `storeMapping` 專案建立。

```javascript
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![contexthub.base模組](assets/base-module.png)

## contexthub.browserinfo UI模組型別 {#contexthub-browserinfo-ui-module-type}

此 `contexthub.browserinfo` UI模組會顯示使用者端Web瀏覽器和作業系統的相關資訊。 資訊取自surferinfo商店，依據為 [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) 商店候選者。

![contexthub.browserinfo模組](assets/browserinfo-module.png)

UI模組的原始碼位於 `/libs/granite/contexthub/components/modules/browserinfo`. 雖然 `contexthub.browserinfo` 擴充 `contexthub.base` UI模組，則不會覆寫或提供其他功能。 實作提供呈現瀏覽器資訊的預設設定。

### 設定 {#configuration-1}

contexthub.browserinfo UI模組的執行個體不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。

```javascript
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## contexthub.datetime UI模組型別 {#contexthub-datetime-ui-module-type}

此 `contexthub.datetime` UI模組顯示儲存在名為datetime的存放區中的日期和時間，該存放區是根據 `contexthub.datetime` 商店候選者。

![contexthub.datetime模組](assets/datetime-module.png)

此模組提供彈出表單，可讓您變更商店中的日期和時間。

的來源 `contexthub.datetime` UI模組位於 `/libs/granite/contexthub/components/modules/datetime`.

### 設定 {#configuration-2}

contexthub.datetime UI模組的例項不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。

```javascript
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## contexthub.location UI模組型別 {#contexthub-location-ui-module-type}

此 `contexthub.location` UI模組會顯示使用者端的經度和緯度。 此模組會提供一個彈出視窗，其中顯示Google地圖，您可以按一下該視窗來變更目前位置。 模組會從名為geolocation的ContextHub存放區取得資訊，該存放區是根據 [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) 商店候選者。

![contexthub.location模組](assets/location-module.png)

UI模組的來源位於 `/etc/cloudsettings/default/contexthub/geolocation`.

### 設定 {#configuration-4}

contexthub.location UI模組的例項不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。

```javascript
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI模組型別 {#contexthub-screen-orientation-ui-module-type}

此 `contexthub.screen-orientation` UI模組顯示使用者端目前的畫面方向。 雖然預設為停用，但模組會提供一個彈出視窗，讓您選取方向。 此模組會從名為模擬器的ContextHub存放區取得資訊，該模擬器是根據 [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) 商店候選者。

![contexthub.screen-orientation模組](assets/screen-orientation-module.png)

UI模組的來源位於 `/libs/granite/contexthub/components/modules/screen-orientation`.

### 設定 {#configuration-5}

的例項 `contexthub.screen-orientation` UI模組不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。 此 `clickable` 屬性為 `false` 依預設。 如果您覆寫要設定的預設設定 `clickable` 至 `true`，按一下模組會顯示快顯視窗，讓您選取方向。

```javascript
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud UI模組型別 {#contexthub-tagcloud-ui-module-type}

此 `contexthub.tagcloud` UI模組會顯示標籤的相關資訊。 在工具列上，UI模組顯示標籤數量。 快顯視窗會顯示Tagcloud和用於新增標籤的文字方塊。 UI模組會從名為tagcloud的ContextHub存放區取得資訊，該存放區是根據 `contexthub.tagcloud` 商店候選者。

![contexthub.tagcloud模組](assets/tagcloud-module.png)

UI模組的來源位於 `/libs/granite/contexthub/components/modules/tagcloud`.

### 設定 {#configuration-6}

的例項 `contexthub.tagcloud` UI模組不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。

```javascript
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI模組型別 {#granite-profile-ui-module-type}

此 `granite.profile` ContextHub UI模組會顯示目前使用者的顯示名稱。 快顯視窗會顯示使用者的登入名稱，並可讓您變更顯示名稱的值。 UI模組會從名為profile的ContextHub存放區取得資訊，該存放區是根據 [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) 商店候選者。

![granite.profile模組](assets/profile-module.png)

UI模組的來源為 `/libs/granite/contexthub/components/modules/profile`.

### 設定 {#configuration-7}

的例項 `granite.profile` UI模組不需要詳細資料設定的值。 以下JSON文字代表模組的預設設定。

```javascript
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
