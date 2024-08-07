---
title: AEM 中 Universal Editor 快速入門
description: 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 395cb7b2e37c7358baa7ae07329f42bd5a560cb1
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 68%

---


# AEM 中 Universal Editor 快速入門 {#getting-started}

了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。

>[!TIP]
>
>如果您想直接研究範例，可以查看 [GitHub 上的 Universal Editor 範例應用程式。](https://github.com/adobe/universal-editor-sample-editable-app)

## 上線步驟 {#onboarding}

雖然 Universal Editor 可以編輯來自任何來源的內容，但本文件將以 AEM 應用程式為例。

入門使用AEM應用程式並檢測其是否使用通用編輯器有數個步驟。

1. [包括 Universal Editor 核心庫。](#core-library)
1. [新增必要的 OSGi 設定。](#osgi-configurations)
1. [檢測頁面。](#instrument-page)

本文件將引導您完成這些步驟。

## 包括 Universal Editor 核心庫。 {#core-library}

您必須先包含下列相依性，應用程式才能透過通用編輯器進行檢測。

```javascript
@adobe/universal-editor-cors
```

若要啟動檢測，必須將下列匯入加入您的`index.js`。

```javascript
import "@adobe/universal-editor-cors";
```

### Non-React 應用程式的替代方案 {#alternative}

如果您未實作React應用程式和/或需要伺服器端轉譯，另一種方法是在檔案本文中納入以下內容。

```html
<script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST" async></script>
```

我們一律會建議使用最新版本，但若發生重大變更，可參考舊版服務。

* `https://universal-editor-service.experiencecloud.live/corslib/LATEST` — 最新UE CORS程式庫
* `https://universal-editor-service.experiencecloud.live/corslib/2/LATEST` - 2.x版下最新的UE CORS程式庫
* `https://universal-editor-service.experiencecloud.live/corslib/2.1/LATEST` - 2.1.x版下最新的UE CORS程式庫
* `https://universal-editor-service.experiencecloud.live/corslib/2.1.1` — 完全相同的UE CORS程式庫2.1.1版

## 新增必要的 OSGi 設定 {#osgi-configurations}

為了能夠使用 Universal Editor 透過您的應用程式編輯 AEM 內容，必須在 AEM 中完成 CORS 和 Cookie 設定。

[必須在 AEM 編寫執行個體上設定以下 OSGi 設定。](/help/implementing/deploying/configuring-osgi.md)

* `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` 中的 `SameSite Cookies = None`
* 移除 X-FRAME-OPTIONS：`org.apache.sling.engine.impl.SlingMainServlet` 中的 SAMEORIGIN 標頭

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

登入權杖 Cookie 必須作為協力廠商網域發送到 AEM。因此，必須將同網站的 Cookie 明確設定為 `None`。

此屬性必須在 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`OSGi 設定中設定。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options：SAMEORIGIN 禁止在 iframe 中呈現 AEM 頁面。移除標頭可載入頁面。

此屬性必須在 `org.apache.sling.engine.impl.SlingMainServlet`OSGi 設定中設定。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## 檢測頁面 {#instrument-page}

Universal Editor 服務需要[統一資源名稱 (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 來識別和使用正確的後端系統來處理應用程式中正在編輯的內容。因此，需要 URN 模式將內容對應回內容資源。

### 建立連線 {#connections}

應用程式中使用的連線會儲存為`<meta>`頁面中的標記`<head>`。

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` — 這是具有兩個選項的連線分類。
   * `system` — 用於連線端點
   * `config` — 針對[定義選擇性組態設定](#configuration-settings)
* `<referenceName>` - 這是簡短名稱，可在文件中重複使用以標識連線。例如 `aemconnection`
* `<protocol>` - 這代表要使用 Universal Editor 持續性服務的哪個持續性外掛程式。例如 `aem`
* `<url>` - 這是儲存變更之系統的 URL。例如 `http://localhost:4502`

識別碼 `urn:adobe:aue:system` 表示 Adobe Universal Editor 連線。

`data-aue-resource` 將使用 `urn` 首碼來縮短識別碼。

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>` - 這是 `<meta>` 標記中提及的命名參考。例如 `aemconnection`
* `<resource>` - 這是指向目標系統中資源的指標。像是 AEM 內容路徑，例如 `/content/page/jcr:content`

>[!TIP]
>
>請參閱文件[屬性和類型](attributes-types.md)以深入了解 Universal Editor 需要的資料屬性和類型。

### 連線範例 {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### 組態設定 {#configuration-settings}

您可以視需要使用連線URN中的`config`首碼來設定服務和擴充端點。

如果您不想使用由Adobe託管（但您自己的託管版本）的通用編輯器服務，可以在中繼標籤中設定此專案。 若要覆寫Universal Editor提供的預設服務端點，請設定您自己的服務端點：

* 中繼名稱 — `urn:adobe:aue:config:service`
* 中繼內容 — `content="https://adobe.com"` （範例）

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

如果您只想為頁面啟用特定擴充功能，可以在meta標籤中加以設定。 若要擷取擴充功能，請設定擴充功能端點：

* 中繼名稱： `urn:adobe:aue:config:extensions`
* 中繼內容： `content="https://adobe.com,https://anotherone.com,https://onemore.com"` （範例）

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## 您已準備好使用 Universal Editor {#youre-ready}

您的應用程式現在可以使用 Universal Editor 了！

請參閱[使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md)以了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
* [使用通用編輯器發佈內容](/help/sites-cloud/authoring/universal-editor/publishing.md) — 瞭解通用編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。

