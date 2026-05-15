---
title: AEM as a Cloud Service中的內容實驗
description: 瞭解如何使用實驗邊欄將實驗功能新增到您的網站。
feature: Administering
role: Admin
exl-id: 420f8d5e-27f9-4081-b174-b2d7752779f7
source-git-commit: 4764d9b3343ca88e0de7506d955741e8cac2f2e1
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 2%

---

# AEM as a Cloud Service中的內容實驗 {#contextual-experimentation}

實驗是測試您網站的設計、功能和程式碼的作法，目的是改善效能並使您的網站更有效率、更簡化。 這是透過變更內容或功能、將結果與先前版本進行比較以及挑選具有可衡量效果的改善專案來達成。

若做法正確，這是改善轉換、參與和訪客體驗的強大模式。 一般而言，在尋求採用此做法時，需要避免幾個問題：

* **太少**：大多數公司沒有足夠的實驗，當他們進行實驗時，他們嘗試的流量太少，無法取得有意義的結果。
* **太慢**：許多實驗架構會讓網站速度變慢，以致於潛在的新轉換無法彌補轉譯速度緩慢而造成的流量損失和跳出數。
* **太複雜**：如果設定新實驗花費太多時間，則會執行較少的實驗。

對於在Adobe Experience Manager上執行的網站，開發人員可選擇在其網站上新增實驗功能。 三件事讓此方法與其他實驗架構不同：

* 使用作者已熟悉的工具可輕鬆設定測試，且不需要個別登入。
* 它可深入整合至AEM傳送系統，不會減慢網站的速度，且可復原程式碼和內容的變更。
* 它可讓您測試簡單的內容變更，以及涵蓋設計、功能和程式碼的實驗。

## 實驗邊欄 {#experimentation-rail}

實驗邊欄是設定實驗的主要方式。 可在[Edge Delivery Services](/help/edge/overview.md)內容或[通用編輯器](/help/implementing/universal-editor/introduction.md)中搭配您的專案使用。 因此，您將需要Github帳戶、SharePoint或Google Drive之類的內容存放庫，而且您還需要[AEM Sidekick](https://www.aem.live/docs/sidekick)外掛程式。 若要使用通用編輯器，您還需要存取[AEM as a Cloud Service環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。 另請參閱[快速入門 — Universal Editor開發人員教學課程頁面](https://www.aem.live/developer/tutorial)。

>[!WARNING]
>需要使用實驗引擎才能使用實驗功能。 在實作下列步驟之前，請確定引擎已安裝且已正確更新。 如需詳細資訊，請參閱下列[安裝頁面](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation)。

### 在Edge Delivery Services中使用AEM Sidekick設定實驗

若要存取Edge Delivery Services專案中的實驗邊欄功能，您需要[AEM Sidekick](https://www.aem.live/docs/sidekick)外掛程式。 若要設定Sidekick，請執行下列步驟：

1. 新增[AEM Sidekick擴充功能](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar)並將其釘選到您的瀏覽器中。
1. 以預覽模式開啟您的專案頁面。
1. 在AEM Sidekick列上，按一下設定圖示![設定](/help/sites-cloud/administering/assets/settings-1.png)並選取&#x200B;**新增此專案**。
1. 按一下Experimentation標籤以開啟實驗邊欄。

### 在通用編輯器中設定實驗

在設定實驗之前，請記住，您需要使用AEM網站作為內容來源，才能在通用編輯器中創作。 如有需要，您可以依照[設定AEM as a Content Source](https://www.aem.live/developer/ue-tutorial)頁面中提供的教學課程，將現有的專案轉換為內容來源的AEM Sites網站。 當您準備好在Universal Editor中設定實驗時，請遵循下列步驟：

1. 在Universal Editor中開啟專案，並檢查&#x200B;**A/B**&#x200B;圖示延伸。 如果圖示未顯示，請確認您是否已在擴充功能管理員中啟用該功能。 如果未啟用，請啟用或要求存取權。
   <!--1. Open your GitHub repository and check if the `plugins/experimention` folder exists. If not, you will need to set up the experimentation engine and MFE first (see the note above).-->
1. 將您的`fstab.yaml`設定指向您的專案設定，並將其連結至您的AEM作者執行個體。 另請參閱[將您的程式碼連線至您的內容](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)
1. 開啟您的AEM執行個體，如果您已準備好專案，請直接在Universal Editor中開啟。
1. 開啟您要執行實驗的專案和索引頁面，然後按一下頂端列上的&#x200B;**編輯**。
1. 按一下A/B圖示以開啟實驗擴充功能。

>[!NOTE]
>如果您在設定專案的實驗時遇到問題，請連絡[aem-contextual-experimentation@adobe.com](mailto:aem-contextual-experimentation@adobe.com)。

>[!NOTE]
>如需如何設定及設定實驗引擎的詳細資訊，請參閱以下[存放庫](https://github.com/adobe/aem-experimentation/tree/v2-ui)的檔案區段。

## 實驗變體和一般工作流程 {#experiment-variants-workflow}

在依照指南的其餘內容設定您的第一個實驗之前，您應該熟悉一些常用的術語：

* **控制**：執行實驗之前的體驗。 所有實驗都會嘗試測試和示範控制體驗的改善。
* **Challenger**：與控制體驗不同的體驗，並且已針對控制體驗或搭配控制體驗「測試」。
* **變體**：控制項和挑戰者都是實驗的變體。
* **統計顯著性**：評估您的挑戰者是否真的比控制項好。 計算統計顯著性可讓您排除運氣，並專注於具有實際效果的結果。

一般而言，設定實驗時，您將使用原先存在的頁面作為控制頁面。 透過使用實驗邊欄，您隨後將建立挑戰者頁面，該頁面最初是控制頁面的副本。 在挑戰者頁面中，您可以測試內容變體、不同頁面配置、call-to-action (CTA)等不同專案。 您也可以使用AI產生的變體，方法是使用實驗邊欄中的&#x200B;**產生變體**&#x200B;功能。

對於每個實驗，流量最初會在控制項和挑戰者之間按50/50的分割，但您可以視需要設定如何分割流量。 啟動實驗後，您將透過操作遙測服務接收資料。

[作業遙測服務](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)會收集資料，例如，控制頁面與挑戰者頁面的訪客數。 然後您可使用這些資料為您的網站選取必要的改善專案。 只要您維持在網站既定設計語言內並使用現有功能，您就應該能夠設定實驗變體，並在幾分鐘內將其傳送至生產環境。

>[!NOTE]
>請記得，外掛程式不會使用或持續使用任何可能導致使用者身分識別的一般使用者資料。 使用AEM as a Cloud Service[&#128279;](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)中使用作業遙測服務的預設設定時，不需要使用者選擇加入或Cookie同意。

<!--### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. -->

### 在通用編輯器中建立實驗

若要在Universal Editor中使用實驗功能，您必須先設定實驗邊欄（如上述章節所詳述），並確定您使用AEM網站作為內容來源。 完成所有設定後，請依照下列步驟操作。

### 開始在Universal Editor中編輯專案

開啟您的AEM執行個體，如果您已準備好專案，請直接在Universal Editor中開啟。 如果您尚未準備好專案，且AEM網站已設定為內容來源，請從提供的範本建立新的樣板專案。 您可以連結您的存放庫或我們的範例存放庫，以驅動它[https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation)。 另請參閱[設定AEM Sites as a Content Source](https://www.aem.live/developer/ue-tutorial)頁面。 設定專案後，請開啟專案以及您要執行實驗的索引頁面，然後按一下頂端列上的&#x200B;**編輯**。

### 啟動A/B擴充功能

按一下&#x200B;**A/B**&#x200B;圖示以開啟實驗擴充功能。 第一次使用時，介面會是空的。 按一下&#x200B;**新建**&#x200B;以開始新的實驗。

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### 設定實驗詳細資料

部分實驗值是預先定義的，如下所示：

**實驗型別**： A/B測試（目前僅支援型別）
**針對**&#x200B;最佳化：轉換（目前僅支援型別）

您也可以將實驗重新命名為較清楚描述的型別，例如`homepage-head-experiment`。

![實驗詳細資料](/help/sites-cloud/administering/assets/exp-values.png)

### 新增和編輯變體

在繼續之前，請務必瞭解上述挑戰者和變體的概念。 按一下&#x200B;**新增**&#x200B;以建立挑戰者變體：

* 您將會被帶往同一標籤中的挑戰者頁面 — 一開始只是您控制項的復本。
* 直接在內容中編輯頁面，或按一下&#x200B;**產生變數**&#x200B;以使用AI協助。
* 進行變更後，請返回擴充功能以繼續。

![Control-variant](/help/sites-cloud/administering/assets/control-variant.png)

### 定義其他屬性並儲存為草稿

在實驗邊欄中，您可以設定開始和結束日期（兩者皆為選用）。 如果未提供開始日期，則測試會在發佈後開始。 如果未提供結束日期，則測試會無限期地執行。 您也可以調整流量分割，我們建議從偶數50/50分割開始。

完成後，按一下&#x200B;**儲存** — 這會將您的實驗儲存為草稿。 請注意，實驗尚未啟用。 您可以按一下&#x200B;**返回實驗**&#x200B;以返回總覽，或者您可以停留在[編輯]介面以啟動實驗。

![草稿](/help/sites-cloud/administering/assets/draft-save.png)

### 啟動實驗

準備就緒後，按一下&#x200B;**啟動**&#x200B;以啟動實驗並發佈實驗頁面。 測試將開始收集作業遙測(RUM)資料（請參閱以下章節的詳細資訊）。

![啟動](/help/sites-cloud/administering/assets/activate.png)

### 監視和提升

實驗達到統計顯著性後，按一下&#x200B;**升級**&#x200B;將所需的變體變成新的控制項。 請記住，您可以在啟用後的任何時間點提升實驗變體，即使它未達到統計顯著性。

### 在Edge Delivery Services中搭配AEM Sidekick使用實驗

如果您已安裝AEM Sidekick，則可以直接在Edge Delivery Service中將實驗邊欄用於您的專案，而不使用通用編輯器。 功能基本上與上述A/B測試相同，請記住，您必須處於&#x200B;**預覽**&#x200B;模式才能編輯和設定測試。 完成設定測試之後，請按一下[啟動]，將控制項和挑戰者變體推上線，並開始收集遙測資料。**&#x200B;**

<!-- ### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the “Experiment ID”. Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let’s assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

<!--- The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md). -->

<!--- ### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like. -->

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

以下提供使用內容實驗時應考量的幾個方面。

### 轉換 {#conversion}

實驗已設定為處理轉換（追蹤頁面上的可點按元素）。 目前，我們支援頁面層級實驗，每頁一個實驗。

<!--### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.-->

## 開發人員和技術資源 {#dev-resources}

Adobe Experience Manager 使用[操作遙測](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)來收集操作資料，因為必須掌握這些操作資料，才能發現與修復 Adobe Experience Manager 支援之網站的功能性和效能問題。 操作遙測資料可用於診斷效能問題。 作業遙測會透過取樣來保留訪客的隱私權（僅會監視所有頁面檢視的一小部分）。

### 隱私策略 {#privacy-experimentation}

AEM as a Cloud Service[&#128279;](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)中的作業遙測服務是專為保留訪客隱私權及最小化資料收集而設計。 身為訪客，這表示Adobe不會嘗試收集您的個人資訊或可追蹤回您的資訊。 身為網站操作者，請檢閱以下收集的資料專案以瞭解其是否需要同意。
AEM作業遙測不使用任何使用者端狀態或ID （例如Cookie或`localStorage`、`sessionStorage`或類似專案）來收集使用量度。 資料是透過`Navigator.sendBeacon`呼叫以透明方式提交，而非透過畫素或類似技術提交。 裝置或個人無法透過其IP位址、使用者代理字串或任何其他資料進行「指紋識別」，以擷取取樣資料。

不允許將任何個人資料新增至作業遙測資料收集，且作業遙測資料不得用於超出絕對必要範圍的使用案例。
