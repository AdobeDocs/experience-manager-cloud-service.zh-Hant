---
title: Screens as aCloud Service中的Dispatcher設定
description: 本頁將Screens中的Dispatcher設定描述為Cloud Service。
source-git-commit: b00856e1be8842c4e9fa6ed4ada9129926c73ef5
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Screens as aCloud Service中的Dispatcher設定{#dispatcher-configurations-screens-cloud}

本節將Screens的Dispatcher設定說明為Cloud Service。

## 以Screens作為Cloud Service部署的Dispatcher設定 {#deployment}

在Screens中，針對發佈例項，在Dispatcher中允許下列篩選器和快取規則作為Cloud Service。

### 濾鏡 {#filters}

## AEM Screens篩選器

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

## 快取規則 {#cache-rules}

* 將`/statfileslevel "10"`新增至`publish_farm.any`/中的`/cache`區段。

   >[!NOTE]
   >這可支援從快取快取最多10個層級，且在內容發佈時會失效，而非讓所有內容失效。 您可以根據內容結構的深度來變更此層級。

* 將下列內容新增至`publish_farm.any`中的`/invalidate`區段。

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 將下列規則新增至publish_farm.any中`/cache`區段或`publish_farm.any`所含檔案中的`/rules`區段。

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
