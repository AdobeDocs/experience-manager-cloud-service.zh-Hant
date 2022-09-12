---
title: Cloud Manager常見問題集
description: 在AEM as a Cloud Service中尋找有關Cloud Manager最常問問題的解答。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 698ea704d821d26067e29a89b562388d7517772e
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---


# Cloud Manager常見問題集 {#cloud-manager-faqs}

本檔案提供AEMas a Cloud Service中Cloud Manager最常見問題的解答。

## Java 11是否可搭配Cloud Manager組建使用？ {#java-11-cloud-manager}

可以。 您需要新增 `maven-toolchains-plugin` 以及Java 11的正確設定。

此程式已記錄下來 [此處](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

例如，請參閱 [wknd專案範例專案程式碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## 從Java 8切換至Java 11後，我的組建因maven-scr-plugin的錯誤而失敗。 我能做什麼？ {#build-fails-maven-scr-plugin}

嘗試將組建從Java 8切換為11時，AEM Cloud Manager組建可能會失敗。 如果您遇到下列錯誤，則需要移除 `maven-scr-plugin` 並將所有OSGi注釋轉換為OSGi R6注釋。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

如需如何移除此外掛程式的指示，請參閱 [這裡。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## 從Java 8切換至Java 11後，我的組建因RequireJavaVersion錯誤而失敗。 我能做什麼？ {#build-fails-requirejavaversion}

若為Cloud Manager組建， `maven-enforcer-plugin` 可能會因此錯誤而失敗。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

這是已知問題，因為Cloud manager使用不同版本的Java來執行maven命令與編譯程式碼。 只是忽略 `requireJavaVersion` 從 `maven-enforcer-plugin` 設定。

## 程式碼品質檢查失敗，我們的部署卡住。 有辦法繞過這個檢查嗎？ {#deployment-stuck}

可以。 除了安全性評等以外，所有程式碼品質檢查失敗都是非關鍵量度，因此您可以在部署管道中擴增結果UI中的項目，以略過這些失敗。

使用 [部署經理、項目經理或業務負責人](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) 角色可以覆寫問題，在這種情況下，管道會繼續，或者他們可以接受問題，在這種情況下，管道會因失敗而停止。

查看文檔 [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate) 和 [設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines) 以取得更多詳細資訊。

## 我可以將SNAPSHOT用於Maven項目的版本嗎？ {#use-snapshot}

可以。 針對開發人員部署，Git分支 `pom.xml` 檔案必須包含 `-SNAPSHOT` 在 `<version>` 值。

這可讓版本未變更時仍安裝後續部署。 在開發人員部署中，不會針對Maven組建新增或產生任何自動版本。

您也可以將版本設為 `-SNAPSHOT` 用於預備和生產組建或部署。 Cloud Manager會自動設定正確的版本號碼，並在git中為您建立標籤。 如有需要，此標籤稍後可參考。

有關版本處理的更多詳細資訊包括 [這裡有記錄。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

## 套件和套件版本設定如何適用於預備和生產部署？ {#snapshot-version}

在預備和生產部署中，會自動產生版本，作為 [這裡有記錄。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

若要在預備和生產部署中自訂版本設定，請設定適當的三個部分Maven版本，如 `1.0.0`. 每次部署至生產環境時都增加版本。

Cloud Manager會自動將其版本新增至預備和生產組建，並建立Git分支。 不需要特殊配置。 如果您未如先前所述設定Maven版本，部署仍會成功，且版本會自動設定。

## 我的maven組建無法部署Cloud Manager，但會在本機建置，而不會發生錯誤。 怎麼了？ {#maven-build-fail}

請參閱 [此git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 以取得更多詳細資訊。

## 如果在AEM as a Cloud Service的部署步驟中Cloud Manager部署失敗，怎麼辦？ {#cloud-manager-deployment-cloud-service}

部署失敗的最常見原因是權限不足 `sling-distribution-importer` 使用者。 在此情況下，在Cloud Manager部署期間，部署步驟會失敗，並產生下列錯誤。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

此 `sling-distribution-importer` 使用者需要中定義之內容路徑的其他權限 `ui.content package`.  這通常表示您需要為兩者新增權限 `/conf` 和 `/var`.

解決方案是新增 [RepositoryInitializer OSGi配置](/help/implementing/deploying/overview.md#repoint) 指令碼到應用程式部署包，以添加 `sling-distribution-importer` 使用者。

在上一個範例錯誤中，套件 `myapp-base.ui.content-*.zip` 包含 `/conf` 和 `/var/workflow`. 為了部署成功，請 `sling-distribution-importer` 需要。

以下是 [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) 新增其他權限的OSGi設定 `sling-distribution-importer` 使用者。  設定會在 `/var`.  此類配置必須添加到以下的應用程式包 `/apps/myapp/config` （其中myapp是儲存應用程式程式碼的資料夾）。

## 在AEMas a Cloud Service的部署步驟中，我的Cloud Manager部署會失敗，而且我已新增RepositoryInitializer OSGi設定。 我還能做什麼？ {#build-failures}

若 [添加RepositoryInitializer OSGi配置](#cloud-manager-deployment-cloud-service) 未解決錯誤，可能是因為其中一個額外問題。

* 部署可能因OSGi配置錯誤而失敗，該配置會中斷現成可用的服務。
   * 在部署期間檢查記錄，以查看是否有明顯錯誤。

* 部署可能會因Dispatcher或Apache設定錯誤而失敗。
   * 請務必使用SDK中包含的Docker影像，在本機測試您的Apache和Dispatcher設定。
   * 請參閱 [雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery) 關於如何設定dispatcher Docker容器以方便進行本機測試的資訊。

* 從製作復寫到發佈執行個體的內容套件（Sling散發）期間，由於其他部分失敗，部署可能會失敗。
   * 請依照下列步驟，模擬本機設定上的問題。
      1. 使用最新的AEM SDK Jar在本機安裝製作與發佈執行個體。
      1. 登入製作例項。
      1. 前往 **工具** -> **部署** -> **分發**.
      1. 分發屬於程式碼基底的內容套件，並查看佇列是否因錯誤而遭到封鎖。

## 我無法使用aio命令設定變數。 我能做什麼？ {#set-variable}

您可能會收到 `403` 嘗試透過列出或設定管道變數時，發生下列錯誤 `aio` 命令。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在這種情況下，執行這些命令的用戶需要添加到 **部署管理員** 角色。

請參閱 [API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) 以取得更多詳細資訊。
