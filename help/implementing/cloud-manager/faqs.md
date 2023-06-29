---
title: Cloud Manager 常見問題集
description: 在AEMas a Cloud Service中尋找Cloud Manager常見問題的解答。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 62%

---


# Cloud Manager 常見問題集 {#cloud-manager-faqs}

本檔案提供AEMas a Cloud Service中Cloud Manager常見問題的解答。

## 是否可能將Java™ 11與Cloud Manager組建一起使用？ {#java-11-cloud-manager}

可以。新增 `maven-toolchains-plugin` 有正確的Java™ 11設定。

本流程的記錄在[此處](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started)。

如需範例，請參閱 [wknd 專案範例專案計劃碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

## 從Java™ 8切換到Java™ 11後，我的組建失敗並出現有關maven-scr-plugin的錯誤。 該怎麼辦？ {#build-fails-maven-scr-plugin}

嘗試將組建從Java™ 8切換到11時，您的AEM Cloud Manager組建可能會失敗。 如果您遇到以下錯誤，則必須移除 `maven-scr-plugin` 並將所有OSGi註解轉換為OSGi R6註解。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

如需有關如何移除此外掛程式的說明，請參閱 [此處](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/).

## 從Java™ 8切換到Java™ 11後，我的組建失敗並出現有關RequireJavaVersion的錯誤。 該怎麼辦？ {#build-fails-requirejavaversion}

對於 Cloud Manager 組建，`maven-enforcer-plugin` 可能由於此錯誤而失敗。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

這是一個已知問題，原因在於Cloud Manager使用不同版本的Java™來執行maven命令而不是編譯程式碼。 只需忽略您的 `maven-enforcer-plugin` 設定中的 `requireJavaVersion`。

## 程式碼品質檢查失敗，部署無法進行。 是否有辦法略過這項檢查？ {#deployment-stuck}

可以。 除了安全評等之外，所有計劃碼品質檢查失敗都是非關鍵性量度，因此可透過擴展結果 UI 中的專案將其視為部署管道的一部分而略過。

具有[部署管理員、專案管理員或企業所有者](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)角色的使用者可覆寫此問題，這種情況下，管道會繼續進行，或者他們可接受此問題，這種情況下，管道會因失敗而停止。

如需詳細資訊，請參閱文件：[計劃碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate)和[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines)。

## 我是否能將 SNAPSHOT 用於 Maven 專案的版本？ {#use-snapshot}

可以。 對於開發人員部署，Git 分支 `pom.xml` 檔案在 `<version>` 值的末尾必須包含 `-SNAPSHOT`。

當版本未變更時，此值允許仍安裝後續部署。 在開發人員部署中，不會為 Maven 組建新增或產生自動版本。

您還可以將版本設定為 `-SNAPSHOT`，以用於測試和生產組建或部署。Cloud Manager 會自動設定適當的版本編號並在 Git 中為您建立標記。如有需要，可稍後參考此標籤。

有關版本處理的進一步詳情如下 [在此處記錄](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

## 套件和套裝的版本設定如何用於測試和生產部署？ {#snapshot-version}

在測試和生產部署中，會自動產生版本為 [在此處記錄](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

對於測試和生產部署中的自訂版本設定，請設定適當的三部分 Maven 版本，例如 `1.0.0`。 每次部署到生產時，都需增加版本。

Cloud Manager 會自動將其版本新增到測試和生產組建，並建立 Git 分支。不需要特別設定。如果您未依照先前所述設定Maven版本，部署仍會成功，且會自動設定版本。

## 對於 Cloud Manager 部署，我的 Maven 組建失敗，但它在本機建置且沒有出現錯誤。有什麼問題嗎？ {#maven-build-fail}

如需更多詳細資訊，請參閱[此 Git 資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 如果 Cloud Manager 部署在 AEM as a Cloud Service 中的部署步驟失敗，我該怎麼辦？ {#cloud-manager-deployment-cloud-service}

部署失敗的最常見原因是 `sling-distribution-importer` 使用者權限不足。在這種情況下，Cloud Manager 部署期間部署步驟會失敗，並會產生如下錯誤。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

`sling-distribution-importer`使用者需要 `ui.content package` 中定義內容路徑的額外權限 。此規則通常表示您必須為兩者新增許可權 `/conf` 和 `/var`.

解決方案是新增 [RepositoryInitializer OSGi 設定](/help/implementing/deploying/overview.md#repoint)指令碼到您的應用計劃部署套件中，以為 `sling-distribution-importer` 使用者新增 ACL。

在先前的錯誤範例中，`myapp-base.ui.content-*.zip`套件包括 `/conf` 和 `/var/workflow` 底下的內容。為了部署成功， `sling-distribution-importer` 需要在這些路徑下。

以下是為 `sling-distribution-importer` 使用者新增額外權限的 [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) OSGi 設定範例。設定在 `/var` 底下新增權限。這類設定必須新增到 `/apps/myapp/config` 底下的應用計劃套件中 (其中 myapp 是儲存應用計劃計劃碼的檔案夾)。

## 我的 Cloud Manager 部署在 AEM as a Cloud Service 中的部署步驟失敗，並且我已經新增了 RepositoryInitializer OSGi 設定。我還能怎麼做？ {#build-failures}

如果[新增 RepositoryInitializer OSGi 設定](#cloud-manager-deployment-cloud-service)沒有解決錯誤，可能是由於以下其他問題造成的。

* 由於錯誤的 OSGi 設定破壞了現成的服務，部署可能會失敗。
   * 在部署期間檢查記錄，以便檢視是否有任何明顯的錯誤。

* 由於Dispatcher或Apache設定錯誤，部署可能會失敗。
   * 請務必使用SDK中包含的Docker影像在本機測試您的Apache和Dispatcher設定。
   * 另請參閱 [雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery) 有關如何設定Dispatcher Docker容器以輕鬆進行本機測試。

* 在將內容套件 (Sling 指派) 從作者複製到發佈執行個體期間，部署可能會因某些其他錯誤而失敗。
   * 請依照下列步驟操作，以便在本機設定上模擬問題。
      1. 使用最新的 AEM SDK jar 在本機安裝作者和發佈執行個體。
      1. 登入作者執行個體。
      1. 前往&#x200B;**工具** -> **部署** -> **指派**。
      1. 指派作為計劃碼庫 一部分的內容套件，並查看佇列是否因錯誤而阻塞。

## 我無法使用 aio 命令設定變數。該怎麼辦？ {#set-variable}

您可能會收到 `403` 嘗試透過以下方式列出或設定管道變數時出現以下錯誤 `aio` 命令。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在此情況下，執行這些命令的使用者必須新增至 **部署管理員** Admin Console中的角色。

如需更多詳細資訊，請參閱 [API 權限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)。
