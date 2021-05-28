---
title: AEM技術基礎
description: 概述AEM的技術基礎，包括AEM的結構方式和基本技術（例如JCR、Sling和OSGi）。
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 8ba7968ee7f4d3c808740054bf841dbaf9dd4254
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 0%

---

# AEM技術基礎{#aem-technical-foundations}

AEM是以經驗證、可擴充且靈活的技術為基礎而打造的強大平台。 本檔案詳細說明組成AEM的各個部件，並打算作為完整堆疊AEM開發人員的技術附錄。 這不是快速入門手冊。 若您為AEM開發的新手，請參閱[開發AEM Sites快速入門 — WKND教學課程](develop-wknd-tutorial.md)，作為第一步。

>[!TIP]
>
>在深入探討AEM的核心技術之前，Adobe建議您先完成[開發AEM Sites快速入門 — WKND教學課程。](develop-wknd-tutorial.md)

## 基本面 {#fundamentals}

作為現代內容管理系統，AEM仰賴標準網路技術：

* 請求 — 回應(XMLHttpRequest / XMLHttpResponse)週期
* HTML
* CSS
* JavaScript

基礎內容存放庫和業務邏輯層是以Java技術為基礎而構建的：

* JCR
* Sling
* OSGi

## Java內容儲存庫{#java-content-repository}

Java內容儲存庫(JCR)標準[JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)指定了獨立於供應商和獨立於實施的方式，以在內容儲存庫的精細級別上雙向訪問內容。 Adobe研究（瑞士）AG持有規格領頭。

[JCR API 2.0](https://docs.adobe.com/content/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html)套件`javax.jcr.*`用於直接存取和操作存放庫內容。

AEM建置在JCR上。

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) 為可擴充且高效能的階層式內容存放庫之實作，以作為現代世界級網站及其他苛刻內容應用程式之基礎，符合JCR標準。

Jackrabbit Oak（也稱為Oak）是建置AEM所依據之JCR標準的實作。

## Sling要求處理{#sling-request-processing}

AEM是使用[Sling](https://sling.apache.org/site/index.html)建立的，這是一個基於REST原則的Web應用程式框架，可以輕鬆開發麵向內容的應用程式。 Sling使用JCR存放庫（例如Apache Jackrabbit Oak）作為其資料存放區。 Sling已對Apache Software Foundation作出貢獻 — 如需詳細資訊，請參閱Apache。

### Sling {#introduction-to-sling}簡介

使用Sling時，要轉譯的內容類型不是第一個處理考量。 相反，主要考量是URL是否解析至內容物件，接著便找到指令碼來執行轉譯。 這為網頁內容作者提供絕佳的支援，以建立可輕鬆根據其需求自訂的頁面。

在具有廣泛不同內容元素的應用程式中，或當您需要可輕鬆自訂的頁面時，這種靈活性的優勢就顯而易見。 尤其是實作Web內容管理系統(例如AEM)時。

如需使用Sling開發的前幾個步驟，請參閱[在15分鐘內探索Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)。

下圖說明Sling指令碼解析度：它會顯示如何從HTTP請求到內容節點、從內容節點到資源類型、從資源類型到指令碼，以及哪些指令碼變數可用。

![了解Apache Sling指令碼解析度](assets/sling-cheatsheet-01.png)

下圖說明了處理`SlingPostServlet`時可以使用的所有隱藏但功能強大的請求參數，是所有POST請求的預設處理程式，為您提供建立、修改、刪除、複製和移動儲存庫中節點的無數選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以內容為中心{#sling-is-content-centric}

Sling是&#x200B;*內容中心*。 這表示處理作業會聚焦在內容上，因為每個(HTTP)請求會以JCR資源（存放庫節點）的形式對應至內容：

* 第一個目標是保留內容的資源（JCR節點）
* 其次，表示或指令碼是結合請求的特定部分（例如選取器和/或擴充功能）從資源屬性中找到

### RESTful Sling {#restful-sling}

由於其以內容為中心的理念，Sling實作了REST導向的伺服器，因此在Web應用程式架構中提供新概念。 優點如下：

* 非常RESTful，不只是表面上；資源和表示在伺服器內正確建模
* 移除一或多個資料模型
   * 其他內容管理框架可能需要URL結構、業務對象、資料庫架構才能訪問資源。
   * 使用Sling時，此功能會簡化為：URL =資源= JCR結構

### URL分解{#url-decomposition}

在Sling中，處理是由使用者要求的URL驅動。 這會定義要由適當指令碼顯示的內容。 為此，會從URL中擷取資訊。

如果我們分析下列URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 |  | 內容路徑 | 選取器 | 擴充功能 |  | 尾碼 |  | 參數 |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **通訊協定**  - HTTPS
* **主機**  — 網站的網域
* **內容路徑**  — 指定要轉譯的內容，並與擴充功能搭配使用的路徑；在此範例中，這些  `tools/spy.html`
* **選取器**  — 用於轉譯內容的替代方法；在此示例中，以A4格式顯示打印機友好版本
* **擴充功能**  — 內容格式；也指定要用於呈現的指令碼
* **尾碼**  — 可用來指定其他資訊
* **參數**  — 動態內容所需的任何參數

#### 從URL到內容和指令碼{#from-url-to-content-and-scripts}

使用URL分解的原則：

* 對應使用從請求中擷取的內容路徑來尋找資源。
* 找到適當的資源時，會擷取Sling資源類型，並用來尋找要用於轉譯內容的指令碼。

下圖說明所使用的機制，將在以下各節中詳細討論。

![URL對應機制](assets/url-mapping.png)

使用Sling時，您可以指定哪個指令碼會轉譯特定實體（透過在JCR節點中設定`sling:resourceType`屬性）。 此機制提供的自由比指令碼訪問資料實體（PHP指令碼中的SQL陳述式會這樣做）的自由多，因為資源可以有多個格式副本。

#### 將請求映射到資源{#mapping-requests-to-resources}

會劃分要求並擷取必要資訊。 系統會搜索所請求的資源（內容節點）:

* 第一個Sling會檢查節點是否存在於要求中指定的位置；例如`../content/corporate/jobs/developer.html`
* 如果未找到節點，則刪除擴展並重複搜索；例如`../content/corporate/jobs/developer`
* 如果找不到節點，Sling會傳回http程式碼404（找不到）。

Sling也允許JCR節點以外的其他項目成為資源，但這是進階功能。

### 找到指令碼{#locating-the-script}

找到適當的資源（內容節點）時，會擷取&#x200B;**sling資源類型**。 這是路徑，可找出要用於轉譯內容的指令碼。

`sling:resourceType`所指定的路徑可以是：

* 絕對
* 相對於配置參數

>[!TIP]
>
>相對路徑因可移植性提高而建議由Adobe使用。

所有Sling指令碼都儲存在`/apps`（可變，用戶指令碼）或`/libs`（不可變，系統指令碼）的子資料夾中，這些子資料夾將按此順序進行搜索。

其他注意事項包括：

* 當需要方法(GET、POST)時，將根據HTTP規範(例如，`jobs.POST.esp`
* 支援各種指令碼引擎，但常見且建議的指令碼為HTL和JavaScript。

指定AEM例項支援的指令碼引擎清單會列在Felix Management Console(`http://<host>:<port>/system/console/slingscripting`)中。

使用上一個範例，如果`sling:resourceType`為`hr/jobs`，則適用於：

* GET/HEAD要求和結尾為`.html`的URL（預設請求類型，預設格式）
   * 指令碼將為`/apps/hr/jobs/jobs.esp`;`sling:resourceType`的最後一節將形成檔案名。
* POST請求(所有請求類型，除GET/HEAD外，方法名稱必須為大寫)
   * POST將用於指令碼名稱中。
   * 指令碼將為`/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，結尾不是`.html`
   * 例如`../content/corporate/jobs/developer.pdf`
   * 指令碼將為`/apps/hr/jobs/jobs.pdf.esp`;尾碼會新增至指令碼名稱。
* 具有選取器的URL
   * 選取器可用來以替代格式顯示相同的內容。 例如，打印機友好版本、RSS源或摘要。
   * 如果查看打印機友好版本，其中選擇器可能為`print`;如`../content/corporate/jobs/developer.print.html`
   * 指令碼將為`/apps/hr/jobs/jobs.print.esp`;選取器會新增至指令碼名稱。
* 如果尚未定義`sling:resourceType`，則：
   * 內容路徑將用於搜索適當的指令碼（如果基於`ResourceTypeProvider`的路徑處於活動狀態）。
   * 例如，`../content/corporate/jobs/developer.html`的指令碼會在`/apps/content/corporate/jobs/`中產生搜尋。
   * 將使用主節點類型。
* 如果完全找不到指令碼，則將使用預設指令碼。
   * 預設轉譯目前支援為純文字(`.txt`)、HTML(`.html`)和JSON(`.json`)，所有這些都將列出節點的屬性（適當的格式化）。 副檔名`.res`或沒有請求副檔名的請求的預設轉譯是將資源轉存（如果可能）。
* 若是http錯誤處理（程式碼403或404）,Sling會在下列任一位置尋找指令碼：
   * 自定義指令碼的位置`/apps/sling/servlet/errorhandler`
   * 或標準指令碼`/libs/sling/servlet/errorhandler/404.jsp`的位置

如果指定請求套用多個指令碼，則會選取最符合的指令碼。 比賽越具體，越好；換言之，無論任何請求擴充功能或方法名稱相符，選取器符合的越多越好。

例如，請考慮存取資源的請求

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

除了資源類型（主要由`sling:resourceType`屬性定義）外，還有資源超類型。 這通常由`sling:resourceSuperType`屬性表示。 嘗試尋找指令碼時，也會考慮這些超類型。 資源超類型的優勢在於，它們可能形成資源的層次結構，其中預設資源類型`sling/servlet/default`（由預設servlet使用）實際上是根。

資源的資源超類型可以用兩種方式定義：

* 的`sling:resourceSuperType`屬性。
* `sling:resourceType`指向的節點的`sling:resourceSuperType`屬性。

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

類型階層：

* `/x`
   * 是`[ c, b, a, <default>]`
* 對於`/y`而言
   * 階層為`[ c, a, <default>]`

這是因為`/y`具有`sling:resourceSuperType`屬性，而`/x`沒有，因此其超類型取自於其資源類型。

#### 無法直接呼叫Sling指令碼{#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會打破REST伺服器的嚴格概念；你會混合資源和陳述。

如果您直接呼叫表示法（指令碼），會隱藏指令碼內的資源，讓架構(Sling)不再知道。 因此，您會失去某些功能：

* 自動處理GET以外的http方法，包括：
   * POST、PUT、DELETE，使用sling預設實作處理
   * `sling:resourceType`位置中的`POST.jsp`指令碼
* 您的程式碼架構已不再像原來那樣簡潔，也不再像原來那樣清晰；對大規模發展至關重要

### Sling API {#sling-api}

這會使用Sling API套件、`org.apache.sling.*`和標籤程式庫。

### 使用sling:include {#referencing-existing-elements-using-sling-include}參考現有元素

最後考量是必須參考指令碼內的現有元素。

更複雜的指令碼（聚合指令碼）可能需要訪問多個資源（例如導航、側欄、頁尾、清單的元素），並通過包括&#x200B;*resource*&#x200B;來執行此操作。

要執行此操作，可使用`sling:include("/<path>/<resource>")`命令。 這將有效地包括所參考資源的定義。

## OSGi {#osgi}

OSGi(Open Services Gateway Initiative)定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Dynamic Module System for Java）。 OSGi容器可讓您將應用程式分成個別模組（是含有其他中繼資訊的jar檔案，在OSGi術語中稱為套件組合），並透過以下功能管理應用程式之間的交叉相依性：

* 在容器內實作的服務
* 容器與應用程式之間的合約

這些服務和合同提供了一個體系結構，它使各個元素能夠動態地發現彼此以進行協作。

然後，OSGi框架將為您提供這些套件組合的動態載入/卸載、配置和控制 — 無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在[OSGi網站](https://www.osgi.org)中找到。
>
>其「基礎教育」頁面尤其包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling因此會使用OSGi的[Apache Felix](https://felix.apache.org/)實作。 它們都是在OSGi架構內執行的OSGi套件組合集合。

這可讓您對安裝中的任何套件執行下列動作：

* 安裝
* 啟動
* 停止
* 更新
* 解除安裝
* 查看當前狀態
* 存取有關特定套件組合的更詳細資訊（例如符號名稱、版本、位置等）

如需詳細資訊，請參閱[為AEM設定OSGi作為Cloud Service](/help/implementing/deploying/configuring-osgi.md) 。

## 儲存庫{#structure-within-the-repository}內的結構

下列清單提供您在存放庫中會看到的結構概述。

* `/apps`  — 與申請有關；包含您網站專屬的元件定義。您開發的元件可以根據`/libs/core/wcm/components`中可用的現成元件。
* `/content`  — 為您的網站建立的內容。
* `/etc`
* `/home`  — 使用者和群組資訊。
* `/libs`  — 屬於AEM核心的程式庫和定義。`/libs`中的子資料夾代表現成可用的AEM功能。 不能修改`/libs`中的內容。 您網站的特定功能應在`/apps`下製作。
* `/tmp` 臨時工作區。
* `/var`  — 系統更改和更新的檔案；例如審核日誌、統計資訊、事件處理。

>[!CAUTION]
>
>應謹慎變更此結構或其內的檔案。 請務必充分了解所做任何變更的含意。
>
>您不得變更`/libs`路徑中的任何項目。 對於配置和其他更改，將項從`/libs`複製到`/apps`，並在`/apps`內進行任何更改。
