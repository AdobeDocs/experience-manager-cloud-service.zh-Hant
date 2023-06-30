---
title: 部署至 AEM as a Cloud Service
description: 部署至 AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 45%

---

# 部署至 AEM as a Cloud Service  {#deploying-to-aem-as-a-cloud-service}

## 簡介 {#introduction}

與 AEM On Premise 和 Managed Services 解決方案相比，AEM as a Cloud Service 的程式碼開發基礎相似。開發人員撰寫程式碼並在本機進行測試，然後推送到AEMas a Cloud Service上的遠端環境。 需要有 Cloud Manager，這是 Managed Services 的選用內容傳遞工具。此傳送工具現在是將程式碼部署到AEMas a Cloud Service開發、中繼和生產環境的唯一機制。 為了在部署前述環境之前快速驗證和偵錯功能，可將程式碼從本機環境同步至 [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md).

[AEM 版本](/help/implementing/deploying/aem-version-updates.md) 的更新始終是獨立於推送[自訂程式碼](#customer-releases) 的部署事件。換個角度來看，自訂程式碼發行版本應該根據生產環境中的AEM版本進行測試，因為這是部署在頂端的功能。 之後會經常發生AEM版本更新，且會自動套用。 它們旨在可回溯相容於已部署的客戶程式碼。

本檔案的其餘部分說明開發人員應如何調整其實務，以便他們同時使用AEMas a Cloud Service的版本更新和客戶更新。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客戶發行版本 {#customer-releases}

### 針對正確的 AEM 版本編寫程式碼 {#coding-against-the-right-aem-version}

對於以前的 AEM 解決方案，最新的 AEM 版本很少更改 (大約每年更換每季的 Service Pack)，客戶會根據自己的時間將生產執行個體更新到最新的快速啟動，參考 API Jar。不過，AEMas a Cloud Service上的應用程式會更頻繁地自動更新至最新版AEM，因此內部版本的自訂程式碼應根據最新AEM版本建置。

如同現有的非雲端AEM版本，系統支援以特定快速入門為基礎的本機、離線開發，且通常是除錯的首選工具。

>[!NOTE]
>應用程式在本機電腦的行為與在 Adobe Cloud 上的行為有細微差異。在本機開發過程中必須考慮這些架構差異，在雲端基礎結構上部署時可能會導致不同的行為。由於存在這些差異，因此在生產環境中推出新的自訂程式碼之前，務必要先在開發和測試環境中執行詳盡的測試。

若要開發內部版本的自訂程式碼，需使用內部版本的相關版本， [AEMAS A CLOUD SERVICESDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 應下載並安裝。 如需有關使用 AEM as a Cloud Service Dispatcher 工具的詳細資訊，請參閱[此頁面](/help/implementing/dispatcher/disp-overview.md)。

以下影片提供如何將程式碼部署到AEMas a Cloud Service的高階概觀：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 透過Cloud Manager和封裝管理員部署內容封裝 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 透過Cloud Manager部署 {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

客戶透過 Cloud Manager 將自訂程式碼部署到雲端環境。Cloud Manager會將本機組合的內容套件轉換為符合Sling功能模型的成品，這是在AEMas a Cloud Service上執行應用程式在雲端環境中的描述。 因此，在中檢視套件時 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在雲端環境中，名稱會包含「cp2fm」，而轉換後的套件會移除所有中繼資料。 它們無法互動，這表示它們無法下載、複製或開啟。轉換器的詳細文件位於[此處](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

為AEMas a Cloud Service上的應用程式編寫的內容套件必須在不可變和可變內容之間有乾淨的分離，並且Cloud Manager只會安裝可變內容，也會輸出如以下訊息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本節的其餘部分說明不可變和可變套件的構成和含義。

### 不可變內容套件 {#immutabe-content-packages}

永久存放在不可變存放庫的中的所有內容和程式碼都必須簽入 git 並透過 Cloud Manager 進行部署。換句話說，與目前 AEM 解決方案不同，程式碼永遠不會直接部署到執行中的 AEM 執行個體。此工作流程會確保在任何雲端環境中為指定版本執行的程式碼都相同，消除了生產環境中無意間變更程式碼的風險。 例如，OSGI設定應提交至原始檔控制，而不是在執行階段透過AEM Web主控台的Configuration Manager進行管理。

由於部署模式導致的應用程式變更是由交換器啟用的，除了服務使用者、其ACL、節點型別和索引定義變更之外，它們不能依賴可變儲存庫中的變更。

對於擁有現有程式碼庫的客戶，至關重要的是完成 AEM 文件描述的存放庫重組練習，以確保將以前位於 /etc 下的內容移動到正確的位置。

一些額外的限制適用於這些程式碼套件，例如不支援 [安裝 Hook](https://jackrabbit.apache.org/filevault/installhooks.html)。

## OSGI 設定 {#osgi-configuration}

如上所述，OSGI 設定應該提交給原始檔控制，而不是透過 Web 主控台。相關的技術包括：

* 使用 AEM Web 主控台的 Configuration Manager 對開發人員的本機 AEM 環境進行必要的變更，然後將結果匯出到本機檔案系統上的 AEM 專案。
* 手動在本機檔案系統的 AEM 專案中建立 OSGI 設定，為屬性名稱參考 AEM 主控台的 Configuration Manager。

在[為 AEM as a Cloud Service 設定 OSGi](/help/implementing/deploying/configuring-osgi.md) 閱讀有關 OSGI 設定的詳細資訊。

## 可變內容 {#mutable-content}

有時候，在原始檔控制中準備內容變更可能會有幫助，這樣Cloud Manager可以在環境更新時部署它。 例如，為某些根資料夾結構植入種子可能是合理的。 或者，排列可編輯範本中的變更，以啟用應用程式部署所更新的原則元件。

有兩種策略可說明Cloud Manager部署至可變存放庫的內容、可變內容套件和 `repoinit` 陳述式。

### 可變內容套件 {#mutable-content-packages}

資料夾路徑階層、服務使用者和存取控制 (ACL) 等內容通常會提交到 Maven 原型 AEM 專案中。技術包括從 AEM 匯出或直接寫成 XML。在建置和部署流程中，Cloud Manager 會封裝產生的可變內容套件。可變內容會在管道中的部署階段期間在三個不同的時間安裝：

在啟動新版本應用程式之前：

* 索引定義 (新增、修改、移除)

在啟動新版本應用程式期間但在切換之前：

* 服務使用者 (新增)
* 服務使用者 ACL (新增)
* 節點類型 (新增)

切換到新版本應用程式之後：

* 所有其他可透過Jackrabbit儲存庫定義的內容。 例如：
   * 資料夾 (新增、修改、移除)
   * 可編輯的範例 (新增、修改、移除)
   * 內容感知設定 (`/conf` 下的任何內容) (新增、修改、移除)
   * 指令碼 (可以在套件安裝流程的各個階段觸發安裝 Hook。另請參閱 [Jackrabbit filevault檔案](https://jackrabbit.apache.org/filevault/installhooks.html) 關於安裝鉤點。 AEM CS目前使用Filevault 3.4.0版，限制管理員使用者、系統使用者及管理員群組成員的安裝掛接)。

透過在 `/apps`下的 install.author 或 install.publish 資料夾中嵌入套件，可以將可變內容安裝限制在作者或發佈。在 AEM 6.5 中進行了重組以反映這種分離，有關建議的專案重組的詳細資料位在 [AEM 6.5 文件。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>內容套件部署到所有環境類型 (開發、預備、生產)。不可能將部署限制在特定環境中。此限制的目的是在確保可以選擇對自動執行進行測試執行。環境特定的內容需要透過以下方式手動安裝： [封裝管理員](/help/implementing/developing/tools/package-manager.md).

此外，在套用可變內容套件變更後，沒有任何機制可以回復這些變更。如果客戶偵測到問題，他們可以選擇在下一個程代碼版本中進行修復，或者採取最後手段，將整個系統還原到部署前的某個時間點。

任何包含的協力廠商套件都必須驗證為AEMas a Cloud Service相容，否則包含協力廠商套件會導致部署失敗。

如上所述，擁有現有程式碼庫的客戶應遵守6.5中所述存放庫變更所需的存放庫重組練習。 [AEM 6.5檔案。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## repoinit {#repoinit}

對於以下情況，最好採用在 OSGI 工廠設定中手動編寫明確內容建立 `repoinit` 陳述式的方法：

* 建立/刪除/停用服務使用者
* 建立/刪除群組
* 建立/刪除使用者
* 新增 ACL

  >[!NOTE]
  >
  >ACL 的定義要求已存在的節點結構。因此，前面必須要有建立路徑陳述式。

* 新增路徑 (例如根資料夾結構)
* 新增 CND (節點類型定義)

由於以下好處，repoinit 更適合這些受支援的內容修改使用案例：

* `Repoinit` 在啟動時會建立資源，因此邏輯可以視這些資源的存在是理所當然的。在可變內容套件方法中，資源是在啟動後建立的，因此依賴它們的應用程式的程式碼可能會失敗。
* `Repoinit` 是一個相對安全的指令集，因為您可以明確控制要進行的動作。此外，除了少數安全性相關案例外，僅支援額外操作，可移除使用者、服務使用者和群組。 相反地，在可變內容套件方法中移除某些內容是很明確的；當您定義篩選器時，篩選器覆蓋的任何內容都會被刪除。 儘管如此，仍應謹慎，因為對於任何內容，在某些情況下，新內容的存在可能會改變應用程式的行為。
* `Repoinit` 執行快速和不可部分完成作業。相反地，可變內容套件在效能上高度依賴於篩選器涵蓋的結構。即使您更新單一節點，也可能會建立大型樹狀的快照。
* 可以驗證 `repoinit` 陳述式，因為它們會在OSGi設定註冊時執行。
* `Repoinit` 陳述式為原子且明確，如果狀態已經相符，則會略過。

當 Cloud Manager 部署應用程式時，它會獨立於任何內容套件的安裝，執行這些陳述式。

建立 `repoinit` 語句，請遵循以下步驟：

1. 在專案的設定資料夾中為工廠 PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` 新增 OSGi 設定。為設定使用描述性名稱，例如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 新增 `repoinit` 陳述式至config的script屬性。 [Sling 文件](https://sling.apache.org/documentation/bundles/repository-initialization.html) 中記錄了語法和選項。在子資料夾之前，應該先明確建立父資料夾。 例如，在 `/content/myfolder` 之前明確建立 `/content`，再建立 `/content/myfolder/mysubfolder`。若是在低階結構上設定的ACL，建議將其設定在較高階層，並搭配使用 `rep:glob` 限制。 例如， `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. 在執行階段時於本機開發環境上進行驗證。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>針對底下節點定義的ACL `/apps` 或 `/libs` 此 `repoinit`，會在空白存放庫上開始執行。 套件會在以下之後安裝： `repoinit` 因此，陳述式不能依賴套件中定義的任何內容，但必須定義前置條件，如底下的父結構。

>[!TIP]
>
>對於ACL，建立深層結構可能會很麻煩。 因此，更合理的做法是在較高層級定義ACL，並限制它應該透過以下方式執行的位置： `rep:glob` 限制。

更多關於的詳細資訊 `repoinit` 您可在以下網址找到： [Sling檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可變內容套件的套件管理員「一次性」 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="套件管理員 - 移轉可變內容套件"
>abstract="探索封裝管理員在使用案例中的使用情況，在這些案例中，內容套件的安裝應為「一次性」。此安裝包括將特定內容從生產環境匯入至預備環境以偵錯生產問題，將小型內容套件從內部部署環境轉移至 AEM 雲端環境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en" text="內容轉移工具"

在某些使用案例中，內容套件應做為「一次性」安裝。例如，將特定內容從生產環境匯入到中繼環境，以偵錯生產問題。 對於這些情況， [封裝管理員](/help/implementing/developing/tools/package-manager.md) 可用於AEMas a Cloud Service上的環境。

由於套件管理員是一個執行階段概念，不可能將內容或程式碼安裝到不可變存放庫中，因此這些內容套件應該只包含可變內容 (主要是 `/content` 或 `/conf`)。如果內容套件包含混合的內容（可變和不可變內容），則只會安裝可變內容。

>[!IMPORTANT]
>
>封裝管理程式使用者介面可能會傳回 **未定義** 如果套件安裝時間超過10分鐘，則會出現錯誤訊息。
>
>這次不是因為安裝發生錯誤，而是因為Cloud Service針對所有要求逾時。
>
>如果您看到此類錯誤，請不要重試安裝。安裝作業正在背景正確進行。如果您確實重新啟動安裝，則多個並行匯入程式可能會造成某些衝突。

透過Cloud Manager安裝的任何內容套件（可變和不可變）都會在AEM Package Manager的使用者介面中顯示為凍結狀態。 這些套件無法重新安裝、重新建立或甚至下載，而且以 **&quot;cp2fm&quot;** 字尾，表示其安裝是由Cloud Manager管理。

### 包含協力廠商套件 {#including-third-party}

客戶通常會包含來自協力廠商的預先建立套件，例如Adobe的翻譯合作夥伴等軟體廠商。 建議將這些套件託管在遠端存放庫中，並在 `pom.xml`中參考它們。此方法適用於公開存放庫及具有密碼保護的私人存放庫，如中所述 [受密碼保護的maven存放庫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

如果無法將套件儲存在遠端存放庫中，客戶可以將套件放在以檔案系統為基礎的本機Maven存放庫中，該存放庫會作為專案的一部分提交給SCM。 相依的任何專案都會參考它。 存放庫會在專案pom中宣告，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方套件都必須遵守本文所述的AEMas a Cloud Service編碼和封裝指導方針，否則包含它會導致部署失敗。

以下Maven `POM.xml` 程式碼片段顯示如何將協力廠商套件內嵌在專案的「容器」套件中，通常名為 **&#39;all&#39;**，方式為 **filevault-package-maven-plugin** Maven外掛程式設定。

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

和AEM更新一樣，客戶版本是使用滾動部署策略來部署，以便在適當的情況下消除作者叢集停機時間。 事件的一般序列如下所述，其中新舊版本客戶代碼的節點正在執行相同版本的 AEM 程式碼。

* 舊版本的節點處於使用中狀態，且新版本的候選發佈版本已建置並可供使用。
* 如果有任何新的或更新的索引定義，即會處理對應的索引。舊版本的節點一律使用舊索引，而新版本的節點一律使用新索引。
* 具有新版本的節點啟動，而舊版本仍會提供流量。
* 具有舊版本的節點正在執行並保持服務，而具有新版本的節點會透過健康狀態檢查來檢查是否整備。
* 具有新版本的節點已就緒、接受流量，然後以已停止使用的舊版本取代節點。
* 舊版本的節點會隨著時間被新版本的節點取代，直到只剩下新版本的節點，如此即完成部署。
* 接著即會部署任何新的或修改的可變內容.

## 索引 {#indexes}

新版本或修改過的索引會在新版本開始傳輸流量之前，造成額外的索引或重新索引步驟。 有關 AEM as a Cloud Service 中索引管理的詳細資訊，請參閱[這篇文章](/help/operations/indexing.md)。您可以在Cloud Manager上檢查組建頁面的索引狀態，並在新版本準備好接收流量時收到通知。

>[!NOTE]
>
>滾動式部署所需的時間視索引大小而定。 原因是因為新版本在產生新索引之前無法接受流量。

目前，AEMas a Cloud Service無法搭配索引管理工具使用，例如ACS Commons Secure Oak Index工具。

## 複製 {#replication}

發佈機制向後相容於 [AEM復寫Java™ API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html).

若要使用雲端就緒AEM快速入門開發和測試復寫，經典復寫功能必須搭配製作/發佈設定使用。 如果為雲端移除了AEM Author上的使用者介面進入點，使用者將前往 `http://localhost:4502/etc/replication` 進行設定。

## 回溯相容程式碼以進行滾動部署 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM as a Cloud Service 的滾動部署策略表示新舊版本可能同時執行。因此，請注意程式碼變更是否無法回溯相容於仍在運作的舊版 AEM。

此外，如果有倒回，則應測試舊版本與新版本套用的任何新可變內容結構的相容性，因為可變內容並未移除。

### 服務使用者和 ACL 變更 {#service-users-and-acl-changes}

變更服務使用者（或存取內容或程式碼的ACL）可能會導致舊版AEM發生錯誤，導致使用過時的服務使用者存取該內容或程式碼。 若要解決此行為，建議將變更分散到至少兩個版本，在後續版本中清理之前，第一個版本會作為連結。

### 索引變更 {#index-changes}

如果變更了索引，需確保新版本在終止前持續使用其索引，同時舊版本則使用自己的已修改索引集。開發人員應遵循[本篇文章](/help/operations/indexing.md)中描述的索引管理技術。

### 針對回復作業的保守編碼 {#conservative-coding-for-rollbacks}

如果在部署後報告或偵測到失敗，則可能需要復原到舊版本。 確保新程式碼與該新版本建立的任何新結構相容，因為新結構（任何可變內容）不會回覆。 如果舊程式碼不相容，必須在後續客戶版本中套用修正。

## 快速開發環境 (RED) {#rde}

[快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) （簡稱RDE）可讓開發人員快速部署及檢閱變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

與透過Cloud Manager管道部署計畫碼的常規開發環境不同，開發人員使用命令列工具將計畫碼從本機開發環境同步到RDE。 在RDE中成功測試變更後，透過Cloud Manager管道將它們部署到常規的雲端開發環境，這會使計畫碼通過適當的品質閘道。

## 執行模式 {#runmodes}

在現有的 AEM 解決方案中，客戶可以選擇以任意執行模式來使執行個體運作，並在這些特定執行個體套用 OSGI 設定或安裝 OSGI 套裝。定義的執行模式通常包括&#x200B;*服務* (作者和發佈) 與環境 (快速開發環境、開發、預備、生產)。

另一方面，AEM as a Cloud Service 對於哪些執行模式可用，以及如何將 OSGI 套裝和 OSGI 設定對應到它們更有自己的做法：

* OSGI設定執行模式必須參考環境的RDE、開發、暫存、生產或服務的作者、發佈。 組合 `<service>.<environment_type>` 受支援，但這些環境必須以特定順序使用(例如 `author.dev` 或 `publish.prod`)。 應直接從程式碼參照OSGI權杖，而非使用 `getRunModes` 方法，不再包含 `environment_type` 在執行階段。 如需詳細資訊，請參閱[為 AEM as a Cloud Service 設定 OSGi](/help/implementing/deploying/configuring-osgi.md)。
* OSGI 套裝執行模式限制在服務 (作者、發佈)。預執行模式 OSGI 套裝應安裝在 `install.author` 或 `install.publish` 下的內容套件中。

AEM as a Cloud Service 不允許使用執行模式為特定環境或服務安裝內容。如果開發環境必須內建不在中繼或生產環境中的資料或HTML，可以使用Package Manager。

支援的執行模式設定包括：

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

會使用最符合執行模式的OSGI設定。

在本機開發時，執行模式啟動引數 `-r`，用於指定執行模式OSGI設定。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 原始檔控制系統中的維護任務設定。 {#maintenance-tasks-configuration-in-source-control}

維護任務設定必須保留在原始檔控制中，因為 **「工具」>「作業」** 熒幕在雲端環境中無法使用。 此優點可確保變更能有意持續存在，而非以反應式方式套用並遺忘。 另請參閱 [維護任務文章](/help/operations/maintenance.md) 以取得其他資訊。
