---
title: 螢幕中的Dispatcher設定as a Cloud Service
description: 本頁說明Screensas a Cloud Service的Dispatcher設定。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 螢幕中的Dispatcher設定as a Cloud Service {#dispatcher-configurations-screens-cloud}

本節說明Screensas a Cloud Service的Dispatcher設定。

## 在Dispatcher for Screens中新增篩選器和快取規則，以as a Cloud Service部署 {#deployment}

在Screensas a Cloud Service中，為發佈例項在Dispatcher中允許下列篩選器和快取規則。

### AEM Screens篩選器 {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### 快取規則 {#cache-rules}

* 新增 `/statfileslevel "10"` to `/cache` 區段 `publish_farm.any`/.

   >[!NOTE]
   >此快取規則支援從快取快取中快取高達10個層級，且內容發佈時會失效，而非使所有內容失效。 您可以根據內容結構的設定深度來變更此層級。

* 將下列項目新增至 `/invalidate` 區段 `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 將下列規則新增至 `/rules` 區段 `/cache` 在publish_farm.any中，或包含在 `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
        }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
