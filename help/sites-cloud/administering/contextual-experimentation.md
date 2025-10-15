---
title: AEM as a Cloud Service中的內容實驗
description: 瞭解如何使用實驗外掛程式，將實驗功能新增至您的網站。
feature: Administering
role: Admin
source-git-commit: 66ee08babae1f6640158260af051f8ad5f9bde85
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 0%

---

# AEM as a Cloud Service中的內容實驗 {#contextual-experimentation}

>[!NOTE]
>目前，內容實驗功能僅可透過Beta版計畫使用。 請聯絡Adobe支援或您的帳戶管理員以取得此測試版計畫的存取權。

實驗是測試您網站的設計、功能和程式碼的作法，目的是改善效能並使您的網站更有效率、更簡化。 這是透過變更內容或功能、將結果與先前版本進行比較以及挑選具有可衡量效果的改善專案來達成。

若做法正確，這是改善轉換、參與和訪客體驗的強大模式。 一般而言，在尋求採用此做法時，需要避免幾個問題：

* **太少**：大多數公司沒有足夠的實驗，當他們進行實驗時，他們嘗試的流量太少，無法取得有意義的結果。
* **太慢**：許多實驗架構會讓網站速度變慢，以致於潛在的新轉換無法彌補轉譯速度緩慢而造成的流量損失和跳出數。
* **太複雜**：如果設定新實驗花費太多時間，則會執行較少的實驗。

對於在Adobe Experience Manager上執行的網站，有「現成」的&#x200B;**實驗外掛程式**，可讓開發人員在其網站上新增實驗功能。 三件事讓此方法與其他實驗架構不同：

* 使用作者已熟悉的工具可輕鬆設定測試，且不需要個別登入。
* 它可深入整合至AEM傳送系統，不會減慢網站的速度，且可復原程式碼和內容的變更。
* 它可讓您測試簡單的內容變更，以及涵蓋設計、功能和程式碼的實驗。

## 開始之前 {#before-start}

實驗外掛程式用於[Edge Delivery Services](/help/edge/overview.md)的內容中，因此您需要Github帳戶、SharePoint或Google Drive之類的內容存放庫，此外也需要[AEM Sidekick](https://www.aem.live/docs/sidekick)。 另請參閱[快速入門 — Universal Editor開發人員教學課程頁面](https://www.aem.live/developer/tutorial)和[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)。

完成所有設定後，**請觀看此影片** （標題為[立即實驗](https://business.adobe.com/tw/products/experience-manager/sites/testing-optimization.html)），以簡短示範實驗外掛程式的運作方式。

## 常用詞語 {#frequently-used-terms}

在依照指南的其餘內容設定您的第一個實驗之前，您應該熟悉一些常用的術語：

* **控制**：執行實驗之前的體驗。 所有實驗都會嘗試測試和示範控制體驗的改善。
* **Challenger**：與控制體驗不同的體驗，並且已針對控制體驗或搭配控制體驗「測試」。
* **變體**：控制項和挑戰者都是實驗的變體。
* **統計顯著性**：評估您的挑戰者是否真的比控制項好。 計算統計顯著性可讓您排除運氣，並專注於具有實際效果的結果。

## 實驗變體和一般工作流程 {#experiment-variants-workflow}

一般而言，設定實驗時，您將使用原先存在的頁面作為控制頁面。 接著您將建立挑戰者頁面，取代部分訪客的控制頁面。 在挑戰者頁面中，您可以測試內容變體、不同頁面配置、call-to-action (CTA)等不同專案。 您可以透過在控制頁面中新增中繼資料引數（請參閱下文）來設定這些實驗變體。

[作業遙測服務](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)接著會收集資料，例如，控制頁面與挑戰者頁面的訪客數。 然後您可使用這些資料為您的網站選取必要的改善專案。 只要您維持在網站既定的設計語言範圍內，並使用現有的區塊功能，您就應該能夠設定實驗變體，並在幾分鐘內將其傳送至生產環境。

>[!NOTE]
>請記得，外掛程式不會使用或持續使用任何可能導致使用者身分識別的一般使用者資料。 使用AEM as a Cloud Service[中使用](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)作業遙測服務的預設設定時，不需要使用者選擇加入或Cookie同意。

### 實驗識別碼 {#experiment-identifier}

開始之前，每個實驗都應該有自己的識別碼來追蹤和分析目的。 一個好的起點是為您的實驗想出一個好的唯一識別碼，將是「Experiment ID」。 實驗通常是線性編號，或相關至問題追蹤器或管理系統中的問題ID。 實驗ID通常使用專案的前置詞，例如： `OPT-0134`、`EXP0004`或`CCX0076`。

### 建立您的挑戰者頁面 {#create-challenger-page}

根據慣例，建議在您的`/experiments/ folder`中建立實驗識別碼為小寫的資料夾（例如/experiments/ccx0076/）。 挑戰者變體的所有頁面都位於此資料夾中。 您可在本機存放庫中建立此資料夾，例如Sharepoint或Goggle Drive。

您的實驗資料夾應如下所示：

![個實驗 — 資料夾](/help/sites-cloud/administering/assets/experiments-folder.png)

建立資料夾後，將控制頁面副本放入該資料夾，並將變更套用至您要作為實驗變體的一部分測試的頁面（請參閱以上影片）。 例如，假設我們要在網站上執行實驗的網站上有以下頁面：

![control-page](/help/sites-cloud/administering/assets/control-page.png)

您放置在`experiments/<experiment-id>`資料夾中的挑戰者復本可能如下所示：

![挑戰者頁面](/help/sites-cloud/administering/assets/challenger-page.png)

使用Sidekick預覽並發佈挑戰者頁面，以及當您完成編寫挑戰者頁面時。 已發佈挑戰者的URL將用於下一節 — 設定實驗。

### 設定實驗 {#configure-experiment}

只要挑戰者頁面已準備好移轉，您就需要返回「控制」頁面，並新增表示該頁面現在是測試一部分的中繼資料。

實驗變體需要新增兩個中繼資料列。

* **實驗**：包含實驗識別碼。

* **實驗變體**：包含此頁面所有挑戰者的URL，如果您有多個挑戰者，請用分行符號分隔。

請參閱下列範例：

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

對於每個實驗，流量會在所有變體（控制項和挑戰者）之間分割，並自動設定為偶數分佈。 因此，如果您有一個挑戰者，控制項和挑戰者之間會自動有平均50/50的分割。 如果您有兩個挑戰者，您將會自動看到三分之一流量分配給控制，以及每個挑戰者等等。

您可以透過設定中繼資料來覆寫流量分割。 如需有關如何自訂實驗中使用的中繼資料的詳細資訊，請參閱下列[頁面](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring)。

### 預覽和預備您的實驗變體 {#preview-stage-experiment}

當您準備好預覽和準備實驗時，請從左上角的側踢按一下預覽。 每當您預覽具有執行中實驗的頁面時，都會在`.aem.page`預覽環境中看到實驗覆蓋。 實驗覆蓋可讓您在實驗變體之間切換，並提供流量資料。

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

測量每個變體有效性的資料收集是以AEM as a Cloud Service[中的](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)作業遙測服務為基礎。

### 將您的實驗變體傳送到生產環境 {#production-experiment}

選取實驗頁面，然後從Side-kick中按一下「發佈」 ，將控制項和挑戰者變體都推上線。

### 使用案例範例 {#use-case-examples}

以下是實驗變體的幾個使用案例範例。 一般而言，基本工作流程將與上述工作流程類似，對每個使用案例會有特定變更（例如挑戰者頁面數量或中繼資料變更）。

#### 全頁實驗 {#full-page}

您可以使用完整頁面實驗，來測試同一頁面的兩個變體之間。 這是a/b測試的全頁變體，您有控制項和挑戰者頁面。 您將以不同型別的內容取代挑戰者變體中「原始」控制項的整個內容。 請記住，客戶流量預設會平均分割(50/50)，但如有需要，您可以建立自訂分割。

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## 其他考量 {#other-considerations}

以下是您使用內容實驗時應考量的其他幾個方面。

### 轉換 {#conversion}

實驗已設定為處理轉換（追蹤頁面上的可點按元素）。 必須針對下列專案定義所有實驗：

* 實驗型別
* 實驗將套用的體驗區塊
* 實驗將包含多少變體
* 每個變體的組成為何

### 請確定實驗變體未編制索引 {#experiment-not-indexed}

執行實驗時，通常最佳作法是從Sitemap中排除變體，並確保搜尋引擎不會將其編制索引。 這是因為變體頁面可能會被視為重複的內容，並對SEO造成負面影響。

您可以使用下列兩種方法其中之一來達成此目的：

* 如果您將所有實驗集中在專用的資料夾，例如`/experiments`：請確定您的大量`metadata.xlsx`工作表包含以`/experiments/**`為路徑的列，以及值為`noindex`、`nofollow`的Robots欄。
* 如果您保留具有一般內容的實驗控制項和變體：請在每個變體的頁面中繼資料中新增Robots專案，值為`noindex`， `nofollow`。

## 開發人員和技術資源 {#dev-resources}

Adobe Experience Manager使用[作業遙測]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)

)，收集必要的操作資料，以發現並修正Adobe Experience Manager支援之網站的功能和效能問題。 操作遙測資料可用於診斷效能問題。 作業遙測會透過取樣來保留訪客的隱私權（僅會監視所有頁面檢視的一小部分）。

### 隱私策略 {#privacy-experimentation}

AEM as a Cloud Service[中的](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)作業遙測服務是專為保留訪客隱私權及最小化資料收集而設計。 身為訪客，這表示Adobe不會嘗試收集您的個人資訊或可追蹤回您的資訊。 身為網站操作者，請檢閱以下收集的資料專案以瞭解其是否需要同意。
AEM作業遙測不使用任何使用者端狀態或ID （例如Cookie或`localStorage`、`sessionStorage`或類似專案）來收集使用量度。 資料是透過`Navigator.sendBeacon`呼叫以透明方式提交，而非透過畫素或類似技術提交。 裝置或個人無法透過其IP位址、使用者代理字串或任何其他資料進行「指紋識別」，以擷取取樣資料。

不允許將任何個人資料新增至作業遙測資料收集，且作業遙測資料不得用於超出絕對必要範圍的使用案例。

### 常見問題 {#faq}

以下是常見問題集清單：

問：我可以調整實驗變體之間的分割比例（例如控制項為10%，挑戰者為90%）嗎？

可以，分割比率可透過[中繼資料](#configure-experiment)設定。

問：我可以在文字和影像上實驗嗎？

可以，變體可以是完全不同的頁面，因此您甚至可以測試版面變更。
