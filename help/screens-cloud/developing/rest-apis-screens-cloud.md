---
title: REST API
description: Screens as a Cloud Service提供符合Siren規範的簡單RESTful API。 請依照本頁了解如何導覽內容結構，並將命令傳送至環境中的裝置。
source-git-commit: fc3c047c6ad08db6e992a2aedc58c9cc1478b99f
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# REST API {#rest-apis}

AEM Screens提供遵循的簡單RESTful API [瑟靈](https://github.com/kevinswiber/siren) 規範。 它可導覽內容結構，並將命令傳送至環境中的裝置。

API可於 [*http://localhost:4502/api/screens.json*](http://localhost:4502/api/screens.json).

## 導覽內容結構 {#navigating-content-structure}

API呼叫傳回的JSON會列出與目前資源相關的實體。 在列出的自我連結後，這些實體中的每個都可作為REST資源再次存取。

例如，若要存取示範旗艦位置中的顯示器，您可以呼叫：

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

或使用curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

結果會如下：

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

接著，若要存取「單一畫面顯示」，您可以呼叫：

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## 對資源執行動作 {#executing-actions-on-the-resource}

API呼叫傳回的JSON可包含資源上可用的動作清單。

例如，顯示會列出 *廣播命令* 允許向分配給該顯示的所有設備發送命令的操作。

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

或使用curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***結果:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "title": "",
      "name": "broadcast-command",
      "method": "POST",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "fields": [
        {
          "name": ":operation",
          "value": "broadcast-command",
          "type": "hidden"
        },
        {
          "name": "msg",
          "type": "text"
        }
      ]
    }
  ]
}
```

若要觸發此動作，請呼叫：

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&msg=reboot
```

或使用curl:

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&msg=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```
