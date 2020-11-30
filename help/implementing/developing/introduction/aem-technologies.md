---
title: AEM技術基礎
description: 概觀AEM的技術基礎，包括AEM的結構和基本技術（例如JCR、Sling和OSGi）。
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# AEM技術基礎 {#aem-technical-foundations}

AEM是建立在證實可行、可擴充且有彈性的技術之上的強穩平台。 本檔案提供AEM的各種組成部分的詳細概述，並做為完整堆疊AEM開發人員的技術附錄。 它不是以快速入門手冊為目的。 如果您是AEM開發的新手，請參閱「開 [始開發AEM網站- WKND教學課程](develop-wknd-tutorial.md) 」（第一步）。

>[!TIP]
>
>在深入探討AEM的核心技術之前，Adobe建議您先完成「開 [始開發AEM網站- WKND教學課程」。](develop-wknd-tutorial.md)

## 基礎 {#fundamentals}

AEM是現代內容管理系統，採用標準Web技術：

* 請求——回應(XMLHttpRequest / XMLHttpResponse)週期
* HTML
* CSS
* JavaScript

底層內容儲存庫和業務邏輯層是基於Java技術構建的：

* JCR
* Sling
* OSGi

## Java內容儲存庫 {#java-content-repository}

Java Content Repository(JCR)標準 [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)，指定了獨立於供應商和獨立於實施的方式，以便在內容儲存庫的精細級別上雙向訪問內容。 規格領導者由Adobe Research（瑞士）AG持有。

JCR [API 2.0套件](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) , `javax.jcr.*` 用於直接存取和控制儲存庫內容。

AEM是以JCR為基礎。

## 阿帕奇傑克拉布特橡樹 {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) 是可擴充且高效能的階層式內容儲存庫的實作，以做為現代世界級網站及其他要求苛刻的內容應用程式的基礎，符合JCR標準。

Jackrabbit Oak（也稱為Oak）是建立AEM所依據的JCR標準的實作。

## Sling請求處理 {#sling-request-processing}

AEM是使用 [Sling](https://sling.apache.org/site/index.html)（以REST原則為基礎的Web應用程式架構）建立的，可輕鬆開發內容導向應用程式。 Sling使用JCR儲存庫，例如Apache Jackrabbit Oak，做為其資料儲存。 Sling已對Apache Software Foundation做出貢獻——如需詳細資訊，請參閱Apache。

### Sling簡介 {#introduction-to-sling}

使用Sling，要轉譯的內容類型不是第一個處理考量。 主要考量是URL是否解析為內容物件，然後可找到指令碼來執行轉譯。 這為網頁內容製作者提供絕佳的支援，讓他們建立可輕鬆依其需求自訂的頁面。

此彈性的優點在具有多種不同內容元素的應用程式中，或當您需要可輕鬆自訂的頁面時，都十分明顯。 尤其是在實作網頁內容管理系統（例如AEM）時。

請參 [閱Discover Sling in 15 minutes](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) for the first steps for developing with Sling。

下圖說明Sling指令碼解析度：它說明如何從HTTP請求到內容節點，從內容節點到資源類型，從資源類型到指令碼，以及可用的指令碼變數。

![瞭解Apache Sling指令碼解析度](assets/sling-cheatsheet-01.png)

下圖說明了處理所有POST請求的預設處理程式時，您可以使用的所有隱藏但功能強大的請求參數 `SlingPostServlet`，這些預設處理程式為您提供了在儲存庫中建立、修改、刪除、複製和移動節點的無窮選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling is Content Centric {#sling-is-content-centric}

Sling是以 *內容為中心*。 這表示處理會以JCR資源（儲存庫節點）的形式，將每個(HTTP)請求映射至內容時，將重點放在內容上：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示或指令碼與請求的某些部分（例如選擇器和／或擴展）組合從資源屬性中定位

### RESTful Sling {#restful-sling}

由於其內容導向的理念，Sling建置了REST導向的伺服器，因此在Web應用程式架構中具有新概念。 其優點是：

* 非常REST風格，不只是表面上；資源和表示法在伺服器內正確建模
* 移除一或多個資料模型
   * 其他內容管理架構可能需要URL結構、商業物件、DB架構才能存取資源。
   * 使用Sling，這將縮小為：URL =資源= JCR結構

### URL分解 {#url-decomposition}

在Sling中，處理是由使用者要求的URL所驅動。 這定義了要由相應指令碼顯示的內容。 若要這麼做，會從URL擷取資訊。

如果我們分析下列URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 |  | 內容路徑 | 選擇器 | extension |  | 尾碼 |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **通訊協定** - HTTPS
* **host** —— 站點的域
* **內容路徑** -指定要轉譯的內容，並與副檔名一起使用的路徑；在本範例中，他們會轉譯為 `tools/spy.html`
* **selector(s)** -用於轉換內容的替代方法；在此示例中，打印機友好版本為A4格式
* **extension** —— 內容格式；也指定要用於呈現的指令碼
* **suffix** —— 可用來指定其他資訊
* **param(s)** -動態內容所需的任何參數

#### 從URL到內容和指令碼 {#from-url-to-content-and-scripts}

使用URL分解原則：

* 映射使用從請求提取的內容路徑來定位資源。
* 當找到適當的資源時，會擷取sling資源類型，並用來尋找要用來呈現內容的指令碼。

下圖說明所使用的機制，將在以下幾節中詳細討論。

![URL對應機制](assets/url-mapping.png)

使用Sling，您可指定哪個指令碼會轉譯特定實體(透過在JCR節 `sling:resourceType` 點中設定屬性)。 此機制提供比指令碼訪問資料實體（如PHP指令碼中的SQL陳述式）更多的自由，因為資源可以有多個轉譯。

#### 將請求對應至資源 {#mapping-requests-to-resources}

請求會細分並擷取必要的資訊。 系統將搜索儲存庫以查找請求的資源（內容節點）:

* First Sling會檢查節點是否存在於請求中指定的位置；例如， `../content/corporate/jobs/developer.html`
* 如果沒有找到節點，則會丟棄擴展，並重複搜索；例如， `../content/corporate/jobs/developer`
* 如果找不到節點，Sling將會傳回http code 404(Not Found)。

Sling也允許JCR節點以外的項目成為資源，但這是進階功能。

### 查找指令碼 {#locating-the-script}

當找到適當的資源（內容節點）時， **會擷取sling資源類型** 。 這是路徑，可找到要用於呈現內容的指令碼。

由指定的路 `sling:resourceType` 徑可以是：

* 絕對
* 相對於配置參數

>[!TIP]
>
>Adobe建議使用相對路徑，因為相對路徑可提升可攜性。

所有Sling指令碼都儲存在(mutable, user scripts)或 `/apps``/libs` (immutable, system scripts)的子檔案夾中，依此順序搜尋。

還需注意的一點是：

* 當需要方法(GET、POST)時，將按照HTTP規範(例如， `jobs.POST.esp`
* 支援各種指令碼引擎，但常見、建議的指令碼是HTL和JavaScript。

AEM的指定例項支援的指令碼引擎清單會列在Felix Management Console( `http://<host>:<port>/system/console/slingscripting`)上。

使用上一個範例，如果 `sling:resourceType` 是 `hr/jobs` :

* GET/HEAD請求和URL結尾 `.html` 為（預設請求類型、預設格式）
   * 劇本是 `/apps/hr/jobs/jobs.esp`;最後一部分將 `sling:resourceType` 形成檔案名。
* POST請求（除GET/HEAD外的所有請求類型，方法名稱必須大寫）
   * POST將用於指令碼名稱。
   * 指令碼是 `/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，不以 `.html`
   * For example `../content/corporate/jobs/developer.pdf`
   * 劇本是 `/apps/hr/jobs/jobs.pdf.esp`;尾碼將添加到指令碼名稱中。
* 具有選擇器的URL
   * 選擇器可用來以替代格式顯示相同的內容。 例如，印表機友好版本、RSS饋送或摘要。
   * 如果我們查看打印機友好版本，選擇器可能位於 `print`;as in `../content/corporate/jobs/developer.print.html`
   * 劇本是 `/apps/hr/jobs/jobs.print.esp`;選取器會新增至指令碼名稱。
* 如果尚未 `sling:resourceType` 定義，則：
   * 內容路徑將用來搜尋適當的指令碼（如果以路徑為基礎）。 `ResourceTypeProvider`
   * 例如，的指令碼將 `../content/corporate/jobs/developer.html` 在中生成搜索 `/apps/content/corporate/jobs/`。
   * 將使用主節點類型。
* 如果根本找不到指令碼，則將使用預設指令碼。
   * 預設轉譯目前支援純文字(`.txt`)、HTML(`.html`)和JSON(`.json`)格式，所有格式都會列出節點的屬性（適當格式化）。 副檔名(或請求副檔 `.res`名未包含請求副檔名的請求)的預設轉譯，是將資源轉存（如果可能）。
* 對於http錯誤處理（代碼403或404）,Sling會在下列任一處尋找指令碼：
   * 自訂指令 `/apps/sling/servlet/errorhandler` 碼的位置
   * 或標準指令碼的位置 `/libs/sling/servlet/errorhandler/404.jsp`

如果多個指令碼套用至指定的請求，則會選取最符合的指令碼。 比賽越具體，越好；換言之，無論任何請求副檔名或方法名稱相符，選擇器與選取器的匹配程度都越高。

例如，考慮請求訪問資源

* `/content/corporate/jobs/developer.print.a4.html`

類型

* `sling:resourceType="hr/jobs"`

假設我們在正確位置有下列指令碼清單：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

優先順序為(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了資源類型（主要由屬性定義）外，還 `sling:resourceType` 有資源super類型。 這通常由屬性指 `sling:resourceSuperType` 示。 嘗試尋找指令碼時，也會考慮這些超類型。 資源超類型的優勢在於，它們可以形成資源的層次結構，其中預設資源類型 `sling/servlet/default` （由預設servlet使用）實際上是根。

資源的資源超類型可以用兩種方式定義：

* 按資 `sling:resourceSuperType` 源的屬性。
* 由指向 `sling:resourceSuperType` 的節點的屬性所 `sling:resourceType` 示。

例如：

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

以下類型的層次結構：

* `/x`
   * Is `[ c, b, a, <default>]`
* While for `/y`
   * 階層是 `[ c, a, <default>]`

這是因為 `/y` 有屬性， `sling:resourceSuperType` 但 `/x` 沒有，因此其超類型取自其資源類型。

#### Sling Scripts無法直接呼叫 {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會打破REST伺服器的嚴格概念；你會混合資源和陳述。

如果您直接呼叫表示法（指令碼），就會隱藏指令碼內的資源，因此架構(Sling)不再知道。 因此，您會失去某些功能：

* 自動處理GET以外的http方法，包括：
   * POST、PUT、DELETE，這些處理方式都包含sling預設實作
   * 您所 `POST.jsp` 在位置的腳 `sling:resourceType` 本
* 您的程式碼架構已不再像原本那樣簡潔，也不再像原本那樣清晰；對於大規模發展至關重要

### Sling API {#sling-api}

這會使用Sling API套件 `org.apache.sling.*`和標籤庫。

### 使用sling:include參照現有元素 {#referencing-existing-elements-using-sling-include}

最後考慮的是，需要參考指令碼中的現有元素。

更複雜的指令碼（匯整指令碼）可能需要存取多個資源（例如導覽、側欄、頁尾、清單元素），並加入資 *源*。

要執行此操作，可使用命 `sling:include("/<path>/<resource>")` 令。 這將有效地包括引用資源的定義。

## OSGi {#osgi}

OSGi（Open Services Gateway Initiative，開放服務網關計畫）定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Java動態模組系統）。 OSGi容器可讓您將應用程式分割為個別模組（在OSGi術語中，是包含額外中繼資訊的jar檔案，並稱為bundles），並透過下列功能管理它們之間的跨相依性：

* 在容器內實施的服務
* 容器與應用程式之間的合約

這些服務和合約提供一種架構，可讓個別元素動態發現彼此以進行協作。

然後，OSGi框架可為您提供這些捆綁包的動態載入／卸載、配置和控制——無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在 [OSGi網站上找到](https://www.osgi.org)。
>
>尤其是，其「基本教育」頁面包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling，因此AEM會使用 [Apache Felix](https://felix.apache.org/) implementation of OSGi。 它們都是在OSGi框架內運行的OSGi捆綁包的集合。

這可讓您對安裝中的任何軟體包執行以下操作：

* 安裝
* 啟動
* 停止
* 更新
* 解除安裝
* 查看當前狀態
* 存取有關特定組合的更多詳細資訊（例如符號名稱、版本、位置等）

如需 [詳細資訊，請參閱「將AEM的OSGi設定為雲端服務](/help/implementing/deploying/configuring-osgi.md) 」。

## 儲存庫內的結構 {#structure-within-the-repository}

以下清單概述了在儲存庫中將看到的結構。

* `/apps` -與應用程式相關；包含您網站專屬的元件定義。 您開發的元件可以以位於的立即可用元件為基礎 `/libs/core/wcm/components`。
* `/content` -為您的網站建立的內容。
* `/etc`
* `/home` -使用者和群組資訊。
* `/libs` -屬於AEM核心的程式庫和定義。 中的子資料 `/libs` 夾代表現成可用的AEM功能。 中的內容 `/libs` 不得修改。 您網站的特定功能應在下 `/apps`。
* `/tmp` -臨時工作區。
* `/var` -系統更改和更新的檔案；例如審核記錄、統計資料、事件處理。

>[!CAUTION]
>
>對此結構或其中的檔案進行更改時應小心謹慎。 請務必充分瞭解您所做的任何變更的影響。
>
>您不得變更路徑中的任 `/libs` 何項目。 對於配置和其他更改，將項目從復 `/libs` 制到 `/apps` 並在中進行任何更改 `/apps`。
