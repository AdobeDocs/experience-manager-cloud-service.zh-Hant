---
title: 技AEM術基礎
description: 概述技術基礎，AEM包括AEMJCR、Sling和OSGi等結構化和基本技術。
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 0%

---

# 技AEM術基礎 {#aem-technical-foundations}

AEM是一個基於經驗證、可擴展和靈活的技術構建的強健平台。 本文檔詳細概述了構成整個堆棧開發AEM人員的各個部件，並打算作為技術附AEM錄。 它不是作為入門指南。 如果您是新開發AEM人員，請咨詢 [開始開發AEM Sites- WKND教程](develop-wknd-tutorial.md) 作為第一步。

>[!TIP]
>
>在深入瞭解核心技術之前AEM,Adobe建議完成 [開始開發AEM Sites- WKND教程。](develop-wknd-tutorial.md)

## 基礎 {#fundamentals}

作為一個現代內容管理系統，AEM它依賴於標準的Web技術：

* 請求 — 響應(XMLHttpRequest / XMLHttpResponse)週期
* HTML
* CSS
* JavaScript

底層內容儲存庫和業務邏輯層是圍繞Java技術構建的：

* JCR
* Sling
* OSGi

## Java內容儲存庫 {#java-content-repository}

Java內容儲存庫(JCR)標準， [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)，指定一種獨立於供應商和獨立於實施的方法，以在內容儲存庫的粒度級別上雙向訪問內容。 規格線索由Adobe研究公司（瑞士）AG持有。

的 [JCR API 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包， `javax.jcr.*` 用於直接訪問和處理儲存庫內容。

建AEM立在JCR上。

## 阿帕奇長兔橡樹 {#jackrabbit-oak}

[阿帕奇長兔橡樹](https://jackrabbit.apache.org/oak/) 是可擴展的高效能分層內容儲存庫的實現，用於作為現代世界級網站和其他要求苛刻的內容應用程式的基礎，符合JCR標準。

Jackrabbit Oak（也簡稱Oak）是JCR標準的實施，其基礎是JCRAEM標準。

## Sling請求處理 {#sling-request-processing}

AEM使用 [吊帶](https://sling.apache.org/site/index.html)Web應用程式框架，它基於REST原理，提供面向內容的應用程式的輕鬆開發。 Sling使用JCR儲存庫（如Apache Jackrabbit Oak）作為其資料儲存。 Sling已經為Apache Software Foundation提供了幫助 — 有關詳細資訊，請參閱Apache。

### Sling簡介 {#introduction-to-sling}

使用Sling，要呈現的內容類型不是第一個處理考慮。 相反，主要考慮的是URL是否解析為內容對象，然後可以找到指令碼來執行呈現。 這為Web內容作者構建可輕鬆根據其要求定製的頁面提供了極好的支援。

這種靈活性的優點在具有多種不同內容元素的應用程式中，或在您需要可輕鬆定製的頁面時都顯而易見。 特別是，當實施Web內容管理系統時，例如AEM。

請參閱 [在15分鐘內發現Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 和斯林一起發展的第一步。

下圖說明了Sling指令碼解析：它顯示如何從HTTP請求獲取內容節點、從內容節點獲取資源類型、從資源類型獲取指令碼以及哪些指令碼變數可用。

![瞭解Apache Sling指令碼解析](assets/sling-cheatsheet-01.png)

下圖說明了在處理 `SlingPostServlet`，所有POST請求的預設處理程式，它為您提供了建立、修改、刪除、複製和移動儲存庫中節點的無窮選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以內容為中心 {#sling-is-content-centric}

吊帶 *以內容為中心*。 這意味著，當每個(HTTP)請求以JCR資源（儲存庫節點）的形式映射到內容時，處理將集中在內容上：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示或指令碼與請求的某些部分（例如選擇器和/或擴展）組合從資源屬性中定位

### REST風格吊帶 {#restful-sling}

由於其以內容為中心的理念，Sling實現了面向REST的伺服器，因此在Web應用框架中具有新的概念。 其優點是：

* 非常REST風格，不僅僅在表面；資源和表示形式在伺服器內正確建模
* 刪除一個或多個資料模型
   * 其他內容管理框架可能需要URL結構、業務對象、資料庫架構來訪問資源。
   * 使用Sling，這將縮減為：URL =資源= JCR結構

### URL分解 {#url-decomposition}

在Sling中，處理由用戶請求的URL驅動。 這定義了由相應指令碼顯示的內容。 為此，從URL中提取資訊。

如果分析以下URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 |  | 內容路徑 | 選擇器 | 擴展 |  | 尾碼 |  | 參數 |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **協定** - HTTPS
* **主機**  — 站點的域
* **內容路徑**  — 指定要呈現的內容並與擴展結合使用的路徑；在本例中，它們轉換為 `tools/spy.html`
* **選擇器**  — 用於繪製內容的替代方法；在本示例中，打印機友好版本（A4格式）
* **擴展**  — 內容格式；還指定要用於呈現的指令碼
* **尾碼**  — 可用於指定其他資訊
* **參數**  — 動態內容所需的任何參數

#### 從URL到內容和指令碼 {#from-url-to-content-and-scripts}

利用URL分解的原理：

* 映射使用從請求中提取的內容路徑來定位資源。
* 當找到適當的資源時，提取sling資源類型，並用於定位用於呈現內容的指令碼。

下圖說明了所使用的機制，將在以下各節中詳細討論該機制。

![URL映射機制](assets/url-mapping.png)

使用Sling，可指定呈現特定實體的指令碼(通過設定 `sling:resourceType` 屬性)。 此機制提供了比指令碼訪問資料實體（如PHP指令碼中的SQL陳述式所做）更多的自由，因為資源可以具有多個格式副本。

#### 將請求映射到資源 {#mapping-requests-to-resources}

請求被分解並提取必要的資訊。 系統會搜索儲存庫以查找請求的資源（內容節點）:

* First Sling檢查節點是否位於請求中指定的位置；例如 `../content/corporate/jobs/developer.html`
* 如果找不到節點，則刪除擴展並重複搜索；例如 `../content/corporate/jobs/developer`
* 如果找不到節點，Sling將返回http代碼404（未找到）。

Sling還允許JCR節點以外的其他內容成為資源，但這是一個高級功能。

### 查找指令碼 {#locating-the-script}

找到相應的資源（內容節點）時， **sling資源類型** 的子菜單。 這是路徑，它定位用於呈現內容的指令碼。

由 `sling:resourceType` 可以選擇：

* 絕對
* 相對於配置參數

>[!TIP]
>
>相對路徑是Adobe推薦的，因為它們增加了可移植性。

所有Sling指令碼都儲存在任意一個子資料夾中 `/apps` （mutable、用戶指令碼）或 `/libs` （不可變，系統指令碼），將按此順序進行搜索。

還需注意的幾點是：

* 當需要方法(GET、POST)時，將按照HTTP規範(例如， `jobs.POST.esp`
* 支援各種指令碼引擎，但推薦的常見指令碼是HTL和JavaScript。

Felix管理控制台上列出了給定實例支援AEM的指令碼引擎清單( `http://<host>:<port>/system/console/slingscripting`)。

使用上一個示例，如果 `sling:resourceType` 是 `hr/jobs` 則為：

* GET/HEAD請求和以結尾的URL `.html` （預設請求類型，預設格式）
   * 指令碼將 `/apps/hr/jobs/jobs.esp`;最後一部分 `sling:resourceType` 形成檔案名。
* POST請求(除GET/HEAD外的所有請求類型，方法名稱必須為大寫)
   * POST將用於指令碼名。
   * 指令碼將 `/apps/hr/jobs/jobs.POST.esp`。
* 其他格式的URL，不以結尾 `.html`
   * 例如 `../content/corporate/jobs/developer.pdf`
   * 指令碼將 `/apps/hr/jobs/jobs.pdf.esp`;尾碼將添加到指令碼名稱。
* 具有選擇器的URL
   * 選擇器可用於以替代格式顯示相同的內容。 例如，打印機友好版本、RSS源或摘要。
   * 如果查看打印機友好版本，選擇器可能位於 `print`;在 `../content/corporate/jobs/developer.print.html`
   * 指令碼將 `/apps/hr/jobs/jobs.print.esp`;選擇器將添加到指令碼名稱。
* 否 `sling:resourceType` 定義：
   * 內容路徑將用於搜索適當的指令碼（如果基於路徑） `ResourceTypeProvider` 活動)。
   * 例如， `../content/corporate/jobs/developer.html` 會在 `/apps/content/corporate/jobs/`。
   * 將使用主節點類型。
* 如果根本找不到指令碼，則將使用預設指令碼。
   * 預設格式副本當前支援為純文字檔案(`.txt`),HTML(`.html`)和JSON(`.json`)，所有這些都將列出節點的屬性（適當格式化）。 擴展的預設格式副本 `.res`，或沒有請求擴展的請求，則將資源假離線（如果可能）。
* 對於http錯誤處理（代碼403或404）,Sling將在以下任一位置查找指令碼：
   * 位置 `/apps/sling/servlet/errorhandler` 用於自定義指令碼
   * 或者標準指令碼的位置 `/libs/sling/servlet/errorhandler/404.jsp`

如果多個指令碼應用於給定的請求，則選擇匹配程度最佳的指令碼。 比賽越具體越好，換句話說，無論任何請求副檔名或方法名稱是否匹配，選擇器越匹配越好。

例如，考慮訪問資源的請求

* `/content/corporate/jobs/developer.print.a4.html`

類型

* `sling:resourceType="hr/jobs"`

假設我們在正確的位置有以下指令碼清單：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

然後優先順序是(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除資源類型外(主要由 `sling:resourceType` 屬性)也有資源超級類型。 這通常由 `sling:resourceSuperType` 屬性。 在嘗試查找指令碼時，也會考慮這些超類型。 資源超級類型的優點是它們可以形成預設資源類型的資源層次結構 `sling/servlet/default` （由預設servlet使用）是根。

資源的資源超級類型可以用兩種方式定義：

* 的 `sling:resourceSuperType` 資源的屬性。
* 的 `sling:resourceSuperType` 節點的屬性 `sling:resourceType` 點。

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

類型層次結構：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 為 `/y`
   * 層次結構為 `[ c, a, <default>]`

這是因為 `/y` 的 `sling:resourceSuperType` 財產 `/x` 不是，因此其超類型從其資源類型中獲取。

#### 無法直接調用Sling指令碼 {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接調用指令碼，因為這會打破REST伺服器的嚴格概念；你會把資源和陳述混為一談。

如果直接調用表示法（指令碼），則會在指令碼內隱藏資源，因此框架(Sling)不再知道它。 因此，您會丟失某些功能：

* 自動處理除GET之外的http方法，包括：
   * POST、PUT、DELETE，使用sling預設實現處理
   * 的 `POST.jsp` 指令碼 `sling:resourceType` 位置
* 您的代碼體系結構不再像原來那樣乾淨，也不再像原來那樣清晰；對於大規模開發至關重要

### Sling API {#sling-api}

這使用Sling API包， `org.apache.sling.*`和標籤庫。

### 使用sling:include引用現有元素 {#referencing-existing-elements-using-sling-include}

最後考慮的是需要引用指令碼中的現有元素。

更複雜的指令碼（聚合指令碼）可能需要訪問多個資源（例如導航、邊欄、腳注、清單元素），並通過包括 *資源*。

要執行此操作，可以使用 `sling:include("/<path>/<resource>")` 的子菜單。 這將有效地包括引用資源的定義。

## OSGi {#osgi}

OSGi（開放服務網關計畫）定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Java動態模組系統）。 OSGi容器允許您將應用程式拆分為各個模組（是包含附加元資訊的jar檔案，在OSGi術語中稱為捆綁包），並通過以下方式管理它們之間的交叉依賴關係：

* 在容器內實施的服務
* 容器與應用程式之間的合同

這些服務和合同提供了一種使各個元素能夠動態發現彼此以進行協作的體系結構。

然後，OSGi框架將為您提供這些捆綁包的動態載入/卸載、配置和控制 — 無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在 [OSGi網站](https://www.osgi.org)。
>
>特別是，他們的「基礎教育」頁面包含一系列演示和教程。

此體系結構允許您擴展Sling與應用程式特定模組。 吊帶，因AEM此使用 [阿帕奇費利克斯](https://felix.apache.org/) OSGi的實施。 它們都是OSGi框架內運行的OSGi捆綁包的集合。

這使您能夠對安裝中的任何軟體包執行以下操作：

* 安裝
* 啟動
* 停止
* 更新
* 解除安裝
* 查看當前狀態
* 訪問有關特定捆綁包的更多詳細資訊（如符號名稱、版本、位置等）

請參閱 [配置OSGiAEM以as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) 的子菜單。

## 儲存庫內的結構 {#structure-within-the-repository}

以下清單概述了在儲存庫中將看到的結構。

* `/apps`  — 與申請相關；包括特定於您網站的元件定義。 開發的元件可基於以下位置提供的現成元件 `/libs/core/wcm/components`。
* `/content`  — 為網站建立的內容。
* `/etc`
* `/home`  — 用戶和組資訊。
* `/libs`  — 屬於核心的庫和定AEM義。 中的子資料夾 `/libs` 表示出廠設AEM置。 中的內容 `/libs` 不能修改。 您網站的特定功能應在 `/apps`。
* `/tmp`  — 臨時工作區。
* `/var`  — 系統更改和更新的檔案；如審計日誌、統計、事件處理。

>[!CAUTION]
>
>對此結構或其中的檔案進行更改時應謹慎。 確保您完全瞭解所做的任何更改的含義。
>
>您不能更改 `/libs` 路徑。 對於配置和其他更改，請從 `/libs` 至 `/apps` 在 `/apps`。
