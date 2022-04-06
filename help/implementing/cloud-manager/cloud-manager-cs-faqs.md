---
title: Cloud Manager常見問題
description: 在as a Cloud Service中查找有關Cloud Manager的最常見問題的答AEM案。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 11ac22974524293ce3e4ceaa26e59fe75ea387e6
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Cloud Manager常見問題 {#cloud-manager-faqs}

本文檔提供有關as a Cloud Service中Cloud Manager的最常見問題的答AEM案。

## 是否可以將Java 11與Cloud Manager生成一起使用？ {#java-11-cloud-manager}

嘗AEM試將生成從Java 8切換到11時，Cloud Manager生成可能失敗。 問題可能有許多原因，本節記錄了最常見的原因。

* 添加 `maven-toolchains-plugin` 為Java 11設定。
   * 這是有記錄的 [這裡](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started)。
   * 例如，請參見 [wknd項目示例項目代碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果遇到以下錯誤，則需要刪除 `maven-scr-plugin` 將所有OSGi注釋轉換為OSGi R6注釋。
   * 有關說明，請參見 [給。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   ```text
   [main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
   ```

* 對於Cloud Manager版本， `maven-enforcer-plugin` 錯誤 `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 這是已知問題，因為Cloud Manager使用不同版本的Java運行maven命令而不是編譯代碼。 暫時省略 `requireJavaVersion` 從 `maven-enforcer-plugin` 配置。

## 代碼質量檢查失敗，我們的部署停滯。 有辦法繞過這張支票嗎？ {#deployment-stuck}

除安全評級之外的所有代碼質量檢查失敗都是非關鍵度量，因此可以通過擴展結果UI中的項來繞過它們。

中的用戶 [部署管理器、程式管理器或業務所有者](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md) 角色可以覆蓋問題，在這種情況下，管道將繼續。 這些用途還可以接受問題，在這種情況下，管線會因故障而停止。

查看文檔 [代碼質量測試](/help/implementing/cloud-manager/code-quality-testing.md) 的子菜單。

## 是否可以將SNAPSHOT用於Maven項目的版本？ 軟體包和捆綁jar檔案的版本控制如何用於階段和生產部署？ {#snapshot-version}

以下方案涉及用於階段和生產部署的包和捆綁包jar檔案版本控制。

* 對於開發人員部署， Git分支 `pom.xml` 檔案必須包含 `-SNAPSHOT` 在 `<version>` 值。
   * 這允許在版本未更改時仍安裝後續部署。 在開發人員部署中，不會為maven內部版本添加或生成自動版本。

* 在階段和生產部署中，自動版本生成為 [記錄在此。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

* 對於階段和生產部署中的自定義版本控制，請設定一個適當的三部分版本，如 `1.0.0`。 每次部署到生產環境時都增加版本。

* Cloud Manager會自動將其版本添加到舞台和生產構建中並建立Git分支。 不需要特殊配置。 如果未按前面所述設定主版本，則部署仍將成功，並自動設定版本。

* 可以將版本設定為 `-SNAPSHOT` 用於無問題的階段和生產構建或部署。 Cloud Manager會自動設定正確的版本號，並以Git為您建立標籤。 如果需要，可以稍後引用此標籤。

* 如果要在開發環境中嘗試一些實驗代碼，可以建立新的git分支並設定管道以使用該分支。
   * 當部署失敗時，此功能非常有用，您希望與較舊版本的代碼test，以確定導致故障的更改。

   * 下面的git命令將建立一個名為 `testbranch1` 基於預先存在的提交 `485548e4fbafbc83b11c3cb12b035c9d26b6532b`。  此分支可在Cloud Manager中使用，而不影響任何其他分支。

   ```shell
   git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1
   ```

   * 查看 [git文檔](https://git-scm.com/book/en/v2/Git-Internals-Git-References) 的子菜單。

   * 如果以後要刪除test分支，請使用delete命令：

   ```shell
   git push origin --delete testbranch1
   ```

## 我的maven生成對Cloud Manager部署失敗，但是它在本地生成，沒有錯誤。 怎麼了？ {#maven-build-fail}

請參閱 [Git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 的子菜單。

## 如果Cloud Manager部署在as a Cloud Service的部署步驟失敗，我該怎麼辦AEM? {#cloud-manager-deployment-cloud-service}

部署失敗的最常見原因是： `sling-distribution-importer` 。 在這種情況下，部署步驟在Cloud Manager部署期間失敗，並生成以下錯誤。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

在這個例子中， `sling-distribution-importer` 用戶需要對中定義的內容路徑的附加權限 `ui.content package`。  這通常意味著您需要為兩者添加權限 `/conf` 和 `/var`。

解決方案是 [RepositoryInitializer OSGi配置](/help/implementing/deploying/overview.md#repoint) 指令碼到應用部署包，以添加ACL `sling-distribution-importer` 。

在上一個示例錯誤中，包 `myapp-base.ui.content-*.zip` 包含內容 `/conf` 和 `/var/workflow`。 為使部署成功， `sling-distribution-importer` 這些道路是必要的。

這是一個例子 [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) 添加對 `sling-distribution-importer` 。  此配置在以下項下添加權限 `/var`。  下面的此xml檔案 [1] 需要添加到應用程式套件中 `/apps/myapp/config` （其中myapp是儲存應用程式碼的資料夾）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

如果添加RepositoryInitializer OSGi配置未解決錯誤，則可能是由於以下其他問題之一所致。

* 部署可能因OSGi配置錯誤而失敗，該配置中斷了現成服務。
   * 在部署期間檢查日誌，查看是否存在明顯錯誤。

* 部署可能由於調度程式或Apache配置錯誤而失敗。
   * 確保使用SDK中包含的Docker映像在本地testApache和調度程式配置。
   * 請參閱 [雲中的調度程式](/help/implementing/dispatcher/disp-overview.md#content-delivery) 有關如何設定dispatcher Docker容器以便進行輕鬆的本地測試。

* 部署可能由於從作者複製到發佈實例的內容包（Sling分發）期間出現其他故障而失敗。
   * 按照以下步驟模擬本地設定上的問題。
      1. 使用最新的SDK Jar安裝作者並在本地發AEM布實例。
      1. 登錄到作者實例。
      1. 轉到 **工具** -> **部署** -> **分佈**。
      1. 分發作為代碼庫一部分的內容包，並查看隊列是否因錯誤而被阻止。

## 無法使用aio命令設定變數。 我能做什麼？ {#set-variable}

您可能會收到 `403` 嘗試通過列出或設定管線變數時出現以下錯誤 `aio` 的雙曲餘切值。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在這種情況下，需要將執行這些命令的用戶添加到 **部署管理** 在Admin Console中。

請參閱 [API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) 的子菜單。
