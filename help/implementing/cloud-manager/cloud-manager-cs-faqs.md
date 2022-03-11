---
title: Cloud Manager -Cloud Services常見問題
seo-title: Cloud Manager FAQs
description: 請參閱雲管理器瞭解Cloud Services常見問題，以獲取一些故障排除提示
seo-description: Follow this page to get answers on Cloud Manager - Cloud Services FAQs
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%

---

# Cloud Manager常見問題 {#cloud-manager-faqs}

以下部分提供與Cloud Manager相關的常見問題的答案，供Cloud Services使用。

## 是否可以將Java 11與Cloud Manager生成一起使用？ {#java-11-cloud-manager}

嘗AEM試將生成從Java 8切換到11時，Cloud Manager生成失敗。 問題可能有許多原因，下面列出了最常見的原因：

* 添加帶有正確Java 11設定的maven-toolchains插件，如文所述 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)。  例如，請參見 [wknd示例項目代碼](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果遇到以下錯誤，則需要刪除 `maven-scr-plugin` 將所有OSGi注釋轉換為OSGi R6注釋。 有關說明，請參見 [這裡](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 對於Cloud Manager生成，Maven Enforcer插件失敗，並出現錯誤 `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 這是已知問題，因為Cloud Manager使用不同版本的Java運行maven命令而不是編譯代碼。 暫時省略 `requireJavaVersion` 從maven-enforcer插件配置中。

## 由於代碼質量檢查失敗，我們的部署停滯。 有辦法繞過這張支票嗎？ {#deployment-stuck}

所有代碼質量失敗(除 *安全等級* 是非關鍵度量，因此可以通過擴展結果UI中的項來繞過這些度量。

具有 [部署經理、項目經理或業務所有者](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) 角色可以覆蓋問題，在這種情況下，管線將繼續，或者他們可以接受問題，在這種情況下，管線將因失敗而停止。  請參閱 [運行管道時的三層門](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) 的子菜單。


## 是否允許在Maven項目的版本中使用SNAPSHOT? 包和捆綁jar檔案的版本控制如何用於階段和生產部署？ {#snapshot-version}

請參閱以下方案，瞭解有關用於階段和生產部署的包和捆綁jar檔案的版本控制：

1. 對於開發人員部署，Git分支 `pom.xml` 檔案必須包含 `-SNAPSHOT` 在 `<version>` 值。 這允許後續部署，其中版本不會更改，仍可安裝。 在開發人員部署中，不會為maven內部版本添加或生成自動版本。

1. 在階段和生產部署中，自動版本將根據文檔生成 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)。

1. 對於階段和生產部署中的自定義版本控制，請設定3個部件正確的版本，如 `1.0.0`。 每次必須進行另一次部署到生產時，都增加版本。

1. Cloud Manager會自動將其版本添加到Stage和Production內部版本，甚至建立Git分支。 不需要特殊配置。 如果跳過上面的步驟3，部署仍將正常工作，並自動設定版本。

1. 沒有問題，如果您將版本 `-SNAPSHOT` 用於階段和生產生成或部署。 Cloud Manager會自動設定正確的版本號，並在Git中為您建立標籤。 如果需要，可以稍後引用此標籤。

1. 如果要在開發環境上嘗試一些實驗代碼，可以建立新的Git分支並設定管道以使用該不同的分支。 當部署開始失敗，並且您希望與較舊版本的代碼test，以查看代碼何時破壞時，此功能非常有用。

   下面的Git命令將建立一個名為 *測試分支* 針對特定的預先存在的承諾 `485548e4fbafbc83b11c3cb12b035c9d26b6532b`。  此特殊分支可在Cloud Manager中使用，而不影響任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   查看 [Git文檔](https://git-scm.com/book/en/v2/Git-Internals-Git-References) 的子菜單。

   如果以後要刪除test分支，請使用delete命令：

   `git push origin --delete testbranch1`

## 在雲管理器中部署Maven生成失敗，但在本地生成時沒有錯誤。 如何調試？ {#maven-build-fail}

請參閱 [Git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 的子菜單。

## 如果Cloud Manager部署在as a Cloud Service環境中部署步驟失敗，AEM該怎麼辦？ {#cloud-manager-deployment-cloud-service}

部署失敗的最常見原因是權限不足 *吊裝配 — 進口商* 。
請參閱下面的示例，瞭解問題、原因和解決方案：

**問題**
在as a Cloud Service環境上部署Cloud ManagerAEM時，部署步驟會失敗，並會發現以下錯誤。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importer用戶需要對ui.content包中定義的內容路徑具有附加權限。  這通常意味著我們需要為/conf和/var添加權限。

**解決方案**
解決方法是 [RepositoryInitializer OSGi配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) 指令碼到應用程式部署包，以為slin-distribution-importer用戶添加ACL。
在上面的示例錯誤中，包myapp-base.ui.content-*.zip包含以下內容 `/conf` 和 `/var/workflow`。 為了使部署不失敗，我們需要在這些路徑下添加對sling-distribution-importer的權限。
這是一個例子 [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) 添加sling-distribution-importer用戶的附加權限的OSGi配置。  此配置在/var下添加權限。  下面的此xml檔案 [1] 需要添加到應用程式套件中 `/apps/myapp/config` （其中myapp是儲存應用程式碼的資料夾）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. 如果 *吊裝配 — 進口商* 不是原因，則部署可能由於OSGi配置錯誤而失敗，因為該配置中斷了開箱服務。 在部署期間檢查日誌，查看是否存在明顯錯誤。

1. 部署可能由於錯誤的調度程式或apache配置而失敗。 確保使用SDK中包含的Docker映像在本地testApache配置和Dispatcher配置。 請參閱 [雲中的調度程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) 有關如何設定dispatcher Docker容器以便進行輕鬆的本地測試。

1. 部署可能會失敗，因為在將內容包(sling distribution)從作者複製到發佈實例期間出現其他故障。

   請參閱以下步驟，在本地設定中模擬此操作：

   * 安裝Author和Publish實例(使用最新AEM的SDKjar)
   * 登錄到Author實例
   * 轉到 **工具** -> **部署** -> **分佈**
   * 分發作為代碼庫一部分的內容包，並查看隊列是否因錯誤而被阻止

## 無法通過aio雲管理器設定管道變數來設定變數。 如何調試這些問題？ {#set-variable}

如果你要 `403` 嘗試通過類似於以下命令的命令列出或設定管道變數時出錯，則需要將您添加為 *部署管理器* Admin Console中的Cloud Manager產品角色。\
請參閱 [API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) 的子菜單。

相關命令和錯誤：

`$ aio cloudmanager:list-pipeline-variables 222`

*錯誤*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*錯誤*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*錯誤*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
