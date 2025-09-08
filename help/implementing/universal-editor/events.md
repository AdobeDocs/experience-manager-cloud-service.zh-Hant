---
title: 通用編輯器事件
description: 了解通用編輯器傳送的不同事件，而您可以使用這些事件回應遠端應用程式中的內容或使用者介面變更。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '510'
ht-degree: 100%

---

# 通用編輯器事件 {#events}

了解通用編輯器傳送的不同事件，而您可以使用這些事件回應遠端應用程式中的內容或使用者介面變更。

## 簡介 {#introduction}

應用程式對於頁面或元件更新可能有不同的需求。因此，通用編輯器會將已定義的事件傳送至遠端應用程式。如果遠端應用程式沒有自訂的事件監聽器可以處理所傳送的事件，便會執行 `universal-editor-cors` 封裝提供的[後備事件監聽器](#fallback-listeners)。

在遠端頁面的受影響 DOM 元素上會叫用所有事件。事件會逐層向上傳播至 `BODY` 元素，而由 `universal-editor-cors` 封裝所提供的預設事件監聽器就是在這裡註冊的。內容和使用者介面均有各自的事件。

所有事件都遵循命名慣例。

* `aue:<content-or-ui>-<event-name>`

例如，`aue:content-update` 和 `aue:ui-select`

事件包括請求和回應的承載，並在相應的呼叫成功後觸發。關於呼叫及其承載範例的更多詳細資訊，請參閱[通用編輯器呼叫](/help/implementing/universal-editor/calls.md)文件。

## 內容更新事件 {#content-events}

### aue:content-add {#content-add}

當新元件新增至容器時會觸發 `aue:content-add` 事件。

承載是來自通用編輯器服務的內容，以及來自元件定義的後備內容。

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

當屬性面板中載入元件時會觸發 `aue:content-details` 事件。

承載是元件的內容，以及可選擇包含其結構描述。

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:content-move {#content-move}

當元件移動時會觸發 `aue:content-move` 事件。

承載是元件、來源容器和目標容器。

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-patch {#content-patch}

當屬性面板中元件的資料更新時會觸發 `aue:content-patch` 事件。

承載是所更新屬性的 JSON 修補程式。

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-remove {#content-remove}

當元件從容器中移除時會觸發 `aue:content-remove` 事件。

承載是所移除元件的項目 ID。

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-update {#content-update}

當元件的屬性在內容中更新時，會觸發 `aue:content-update` 事件。

承載是所更新的值。

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### 傳遞承載 {#passing-payloads}

對於所有內容更新事件，所請求的承載以及回應承載都會傳遞至事件中。例如，對於更新呼叫：

請求承載：

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

回應承載

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## 使用者介面事件 {#ui-events}

### aue:ui-preview {#ui-preview}

當頁面的編輯模式變更為「**預覽**」時會觸發 `aue:ui-preview` 事件。

此事件的承載為空。

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

當頁面的編輯模式變更為「**編輯**」時會觸發 `aue:ui-edit` 事件。

此事件的承載為空。

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

當檢視區大小變更時會觸發 `aue:ui-viewport-change` 事件。

承載是檢視區的尺寸。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initialized {#initialized}

觸發 `aue:initialized` 事件，讓遠端頁面知道其已成功載入通用編輯器中。

此事件的承載為空。

```json
{
    details: {}
}
```

## 後備事件監聽器 {#fallback-listeners}

### 內容更新 {#content-update-fallbacks}

| 事件 | 行為 |
|---|---|
| `aue:content-add` | 頁面重新載入 |
| `aue:content-details` | 無任何動作 |
| `aue:content-move` | 將元件的內容/結構移動至目標區域 |
| `aue:content-patch` | 頁面重新載入 |
| `aue:content-remove` | 移除 DOM 元素 |
| `aue:content-update` | 使用承載更新 `innerHTML` |

### 使用者介面事件 {#ui-event-fallbacks}

| 事件 | 行為 |
|---|---|
| `aue:ui-select` | 捲動至所選元素 |
| `aue:ui-preview` | 將 `class="adobe-ue-preview"` 新增至 HTML 標記 |
| `aue:ui-edit` | 將 `class=adobe-ue-edit"` 新增至 HTML 標記 |
| `aue:ui-viewport-change` | 無任何動作 |
| `aue:initialized` | 無任何動作 |

## 其他資源 {#additional-resources}

* [通用編輯器呼叫](/help/implementing/universal-editor/calls.md)

