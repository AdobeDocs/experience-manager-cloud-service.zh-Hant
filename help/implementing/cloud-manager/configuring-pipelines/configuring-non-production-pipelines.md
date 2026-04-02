---
title: 新增非生產管道
description: 瞭解如何新增非生產管道，以在部署到生產環境之前測試計畫碼的品質。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7663af90b17e4b9d9567041c3bed8e20465c87d9
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 21%

---


# 新增非生產管道 {#configuring-non-production-pipelines}

在Cloud Manager UI中設定方案並建立至少一個環境後，您可以新增非生產管道。 這些管道可讓您在部署到生產環境之前測試計畫碼品質。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定非生產管道。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增一個全新非生產管道 {#adding-non-production-pipeline}

在您設定方案並在Cloud Manager UI中建立至少一個環境後，您可以新增非生產管道。 在部署到生產環境之前，使用這些管道來測試計畫碼品質。

**若要新增非生產管道：**

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在「**快速存取**」區段中，按一下「**Experience Manager**」。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。
1. 在「**我的程式**」控制台中，按一下某個程式。
1. 在左側面板中，按一下&#x200B;**管道**。
1. 在&#x200B;**管道**&#x200B;頁面的右上角附近，按一下&#x200B;**新增管道** > **新增非生產管道**。

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**新增非生產管道**&#x200B;對話方塊的&#x200B;**設定**&#x200B;索引標籤上，選取您要建立的下列非生產管道之一：

   * **程式碼品質管道** — 建立在GIT分支上建置程式碼、執行單元測試和評估程式碼品質的管道，而不部署至環境。
   * **部署管道** — 建立管道，用於建置程式碼、執行單元測試、評估程式碼品質，以及部署到非生產環境。

   ![新增非生產管道對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 在&#x200B;**管道設定**&#x200B;區段的&#x200B;**非生產管道名稱**&#x200B;欄位中，輸入非生產管道的說明。
1. 在&#x200B;**部署選項**&#x200B;區段下，選取您要使用的下列部署觸發程式之一：

   * **手動** - 讓您能手動啟動管道。
   * **在 Git 變更時** - 當認可版本新增到所設定的 Git 分支時啟動管道。 使用此選項，您仍然可以在必要時手動啟動管道。

1. 選取您要使用的&#x200B;**重要量度失敗行為**。

   * **每次都詢問** - 此行為是預設設定，要求對任何重要失敗進行手動介入。
   * **立即失敗** - 如果選取，則每當重要失敗發生時，會取消管道。它基本上會模擬使用者手動拒絕每個失敗。
   * **立即持續** - 如果選取，則每當重要失敗發生時，管道會自動繼續。它基本上會模擬使用者手動核准每次失敗。

1. 按一下「**繼續**」。

1. 您用於完成非生產管道設定的剩餘步驟，取決於您選擇使用的原始碼型別。
在&#x200B;**新增非生產管道**&#x200B;對話方塊的&#x200B;**Source程式碼**&#x200B;索引標籤上，選取非生產管道應處理的程式碼型別。

   * **[我正在使用完整棧疊代碼](#full-stack-code)**
   * **[我正在使用目標部署](#targeted-deployment)**

   如需有關管道型別的詳細資訊，請參閱[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。


### 我使用完整棧疊計畫碼 {#full-stack-code}

完整棧疊計畫碼管道同時部署包含一個或多個AEM伺服器應用程式以及HTTPD/Dispatcher配置的後端和前端計畫碼構建。

>[!NOTE]
>
>如果所選環境存在完整堆疊程式碼管道，則此選項會停用。

若要完成完整棧疊計畫碼非生產管道的設定，請執行以下操作：

1. 在&#x200B;**Source程式碼**&#x200B;區段中，定義下列選項。

   * **合格的部署環境** — 僅當您編輯非生產管道時可用。 如果您的管道是部署管道，則必須選擇它應該部署到哪些環境。
   * **存放庫** — 從下拉式清單中，選擇管道用作其來源的Git存放庫。 Cloud Manager會從您在此選擇的存放庫建置程式碼。

     >[!TIP]
     > 
     >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，以便了解如何在 Cloud Manager 中新增和管理存放庫，

   * **Git分支** — 從下拉式清單中，選擇管道建置應在所選存放庫中的哪個分支。 預設為 `main`。 管道使用所選分支作為構建和部署的來源。 如有必要，請按一下[重新整理]&#x200B;**&#x200B;**&#x200B;來更新所選存放庫的可用分支清單。 如果最近建立的分支未出現在清單中，請使用此選項。
   * **建置策略**
      * **完整組建** — 每次都會建置存放庫中的所有模組
      * Beta **智慧型組建** — 僅建置自上次認可後已變更的模組。<br>進一步瞭解[在非生產管道中使用Smart Build](#about-smart-build-non-production-pipeline)。

        >[!IMPORTANT]
        >
        >智慧型組建僅適用於計畫碼品質管道和開發完整棧疊計畫碼部署管道。

   * **忽略Web層設定**&#x200B;核取方塊 — 勾選後，管道不會部署您的Web層設定。

1. 在&#x200B;**管道**&#x200B;區段中，如果您的管道是部署管道，您可以選擇執行測試階段。 確認您希望在此階段啟用的選項。如果沒有選取任何選項，則在管道執行期間不會顯示測試階段。

   * **產品功能測試** — 針對開發環境執行[產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。
   * **自訂功能測試** — 針對開發環境執行[自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。
   * **自訂UI測試** — 執行自訂應用程式的[自訂UI測試](/help/implementing/cloud-manager/ui-testing.md)。
   * **體驗稽核** — 執行[體驗稽核](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![完整堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以[管理您的管道]&#x200B;(managing-pipe)
lines.md) （位於&#x200B;**方案總覽**&#x200B;頁面上的&#x200B;**管道**&#x200B;卡上）。

### 我正在使用目標部署 {#targeted-deployment}

目標部署只會為AEM應用程式的選定部分部署程式碼。 在這種部署中，您可以選擇&#x200B;**包含**&#x200B;下列其中一個型別的程式碼：

![目標部署選項](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **前端計畫碼** — 為AEM應用計畫的前端設定JavaScript和CSS。
   * 有了前端管道，給前端開發者更多的獨立性，可以加快開發進程。
   * 請參閱文件[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此程序的工作原理以及需要注意的一些注意事項，以充分發揮此程序的潛力。
* **網頁層設定** — 設定Dispatcher屬性，以儲存、處理及傳送網頁給使用者端。
   * 如需詳細資訊，請參閱檔案[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所選環境存在 Web 層程式碼管道，則此選項會停用。
   * 如果完整棧疊管道已部署到環境，您仍然可以為該同一環境建立Web層配置管道。 若您這麼做，Cloud Manager會忽略完整棧疊管道中的網頁層設定。

     >[!NOTE]
     >
     >私人存放庫不支援 Web 層和設定管道。請參閱[在Cloud Manager中新增私人存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，以取得詳細資訊和完整的限制清單。

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. 在&#x200B;**Source程式碼**&#x200B;區段下，定義下列選項：

   * **存放庫** — 此選項會定義非生產管道應該從哪個GIT存放庫擷取程式碼。

     >[!TIP]
     > 
     >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，以便了解如何在 Cloud Manager 中新增和管理存放庫，

   * **Git分支** — 此選項會定義所選管道中應該從哪個分支擷取程式碼。 輸入分支名稱的前幾個字元，該欄位的自動完成功能。會尋找相符的分支以幫助您進行選取。
   * **程式碼位置** - 此選項會定義管道應從所選存放庫的分支中擷取程式碼的路徑。

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. 如果您已啟用體驗稽核，請按一下「**繼續**」以前往「**體驗稽核**」標籤，您可以在其中定義應一律包含在體驗稽核中的路徑。

   * 如果您已啟用&#x200B;**體驗稽核**，請參閱檔案[體驗稽核](/help/implementing/cloud-manager/reports/report-experience-audit.md)以瞭解如何設定的詳細資訊。
   * 如果您沒有這麼做，請略過此步驟。

1. 按一下&#x200B;**儲存**，即可儲存管道。

管道已儲存，您現在可以在&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。


## 關於在非生產管道中使用Smart Build{#about-smart-build-non-production-pipeline}

Cloud Manager中的&#x200B;**智慧型組建**&#x200B;是非生產管道的最佳組建策略。 Smart Build會快取模組，並只重新建置自上次成功執行後已變更的模組，藉此縮短建置時間。 未變更的模組會從快取中重複使用，而只會重建已修改的模組及其相依性，進而提高反複開發工作流程的效率。

Smart Build目前僅適用於下列專案：

* 計畫碼品質管道。
* 開發完整棧疊部署管道。

>[!NOTE]
>
>啟用Smart Build後的首次執行行為類似於Full Build，因為快取是空的。

發生下列情況時，建議使用Smart Build：

* 您正在積極開發和提交頻繁的增量變更。
* 您的專案包含多個Maven模組。
* 完整組建需要相當長的時間。

有以下情況時，Smart Build並不總是理想的選擇：

* 您的組建嚴重依賴外掛程式，這些外掛程式會在Maven的相依性圖表之外執行操作。
* 每次執行都需要完整重建驗證。

### 瞭解組建效能{#smart-build-performance}

使用Smart Build的效能提升取決於幾個因素，包括：

* 專案中的模組數。
* 程式碼變更的頻率和範圍。
* 跨模組的相依性分佈。

一般而言，具有許多獨立模組的專案可以有最大的改善。

### 每個模組快取選擇退出{#smart-build-cache-optout}

Smart Build提供可讓您停用特定模組快取的精細控制項。 此功能在某些模組中相當實用：

* 使用外掛程式，例如`exec-maven-plugin`或`maven-antrun-plugin`。
* 執行Maven相依性未追蹤的檔案操作。
* 快取內容會產生不一致的結果。

### 停用模組的快取{#smart-build-disable-caching}

您可以將下列屬性新增至受影響模組的`pom.xml`：

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

此語法會強制模組在每次管道執行時重建，而其他模組會繼續受益於快取。

### 使用Smart Build時的限制和考量{#smart-build-limitations}

使用Smart Build時，請記得下列事項：

* Smart Build仰賴Maven相依性分析。
* 相依性圖表以外的變更可能不會觸發重新建置。
* 有些外掛程式可能與快取不完全相容。
* 您可以透過編輯非生產管道隨時切換回&#x200B;**完整組建**。

如果您遇到非預期的建置行為，請考慮停用特定模組的快取，或暫時將建置策略切換為&#x200B;**完整建置**。

### 疑難排解智慧型組建問題{#smart-build-troubleshoot}

| 問題 | 建議的解決方案 |
| --- | --- |
| 建置結果不一致 | ·停用受影響模組的快取。<br>·驗證外掛程式行為（尤其是`exec`/`antrun`外掛程式）。 |
| 沒有效能改善 | ·確認已執行多次（快取熱身）。<br>·檢查大多數模組是否頻繁變更。 |
| 未預期的成品或遺失的變更 | ·檢閱變更是否在Maven相依性追蹤之外。<br>·使用&#x200B;**完整組建**&#x200B;進行驗證。 |

請參閱[新增非生產管道](#adding-non-production-pipeline)以啟用智慧建置。











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## 排除Dispatcher套件 {#exclude-dispatcher-packages}

如果您想要在管道中建置Dispatcher套件，但未上傳到建置儲存，請停用發佈。 這樣做可以縮短管道的執行時間。

將下列設定新增至您的專案`pom.xml`檔案，以停用發佈Dispatcher套件。 在Cloud Manager建置容器中設定環境變數，以標幟何時忽略Dispatcher套件。 管道會讀取此旗標並據此忽略它們。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
