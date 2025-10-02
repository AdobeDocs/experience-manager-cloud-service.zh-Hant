---
title: AEM 中 Universal Editor 快速入門
description: 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8e1610e2835a9e85de2d2bffa6a883777c92fe96
workflow-type: ht
source-wordcount: '979'
ht-degree: 100%

---


# AEM 中 Universal Editor 快速入門 {#getting-started}

了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。

>[!TIP]
>
>若您比較喜歡直接從範例著手，可以檢閱 [GitHub 上的通用編輯器範例應用程式](https://github.com/adobe/universal-editor-sample-editable-app)。

雖然通用編輯器可以編輯來自任何來源的內容，但本文件會以 AEM 應用程式為例。本文件將引導您完成這些步驟。

## 檢測頁面 {#instrument-page}

通用編輯器需要一個 JavaScript 程式庫，才能在編輯器中轉譯和編輯頁面。

此外，通用編輯器服務需要[統一資源名稱 (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name)，才能針對正在編輯的應用程式之內容，找出並使用正確的後端系統。因此，必須使用 URN 結構描述，才能將內容對應回內容資源。

### 包括通用編輯器 CORS 程式庫 {#cors-library}

為了讓通用編輯器連結至您的應用程式，您的應用程式必須包含通用編輯器 CORS 程式庫。將以下指令碼新增至您的應用程式。

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### 建立連線 {#connections}

應用程式中使用的連線會儲存為`<meta>`頁面中的標記`<head>`。

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - 這是連線的分類，並有兩個選項。
   * `system` - 用於連線端點
   * `config` - 用於[定義選用設定](#configuration-settings)
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

### 設定 {#configuration-settings}

如需要，您可以使用連線 URN 中的 `config` 前置詞設定服務和擴充端點。

如果您不想使用由 Adobe 託管的通用編輯器服務，而是使用您自己的託管版本，可以在後設標記中進行設定。若要覆寫通用編輯器所提供的預設服務端點，請設定您自己的服務端點：

* 後設名稱 - `urn:adobe:aue:config:service`
* 後設內容 - `content="https://adobe.com"` (範例)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

如果您只想啟用特定的頁面擴充功能，可以在後設標記中進行設定。若要取得擴充功能，請設定擴充端點：

* 後設名稱：`urn:adobe:aue:config:extensions`
* 後設內容：`content="https://adobe.com,https://anotherone.com,https://onemore.com"` (範例)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## 定義通用編輯器應針對哪些內容路徑或 `sling:resourceType` 而開啟。(選用) {#content-paths}

若您有現有的 AEM 專案使用[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)，則當內容作者編輯頁面時，頁面會自動使用頁面編輯器開啟。無論所選內容需要使用哪個編輯器，您都可以根據內容路徑或 `sling:resourceType` 來定義 AEM 應開啟哪個編輯器，為您的作者提供順暢體驗。

1. 開啟 Configuration Manager。

   `http://<host>:<port>/system/console/configMgr`

1. 在清單中找到「**通用編輯器 URL 服務**」，然後按一下「**編輯設定值**」。

1. 定義通用編輯器應針對哪些內容路徑或 `sling:resourceType` 而開啟。

   * 在「**通用編輯器開啟對應**」欄位中，提供通用編輯器的開啟路徑。
   * 在「**應由通用編輯器開啟之 Sling:resourceTypes**」欄位中，列出由通用編輯器直接開啟的資源。

1. 按一下「**儲存**」。

1. 查看您的 [Externalizer 設定](/help/implementing/developing/tools/externalizer.md)，並確保至少已設定本機、作者和發佈環境，如下列範例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成這些設定步驟後，AEM 會依照以下順序開啟頁面的通用編輯器。

1. AEM 會檢查 `Universal Editor Opening Mapping` 之下的對應，若內容位於該處所定義的任何路徑之下，便會針對該內容開啟通用編輯器。
1. 對於不在 `Universal Editor Opening Mapping` 中所定義路徑之下的內容，AEM 會檢查內容的 `resourceType` 是否與「**應由通用編輯器開啟之 Sling:resourceTypes**」中定義者相符，若內容符合其中一種類型，便會針對該內容在 `${author}${path}.html` 開啟通用編輯器。
1. 否則，AEM 會開啟頁面編輯器。

在「**通用編輯器開啟對應**」欄位中可以使用以下變數來定義您的對應。

* `path`：要開啟的資源內容路徑
* `localhost`：`localhost` 的 Externalizer 項目，無結構描述，例如 `localhost:4502`
* `author`：作者的 Externalizer 項目，無結構描述，例如 `localhost:4502`
* `publish`：發佈的 Externalizer 項目，無結構描述，例如 `localhost:4503`
* `preview`：預覽的 Externalizer 項目，無結構描述，例如 `localhost:4504`
* `env`：`prod`、`stage`、`dev`，根據所定義的 Sling 執行模式
* `token`：`QueryTokenAuthenticationHandler` 所需的查詢權杖

### 對應範例 {#example-mappings}

* 在 AEM Author 上開啟 `/content/foo` 之下的所有頁面：

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 這樣會開啟 `https://localhost:4502/content/foo/x.html?login-token=<token>`

* 在遠端 NextJS 伺服器上開啟 `/content/bar` 之下的所有頁面，並提供所有變數做為資訊：

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 這樣會開啟 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

## 您已準備好使用 Universal Editor {#youre-ready}

您的應用程式現在可以使用 Universal Editor 了！

請參閱[使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md)以了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。

{{ue-headless-auth}}

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
* [使用通用編輯器發佈內容](/help/implementing/universal-editor/publishing.md) - 了解通用編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。

