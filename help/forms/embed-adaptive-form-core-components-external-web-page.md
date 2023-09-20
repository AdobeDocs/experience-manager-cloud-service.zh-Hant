---
title: 在外部網頁中內嵌適用性表單
description: 了解如何在外部網頁中嵌入調適型表單
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
source-git-commit: 6d0e3ee08862030e9eb7d068b251d13bc3e8e08f
workflow-type: ht
source-wordcount: '979'
ht-degree: 100%

---


# 根據核心元件將調適性表單內嵌至外部網頁 {#embed-adaptive-form-in-external-web-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | 本文章 |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html) |


你可以[在 AEM Sites 頁面嵌入調適型表單](/help/forms/embed-adaptive-form-aem-sites.md)或在 AEM 外部託管的網頁嵌入調適型表單。嵌入式調適型表單功能齊全，使用者無需離開頁面即可填寫並提交表單。此功能可幫助使用者在網頁維持相關的其他元素，並同時與表單進行互動。

## 先決條件 {#prerequisites}

將調適型表單嵌入外部網站之前執行以下步驟

* 發佈調適型表單，以便被嵌入 AEM Forms 伺服器的發佈執行個體。
* 在您的網站上建立或識別一個網頁，以便託管調適型表單。確保網頁可以[從 CDN 讀取 jQuery 檔案](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)，或者網頁有已嵌入 jQuery 的本機副本。必須有 jQuery 才可呈現調適型表單。
* 當 AEM 伺服器和網頁在不同網域上，請執行這部份所列步驟，[啟用 AEM Forms 為跨網域網站提供調適型表單](#cross-site)。

## 內嵌調適型表單 {#embed-adaptive-form}

您可以在網頁中插入幾行 JavaScript 來嵌入調適型表單。代碼中的 API 會向 AEM 伺服器發送 HTTP 請求以獲得調適型表單資源，並將調適型表單注入指定的表單容器中。

內嵌調適型表單：

1. 使用以下代碼在您的網站上建立網頁：

   ```html
        <!doctype html>
        <html>
          <head>
            <title>This is the title of the webpage!</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
          </head>
          <body>
          <div class="customafsection"/>
            <p>This section is replaced with the adaptive form.</p>
   
         <script>
         var options = {path:"/content/forms/af/myadaptiveform.html", CSS_Selector:".customafsection"};
         alert(options.path);
         var loadAdaptiveForm = function(options){
         //alert(options.path);
            if(options.path) {
                // options.path refers to the path of the adaptive form
                // For Example: /content/forms/af/ABC, where ABC is the adaptive form
                // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
                var path = options.path;
                $.ajax({
                    url  : path ,
                    type : "GET",
                    data : {
                        // wcmmode=disabled is only required for author instance
                        // wcmmode : "disabled"
                    },
                    async: false,
                    success: function (data) {
                        // If jquery is loaded, set the inner html of the container
                        // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not        evaluate the script tag in HTML as per the HTML5 spec
                        // For example: document.getElementById().innerHTML
                        if(window.$ && options.CSS_Selector){
                            // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the        script tag.
                            $(options.CSS_Selector).html(data);
                        }
                    },
                    error: function (data) {
                        // any error handler
                    }
                });
            } else {
                if (typeof(console) !== "undefined") {
                    console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
                }
            }
         }(options);
   
         </script>
          </body>
        </html>
   ```

1. 在嵌入代碼中：

   * *options.path*&#x200B;變數的變更值，以及調適型表單的發佈 URL 路徑。如果 AEM 伺服器在上下文路徑上執行，請確保 URL 包含上下文路徑。一定要提及調適型表單的完整名稱，包括副檔名。例如，上述代碼和調適型表單位在同一個 AEM Forms 伺服器上，因此該範例使用調適型表單 /content/forms/af/locbasic.html 的上下文路徑。
   * CSS_Selector 是所嵌入調適型表單的表單容器 CSS 選擇器。例如，.customafsection css 類是上面範例中的 CSS 選擇器。

調適型表單嵌入網頁中。在嵌入式調適型表單中觀察以下內容：

* 草稿和提交的表單列在表單入口網站的「草稿」和「提交」標籤中。
* 設定在原始調適型表單上的「提交」動作將保留在嵌入式表單中。
* 調適型表單規則保留在嵌入式表單中並完全發揮作用。
* 在原始調適型表單中設定的體驗鎖定目標和 A/B 測試在嵌入式表格中不能使用。
* 如果 Adob&#x200B;&#x200B;e Analytics 設定在原始表單上，則分析資料會在 Adob&#x200B;&#x200B;e Analytics 伺服器中擷取。但是，在 Forms 分析報告中不能使用。
* 在以核心元件為主的調適型表單中，用戶端資料庫 (ClientLibs) 會包含在內，並會連同載入表單的標頭和頁腳元件。因此，當您將以核心元件為主的調適型表單嵌入網頁時，此表單一定會包含表單的標頭和頁腳。

## 範例拓撲 {#sample-topology}

嵌入式調適型表單的外部網頁會發送請求至 AEM 伺服器；伺服器通常位於私人網絡中的防火牆後面。為確保將請求安全導向 AEM 伺刷器，建議設定反向代理伺服器。

我們來看看如何在沒有 Dispatcher 情況下設定 Apache 2.4 反向代理伺服器的範例。在本範例中，您將針對反向代理使用 `/forms` 上下文路徑和映射`/forms` 託管 AEM 伺服器。這可確保將 Apache 伺服器上的 `/forms` 任何請求導向 AEM 執行個體。此拓撲有助在 Dispatcher 層級減少規則數量，因為所有帶有 `/forms`前綴的請求會路由至 AEM 伺服器。

1. 開啟 `httpd.conf` 設定檔案並取消註釋以下代碼行。或者，您可以將這些代碼行加入檔案中。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 將以下代碼行加入 `httpd-proxy.conf` 設定檔案中，以設定代理規則。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   以規則中的 AEM 伺服器發佈 URL 取代 `[AEM_Instance]`。

如果您未將 AEM 侵服器掛載在上下文路徑上，則 Apache 層級的代理規則將如下：

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>如果您設定任何其他拓撲，請確保將提交、預填充和其他 URL 加入 Dispatcher 層級的允許清單。

## 最佳做法 {#best-practices}

將調適型表單嵌入網頁時，請考慮以下最佳做法：

* 確保網頁 CSS 定義的樣式規則與表單物件 CSS 不衝突。為了避免衝突，您可以在使用 AEM 用戶端資料庫的調適型表單主題中重複使用網頁 CSS。有關使用調適型主題的用戶端資料庫資訊，請參閱 [AEM Forms 主題](/help/forms/using-themes-in-core-components.md)。
* 讓網頁中的表單容器使用整個視窗寬度。這樣可確保為行動裝置設定的 CSS 規則可使用，而無需任何變更。如果表單容器未使用整個視窗寬度，則需要編寫自訂 CSS，使表單適用於不同的行動裝置。
* 使用 `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API，取得用戶端以 XML 或 JSON 表示的表單資料。
* 使用 `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API 從 HTML DOM 卸載調適型表單。
* 從 AEM 伺服器發送回應時，設定 access-control-origin 標頭。

## 啟用 AEM Forms 向跨網域的網站提供調適型表單 {#cross-site}

1. 在 AEM 發佈執行個體上，前往 AEM Web 主控台的 Configuration Manager：`https://'[server]:[port]'/system/console/configMgr`。
1. 找到並開啟 **Apache Sling 查閱者篩選器**&#x200B;設定。
1. 在允許的主機欄位中，指定網頁所在的網域。這樣可讓主機向 AEM 伺服器發送 POST 請求。您還可以使用規則運算式來指定一系列的外部應用程式網域。



