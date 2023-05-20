---
title: 示例ContextHub儲存候選
description: ContextHub提供了幾個示例儲存候選，您可以在解決方案中使用
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# 示例ContextHub儲存候選 {#sample-contexthub-store-candidates}

ContextHub提供了幾個示例儲存候選，您可以在解決方案中使用。 為每個示例提供以下資訊：

* 在何處查找原始碼，以便您可以開啟它以用於學習目的。
* 如何配置從候選儲存庫建立的儲存庫。
* 儲存資料的結構，以便您能夠訪問它。

>[!WARNING]
>
>示例儲存候選作為參考配置提供，以幫助您為項目構建自己的專用配置，因此不應直接使用。

## aem.分段樣本儲存候選 {#aem-segmentation-sample-store-candidate}

儲存已解析和未解析的ContextHub段。 自動從ContextHub SegmentManager中檢索段。

### 源位置 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基本實施 {#base-implementation-segmentation}

aem.segmentation儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-segmentation}

建立 `aem.segmentation` 儲存，您不需要提供詳細的配置。 預設配置指定ContextHub段定義的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation示例儲存候選 {#contexthub-geolocation-sample-store-candidate}

的 `contexthub.geolocation` 樣例儲存候選項使用Google地圖獲取和儲存有關客戶端位置的資訊。

### 源位置 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基本實施 {#base-implementation-geolocation}

的 `contexthub.geolocation` 儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-geolocation}

預設配置指定有關Google服務以及初始經緯度坐標的資訊。

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### 資料項 {#data-items-geolocation}

儲存使用與以下示例類似的資料樹：

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中引入的安全策略要求所有與地理位置相關的呼叫都通過安全連接進行。 因此，AEM如果在https上運行，則強AEM制對地理位置API調用使用https。 否則，使用http來符合同一源的策略。
>
>請參閱 [Google部落格](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) 的子菜單。

## contexthub.surferinfo示例儲存候選 {#contexthub-surferinfo-sample-store-candidate}

儲存有關當前客戶端環境的資訊，如設備、窗口、瀏覽器、日期和時間。

### 源位置 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基本實施 {#base-implementation-surferinfo}

的 `contexthub.surferinfo` 儲存候選擴展 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-surferinfo}

預設配置繼承自 `ContextHub.Store.PersistedStore`。

### 資料項 {#data-items-surferinfo}

使用此儲存候選的儲存具有與以下示例類似的資料樹：

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators樣本儲存候選 {#granite-emulators-sample-store-candidate}

的 `granite.emulators` 示例儲存候選項儲存有關客戶端設備的資訊。

### 源位置 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基本實施 {#base-implementation-emulators}

的 `granite.emulators` 儲存候選擴展 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)。

### 設定 {#configuration-emulators}

預設配置包括名為 `defaultEmulators` 包含有關不同設備的資訊。 建立儲存時，請根據需要在「詳細配置」屬性中提供不同的設備配置檔案，格式如下例所示：

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### 資料項 {#data-items-emulators}

儲存資料樹與以下示例類似：

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile樣例儲存候選 {#granite-profile-sample-store-candidate}

儲存有關當前用戶的資訊。

### 源位置 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基本實施 {#base-implementation-profile}

的 `granite.profile` 儲存候選擴展 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)。

### 設定 {#configuration-profile}

使用以下預設配置。 您不應更改此配置。

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### 資料項 {#data-items-profile}

使用此儲存候選的儲存具有與以下示例類似的資料樹：

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
