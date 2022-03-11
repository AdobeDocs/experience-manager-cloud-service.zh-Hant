---
title: 在as a Cloud Service上使用客戶端庫AEM
description: 提AEM供客戶端庫資料夾，這些資料夾允許您將客戶端代碼（客戶端代碼）儲存在儲存庫中，將其組織成類別，並定義將每類代碼提供給客戶端的時間和方式
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 0%

---

# 在as a Cloud Service上使用客戶端庫AEM {#using-client-side-libraries}

數字型驗在很大程度上依賴於由複雜的JavaScript和CSS代碼驅動的客戶端處理。 客AEM戶端庫（客戶端庫）允許您在儲存庫中組織和集中儲存這些客戶端庫。 與 [在項目原型中AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 管理項目的前端代碼AEM變得簡單。

在中使用客戶端的優AEM點包括：

* 客戶端代碼與所有其他應用程式碼和內容一樣儲存在儲存庫中
* 中的客戶端AEM可以將所有CSS和JS聚合到一個檔案中
* 通過可通過以下路徑訪問的路徑公開客戶端 [調度](/help/implementing/dispatcher/disp-overview.md)
* 允許重寫被引用的檔案或影像的路徑

客戶端是用於從中提供CSS和Javascript的內置解決AEM方案。

>[!TIP]
>
>為項目建立CSS和Javascript的前AEM端開發人員也應熟悉 [AEMProject Archetype及其自動前端構建流程。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什麼是客戶端庫 {#what-are-clientlibs}

站點要求在客戶端處理JavaScript和CSS以及靜態資源（如表徵圖和Web字型）。 客戶端庫是AEM參考（如果需要，按類別）和為此類資源提供服務的機制。

將站AEM點的CSS和Javascript收集到一個位於中央位置的單個檔案中，以確保在HTML輸出中只包含任何資源的一個副本。 這將最大限度地提高交付效率，並允許通過代理將此類資源集中維護在儲存庫中，從而保持訪問安全。

## 前端開發，用於AEMas a Cloud Service {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端資產應在 [項目原型的ui.AEMfronted模組。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的靈活性允許您使用您選擇的現代Web工具建立和管理這些資源。

然後，原型可以將資源編譯為單個CSS和JS檔案，並將它們自動嵌入到 `cq:clientLibraryFolder` 的下界。

## 客戶端庫資料夾結構 {#clientlib-folders}

客戶端庫資料夾是類型的儲存庫節點 `cq:ClientLibraryFolder`。 其定義 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html) 是

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 節點可以放在任意位置 `/apps` 儲存庫的子樹。
* 使用 `categories` 用於標識其所屬庫類別的節點的屬性。

每個 `cq:ClientLibraryFolder` 將填充一組JS和/或CSS檔案，以及幾個支援檔案（請參閱下面）。 的重要屬性 `cq:ClientLibraryFolder` 配置如下：

* `allowProxy`:因為所有客戶端必須儲存在 `apps`，此屬性允許訪問客戶端庫代理servlet。 請參閱 [查找客戶端庫資料夾並使用代理客戶端庫Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下。
* `categories`:標識此內的JS和/或CSS檔案集的類別 `cq:ClientLibraryFolder` 摔倒。 的 `categories` 屬性是多值的，它允許庫資料夾成為多個類別的一部分（有關此類別可能有用的資訊，請參閱下面）。

如果客戶端庫資料夾包含一個或多個在運行時合併到單個JS和/或CSS檔案的源檔案。 生成的檔案的名稱是節點名稱，其中 `.js` 或 `.css` 檔案副檔名。 例如，名為 `cq.jquery` 生成名為 `cq.jquery.js` 或 `cq.jquery.css`。

客戶端庫資料夾包含以下項：

* JS和/或CSS源檔案
* 支援CSS樣式的靜態資源，如表徵圖、Web字型等。
* 一 `js.txt` 檔案和/或一個 `css.txt` 標識要合併到生成的JS和/或CSS檔案中的源檔案的檔案

![客戶端庫體系結構](assets/clientlib-architecture.drawio.png)

## 建立客戶端庫資料夾 {#creating-clientlib-folders}

客戶端庫必須位於 `/apps`。 這是為了更好地將代碼與內容和配置隔離開來。

為了在 `/apps` 若要訪問，請使用代理伺服器。 ACL仍在客戶端庫資料夾上強制實施，但Servlet允許通過 `/etc.clientlibs/` 的 `allowProxy` 屬性設定為 `true`。

1. 在Web瀏覽器中開啟CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 選擇 `/apps` 資料夾，按一下 **「建立」>「建立節點」**。
1. 在 **類型** 清單選擇 `cq:ClientLibraryFolder`。 按一下 **確定** 然後按一下 **全部保存**。
1. 要指定庫所屬的類別或類別，請選擇 `cq:ClientLibraryFolder` 節點，添加以下屬性，然後按一下 **全部保存**:
   * 名稱: `categories`
   * 類型：字串
   * 值：類別名稱
   * 多：已選擇
1. 以便客戶端庫可通過代理訪問 `/etc.clientlibs`，選擇 `cq:ClientLibraryFolder` 節點，添加以下屬性，然後按一下 **全部保存**:
   * 名稱: `allowProxy`
   * 類型：布爾型
   * 值: `true`
1. 如果需要管理靜態資源，請建立一個名為 `resources` 位於客戶端庫資料夾下。
   * 如果將靜態資源儲存在資料夾下 `resources`，無法在發佈實例上引用它們。
1. 將源檔案添加到庫資料夾。
   * 這通常由 [原型AEM計畫。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 如果需要，可以在子資料夾中組織源檔案。
1. 選擇客戶端庫資料夾，然後按一下 **建立>建立檔案**。
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下「確定」：
   * **`js.txt`:** 使用此檔案名生成JavaScript檔案。
   * **`css.txt`:** 使用此檔案名可生成級聯樣式表。
1. 開啟檔案並鍵入以下文本以標識源檔案路徑的根：
   * `#base=*[root]*`
   * 替換 `[root]` 與TXT檔案相對的資料夾路徑。 例如，當源檔案與TXT檔案位於同一資料夾中時，請使用以下文本：
      * `#base=.`
   * 以下代碼將根目錄設定為位於以下位置的名為mobile的資料夾 `cq:ClientLibraryFolder` 節點：
      * `#base=mobile`
1. 在下面的行上 `#base=[root]`，鍵入源檔案相對於根目錄的路徑。 將每個檔案名置於單獨的行上。
1. 按一下 **全部保存**。

## 服務客戶端庫 {#serving-clientlibs}

一旦客戶端庫資料夾 [根據需要配置，](#creating-clientlib-folders) 客戶端可通過代理請求。 例如：

* 您在 `/apps/myproject/clientlibs/foo`
* 您在 `/apps/myprojects/clientlibs/foo/resources/icon.png`

的 `allowProxy` 屬性允許您請求：

* 通過j建立客戶端庫`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 靜態映像通過 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 通過HTL載入客戶端庫 {#loading-via-htl}

一旦客戶端在其客戶端庫資料夾中成功儲存和管理，就可以通過HTL訪問它們。

客戶端庫通過由提供的幫助模板加AEM載，可通過 `data-sly-use`。 幫助程式模板在此檔案中可用，可通過 `data-sly-call`。

每個幫助程式模板都需要 `categories` 的子菜單。 該選項可以是字串值的陣列，也可以是包含逗號分隔值清單的字串。

[請參閱HTL文檔](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 的子菜單。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 作者與發佈上的客戶端庫 {#clientlibs-author-publish}

發佈實例上需要大AEM多數客戶端。 也就是說，大多數客戶端的目的是提供內容的最終用戶體驗。 對於發佈實例上的客戶端， [前端構建工具](#fed-for-aemaacs) 可通過 [客戶端庫資料夾，如上所述。](#creating-clientlib-folders)

但有時可能需要客戶端庫來自定義創作體驗。 例如，自定義對話框可能需要將CSS或JS的小位部署到創AEM作實例。

### 在作者上管理客戶端庫 {#clientlibs-on-author}

如果需要在作者中使用客戶端庫，可以在 `/apps` 使用與發佈相同的方法，但直接將其寫入 `/apps/.../clientlibs/foo` 而不是建立整個項目來管理它。

然後，通過將客戶端庫添加到現成的客戶端庫類別中，可以「掛接」到創作JS中。

## 調試工具 {#debugging-tools}

提AEM供了幾種調試和測試客戶端庫資料夾的工具。

### 發現客戶端庫 {#discover-client-libraries}

的 `/libs/cq/granite/components/dumplibs/dumplibs` 元件生成關於系統上所有客戶端庫資料夾的資訊頁面。 的 `/libs/granite/ui/content/dumplibs` 節點將元件作為資源類型。 要開啟該頁，請使用以下URL（根據需要更改主機和埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

該資訊包括庫路徑和類型（CSS或JS）以及庫屬性的值，如類別和依賴項。 該頁上的後續表顯示了每個類別和通道中的庫。

### 請參閱生成的輸出 {#see-generated-output}

的 `dumplibs` 元件包括test選擇器，該選擇器顯示為 `ui:includeClientLib` 標籤。 該頁包括js、css和主題屬性的不同組合的代碼。

1. 使用以下方法之一開啟「Test輸出」頁：
   * 從 `dumplibs.html` 中，按一下 **按一下這裡進行輸出測試** 的子菜單。
   * 在Web瀏覽器中開啟以下URL（根據需要使用其他主機和埠）:
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 預設頁顯示類別屬性沒有值的標籤的輸出。
1. 要查看類別的輸出，請鍵入客戶端庫的 `categories` 屬性，按一下 **提交查詢**。

## 其他客戶端庫資料夾功能 {#additional-features}

中的客戶端庫資料夾支援許多其他功AEM能。 但是，在as a Cloud Service上不AEM需要這些，因此不鼓勵使用。 這裡列出了它們以實現完整性。

>[!WARNING]
>
>as a Cloud Service上不需要客戶端庫資料夾的這些附AEM加功能，因此不鼓勵使用。 這裡列出了它們以實現完整性。

### Adobe花崗岩HTML庫經理 {#html-library-manager}

可以通過 **Adobe花崗岩HTML庫經理** 位於的系統控制檯面板 `https://<host>:<port>/system/console/configMgr`)。

### 其他資料夾屬性 {#additional-folder-properties}

其他資料夾屬性包括允許控制依賴項和嵌入，但通常不再需要這些屬性，也不鼓勵使用它們：

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。 例如，給出兩個 `cq:ClientLibraryFolder` 節點 `F` 和 `G`，如果檔案在 `F` 需要另一個檔案 `G` 為了能正常工作，那麼 `categories` 共 `G` 應該是 `dependencies` 共 `F`。
* `embed`:用於從其他庫中嵌入代碼。 如果節點 `F` 嵌入節點 `G` 和 `H`，生成的HTML將是節點中內容的連接 `G` 和 `H`。

### 連結到依賴項 {#linking-to-dependencies}

當客戶端庫資料夾中的代碼引用其他庫時，將其他庫標識為依賴項。 的 `ui:includeClientLib` 引用客戶端庫資料夾的標籤會導致HTML代碼包含到生成的庫檔案的連結以及依賴關係。

依賴項必須是另一個 `cq:ClientLibraryFolder`。 要確定依賴項，請向 `cq:ClientLibraryFolder` 具有以下屬性的節點：

* **名稱：** 依賴
* **類型：** 字串[]
* **值：** 當前庫資料夾所依賴的cq:ClientLibraryFolder節點的categories屬性的值。

例如， `/etc/clientlibs/myclientlibs/publicmain` 對 `cq.jquery` 的下界。 引用主客戶端庫的頁面生成包含以下代碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他庫中嵌入代碼 {#embedding-code-from-other-libraries}

您可以將代碼從客戶端庫嵌入到另一個客戶端庫。 在運行時，嵌入庫的生成JS和CSS檔案包括嵌入庫的代碼。

嵌入代碼對於提供對儲存在儲存庫的安全區域中的庫的訪問是有用的。

#### 特定於應用的客戶端庫資料夾 {#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在以下應用程式資料夾中 `/app`。 拒絕網站訪問者訪問 `/app` 的子菜單。 要滿足這兩種最佳做法，請在 `/etc` 位於下面的客戶端庫中的資料夾 `/app`。

使用categories屬性標識要嵌入的客戶端庫資料夾。 要嵌入庫，請向嵌入添加屬性 `cq:ClientLibraryFolder` 節點，使用以下屬性屬性：

* **名稱：** 嵌入
* **類型：** 字串[]
* **值：** 的類別屬性的值 `cq:ClientLibraryFolder` 要嵌入的節點。

#### 使用嵌入最小化請求 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現發佈實例為典型頁面生成的最終HTML包含相對大量 `<script>` 元素。

在這種情況下，將所有所需的客戶端庫代碼合併到單個檔案中是非常有用的，因此減少了頁面負載上來回請求的數量。 為此，您可以 `embed` 使用應用程式的embed屬性將所需的庫放入特定於應用程式的客戶端庫 `cq:ClientLibraryFolder` 的下界。

#### CSS檔案中的路徑 {#paths-in-css-files}

嵌入CSS檔案時，生成的CSS代碼使用與嵌入庫相關的資源的路徑。 例如，可公開訪問的庫 `/etc/client/libraries/myclientlibs/publicmain` 嵌入 `/apps/myapp/clientlib` 客戶端庫：

的 `main.css` 檔案包含以下樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS檔案 `publicmain` 節點使用原始影像的URL生成包含以下樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 請參閱HTML輸出中的嵌入檔案 {#see-embedded-files}

要跟蹤嵌入式代碼的源，或確保嵌入式客戶端庫生成預期結果，可以查看運行時嵌入的檔案的名稱。 要查看檔案名，請追加 `debugClientLibs=true` 的URL。 生成的庫包含 `@import` 語句而不是嵌入代碼。

在上一個示例中 [從其他庫中嵌入代碼](#embedding-code-from-other-libraries) 的子菜單。 `/etc/client/libraries/myclientlibs/publicmain` 客戶端庫資料夾嵌入 `/apps/myapp/clientlib` 客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中生成以下連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟 `publicmain.css` 檔案顯示以下代碼：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web瀏覽器的地址框中，將以下文本添加到HTML的URL:
   * `?debugClientLibs=true`
1. 載入頁面時，查看頁面源。
1. 按一下作為連結元素的href提供的連結以開啟檔案並查看原始碼。

### 使用預處理器 {#using-preprocessors}

允AEM許可插拔的預處理器，並支援 [YUI壓縮機](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 用於CSS和JavaScript和 [Google關閉編譯器(GCC)](https://developers.google.com/closure/compiler/) 將UIY設定為預設預AEM處理器的JavaScript。

可插拔預處理器允許靈活使用，包括：

* 定義可處理指令碼源的ScriptProcessor
* 處理器可配置為選項
* 處理器可用於微型化，也可用於非微型化案例
* 客戶端庫可以定義要使用的處理器

>[!NOTE]
>
>預設情況下，AEM使用YUI壓縮程式。 查看 [UIY壓縮程式GitHub文檔](https://github.com/yui/yuicompressor/issues) 清單。 切換到特定客戶端的GCC壓縮器可解決使用UYI時觀察到的一些問題。

>[!CAUTION]
>
>不要在客戶端庫中放置精簡庫。 而是提供原始庫，如果需要進行精簡，則使用預處理器的選項。

#### 使用狀況 {#usage}

您可以選擇按客戶端庫或系統範圍配置預處理器配置。

* 添加多值屬性 `cssProcessor` 和 `jsProcessor` 在客戶端庫節點上
* 或通過 **HTML庫管理器** OSGi配置

客戶端庫節點上的預處理程式配置優先於OSGI配置。

#### 格式和示例 {#format-and-examples}

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### UYI壓縮機用於CSS縮小和GCC用於JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Typescript預處理，然後GCC細化和模糊處理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有關GCC選項的詳細資訊，請參見 [GCC文檔](https://developers.google.com/closure/compiler/docs/compilation_levels)。

#### 設定系統預設迷你器 {#set-system-default-minifier}

UIY在中設定為預設管理符AEM。 要將此更改為GCC，請執行以下步驟。

1. 轉至Apache Felix Config Manager(`http://<host>:<portY/system/console/configMgr`)
1. 查找和編輯 **Adobe花崗岩HTML庫經理**。
1. 啟用 **微型** 選項（如果尚未啟用）。
1. 設定值 **JS處理器預設配置** 至 `min:gcc`。
   * 如果用分號(如 `min:gcc;obfuscate=true`。
1. 按一下 **保存** 的子菜單。
