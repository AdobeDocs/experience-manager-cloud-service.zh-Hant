---
title: 部署至 AEM 雲端服務
description: '部署至 AEM 雲端服務 '
translation-type: tm+mt
source-git-commit: 10e12a8b15e6ea51e8b022deefaefed52780d48a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 部署至 AEM 雲端服務 {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與AEM On Premise和Managed Services解決方案相比，AEM中程式碼開發的基礎與雲端服務類似。 開發人員可編寫程式碼並在本機進行測試，然後將它推送至遠端AEM做為雲端服務環境。 Cloud Manager是Managed Services的選用內容傳送工具，是必要項。 現在，這是將程式碼部署至AEM做為雲端服務環境的唯一機制。

AEM版本的更新永遠是個別的部署事件，與推送自訂代碼不同。 以另一種方式檢視，自訂程式碼版本應針對生產中的AEM版本進行測試，因為它將部署在的上方。 此後發生的AEM版本更新（與現今的Managed Services相比，此更新會很頻繁）會自動套用。 這些程式碼會向後相容於已部署的客戶程式碼。

以下影片提供如何將程式碼部署至AEM做為雲端服務的高階概觀：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

本檔案的其餘部分將說明開發人員如何調整其實務，以便搭配AEM搭配Cloud Service的版本更新和客戶更新。

>[!NOTE]
>建議使用現有程式碼庫的客戶進行 [AEM檔案所述的儲存庫重組練習](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)。


## AEM版本更新 {#version-updates}

瞭解AEM會經常更新，可能像每天更新一次一樣頻繁，並著重於錯誤修正和效能增強。 更新將透明地進行，不會造成停機。 此更新旨在向後相容，這表示您不需要修改自訂程式碼。 事實上，AEM更新是客戶程式碼部署的獨立事件。 AEM更新會部署在您上次成功的程式碼推播上，這表示不會部署自上次推送至生產作業後所提交的任何變更。

>[!NOTE]
>
> 如果自訂代碼已推送至測試，然後遭到您拒絕，下一次AEM更新會移除這些變更，以反映上次成功客戶發行的git標籤至生產環境。

功能版本將定期推出，主要針對功能新增和增強功能，與日常版本相比，這些功能將對使用者體驗產生更大影響。 觸發功能發行的不是部署大型變更集，而是翻動發行切換，啟動在數天或數週內透過每日更新累積的程式碼。

Health checks are used to monitor the health of the application. 如果這些檢查在AEM的雲端服務更新期間失敗，則該版本將不會針對該環境繼續，而Adobe將調查更新為何會造成此非預期行為。

### 複合節點儲存 {#composite-node-store}

如上所述，在大多數情況下，更新將導致零停機，包括作者（即節點群集）。 由於Oak中的「複合節點儲存區」功能，因此可進行滾動更新。 此功能可讓AEM同時參考多個儲存庫。 在滾動部署中，新的綠色AEM版本包含其自己的 `/libs` (以TarMK為基礎的不可變儲存庫)，與舊版Blue AEM不同，不過兩者都參照共用的DocumentMK可變儲存庫，其中包含 `/content`、 `/conf``/etc` 和其他區域。 由於藍色和綠色都有各自的版本 `/libs`，因此在滾動更新期間，兩者都可以處於活動狀態，在藍色完全被綠色取代之前，都會進行流量。

## 客戶發行 {#customer-releases}

### 依正確的AEM版本編碼 {#coding-against-the-right-aem-version}

對於舊版AEM解決方案，最新的AEM版本不常變更（大約每年每季一次都會變更服務套件），客戶會自行將生產執行個體更新為最新的快速啟動，並參照API Jar。 不過，AEM(Cloud Service)應用程式會更頻繁地自動更新為最新版的AEM，因此內部版本的自訂代碼應以這些較新的AEM介面為基礎。

和現有的非雲端AEM版本一樣，支援以特定快速入門為基礎的本機離線開發，並預期在大多數情況下都是除錯的首選工具。

>[!NOTE]
>應用程式在本機電腦上的運作方式與Adobe Cloud有細微的操作差異。 這些架構差異必須在本機開發期間得到尊重，並可能導致在雲端基礎架構上部署時產生不同的行為。 由於這些差異，在生產中推出新的自訂程式碼之前，請務必先對開發與階段環境執行詳盡的測試。

為了開發內部版本的自訂程式碼，應下載並安裝 [AEM(Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) )的相關版本。 如需將AEM當做Cloud Service Dispatcher Tools的其他資訊，請參閱 [本頁](/help/implementing/dispatcher/overview.md)。

## 透過Cloud Manager和Package Manager部署內容套件 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 透過Cloud Manager進行部署 {#deployments-via-cloud-manager}

客戶可透過Cloud Manager將自訂代碼部署至雲端環境。 請注意，Cloud Manager會將本機組裝的內容套件轉換為符合Sling Feature Model的物件，這是在雲端環境中執行時，AEM如何描述為雲端服務應用程式。 因此，在查看Cloud環境上的Package Manager中的包時，名稱將包含「cp2fm」，而轉換的包會移除所有元資料。 無法與之互動，亦即無法下載、複製或開啟。 有關轉換器的詳細文檔可 [在此處找到](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

為AEM撰寫為雲端服務應用程式的內容套件，在不可變和可變內容之間必須有明確的分隔，Cloud Manager會透過失敗建置來強制執行，並輸出如下訊息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本節的其餘部分將說明不可改變和可變包裝的組成和含義。

### 不可變的內容包 {#immutabe-content-packages}

所有保存在不可變儲存庫中的內容和代碼都必須簽入git並通過Cloud Manager部署。 換言之，與目前的AEM解決方案不同，程式碼永遠不會直接部署至執行中的AEM例項。 如此可確保在任何雲端環境中執行特定版本的程式碼都相同，如此可避免在生產時意外變更程式碼的風險。 例如，OSGI設定應提交至來源控制項，而不是透過AEM網頁主控台的設定管理員在執行時期進行管理。

由於交換機啟用了藍綠部署模式而導致的應用程式更改，因此它們不能依賴於可變儲存庫中的更改，但服務用戶、其ACL、節點類型和索引定義更改除外。

對於具備現有程式碼庫的客戶，請務必進行AEM檔案中所述的儲存庫重組練習，以確保將先前位於/etc下的內容移至正確的位置。

## OSGI配置 {#osgi-configuration}

如上所述，OSGI配置應提交給原始碼控制，而不是通過Web控制台。 這樣做的技巧包括：

* 使用AEM網頁主控台的組態管理員，對開發人員的本機AEM環境進行必要的變更，然後將結果匯出至本機檔案系統上的AEM專案
* 在本機檔案系統的AEM專案中手動建立OSGI設定，以參照AEM主控台的設定管理員，取得屬性名稱。

如需OSGI設定的詳細資訊，請 [參閱「將OSGi設定為雲端服務」](/help/implementing/deploying/configuring-osgi.md)。

## 可變內容 {#mutable-content}

在某些情況下，在原始碼控制中準備內容更改可能會很有用，這樣，每當環境更新時，Cloud Manager就可以部署它。 例如，為某些根資料夾結構植入種子或在可編輯的模板中排列更改，以便為應用程式部署更新的元件啟用策略，這可能是合理的。

有兩種策略可描述Cloud Manager將部署到可變儲存庫、可變內容包和重新指向語句的內容。

### 可變內容套件 {#mutable-content-packages}

資料夾路徑階層、服務使用者和存取控制(ACL)等內容通常會提交至以主原型為基礎的AEM專案中。 技巧包括從AEM匯出或直接以XML格式撰寫。 在建立和部署過程中，Cloud Manager會封裝產生的可變內容封裝。 可變內容在流水線的部署階段中安裝的時間不同：

在新版應用程式啟動之前：

* 索引定義（添加、修改、刪除）

在啟動新版應用程式期間，但在切換之前：

* 服務使用者（新增）
* 服務用戶ACL（添加）
* 節點類型（添加）

切換到新版本的應用程式後：

* 所有其他可透過Jackrabbit Vault定義的內容。 例如：
   * 資料夾（添加、修改、刪除）
   * 可編輯的範本（新增、修改、移除）
   * 上下文感知配置(下面的任 `/conf`何內容)（添加、修改、刪除）
   * 指令碼(軟體包可以在軟體包安裝過程中的各個階段觸發安裝掛接

可將可變內容安裝限制為製作或發佈，方法是將套件內嵌在install.author或install.publish檔案夾中，位於 `/apps`。 如需建議專案重組的詳細 [資訊](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) ，請參閱AEM檔案。

>[!NOTE]
>內容包部署到所有環境類型(dev、stage、prod)。 無法將部署限制在特定環境。 此限制是為了確保自動執行測試執行的選項。 特定於環境的內容需要通過Package Manager手動安裝。

此外，在套用可變內容包更改後，沒有回滾這些更改的機制。 如果客戶發現問題，可以選擇在下次代碼發行中修正問題，或作為最後手段，將整個系統還原到部署之前的某個時間點。

任何包含的第三方套件都必須經過驗證為AEM與雲端服務相容，否則其包含將會導致部署失敗。

如上所述，現有程式碼庫的客戶應符合 [AEM檔案所述的儲存庫重組練習](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

## 重點 {#repoinit}

在以下情況下，最好在OSGI工廠配置中採用手動編碼顯式內容創 `repoinit` 建語句的方法：

* 建立／刪除／禁用服務用戶
* 建立／刪除群組
* 建立／刪除使用者
* 添加ACL
   > [!NOTE]
   >定義ACL要求節點結構已存在。 因此，可能需要在建立路徑語句之前執行。
* 添加路徑（例如根資料夾結構）
* 新增CND（nodetype定義）

由於以下優點，因此，最好對這些支援的內容修改使用案例進行重新分析：

* Repoinit會在啟動時建立資源，讓邏輯可以將這些資源的存在視為已授予。 在可變內容封裝方法中，資源是在啟動後建立的，因此依賴資源的應用程式碼可能會失敗。
* Repoinit是相對安全的指令集，因為您明確控制要執行的動作。 此外，除了允許移除使用者、服務使用者和群組的少數安全性相關案例外，唯一支援的作業是加入的。 相反，移除可變內容包方法中的某些內容是明確的；  當您定義篩選器時，篩選器所涵蓋的任何項目都會被刪除。 不過，我們仍應小心謹慎，因為如果有任何內容，新內容的存在可能會改變應用程式的行為。
* Repoinit可執行快速和原子操作。 相比之下，可變內容封裝可以高度依賴於濾鏡所覆蓋的結構。 即使您更新單個節點，也可能建立大型樹的快照。
* 可在運行時驗證本地開發環境上的repoinit語句，因為這些語句將在註冊OSGi配置時執行。
* 重新指向語句是原子和顯式語句，如果狀態已匹配，則將跳過。

當Cloud Manager部署應用程式時，它會執行這些陳述式，而與安裝任何內容套件無關。

要建立重新指向語句，請遵循以下過程：

1. 將OSGi配置添加 `org.apache.sling.jcr.repoinit.RepositoryInitializer` 到項目的配置資料夾中
1. 將重新指向語句添加到配置的指令碼屬性中。 語法和選項會記錄在 [Sling檔案中](https://sling.apache.org/documentation/bundles/repository-initialization.html)。 請注意，在父資料夾的子資料夾之前應明確建立父資料夾。 例如，在之前、之 `/content` 前明 `/content/myfolder`確建立 `/content/myfolder/mysubfolder`。 對於在低級結構上設定的ACL，建議將其設定在更高級別上，並使用限 `rep:glob` 制。  For example `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. 在執行時期在本機開發環境上驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>對於為下面的節點定 `/apps` 義的ACL `/libs` ，或重新指向執行將在空的儲存庫上啟動。 軟體包在重新指向後安裝，因此語句不能依賴於軟體包中定義的任何內容，但必須定義諸如下面的父結構之類的先決條件。

>[!TIP]
>
>對於ACL，建立深層結構可能很麻煩，因此更合理地在更高級別定義ACL並限制它應通過rep:glob限制執行的位置。

有關repoinit的更多詳細資訊，請參閱 [Sling檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Package Manager對可變內容包的「一次性」 {#package-manager-oneoffs-for-mutable-content-packages}

有些使用案例會將內容套件安裝為「一次性」。 例如，將特定內容從生產導入到測試階段，以除錯生產問題。 對於這些案例，Package Manager可以在AEM中當做雲端服務環境使用。

由於Package Manager是執行時期概念，因此無法將內容或代碼安裝到不可變的儲存庫中，因此這些內容包只能由可變的內容(主要 `/content` 或 `/conf`)組成。 如果內容包含混合的內容（可變內容和不可變內容），則只安裝可變內容。

透過Cloud Manager安裝的任何內容封裝（可變和不可變），都會在AEM Package Manager的使用者介面中顯示為凍結狀態。 這些軟體包無法重新安裝、重建或甚至下載，並且將以「 **cp2fm」尾碼列出** ，表示其安裝由Cloud Manager管理。

### 包括第三方包 {#including-third-party}

客戶通常會加入來自第三方來源（例如Adobe的翻譯合作夥伴等軟體廠商）的預建套件。 建議將這些軟體包裝載在遠程儲存庫中，並在中引用它們 `pom.xml`。 這僅對公共儲存庫可能。

如果無法將軟體包儲存在遠程儲存庫中，客戶可以將軟體包放在基於檔案系統的本地Maven儲存庫中，該儲存庫作為項目的一部分提交到SCM ，並由任何依賴它的系統引用。 儲存庫將在項目提示中聲明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方套件都必須遵守AEM的雲端服務編碼與封裝准則（本文所述），否則，其包含將會導致部署失敗。

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

## 滾動部署的運作方式 {#how-rolling-deployments-work}

和AEM更新一樣，客戶版本也會使用滾動部署策略進行部署，以在適當的情況下避免作者叢集的停機時間。 事件的一般順序如下所述，其中 **Blue** 是舊版客戶代碼， **Green** 是新版本。 Blue和Green都執行相同版本的AEM程式碼。

* 藍色版本處於活動狀態，並且已構建並提供綠色版本候選版本
* 如果有任何新的或更新的索引定義，則會處理相應的索引。 請注意，藍色部署將始終使用舊索引，而綠色部署將始終使用新索引。
* Blue仍在服務時，Green正在啟動
* Blue is running and serving while Green is checked for readiness via health checks
* 已準備好接受通信的綠色節點並替換已關閉的藍色節點
* 隨著時間的推移，藍色節點被綠色節點替換，直到只保留綠色節點，從而完成部署
* 部署任何新的或修改的可變內容

## 索引 {#indexes}

新的或修改的索引將在新的（綠色）版本開始處理流量之前，導致額外的索引建立或重新建立索引步驟。 本文詳細介紹了Skyline中的索引管 [理](/help/operations/indexing.md)。 您可以在Cloud Manager構建頁面上檢查索引作業的狀態，並在新版本準備就緒時收到通知。

>[!NOTE]
>
>滾動部署所需的時間會因索引的大小而異，因為生成新索引之前，綠色版本無法接受流量。

目前，Skyline無法與索引管理工具（例如ACS Commons Ensure Oak Index工具）搭配使用。

## 複寫 {#replication}

出版機制與 [AEM Replication Java API向後相容](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)。

為了使用雲端就緒的AEM Quickstart來開發和測試複製，必須搭配「作者／發佈」設定使用傳統的複製功能。 如果AEM Author的UI登入點已移除給雲端，使用者會前往進行 `http://localhost:4502/etc/replication` 設定。

## 適用於滾動部署的向後相容程式碼 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM作為Cloud Service的滾動部署策略意味著舊版和新版本可能同時運行。 因此，請謹慎處理程式碼變更，這些變更不向後相容於仍在運作的舊版AEM。

此外，舊版應測試是否與新版套用的任何新可變內容結構相容，因為不會移除可變內容。

### 服務用戶和ACL更改 {#service-users-and-acl-changes}

變更存取內容或程式碼所需的服務使用者或ACL，可能會導致舊版AEM中發生錯誤，導致對過時服務使用者的內容或程式碼存取。 為瞭解決此行為，建議您至少在2個版本中進行變更，第一個版本在後續版本中先充當橋梁。

### 索引更改 {#index-changes}

如果對索引進行了更改，Blue版本應繼續使用其索引，直到其終止，而Green版本則使用其自己修改的索引集。 開發人員應遵循本文所述的索引管 [理技術](/help/operations/indexing.md)。

### 回滾的保守編碼 {#conservative-coding-for-rollbacks}

如果在部署後報告或檢測到故障，則可能需要回滾到Blue版本。 最好確保藍色代碼與綠色版本建立的任何新結構相容，因為新結構（任何可變內容內容）將不會回退。 如果舊程式碼不相容，則需要在後續的客戶版本中套用修正。

## 執行模式 {#runmodes}

在現有的AEM解決方案中，客戶可以選擇以任意執行模式執行例項，並套用OSGI設定或將OSGI搭售安裝至這些特定例項。 定義的運行模式通常包括 *服務* （作者和發佈）和環境(dev、stage、prod)。

另一方面，AEM是雲端服務，對於哪些執行模式可用，以及如何將OSGI組合和OSGI組態對應至它們，則有更多看法：

* OSGI配置運行模式必須參考dev、stage、prod for the environment或author, publish for the service。 支援組合 `<service>.<environment_type>` ，但必須依此特定順序（例如或）使 `author.dev` 用 `publish.prod`這些。 OSGI Token應直接從程式碼參考，而不是使用 `getRunModes` 方法，方法將不再包含在執行 `environment_type` 時期。 如需詳細資訊，請 [參閱「將AEM的OSGi設定為雲端服務」](/help/implementing/deploying/configuring-osgi.md)。
* OSGI組合的執行模式僅限於服務（作者、發佈）。 Per-run mode OSGI bundles should be installed in the content package under `install/author` or `install/publish`.

和現有的AEM解決方案一樣，您也無法使用執行模式來安裝特定環境或服務的內容。 如果想要為未在舞台或生產環境中的資料或HTML建立開發環境，則可使用封裝管理員。

支援的執行模式組態包括：

* **config** (*預設值，套用至所有AEM服務*)
* **config.author** (套&#x200B;*用至所有AEM Author服務*)
* **config.author.dev** (套&#x200B;*用至AEM Dev Author服務*)
* **config.author.stage** (*套用至AEM Staging Author服務*)
* **config.author.prod** (*套用至AEM Production Author服務*)
* **config.publish** (套&#x200B;*用至AEM Publish服務*)
* **config.publish.dev** (套&#x200B;*用至AEM Dev Publish服務*)
* **config.publish.stage** (*套用至AEM Staging Publish服務*)
* **config.publish.prod** (套&#x200B;*用至AEM Production Publish服務*)
* **config.dev** （*套用至AEM Dev服務）
* **config.stage** （*適用於AEM Staging Services）
* **config.prod** (*Apples to AEM Production services)

會使用最符合執行模式的OSGI設定。

在本機開發時，可傳入runmode啟動參數，以指定將使用哪個runmode OSGI組態。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Source Control中的維護任務配置 {#maintenance-tasks-configuration-in-source-control}

維護任務配置必須保留在原始碼控制中，因為 **「工具」>「操作** 」螢幕將不再可用於雲環境。 這有利於確保變革是蓄意持續的，而不是反動地實施，甚至可能被遺忘。 如需詳細資 [訊，請參閱「維護工作](/help/operations/maintenance.md) 」文章。
