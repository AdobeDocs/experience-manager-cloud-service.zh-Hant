---
title: 在AEMas a Cloud Service上使用用戶端程式庫
description: AEM提供用戶端程式庫資料夾，可讓您將用戶端程式碼(clientlibs)儲存在存放庫中、將其組織為類別，以及定義將每個類別的程式碼提供給用戶端的時間和方式
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: b93ec12616742910e35a3dac4224b690cd2c7116
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 1%

---


# 在AEMas a Cloud Service上使用用戶端程式庫 {#using-client-side-libraries}

數位體驗嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 AEM用戶端程式庫(clientlibs)可讓您組織這些用戶端程式庫，並集中儲存在存放庫中。 與 [AEM專案原型中的前端建置程式，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 管理AEM專案的前端程式碼變得簡單。

在AEM中使用clientlib的優點包括：

* 用戶端代碼與所有其他應用程式代碼和內容一樣儲存在儲存庫中
* AEM中的Clientlib可將所有CSS和JS匯總為一個檔案
* 透過可透過 [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* 允許重寫引用的檔案或影像的路徑

Clientlibs是從AEM傳送CSS和Javascript的內建解決方案。

>[!TIP]
>
>為AEM專案建立CSS和Javascript的前端開發人員也應熟悉 [AEM專案原型及其自動化前端建置程式。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什麼是用戶端程式庫 {#what-are-clientlibs}

網站需要JavaScript和CSS，以及靜態資源（例如圖示和網頁字型），才能在用戶端處理。 clientlib是AEM機制，可參考（若需要，可依類別）並提供這類資源。

AEM會將網站的CSS和Javascript收集到集中位置的單一檔案，以確保HTML輸出中只包含任何資源的一個副本。 這可最大化傳送效率，並允許透過代理在存放庫中集中維護這些資源，以保證存取安全。

## AEMas a Cloud Service的前端開發 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端資產都應在 [AEM專案原型的ui.frontend模組。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的彈性可讓您使用您所選擇的現代化網頁工具來建立及管理這些資源。

原型隨後可將資源編譯為單一CSS和JS檔案，並自動將其內嵌至 `cq:clientLibraryFolder` 儲存庫中。

## 用戶端程式庫資料夾結構 {#clientlib-folders}

用戶端程式庫資料夾是類型的存放庫節點 `cq:ClientLibraryFolder`. 其定義於 [CND標籤法](https://jackrabbit.apache.org/node-type-notation.html) is

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 節點可以放置在 `/apps` 存放庫的子樹狀結構。
* 使用 `categories` 節點的屬性，以識別其所屬的程式庫類別。

每個 `cq:ClientLibraryFolder` 會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下方）。 重要屬性 `cq:ClientLibraryFolder` 設定如下：

* `allowProxy`:由於所有clientlib必須儲存在 `apps`，此屬性可透過代理servlet存取用戶端程式庫。 請參閱 [找到客戶端庫資料夾並使用代理客戶端庫Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下方。
* `categories`:識別JS和/或CSS檔案集在此內所屬的類別 `cq:ClientLibraryFolder` 摔倒。 此 `categories` 屬性為多值，可讓程式庫資料夾成為多個類別的一部分（請參閱下方以了解其效用）。

如果用戶端程式庫資料夾包含一或多個執行階段會合併為單一JS和/或CSS檔案的來源檔案。 產生的檔案名稱為節點名稱，且 `.js` 或 `.css` 檔案名副檔名。 例如，名為的程式庫節點 `cq.jquery` 導致產生的檔案名為 `cq.jquery.js` 或 `cq.jquery.css`.

用戶端程式庫資料夾包含下列項目：

* JS和/或CSS來源檔案
* 支援CSS樣式的靜態資源，例如圖示、網頁字型等。
* 一 `js.txt` 檔案和/或一個 `css.txt` 識別要合併到所產生JS和/或CSS檔案的來源檔案的檔案

![Clientlib架構](assets/clientlib-architecture.drawio.png)

## 建立用戶端程式庫資料夾 {#creating-clientlib-folders}

客戶端庫必須位於 `/apps`. 這是為了更妥善地將程式碼與內容及設定隔離。

為了在 `/apps` 若要存取，請使用代理伺服器。 ACL仍在客戶端庫資料夾上強制執行，但Servlet允許通過讀取內容 `/etc.clientlibs/` 若 `allowProxy` 屬性設為 `true`.

1. 在網頁瀏覽器中開啟CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 選取 `/apps` 資料夾，按一下 **建立>建立節點**.
1. 輸入程式庫資料夾的名稱，並在 **類型** 清單選取 `cq:ClientLibraryFolder`. 按一下 **確定** 然後按一下 **全部儲存**.
1. 若要指定程式庫所屬的類別或類別，請選取 `cq:ClientLibraryFolder` 節點，添加以下屬性，然後按一下 **全部儲存**:
   * 名稱: `categories`
   * 類型：字串
   * 值：類別名稱
   * 多重：已選取
1. 以便透過下方的Proxy存取用戶端程式庫 `/etc.clientlibs`，請選取 `cq:ClientLibraryFolder` 節點，添加以下屬性，然後按一下 **全部儲存**:
   * 名稱: `allowProxy`
   * 類型：布林值
   * 值: `true`
1. 如果您需要管理靜態資源，請建立名為 `resources` 在客戶端庫資料夾下。
   * 如果將靜態資源儲存在資料夾下以外的任何位置 `resources`，則無法在發佈例項上參照。
1. 將源檔案添加到庫資料夾。
   * 這通常是由 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 您可以視需要在子資料夾中組織源檔案。
1. 選擇客戶端庫資料夾，然後按一下 **建立>建立檔案**.
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下「確定」：
   * **`js.txt`:** 使用此檔案名生成JavaScript檔案。
   * **`css.txt`:** 使用此檔案名生成級聯樣式表。
1. 開啟檔案並鍵入以下文本以標識源檔案路徑的根：
   * `#base=*[root]*`
   * 取代 `[root]` 包含源檔案的資料夾路徑（相對於TXT檔案）。 例如，當源檔案與TXT檔案位於同一資料夾時，請使用以下文本：
      * `#base=.`
   * 下列程式碼會將根設定為行動資料夾，名為在 `cq:ClientLibraryFolder` 節點：
      * `#base=mobile`
1. 在下面的行 `#base=[root]`，鍵入源檔案相對根的路徑。 將每個檔案名放在單獨的一行。
1. 按一下 **全部儲存**.

## 提供用戶端程式庫 {#serving-clientlibs}

一旦您的客戶端庫資料夾 [視需要設定，](#creating-clientlib-folders) 您的clientlib可透過proxy來請求。 例如：

* 您的 `/apps/myproject/clientlibs/foo`
* 您的 `/apps/myprojects/clientlibs/foo/resources/icon.png`

此 `allowProxy` 屬性可讓您要求：

* clientlib(透過 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 靜態影像，透過 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 透過HTL載入用戶端程式庫 {#loading-via-htl}

在您的用戶端資料庫成功儲存及管理至其用戶端資料庫資料夾後，即可透過HTL存取。

用戶端程式庫會透過AEM提供的協助程式範本載入，可透過 `data-sly-use`. 此檔案中提供協助程式範本，可透過 `data-sly-call`.

每個 helper 範本都需要 `categories` 選項來參照所需的用戶端程式庫。 這個選項可以是字串值陣列，或是包含逗號分隔值清單的字串。

[請參閱HTL檔案](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 如需透過HTL載入clientlibs的詳細資訊。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 製作與發佈上的用戶端程式庫 {#clientlibs-author-publish}

AEM發佈例項上將需要大部分的clientlib。 也就是說，大部分clientlib的目的都是要產生內容的使用者體驗。 若為發佈例項上的clientlibs, [前端構建工具](#fed-for-aemaacs) 可透過 [客戶端庫資料夾，如上所述。](#creating-clientlib-folders)

不過，有時候可能需要用戶端程式庫來自訂編寫體驗。 例如，自訂對話方塊可能需要將少量CSS或JS部署至AEM製作例項。

### 在作者上管理用戶端程式庫 {#clientlibs-on-author}

如果您需要在作者上使用用戶端程式庫，您可以在 `/apps` 使用與發佈相同的方法，但直接在下方撰寫 `/apps/.../clientlibs/foo` 而不是建立整個專案來管理它。

然後，您可以將用戶端程式庫新增至現成可用的用戶端程式庫類別，以「連結」至編寫JS。

## 偵錯工具 {#debugging-tools}

AEM提供數種工具，用於偵錯和測試用戶端程式庫資料夾。

### 探索用戶端程式庫 {#discover-client-libraries}

此 `/libs/cq/granite/components/dumplibs/dumplibs` 元件生成有關係統上所有客戶端庫資料夾的資訊頁。 此 `/libs/granite/ui/content/dumplibs` 節點將元件作為資源類型。 若要開啟頁面，請使用下列URL（視需要變更主機和連接埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

資訊包括程式庫路徑和類型（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和管道中的程式庫。

### 請參閱生成的輸出 {#see-generated-output}

此 `dumplibs` 元件包含測試選擇器，可顯示為 `ui:includeClientLib` 標籤。 頁面包含不同js、css和主題屬性組合的程式碼。

1. 使用下列其中一種方法開啟「測試輸出」頁面：
   * 從 `dumplibs.html` 頁面，按一下 **按一下這裡進行輸出測試** 文字。
   * 在網頁瀏覽器中開啟下列URL（視需要使用不同的主機和連接埠）:
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 預設頁面顯示沒有類別屬性值之標籤的輸出。
1. 若要查看類別的輸出，請輸入用戶端程式庫的 `categories` 屬性，按一下 **提交查詢**.

## 其他客戶端庫資料夾功能 {#additional-features}

AEM中的用戶端程式庫資料夾支援許多其他功能。 不過，AEMas a Cloud Service並不需要這些參數，因此不鼓勵使用這些參數。 這裡是為了完整性。

>[!WARNING]
>
>AEMas a Cloud Service不需要這些用戶端程式庫資料夾的額外功能，因此不建議使用這些功能。 這裡是為了完整性。

### AdobeGraniteHTMLLiBrary Manager {#html-library-manager}

其他用戶端程式庫設定可透過 **AdobeGraniteHTML程式庫管理員** 的 `https://<host>:<port>/system/console/configMgr`)。

### 其他資料夾屬性 {#additional-folder-properties}

其他資料夾屬性包括允許控制相依性和內嵌，但通常不再需要，也不建議使用：

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。 例如，在 `cq:ClientLibraryFolder` 節點 `F` 和 `G`，若 `F` 需要另一個檔案 `G` 為了正常運作， `categories` of `G` 應該屬於 `dependencies` of `F`.
* `embed`:用於從其他程式庫中內嵌程式碼。 如果節點 `F` 內嵌節點 `G` 和 `H`，產生的HTML會是節點中內容的串連 `G` 和 `H`.

### 連結至相依性 {#linking-to-dependencies}

當用戶端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 此 `ui:includeClientLib` 參考用戶端程式庫資料夾的標籤會導致HTML程式碼包含您產生的程式庫檔案的連結，以及相依性。

相依性必須是其他 `cq:ClientLibraryFolder`. 若要識別相依性，請新增屬性至 `cq:ClientLibraryFolder` 節點（具有以下屬性）:

* **名稱：** 相依性
* **類型：** 字串[]
* **值：** 當前庫資料夾所依賴的cq:ClientLibraryFolder節點的categories屬性的值。

例如， `/etc/clientlibs/myclientlibs/publicmain` 對 `cq.jquery` 程式庫。 參考主要用戶端程式庫的頁面會產生包含下列程式碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫內嵌程式碼 {#embedding-code-from-other-libraries}

您可以將用戶端程式庫的程式碼內嵌至另一個用戶端程式庫。 在執行階段，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

嵌入代碼對於提供對儲存在儲存庫安全區域中的庫的訪問非常有用。

#### 應用程式專屬用戶端程式庫資料夾 {#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在以下其應用程式資料夾中 `/apps`. 也是拒絕網站訪客存取 `/apps` 檔案夾。 若要同時滿足這兩種最佳實務，請在 `/etc` 內嵌用戶端程式庫的資料夾，位於下方 `/apps`.

使用categories屬性來識別要內嵌的用戶端程式庫資料夾。 若要內嵌程式庫，請新增屬性至內嵌 `cq:ClientLibraryFolder` 節點，使用以下屬性：

* **名稱：** 內嵌
* **類型：** 字串[]
* **值：** 類別屬性的值 `cq:ClientLibraryFolder` 要嵌入的節點。

#### 使用內嵌將請求減至最少 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現，您的發佈例項針對一般頁面產生的最終HTML包含相對大量 `<script>` 元素。

在這種情況下，將所有必要的用戶端程式庫程式碼合併到單一檔案中，以減少頁面載入時來回請求的數量，會是很實用的作法。 要執行此操作，您可以 `embed` 使用的內嵌屬性，將必要的程式庫放入應用程式專用的用戶端程式庫中 `cq:ClientLibraryFolder` 節點。

#### CSS檔案中的路徑 {#paths-in-css-files}

內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫 `/etc/client/libraries/myclientlibs/publicmain` 內嵌 `/apps/myapp/clientlib` 用戶端程式庫：

此 `main.css` 檔案包含下列樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

用於 `publicmain` 節點使用原始影像的URL生成包含以下樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 請參閱HTML輸出中的內嵌檔案 {#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌的用戶端程式庫能產生預期的結果，您可以在執行階段查看內嵌的檔案名稱。 若要查看檔案名稱，請附加 `debugClientLibs=true` 參數。 產生的程式庫包含 `@import` 陳述式，而非內嵌程式碼。

在上一個範例中 [從其他程式庫內嵌程式碼](#embedding-code-from-other-libraries) 區段 `/etc/client/libraries/myclientlibs/publicmain` 用戶端程式庫資料夾內嵌 `/apps/myapp/clientlib` 客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟 `publicmain.css` 檔案會顯示下列程式碼：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL:
   * `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下作為連結元素的href提供的連結，以開啟檔案並檢視原始碼。

### 使用前置處理器 {#using-preprocessors}

AEM支援可插拔的前置處理器，並支援 [YUI壓縮機](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) CSS和JavaScript適用的 [Google封閉編譯器(GCC)](https://developers.google.com/closure/compiler/) YUI設為AEM預設預處理器的JavaScript適用的。

可插拔預處理器允許靈活使用，包括：

* 定義可處理指令碼源的指令碼處理器
* 處理器可配置選項
* 處理器可用於縮制，但也可用於非縮制的情況
* clientlib可定義要使用的處理器

>[!NOTE]
>
>依預設，AEM會使用YUI壓縮器。 請參閱 [YUI壓縮程式GitHub檔案](https://github.com/yui/yuicompressor/issues) 以取得已知問題的清單。 切換至特定客戶端的GCC壓縮機可解決使用UI時觀察到的一些問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入用戶端程式庫。 請改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

#### 使用狀況 {#usage}

您可以選擇為每個客戶端庫或系統範圍配置前置處理器配置。

* 新增多值屬性 `cssProcessor` 和 `jsProcessor` 在clientlibrary節點上
* 或者，透過 **HTML程式庫管理員** OSGi配置

clientlib節點上的預處理器配置優先於OSGI配置。

#### 格式和範例 {#format-and-examples}

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### CSS縮制和GCC for JS的YUI壓縮器 {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Typescript以預處理，然後GCC以縮制和模糊化 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### 其他GCC選項 {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有關GCC選項的更多詳細資訊，請參見 [GCC檔案](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### 設定系統預設縮制符 {#set-system-default-minifier}

在AEM中，YUI設為預設縮制碼。 要將此更改為GCC，請執行以下步驟。

1. 前往Apache Felix Config Manager()`http://<host>:<portY/system/console/configMgr`)
1. 尋找和編輯 **AdobeGraniteHTML程式庫管理員**.
1. 啟用 **Minify** 選項（如果尚未啟用）。
1. 設定值 **JS處理器預設配置** to `min:gcc`.
   * 如果以分號分隔，則可傳遞選項，例如 `min:gcc;obfuscate=true`.
1. 按一下 **儲存** 以儲存變更。
