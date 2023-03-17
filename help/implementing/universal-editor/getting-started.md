---
title: AEM通用編輯器快速入門
description: 了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。
source-git-commit: acafa752c354781e41b11e46ac31a59feb8d94e7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# AEM通用編輯器快速入門 {#getting-started}

了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。

>[!TIP]
>
>如果您想要直接參閱範例，您可以檢閱 [GitHub上的通用編輯器範例應用程式。](https://github.com/adobe/universal-editor-sample-editable-app)

## 入門步驟 {#onboarding}

雖然通用編輯器可以編輯來自任何來源的內容，但本檔案將以AEM應用程式為例。

您可以執行許多步驟來建立AEM應用程式，並檢測應用程式以使用通用編輯器。

1. [請求對通用編輯器的存取權。](#request-access)
1. [包含通用編輯器核心程式庫。](#core-library)
1. [新增必要的OSGi設定。](#osgi-configurations)
1. [檢測頁面。](#instrument-page)

本檔案將引導您完成這些步驟。

## 要求存取通用編輯器 {#request-access}

您必須先要求通用編輯器的存取權。 請前往 [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor) 和驗證您是否擁有通用編輯器的存取權。

如果您沒有存取權，可透過連結至相同頁面的表單來請求。

## 包含通用編輯器核心程式庫 {#core-library}

應用程式必須包含下列相依性，才能檢測供通用編輯器使用。

```javascript
@adobe/universal-editor-cors
```

要激活檢測，需要將以下導入添加到 `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### 非React應用程式的替代方案 {#alternative}

若您未實作React應用程式，且/或需要伺服器端轉譯，替代方法是將下列內容納入檔案內文。

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## 新增必要的OSGi設定 {#osgi-configurations}

若要使用通用編輯器來編輯AEM內容與您的應用程式，必須在AEM內完成CORS和Cookie設定。

以下 [OSGi設定必須在AEM製作執行個體上設定。](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` 在 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* 刪除X-FRAME-OPTIONS:中的SAMEORIGIN標題 `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

登入Token Cookie必須以第三方網域的形式傳送至AEM。 因此，同網站Cookie必須明確設定為 `None`.

此屬性必須設定在 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` OSGi配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options:SAMEORIGIN可防止在iframe內轉譯AEM頁面。 移除標題可讓頁面載入。

此屬性必須設定在 `org.apache.sling.engine.impl.SlingMainServlet` OSGi配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## 檢測頁面 {#instrument-page}

通用編輯器服務需要 [統一資源名稱(URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 識別並運用正在編輯之應用程式中內容的正確後端系統。 因此，需要URN架構將內容對應回內容資源。

添加到頁面的檢測屬性大多由 [HTML微資料，](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) 一種行業標準，也可用於使HTML更加語義化、使HTML文檔可索引等等。

### 建立連線 {#connections}

應用程式中使用的連線會儲存為 `<meta>` 頁面的標籤 `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>`  — 這是一個簡短名稱，在文檔中重複使用，用於標識連接。 例如 `aemconnection`
* `<protocol>`  — 這表示要使用的通用編輯器持久性服務的持久性插件。 例如 `aem`
* `<url>`  — 這是系統的URL，系統會保存變更。 例如 `http://localhost:4502`

簡短識別碼 `auecon` 代表Adobe通用編輯器連線。

`itemid`s將使用 `urn` 前置詞來縮短識別碼。

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>`  — 這是 `<meta>` 標籤。 例如 `aemconnection`
* `<resource>`  — 這是指向目標系統中資源的指針。 例如AEM內容路徑，例如 `/content/page/jcr:content`

>[!TIP]
>
>請參閱檔案 [屬性和類型](attributes-types.md) 有關通用編輯器所需資料屬性和類型的詳細資訊。

### 連線範例 {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### 通用編輯器翻譯服務 {#translation}

通用編輯器根據檢測元資料執行翻譯。

#### 基本翻譯原則 {#principle}

請考量上一個範例中的下列選取項目。

```html
<meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
```

編輯器將執行替換，並在內部執行 `itemid` 會重新寫入下列內容。

```html
itemid="urn:aem:https://localhost:4502/content/example/list"
```

這會產生詞語 `aemconnection` 被 `<meta>` 標籤。

#### 查詢選擇器 {#query-selector}

這項取代將產生John Smith的下列查詢字串。

```html
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
  <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="urn:fcs:type/fragment">.  
    <p itemprop="name" itemtype="text">John Smith</p>
    <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
    <img itemprop="avatar" src="urn:fcs:missing" itemtype="image" alt="avatar"/>
  </li>
```

`[itemid="urn:fcs:https://example.franklin.adobe.com/345fcdd/content/example/list][itemprop="name"]`

如果要更改John Smith的表徵圖，選擇器將如下。

`[itemid="urn:aem:https://localhost:4502/content/example/another-source"][itemprop="title"]`

取代繼承 `itemid`通用編輯器使用範圍。 可以在節點級別上定義範圍，並由整個子結構繼承。

如果結構內的子結構或定義的離開需要不同的範圍，則另一個 `itemid` 可定義。

## 準備好使用通用編輯器 {#youre-ready}

您的應用程式現在經過創作，可使用通用編輯器！

請參閱該文檔 [使用通用編輯器編寫內容](authoring.md) 了解內容作者使用通用編輯器建立內容有多簡單且直覺。

## 其他資源 {#additional-resources}

若要進一步了解通用編輯器，請參閱這些檔案。

* [通用編輯器簡介](introduction.md)  — 了解通用編輯器如何啟用編輯任何實作中任何內容的任何方面，以提供優越的體驗、提高內容速度，並提供最新的開發人員體驗。
* [使用通用編輯器編寫內容](authoring.md)  — 了解內容作者使用通用編輯器建立內容有多簡單且直覺。
* [通用編輯器架構](architecture.md)  — 了解通用編輯器的架構，以及資料在其服務與層之間如何流動。
* [屬性和類型](attributes-types.md)  — 了解通用編輯器需要的資料屬性和類型。
* [通用編輯器驗證](authentication.md)  — 了解通用編輯器如何驗證。
