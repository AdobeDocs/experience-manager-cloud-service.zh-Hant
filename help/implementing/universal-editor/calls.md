---
title: 通用編輯器呼叫
description: 了解通用編輯器對您的應用程式進行的不同類型的呼叫，以協助您進行偵錯。
exl-id: 00d66e59-e445-4b5c-a5b1-c0a9f032ebd9
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 100%

---


# 通用編輯器呼叫 {#calls}

了解通用編輯器對您的應用程式進行的不同類型的呼叫，以協助您進行偵錯。

## 概觀 {#overview}

通用編輯器會透過一系列定義的呼叫，與您已檢測的應用程式進行通訊。一般使用者不會察覺這個過程，對於使用者體驗也不會造成影響。

然而，對於開發人員來說，了解這些呼叫及其作用，在使用通用編輯器進行應用程式偵錯時便能發揮重要作用。若已對應用程式進行檢測，其運作情況卻不如預期，您在應用程式中編輯內容時，可在瀏覽器中開啟開發人員工具的「**網路**」標籤並檢查呼叫，這會有所幫助。

![瀏覽器開發人員工具「網路」標籤上詳細資訊呼叫的範例](assets/calls-network-tab.png)

* 呼叫的&#x200B;**承載**&#x200B;包含編輯器正在更新之內容的詳細資訊，包括識別要更新的內容以及更新方式。
* **回應**&#x200B;包含編輯器服務實際更新之內容的詳細資訊。這是為了方便重新整理編輯器中的內容。在某些情況下，例如 `move` 呼叫，必須重新整理整個頁面。

呼叫成功完成後，即會觸發包含請求承載和回應承載的事件，而您可以針對自己的應用程式進行自訂。如需更多詳細資訊，請參閱[通用編輯器事件](/help/implementing/universal-editor/events.md)文件。

以下清單是通用編輯器對您的應用程式發出之呼叫類型，並提供承載和回應的範例。

## 更新 {#update}

當您使用通用編輯器編輯應用程式中的內容時，會發生 `update` 呼叫。`update` 會保留變更。

其承載包括要寫回 JCR 之內容的詳細資訊。

* `resource`：要更新的 JCR 路徑
* `prop`：正在進行更新的 JCR 屬性
* `type`：正在更新之屬性的 JCR 值類型
* `value`：已更新的資料

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

>[!TAB 回應範例]

```json
{
  "updates": [
    {
      "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
      "prop": "jcr:title",
      "type": "text"
    }
  ]
}
```

>[!ENDTABS]

## 詳細資訊 {#details}

在通用編輯器中載入您的應用程式以檢索應用程式內容時，會發生 `details` 呼叫。

其承載包括要轉譯的資料，以及資料所代表之內容 (結構描述) 的詳細資訊，使其可以在通用編輯器中進行轉譯。

* 對於元件，通用編輯器僅會檢索 `data` 物件，因為資料的結構描述是在應用程式中定義的。
* 對於內容片段，通用編輯器也會檢索 `schema` 物件，因為內容片段模型是在 JCR 中定義的。

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "component",
    "prop": ""
  }
}
```

>[!TAB 回應範例]

```json
{
  "data": {
    "jcr:primaryType": "nt:unstructured",
    "jcr:title": "Tiny Toon Adventures",
    "fileReference": "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/adobestock-216674449.jpeg",
    "cq:panelTitle": "WKND Adventures",
    "actionsEnabled": "true",
    "jcr:lastModifiedBy": "admin",
    "titleFromPage": "false",
    "jcr:description": "<p>With WKND Adventures, you don't just see the world you experinece it.</p>\r\n",
    "jcr:lastModified": "Fri Jan 19 2024 11:05:59 GMT+0100",
    "descriptionFromPage": "true",
    "sling:resourceType": "wknd/components/teaser",
    "textIsRich": "true",
    "cq:styleIds": [
      "1555543212672"
    ],
    "actions": {
      "jcr:primaryType": "nt:unstructured",
      "item0": {
        "jcr:primaryType": "nt:unstructured",
        "link": "/content/wknd/language-masters/en/adventures",
        "text": "View Trips"
      }
    }
  }
}
```

>[!ENDTABS]

## 新增 {#add}

當您使用通用編輯器在應用程式中放置新元件時，會發生 `add` 呼叫。

其承載包括 `path` 物件，其中包含新增內容應該放在哪個位置。

此呼叫亦包含 `content` 物件，而此物件中有額外的物件，用來儲存[每個外掛程式](/help/implementing/universal-editor/architecture.md)的內容之端點特定詳細資訊。例如，若您的應用程式以 AEM 和 Magento 的內容為基礎，則承載會包含每個系統的資料物件。

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  },
  "content": {
    "name": "text",
    "aem": {
      "page": {
        "resourceType": "wknd/components/text",
        "template": {
          "text": "Default Text"
        }
      }
    }
  }
}
```

>[!TAB 回應範例]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ],
  "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521"
}
```

>[!ENDTABS]

## 移動 {#move}

當您使用通用編輯器在應用程式內移動元件時，會發生 `move` 呼叫。

其承載包含 `from` 物件，負責定義元件先前的位置，並包含 `to` 物件，負責定義元件移動至何處。

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "from": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    },
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847",
      "type": "media",
      "prop": "fileReference"
    }
  },
  "to": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

>[!TAB 回應範例]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ]
}
```

>[!ENDTABS]

## 移除 {#remove}

當您使用通用編輯器在應用程式內刪除元件時，會發生 `remove` 呼叫。

其承載包含所移除物件的路徑。

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_593170193",
      "type": "text",
      "prop": "text"
    },
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

>[!TAB 回應範例]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "prop": "",
      "type": "container"
    }
  ]
}
```

>[!ENDTABS]

## 發佈 {#publish}

當您按一下通用編輯器中的「**發佈**」按鈕發佈您所編輯的內容時，會發生 `publish` 呼叫。

通用編輯器會逐一檢查相關內容，並產生同樣必須發佈的參照清單。

>[!BEGINTABS]

>[!TAB 承載範例]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "references": [
    "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/title",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/title",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_229050934",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_2123678383",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1668104604",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847"
  ]
}
```

>[!TAB 回應範例]

```json
{
  "publishes": [
    "/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway",
    "/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp",
    "/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand",
    "/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah",
    "/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany",
    "/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming",
    "/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting",
    "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia",
    "/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc",
    "/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica",
    "/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing",
    "/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling",
    "/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking",
    "/content/wknd/us/en/newsletter",
    "/content/wknd/language-masters/en/universal-editor-container"
  ]
}
```

>[!ENDTABS]

## 其他資源 {#additional-resources}

* [通用編輯器事件](/help/implementing/universal-editor/events.md)

