---
title: Screens中的Dispatcher設定as a Cloud Service
description: 本頁說明Screensas a Cloud Service中的Dispatcher設定。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Screens中的Dispatcher設定as a Cloud Service {#dispatcher-configurations-screens-cloud}

本節說明Screensas a Cloud Service的Dispatcher設定。

## 在適用於Screensas a Cloud Service部署的Dispatcher中新增篩選器和快取規則 {#deployment}

在Screens as a Cloud Service中，允許發佈執行個體在Dispatcher中使用以下篩選器和快取規則。

### AEM Screens篩選器 {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### 快取規則 {#cache-rules}

* 將`/statfileslevel "10"`新增至`publish_farm.any`/中的`/cache`區段。

  >[!NOTE]
  >此快取規則支援快取docroot中的最多10個層級，且在內容發佈時失效，而不是使所有內容失效。 您可以根據內容結構的設定深度來變更此層級。

* 新增下列內容至`publish_farm.any`中的`/invalidate`區段。

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* 將下列規則新增至publish_farm.any中`/cache`的`/rules`區段或從`publish_farm.any`包含的檔案中。

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
