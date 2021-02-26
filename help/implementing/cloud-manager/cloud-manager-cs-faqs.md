---
title: Cloud Manager -Cloud Services常見問答
seo-title: Cloud Manager常見問答集
description: 請參閱Cloud Manager以取得Cloud Services常見問答，以取得一些疑難排解提示
seo-description: 請依照本頁取得有關Cloud Manager -Cloud Services常見問答集的解答
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Cloud Manager常見問題{#cloud-manager-faqs}

以下部分提供有關Cloud Manager的常見問題的解答，以供Cloud Services使用。

## Java 11是否可搭配Cloud Manager組建使用？{#java-11-cloud-manager}

嘗AEM試將Java 8版本轉換為11版本時，Cloud Manager版本會失敗。 問題可能有許多原因，最常見的原因如下：

* 如[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)所述，新增具有正確Java 11設定的maven-toolchains-plugin。  例如，請參閱[wknd範例專案程式碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果您遇到以下錯誤，則需要刪除`maven-scr-plugin`的使用，並將所有OSGi注釋轉換為OSGi R6注釋。 如需指示，請參閱[此處](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 對於Cloud Manager構建版本，maven enforcer插件失敗，錯誤為`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 這是已知問題，因為Cloud Manager使用不同版本的Java來執行maven命令，而不是編譯代碼。 目前，請從maven-enforcer-plugin組態中省略`requireJavaVersion`。

## 我們的部署因程式碼品質檢查失敗而卡住。 有辦法繞過這張支票嗎？{#deployment-stuck}

除&#x200B;*安全性評分*&#x200B;以外的所有程式碼品質失敗都是非關鍵度量，因此可以透過展開結果UI中的項目來略過這些錯誤。

具有[部署管理員、項目經理或業務所有者](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)角色的用戶可以覆蓋問題，在這種情況下，管線將繼續進行，或者他們可以接受問題，在這種情況下，管線將因故障而停止。  有關詳細資訊，請參見[運行管線時的三層門。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)


## 我們是否允許在Maven項目版本中使用SNAPSHOT? 套件和捆綁jar檔案的版本控制如何適用於舞台和生產部署？{#snapshot-version}

請參閱以下案例，以瞭解用於舞台和生產部署的軟體包和捆綁jar檔案的版本修訂：

1. 對於開發人員部署，Git分支`pom.xml`檔案必須在`<version>`值結尾處包含`-SNAPSHOT`。 如此可讓後續部署版本未變更，仍可安裝。 在開發人員部署中，不會為Maven Build新增或產生任何自動版本。

1. 在「階段」和「生產」部署中，會根據[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)的說明產生自動版本。

1. 對於舞台和生產部署中的自定義版本，請設定3個部件正確的版本，如`1.0.0`。 每次您必須進行其他部署至生產環境時，都會增加版本。

1. Cloud Manager會自動將其版本新增至「舞台(Stage)」和「生產(Production)」組建，甚至會建立Git分支。 不需要特殊配置。 如果跳過上述步驟3，部署仍可正常運作，而且會自動設定版本。

1. 如果您將版本保留在`-SNAPSHOT`的「舞台(Stage)」和「生產(Production)」組建或部署版本中，則沒有問題。 Cloud Manager會自動設定正確的版本號碼，並在Git中為您建立標籤。 如有需要，此標籤可在稍後參考。

1. 如果您想在「開發」環境中試用一些實驗性程式碼，可以建立新的Git分支，並設定管線以使用該不同的分支。 當部署開始失敗，而且您想要測試舊版程式碼，以檢視程式碼何時中斷時，這個功能會很有用。

   下面的Git命令針對特定的預存提交`485548e4fbafbc83b11c3cb12b035c9d26b6532b`建立名為&#x200B;*testbranch1*&#x200B;的遠程分支。  此特殊分支可用於Cloud Manager，而不會影響任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   如需詳細資訊，請參閱[Git檔案](https://git-scm.com/book/en/v2/Git-Internals-Git-References)。

   如果以後要刪除測試分支，請使用delete命令：

   `git push origin --delete testbranch1`

## Maven組建在Cloud Manager部署中失敗，但在本機建置時未出現錯誤。 如何除錯？{#maven-build-fail}

如需詳細資訊，請參閱[Git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 如果Cloud Manager部署在部署步驟中作為Cloud Service環境失敗，AEM該怎麼辦？{#cloud-manager-deployment-cloud-service}

部署失敗最常見的原因是&#x200B;*sling-distribution-importer*使用者的權限不足。
請參閱以下範例，瞭解問題、原因和解決方案：

**問**
題在部署Cloud Manager時，將部署步AEM驟作為Cloud Service環境失敗，並出現以下錯誤。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importer使用者需要針對ui.content套件中定義的內容路徑擁有額外權限。  這通常表示我們需要新增/conf和/var的權限。

**解**
決方案解決方案是將 [RepositoryInitializer OSGi ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) configurationscript新增至您的應用程式部署套件，以新增sling-distribution-importer使用者的ACL。在上述範例錯誤中，myapp-base.ui.content-*.zip套件包含`/conf`和`/var/workflow`下的內容。 為了讓部署不失敗，我們需要在這些路徑下新增sling-distribution-importer的權限。
以下是其中一個此類OSGi組態的[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config)範例，新增sling-distribution-importer使用者的其他權限。  此設定會在/var下新增權限。  [1]下方的此xml檔案必須新增至`/apps/myapp/config`下方的應用程式套件（其中myapp是儲存您應用程式碼的資料夾）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. 如果&#x200B;*sling-distribution-importer*&#x200B;不是原因，則部署可能會因為OSGi組態錯誤而失敗，而中斷了包裝盒服務。 在部署期間檢查記錄檔，以查看是否有明顯的錯誤。

1. 部署可能因為錯誤的調度程式或Apache配置而失敗。 請務必使用SDK中包含的Docker影像，在本機測試您的Apache組態和Dispatcher組態。 請參閱Cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)中的[Dispatcher，瞭解如何設定dispatcher Docker容器以方便進行本機測試。

1. 部署可能會失敗，因為從作者複製內容套件(sling distribution)至發佈例項時，會發生其他故障。

   請參閱以下步驟，在本機設定中模擬此動作：

   * 安裝作者和發佈例項(使用最新AEM的SDK Jar)
   * 登入「作者」例項
   * 前往&#x200B;**Tools** -> **Deployment** -> **Distribution**
   * 散發屬於程式碼基底的內容封裝，並查看佇列是否因錯誤而遭到封鎖

## 無法透過aio雲端管理器設定變數，以設定管道變數。 如何除錯這些問題？{#set-variable}

如果您嘗試透過類似下列命令的命令列出或設定管道變數時遇到`403`錯誤，則需要在Admin Console中新增為&#x200B;*Deployment Manager* Cloud Manager產品角色。\
如需詳細資訊，請參閱[API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)。

相關命令和錯誤：

`$ aio cloudmanager:list-pipeline-variables 222`

*錯誤*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*錯誤*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*錯誤*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
