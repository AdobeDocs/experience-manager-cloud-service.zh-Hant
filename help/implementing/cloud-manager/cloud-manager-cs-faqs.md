---
title: Cloud Manager -Cloud Services常見問題集
seo-title: Cloud Manager常見問題集
description: 如需Cloud Services常見問題集，請參閱Cloud Manager以取得一些疑難排解秘訣
seo-description: 請詳閱本頁，了解Cloud Manager -Cloud Services常見問題集
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Cloud Manager常見問題集{#cloud-manager-faqs}

以下章節提供與Cloud Manager for Cloud Manager相關的常見問題解答，以供Cloud Services使用。

## Java 11是否可搭配Cloud Manager組建使用？{#java-11-cloud-manager}

AEM Cloud Manager組建嘗試從Java 8切換為11時失敗。 問題可能有許多原因，且最常見的原因如下：

* 以[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)的說明，新增具有Java 11正確設定的maven-toolchains-plugin。  例如，請參閱[wknd範例專案代碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果您遇到以下錯誤，則需要刪除`maven-scr-plugin`的使用，並將所有OSGi注釋轉換為OSGi R6注釋。 有關說明，請參見[here](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 對於Cloud Manager組建，Maven Enforcer外掛程式會因錯誤`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`而失敗。 這是已知問題，因為Cloud manager使用不同版本的Java來執行maven命令與編譯程式碼。 目前，請忽略maven-enforcer-plugin配置中的`requireJavaVersion`。

## 由於代碼質量檢查失敗，我們的部署卡住。 有辦法繞過這個檢查嗎？{#deployment-stuck}

除&#x200B;*安全評等*&#x200B;以外的所有程式碼品質失敗都是非關鍵量度，因此您可以展開結果UI中的項目來略過這些失敗。

[具有](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)部署管理員、項目經理或業務所有者角色的用戶可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道將因故障而停止。  如需詳細資訊，請參閱[執行管道時的三層柵](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) 。


## 是否允許在Maven項目的版本中使用SNAPSHOT? 套件和套件jar檔案的版本設定如何適用於預備和生產部署？{#snapshot-version}

請參閱下列案例，了解用於預備和生產部署的套件和套件jar檔案版本設定：

1. 若為開發人員部署，Git分支`pom.xml`檔案必須在`<version>`值的結尾處包含`-SNAPSHOT`。 這可讓後續部署，其中版本不會變更，仍可安裝。 在開發人員部署中，不會針對Maven組建新增或產生任何自動版本。

1. 在「預備」和「生產」部署中，會產生自動版本，如[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)所述。

1. 對於「預備」和「生產」部署中的自訂版本設定，請設定3個部分適當的Maven版本，如`1.0.0`。 每次您必須進行其他部署至生產環境時，都增加版本。

1. Cloud Manager會自動將其版本新增至Stage和Production組建，甚至會建立Git分支。 不需要特殊配置。 如果略過上述步驟3，部署仍可正常運作，且會自動設定版本。

1. 如果您將版本保留為`-SNAPSHOT`，以用於預備和生產組建或部署，則沒有問題。 Cloud Manager會自動設定正確的版本號碼，並在Git中為您建立標籤。 如有需要，此標籤稍後可參考。

1. 若您想在開發環境中試用一些實驗性程式碼，可以建立新的Git分支，並設定管道以使用該不同分支。 當部署開始失敗，而且您想要使用舊版程式碼進行測試，以查看其中斷的時間時，這個功能會很實用。

   下面的Git命令針對特定的預先存在的提交`485548e4fbafbc83b11c3cb12b035c9d26b6532b`建立名為&#x200B;*testbranch1*&#x200B;的遠程分支。  此特殊分支可用於Cloud Manager，不會影響任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   如需詳細資訊，請參閱[Git檔案](https://git-scm.com/book/en/v2/Git-Internals-Git-References)。

   如果以後要刪除測試分支，則使用delete命令：

   `git push origin --delete testbranch1`

## Maven組建在Cloud Manager中部署失敗，但在本機部署組建時未發生錯誤。 如何偵錯？{#maven-build-fail}

如需詳細資訊，請參閱[Git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 。

## 如果在AEM as a Cloud Environment中部署步驟中，Cloud Manager部署失敗，該怎麼辦？{#cloud-manager-deployment-cloud-service}

部署失敗的最常見原因是&#x200B;*sling-distribution-importer*使用者的權限不足。
請參閱以下範例，了解問題、原因和解決方案：

****
問題在AEM as aCloud Service環境上部署Cloud Manager期間，部署步驟會失敗，並出現下列錯誤。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importer使用者需要ui.content套件中定義之內容路徑的其他權限。  這通常表示我們需要為/conf和/var新增權限。

****
解決方案解決方案是將RepositoryInitializer OSGi  [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) configurationscript新增至應用程式部署套件，以新增sling-distribution-importer使用者的ACL。在上述範例錯誤中，myapp-base.ui.content-*.zip套件包含`/conf`和`/var/workflow`下的內容。 為了讓部署不會失敗，我們需要在這些路徑下新增sling-distribution-importer的權限。
以下是其中一個OSGi設定的範例[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config)，該設定會新增sling-distribution-importer使用者的其他權限。  此設定會在/var下新增權限。  [1]下的此xml檔案需要添加到`/apps/myapp/config`下的應用程式包中（其中myapp是儲存應用程式代碼的資料夾）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. 如果&#x200B;*sling-distribution-importer*&#x200B;不是原因，則部署可能會因OSGi配置錯誤而失敗，因為該配置會中斷現成可用的服務。 在部署期間檢查記錄，以查看是否有明顯錯誤。

1. 部署可能會因Dispatcher或Apache設定錯誤而失敗。 請務必使用SDK中包含的Docker影像，在本機測試您的Apache設定和Dispatcher設定。 請參閱雲端中的[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) ，了解如何設定Dispatcher Docker容器以方便進行本機測試。

1. 從製作復寫到發佈執行個體的內容套件（sling散發）期間，由於其他部分失敗，部署可能會失敗。

   請參閱下列步驟，在本機設定中模擬此程式：

   * 安裝製作與發佈例項(使用最新的AEM SDK jar)
   * 登入製作例項
   * 前往&#x200B;**工具** -> **部署** -> **分發**
   * 分發屬於代碼庫一部分的內容包，並查看隊列是否因錯誤而被阻止

## 無法透過aio cloud manager設定管道變數來設定變數。 如何對這些問題進行除錯？{#set-variable}

如果您嘗試透過類似以下命令的命令列出或設定管道變數時收到`403`錯誤，則需要在Admin Console中將您新增為&#x200B;*Deployment Manager* Cloud Manager產品角色。\
如需詳細資訊，請參閱[API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) 。

相關命令和錯誤：

`$ aio cloudmanager:list-pipeline-variables 222`

*錯誤*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*錯誤*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*錯誤*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
