---
title: 在外部網頁中內嵌適用性表單
description: 瞭解如何將最適化表單內嵌在外部網頁中
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
source-git-commit: 6d0e3ee08862030e9eb7d068b251d13bc3e8e08f
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 2%

---


# 根據核心元件將最適化表單內嵌到外部網頁 {#embed-adaptive-form-in-external-web-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | 本文章 |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html) |


您可以 [將調適型表單內嵌到AEM Sites頁面中](/help/forms/embed-adaptive-form-aem-sites.md) 或託管於AEM外部的網頁。 內嵌的最適化表單功能齊全，使用者無須離開頁面即可填寫並提交表單。 它有助於使用者停留在網頁上其他元素的內容中，同時與表單互動。

## 先決條件 {#prerequisites}

將最適化表單內嵌至外部網站之前，請先執行下列步驟

* 發佈要內嵌至AEM Forms伺服器發佈例項的最適化表單。
* 在您的網站上建立或識別要託管最適化表單的網頁。 確保網頁可以 [從CDN讀取jQuery檔案](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 或內嵌jQuery的本機副本。 需要jQuery才能演算最適化表單。
* 當AEM伺服器和網頁位於不同的網域時，請執行區段中列出的步驟， [讓AEM Forms能夠為跨網域網站提供最適化表單](#cross-site).

## 內嵌最適化表單 {#embed-adaptive-form}

您可以在網頁中插入幾行JavaScript，以內嵌最適化表單。 程式碼中的API會傳送HTTP請求給AEM伺服器以取得調適型表單資源，並將調適型表單插入指定的表單容器中。

若要內嵌調適型表單：

1. 使用以下程式碼在您的網站上建立網頁：

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

1. 在內嵌程式碼中：

   * 變更的值 *options.路徑* 變數，搭配最適化表單的發佈URL路徑。 如果AEM伺服器是在內容路徑上執行，請確定URL包含內容路徑。 一律提及最適化表單的完整名稱，包括擴充功能。   例如，上述程式碼和調適型來自位於同一個AEM表單伺服器上，因此此範例使用調適型表單/content/forms/af/locbasic.html的內容路徑。
   * CSS_Selector為內嵌最適化表單之表單容器的CSS選取器。 例如，.customafsection css類別是上述範例中的CSS選取器。

最適化表單已內嵌在網頁中。 在內嵌的最適化表單中觀察下列事項：

* 您可在Forms入口網站的「草稿與提交」索引標籤中取得草稿與已提交的表單。
* 在原始最適化表單上設定的提交動作會保留在內嵌表單中。
* 最適化表單規則會保留，並完整發揮內嵌表單的功能。
* 在原始最適化表單中設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。
* 如果在原始表單上設定Adobe Analytics，則會在Adobe Analytics伺服器中擷取分析資料。 但是，Forms分析報表中並未提供此函式。
* 在基於核心元件的調適型Forms中，使用者端資料庫(ClientLibs)會與表單的頁首和頁尾元件一起包含和載入。 因此，當您根據核心元件嵌入最適化Forms至網頁時，其中一律包含表單的頁首和頁尾。

## 範例拓撲 {#sample-topology}

內嵌最適化表單的外部網頁會將請求傳送至AEM伺服器，該伺服器通常位於私人網路的防火牆之後。 為確保將請求安全地導向至AEM伺服器，建議設定反向Proxy伺服器。

讓我們來看一個範例，瞭解如何在不使用Dispatcher的情況下設定Apache 2.4反向Proxy伺服器。 在此範例中，您會以代管AEM伺服器 `/forms` 內容路徑與地圖 `/forms` 用於反向Proxy。 這可確保針對以下專案的任何請求： `/forms` Apache伺服器上的會導向至AEM執行個體。 此拓撲有助於減少Dispatcher層上的規則數量，因為所有請求都有前置詞 `/forms` 路由至AEM伺服器。

1. 開啟 `httpd.conf` 設定檔案並取消註解下列幾行程式碼。 或者，您可以在檔案中新增這些行程式碼。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 將下列幾行程式碼新增至 `httpd-proxy.conf` 組態檔。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   取代 `[AEM_Instance]` 在規則中設定AEM伺服器發佈URL。

如果您未在內容路徑上掛載AEM伺服器，Apache層的Proxy規則將如下所示：

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
>如果您設定任何其他拓撲，請確定您將提交、預填和其他URL新增到Dispatcher層的允許清單。

## 最佳實務 {#best-practices}

將最適化表單內嵌在網頁中時，請考慮下列最佳實務：

* 請確保網頁CSS中定義的樣式規則不會與表單物件CSS衝突。 若要避免衝突，您可以使用AEM使用者端資料庫，重複使用最適化表單主題中的網頁CSS。 如需有關在最適化表單主題中使用使用者端資料庫的資訊，請參閱 [AEM Forms中的主題](/help/forms/using-themes-in-core-components.md).
* 讓網頁中的表單容器使用整個視窗寬度。 這可確保為行動裝置設定的CSS規則可在沒有任何變更的情況下運作。 如果表單容器未採用完整的視窗寬度，您需要撰寫自訂CSS，讓表單能適應不同的行動裝置。
* 使用 `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` 用於取得使用者端中表單資料的XML或JSON表示的API。
* 使用 `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API可從HTMLDOM解除安裝調適型表單。
* 設定從AEM伺服器傳送回應時的存取控制來源標頭。

## 啟用AEM Forms以向跨網域網站提供最適化表單 {#cross-site}

1. 在AEM發佈執行個體上，前往AEM Web主控台設定管理員，位於 `https://'[server]:[port]'/system/console/configMgr`.
1. 找到並開啟 **Apache Sling查閱者篩選器** 設定。
1. 在允許的主機欄位中，指定網頁所在的網域。 這可讓主機向AEM伺服器發出POST要求。 您也可以使用規則運算式來指定一系列外部應用程式網域。



