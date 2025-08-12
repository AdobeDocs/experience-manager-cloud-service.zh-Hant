---
title: '部署至 AEM as a Cloud Service '
description: 了解部署至 AEM as a Cloud Service 的基礎知識和最佳做法
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '3440'
ht-degree: 93%

---

# 部署至 AEM as a Cloud Service  {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與 AEM On Premise 和 Managed Services 解決方案相比，AEM as a Cloud Service 的程式碼開發基礎相似。開發人員編寫程式碼並在本機進行測試，然後將程式碼推送到遠端 AEM as a Cloud Service 環境。需要有 Cloud Manager，這是 Managed Services 的選用內容傳遞工具。此傳遞工具現在是將程式碼部署到 AEM as a Cloud Service 環境、階段和生產環境的唯一機制。為了在部署前述環境之前進行快速功能驗證和除錯，可以將程式碼從本機環境同步到[快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md)。

[AEM 版本](/help/implementing/deploying/aem-version-updates.md) 的更新始終是獨立於推送[自訂程式碼](#customer-releases) 的部署事件。從另一個角度來看，自訂程式碼版本應該針對 AEM 生產版本進行測試，因為它部署在頂端。之後發生的AEM版本更新（經常使用且會自動套用），旨在與已部署的客戶程式碼回溯相容。

本文件的其餘部分在描述開發人員應如何調整他們的做法，以便他們同時使用 AEM as a Cloud Service 的版本更新和客戶更新。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客戶發行版本 {#customer-releases}

### 針對正確的 AEM 版本編寫程式碼 {#coding-against-the-right-aem-version}

對於以前的 AEM 解決方案，最新的 AEM 版本很少更改 (大約每年更換每季的 Service Pack)，客戶會根據自己的時間將生產執行個體更新到最新的快速啟動，參考 API Jar。但是，AEM as a Cloud Service 上的應用程式會更頻繁地自動更新到最新版本 AEM，因此應針對最新版本 AEM 建置內部版本的自訂程式碼。

與現有的非雲端 AEM 版本一樣，以特定快速入門為基礎的本機離線開發受支援，通常會成為首選的偵錯工具。

>[!NOTE]
>應用程式在本機電腦的行為與在 Adobe Cloud 上的行為有細微差異。在本機開發過程中必須考慮這些架構差異，在雲端基礎結構上部署時可能會導致不同的行為。由於這些差異，在生產環境中推出新的自訂程式碼之前，在開發和中繼環境中執行詳盡的測試非常重要。

若要為內部版本開發自訂程式碼，應下載並安裝相關版本的 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。如需使用AEM as a Cloud Service Dispatcher工具的其他資訊，請參閱[雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md)。

以下影片提供了有關如何將程式碼部署到 AEM as a Cloud Service 的概略說明：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 透過 Cloud Manager 和封裝管理員部署內容套件 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 透過 Cloud Manager 部署 {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

客戶透過 Cloud Manager 將自訂程式碼部署到雲端環境。Cloud Manager 將本機組裝的內容套件轉換為符合 Sling Feature Model 的成品，這就是在雲端環境中執行時描述 AEM as a Cloud Service 上的應用程式的方式。因此，在雲端環境中查看 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 中的套件時，名稱包含「cp2fm」，並且轉換後套件已刪除所有中繼資料。它們無法互動，這表示它們無法下載、複製或開啟。如需轉換器的詳細檔案，請參閱GitHub[上的](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)sling-org-apache-sling-feature-cpconverter 。

為 AEM as a Cloud Service 上的應用程式編寫的內容套件必須明確區分不可變內容和可變內容，Cloud Manager 僅安裝可變內容，同時輸出如下訊息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本章節的其餘部分會描述不可變和可變套件的構成和含義。

### 不可變內容套件 {#immutabe-content-packages}

永久存放在不可變存放庫的中的所有內容和程式碼都必須簽入 git 並透過 Cloud Manager 進行部署。換句話說，與目前 AEM 解決方案不同，程式碼永遠不會直接部署到執行中的 AEM 執行個體。此工作流程確保了在任何雲端環境中為特定版本執行的程式碼是相同的，從而消除了程式碼在生產環境意外發生變化的風險。例如，OSGI 設定應交給原始檔控制，而不是在執行階段透過 AEM 網頁主控台的 Configuration Manager 管理。

由於部署模式導致的應用程式變更會由開關啟用，因此它們不能仰賴可變存放庫中的變更，但服務使用者、其 ACL、節點類型和索引定義變更除外。

對於擁有現有程式碼庫的客戶，至關重要的是完成 AEM 文件描述的存放庫重組練習，以確保將以前位於 /etc 下的內容移動到正確的位置。

這些程式碼套件會套用一些其他限制，例如，不支援[安裝鉤點](https://jackrabbit.apache.org/filevault/installhooks.html)。

## OSGI 設定 {#osgi-configuration}

如上所述，OSGI 設定應該提交給原始檔控制，而不是透過 Web 主控台。相關的技術包括：

* 使用 AEM Web 主控台的 Configuration Manager 對開發人員的本機 AEM 環境進行必要的變更，然後將結果匯出到本機檔案系統上的 AEM 專案。
* 手動在本機檔案系統的 AEM 專案中建立 OSGI 設定，為屬性名稱參考 AEM 主控台的 Configuration Manager。

在[為 AEM as a Cloud Service 設定 OSGi](/help/implementing/deploying/configuring-osgi.md) 閱讀有關 OSGI 設定的詳細資訊。

## 可變內容 {#mutable-content}

有時，在原始檔碼管理中準備內容變更可能很有用，如此在環境更新時 Cloud Manager 就可以部署。例如，植入特定根資料夾結構可能是合理的。或者，排列可編輯範本中的變更以啟用由應用程式部署更新的政策元件。

有兩種策略可用來描述 Cloud Manager 部署到可變存放庫的內容、可變內容套件和 `repoinit` 陳述式。

### 可變內容套件 {#mutable-content-packages}

資料夾路徑階層、服務使用者和存取控制 (ACL) 等內容通常會提交到 Maven 原型 AEM 專案中。技術包括從 AEM 匯出或直接寫成 XML。在建置和部署流程中，Cloud Manager 會封裝產生的可變內容套件。可變內容在管道部署階段的三個不同時間安裝：

在啟動新版本應用程式之前：

* 索引定義 (新增、修改、移除)

在啟動新版本應用程式期間但在切換之前：

* 服務使用者 (新增)
* 服務使用者 ACL (新增)
* 節點類型 (新增)

切換到新版本應用程式之後：

* 可透過 jackrabbit 保存庫定義的所有其他內容。例如：
   * 資料夾 (新增、修改、移除)
   * 可編輯的範例 (新增、修改、移除)
   * 內容感知設定 (`/conf` 下的任何內容) (新增、修改、移除)
   * 指令碼 (可以在套件安裝流程的各個階段觸發安裝 Hook。請參閱 [Jackrabbit Filevault 文件](https://jackrabbit.apache.org/filevault/installhooks.html)，瞭解如何安裝 Hook。AEM CS 目前使用 Filevault 版本 3.4.0，它將安裝 Hook 限制為管理員使用者、系統使用者和管理員群組的成員))。

透過在 `/apps`下的 install.author 或 install.publish 資料夾中嵌入套件，可以將可變內容安裝限制在編寫或發佈。反映此分隔的重組已在AEM 6.5中完成，而有關建議的專案重組的詳細資訊可在[AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=zh-Hant)中找到。

>[!NOTE]
>內容套件部署到所有環境類型 (開發、中繼、生產)。不可能將部署限制在特定環境中。此限制的目的是在確保可以選擇對自動執行進行測試執行。特定於環境的內容需要透過 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 手動安裝

此外，在套用可變內容套件變更後，沒有任何機制可以回復這些變更。如果客戶偵測到問題，他們可以選擇在下一個程代碼版本中進行修復，或者採取最後手段，將整個系統還原到部署前的某個時間點。

任何包含的協力廠商套件都必須驗證為與 AEM as a Cloud Service 相容，否則包含該套件會導致部署失敗。

如上所述，擁有現有程式碼庫的客戶應符合[AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=zh-Hant)中說明的6.5存放庫變更所需的存放庫重組作業。

## repoinit {#repoinit}

對於以下情況，最好採用在 OSGI 工廠設定中手動編寫明確內容建立 `repoinit` 陳述式的方法：

* 建立/刪除/停用服務使用者
* 建立/刪除群組
* 建立/刪除使用者
* 新增 ACL

  >[!NOTE]
  >
  >ACL 的定義要求已存在的節點結構。因此，前面必須要有建立路徑陳述式。

* 新增路徑（例如，根資料夾結構的路徑）
* 新增 CND (節點類型定義)

由於以下好處，repoinit 更適合這些受支援的內容修改使用案例：

* `Repoinit` 在啟動時會建立資源，因此邏輯可以視這些資源的存在是理所當然的。在可變內容套件方法中，資源是在啟動後建立的，因此依賴它們的應用程式的程式碼可能會失敗。
* `Repoinit` 是一個相對安全的指令集，因為您可以明確控制要進行的動作。此外，除了一些允許刪除使用者、服務使用者和群組的安全相關情況外，唯一支援的操作是相加。相反，在可變內容套件方法中刪除某些內容是明確的；當您定義篩選器時，篩選器涵蓋的任何內容都會被刪除。儘管如此，仍應謹慎，因為對於任何內容，在某些情況下，新內容的存在可能會改變應用程式的行為。
* `Repoinit` 執行快速和不可部分完成作業。相反地，可變內容套件在效能上高度依賴於篩選器涵蓋的結構。即使您更新單一節點，也可能會建立大型樹狀的快照。
* 可以在執行階段於本機開發環境中驗證 `repoinit` 陳述式，因為它們將在 OSGi 設定註冊時執行。
* `Repoinit` 陳述式是不可部分完成和明確的，如果狀態已相符會跳過。

當 Cloud Manager 部署應用程式時，它會獨立於任何內容套件的安裝，執行這些陳述式。

若要建立 `repoinit` 陳述式，請依照以下程序進行：

1. 在專案的設定資料夾中為工廠 PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` 新增 OSGi 設定。為設定使用描述性名稱，例如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 將 `repoinit` 陳述句新增至 config 的指令碼屬性中。[Sling 文件](https://sling.apache.org/documentation/bundles/repository-initialization.html) 中記錄了語法和選項。應先明確建立父資料夾再建立其子資料夾。例如，在 `/content/myfolder` 之前明確建立 `/content`，再建立 `/content/myfolder/mysubfolder`。對於設立在低層級結構上的 ACL，建議將其設定在更高層級並使用 `rep:glob` 限制。例如，`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在執行階段時於本機開發環境上進行驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>對於為 `/apps` 或 `/libs` 下的節點定義的 ACL，`repoinit` 執行會從空白存放庫開始。這些套件是在 `repoinit` 之後安裝的，因此陳述句不能依賴在套件中定義的任何內容，但必須定義先決條件，例如下面的父結構。

>[!TIP]
>
>對於 ACL，建立深層結構可能很麻煩。因此，在更高層級定義 ACL 並透過 `rep:glob`限制來約束其作用位置會更為合理。

如需有關 `repoinit` 的詳細資訊，請參閱 [Sling 文件](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可變內容套件的封裝管理員「一次性」 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="封裝管理員 - 移轉可變內容套件"
>abstract="探索封裝管理員在使用案例中的使用情況，在這些案例中，內容套件的安裝應為「一次性」。此安裝包括將特定內容從生產環境匯入至中繼環境以偵錯生產問題，將小型內容套件從內部部署環境轉移至 AEM 雲端環境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=zh-Hant" text="內容轉移工具"

在某些使用案例中，內容套件應做為「一次性」安裝。例如，將特定內容從生產環境匯入至中繼環境以偵錯生產問題。對於這些情況，[封裝管理員](/help/implementing/developing/tools/package-manager.md) 可以用在 AEM as a Cloud Service 中的環境。

由於封裝管理員是一個執行階段概念，不可能將內容或程式碼安裝到不可變存放庫中，因此這些內容套件應該只包含可變內容 (主要是 `/content` 或 `/conf`)。如果內容套件包含混合內容 (可變內容和不可變內容)，則只會安裝可變內容。

>[!IMPORTANT]
>
>如果安裝套件的時間超過十分鐘，封裝管理員使用者介面可能會傳回&#x200B;**未定義**&#x200B;錯誤訊息。
>
>這次不是因為安裝錯誤，而是由於 Cloud Service 對所有的要求逾時。
>
>如果您看到此類錯誤，請不要重試安裝。安裝作業正在背景正確進行。如果您真的重新啟動安裝，則多個並行匯入流程可能會造成一些衝突。

任何透過 Cloud Manager 安裝的內容套件 (可變和不可變) 都會以凍結狀態出現在 AEM 封裝管理員使用者介面中。這些套件無法重新安裝、重新建置甚至下載，並且字尾會出現 **「cp2fm」**，表示其安裝是由 Cloud Manager 管理。

### 包括協力廠商套件 {#including-third-party}

客戶通常會包含來自協力廠商來源 (例如 Adobe 翻譯合作夥伴等軟體供應商) 的預建套件。建議將這些套件託管在遠端存放庫中，並在 `pom.xml`中參考它們。此方法對於公共存放庫和具有密碼保護的私有存放庫都是可能的，如[密碼保護的 maven 存放庫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)中所述。

如果無法將套件存放在遠端存放庫中，客戶可以將其放在本機、檔案系統式 Maven 存放庫中，該存放庫會以專案的一部分提交給 SCM。由依賴它的任何內容參照。該存放庫會在專案 pom 中宣告，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何內含的第三方套件都必須遵守本文所述的 AEM as a Cloud Service 編碼和封裝指引，否則將其納入會導致部署失敗。

以下 Maven`POM.xml` 程式碼片段顯示如何透過 **filevault-package-maven-plugin** Maven 增效模組設定，將協力廠商套件嵌入在專案的「容器」套件中，通常稱為 **&#39;all&#39;**。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## 滾動部署的工作原理 {#how-rolling-deployments-work}

如同 AEM 更新，客戶版本使用滾動部署策略進行部署，以便在適當的情況下消除作者叢集停機時間。事件的一般序列如下所述，其中新舊版本客戶代碼的節點正在執行相同版本的 AEM 程式碼。

* 舊版本的節點處於使用中狀態，且新版本的候選發佈版本已建置並可供使用。
* 如果有任何新的或更新的索引定義，即會處理對應的索引。請注意，舊版本的節點會一律使用舊索引，而新版本的節點則一律使用新索引。
* 舊版本仍在為流量提供服務時，新版本的節點即會啟動。
* 透過健康檢查來檢查新版本的節點是否就緒時，舊版本的節點正在執行並繼續提供服務。
* 已就緒的新版本節點會接受流量，並取代已關閉的舊版本節點。
* 舊版本的節點會隨著時間被新版本的節點取代，直到只剩下新版本的節點，如此即完成部署。
* 接著即會部署任何新的或修改的可變內容.

## 索引 {#indexes}

在新版本可以處理流量之前，新的或修改的索引會導致額外的建立索引或重新索引步驟。有關AEM as a Cloud Service中索引管理的詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md)。 您可以在 Cloud Manager 檢查建置頁面的建立索引狀態，並在新版本準備就緒可接收流量時收到通知。

>[!NOTE]
>
>滾動部署所需的時間根據索引的大小而有所不同。原因是新版本在產生新索引之前無法接受流量。

目前，AEM as a Cloud Service 無法與 ACS Commons Ensure Oak Index 工具等索引管理工具搭配使用。

## 複製 {#replication}

發佈機制可回溯相容於 [AEM Replication Java™ API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)。

為了使用 cloud ready AEM 快速入門來開發和測試複製，傳統複製功能必須與作者/發佈設定一起使用。如果 AEM Author 的使用者介面進入點已針對雲端刪除，使用者將移至 `http://localhost:4502/etc/replication` 進行設定。

## 回溯相容程式碼以進行滾動部署 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM as a Cloud Service 的滾動部署策略表示新舊版本可能同時執行。因此，請注意程式碼變更是否無法回溯相容於仍在運作的舊版 AEM。

此外，如果回復，應測試舊版本是否相容於新版本套用的任何新可變內容結構，因為可變內容不會被刪除。

### 服務使用者和 ACL 變更 {#service-users-and-acl-changes}

變更存取內容或程式碼的服務使用者和 ACL，可能會導致 AEM 舊版本出現錯誤，從而導致使用過時的服務使用者存取該內容或程式碼。若要解決此行為，建議將變更分佈在至少兩個版本中，其中第一個版本在後續版本中清除前會充當連結。

### 索引變更 {#index-changes}

如果對索引進行了變更，則舊版本繼續使用其索引直到終止很重要，而新版本則使用自己的修改索引集。 開發人員應遵循[內容搜尋與索引](/help/operations/indexing.md)中所述的索引管理技術。

### 針對回復作業的保守編碼 {#conservative-coding-for-rollbacks}

如果部署後有回報或偵測到故障，則可能需要回復至舊版本。確保新程式碼和新版本建立的任何新結構相容，因為新結構 (任何可變內容) 不會回復。如果舊程式碼不相容，則必須在後續的客戶版本中套用修復。

## 快速開發環境 (RDE) {#rde}

[快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) (或簡稱 RDE) 允許開發人員快速部署和查看變動情形，可中大幅減少測試已證明可在本機開發環境中執行功能所需的時間。

與透過 Cloud Manager 管道部署程式碼的一般開發環境不同，開發人員會使用命令行工具將程式碼從本機開發環境同步到 RDE。在 RDE 中成功測試變動內容，這些變動應該透過 Cloud Manager 管道部署到一般雲端開發環境，這將使程式碼能通過適當的品質關卡。

## 執行模式 {#runmodes}

在現有的 AEM 解決方案中，客戶可以選擇以任意執行模式來使執行個體運作，並在這些特定執行個體套用 OSGI 設定或安裝 OSGI 套裝。定義的執行模式通常包括&#x200B;*服務* (編寫和發佈) 與環境 (快速開發環境、開發、中繼、生產)。

另一方面，AEM as a Cloud Service 對於哪些執行模式可用，以及如何將 OSGI 套裝和 OSGI 設定對應到它們更有自己的做法：

* OSGI 設定執行模式必須參照快速開發環境、開發、中繼、生產環境，或編寫、發佈服務。支援`<service>.<environment_type>`的組合，但這些環境必須以此特定順序使用（例如，`author.dev`或`publish.prod`）。 應直接從程式碼中參考 OSGI 權杖，而不是使用 `getRunModes` 方法，後者在執行階段不再包含 `environment_type`。如需詳細資訊，請參閱[為 AEM as a Cloud Service 設定 OSGi](/help/implementing/deploying/configuring-osgi.md)。
* OSGI 套裝執行模式限制在服務 (編寫、發佈)。預執行模式 OSGI 套裝應安裝在 `install.author` 或 `install.publish` 下的內容套件中。

AEM as a Cloud Service 不允許使用執行模式為特定環境或服務安裝內容。如果開發環境必須使用中繼或生產環境中不存在的資料或 HTML 進行植入，則可以使用封裝管理員。

支援的執行模式設定：

* **config** (*預設值，套用到所有 AEM 服務*)
* **config.author** (*套用到所有 AEM Author 服務*)
* **config.author.dev** (*套用到 AEM Dev Author 服務*)
* **config.author.rde** (*套用到所有 AEM RDE Author 服務*)
* **config.author.stage** (*套用到 AEM Staging Author 服務*)
* **config.author.prod** (*套用到 AEM Production Author 服務*)
* **config.publish** (*套用到 AEM Publish 服務*)
* **config.publish.dev** (*套用到 AEM Dev Publish 服務*)
* **config.publish.rde** (*套用到 AEM RDE Publish 服務*)
* **config.publish.stage** (*套用到 AEM Staging Publish 服務*)
* **config.publish.prod** (*套用到 AEM Production Publish 服務*)
* **config.dev** (*套用到 AEM Dev 服務*)
* **config.rde** (*套用到 RDE 服務*)
* **config.stage** (*套用到 AEM Staging 服務*)
* **config.prod** (*套用到 AEM Production 服務*)

使用具有最相符執行模式的 OSGI 設定。

在本機開發時，執行模式啟動參數 `-r` 用於指定執行模式 OSGI 設定。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 原始檔控制系統中的維護任務設定。 {#maintenance-tasks-configuration-in-source-control}

維護任務設定必須保留在原始檔控制中，因為&#x200B;**工具 > 操作**&#x200B;畫面在雲端環境中不再可用。這樣做的好處是可以確保變更是有意保留的，而不是被動套用和被遺忘的。如需詳細資訊，請參閱AEM as a Cloud Service中的[維護工作](/help/operations/maintenance.md)。
