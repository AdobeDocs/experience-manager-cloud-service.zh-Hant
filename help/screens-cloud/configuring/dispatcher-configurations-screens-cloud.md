---
title: 螢幕中的Dispatcher配置as a Cloud Service
description: 本頁介紹螢幕as a Cloud Service中的Dispatcher配置。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 螢幕中的Dispatcher配置as a Cloud Service {#dispatcher-configurations-screens-cloud}

本節介紹螢幕as a Cloud Service的調度程式配置。

## 在Dispatcher中為螢幕添加篩選器和快取規則as a Cloud Service部署 {#deployment}

允許在調度程式中為螢幕as a Cloud Service中的發佈實例使用以下篩選器和快取規則。

### AEM Screens過濾器 {#filters}

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

* 添加 `/statfileslevel "10"` 至 `/cache` 部分 `publish_farm.any`/。

   >[!NOTE]
   >此快取規則支援從快取域快取多達10個級別，並在發佈內容時使其失效，而不是使所有內容失效。 您可以根據內容結構的設定深度更改此級別。

* 將以下內容添加到 `/invalidate` 部分 `publish_farm.any`。

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 將以下規則添加到 `/rules` 部分 `/cache` publish_farm.any或包含於 `publish_farm.any`。

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
