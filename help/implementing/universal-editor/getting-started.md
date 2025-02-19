---
title: AEM 中 Universal Editor 快速入門
description: 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 07a8ad6083dbb7cf69148773d266b33e8cf32a38
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 36%

---


# AEM 中 Universal Editor 快速入門 {#getting-started}

了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。

>[!TIP]
>
>如果您想直接深入瞭解範例，可以在GitHub](https://github.com/adobe/universal-editor-sample-editable-app)上檢閱[通用編輯器範例應用程式。

雖然通用編輯器可以編輯任何來源的內容，但本檔案將以AEM應用程式為例。 本文件將引導您完成這些步驟。

## 檢測頁面 {#instrument-page}

Universal Editor需要JavaScript程式庫，才能在編輯器中轉譯和編輯頁面。

此外，Universal Editor服務需要[統一資源名稱(URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name)，才能識別及使用所編輯應用程式內容的正確後端系統。 因此，需要 URN 結構描述將內容對應回內容資源。

### 包含通用編輯器CORS資料庫 {#cors-library}

為了讓Universal Editor連線至您的應用程式，您的應用程式必須包含Universal Editor CORS資料庫。 將下列指令碼新增至您的應用程式。

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

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

如果您不想使用由Adobe託管但您自己託管版本的通用編輯器服務，可以在中繼標籤中設定此專案。 若要覆寫Universal Editor提供的預設服務端點，請設定您自己的服務端點：

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

## 定義應開啟通用編輯器的內容路徑或`sling:resourceType`。 (可選) {#content-paths}

如果您有使用[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)的現有AEM專案，內容作者編輯頁面時，頁面會自動使用頁面編輯器開啟。 您可以根據內容路徑或`sling:resourceType`定義應開啟AEM的編輯器，讓您的作者獲得流暢的體驗，無論所選內容需要哪個編輯器。

1. 若要使用此設定功能，請聯絡Adobe客戶服務，為您的方案啟用對通用編輯器URL服務的存取權。

1. 一旦客戶服務啟用了通用編輯器URL服務的存取權，請開啟Configuration Manager。

   `http://<host>:<port>/system/console/configMgr`

1. 在清單中找到&#x200B;**通用編輯器URL服務**，然後按一下&#x200B;**編輯設定值**。

1. 定義應開啟通用編輯器的內容路徑或`sling:resourceType`。

   * 在&#x200B;**Universal Editor Opening Mapping**&#x200B;欄位中，提供開啟Universal Editor的路徑。
   * 在應由通用編輯器開啟的&#x200B;**Sling：resourceTypes**&#x200B;欄位中，提供由通用編輯器直接開啟的資源清單。

1. 按一下「**儲存**」。

1. 檢查您的[外部化程式組態](/help/implementing/developing/tools/externalizer.md)，並確定您至少有本機、作者和發佈環境設定，如下列範例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成這些設定步驟後，AEM將依下列順序開啟頁面的通用編輯器。

1. AEM將檢查`Universal Editor Opening Mapping`底下的對應，如果內容位於該處定義的任何路徑下，則會為其開啟通用編輯器。
1. 對於不在`Universal Editor Opening Mapping`中定義的路徑下的內容，AEM會檢查內容的`resourceType`是否與&#x200B;**Sling：resourceTypes （應由通用編輯器**&#x200B;開啟）中定義的內容相符，如果內容符合其中一個型別，則在`${author}${path}.html`為其開啟通用編輯器。
1. 否則，AEM會開啟頁面編輯器。

下列變數可用於在&#x200B;**Universal Editor Opening Mapping**&#x200B;欄位中定義您的對應。

* `path`：要開啟之資源的內容路徑
* `localhost`： `localhost`的Externalizer專案沒有結構描述，例如`localhost:4502`
* `author`：沒有結構描述的作者的Externalizer專案，例如`localhost:4502`
* `publish`：用於沒有結構描述的發行的Externalizer專案，例如`localhost:4503`
* `preview`：預覽的外部化程式專案，不含結構描述，例如`localhost:4504`
* `env`： `prod`、`stage`、`dev`根據定義的Sling執行模式
* `token`： `QueryTokenAuthenticationHandler`所需的查詢權杖

### 範例對應 {#example-mappings}

* 在AEM作者上開啟`/content/foo`下的所有頁面：

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 這會導致開啟`https://localhost:4502/content/foo/x.html?login-token=<token>`

* 在遠端NextJS伺服器上開啟`/content/bar`下的所有頁面，提供所有變數作為資訊：

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 這會導致開啟`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

## 您已準備好使用 Universal Editor {#youre-ready}

您的應用程式現在可以使用 Universal Editor 了！

請參閱[使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md)以了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 編寫內容](/help/sites-cloud/authoring/universal-editor/authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
* [使用通用編輯器發佈內容](/help/implementing/universal-editor/publishing.md) — 瞭解通用編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。

