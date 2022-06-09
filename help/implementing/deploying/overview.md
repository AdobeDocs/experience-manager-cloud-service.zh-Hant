---
title: '部署至 AEM as a Cloud Service '
description: '部署至 AEM as a Cloud Service  '
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 91361eb49eaf4ec3b89dbd816aecca3c5bfe029f
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 2%

---

# 部署至 AEM as a Cloud Service  {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與On Premise和Managed Services解決方案相AEM比，代碼開發的AEM基礎在as a Cloud Service上相似。 開發人員編寫代碼並在本地test，然後將代碼推送到遠AEM程as a Cloud Service環境。 Cloud Manager是Managed Services的可選內容交付工具，是必需的。 現在，這是將代碼部署到as a Cloud Service環境的AEM唯一機制。

更新 [AEM版本](/help/implementing/deploying/aem-version-updates.md) 始終是單獨的部署事件與推送 [自定義代碼](#customer-releases)。 換種方式來看，定制代碼版本應針對生產版AEM本進行測試，因為這是將在頂部部署的版本。 之後AEM發生的版本更新，此更新將頻繁且自動應用。 它們旨在向後相容已部署的客戶代碼。

本文檔的其餘部分將介紹開發人員應如何調整其做法，以便他們能夠AEM同時使用as a Cloud Service的版本更新和客戶更新。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客戶發放 {#customer-releases}

### 按正確版本編AEM碼 {#coding-against-the-right-aem-version}

對於以前AEM的解決方案，最新版AEM本不常更改（大約每年使用季度Service Pack），客戶將自己的時間將生產實例更新為最新的快速啟動，並引用API Jar。 但是，AEMas a Cloud Service應用程式會更頻繁地自動更新到最新AEM版本，因此內部版本的自定義代碼應根據最新版本AEM生成。

與現有非雲版本AEM類似，將支援基於特定快速啟動的本地離線開發，並且在大多數情況下，它將是調試的首選工具。

>[!NOTE]
>應用程式在本地電腦上的行為與Adobe雲之間存在細微的操作差異。 這些架構差異必須在本地開發過程中得到尊重，並可能導致在雲基礎架構上部署時出現不同的行為。 由於這些差異，在生產中推出新的自定義代碼之前，必須對開發和階段環境執行詳盡的test。

為開發內部版本的自定義代碼， [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 應下載並安裝。 有關使用as a Cloud Service調度器工AEM具的其他資訊，請參見 [此頁](/help/implementing/dispatcher/disp-overview.md)。

以下視頻提供了有關如何將代碼部署到AEMas a Cloud Service的高級概述：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 通過雲管理器和包管理器部署內容包 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 通過雲管理器部署 {#deployments-via-cloud-manager}

客戶通過Cloud Manager將自定義代碼部署到雲環境。 應該注意的是，Cloud Manager將本地組裝的內容包轉換為符合Sling Feature Model的工件，Sling Feature Model是在雲環境中運行時對AEMas a Cloud Service應用程式的描述。 因此，在查看 [包管理器](/help/implementing/developing/tools/package-manager.md) 在雲環境中，名稱將包含「cp2fm」，轉換後的包刪除了所有元資料。 它們無法相互作用，這意味著它們無法下載、複製或開啟。 有關轉換器的詳細文檔可以 [此處](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

為as a Cloud Service應用程AEM序編寫的內容包必須在不可變內容和可變內容之間保持乾淨的隔離，Cloud Manager將只安裝可變內容，並輸出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本節的其餘部分將介紹不可變和可變軟體包的組成和含義。

### 不可變的內容包 {#immutabe-content-packages}

必須將保留在不可變儲存庫中的所有內容和代碼簽入git並通過雲管理器進行部署。 換句話說，與當前解決AEM方案不同，代碼從未直接部署到正在運行的AEM實例。 這可確保在任何雲環境中為給定版本運行的代碼都完全相同，從而消除了在生產過程中意外發生代碼變化的風險。 例如，OSGI配置應提交到原始碼管理，而不是通過Web控制台的AEM配置管理器在運行時進行管理。

由於交換機啟用了藍綠部署模式導致的應用程式更改，因此它們不能依賴於可變儲存庫中的更改，但服務用戶、其ACL、節點類型和索引定義更改除外。

對於具有現有代碼庫的客戶，必須完成文檔中介紹的儲存庫重組練習AEM，以確保以前在/etc下的內容移動到正確的位置。

對這些代碼包應用一些附加限制，例如 [安裝掛接](http://jackrabbit.apache.org/filevault/installhooks.html) 不支援。

## OSGI配置 {#osgi-configuration}

如上所述，OSGI配置應提交到原始碼管理，而不是通過Web控制台。 這樣做的技術包括：

* 使用Web控制台的配置管理器AEM對開發人員的本地AEM環境進行必要的更改，然後將結果導出到本地文AEM件系統上的項目
* 在本地檔案系統上的項AEM目中手動建立OSGI配置，該配置引用AEM了控制台的配置管理器的屬性名稱。

閱讀有關OSGI配置的更多資訊，請訪問 [配置OSGiAEM以as a Cloud Service](/help/implementing/deploying/configuring-osgi.md)。

## 可變內容 {#mutable-content}

在某些情況下，在原始碼管理中準備內容更改可能會非常有用，以便在更新環境時，Cloud Manager可以部署此內容。 例如，可以合理地植入某些根資料夾結構，或在可編輯模板中排列更改，以啟用應用程式部署更新的元件的策略。

有兩種策略可描述Cloud Manager將部署到可變儲存庫、可變內容包和重新指向語句的內容。

### 可變內容包 {#mutable-content-packages}

資料夾路徑層次結構、服務用戶和訪問控制(ACL)等內容通常被提交到基於主原型的項AEM目中。 技術包括從XMLAEM導出或直接寫入。 在生成和部署過程中，Cloud Manager會將生成的可變內容包打包。 可變內容在管道的部署階段中以3個不同的時間安裝：

在啟動新版本的應用程式之前：

* 索引定義（添加、修改、刪除）

在啟動新版本的應用程式期間但在切換之前：

* 服務用戶（添加）
* 服務用戶ACL（添加）
* 節點類型（添加）

切換到新版本的應用程式後：

* 所有其它內容可通過jackrabbit保險庫定義。 例如：
   * 資料夾（添加、修改、刪除）
   * 可編輯模板（添加、修改、刪除）
   * 上下文感知配置(下面的任何內容 `/conf`)（添加、修改、刪除）
   * 指令碼(軟體包可以在軟體包安裝過程的各個階段觸發安裝掛接。 查看 [Jackrabbit檔案](http://jackrabbit.incubator.apache.org/filevault/installhooks.html) 關於安裝掛接。 請注意AEM,CS當前使用Filevault版本3.4.0，該版本將安裝掛接限制為管理員用戶、系統用戶和管理員組成員)。

通過將包嵌入install.author或install.publish資料夾中，可以將可變內容安裝限制為創作或發佈 `/apps`。 6.5中進行了重組，以AEM反映這一分離，建議的項目重組詳情見 [AEM6.5文檔。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>內容包將部署到所有環境類型(dev、stage、prod)。 無法將部署限制到特定環境。 此限制是為了確保test運行自動執行選項。 特定於環境的內容需要通過 [包管理器。](/help/implementing/developing/tools/package-manager.md)

此外，在應用可變內容包更改後，沒有回滾這些更改的機制。 如果客戶檢測到問題，他們可以選擇在下次代碼發行時解決它，或者作為最後手段，將整個系統恢復到部署前的某個時間點。

任何包含的第三方包都必須驗證為與AEMas a Cloud Service服務相容，否則其包含將導致部署失敗。

如上所述，具有現有代碼庫的客戶應遵守中介紹的6.5儲存庫更改所需的儲存庫重組操作 [AEM6.5文檔。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## 重點 {#repoinit}

對於以下情況，最好採用手工編碼顯式內容建立的方法 `repoinit` OSGI工廠配置中的語句：

* 建立/刪除/禁用服務用戶
* 建立/刪除組
* 建立/刪除用戶
* 添加ACL

   >[!NOTE]
   >
   >ACL的定義要求節點結構已存在。 因此，可能需要在建立路徑語句之前執行。

* 添加路徑（例如根資料夾結構）
* 添加CND（nodetype定義）

由於以下優點，對於這些受支援的內容修改使用案例，重點說明是可取的：

* Repoinit在啟動時建立資源，以便邏輯可以將這些資源的存在視為已授予。 在可變內容包方法中，資源是在啟動後建立的，因此依賴於它們的應用程式碼可能會失敗。
* 重點是相對安全的指令集，因為您明確控制要執行的操作。 此外，唯一支援的操作是附加操作，但允許刪除用戶、服務用戶和組的幾個安全相關案例除外。 相反，移除可變內容包方法中的某些內容是明確的；在定義篩選器時，篩選器所涵蓋的任何內容都將被刪除。 但是，應當謹慎行事，因為對於任何內容，都存在新內容可能會改變應用程式的行為。
* 重定位執行快速和原子操作。 相比之下，可變內容包可以高度依賴於過濾器所覆蓋的結構。 即使您更新單個節點，也可能建立大樹的快照。
* 可以在運行時驗證本地開發環境中的repoinit語句，因為在註冊OSGi配置時將執行這些語句。
* 重點語句是原子語句和顯式語句，如果狀態已匹配，則將跳過。

Cloud Manager部署應用程式時，它將執行這些語句，與任何內容包的安裝無關。

要建立repoint語句，請按照以下步驟操作：

1. 為工廠PID添加OSGi配置 `org.apache.sling.jcr.repoinit.RepositoryInitializer` 的子菜單。 使用配置的描述性名稱，如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 將repoinit語句添加到配置的指令碼屬性。 語法和選項在 [Sling文檔](https://sling.apache.org/documentation/bundles/repository-initialization.html)。 請注意，應在父資料夾的子資料夾之前顯式建立父資料夾。 例如， `/content` 先 `/content/myfolder`在 `/content/myfolder/mysubfolder`。 對於在低級結構上設定的ACL，建議將其設定在更高級別上，並使用 `rep:glob` 限制。  例如 `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在運行時在本地開發環境上驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>為下面的節點定義的ACL `/apps` 或 `/libs` 將在空白儲存庫上啟動重新定位執行。 這些包在重新指向後安裝，因此語句不能依賴於包中定義的任何內容，但必須定義先決條件，如下面的父結構。

>[!TIP]
>
>對於ACL，建立深層結構可能比較麻煩，因此，在更高級別上定義ACL並通過rep:glob限制約束它應在何處操作更合理。

有關重點位置的詳細資訊，請參閱 [Sling文檔](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可變內容包的包管理器「一個」 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="包管理器 — 遷移可變內容包"
>abstract="探索軟體包管理器的使用情況，瞭解內容軟體包應作為「一次性」安裝的使用情形，包括將特定內容從生產導入到暫存，以調試生產問題、將小型內容軟體包從內部環境傳輸到AEM雲環境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="內容轉移工具"

有些使用情形中，內容包應作為「一次性」安裝。 例如，將特定內容從生產導入到暫存以調試生產問題。 對於這些情景， [包管理器](/help/implementing/developing/tools/package-manager.md) 可用於AEMas a Cloud Service環境。

由於包管理器是運行時概念，因此無法將內容或代碼安裝到不可變的儲存庫中，因此這些內容包只應由可變內容(主要是 `/content` 或 `/conf`)。 如果內容包包含混合的內容（可變內容和不可變內容），則只安裝可變內容。

>[!IMPORTANT]
>
>包管理器UI可能返回 **未定義** 如果安裝軟體包需要10分鐘以上，則會出現錯誤消息。
>
>這不是因為安裝錯誤，而是由於Cloud Service對所有請求的超時。
>
>如果您看到此類錯誤，請不要重試安裝。 安裝在後台正在正確進行。 如果您確實重新啟動安裝，則多個併發導入進程可能會引入一些衝突。

通過Cloud Manager安裝的任何內容包（可變和不可變）都將在AEMPackage Manager的用戶介面中以凍結狀態顯示。 無法重新安裝、重建甚至下載這些軟體包，並將隨 **&quot;cp2fm&quot;** 尾碼，表示其安裝由雲管理器管理。

### 包括第三方包 {#including-third-party}

客戶通常會包括來自第三方來源的預構建軟體包，如Adobe翻譯合作夥伴等軟體供應商。 建議將這些軟體包托管在遠程儲存庫中，並在 `pom.xml`。 這對於公共儲存庫和具有密碼保護的專用儲存庫是可能的，如中所述 [受密碼保護的maven主要儲存庫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)。

如果無法將包儲存在遠程儲存庫中，則客戶可以將其放置在基於本地檔案系統的Maven儲存庫中，該儲存庫作為項目的一部分提交給SCM，並由任何依賴它的資訊引用。 儲存庫將在項目pom中聲明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方包都必須遵守本文中AEM描述的as a Cloud Service服務編碼和打包指南，否則，包含它將導致部署失敗。

以下Maven POM XML程式碼片段顯示如何透過 **filevault-package-maven-plugin** Maven增效模組組態，將第三方套件內嵌在專案的「容器」套件中，通常稱為 **** &#39;all&#39;。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## 滾動部署的工作方式 {#how-rolling-deployments-work}

與更AEM新一樣，客戶版本使用滾動部署策略進行部署，以在適當的情況下消除作者群集停機時間。 事件的一般順序如下所述，其中 **藍色** 是舊版本的客戶代碼 **綠色** 是新版本。 藍色和綠色都運行相同版本的代AEM碼。

* 藍色版本處於活動狀態，並且已生成並可用綠色版本候選
* 如果存在任何新的或更新的索引定義，則處理相應的索引。 請注意，藍色部署將始終使用舊索引，而綠色部署將始終使用新索引。
* 藍色還在服務時，綠色正在啟動
* 藍色正在運行，並在通過運行狀況檢查檢查綠色是否就緒時提供服務
* 準備就緒的綠色節點接受通信並替換藍色節點（已關閉）
* 隨著時間的推移，藍色節點被綠色節點替換，直到僅保留綠色，從而完成部署
* 部署任何新的或修改的可變內容

## 索引 {#indexes}

新索引或已修改的索引將導致在新（綠色）版本開始通信之前執行額外的索引或重新索引步驟。 有關as a Cloud Service中索引管AEM理的詳細資訊，請參閱 [這篇文章](/help/operations/indexing.md)。 您可以在Cloud Manager生成頁上檢查索引作業的狀態，並在新版本準備接收通信時收到通知。

>[!NOTE]
>
>滾動部署所需的時間會因索引的大小而異，因為在生成新索引之前，綠色版本不能接受通信。

目前，AEMas a Cloud Service不能使用索引管理工具，如ACS Commons Ensure Oak Index工具。

## 複寫 {#replication}

發佈機制與 [復AEM制Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)。

為了利用雲就緒快速啟動開發和test復AEM制功能，需要將經典複製功能與「作者/發佈」設定一起使用。 如果AEM作者上的UI入口點已被刪除，則用戶將轉到 `http://localhost:4502/etc/replication` 的子菜單。

## 滾動部署的向後相容代碼 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEMas a Cloud Service的滾動部署策略意味著舊版本和新版本可能同時運行。 因此，請謹慎處理代碼更改，這些代碼更改與仍在運行的AEM舊版本不向後相容。

此外，應測試舊版本是否與新版本在回滾時應用的任何新可變內容結構相容，因為不會刪除可變內容。

### 服務用戶和ACL更改 {#service-users-and-acl-changes}

更改訪問內容或代碼所需的服務用戶或ACL可能會導致較舊版本中的錯誤AEM，從而導致過時的服務用戶訪問該內容或代碼。 要解決此行為，建議在至少2個版本之間進行更改，第一個版本在後續版本中清理之前充當橋梁。

### 索引更改 {#index-changes}

如果對索引進行了更改，則藍色版本繼續使用其索引直到終止，而綠色版本使用其自己修改的索引集是非常重要的。 開發人員應遵循描述的索引管理技術 [本文](/help/operations/indexing.md)。

### 回退的保守編碼 {#conservative-coding-for-rollbacks}

如果在部署後報告或檢測到故障，則可能需要回滾到藍色版本。 最好確保藍色代碼與綠色版本建立的任何新結構相容，因為新結構（任何可變內容內容）不會回滾。 如果舊代碼不相容，則需要在後續客戶版本中應用修復。

## 執行模式 {#runmodes}

在現有解AEM決方案中，客戶可以選擇以任意運行模式運行實例，並將OSGI配置或安裝OSGI捆綁包到這些特定實例。 通常定義的運行模式包括 *服務* （作者和發佈）和環境(dev、stage、prod)。

另AEM一方面，as a Cloud Service的是對哪些運行模式可用以及如何將OSGI捆綁包和OSGI配置映射到它們：

* OSGI配置運行模式必須引用開發、階段、環境或作者的產品、服務的發佈。 組合 `<service>.<environment_type>` 是受支援的，但必須按此特定順序使用(例如 `author.dev` 或 `publish.prod`)。 OSGI令牌應直接從代碼引用，而不是使用 `getRunModes` 方法，該方法將不再包括 `environment_type` 運行時。 有關詳細資訊，請參見 [配置OSGiAEM以as a Cloud Service](/help/implementing/deploying/configuring-osgi.md)。
* OSGI捆綁包的運行模式僅限於服務（作者、發佈）。 每運行模式OSGI捆綁包應安裝在內容包中， `install/author` 或 `install/publish`。

與現有解決AEM方案一樣，無法使用運行模式來僅安裝特定環境或服務的內容。 如果希望為開發環境植入資料或HTML，而不是在階段或生產環境中，則可以使用包管理器。

支援的運行模式配置包括：

* **配置** (*預設值，適用於所有服AEM務*)
* **config.author** (*適用於所有AEM作者服務*)
* **config.author.dev** (*應用於開發AEM人員作者服務*)
* **config.author.stage** (*應用於AEM暫存作者服務*)
* **config.author.prod** (*應用於AEMProduction Author服務*)
* **config.publish** (*應用於AEM發佈服務*)
* **config.publish.dev** (*應用於開發AEM人員發佈服務*)
* **config.publish.stage** (*應用於AEM臨時發佈服務*)
* **config.publish.prod** (*應用於AEM生產發佈服務*)
* **config.dev** (*適用於開發AEM服務*)
* **config.stage** (*適用於AEM暫存服務*)
* **config.prod** (*適用於生AEM產服務*)

使用具有最匹配運行模式的OSGI配置。

本地開發時，運行模式啟動參數， `-r`，用於指定運行模式OSGI配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 原始碼管理中的維護任務配置 {#maintenance-tasks-configuration-in-source-control}

維護任務配置必須保留在原始碼管理中，因為 **工具>操作** 雲環境中將不再提供螢幕。 這樣做的好處是確保變革被有意地持續，而不是重新應用或被遺忘。 請參考 [維護任務文章](/help/operations/maintenance.md) 的雙曲餘切值。
