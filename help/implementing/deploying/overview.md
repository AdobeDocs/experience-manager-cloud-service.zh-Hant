---
title: '部署至 AEM as a Cloud Service '
description: '部署至 AEM as a Cloud Service  '
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 部署至 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與On Premise和Managed Services解決方案相AEM比，程式碼開發的基礎AEM類似於Cloud Service。 開發人員可編寫程式碼並在本端進行測試，然後將程式碼推送至遠端AEM做為Cloud Service環境。 Cloud Manager是Managed Services的選用內容傳送工具，是必要工具。 現在，這是將程式碼部署為Cloud ServiceAEM環境的唯一機制。

[版本&lt;a1/AEM>的更新永遠是與推送[自訂代碼](#customer-releases)不同的部署事件。 ](/help/implementing/deploying/aem-version-updates.md)以另一種方式檢視，自訂程式碼版本應針對生產版AEM本進行測試，因為它將部署在頂端。 之AEM後會發生的版本更新，此更新會頻繁且自動套用。 這些程式碼可向後相容於已部署的客戶程式碼。

本檔案的其餘部分將說明開發人員如何調整其實務，以便搭配使用，AEM做為Cloud Service的版本更新和客戶更新。

>[!NOTE]
>建議使用現有代碼庫的客戶進行[文檔](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中介紹的資AEM料庫重構練習。

## 客戶發行{#customer-releases}

### 根據正確版AEM本{#coding-against-the-right-aem-version}編碼

對於舊AEM版解決方案，最新版本不常變AEM更（大約每年每季一次都會變更服務套件），客戶會自行將生產執行個體更新為最新的快速啟動，並參照API Jar。 不過，AEM由於Cloud Service應用程式會更頻繁地自動更新為最新AEM版本，因此內部版本的自訂程式碼應根據最新版本AEM建立。

和現有非雲端版本AEM一樣，支援以特定快速入門為基礎的本端離線開發，並預期在大多數情況下都是除錯工具。

>[!NOTE]
>應用程式在本機機器上的運作方式與在Adobe雲端上的運作方式有細微的差異。 這些架構差異必須在本機開發期間得到尊重，並可能導致在雲端基礎架構上部署時產生不同的行為。 由於這些差異，在生產中推出新的自訂程式碼之前，請務必先對開發與階段環境執行詳盡的測試。

為了開發內部版本的自訂程式碼，應下載並安AEM裝作為Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的相關版本。 [有關將作為Cloud ServiceDispatcher工AEM具使用的其他資訊，請參見[此頁](/help/implementing/dispatcher/disp-overview.md)。

以下影片提供如何將程式碼部署為Cloud Service的AEM高階概觀：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

>[!NOTE]
>建議使用現有代碼庫的客戶進行[文檔](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中介紹的資AEM料庫重構練習。

## 透過Cloud Manager和Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}部署內容封裝

### 透過Cloud Manager {#deployments-via-cloud-manager}進行部署

客戶可透過Cloud Manager將自訂代碼部署至雲端環境。 請注意，Cloud Manager會將本機組裝的內容套件轉換為符合Sling Feature Model的物件，這是當在雲端環境中執行時，將作AEM為Cloud Service應用程式的描述方式。 因此，在查看Cloud環境上的Package Manager中的包時，名稱將包含「cp2fm」，而轉換的包會移除所有元資料。 無法與之互動，亦即無法下載、複製或開啟。 有關轉換器的詳細文檔可以在[這裡找到](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

作為Cloud Service應用AEM程式寫入的內容包必須在不可變內容和可變內容之間保持乾淨的隔離，Cloud Manager將通過失敗構建來強制執行，並輸出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本節的其餘部分將說明不可改變和可變包裝的組成和含義。

### 不可變的內容包{#immutabe-content-packages}

所有保存在不可變儲存庫中的內容和代碼都必須簽入git並通過Cloud Manager部署。 換言之，與目前的解決方AEM案不同，程式碼永遠不會直接部署至執行中的AEM執行個體。 如此可確保在任何雲端環境中執行特定版本的程式碼都相同，如此可避免在生產時意外變更程式碼的風險。 例如，OSGI組態應提交至來源控制，而非透過網頁主控台的組態管理AEM員在執行時期進行管理。

由於交換機啟用了藍綠部署模式而導致的應用程式更改，因此它們不能依賴於可變儲存庫中的更改，但服務用戶、其ACL、節點類型和索引定義更改除外。

對於現有代碼庫的客戶，請務必進行文檔中介紹的儲存庫重構練習AEM，以確保將先前位於/etc下的內容移動到正確的位置。

不支援這些程式碼套件的其他限制，例如[install hooks](http://jackrabbit.apache.org/filevault/installhooks.html)。

## OSGI配置{#osgi-configuration}

如上所述，OSGI配置應提交給原始碼控制，而不是通過Web控制台。 這樣做的技巧包括：

* 使用Web控制台的配置管理器對開發AEM人員的本AEM地環境進行必要的更改，然後將結果導出到本地文AEM件系統上的項目
* 在本地檔案系統的項目中手AEM動建立OSGI配置，該配置引用AEM控制台的配置管理器的屬性名稱。

有關OSGI配置的更多資訊，請訪問[將OSGi配置AEM為Cloud Service](/help/implementing/deploying/configuring-osgi.md)。

## 可變內容{#mutable-content}

在某些情況下，在原始碼控制中準備內容更改可能會很有用，這樣，每當環境更新時，Cloud Manager就可以部署它。 例如，為某些根資料夾結構植入種子或在可編輯的模板中排列更改，以便為應用程式部署更新的元件啟用策略，這可能是合理的。

有兩種策略可描述Cloud Manager將部署到可變儲存庫、可變內容包和重新指向語句的內容。

### 可變內容包{#mutable-content-packages}

資料夾路徑階層、服務使用者和存取控制(ACL)等內容通常會提交至以原型為基礎的主AEM要專案。 技術包括從XMLAEM匯出或直接寫入。 在建立和部署過程中，Cloud Manager會封裝產生的可變內容封裝。 可變內容在流水線的部署階段中安裝的時間不同：

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
   * 上下文感知配置（`/conf`下的任何內容）（添加、修改、刪除）
   * 指令碼(軟體包可以在軟體包安裝過程中的各個階段觸發安裝掛接

可將可變內容安裝限制為製作或發佈，方法是將套件內嵌在`/apps`下的install.author或install.publish資料夾中。 在6.5中進行了重組，以反映AEM這一分離情況，建議的項目重組細節可在[AEM 6.5文檔中找到。](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>內容包部署到所有環境類型(dev、stage、prod)。 無法將部署限制在特定環境。 此限制是為了確保自動執行測試執行的選項。 特定於環境的內容需要通過Package Manager手動安裝。

此外，在套用可變內容包更改後，沒有回滾這些更改的機制。 如果客戶發現問題，可以選擇在下次代碼發行中修正問題，或作為最後手段，將整個系統還原到部署之前的某個時間點。

所有包含的第三方軟體包都必須經過驗證AEM為與Cloud Service服務相容，否則其包含將導致部署失敗。

如上所述，現有代碼庫的客戶應符合[AEM 6.5文檔中描述的6.5儲存庫更改所需的儲存庫重構練習。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## 重新指向{#repoinit}

在以下情況下，最好在OSGI工廠配置中採用手動編碼方式建立顯式內容`repoinit`語句：

* 建立／刪除／禁用服務用戶
* 建立／刪除群組
* 建立／刪除使用者
* 添加ACL

   >[!NOTE]
   >
   >定義ACL要求節點結構已存在。 因此，可能需要在建立路徑語句之前執行。

* 添加路徑（例如根資料夾結構）
* 新增CND（nodetype定義）

由於以下優點，因此，最好對這些支援的內容修改使用案例進行重新分析：

* Repoinit會在啟動時建立資源，讓邏輯可以將這些資源的存在視為已授予。 在可變內容封裝方法中，資源是在啟動後建立的，因此依賴資源的應用程式碼可能會失敗。
* Repoinit是相對安全的指令集，因為您明確控制要執行的動作。 此外，除了允許移除使用者、服務使用者和群組的少數安全性相關案例外，唯一支援的作業是加入的。 相反，移除可變內容包方法中的某些內容是明確的； 當您定義篩選器時，篩選器所涵蓋的任何項目都會被刪除。 不過，我們仍應小心謹慎，因為如果有任何內容，新內容的存在可能會改變應用程式的行為。
* Repoinit可執行快速和原子操作。 相比之下，可變內容封裝可以高度依賴於濾鏡所覆蓋的結構。 即使您更新單個節點，也可能建立大型樹的快照。
* 可在運行時驗證本地開發環境上的repoinit語句，因為這些語句將在註冊OSGi配置時執行。
* 重新指向語句是原子和顯式語句，如果狀態已匹配，則將跳過。

當Cloud Manager部署應用程式時，它會執行這些陳述式，而與安裝任何內容套件無關。

要建立重新指向語句，請遵循以下過程：

1. 將工廠PID `org.apache.sling.jcr.repoinit.RepositoryInitializer`的OSGi配置添加到項目的配置資料夾中。 請為設定使用描述性名稱，例如&#x200B;**org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 將重新指向語句添加到配置的指令碼屬性中。 語法和選項記錄在[Sling documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html)中。 請注意，在父資料夾的子資料夾之前應明確建立父資料夾。 例如，在`/content/myfolder`之前、在`/content/myfolder/mysubfolder`之前明確建立`/content`。 對於在低級結構上設定的ACL，建議將其設定在更高級別上，並使用`rep:glob`限制。  例如`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在執行時期在本機開發環境上驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>對於為`/apps`或`/libs`下的節點定義的ACL，重新指向的執行將在空白儲存庫上啟動。 軟體包在重新指向後安裝，因此語句不能依賴於軟體包中定義的任何內容，但必須定義諸如下面的父結構之類的先決條件。

>[!TIP]
>
>對於ACL，建立深層結構可能很麻煩，因此更合理地在更高級別定義ACL並限制它應通過rep:glob限制執行的位置。

有關repoinit的更多詳細資訊，請參閱[Sling documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可變內容包的包管理器{#package-manager-oneoffs-for-mutable-content-packages}的「一次性」

有些使用案例會將內容套件安裝為「一次性」。 例如，將特定內容從生產導入到測試階段，以除錯生產問題。 對於這些情況，可將包管理器用作AEMCloud Service環境。

由於Package Manager是執行時期概念，因此無法將內容或代碼安裝到不可變的儲存庫中，因此這些內容包只能由可變的內容（主要是`/content`或`/conf`）組成。 如果內容包含混合的內容（可變內容和不可變內容），則只安裝可變內容。

透過Cloud Manager安裝的任何內容封裝（可變和不可變），都會出現在AEMPackage Manager的使用者介面中，處於凍結狀態。 這些軟體包無法重新安裝、重建或甚至下載，並且將以&#x200B;**&quot;cp2fm&quot;**&#x200B;字尾列出，表示其安裝由Cloud Manager管理。

### 包括第三方包{#including-third-party}

客戶通常會從第三方來源(如Adobe翻譯合作夥伴等軟體供應商)中加入預先構建的軟體包。 建議將這些軟體包裝載在遠程儲存庫中，並在`pom.xml`中引用它們。 對於公共儲存庫和具有密碼保護的專用儲存庫，這是可能的，如[密碼保護的maven儲存庫](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)中所述。

如果無法將軟體包儲存在遠程儲存庫中，客戶可以將軟體包放在基於檔案系統的本地Maven儲存庫中，該儲存庫作為項目的一部分提交到SCM ，並由任何依賴它的系統引用。 儲存庫將在項目提示中聲明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的協力廠商套件都必須遵守本文AEM所述之Cloud Service服務編碼與封裝准則，否則，其包含將會導致部署失敗。

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

## 滾動部署如何運作{#how-rolling-deployments-work}

與更AEM新一樣，客戶版本也使用滾動部署策略進行部署，以便在適當的情況下消除作者群集停機。 事件的一般順序如下所述，其中&#x200B;**Blue**&#x200B;是舊版客戶代碼，而&#x200B;**Green**&#x200B;是新版本。 藍色和綠色都執行相同版本的程AEM式碼。

* 藍色版本處於活動狀態，並且已構建並提供綠色版本候選版本
* 如果有任何新的或更新的索引定義，則會處理相應的索引。 請注意，藍色部署將始終使用舊索引，而綠色部署將始終使用新索引。
* Blue仍在服務時，Green正在啟動
* Blue is running and serving while Green is checked for readiness via health checks
* 已準備好接受通信的綠色節點並替換已關閉的藍色節點
* 隨著時間的推移，藍色節點被綠色節點替換，直到只保留綠色節點，從而完成部署
* 部署任何新的或修改的可變內容

## 索引{#indexes}

新的或修改的索引將在新的（綠色）版本開始處理流量之前，導致額外的索引建立或重新建立索引步驟。 有關作為Cloud Service的索AEM引管理的詳細資訊，請參閱本文[。 ](/help/operations/indexing.md)您可以在Cloud Manager構建頁面上檢查索引作業的狀態，並在新版本準備就緒時收到通知。

>[!NOTE]
>
>滾動部署所需的時間會因索引的大小而異，因為生成新索引之前，綠色版本無法接受流量。

目前，因AEM為Cloud Service無法使用索引管理工具，例如ACS Commons Ensure Oak Index工具。

## 複寫 {#replication}

發佈機制向後相容[AEM複製Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)。

為了使用雲即用快速啟動進行複製開發和測AEM試，需要將傳統複製功能與「作者／發佈」設定一起使用。 如果AEM Author的UI登入點已針對雲端移除，使用者會前往`http://localhost:4502/etc/replication`進行設定。

## 滾動部署的向後相容代碼{#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM由於Cloud Service的滾動部署策略意味著新舊版本可能同時運行。 因此，請謹慎處理程式碼變更，這些變更不向後相容於AEM仍在運作的舊版本。

此外，舊版應測試是否與新版套用的任何新可變內容結構相容，因為不會移除可變內容。

### 服務用戶和ACL更改{#service-users-and-acl-changes}

更改訪問內容或代碼所需的服務用戶或ACL可能會導致舊版中AEM的錯誤，從而導致對過時服務用戶訪問該內容或代碼。 為瞭解決此行為，建議您至少在2個版本中進行變更，第一個版本在後續版本中先充當橋梁。

### 索引更改{#index-changes}

如果對索引進行了更改，Blue版本應繼續使用其索引，直到其終止，而Green版本則使用其自己修改的索引集。 開發人員應遵循本文](/help/operations/indexing.md)所述的索引管理技術。[

### 回滾的保守編碼{#conservative-coding-for-rollbacks}

如果在部署後報告或檢測到故障，則可能需要回滾到Blue版本。 最好確保藍色代碼與綠色版本建立的任何新結構相容，因為新結構（任何可變內容內容）將不會回退。 如果舊程式碼不相容，則需要在後續的客戶版本中套用修正。

## 運行模式{#runmodes}

在現有AEM的解決方案中，客戶可以選擇以任意執行模式來執行例項，並套用OSGI設定或將OSGI組合安裝至這些特定例項。 定義的運行模式通常包括&#x200B;*service*（作者和發佈）和環境(dev、stage、prod)。

另一AEM方面，Cloud Service對於哪些運行模式可用，以及如何將OSGI捆綁包和OSGI配置映射到它們有更多看法：

* OSGI配置運行模式必須參考dev、stage、prod for the environment或author, publish for the service。 支援`<service>.<environment_type>`的組合，但必須按此特定順序使用`author.dev`或`publish.prod`。 OSGI Token應直接從程式碼引用，而不是使用`getRunModes`方法，此方法在執行時期將不再包含`environment_type`。 如需詳細資訊，請參閱[將OSGi設AEM定為Cloud Service](/help/implementing/deploying/configuring-osgi.md)。
* OSGI組合的執行模式僅限於服務（作者、發佈）。 Per-run mode OSGI bundles should be installed in the content package under `install/author` or `install/publish`.

和現有的解AEM決方案一樣，無法使用執行模式來僅安裝特定環境或服務的內容。 如果想要為未在舞台或生產環境中的資料或HTML建立開發環境，則可使用封裝管理員。

支援的執行模式組態包括：

* **config** (*預設值，套用至所有AEM服務*)
* **config.author** (套&#x200B;*用至所有AEM Author服務*)
* **config.author.dev** (適&#x200B;*用於AEMDev Author服務*)
* **config.author.stage** (*適用於AEMStaging Author服務*)
* **config.author.prod** (*適用於AEMProduction Author服務*)
* **config.publish** (套&#x200B;*用至AEM Publish服務*)
* **config.publish.dev** (*套用至AEMDev Publish服務*)
* **config.publish.stage** (*套用至AEM測試發佈服務*)
* **config.publish.prod** (*套用至AEMProduction Publish服務*)
* **config.dev** (*適用於開AEM發服務)
* **config.stage** (*適用於AEMStaging Services)
* **config.prod** (*適用於生AEM產服務)

會使用最符合執行模式的OSGI設定。

在本機開發時，可傳入runmode啟動參數，以指定將使用哪個runmode OSGI組態。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Source Control {#maintenance-tasks-configuration-in-source-control}中的維護任務配置

維護任務配置必須保留在原始碼控制中，因為&#x200B;**工具>操作**&#x200B;螢幕將不再可用於雲環境。 這有利於確保變革是蓄意持續的，而不是反動地實施，甚至可能被遺忘。 如需詳細資訊，請參閱[維護工作文章](/help/operations/maintenance.md)。
