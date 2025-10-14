---
title: 整備階段
description: 瞭解您必須執行的步驟，以便確定AEM安裝已準備好移至雲端。
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
feature: Migration
role: Admin
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 5%

---

# 整備階段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="規劃您的轉變"
>abstract="在開始轉變至 Cloud Service 的歷程之前，請先熟悉 AEM as a Cloud Service。查看其重大變更以及被取代或棄用的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hant" text="最佳做法分析工具"

在AEM as a Cloud Service移轉歷程的這個階段，您可以熟悉AEM as a Cloud Service。 您可以檢閱引進的重大變更，並瞭解規劃成功移轉至雲端所需的條件。

## 目前進度 {#story-so-far}

上一份檔案[開始使用AEM as a Cloud Service](/help/journey-migration/getting-started.md)概述了您必須經歷的階段清單，以便移轉至AEM as a Cloud Service。 它也概述進行移轉的好處。

## 目標 {#objective}

本檔案可協助您瞭解必須考量哪些因素，以便確定AEM安裝已準備好移至雲端：

* 瞭解重大變更和已棄用的功能
* 瞭解如何規劃移轉至AEM as a Cloud Service

## 檢閱AEM as a Cloud Service架構的重大變更 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service提供許多管理AEM專案的新功能，並帶來許多可能性。

隨著這些改善，與AEM as a Cloud Service相比，AEM的內部部署安裝和Adobe Managed Services之間也引進了幾項差異。

下表中的專案清單是與移轉至AEM as a Cloud Service最相關的變更子集。 您可以參閱Adobe Experience Manager as a Cloud Service[&#128279;](/help/release-notes/aem-cloud-changes.md)的重大變更完整清單。

<table>
<thead>
  <tr>
    <th>變更內容？</th>
    <th>參考</th>
    <th>重要技巧</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>將可變和不可變篩選器分隔到對應的套件中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hant">AEM as a Cloud Service重大變更</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant#mutable-vs-immutable">AEM as a Cloud Service的AEM專案結構</a></td>
    <td>可部署到AEM as a Cloud Service的單一套件可以具有子套件，主要用於包含分隔到其自身套件中的可變和不可變內容。</td>
  </tr>
  <tr>
    <td>存放庫初始</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit檔案</a></td>
    <td>Repoinit指令碼是建立任何初始節點結構、使用者、群組或服務使用者的最佳作法。 由於這些指令碼可以透過執行模式鎖定目標，並可透過程式碼套件部署加以管理，因此在實現存放庫初始化任務時可提供很大彈性。</td>
  </tr>
  <tr>
    <td>不允許自訂執行模式</td>
    <td></td>
    <td>僅支援隨AEM as a Cloud Service一起提供的現成執行模式。<br>新增其他開發環境時，所有環境都會繫結至「開發」執行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道執行是部署的唯一方法</td>
    <td></td>
    <td>在AEM as a Cloud Service中，不允許存取/system/console，因此所有OSGi設定都必須是程式碼的一部分，並應部署為程式碼。<br>OSGi設定以唯讀模式提供，可透過Cloud Manager透過Developer Console檢視</td>
  </tr>
  <tr>
    <td>復寫代理程式已由Sling Content Distribution取代</td>
    <td></td>
    <td>Sing Content Distribution已取代復寫代理程式的概念。 如果有使用復寫代理程式的自訂，則必須重新設計。<br>不支援反向復寫</td>
  </tr>
  <tr>
    <td>CRX/DE和封裝管理員</td>
    <td></td>
    <td>CRX/DE僅允許在開發環境中使用。<br>封裝管理員可在所有編寫執行個體上存取，但即將部署的封裝必須僅包含可變內容（例如： /content或/conf）</td>
  </tr>
  <tr>
    <td>內建CDN並取得您自己的CDN</td>
    <td></td>
    <td>AEM as a Cloud Service包含適用於所有環境的CDN，此環境已針對大部分使用案例最佳化。<br>如果您想要設定自己的CDN，必須向Adobe支援提交要求才能獲得核准。<br>如果獲得核准，CDN會指向Fastly，而不是任何環境中的AEM執行個體。</td>
  </tr>
  <tr>
    <td>長時間執行的工作</td>
    <td></td>
    <td>避免長時間執行工作，例如Sling排程器或Cron工作，因為容器中執行的AEM執行個體隨時可以來回執行。<br>重新思考這些功能，以便將其解除安裝至Adobe Developer。</td>
  </tr>
  <tr>
    <td>切換至非同步作業</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html?lang=zh-Hant#configuring-asynchronous-msm-operations">設定非同步操作</a></td>
    <td>為了改善環境的整體效能，某些作業會以非同步模式執行。 當系統資源可用時，非同步工作會排入佇列並執行。</td>
  </tr>
  <tr>
    <td>權杖型驗證和整合策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=zh-Hant#the-server-to-server-flow">產生伺服器端API的存取權杖</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=zh-Hant#authentication">權杖型驗證教學課程</a></td>
    <td>AEM外部的系統通常會嘗試在AEM內執行HTTP作業。<br>建議的方法是實作這裡概述的策略，而不是依賴在AEM中使用密碼建立本機使用者名稱。</td>
  </tr>
  <tr>
    <td>檔案IO/磁碟使用量</td>
    <td></td>
    <td>無法保證會分配多少磁碟空間，而且容器中的執行個體會來回切換。 因此，不建議使用檔案I/O作業來寫入或讀取附加至AEM執行個體的磁碟。</td>
  </tr>
  <tr>
    <td>dam更新資產工作流程</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=zh-Hant">asset compute服務</a></td>
    <td>屬於DAM更新資產工作流程一部分的媒體處理步驟現在由Asset Compute服務取代</td>
  </tr>
  <tr>
    <td>AEM as a Cloud Service中的資產上傳方法和支援的工作流程步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html?lang=zh-Hant#post-processing-workflows-steps">上傳API比較和支援的WF流程步驟</a></td>
    <td>在AEM as a Cloud Service中，在上傳或下載資產期間，資產會直接流入或流出二進位儲存體。 <br>AEMaaCS不支援所有工作流程處理步驟。</td>
  </tr>
  <tr>
    <td>工作流程啟動器</td>
    <td></td>
    <td>從您的程式碼中移除所有觸發現成可用或自訂DAM更新資產工作流程的工作流程啟動器。 <br>所有上傳至AEM as a Cloud Service的資產將由資產處理服務處理。 如需自訂步驟，請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=zh-Hant#post-processing-workflows">後處理工作流程</a>，瞭解如何設定與設定後處理工作流程。</td>
  </tr>
  <tr>
    <td>自訂轉譯步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=zh-Hant">處理設定檔</a></td>
    <td>任何自訂轉譯產生、影像轉換或視訊編碼都必須透過建立對應的處理設定檔，將解除安裝至資產處理服務。</td>
  </tr>
  <tr>
    <td>內容搜尋與索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=zh-Hant">內容搜尋和索引變更</a></td>
    <td>索引的基礎處理及其開始執行的時間有相當大變化。<br>在您部署的程式碼中管理Oak索引之前，請完全瞭解並重新調整。</td>
  </tr>
  <tr>
    <td>並非所有維護任務都是可設定的</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html?lang=zh-Hant">AEM as a Cloud Service維護任務</a></td>
    <td>您只能使用AEM as a Cloud Service設定某些維護任務。</td>
  </tr>
  <tr>
    <td>Publish存放庫的變更</td>
    <td></td>
    <td>不允許直接變更Publish存放庫，除了/home底下的變更。 一律建議散佈對作者所做的任何變更。 所有程式碼和設定變更都必須透過對應的Cloud Manager管道進行部署。</td>
  </tr>
  <tr>
    <td>Dispatcher設定和快取</td>
    <td>雲端中的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=zh-Hant">Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html?lang=zh-Hant#other-content">快取管理<br></td>
    <td>Dispatcher設定必須遵循特定結構。<br>這些設定必須作為程式碼的一部分進行管理，並透過Cloud Manager管道進行部署。</td>
  </tr>
  <tr>
    <td>備份和還原</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=zh-Hant">AEM as a Cloud Service備份與還原</a></td>
    <td></td>
  </tr>
  <tr>
    <td>驗證變更</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant">AEM as a Cloud Service 的 IMS 支援</td>
    <td>如果您先前在移至Cloud Service之前在作者和發佈上使用SAML 2.0整合，主要變更為AEM as a Cloud Service Author僅與Adobe IMS整合。 不過，AEM as a Cloud Service Publish層級仍可使用SAML或其他驗證整合。 AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。IMS驗證不支援客戶網站的外部一般使用者，例如網站訪客。</td>
  </tr>
</tbody>
</table>

## 過時的功能 {#deprecated-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

Adobe建議您參閱[已棄用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=zh-Hant#deprecated-features)，以熟悉Experience Manageras a Cloud Service中標示為已棄用的功能。 瞭解對您的AEM部署有何影響。

## 計畫檢閱AEM安裝 {#review-planning}

在您習慣使用AEM as a Cloud Service引進的變更後，是時候開始規劃檢閱您現有的安裝了。 這麼做有助於您評估將它移至雲端所需的變更等級。

下圖將展示稽核階段中的關鍵步驟：

![稽核階段期間涉及的關鍵步驟](/help/journey-migration/assets/planning-phaseimg1.png)

接下來，您會詳細探索這些步驟的意義。

### 評估Cloud Service整備 {#assess-cloud-readiness}

第一步是評估您是否已整備完畢，可從現有的AEM版本移轉至Cloud Service，並判斷需要重構才能與AEM as a Cloud Service相容的區域。

根據重大變更和過時的功能，對您目前的AEM原始程式碼進行全面評估，以確定轉換歷程中預期的投入程度。

發現專案的數量會直接影響時間表與整體專案的成功。 因此，Adobe建議您儘可能多地發掘內容，以便規劃傳送。 或者，開始對話，以便您可以重新設計符合AEM as a Cloud Service最佳實務所需的任何自訂。

**最佳做法分析工具**

您可以針對目前的AEM版本執行Best Practices Analyzer，加速評估。 瞭解其運作方式，是加快評估規劃的關鍵所在。

您可以參閱[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)檔案來閱讀其運作方式。

**建立雲端整備評估報告**

下一步是根據目前所獲得的所有知識建立報告。 若要建立報告，請從中繼和生產執行個體產生Best Practices Analyzer報告，[然後將其上傳至Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam)，以取得可操作專案的可解譯報告。

一般報表應包含下列輸入：

* 詳細說明特定AEM安裝功能集的檔案
* AEM自訂設定和程式碼的詳細資料
* 生產Dispatcher設定
* 網域對應（CDN設定） （如果有的話）

**將報告社交化**

Best Practices Analyzer報表完成之後，請與相關團隊共用，以便您確認發現並規劃後續步驟。 您也可以使用[列印預覽](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam)，根據喜好來分配列印版的報告。

### 複查資源規劃 {#review-resource-planning}

一旦評估好移至Cloud Service所需的投入程度，您就應該確定資源、建立專案團隊，並規劃轉換流程的角色和責任。

### 建立KPI {#establish-kpis}

如果您先前尚未建立關鍵績效指標(KPI)，我們建議您為AEM實作建立KPI，協助您的團隊專注於最重要的事項。

請參閱[開發KPI](https://experienceleague.adobe.com/welcome/aem/part6.html?lang=zh-Hant)，以便瞭解如何為您的企業目標選擇正確的KPI。

## 後續步驟 {#what-is-next}

一旦您瞭解移轉至AEM as a Cloud Service所需的變更範圍，實際執行移轉之前，應該[讓您的程式碼和內容雲端就緒](/help/journey-migration/implementation.md)。

## 其他資源 {#additional-resources}

* [Cloud Acceleration Manager快速入門](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) — 有關如何使用Cloud Acceleration Manager以加速您移至雲端的完整指南。
* [AEM as a Cloud Service：簡介、架構和思考方式不同](https://experienceleague.adobe.com/zh-hant?launch=ExperienceManager-D-1-2021.1.migration&recommended=ExperienceManager-D-1-2021.1.migration&lang=en#dashboard/learning)
* [AEMCloud Service首頁](/help/overview/introduction.md) — 如需Experience Manageras a Cloud Service檔案的概覽，請由此開始。
* [AEM as a Cloud Service概觀](/help/overview/introduction.md) — 本指南提供Experience Manageras a Cloud Service概觀，包括簡介、術語和架構。
* [入門歷程](/help/journey-onboarding/overview.md) — 本指南提供如何開始使用Experience Manageras a Cloud Service的摘要，包括如何存取和設定您的團隊。
