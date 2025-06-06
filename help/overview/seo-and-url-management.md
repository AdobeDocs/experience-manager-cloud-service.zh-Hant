---
title: Adobe Experience Manager as a Cloud Service 的 SEO 和 URL 管理最佳作法
description: Adobe Experience Manager as a Cloud Service 的 SEO 和 URL 管理最佳作法
exl-id: abe3f088-95ff-4093-95a1-cfc610d4b9e9
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 的 SEO 和 URL 管理最佳作法{#seo-and-url-management-best-practices-for-aem}

搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，在許多 Adobe Experience Manager (AEM) as a Cloud Service 專案中，SEO 考量都是需要解決的問題。

本文件首先會說明在 AEM as a Cloud Service 實作中達成上述目標的幾項 [SEO 最佳作法](#seo-best-practices)與建議。接著，本文件會於第一節中再深入探討幾項更[複雜的實作步驟](#aem-configurations)。

## SEO 最佳做法 {#seo-best-practices}

本節說明幾項一般 SEO 最佳做法。

### URL {#urls}

URL 中有一些公認的最佳做法。

在評估 AEM 專案的 URL 時，請先自問以下問題：

*「使用者能在尚未過目任何網頁內容之下，光是看到此 URL 就能描述頁面內容嗎？」*

如果答案是可以，則此 URL 在搜尋引擎中很可能成效良好。

以下為幾項針對 SEO 建構 URL 的常見訣竅：

* 使用連字號來分隔字詞。

   * 請將連字號當作分隔符號來命名網頁。
   * 避免使用駝峰式大小寫、底線和空格。

* 可行的話，避免使用查詢參數。如需使用，請不要超過兩個。

   * 如果可用，請使用目錄結構來指示資訊架構。
   * 如果無法使用目錄結構，請在 URL 中使用 Sling 選擇器，而非查詢字串。除了可提供 SEO 值，Sling 選擇器也會使網頁可供 Dispatcher 快取。

* URL 越容易透過字面理解越好；如果 URL 中存在關鍵字，SEO 值會大幅提升。

   * 在網頁上使用選擇器時，建議使用提供語意值的選取器。
   * 如果使用者無法透過字面理解您的 URL，則搜尋引擎也無法。
   * 例如：
     `mybrand.com/products/product-detail.product-category.product-name.html`
比 `mybrand.com/products/product-detail.1234.html` 更適合

* 盡可能避免子網域，因為搜尋引擎會將子網域視為不同的實體，進而分割網站的 SEO 值。

   * 請使用第一層子路徑。舉例來說，請避免使用 `es.mybrand.com/home.html`，改用 `www.mybrand.com/es/home.html`。

   * 請根據本指引規劃內容階層，以便符合內容呈現方式。

* URL 的長度和關鍵字的位置增加，URL 中關鍵字的有效性就會降低。換句話說，URL 越短越好。

   * 請使用 AEM 提供的 URL 縮短技術和功能來移除不必要的 URL 片段。
   * 舉例來說，`mybrand.com/en/myPage.html` 比 `mybrand.com/content/my-brand/en/myPage.html` 更適合。

* 使用標準 URL。

   * 如果 URL 可從不同路徑或透過不同參數或選擇器運作，請務必在網頁上使用 `rel=canonical` 標籤。

   * 此標籤可納入 AEM 範本的程式碼中。

* 盡可能使 URL 與網頁標題相符。

   * 建議內容作者遵循這項作法。

* 支援在 URL 要求中不區分大小寫。

   * 將 Dispatcher 設定為將所有傳入要求重新寫入為小寫字母。
   * 請訓練內容作者使用小寫字母來建立所有網頁。

* 每個網頁都必須只經由一個通訊協定來提供。

   * 有時，網站會透過 `http` 提供，直到使用者以結帳或登入形式抵達網頁後，才會切換為透過 `https` 提供。從這個頁面連結時，如果使用者可返回 `http` 頁面並透過 `https` 存取，搜尋引擎會將這些頁面當成兩個獨立頁面來追蹤。

   * 目前 Google 偏好使用 `https` 頁面，而非 `http` 頁面。因為這個原因，透過 `https` 提供整個網站通常才能讓每個人的生活更便利。

### 伺服器設定 {#server-configuration}

進行伺服器設定時，您可以執行下列步驟，確保系統只對正確的內容進行編目：

* 使用 `robots.txt` 檔案來阻止系統對任何不應納入索引的內容進行編目。

   * 封鎖測試環境上的&#x200B;**所有**&#x200B;編目動作。

* 如果要啟動的新網站有更新過的 URL，請實作 301 重新導向，確保現有的 SEO 排名不會遺失。
* 加入您網站的 Favicon。
* 實作 XML Sitemap，讓搜尋引擎更容易對您的內容進行編目。請務必加入行動 Sitemap 供行動及/或回應式網站使用。

## AEM 設定 {#aem-configurations}

本節說明設定 AEM 的所需實作步驟，以便遵循上述 SEO 建議。

### 使用 Sling 選擇器 {#using-sling-selectors}

過去，業界在建置企業 Web 應用程式時普遍使用查詢參數。

近年來的趨勢是移除這些查詢參數，以便 URL 更具可讀性。在許多平台上，這種趨勢包括在網頁伺服器或內容傳遞網路 (CDN) 上實作重新導向，但 Sling 可讓這項作業變得簡單明瞭。Sling 選擇器：

* 改善 URL 可讀性。
* 讓您在 Dispatcher 上對網頁進行快取，且通常可提高安全性。
* 您可以直接處理內容，而不是採用一般 servlet 來擷取內容。此特性可讓您將 ACL 的優勢應用在存放庫，並將篩選器應用在 Dispatcher。

#### 針對 servlet 使用選擇器 {#using-selectors-for-servlets}

AEM 提供兩種編寫 servlet 的選項：

* **bin** servlet
* **Sling** servlet

下列範例說明如何註冊同時符合以下兩種模式的 servlet，以及使用 Sling servlet 所獲的益處。

#### Bin servlet (向下一個層級) {#bin-servlets-one-level-down}

**Bin** servlet 符合許多開發人員在 J2EE 程式設計中慣用的模式。Servlet 會註冊於特定路徑，這種情況下 AEM 通常位於 `/bin` 下，而您必須從查詢字串擷取所需要求參數。

此類 servlet 的 SCR 注釋如下所示：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

您接著會透過 `doGet` 方法中所包含的 `SlingHttpServletRequest` 物件從查詢字串中擷取參數；舉例來說：

```
String myParam = req.getParameter("myParam");
```

最後產生的所用 URL 如下所示：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

採用這種方法需要考量以下幾點：

* URL 本身會遺失 SEO 值。存取網站 (包括搜尋引擎) 的使用者不會從 URL 收到任何語意值，因為 URL 代表程式設計路徑，而非內容階層。
* URL 中存在查詢參數，代表 Dispatcher 將無法對回應進行快取。
* 如果要保護此 servlet 的安全，您需要在 servlet 中實作自己的自訂安全邏輯。
* Dispatcher 必須經過審慎設定以公開 `/bin/myApp/myServlet`。僅公開 `/bin`，會使網站訪客可存取不應向他們開放的特定 servlet。

#### Sling servlet (向下一個層級) {#sling-servlets-one-level-down}

**Sling** servlet 可讓您以相反的方式註冊 servlet。您不需要指定 servlet 位址並指定要讓 servlet 根據查詢參數轉譯的內容，僅需指出您想要的內容，並指定應根據 Sling 選擇器轉譯內容的 servlet。

此類 servlet 的 SCR 注釋如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

在這種情況下，URL 所處理的資源 (`myPageType` 資源的執行個體) 可在 servlet 中自動供訪客存取。如要存取該資源，請呼叫：

```
Resource myPage = req.getResource();
```

最後產生的所用 URL 如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

此方法的優點包括：

* 您可以控制經由網站階層和網頁名稱中所呈現語意而獲得的 SEO 值。
* 由於不存在查詢參數，因此 Dispatcher 可以對回應進行快取。此外，已定址網頁一經啟用，對該網頁所做的任何更新都會使這個快取失效。
* 如有使用者嘗試存取此 servlet，套用到 `/content/my-brand/my-page` 的所有 ACL 都會生效。
* Dispatcher 將會已預先設定為將此內容當作為網站供應內容的函式來提供。無需額外設定。

### URL 重新寫入 {#url-rewriting}

在 AEM 中，所有網頁都儲存在下方 `/content/my-brand/my-content`。雖然從存放庫資料管理的角度來看，這樣的設定很實用，但卻未必是您希望客戶看到網站的方式，而且可能與 SEO 指導方針有衝突，不符合盡可能縮短 URL 的原則。此外，您可能會從同一個 AEM 執行個體及不同網域名稱為多個網站供應內容。

本節將說明在 AEM 管理這些 URL 並且以更容易從字面理解的 SEO 建議方法向使用者呈現的可用選項。

#### 虛名 URL {#vanity-urls}

如果作者為了推銷目的而想要讓某個網頁可從第二個位置存取，採用以逐頁方式定義的 AEM 虛名 URL 也許是個好方法。若要新增網頁的虛名 URL，請在&#x200B;**網站**&#x200B;控制台導覽至該頁面，並編輯頁面屬性。在&#x200B;**基本**&#x200B;標籤底部，您會看到可新增虛名 URL 的區段。別忘了，如果某個網頁可透過多個 URL 存取，該頁的 SEO 值就會遭到分割，因此您應將標準 URL 標記新增至該頁才能避免此問題。

#### 本地化的網頁名稱 {#localized-page-names}

建議向翻譯內容的使用者顯示本地化的網頁名稱。例如：

* 與其讓講西班牙語的使用者導覽至：
  `www.mydomain.com/es/home.html`

* 建議讓 URL 顯示為：
  `www.mydomain.com/es/casa.html`。

本地化網頁名稱時會面對的困難是，許多 AEM 平台上可用的本地化工具都需要不同位置的網頁有相符的名稱，才能讓內容保持同步。

`sling:alias` 屬性讓您不僅看得到好處，也享用得到。您可以在任何資源中將 `sling:alias` 新增為屬性，允許資源使用別名。在上一個範例中：

* 原本在 JCR 的網頁是：
  `…/es/home`

* 新增屬性後變成：
  `sling:alias` = `casa`

這樣一來，AEM 翻譯工具 (例如多網站管理員) 就能繼續維護以下兩者的關聯性：

* `/en/home`

* `/es/home`

同時允許使用者以自己的原生語言與網頁名稱互動。

>[!NOTE]
>
>[在編輯網頁屬性時，您可使用別名屬性](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)來設定 `sling:alias` 屬性。

#### /etc/map {#etc-map}

在標準的 AEM 配置中：

* OSGi 設定為
  **Apache Sling Resource Resolver Factory**
( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 屬性為
  **對應位置** ( `resource.resolver.map.location`)

* 預設為 `/etc/map`。

您可以在此位置新增對應定義，以便對應傳入要求、重新寫入 AEM 中的網頁 URL，或兩者皆執行。

如要建立對應，則在此位置的 `sling:Mapping` 或 `/http` 之下建立 `/https` 節點。AEM 會根據設定在此節點上的 `sling:match` 和 `sling:internalRedirect` 屬性，將相符 URL 的所有流量重新導向至在 `internalRedirect` 屬性指定的值。

雖然上述方法已記錄在官方 AEM 和 Sling 文件中，但與直接使用 `SlingResourceResolver` 時的可用選項相比，這種實作方法支援的規則運算式卻範圍有限。此外，以這種方式實作對應可能會導致 Dispatcher 快取失效的問題。

以下是此問題發生的例子：

1. 使用者造訪您的網站並要求 `https://www.mydomain.com/my-page.html`
1. Dispatcher 將此要求轉發到發佈伺服器。
1. 發佈伺服器使用 `/etc/map` 將此要求解析到 `/content/my-brand/my-page`，並呈現網頁。

1. Dispatcher 在 `/my-page.html` 對回應進行快取，並將回應回傳給使用者。
1. 內容作者變更並啟動此頁面。
1. Dispatcher 排清代理程式傳送 `/content/my-brand/my-page`**的無效要求。** 由於 Dispatcher 在此路徑上沒有經過快取的網頁，因此系統會維持對舊內容進行快取，導致內容過時。

有些方法可以設定自訂發送排清規則，針對快取失效將較短的 URL 對應至較長的 URL。

不過，另外也有更簡單的方法可用於管理這個問題：

1. **SlingResourceResolver 規則**

   您可以使用 Web 控制台 (例如 localhost:4502/system/console/configMgr) 設定 Sling Resource Resolver：

   * **Apache Sling Resource Resolver Factory**
     `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。

   建議您建置所需對應來將 URL 縮短為規則運算式，然後在包含在您所建置項目的 OsgiConfignode `config.publish` 下定義這些設定。

   您不必在 `/etc/map` 定義對應，因為這些對應可以直接指派給屬性&#x200B;**URL 對應** ( `resource.resolver.mapping`)：

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在這個簡單範例中，您會從任何存在 `/content/my-brand/` 的 URL 開頭中將之移除。

   於是 URL 會：

   * 從 `/content/my-brand/my-page.html`
   * 轉換成 `/my-page.html`

   這個結果就符合將 URL 盡量縮短的建議做法。

1. **在網頁上對應 URL 輸出**

   在 Apache Sling Resource Resolver 中定義對應後，您必須在元件中使用這些對應，確保您輸出在網頁上的 URL 簡短且整齊。您可以使用 `ResourceResolver` 的對應函式來完成此操作。

   舉例來說，如果您要實作一項自訂導覽元件來列出目前頁面的子項，則可使用如下對應方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

至此，您已與元件中的邏輯一併實作完成對應，以便在將 URL 輸出至頁面時使用這些對應。

最後一個步驟，就是在這些縮短的 URL 進入 `mod_rewrite` 會發揮作用的 Dispatcher 時處理這些 URL。使用 `mod_rewrite` 的最大優點，就是 URL 在傳送到 Dispatcher 模組&#x200B;*之前*&#x200B;會先重新對應到原本的較長格式。也就是說，Dispatcher 會從發佈伺服器要求長 URL 並加以進行快取。因此，任何來自發佈伺服器的 Dispatcher 排清都可以成功使該內容無效。

要實作這些規則，您可以在 Apache HTTP 伺服器設定的虛擬主機下新增 `RewriteRule` 元素。如果您想要拉長上個範例中縮短的 URL，則可實作如下規則：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 標準 URL 標記 {#canonical-url-tags}

標準 URL 標記是放置在 HTML 文件開頭的連結標記，可釐清搜尋引擎在建立內容索引時應如何處理網頁。它們可帶來的好處是，即使連向網頁的 URL 可能有些差異，也可確保系統對其他版本的網頁建立相同索引。

舉例來說，如果網站想要提供適合列印的網頁版本，搜尋引擎可能會對此版本與一般版本分開建立索引。但標準標記會告訴搜尋引擎兩者是相同版本。

範例：

* `<https://www.mydomain.com/my-brand/my-page.html>`
* `<https://www.mydomain.com/my-brand/my-page.print.html>`

兩者都會在網頁開頭套用下列標籤：

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

`href` 可以是相對或絕對的值。程式碼應包含在網頁標記中，以便判斷網頁的標準 URL 並輸出此標籤。

### 將 Dispatcher 設定為不區分大小寫 {#configuring-the-dispatcher-for-case-insensitivity}

使用小寫字母來提供所有網頁是建議的最佳作法。但是，您也不應讓使用者在 URL 中輸入大寫字母來存取網站時，收到 404 錯誤訊息。因此，Adobe 建議您在 Apache HTTP 伺服器設定中新增重新寫入規則，以便將所有傳入的 URL 對應至小寫。此外，內容作者必須接受訓練以小寫名稱建立網頁。

如要設定 Apache 以強制所有轉入流量都轉換為小寫，請將以下內容新增到 `vhost` 設定中：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，將下列內容新增至 `htaccess` 檔案的最上方：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 實作 robots.txt 以保護開發環境 {#implementing-robots-txt-to-protect-development-environments}

搜尋引擎在對網站進行編目之前，*必須*&#x200B;先檢查網站根中是否有 `robots.txt` 檔案。雖然 Google、Yahoo 或 Bing 等主流搜尋引擎都會這麼做，但有些外國搜尋引擎卻並不如此。

封鎖使用者存取整個網站的最簡單方式，是將名為 `robots.txt` 的檔案置於網站根中，且含有以下內容：

```xml
User-agent: *
Disallow: /
```

或者，您可以在即時環境中選擇不允許某些不希望建立索引的路徑。

將 `robots.txt` 檔案置於網站根時應注意，Dispatcher 排清要求可能會清除此檔案，且 URL 對應可能會將網站根置於與 Apache HTTP 伺服器設定中已定義的 `DOCROOT` 不同之處。因此，常見的方式是將此檔案放置在網站根目的編寫執行個體上，並複製到發佈執行個體。

### 在 AEM 上建置 XML Sitemap {#building-an-xml-sitemap-on-aem}

編目程式可透過 XML Sitemap 加強瞭解網站的結構。雖然提供 Sitemap 並不保證可改善 SEO 排名，但這是一項普遍採用的最佳做法。您可以手動在網頁伺服器上維護 XML 檔案，以便將它當作 Sitemap 使用，但建議以程式設計方式產生 Sitemap，確保當作者建立內容時，Sitemap 會自動反映變更。

AEM 使用 [Apache Sling Sitemap 模組](https://github.com/apache/sling-org-apache-sling-sitemap)產生 XML Sitemap，這為開發人員和編輯人員提供了廣泛的選項，使網站 XML Sitemap 保持最新。

Apache Sling Sitemap 模組會區分頂層 Sitemap 和巢狀 Sitemap，這兩者都是為將 `sling:sitemapRoot` 屬性設為 `true` 的任何資源產生的。通常，Sitemap 是使用樹狀頂層 Sitemap 路徑上的選擇器呈現的，這是沒有其他 Sitemap 根上階的資源。此頂層 Sitemap 根也會公開了 Sitemap 索引，這通常是網站所有者在搜索引擎的設定入口網站中設定，或新增到網站的 `robots.txt` 的 Sitemap 索引。

例如，假設有一個網站，將頂層 Sitemap 根定義在 `my-page`，將巢狀 Sitemap 根定義在 `my-page/news`，為新聞子樹狀結構中的頁面產生專用 Sitemap。由此產生的相關 URL 將是

* `<https://www.mydomain.com/my-brand/my-page.sitemap-index.xml>`
* `<https://www.mydomain.com/my-brand/my-page.sitemap.xml>`
* `<https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html>`

>[!NOTE]
>
> 選擇器 `sitemap` 和 `sitemap-index` 可能會干擾自訂實作。如果您不想使用產品功能，請設定您自己的 servlet，為這些選擇器提供大於 0 的 `service.ranking`。

在預設設定中，頁面屬性對話框提供了一個選項來將頁面標記為 Sitemap 根，因此，如上所述，產生它本身 Sitemap 和其子系。此行為由 `SitemapGenerator` 的實作來實作，並且可以透過新增替代實作來擴展。但是，由於重新產生 XML Sitemap 的頻率高度依賴內容編寫工作流程和工作負載，因此該產品不提供任何 `SitemapScheduler` 設定。這使得該功能有效率地選擇加入。

為了啟用產生 XML Sitemap 的背景作業，必須設定 `SitemapScheduler`。若要這麼做，請為 PID `org.apache.sling.sitemap.impl.SitemapScheduler` 建立 OSGI 設定。排程器運算式 `0 0 0 * * ?` 可作為每天午夜一次重新產生所有 XML Sitemap 的起點。

![Apache Sling Sitemap - 排程器](assets/sling-sitemap-scheduler.png)

Sitemap 產生工作可以在編寫層和發佈層執行個體上執行。在大多數情況下，建議在發佈層執行個體上執行產生工作，因為只能在那裡產成標準 URL (由於 Sling 資源對應規則通常僅存在於發佈層執行個體上)。但是，可以透過實作 [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) 執行個體來插入用於產生標準 URL 的具體化機制的自訂實作。如果自訂實作可以在編寫層執行個體上產生 Sitemap 標準 URL，可以針對作者執行模式設定 `SitemapScheduler`，XML Sitemap 產生工作負載可以分配給編寫服務叢集的多個執行個體。在這種情況下，必須特別注意處理尚未發佈、已修改或只有一組受限的使用者可見的內容。

AEM Sites 包含 `SitemapGenerator` 的預設實作，它周遊頁面樹以產生 Sitemap。它被預先設定為僅輸出網站的標準 URL 和任何可用的語言替代選項。如果需要，也可設定為包含頁面的上次修改日期。為此，啟用&#x200B;*Adobe AEM SEO - 頁面樹 Sitemap 產生器*&#x200B;設定的&#x200B;*新增上次修改日期*，並選取&#x200B;*上次修改的來源*。在發佈層產生 Sitemap 時，建議使用 `cq:lastModified` 日期。

![Adobe AEM SEO - 頁面樹 Sitemap 產生器設定](assets/sling-sitemap-pagetreegenerator.png)

若要限制 Sitemap 的內容，可以在需要時實作以下服務介面：

* 可以實作 [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) 以隱藏 AEM Sites 特定 Sitemap 產生器所產生之 XML Sitemap 的頁面。
* 可以實作 [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) 或 [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) 以篩選出 [商務整合框架](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=zh-Hant) 特定 Sitemap 產生器所產生之 XML Sitemap 的產品或類別。

如果預設實作在特定使用案例無法作用或者擴充點不夠靈活，則可以實作自訂 `SitemapGenerator` 以完全控制產生之 Sitemap 的內容。以下範例展示如何使用 AEM Sites 的預設實作邏輯來完成此操作。它使用 [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) 作為周遊頁面樹的起點：

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, and so on
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

此外，為 XML Sitemap 實作的功能也可以用於不同的使用案例，例如將標準連結或語言替代項新增到頁面的頁首。如需詳細資訊，請參閱 [SEO 標記](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html)介面。

### 為舊版 URL 建立 301 重新導向 {#creating-redirects-for-legacy-urls}

以新結構啟動網站時，務必在 Apache HTTP 伺服器中實作並測試 301 重新導向，理由有二：

* 舊版 URL 已累積一段時間的 SEO 值了。實作重新導向，搜尋引擎才可將此值套用至新 URL。
* 您的網站使用者可能已建立連向這些網頁的書籤了。實作重新導向，您才能確實將使用者導向新網站上與他們在嘗試進入舊網站時所前往位置最相符的網頁。

請務必參閱下方的其他資源章節，瞭解實作 301 重新導向的操作指示，並以工具測試重新導向是否如期運作。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱下列其他資源：

<!--
* [Resource Mapping](/help/sites-deploying/resource-mapping.md)
-->

* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
* [https://github.com/apache/sling-org-apache-sling-sitemap](https://github.com/apache/sling-org-apache-sling-sitemap)
