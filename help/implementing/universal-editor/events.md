---
title: 通用編輯器事件
description: 瞭解通用編輯器傳送的不同事件，您可用這些事件對遠端應用程式中的內容或UI變更做出反應。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 通用編輯器事件 {#events}

瞭解通用編輯器傳送的不同事件，您可用這些事件對遠端應用程式中的內容或UI變更做出反應。

## 簡介 {#introduction}

應用程式對頁面或元件更新可能有不同的需求。 因此，Universal Editor會將定義的事件傳送給遠端應用程式。 如果遠端應用程式沒有已傳送事件的自訂事件接聽程式，則會執行[封裝所提供的](#fallback-listeners)遞補事件接聽程式`universal-editor-cors`。

所有事件都會在遠端頁面中受影響的DOM元素上叫用。 事件泡泡至`BODY`元素，其中已註冊`universal-editor-cors`封裝提供的預設事件接聽程式。 UI有內容和事件專用的事件。

所有事件都遵循命名慣例。

* `aue:<content-or-ui>-<event-name>`

例如，`aue:content-update`和`aue:ui-select`

事件包含請求和回應的裝載，並會在對應的呼叫成功時觸發。 如需呼叫及其裝載範例的詳細資訊，請參閱檔案[通用編輯器呼叫](/help/implementing/universal-editor/calls.md)。

## 內容更新事件 {#content-events}

### aue:content-add {#content-add}

將新元件新增至容器時會觸發`aue:content-add`事件。

裝載是來自通用編輯器服務的內容，且包含元件定義的遞補內容。

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

將元件載入屬性面板時，就會觸發`aue:content-details`事件。

裝載是元件的內容，並可選擇是其結構。

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

移動元件時會觸發`aue:content-move`事件。

裝載是元件、來源容器和目標容器。

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

當在屬性面板中更新元件的資料時，就會觸發`aue:content-patch`事件。

裝載是已更新屬性的JSON修補程式。

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

從容器移除元件時會觸發`aue:content-remove`事件。

裝載是已移除元件的專案ID。

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

當在內容中更新元件的屬性時，就會觸發`aue:content-update`事件。

裝載是更新的值。

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### 傳遞裝載 {#passing-payloads}

對於所有內容更新事件，請求的裝載以及回應裝載會傳遞至事件。 例如，對於更新呼叫：

請求裝載：

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

回應裝載

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

## UI事件 {#ui-events}

### aue:ui-preview {#ui-preview}

當頁面的編輯模式變更為`aue:ui-preview`預覽&#x200B;**時，就會觸發**&#x200B;事件。

此事件的裝載是空的。

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

當頁面的編輯模式變更為`aue:ui-edit`編輯&#x200B;**時，就會觸發**&#x200B;事件。

此事件的裝載是空的。

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

檢視區大小變更時會觸發`aue:ui-viewport-change`事件。

裝載是檢視區的維度。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initialized {#initialized}

會觸發`aue:initialized`事件，讓遠端頁面知道它已成功載入通用編輯器中。

此事件的裝載是空的。

```json
{
    details: {}
}
```

## 遞補事件接聽程式 {#fallback-listeners}

### 內容更新 {#content-update-fallbacks}

| 事件 | 行為 |
|---|---|
| `aue:content-add` | 頁面重新載入 |
| `aue:content-details` | 不執行任何動作 |
| `aue:content-move` | 將元件的內容/結構移至目標區域 |
| `aue:content-patch` | 頁面重新載入 |
| `aue:content-remove` | 移除DOM元素 |
| `aue:content-update` | 以承載更新`innerHTML` |

### UI事件 {#ui-event-fallbacks}

| 事件 | 行為 |
|---|---|
| `aue:ui-select` | 捲動至選取的元素 |
| `aue:ui-preview` | 將`class="adobe-ue-preview"`新增至HTML標籤 |
| `aue:ui-edit` | 將`class=adobe-ue-edit"`新增至HTML標籤 |
| `aue:ui-viewport-change` | 不執行任何動作 |
| `aue:initialized` | 不執行任何動作 |

## 其他資源 {#additional-resources}

* [Universal Editor 呼叫](/help/implementing/universal-editor/calls.md)

