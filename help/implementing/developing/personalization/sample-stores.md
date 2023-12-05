---
title: ContextHub存放區候選範例
description: ContextHub提供數個您可在解決方案中使用的候選範例商店
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# ContextHub存放區候選範例 {#sample-contexthub-store-candidates}

ContextHub提供數個您可在解決方案中使用的候選範例商店。 每個範例都會提供下列資訊：

* 在何處尋找原始程式碼，以方便您開啟它以供學習。
* 如何設定您從候選商店建立的商店。
* 如何建構存放區資料以方便您存取。

>[!WARNING]
>
>範例存放區候選專案作為參考設定提供，以幫助您為專案建立自己的專用設定。 請勿直接使用，

## aem.segmentation範例存放區候選專案 {#aem-segmentation-sample-store-candidate}

儲存已解析和未解析的ContextHub區段。 自動從ContextHub SegmentManager擷取區段。

### 來源位置 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 基礎實作 {#base-implementation-segmentation}

aem.segmentation存放區候選擴充 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 設定 {#configuration-segmentation}

當您建立 `aem.segmentation` 儲存，您不需要提供詳細設定。 預設設定會指定ContextHub區段定義的位置。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation範例存放區候選專案 {#contexthub-geolocation-sample-store-candidate}

此 `contexthub.geolocation` 範例存放區候選專案使用Google地圖來取得並儲存有關使用者端位置的資訊。

### 來源位置 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 基礎實作 {#base-implementation-geolocation}

此 `contexthub.geolocation` 存放區候選延伸 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 設定 {#configuration-geolocation}

預設設定會指定有關Google服務以及初始經緯度座標的資訊。

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

### 資料專案 {#data-items-geolocation}

存放區會使用與下列範例類似的資料樹狀結構：

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x中推出的安全性原則要求所有與地理位置相關的呼叫都必須透過安全連線進行。 因此，如果AEM也透過https執行，AEM會強制使用https進行地理位置API呼叫。 否則，會使用http來遵守相同來源的原則。
>
>另請參閱 [此Google部落格](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) 以取得有關Chrome中變更的詳細資訊。

## contexthub.surferinfo範例存放區候選專案 {#contexthub-surferinfo-sample-store-candidate}

儲存有關目前使用者端環境的資訊，例如裝置、視窗、瀏覽器、日期和時間。

### 來源位置 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 基礎實作 {#base-implementation-surferinfo}

此 `contexthub.surferinfo` 存放區候選延伸 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### 設定 {#configuration-surferinfo}

預設設定繼承自 `ContextHub.Store.PersistedStore`.

### 資料專案 {#data-items-surferinfo}

使用此候選存放區的存放區具有類似於以下範例的資料樹狀結構：

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

## granite.emulators範例存放區候選專案 {#granite-emulators-sample-store-candidate}

此 `granite.emulators` 範例存放區候選專案會儲存使用者端裝置的相關資訊。

### 來源位置 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 基礎實作 {#base-implementation-emulators}

此 `granite.emulators` 存放區候選延伸 [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### 設定 {#configuration-emulators}

預設設定包含一個名為的陣列 `defaultEmulators` 包含不同裝置的相關資訊。 建立存放區時，請視需要在「詳細資料組態」屬性中提供不同的裝置設定檔，格式如下例所示：

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

### 資料專案 {#data-items-emulators}

存放區資料樹狀結構類似於以下範例：

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

## granite.profile範例存放區候選專案 {#granite-profile-sample-store-candidate}

儲存目前使用者的相關資訊。

### 來源位置 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 基礎實作 {#base-implementation-profile}

此 `granite.profile` 存放區候選延伸 [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### 設定 {#configuration-profile}

系統會使用下列預設設定。 您不應變更此設定。

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

### 資料專案 {#data-items-profile}

使用此候選存放區的存放區具有類似於以下範例的資料樹狀結構：

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
