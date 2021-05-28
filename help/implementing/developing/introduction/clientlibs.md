---
title: 在AEM上使用用戶端程式庫作為Cloud Service
description: AEM提供用戶端程式庫資料夾，可讓您將用戶端程式碼(clientlibs)儲存在存放庫中、將其組織為類別，以及定義將每個類別的程式碼提供給用戶端的時間和方式
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 0%

---

# 在AEM上使用用戶端程式庫作為Cloud Service{#using-client-side-libraries}

數位體驗嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 AEM用戶端程式庫(clientlibs)可讓您組織這些用戶端程式庫，並集中儲存在存放庫中。 與AEM專案原型中的[前端建置程式結合，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)管理AEM專案的前端程式碼變得簡單。

在AEM中使用clientlib的優點包括：

* 用戶端代碼與所有其他應用程式代碼和內容一樣儲存在儲存庫中
* AEM中的Clientlib可將所有CSS和JS匯總為一個檔案
* 透過可透過[dispatcher](/help/implementing/dispatcher/disp-overview.md)存取的路徑公開clientlibs
* 允許重寫引用的檔案或影像的路徑

Clientlibs是從AEM傳送CSS和Javascript的內建解決方案。

>[!TIP]
>
>為AEM專案建立CSS和Javascript的前端開發人員也應熟悉[AEM專案原型及其自動化前端建置程式。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什麼是用戶端程式庫{#what-are-clientlibs}

網站需要JavaScript和CSS，以及靜態資源（例如圖示和網頁字型），才能在用戶端處理。 clientlib是AEM機制，可參考（若需要，可依類別）並提供這類資源。

AEM會將網站的CSS和Javascript收集到集中位置的單一檔案，以確保HTML輸出中只包含任何資源的一個副本。 這可最大化傳送效率，並允許透過代理在存放庫中集中維護這些資源，以保證存取安全。

## AEM as aCloud Service的前端開發{#fed-for-aemaacs}

所有JavaScript、CSS和其他前端資產都應維護在AEM專案原型的[ui.frontend模組中。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的彈性可讓您使用您所選擇的現代化網頁工具來建立及管理這些資源。

原型隨後可將資源編譯為單一CSS和JS檔案，並自動將其內嵌至存放庫的`cq:clientLibraryFolder`中。

## 用戶端程式庫資料夾結構{#clientlib-folders}

客戶端庫資料夾是`cq:ClientLibraryFolder`類型的儲存庫節點。 其在[CND標籤法](https://jackrabbit.apache.org/node-type-notation.html)中的定義為

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 節點可以放置在存放庫子 `/apps` 樹狀結構內的任何位置。
* 使用節點的`categories`屬性來識別其所屬的程式庫類別。

每個`cq:ClientLibraryFolder`都會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下方）。 `cq:ClientLibraryFolder`的重要屬性配置如下：

* `allowProxy`:由於所有clientlib都必須儲存在下， `apps`因此此屬性可允許透過Proxy servlet存取clientlibraries。請參閱下面的[查找客戶端庫資料夾和使用代理客戶端庫Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。
* `categories`:識別今秋JS和/或CSS檔案集所屬的類 `cq:ClientLibraryFolder` 別。`categories`屬性為多值，可讓程式庫資料夾成為多個類別的一部分（請參閱下方，了解其效用）。

如果用戶端程式庫資料夾包含一或多個執行階段會合併為單一JS和/或CSS檔案的來源檔案。 生成的檔案的名稱是副檔名為`.js`或`.css`的節點名。 例如，名為`cq.jquery`的庫節點會產生名為`cq.jquery.js`或`cq.jquery.css`的生成檔案。

用戶端程式庫資料夾包含下列項目：

* JS和/或CSS來源檔案
* 支援CSS樣式的靜態資源，例如圖示、網頁字型等。
* 一個`js.txt`檔案和/或一個`css.txt`檔案，用於標識要合併到生成的JS和/或CSS檔案中的源檔案

![Clientlib架構](assets/clientlib-architecture.drawio.png)

## 建立客戶端庫資料夾{#creating-clientlib-folders}

客戶端庫必須位於`/apps`下。 這是為了更妥善地將程式碼與內容及設定隔離。

為了存取`/apps`下的用戶端程式庫，需使用代理伺服器。 ACL仍在客戶端庫資料夾上強制執行，但如果`allowProxy`屬性設定為`true`，則servlet允許通過`/etc.clientlibs/`讀取內容。

1. 在網頁瀏覽器中開啟CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 選擇`/apps`資料夾，然後按一下&#x200B;**建立>建立節點**。
1. 輸入庫資料夾的名稱，並在&#x200B;**Type**&#x200B;清單中選擇`cq:ClientLibraryFolder`。 按一下&#x200B;**OK**，然後按一下&#x200B;**Save All**。
1. 要指定庫所屬的類別或類別，請選擇`cq:ClientLibraryFolder`節點，添加以下屬性，然後按一下&#x200B;**保存全部**:
   * 名稱: `categories`
   * 類型：字串
   * 值：類別名稱
   * 多重：已選取
1. 為了讓用戶端程式庫可透過`/etc.clientlibs`下的Proxy存取，請選取`cq:ClientLibraryFolder`節點，新增下列屬性，然後按一下&#x200B;**儲存全部**:
   * 名稱: `allowProxy`
   * 類型：布林值
   * 值: `true`
1. 如果需要管理靜態資源，請在客戶端庫資料夾下建立名為`resources`的子資料夾。
   * 如果將靜態資源儲存在資料夾`resources`下，則無法在發佈執行個體上參照這些資源。
1. 將源檔案添加到庫資料夾。
   * 這通常是由[AEM專案原型的前端建置程式來完成。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 您可以視需要在子資料夾中組織源檔案。
1. 選擇客戶端庫資料夾，然後按一下&#x200B;**建立>建立檔案**。
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下「確定」：
   * **`js.txt`:** 使用此檔案名稱產生JavaScript檔案。
   * **`css.txt`:** 使用此檔案名生成級聯樣式表。
1. 開啟檔案並鍵入以下文本以標識源檔案路徑的根：
   * `#base=*[root]*`
   * 將`[root]`替換為包含源檔案的資料夾的路徑（相對於TXT檔案）。 例如，當源檔案與TXT檔案位於同一資料夾時，請使用以下文本：
      * `#base=.`
   * 下列程式碼會將根設定為`cq:ClientLibraryFolder`節點下方名為mobile的資料夾：
      * `#base=mobile`
1. 在`#base=[root]`下的行中，鍵入源檔案相對於根的路徑。 將每個檔案名放在單獨的一行。
1. 按一下「**全部保存**」。

## 提供用戶端程式庫{#serving-clientlibs}

在根據需要配置客戶端庫資料夾[後，](#creating-clientlib-folders)可以通過代理請求您的客戶端庫。 例如：

* `/apps/myproject/clientlibs/foo`中有clientlib
* `/apps/myprojects/clientlibs/foo/resources/icon.png`中有靜態影像

`allowProxy`屬性可讓您要求：

* 透過j`/etc.clientlibs/myprojects/clientlibs/foo.js`的clientlib
* 透過`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`的靜態影像

### 透過HTL {#loading-via-htl}載入用戶端程式庫

在您的用戶端資料庫成功儲存及管理至其用戶端資料庫資料夾後，即可透過HTL存取。

用戶端程式庫是透過AEM提供的協助程式範本載入，可透過`data-sly-use`存取。 此檔案中提供幫助程式模板，可通過`data-sly-call`調用該模板。

每個幫助程式模板都需要一個`categories`選項來引用所需的客戶端庫。 該選項可以是字串值的陣列，或包含逗號分隔值清單的字串。

[如需透過HTL載](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 入clientlibs的詳細資訊，請參閱HTL檔案。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 製作與發佈上的用戶端程式庫{#clientlibs-author-publish}

AEM發佈例項上將需要大部分的clientlib。 也就是說，大部分clientlib的目的都是要產生內容的使用者體驗。 對於發佈實例上的clientlibs,[前端生成工具](#fed-for-aemaacs)可通過[客戶端庫資料夾使用和部署，如上所述。](#creating-clientlib-folders)

不過，有時候可能需要用戶端程式庫來自訂編寫體驗。 例如，自訂對話方塊可能需要將少量CSS或JS部署至AEM製作例項。

### 在作者{#clientlibs-on-author}上管理用戶端程式庫

如果您需要在作者上使用用戶端程式庫，可以使用與發佈相同的方法在`/apps`下建立用戶端程式庫，但直接在`/apps/.../clientlibs/foo`下撰寫，而不是建立整個專案來管理它。

然後，您可以將用戶端程式庫新增至現成可用的用戶端程式庫類別，以「連結」至編寫JS。

## 調試工具{#debugging-tools}

AEM提供數種工具，用於偵錯和測試用戶端程式庫資料夾。

### 發現客戶端庫{#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`元件生成有關係統上所有客戶端庫資料夾的資訊頁。 `/libs/granite/ui/content/dumplibs`節點將元件作為資源類型。 若要開啟頁面，請使用下列URL（視需要變更主機和連接埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

資訊包括程式庫路徑和類型（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和管道中的程式庫。

### 請參閱生成的輸出{#see-generated-output}

`dumplibs`元件包含測試選擇器，用於顯示為`ui:includeClientLib`標籤生成的原始碼。 頁面包含不同js、css和主題屬性組合的程式碼。

1. 使用下列其中一種方法開啟「測試輸出」頁面：
   * 從`dumplibs.html`頁面，按一下&#x200B;**按一下這裡以輸出測試**&#x200B;文字中的連結。
   * 在網頁瀏覽器中開啟下列URL（視需要使用不同的主機和連接埠）:
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 預設頁面顯示沒有類別屬性值之標籤的輸出。
1. 若要查看類別的輸出，請輸入客戶端庫的`categories`屬性的值，然後按一下&#x200B;**Submit Query**。

## 其他客戶端庫資料夾功能{#additional-features}

AEM中的用戶端程式庫資料夾支援許多其他功能。 不過，AEM作為Cloud Service並不需要這些參數，因此不鼓勵使用這些參數。 這裡是為了完整性。

>[!WARNING]
>
>AEM作為Cloud Service時不需要這些用戶端程式庫資料夾的額外功能，因此不建議使用這些功能。 這裡是為了完整性。

### AdobeGranite HTML庫管理器{#html-library-manager}

可以通過系統控制台的`https://<host>:<port>/system/console/configMgr`面板的&#x200B;**AdobeGranite HTML Library Manager**&#x200B;控制其他客戶端庫設定。

### 其他資料夾屬性{#additional-folder-properties}

其他資料夾屬性包括允許控制相依性和內嵌，但通常不再需要，也不建議使用：

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。例如，給定兩個`cq:ClientLibraryFolder`節點`F`和`G`，如果`F`中的檔案需要`G`中的另一個檔案才能正常工作，則`G`中的`categories`中至少一個應位於`F`的`dependencies`中。
* `embed`:用於從其他程式庫中內嵌程式碼。如果節點`F`嵌入節點`G`和`H`，則生成的HTML將是節點`G`和`H`中內容的串連。

### 連結到依賴項{#linking-to-dependencies}

當用戶端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 參考用戶端程式庫資料夾的`ui:includeClientLib`標籤會使HTML程式碼包含您產生的程式庫檔案的連結，以及相依性。

相依性必須是另一個`cq:ClientLibraryFolder`。 若要識別相依性，請使用下列屬性將屬性新增至您的`cq:ClientLibraryFolder`節點：

* **名稱：** 相依性
* **類型：** 字串[]
* **值：** 目前程式庫資料夾所仰賴之cq:ClientLibraryFolder節點的categories屬性值。

例如， `/etc/clientlibs/myclientlibs/publicmain`與`cq.jquery`庫有相依性。 參考主要用戶端程式庫的頁面會產生包含下列程式碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他庫{#embedding-code-from-other-libraries}嵌入代碼

您可以將用戶端程式庫的程式碼內嵌至另一個用戶端程式庫。 在執行階段，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

嵌入代碼對於提供對儲存在儲存庫安全區域中的庫的訪問非常有用。

#### 應用程式專用客戶端庫資料夾{#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在`/app`以下的應用程式資料夾中。 拒絕網站訪客存取`/app`資料夾也是最佳作法。 要滿足這兩種最佳做法，請在`/etc`資料夾下建立一個客戶端庫資料夾，該資料夾嵌入位於`/app`下的客戶端庫。

使用categories屬性來識別要內嵌的用戶端程式庫資料夾。 若要內嵌程式庫，請使用下列屬性，將屬性新增至內嵌`cq:ClientLibraryFolder`節點：

* **名稱：** 內嵌
* **類型：** 字串[]
* **值：** 要嵌入的節點的categories屬 `cq:ClientLibraryFolder` 性的值。

#### 使用內嵌來最小化請求{#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現，您的發佈例項為一般頁面產生的最終HTML包含相對大量的`<script>`元素。

在這種情況下，將所有必要的用戶端程式庫程式碼合併到單一檔案中，以減少頁面載入時來回請求的數量，會是很實用的作法。 若要這麼做，您可以使用`cq:ClientLibraryFolder`節點的embed屬性，將所需的程式庫`embed`整合至應用程式專用的用戶端程式庫。

#### CSS檔案{#paths-in-css-files}中的路徑

內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫`/etc/client/libraries/myclientlibs/publicmain`內嵌`/apps/myapp/clientlib`用戶端程式庫：

`main.css`檔案包含以下樣式：

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

#### 請參閱HTML輸出{#see-embedded-files}中的內嵌檔案

若要追蹤內嵌程式碼的來源，或確保內嵌的用戶端程式庫能產生預期的結果，您可以在執行階段查看內嵌的檔案名稱。 若要查看檔案名稱，請將`debugClientLibs=true`參數附加至網頁的URL。 產生的程式庫包含`@import`陳述式，而非內嵌程式碼。

在上一個[從其他庫嵌入代碼](#embedding-code-from-other-libraries)部分的示例中， `/etc/client/libraries/myclientlibs/publicmain`客戶端庫資料夾嵌入`/apps/myapp/clientlib`客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟`publicmain.css`檔案會顯示下列程式碼：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL中：
   * `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下作為連結元素的href提供的連結，以開啟檔案並檢視原始碼。

### 使用前置處理器{#using-preprocessors}

AEM支援可插拔的前置處理器，並隨附支援[YUI壓縮器](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)（適用於CSS和JavaScript）和[Google關閉編譯器(GCC)](https://developers.google.com/closure/compiler/)(適用於JavaScript，將YUI設定為AEM預設預處理器)。

可插拔預處理器允許靈活使用，包括：

* 定義可處理指令碼源的指令碼處理器
* 處理器可配置選項
* 處理器可用於縮制，但也可用於非縮制的情況
* clientlib可定義要使用的處理器

>[!NOTE]
>
>依預設，AEM會使用YUI壓縮器。 如需已知問題的清單，請參閱[YUI壓縮機GitHub檔案](https://github.com/yui/yuicompressor/issues)。 切換至特定客戶端的GCC壓縮機可解決使用UI時觀察到的一些問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入用戶端程式庫。 請改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

#### 使用狀況 {#usage}

您可以選擇為每個客戶端庫或系統範圍配置前置處理器配置。

* 在clientlibrary節點上新增多值屬性`cssProcessor`和`jsProcessor`
* 或者，透過&#x200B;**HTML Library Manager** OSGi設定定義系統預設配置

clientlib節點上的預處理器配置優先於OSGI配置。

#### 格式和範例{#format-and-examples}

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### CSS縮制和GCC for JS {#yui-compressor-for-css-minification-and-gcc-for-js}的UI壓縮器

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 鍵入指令碼以預處理，然後GCC到縮制和模糊化{#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

#### 設定系統預設縮制符{#set-system-default-minifier}

在AEM中，YUI設為預設縮制碼。 要將此更改為GCC，請執行以下步驟。

1. 前往(`http://<host>:<portY/system/console/configMgr`)的Apache Felix Config Manager
1. 尋找並編輯&#x200B;**AdobeGranite HTML程式庫管理員**。
1. 啟用&#x200B;**Minify**&#x200B;選項（如果尚未啟用）。
1. 將值&#x200B;**JS處理器預設配置**&#x200B;設定為`min:gcc`。
   * 如果以分號(例如`min:gcc;obfuscate=true`。
1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。
