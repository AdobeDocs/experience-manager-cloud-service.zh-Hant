---
title: Cloud Manager 常見問題集
description: 在 AEM as a Cloud Service 中尋找 Cloud Manager 常見問題的解答。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 81%

---


# Cloud Manager 常見問題集 {#cloud-manager-faqs}

本文件提供了 AEM as a Cloud Service 中 Cloud Manager 常見問題的解答。

## 是否可能將 Java™ 11 和 Cloud Manager 組建一起使用？ {#java-11-cloud-manager}

可以。使用 Java™ 11 的適當設定新增 `maven-toolchains-plugin`。

此程序已記錄 - 請參閱[專案建立精靈](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started)。

例如，請參閱[lWKND專案範例專案程式碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

## 從 Java™ 8 切換到 Java™ 11 後，我的組建失敗並出現有關 maven-scr-plugin 的錯誤。該怎麼辦？ {#build-fails-maven-scr-plugin}

嘗試將組建從 Java™ 8 切換到 11 時，您的 AEM Cloud Manager 組建可能會失敗。如果您遇到下列錯誤，則必須移除 `maven-scr-plugin` 並將所有 OSGi 註解轉換成 OSGi R6 註解。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 > [Help 1]
```

有關如何刪除此外掛程式的說明，請參閱[從 SCR 註解到 OSGI 註解](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

## 從 Java™ 8 切換到 Java™ 11 後，我的組建失敗並出現有關 RequireJavaVersion 的錯誤。該怎麼辦？ {#build-fails-requirejavaversion}

對於 Cloud Manager 組建，`maven-enforcer-plugin` 可能由於此錯誤而失敗。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

這是一個已知問題，原因在於Cloud Manager使用其他版本的Java™來執行Maven命令而不是編譯程式碼。 只需忽略您的 `maven-enforcer-plugin` 設定中的 `requireJavaVersion`。

## 程式碼品質檢查已失敗，部署無法進行。是否有辦法略過這項檢查？ {#deployment-stuck}

可以。除了安全性評等之外，所有程式碼品質檢查失敗都是非關鍵量度。 因此，可以在部署管道中，透過展開結果UI中的專案來略過這些專案。

具有[部署管理員、專案管理員或企業所有者](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)角色的使用者可以覆寫問題。 在這種情況下，配管會進行或接受問題，在這種情況下，配管會因失敗而停止。

如需詳細資訊，請參閱文件：[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate)和[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines)。

## 我是否能將 SNAPSHOT 用於 Maven 專案的版本？ {#use-snapshot}

可以。對於開發人員部署，Git 分支 `pom.xml` 檔案在 `<version>` 值的末尾必須包含 `-SNAPSHOT`。

此值允許在版本未變更時仍安裝後續部署。 在開發人員部署中，不會為 Maven 組建新增或產生自動版本。

您還可以將版本設定為 `-SNAPSHOT`，以用於測試和生產組建或部署。Cloud Manager 會自動設定適當的版本編號並在 Git 中為您建立標記。如有需要，可在稍後參照此標記。

如需版本處理的詳細資訊，請參閱[Maven專案版本處理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)。

## 套件和套裝的版本設定如何用於測試和生產部署？ {#snapshot-version}

在中繼和生產部署中，會產生自動版本 - 請參閱 [Maven 專案版本處理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)。

對於測試和生產部署中的自訂版本設定，請設定適當的三部分 Maven 版本，例如 `1.0.0`。每次部署到生產時，都需增加版本。

Cloud Manager 會自動將其版本新增到測試和生產組建，並建立 Git 分支。不需要特別設定。如果您並未依照之前的說明設定 Maven 版本，部署仍會成功，並會自動設定版本。

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

`sling-distribution-importer`使用者需要 `ui.content package` 中定義內容路徑的額外權限。此規則通常代表您必須為 `/conf` 和 `/var` 新增權限。

解決方案是新增 [RepositoryInitializer OSGi 設定](/help/implementing/deploying/overview.md#repoint)指令碼到您的應用程式部署套件中，以為 `sling-distribution-importer` 使用者新增 ACL。

在先前的錯誤範例中，`myapp-base.ui.content-*.zip`套件包括 `/conf` 和 `/var/workflow` 底下的內容。為了部署成功，需要這些路徑底下的 `sling-distribution-importer` 權限。

以下是為 `sling-distribution-importer` 使用者新增額外權限的 [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) OSGi 設定範例。設定在 `/var` 底下新增權限。這類設定必須新增到`/apps/myapp/config`下的應用程式封裝（其中`myapp`是儲存應用程式程式碼的資料夾）。

## 我的 Cloud Manager 部署在 AEM as a Cloud Service 中的部署步驟失敗，並且我已經新增了 RepositoryInitializer OSGi 設定。我還能怎麼做？ {#build-failures}

如果[新增 RepositoryInitializer OSGi 設定](#cloud-manager-deployment-cloud-service)沒有解決錯誤，可能是由於以下其他問題造成的。

* 由於OSGi設定錯誤導致現成可用的服務中斷，部署可能會失敗。
   * 在部署期間檢查記錄，以便查看是否有任何明顯的錯誤。

* 由於 Dispatcher 或 Apache 設定錯誤，部署可能會失敗。
   * 確保使用 SDK 中包含的 Docker 影像在本機測試您的 Apache 和 Dispatcher 設定。
   * 如需有關如何設定 Dispatcher Docker 容器以進行本機測試，請參閱[雲端中的 Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery)。

* 在將內容套件 (Sling 指派) 從作者複製到發佈執行個體期間，部署可能會因某些其他錯誤而失敗。
   * 按照以下步驟在本機設定上模擬問題。
      1. 使用最新的AEM SDK jar在本機安裝作者和發佈執行個體。
      1. 登入製作執行個體。
      1. 前往「**工具**」>「**部署**」>「**發佈**」。
      1. 指派作為程式碼庫 一部分的內容套件，並查看佇列是否因錯誤而阻塞。

## 我無法使用 aio 命令設定變數。該怎麼辦？ {#set-variable}

嘗試透過 `aio` 命令列出或設定管道變數時，您可能會收到類似以下的 `403` 錯誤。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

這種情況下，必須將執行這些命令的使用者新增到 Admin Console 中的&#x200B;**部署管理員**&#x200B;角色。

如需更多詳細資訊，請參閱 [API 權限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)。
