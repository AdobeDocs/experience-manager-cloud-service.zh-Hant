---
title: AEM技術基礎
description: 概觀AEM的技術基礎，包括AEM的結構和基本技術（例如JCR、Sling和OSGi）。
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# AEM Technical Foundations {#aem-technical-foundations}

AEM是建立在證實可行、可擴充且有彈性的技術之上的強穩平台。 本檔案提供AEM的各個部分的詳細概述，並做為完整堆疊AEM開發人員的技術附錄。 它不是以快速入門手冊為目的。 如果您是AEM開發的新手，請參閱[開始開發AEM網站- WKND教學課程](develop-wknd-tutorial.md)作為第一步。

>[!TIP]
>
>在深入探討AEM的核心技術之前，Adobe建議先完成[開發AEM網站快速入門- WKND教學課程。](develop-wknd-tutorial.md)

## 基礎知識{#fundamentals}

AEM是現代內容管理系統，採用標準Web技術：

* 請求——回應(XMLHttpRequest / XMLHttpResponse)週期
* HTML
* CSS
* JavaScript

底層內容儲存庫和業務邏輯層是基於Java技術構建的：

* JCR
* Sling
* OSGi

## Java內容儲存庫{#java-content-repository}

Java內容儲存庫(JCR)標準[JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)指定了一種獨立於供應商和獨立於實施的方式，以在內容儲存庫的精細級別上雙向訪問內容。 規格領導者由Adobe Research（瑞士）AG持有。

[JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html)套件`javax.jcr.*`用於直接訪問和控制儲存庫內容。

AEM是以JCR為基礎。

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit ](https://jackrabbit.apache.org/oak/) Oakis是可擴充且高效能的階層式內容儲存庫的實作，可做為現代世界級網站及其他要求苛刻的內容應用程式的基礎，符合JCR標準。

Jackrabbit Oak（也稱為Oak）是建立AEM所依據的JCR標準的實作。

## Sling Request Processing {#sling-request-processing}

AEM是使用[Sling](https://sling.apache.org/site/index.html)建立的，此為以REST原則為基礎的Web應用程式架構，提供內容導向應用程式的輕鬆開發。 Sling使用JCR儲存庫，例如Apache Jackrabbit Oak，做為其資料儲存。 Sling已對Apache Software Foundation做出貢獻——如需詳細資訊，請參閱Apache。

### Sling {#introduction-to-sling}簡介

使用Sling，要轉譯的內容類型不是第一個處理考量。 主要考量是URL是否解析為內容物件，然後可找到指令碼來執行轉譯。 這為網頁內容製作者提供絕佳的支援，讓他們建立可輕鬆依其需求自訂的頁面。

此彈性的優點在具有多種不同內容元素的應用程式中，或當您需要可輕鬆自訂的頁面時，都十分明顯。 尤其是在實作網頁內容管理系統（例如AEM）時。

請參閱[Discover Sling in 15 minutes](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)，以取得使用Sling進行開發的第一步驟。

下圖說明Sling指令碼解析度：它說明如何從HTTP請求到內容節點，從內容節點到資源類型，從資源類型到指令碼，以及可用的指令碼變數。

![瞭解Apache Sling指令碼解析度](assets/sling-cheatsheet-01.png)

下圖說明了處理`SlingPostServlet`時可以使用的所有隱藏但功能強大的請求參數。&lt;a0/>是所有POST請求的預設處理程式，為您提供了在儲存庫中建立、修改、刪除、複製和移動節點的無窮選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling is Content Centric {#sling-is-content-centric}

Sling為&#x200B;*content-centric*。 這表示處理會以JCR資源（儲存庫節點）的形式，將每個(HTTP)請求映射至內容時，將重點放在內容上：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示或指令碼與請求的某些部分（例如選擇器和／或擴展）組合從資源屬性中定位

### RESTful Sling {#restful-sling}

由於其內容導向的理念，Sling建置了REST導向的伺服器，因此在Web應用程式架構中具有新概念。 其優點是：

* 非常REST風格，不只是表面上；資源和表示法在伺服器內正確建模
* 移除一或多個資料模型
   * 其他內容管理架構可能需要URL結構、商業物件、DB架構才能存取資源。
   * 使用Sling，這將縮小為：URL =資源= JCR結構

### URL分解{#url-decomposition}

在Sling中，處理是由使用者要求的URL所驅動。 這定義了要由相應指令碼顯示的內容。 若要這麼做，會從URL擷取資訊。

如果我們分析下列URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 |  | 內容路徑 | 選擇器 | extension |  | 尾碼 |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **協定** - HTTPS
* **host** -網站的網域
* **內容路徑** -指定要轉譯的內容，並與擴充功能結合使用的路徑；在本範例中，他們會轉譯為  `tools/spy.html`
* **selector(s)** -用於轉換內容的替代方法；在此示例中，打印機友好版本為A4格式
* **extension**  —— 內容格式；也指定要用於呈現的指令碼
* **suffix**  —— 可用來指定其他資訊
* **param(s)** -動態內容所需的任何參數

#### 從URL到內容和指令碼{#from-url-to-content-and-scripts}

使用URL分解原則：

* 映射使用從請求提取的內容路徑來定位資源。
* 當找到適當的資源時，會擷取sling資源類型，並用來找出要用來呈現內容的指令碼。

下圖說明所使用的機制，將在以下幾節中詳細討論。

![URL對應機制](assets/url-mapping.png)

使用Sling，您可指定要轉譯特定實體的指令碼（透過在JCR節點中設定`sling:resourceType`屬性）。 此機制提供比指令碼訪問資料實體（如PHP指令碼中的SQL陳述式）更多的自由，因為資源可以有多個轉譯。

#### 將請求映射到資源{#mapping-requests-to-resources}

請求會細分並擷取必要的資訊。 系統將搜索儲存庫以查找請求的資源（內容節點）:

* First Sling會檢查節點是否存在於請求中指定的位置；例如，`../content/corporate/jobs/developer.html`
* 如果沒有找到節點，則會丟棄擴展，並重複搜索；例如，`../content/corporate/jobs/developer`
* 如果找不到節點，Sling將會傳回http code 404(Not Found)。

Sling也允許JCR節點以外的項目成為資源，但這是進階功能。

### 查找指令碼{#locating-the-script}

當找到適當的資源（內容節點）時，會擷取&#x200B;**sling資源類型**。 這是路徑，可找到要用於呈現內容的指令碼。

`sling:resourceType`所指定的路徑可以是：

* 絕對
* 相對於配置參數

>[!TIP]
>
>Adobe建議使用相對路徑，因為相對路徑可提升可攜性。

所有Sling指令碼都儲存在`/apps`(mutable, user scripts)或`/libs`(immutable, system scripts)的子檔案夾中，會依此順序搜尋。

還需注意的一點是：

* 當需要方法(GET、POST)時，將按照HTTP規範(例如，`jobs.POST.esp`
* 支援各種指令碼引擎，但常見、建議的指令碼是HTL和JavaScript。

AEM的指定例項支援的指令碼引擎清單列在Felix Management Console(`http://<host>:<port>/system/console/slingscripting`)上。

在上例中，如果`sling:resourceType`是`hr/jobs`，則表示：

* 以`.html`結尾的GET/HEAD要求和URL（預設請求類型，預設格式）
   * 指令碼將為`/apps/hr/jobs/jobs.esp`;`sling:resourceType`的最後一節將形成檔案名。
* POST請求（除GET/HEAD外的所有請求類型，方法名稱必須大寫）
   * POST將用於指令碼名稱。
   * 指令碼將為`/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，不以`.html`結尾
   * 例如`../content/corporate/jobs/developer.pdf`
   * 指令碼將為`/apps/hr/jobs/jobs.pdf.esp`;尾碼將添加到指令碼名稱中。
* 具有選擇器的URL
   * 選擇器可用來以替代格式顯示相同的內容。 例如，印表機友好版本、RSS饋送或摘要。
   * 如果查看打印機友好版本，選擇器可能為`print`;as in `../content/corporate/jobs/developer.print.html`
   * 指令碼將為`/apps/hr/jobs/jobs.print.esp`;選取器會新增至指令碼名稱。
* 如果尚未定義`sling:resourceType`，則：
   * 內容路徑將用於搜索適當的指令碼（如果基於`ResourceTypeProvider`的路徑處於活動狀態）。
   * 例如，`../content/corporate/jobs/developer.html`的指令碼將在`/apps/content/corporate/jobs/`中生成搜索。
   * 將使用主節點類型。
* 如果根本找不到指令碼，則將使用預設指令碼。
   * 預設轉譯目前支援純文字(`.txt`)、HTML(`.html`)和JSON(`.json`)，所有這些都會列出節點的屬性（適當格式化）。 副檔名`.res`（或請求副檔名未包含請求副檔名）的預設轉譯，是將資源轉存（如果可能）。
* 對於http錯誤處理（代碼403或404）,Sling會在下列任一處尋找指令碼：
   * 自定義指令碼的`/apps/sling/servlet/errorhandler`位置
   * 或標準指令碼`/libs/sling/servlet/errorhandler/404.jsp`的位置

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

除了資源類型（主要由`sling:resourceType`屬性定義）外，還有資源super類型。 這通常由`sling:resourceSuperType`屬性指示。 嘗試尋找指令碼時，也會考慮這些超類型。 資源超類型的優勢在於，它們可以形成資源的層次結構，其中預設資源類型`sling/servlet/default`（由預設servlet使用）實際上是根資源。

資源的資源超類型可以用兩種方式定義：

* 按資源的`sling:resourceSuperType`屬性。
* 由`sling:resourceType`指向的節點的`sling:resourceSuperType`屬性。

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
   * 是`[ c, b, a, <default>]`
* 對於`/y`
   * 階層為`[ c, a, <default>]`

這是因為`/y`具有`sling:resourceSuperType`屬性，而`/x`沒有，因此其超類型取自其資源類型。

#### Sling Scripts Cannot Be Called Directly {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會打破REST伺服器的嚴格概念；你會混合資源和陳述。

如果您直接呼叫表示法（指令碼），就會隱藏指令碼內的資源，因此架構(Sling)不再知道。 因此，您會失去某些功能：

* 自動處理GET以外的http方法，包括：
   * POST、PUT、DELETE，這些處理方式都包含sling預設實作
   * `sling:resourceType`位置中的`POST.jsp`指令碼
* 您的程式碼架構已不再像原本那樣簡潔，也不再像原本那樣清晰；對於大規模發展至關重要

### Sling API {#sling-api}

這會使用Sling API套件、`org.apache.sling.*`和標籤庫。

### 使用sling:include {#referencing-existing-elements-using-sling-include}參照現有元素

最後考慮的是，需要參考指令碼中的現有元素。

更複雜的指令碼（匯整指令碼）可能需要存取多個資源（例如導覽、側欄、頁尾、清單的元素），並加入&#x200B;*resource*。

要執行此操作，可使用`sling:include("/<path>/<resource>")`命令。 這將有效地包括引用資源的定義。

## OSGi {#osgi}

OSGi（Open Services Gateway Initiative，開放服務網關計畫）定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Java動態模組系統）。 OSGi容器可讓您將應用程式分割為個別模組（在OSGi術語中，是包含額外中繼資訊的jar檔案，並稱為bundles），並透過下列功能管理它們之間的跨相依性：

* 在容器內實施的服務
* 容器與應用程式之間的合約

這些服務和合約提供一種架構，可讓個別元素動態發現彼此以進行協作。

然後，OSGi框架可為您提供這些捆綁包的動態載入／卸載、配置和控制——無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在[OSGi網站](https://www.osgi.org)中找到。
>
>尤其是，其「基本教育」頁面包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling，因此AEM會使用[Apache Felix](https://felix.apache.org/) OSGi實作。 它們都是在OSGi框架內運行的OSGi捆綁包的集合。

這可讓您對安裝中的任何軟體包執行以下操作：

* 安裝
* 啟動
* 停止
* 更新
* 解除安裝
* 查看當前狀態
* 存取有關特定組合的更多詳細資訊（例如符號名稱、版本、位置等）

如需詳細資訊，請參閱[將AEM的OSGi設定為雲端服務](/help/implementing/deploying/configuring-osgi.md)。

## 資料庫{#structure-within-the-repository}中的結構

以下清單概述了在儲存庫中將看到的結構。

* `/apps` -與應用程式相關；包含您網站專屬的元件定義。您開發的元件可以以`/libs/core/wcm/components`中可用的現成元件為基礎。
* `/content` -為您的網站建立的內容。
* `/etc`
* `/home` -使用者和群組資訊。
* `/libs` -屬於AEM核心的程式庫和定義。`/libs`中的子資料夾代表現成可用的AEM功能。 `/libs`中的內容不得修改。 您網站的特定功能應在`/apps`下。
* `/tmp` -臨時工作區。
* `/var` -系統更改和更新的檔案；例如審核記錄、統計資料、事件處理。

>[!CAUTION]
>
>對此結構或其中的檔案進行更改時應小心謹慎。 請務必充分瞭解您所做的任何變更的影響。
>
>您不得變更`/libs`路徑中的任何項目。 對於配置和其他更改，請將項目從`/libs`複製到`/apps`，並在`/apps`中進行任何更改。
