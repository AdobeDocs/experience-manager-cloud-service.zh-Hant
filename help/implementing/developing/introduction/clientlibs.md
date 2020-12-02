---
title: 在AEM上使用用戶端程式庫做為雲端服務
description: AEM提供「用戶端程式庫檔案夾」，可讓您將用戶端程式碼(clientlibs)儲存在儲存庫中、將它組織成類別，並定義將每個程式碼類別提供給用戶端的時間和方式
translation-type: tm+mt
source-git-commit: d4c031e17c0c83e44b687474502252c89ed37922
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 0%

---


# 在AEM上使用用戶端程式庫做為雲端服務{#using-client-side-libraries}

數位體驗嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 AEM Client-Side Libraries(clientlibs)可讓您組織這些用戶端資料庫並集中儲存在儲存庫中。 再加上AEM Project原型中的[前端建置程式，](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)管理AEM專案的前端程式碼變得簡單。

在AEM中使用clientlibs的優點包括：

* 客戶端代碼與所有其他應用程式碼和內容一樣儲存在儲存庫中
* AEM中的Clientlibs可將所有CSS和JS匯整為一個檔案
* 透過可通過[dispatcher](/help/implementing/dispatcher/disp-overview.md)訪問的路徑來公開clientlibs
* 允許重寫引用檔案或影像的路徑

Clientlibs是內建的解決方案，可從AEM傳送CSS和Javascript。

>[!TIP]
>
>為AEM專案建立CSS和Javascript的前端開發人員也應熟悉[AEM專案原型及其自動化前端建立程式。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什麼是客戶端庫{#what-are-clientlibs}

網站需要JavaScript和CSS，以及靜態資源，例如要在用戶端處理的圖示和網頁字型。 clientlib是AEM的機制，可供參考（視需要依類別）並提供此類資源。

AEM會將網站的CSS和Javascript收集到位於中央位置的單一檔案中，以確保HTML輸出中只包含任何資源的一個副本。 這樣可以最大限度地提高交付效率，並允許通過代理在儲存庫中集中維護這些資源，從而保護訪問安全。

## AEM雲端服務前端開發{#fed-for-aemaacs}

所有JavaScript、CSS和其他前端資產都應維護在AEM專案原型的[ui.frontend模組中。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的彈性可讓您使用您選擇的現代化網頁工具來建立和管理這些資源。

然後，原型可將資源編譯為單個CSS和JS檔案，並將它們自動嵌入儲存庫的`cq:clientLibraryFolder`中。

## 客戶端庫資料夾結構{#clientlib-folders}

客戶端庫資料夾是類型`cq:ClientLibraryFolder`的儲存庫節點。 其在[CND符號中的定義是](https://jackrabbit.apache.org/node-type-notation.html)

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 節點可以放置在儲存庫子 `/apps` 樹內的任意位置。
* 使用節點的`categories`屬性來標識它所屬的庫類別。

每個`cq:ClientLibraryFolder`都會填入一組JS和／或CSS檔案，以及一些支援檔案（請參閱下面）。 `cq:ClientLibraryFolder`的重要屬性配置如下：

* `allowProxy`:由於所有clientlibs都必須儲存在下方， `apps`因此此屬性允許透過proxy servlet存取clientlibraries。請參閱下面的[查找客戶端庫資料夾和使用代理客戶端庫Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。
* `categories`:識別今秋JS和／或CSS檔案集所屬的 `cq:ClientLibraryFolder` 類別。`categories`屬性是多值的，允許庫資料夾屬於多個類別的一部分（請參閱下面以瞭解其可能有何用處）。

如果用戶端程式庫資料夾包含一或多個在執行時期會合併為單一JS和／或CSS檔案的來源檔案。 生成的檔案名是具有`.js`或`.css`檔案名副檔名的節點名。 例如，名為`cq.jquery`的庫節點將生成名為`cq.jquery.js`或`cq.jquery.css`的生成檔案。

客戶端庫資料夾包含以下項目：

* JS和／或CSS來源檔案
* 支援CSS樣式的靜態資源，例如圖示、網頁字型等。
* 一個`js.txt`檔案和／或一個`css.txt`檔案，用以識別要合併到產生的JS和／或CSS檔案中的來源檔案

![Clientlib架構](assets/clientlib-architecture.drawio.png)

## 建立客戶端庫資料夾{#creating-clientlib-folders}

客戶端庫必須位於`/apps`下。 這是為了更好地將程式碼與內容和設定隔離。

為了讓`/apps`下的客戶機庫可以訪問，使用代理伺服器。 ACL仍在客戶端庫資料夾上強制執行，但是，如果`allowProxy`屬性設定為`true`，則servlet允許通過`/etc.clientlibs/`讀取內容。

1. 在網頁瀏覽器(`https://<host>:<port>/crx/de`)中開啟CRXDE Lite。
1. 選擇`/apps`資料夾，然後按一下&#x200B;**建立>建立節點**。
1. 輸入庫資料夾的名稱，並在&#x200B;**類型**&#x200B;清單中選擇`cq:ClientLibraryFolder`。 按一下&#x200B;**確定** ，然後按一下&#x200B;**保存全部**。
1. 要指定庫所屬的類別或類別，請選擇`cq:ClientLibraryFolder`節點，添加以下屬性，然後按一下&#x200B;**保存所有**:
   * 名稱: `categories`
   * 類型：字串
   * 值：類別名稱
   * 多重：已選取
1. 要使客戶端庫可通過`/etc.clientlibs`下的代理訪問，請選擇`cq:ClientLibraryFolder`節點，添加以下屬性，然後按一下&#x200B;**保存所有** :
   * 名稱: `allowProxy`
   * 類型：布林值
   * 值: `true`
1. 如果您需要管理靜態資源，請在客戶端庫資料夾下建立一個名為`resources`的子資料夾。
   * 如果將靜態資源儲存在`resources`資料夾下，則無法在發佈實例上引用這些資源。
1. 將源檔案添加到庫資料夾。
   * 這通常由[AEM Project Archetype的前端建立程式來完成。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 您可視需要在子檔案夾中組織來源檔案。
1. 選擇客戶端庫資料夾，然後按一下「建立」>「建立檔案」**。**
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下確定：
   * **`js.txt`:** 使用此檔案名稱產生JavaScript檔案。
   * **`css.txt`：使** 用此檔案名生成級聯樣式表。
1. 開啟檔案並輸入下列文字，以識別來源檔案路徑的根目錄：
   * `#base=*[root]*`
   * 將`[root]`替換為包含源檔案的資料夾的路徑（相對於TXT檔案）。 例如，當源檔案與TXT檔案位於同一資料夾時，請使用以下文本：
      * `#base=.`
   * 以下代碼將root設定為`cq:ClientLibraryFolder`節點下名為mobile的資料夾：
      * `#base=mobile`
1. 在`#base=[root]`下面的行中，鍵入源檔案相對於根檔案的路徑。 將每個檔案名稱放在單獨的行上。
1. 按一下&#x200B;**保存全部**。

## 服務客戶端庫{#serving-clientlibs}

在根據需要配置客戶端庫資料夾[後，可以通過代理請求您的客戶端庫。 ](#creating-clientlib-folders)例如：

* 您在`/apps/myproject/clientlibs/foo`中有clientlib
* 您的`/apps/myprojects/clientlibs/foo/resources/icon.png`中有靜態影像

`allowProxy`屬性可讓您要求：

* 透過j`/etc.clientlibs/myprojects/clientlibs/foo.js`的clientlib
* 透過`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`的靜態影像

### 透過HTL {#loading-via-htl}載入用戶端程式庫

一旦您的客戶端程式庫成功儲存並管理在其用戶端程式庫資料夾中，就可透過HTL存取。

用戶端程式庫是透過AEM提供的輔助範本載入，可透過`data-sly-use`存取。 此檔案中提供幫助程式模板，可通過`data-sly-call`調用該模板。

每個幫助模板都需要`categories`選項來引用所需的客戶端庫。 該選項可以是字串值陣列或包含逗號分隔值清單的字串。

[如需透過HTL載入](https://docs.adobe.com/content/help/en/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) clientlibs的詳細資訊，請參閱HTL檔案。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 作者與發佈上的用戶端程式庫{#clientlibs-author-publish}

AEM發佈例項上將需要大部分的clientlibs。 也就是說，大部份的clientlibs目的都是要製作內容的使用者體驗。 對於發佈實例上的clientlibs,[前端構建工具](#fed-for-aemaacs)可通過[客戶端庫資料夾使用和部署，如上所述。](#creating-clientlib-folders)

不過，有時可能需要用戶端程式庫來自訂製作體驗。 例如，自訂對話方塊可能需要將CSS或JS的小部份部署至AEM製作例項。

### 在作者{#clientlibs-on-author}上管理客戶端庫

如果您需要在作者上使用用戶端程式庫，可以使用與發佈相同的方法在`/apps`下建立用戶端程式庫，但直接在`/apps/.../clientlibs/foo`下寫入，而不是建立整個專案來管理它。

然後，您可以將用戶端程式庫新增至現成可用的用戶端程式庫類別，以「連結」至編寫JS。

## 調試工具{#debugging-tools}

AEM提供數種工具來除錯和測試用戶端程式庫資料夾。

### Discover客戶端庫{#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`元件生成有關係統上所有客戶端庫資料夾的資訊頁。 `/libs/granite/ui/content/dumplibs`節點將元件作為資源類型。 若要開啟頁面，請使用下列URL（視需要變更主機和連接埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

這些資訊包括程式庫路徑和類型（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和頻道中的程式庫。

### 請參閱生成的輸出{#see-generated-output}

`dumplibs`元件包含測試選擇器，顯示為`ui:includeClientLib`標籤產生的原始碼。 頁面包含js、css和主題屬性不同組合的程式碼。

1. 使用下列其中一種方法來開啟「測試輸出」頁面：
   * 在`dumplibs.html`頁面中，按一下&#x200B;**按一下這裡以輸出測試**&#x200B;文本中的連結。
   * 在網頁瀏覽器中開啟下列URL（視需要使用不同的主機和連接埠）:
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 預設頁面顯示沒有類別屬性值之標籤的輸出。
1. 要查看類別的輸出，請鍵入客戶端庫的`categories`屬性的值，然後按一下&#x200B;**提交查詢**。

## 其他客戶端庫資料夾功能{#additional-features}

AEM中的用戶端資料庫檔案夾支援許多其他功能。 不過，AEM的雲端服務並不需要這些功能，因此不鼓勵使用這些功能。 此處列出它們是為了實現完整性。

>[!WARNING]
>
>AEM上不需要這些「用戶端資料庫檔案夾」的額外功能，因此不建議使用這些功能。 此處列出它們是為了實現完整性。

### Adobe Granite HTML LiBrary Manager {#html-library-manager}

其他用戶端程式庫設定可透過系統主控台（位於`https://<host>:<port>/system/console/configMgr`）的&#x200B;**Adobe Granite HTML Library Manager**&#x200B;面板加以控制。

### 其他資料夾屬性{#additional-folder-properties}

其他資料夾屬性包括允許控制相依性和內嵌式檔案，但通常不再需要，也不建議使用：

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。例如，給定兩個`cq:ClientLibraryFolder`節點`F`和`G`，如果`F`中的檔案需要`G`中的另一個檔案才能正常工作，則`G`的`categories`中至少一個應位於`F`的`dependencies`中。
* `embed`:用於從其他程式庫內嵌程式碼。如果節點`F`嵌入節點`G`和`H`，則生成的HTML將是節點`G`和`H`中內容的串連。

### 連結至相依項{#linking-to-dependencies}

當用戶端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 引用用戶端程式庫資料夾的`ui:includeClientLib`標籤會使HTML程式碼包含您所產生程式庫檔案的連結以及相依性。

相依性必須是另一個`cq:ClientLibraryFolder`。 要標識相依性，請向`cq:ClientLibraryFolder`節點添加具有以下屬性的屬性：

* **名稱：相** 依性
* **類型：字** 串[]
* **值：目** 前程式庫資料夾所依賴之cq:ClientLibraryFolder節點的categories屬性值。

例如，`/etc/clientlibs/myclientlibs/publicmain`與`cq.jquery`庫有相關性。 參考主用戶端程式庫的頁面會產生包含下列程式碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫{#embedding-code-from-other-libraries}內嵌程式碼

您可以將用戶端程式庫的程式碼內嵌至另一個用戶端程式庫。 在執行時期，內嵌程式庫產生的JS和CSS檔案包含內嵌程式庫的程式碼。

嵌入代碼對於提供對儲存在儲存庫的安全區域中的庫的訪問非常有用。

#### 應用程式特定用戶端程式庫資料夾{#app-specific-client-library-folders}

將所有應用程式相關檔案保留在其應用程式資料夾`/app`下方是最佳實務。 此外，拒絕網站訪客存取`/app`資料夾也是最佳做法。 為滿足這兩種最佳做法，請在`/etc`資料夾下建立一個客戶端庫資料夾，該資料夾嵌入`/app`以下的客戶端庫。

使用categories屬性來識別要內嵌的用戶端程式庫資料夾。 要嵌入庫，請使用以下屬性屬性將屬性添加到嵌入`cq:ClientLibraryFolder`節點：

* **名稱：** embed
* **類型：字** 串[]
* **值：** 要嵌入的節點的類別屬 `cq:ClientLibraryFolder` 性的值。

#### 使用內嵌功能將要求減至最少{#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現，您的發佈例項為典型頁面產生的最終HTML包含相對大量的`<script>`元素。

在這種情況下，將所有必要的用戶端程式庫程式碼結合到單一檔案中，以減少頁面載入時的來回請求數，是很有用的。 若要這麼做，您可以使用`cq:ClientLibraryFolder`節點的embed屬性，將所需的程式庫`embed`放入應用程式專用的用戶端程式庫。

#### CSS檔案{#paths-in-css-files}中的路徑

當您內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫`/etc/client/libraries/myclientlibs/publicmain`內嵌於`/apps/myapp/clientlib`用戶端程式庫：

`main.css`檔案包含下列樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain`節點生成的CSS檔案使用原始影像的URL包含以下樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 請參閱「HTML輸出中的內嵌檔案{#see-embedded-files}」

若要追蹤內嵌程式碼的來源，或確保內嵌用戶端程式庫產生預期的結果，您可以在執行時期看到內嵌的檔案名稱。 若要查看檔案名稱，請將`debugClientLibs=true`參數附加至網頁的URL。 產生的程式庫包含`@import`陳述式，而非內嵌程式碼。

在上一個[從其他庫嵌入代碼](#embedding-code-from-other-libraries)部分的示例中，`/etc/client/libraries/myclientlibs/publicmain`客戶端庫資料夾嵌入`/apps/myapp/clientlib`客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟`publicmain.css`檔案會顯示下列程式碼：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL:
   * `?debugClientLibs=true`
1. 頁面載入時，請檢視頁面來源。
1. 按一下作為連結元素href提供的連結，以開啟檔案並檢視原始碼。

### 使用預處理器{#using-preprocessors}

AEM允許可插拔的預處理器，並隨附支援[UYI Plaxporator](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)的CSS和JavaScript以及[Google Closure Compiler(GCC)](https://developers.google.com/closure/compiler/)的JavaScript，而UI已設定為AEM的預處理器。

可插拔的預處理器允許靈活使用，包括：

* 定義可處理指令碼源的指令碼處理器
* 處理器可配置選項
* 處理器可用於微型化，但也可用於非微型化的情況
* clientlib可以定義要使用哪個處理器

>[!NOTE]
>
>依預設，AEM會使用UYI壓縮器。 有關已知問題的清單，請參見[UYI壓縮機GitHub文檔](https://github.com/yui/yuicompressor/issues)。 切換至特定客戶端的GCC壓縮機可解決使用UY時觀察到的一些問題。

>[!CAUTION]
>
>請勿將精簡的程式庫放在用戶端程式庫中。 請改為提供原始程式庫，如果需要精簡，請使用預處理器的選項。

#### 使用狀況 {#usage}

您可以選擇根據客戶端庫或整個系統配置預處理器配置。

* 在clientlibrary節點上添加多值屬性`cssProcessor`和`jsProcessor`
* 或者，透過&#x200B;**HTML Library Manager** OSGi組態定義系統預設組態

clientlib節點上的預處理器配置優先於OSGI配置。

#### {#format-and-examples}格式與範例

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### UYI壓縮器，用於CSS精簡化和GCC for JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 鍵入「預處理」，然後「GCC」，將「GCC」輸入為「最小化」和「模糊化」{#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### 其他GCC選項{#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有關GCC選項的詳細資訊，請參見[GCC文檔](https://developers.google.com/closure/compiler/docs/compilation_levels)。

#### 設定系統預設管理器{#set-system-default-minifier}

UYI在AEM中設為預設微調字元。 要將此更改為GCC，請執行以下步驟。

1. 前往Apache Felix Config Manager(`http://<host>:<portY/system/console/configMgr`)
1. 尋找並編輯&#x200B;**Adobe Granite HTML Library Manager**。
1. 啟用&#x200B;**Minify**&#x200B;選項（如果尚未啟用）。
1. 將值&#x200B;**JS處理器預設配置**&#x200B;設定為`min:gcc`。
   * 若以分號(例如`min:gcc;obfuscate=true`。
1. 按一下&#x200B;**保存**&#x200B;保存更改。
