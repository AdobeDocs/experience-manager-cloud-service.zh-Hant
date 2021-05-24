---
title: '部署至 AEM as a Cloud Service '
description: '部署至 AEM as a Cloud Service  '
feature: 部署
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: abc41d6d9388a8ca63643bd2afd09982811ac490
workflow-type: tm+mt
source-wordcount: '3350'
ht-degree: 1%

---

# 部署至 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與AEM On Premise和Managed Services解決方案相比，AEM中程式碼開發的基礎與Cloud Service類似。 開發人員編寫程式碼並在本機測試，接著再將程式碼推送至遠端AEM作為Cloud Service環境。 需要Cloud Manager，這是Managed Services的選用內容傳送工具。 這是現在將程式碼部署至AEM做為Cloud Service環境的唯一機制。

[AEM版本](/help/implementing/deploying/aem-version-updates.md)的更新一律為個別部署事件，而非推送[自訂程式碼](#customer-releases)。 以其他方式檢視，自訂程式碼發行應針對生產環境中的AEM版本進行測試，因為這是將部署在頂端的程式碼。 AEM版本會更新後發生的，且會經常發生並自動套用。 它們旨在向後相容已部署的客戶代碼。

本檔案的其餘部分將說明開發人員如何調整其實務，以便搭配AEM作為Cloud Service的版本更新和客戶更新使用。

>[!NOTE]
>建議使用現有程式碼基底的客戶進行[AEM檔案](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中所述的存放庫重組練習。

## 客戶版本{#customer-releases}

### 根據正確的AEM版本{#coding-against-the-right-aem-version}編碼

針對先前的AEM解決方案，最新的AEM版本不常變更（大約每年每季提供一次Service Pack），客戶會自行將生產執行個體更新為最新的快速入門，並參考API Jar。 不過，AEM as a Cloud Service應用程式會更頻繁地自動更新為最新版本的AEM，因此內部版本的自訂程式碼應根據最新的AEM版本建置。

與現有非雲端AEM版本一樣，也支援以特定快速入門為基礎的本機離線開發，且大多數情況下，預期會是除錯的首選工具。

>[!NOTE]
>應用程式在本地電腦上的行為與Adobe雲之間存在細微的操作差異。 在本地開發過程中，必須尊重這些體系結構差異，並且在部署到雲基礎架構時，可能會導致不同的行為。 由於這些差異，在生產環境中推出新的自訂程式碼之前，請務必先對開發和預備環境執行詳盡的測試。

若要開發內部版本的自訂程式碼，應下載並安裝[AEM as aCloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的相關版本。 如需有關使用AEM作為Cloud ServiceDispatcher工具的其他資訊，請參閱[本頁](/help/implementing/dispatcher/disp-overview.md)。

以下影片概略介紹如何將程式碼部署至AEM as aCloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

>[!NOTE]
>建議使用現有程式碼基底的客戶進行[AEM檔案](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中所述的存放庫重組練習。

## 透過Cloud Manager和Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}部署內容套件

### 透過Cloud Manager {#deployments-via-cloud-manager}部署

客戶透過Cloud Manager將自訂程式碼部署至雲端環境。 請注意，Cloud Manager會將本機組裝的內容套件轉換為符合Sling功能模型的成品，這是在雲端環境中執行時，AEM作為Cloud Service應用程式的描述方式。 因此，在雲端環境上查看套件管理器中的套件時，名稱將包含「cp2fm」，且轉換的套件已移除所有中繼資料。 無法互動，亦即無法下載、複製或開啟。 有關轉換器的詳細文檔可以在[此處找到](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

為AEM作為Cloud Service應用程式編寫的內容套件必須在不可變和可變內容之間有乾淨的隔離，而Cloud manager只會安裝可變內容，並輸出如下的訊息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本節的其餘部分將介紹不可變和可變包的組成和含義。

### 不可變的內容包{#immutabe-content-packages}

所有保存在不可修改存放庫中的內容和程式碼都必須簽入git，並透過Cloud Manager部署。 換句話說，與目前的AEM解決方案不同，程式碼絕不會直接部署至執行中的AEM例項。 這可確保在任何雲端環境中針對指定版本執行的程式碼都相同，而可避免在生產環境中意外變更程式碼的風險。 例如，OSGI設定應提交至原始碼控制項，而非透過AEM Web主控台的設定管理員在執行階段進行管理。

由於交換機啟用了藍綠色部署模式，因此應用程式更改不能依賴於可變儲存庫中的更改，但服務用戶、其ACL、節點類型和索引定義更改除外。

若客戶有現有的程式碼基底，請務必進行AEM檔案中所述的存放庫重組練習，以確保先前位於/etc下的內容移至正確的位置。

不支援這些程式碼套件套用某些其他限制，例如[安裝鈎點](http://jackrabbit.apache.org/filevault/installhooks.html)。

## OSGI配置{#osgi-configuration}

如上所述，OSGI設定應提交至原始碼控制，而非透過Web主控台。 這樣做的技巧包括：

* 使用AEM Web主控台的組態管理員，對開發人員的本機AEM環境進行必要的變更，然後將結果匯出至本機檔案系統上的AEM專案
* 在本機檔案系統的AEM專案中手動建立OSGI設定，此元件會參照AEM主控台的屬性名稱組態管理器。

請前往[為AEM設定OSGi作為Cloud Service](/help/implementing/deploying/configuring-osgi.md)，深入了解OSGI設定。

## 可變內容{#mutable-content}

在某些情況下，在原始碼控制項中準備內容變更可能會很實用，這樣當環境更新時，Cloud Manager就能部署內容。 例如，為某些根資料夾結構種子或在可編輯的模板中排列更改，以便為那些由應用程式部署更新的元件啟用策略，這可能是合理的。

有兩種策略可描述Cloud Manager將部署到可變儲存庫、可變內容包和重新指向語句的內容。

### 可變內容包{#mutable-content-packages}

資料夾路徑階層、服務使用者和存取控制(ACL)等內容通常會提交至基於主架構的AEM專案。 技術包括從AEM匯出或直接寫入為XML。 在建置和部署程式期間，Cloud Manager會封裝產生的可變內容套件。 可變內容在管道的部署階段期間會安裝3次不同的時間：

新版應用程式啟動前：

* 索引定義（添加、修改、刪除）

在啟動新版本的應用程式期間，但在切換之前：

* 服務用戶（添加）
* 服務用戶ACL（添加）
* 節點類型（新增）

切換到新版本的應用程式後：

* 可透過jackrabbit保管庫定義的所有其他內容。 例如：
   * 資料夾（添加、修改、刪除）
   * 可編輯的範本（新增、修改、移除）
   * 內容感知配置（`/conf`下的任何項）（添加、修改、刪除）
   * 指令碼(軟體包可在軟體包安裝過程的各個階段觸發安裝掛接。 請參閱[Jackrabbit filevault檔案](http://jackrabbit.incubator.apache.org/filevault/installhooks.html)，了解安裝鈎點。 請注意，AEM CS目前使用Filevault 3.4.0版，此版本限制管理員使用者、系統使用者和管理員群組成員的安裝鈎點)。

可借由將套件內嵌在`/apps`下的install.author或install.publish資料夾中，將可變內容安裝限制為製作或發佈。 為反映這一分離，已在AEM 6.5中完成重組，建議的專案重組詳細資訊可在[AEM 6.5檔案中找到。](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>內容包部署到所有環境類型（開發、預備、生產）。 無法將部署限制在特定環境。 此限制的設定是為了確保自動執行的測試執行選項。 環境特定內容需要透過套件管理器手動安裝。

此外，在應用可變內容包更改後，沒有回滾這些更改的機制。 如果客戶檢測到問題，他們可以選擇在下一個代碼版本中修復問題，或作為最後手段，將整個系統恢復到部署之前的某個時間點。

任何包含的第三方套件都必須經過驗證，驗證為AEM as a Cloud Service服務相容，否則其包含會導致部署失敗。

如上所述，使用現有代碼庫的客戶應符合[AEM 6.5檔案中所述的6.5儲存庫更改所需的儲存庫重組練習。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## 重新指向 {#repoinit}

對於下列情況，最好採用手動編碼方法，在OSGI工廠配置中建立明確內容`repoinit`陳述式：

* 建立/刪除/禁用服務用戶
* 建立/刪除群組
* 建立/刪除使用者
* 添加ACL

   >[!NOTE]
   >
   >ACL的定義要求節點結構已存在。 因此，可能需要先建立路徑陳述式。

* 新增路徑（例如根資料夾結構）
* 新增CND（nodetype定義）

由於下列優點，這些支援的內容修改使用案例最好改用重點：

* Repoinit在啟動時會建立資源，這樣邏輯就能將這些資源的存在視為已授予。 在可變內容包方法中，資源是在啟動後建立的，因此依賴這些資源的應用程式代碼可能會失敗。
* 當您明確控制要採取的動作時，重新指示是相對安全的指令集。 此外，唯一支援的操作是附加操作，但少數安全相關案例除外，這些案例允許刪除用戶、服務用戶和組。 相反，移除可變內容包方法中的某些內容是明確的； 當您定義篩選器時，篩選器所涵蓋的任何項目都會遭到刪除。 不過，您仍應小心謹慎，因為如果有任何內容，出現新內容可能會改變應用程式的行為。
* 重新指定執行快速和原子操作。 相比之下，可變內容包可以高度取決於過濾器覆蓋的結構的效能。 即使更新單個節點，也可能建立大型樹的快照。
* 可以在運行時驗證本地開發環境上的repoinit語句，因為這些語句將在註冊OSGi配置時執行。
* 重新指向語句是原子的，且顯式，如果狀態已匹配，則將跳過。

Cloud Manager部署應用程式時，會執行這些陳述式，而不受安裝任何內容套件的影響。

要建立重新指向語句，請遵循以下過程：

1. 在專案的設定資料夾中，新增工廠PID `org.apache.sling.jcr.repoinit.RepositoryInitializer`的OSGi設定。 為設定使用描述性名稱，例如&#x200B;**org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 將重新指向語句添加到配置的指令碼屬性。 [Sling檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html)中記錄了語法和選項。 請注意，應在父資料夾的子資料夾之前明確建立父資料夾。 例如，在`/content/myfolder`之前、在`/content/myfolder/mysubfolder`之前明確建立`/content`。 對於在低級結構上設定的ACL，建議在高級別上設定ACL，並使用`rep:glob`限制。  例如`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在執行階段在本機開發環境上驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>對於為`/apps`或`/libs`下的節點定義的ACL，重新指向執行將在空白儲存庫上啟動。 程式包安裝在重新指向後，因此語句不能依賴程式包中定義的任何內容，但必須定義先決條件，如下面的父結構。

>[!TIP]
>
>對於ACL，建立深層結構可能很麻煩，因此在更高級別上定義ACL並限制它應通過rep:glob限制執行的位置更合理。

有關重新點擊的詳細資訊，請參閱[Sling檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可變內容包{#package-manager-oneoffs-for-mutable-content-packages}的包管理器「一次性」

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="套件管理器 — 移轉可變內容套件"
>abstract="探索套件管理器的使用案例，了解內容套件應安裝為「一次性」的使用案例，包括將特定內容從生產匯入測試環境，以偵錯生產問題、將小型內容套件從內部部署環境傳輸至AEM雲端環境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="內容轉移工具"

有些使用案例會將內容套件安裝為「一次性」。 例如，將特定內容從生產匯入測試環境，以偵錯生產問題。 對於這些情況，可在AEM中將套件管理器用作Cloud Service環境。

由於包管理器是運行時概念，因此無法將內容或代碼安裝到不可修改的儲存庫中，因此這些內容包應僅由可變內容（主要`/content`或`/conf`）組成。 如果內容包含混合的內容（可變和不可變內容），則僅安裝可變內容。

透過Cloud Manager安裝的任何內容套件（可變和不可變），都會在AEM Package Manager的使用者介面中顯示為凍結狀態。 無法重新安裝、重建或甚至下載這些軟體包，並將以&#x200B;**&quot;cp2fm&quot;**&#x200B;尾碼列出，表明其安裝由Cloud Manager管理。

### 包括第三方包{#including-third-party}

客戶通常會包含來自第三方來源(如Adobe的翻譯合作夥伴)的預先建立套件。 建議將這些包托管在遠程儲存庫中，並在`pom.xml`中引用它們。 公用儲存庫以及具有密碼保護的專用儲存庫都可以這樣做，如[受密碼保護的maven儲存庫](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)中所述。

如果無法將包儲存在遠程儲存庫中，則客戶可以將其置於基於本地檔案系統的Maven儲存庫中，該儲存庫作為項目的一部分提交到SCM，並由任何依賴它的資源引用。 儲存庫將在以下所示的項目計畫中聲明：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的協力廠商套件都必須遵守AEM，作為本文所述的Cloud Service服務編碼和封裝准則，否則，包含會導致部署失敗。

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

如同AEM更新，客戶版本也會使用滾動式部署策略進行部署，以在適當的情況下消除製作叢集的停機時間。 事件的一般順序如下所述，其中&#x200B;**Blue**&#x200B;是舊版客戶代碼，**Green**&#x200B;是新版本。 藍色和綠色執行的AEM程式碼版本相同。

* 藍色版本處於活動狀態，並且已建立並提供綠色的候選版本
* 如果有任何新的或更新的索引定義，則會處理相應的索引。 請注意，藍色部署將始終使用舊索引，而綠色部署將始終使用新索引。
* 綠色正在啟動，而藍色仍在使用
* 藍色正在運行且正在使用，同時正在通過運行狀況檢查檢查來檢查綠色是否就緒
* 已準備好接受流量的綠色節點，會取代已關閉的藍色節點
* 隨著時間的推移，藍色節點會取代為綠色節點，直到僅保留綠色為止，因此完成部署
* 部署任何新內容或修改的可變內容

## 索引 {#indexes}

新的或修改的索引將導致在新的（綠色）版本可用於流量之前執行額外的索引或重新索引步驟。 有關AEM as aCloud Service中索引管理的詳細資訊，請參閱[本文](/help/operations/indexing.md)。 您可以在Cloud Manager建置頁面上檢查索引作業的狀態，並在新版本準備好接收流量時收到通知。

>[!NOTE]
>
>滾動部署所需的時間會因索引的大小而異，因為綠色版本在生成新索引之前無法接受流量。

目前，AEM as aCloud Service無法搭配索引管理工具（例如ACS Commons Ensure Oak Index）工具使用。

## 複寫 {#replication}

發佈機制向後相容於[AEM復寫Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)。

若要使用雲端就緒型AEM快速入門來開發和測試復寫功能，必須搭配「作者/發佈」設定使用傳統復寫功能。 如果AEM Author的UI進入點已針對雲端移除，使用者會前往`http://localhost:4502/etc/replication`進行設定。

## 滾動部署的向後相容代碼{#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM as aCloud Service的滾動式部署策略表示舊版和新版本可能同時運作。 因此，請小心，回溯不相容於舊版AEM仍在運作的程式碼變更。

此外，應測試舊版本在回滾時與新版本所套用的任何新可變內容結構是否相容，因為可變內容並未移除。

### 服務用戶和ACL更改{#service-users-and-acl-changes}

變更服務使用者或存取內容或程式碼所需的ACL，可能會導致舊版AEM發生錯誤，導致過時的服務使用者存取該內容或程式碼。 若要解決此問題，建議您先將變更擴散至至少2個版本，第一個版本先充當橋接器，然後再於後續版本中進行清理。

### 索引更改{#index-changes}

如果對索引進行了更改，則Blue版本必須繼續使用其索引，直到其終止，而Green版本則使用其自己修改的索引集。 開發人員應遵循本文](/help/operations/indexing.md)中描述的索引管理技術。[

### 回傳的保守編碼{#conservative-coding-for-rollbacks}

如果在部署後報告或檢測到故障，則可能需要回滾到藍色版本。 最好確保藍色代碼與綠色版本建立的任何新結構相容，因為新結構（任何可變內容內容）將不會回滾。 如果舊程式碼不相容，則需要在後續的客戶版本中套用修正。

## 執行模式 {#runmodes}

在現有的AEM解決方案中，客戶可以選擇以任意執行模式執行例項，並套用OSGI設定或將OSGI套件組合安裝至這些特定例項。 定義的執行模式通常包括&#x200B;*service*（製作和發佈）和環境(dev、stage、prod)。

另一方面，AEM as aCloud Service則對哪些執行模式可用，以及OSGI套件組合和OSGI組態如何對應到這些模式更有意見：

* OSGI設定執行模式必須參考開發、預備、環境產品或製作、服務發佈。 支援`<service>.<environment_type>`的組合，但必須以此特定順序使用（例如`author.dev`或`publish.prod`）。 OSGI代號應直接從程式碼參考，而非使用`getRunModes`方法，這在執行階段將不再包含`environment_type`。 如需詳細資訊，請參閱[為AEM as aCloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md)。
* OSGI套件組合執行模式僅限於服務（製作、發佈）。 每個執行模式的OSGI套件組合應安裝在`install/author`或`install/publish`下的內容套件中。

與現有的AEM解決方案一樣，您無法使用執行模式來僅為特定環境或服務安裝內容。 如果想要為開發環境植入資料或HTML，而該環境不在預備或生產環境中，則可使用套件管理程式。

支援的執行模式設定包括：

* **設定** (*預設值，套用至所有AEM服務*)
* **config.author** (*適用於所有AEM Author服務*)
* **config.author.dev** (*適用於AEM Dev Author服務*)
* **config.author.stage** (*適用於AEM Staging Author服務*)
* **config.author.prod** (*套用至AEM Production Author服務*)
* **config.publish** (*套用至AEM Publish服務*)
* **config.publish.dev** (*套用至AEM Dev Publish服務*)
* **config.publish.stage** (*套用至AEM Staging Publish服務*)
* **config.publish.prod** (*套用至AEM Production Publish服務*)
* **config.dev** (*適用於AEM Dev服務)
* **config.stage** (*適用於AEM Staging服務)
* **config.prod** (*適用於AEM Production Services)

系統會使用最符合執行模式的OSGI設定。

在本機開發時，可將執行模式啟動參數傳入，以指定將使用哪個執行模式OSGI設定。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 原始碼控制項{#maintenance-tasks-configuration-in-source-control}中的維護任務配置

維護任務配置必須保留在原始碼控制中，因為&#x200B;**工具>操作**&#x200B;螢幕將不再在雲環境中可用。 這有益於確保更改被有意保留，而不是被重新應用，或許被遺忘。 有關詳細資訊，請參考[維護任務文章](/help/operations/maintenance.md)。
