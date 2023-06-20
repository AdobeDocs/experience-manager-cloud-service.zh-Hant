---
title: 整備階段
description: 瞭解您需要採取的步驟，以便確保AEM安裝已準備好移至雲端
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 8%

---

# 整備階段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="規劃您的轉換"
>abstract="在展開轉換至 Cloud Service 的過程前，您應該先熟悉 AEM as a Cloud Service、檢視針對其採取的重大變更，並檢視已遭取代或淘汰的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="最佳做法分析工具"

在AEMas a Cloud Service移轉歷程的這個階段，您將熟悉AEMas a Cloud Service、檢閱它引進的重大變更，並瞭解成功移轉至雲端所需的規劃。

## 到目前為止 {#story-so-far}

上一份檔案， [開始使用AEMas a Cloud Service](/help/journey-migration/getting-started.md)，概述您可以移轉至AEMas a Cloud Service所需的階段清單，以及移轉的好處。

## 目標 {#objective}

本檔案可協助您瞭解必須考量的因素，以便確定AEM安裝已準備好移至雲端：

* 瞭解重大變更和已棄用的功能
* 瞭解如何規劃移轉至AEMas a Cloud Service

## 檢閱AEMas a Cloud Service架構的重大變更 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service 提供許多管理 AEM 專案的新功能，並帶來許多可能性。

除了這些改善專案，內部部署安裝的AEM和Adobe Managed Services與AEMas a Cloud Service之間也有所差異。

下表中的專案清單是與移轉至AEMas a Cloud Service最相關的變更的子集。 您可以查閱重大變更的完整清單 [此處](/help/release-notes/aem-cloud-changes.md).

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
    <td>將可變和不可變篩選器分隔成對應的套件</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEMas a Cloud Service重大變更</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEMas a Cloud Service的AEM專案結構</a></td>
    <td>可部署到AEMas a Cloud Service的單一套件可以具有子套件，主要用於包含分隔到其自身套件中的可變和不可變內容。</td>
  </tr>
  <tr>
    <td>Repo Init</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit檔案</a></td>
    <td>Repoinit指令碼是建立任何初始節點結構、使用者、群組或服務使用者的最佳實務。 由於這些指令碼可透過執行模式鎖定目標，並可透過程式碼套件部署加以管理，因此可提供很大的彈性來完成存放庫初始化任務。</td>
  </tr>
  <tr>
    <td>不允許自訂執行模式</td>
    <td></td>
    <td>僅支援隨AEMas a Cloud Service提供的現成執行模式。<br>新增其他開發環境時，所有環境都會連結至「開發」執行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道執行是部署的唯一方法</td>
    <td></td>
    <td>在AEMas a Cloud Service中，不允許存取/system/console，因此所有OSGi設定都必須是程式碼的一部分，並應部署為程式碼。<br>OSGi設定以唯讀模式提供，以便透過Cloud Manager透過開發人員控制檯檢視</td>
  </tr>
  <tr>
    <td>復寫代理程式已由Sling Content Distribution取代</td>
    <td></td>
    <td>Sing Content Distribution已取代復寫代理程式的概念。 如果有利用復寫代理的自訂專案，則必須重新設計。<br>不支援反向復寫</td>
  </tr>
  <tr>
    <td>CRX/DE和封裝管理員</td>
    <td></td>
    <td>CRX/DE僅允許在開發環境中使用。<br>封裝管理員可在所有編寫執行個體上存取，但即將部署的封裝必須僅包含可變內容（例如： /content或/conf）</td>
  </tr>
  <tr>
    <td>內建CDN並取得您自己的CDN</td>
    <td></td>
    <td>AEMas a Cloud Service包含適用於所有環境的CDN，此環境已針對大多數使用案例最佳化。<br>如果您想要設定自己的CDN，您必須向Adobe支援提交請求才能獲得核准。<br>如果獲得核准，CDN將指向Fastly，而不是任何環境中的AEM執行個體。</td>
  </tr>
  <tr>
    <td>長時間執行的工作</td>
    <td></td>
    <td>避免執行長時間執行的工作，例如Sling排程器或Cron工作，因為在容器中執行的AEM執行個體隨時可能來來去去。<br>重新思考這些功能，將其解除安裝至Adobe I/O。</td>
  </tr>
  <tr>
    <td>切換至非同步作業</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">設定非同步操作</a></td>
    <td>為了改善環境的整體效能，某些作業會以非同步模式執行。 當系統資源可用時，非同步工作會排入佇列並執行。</td>
  </tr>
  <tr>
    <td>權杖型驗證和整合策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">為伺服器端API產生存取權杖</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">權杖型驗證教學課程</a></td>
    <td>AEM外部的系統通常會嘗試在AEM內執行HTTP作業。<br>建議的方法是實施這裡概述的策略，而不是依賴在AEM中使用密碼建立本機使用者名稱。</td>
  </tr>
  <tr>
    <td>檔案IO/磁碟使用量</td>
    <td></td>
    <td>由於無法保證分配了多少磁碟空間，而且容器中的執行個體會來來去去，因此不建議使用檔案I/O操作從附加至AEM執行個體的磁碟中寫入或讀取。</td>
  </tr>
  <tr>
    <td>DAM更新資產工作流程</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">asset compute服務</a></td>
    <td>屬於DAM更新資產工作流程一部分的媒體處理步驟現在由Asset compute服務取代</td>
  </tr>
  <tr>
    <td>AEMas a Cloud Service的資產上傳方法和支援的工作流程步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">上傳API比較和支援的WF程式步驟</a></td>
    <td>在AEMas a Cloud Service中，在上傳或下載資產期間，資產會直接流入或流出二進位儲存體。</br>AEMaaCS並不支援所有工作流程處理步驟。</td>
  </tr>
  <tr>
    <td>工作流程啟動器</td>
    <td></td>
    <td>從您的程式碼中移除任何觸發OOTB或自訂DAM更新資產工作流程的工作流程啟動器。</br>所有上傳至AEMas a Cloud Service的資產都將由資產處理服務處理。 如需自訂步驟，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 後處理工作流程</a> 如何設定和設定後處理工作流程。</td>
  </tr>
  <tr>
    <td>自訂轉譯步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">處理設定檔</a></td>
    <td>任何自訂轉譯產生、影像轉換或視訊編碼都必須建立對應的處理設定檔，將之解除安裝至資產處理服務。</td>
  </tr>
  <tr>
    <td>內容搜尋與索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">內容搜尋和索引變更</a></td>
    <td>索引的基礎處理及其開始運作時，會有相當多的變更。<br>在您將部署的程式碼中管理Oak索引之前，請完全瞭解並重新調整Oak索引。</td>
  </tr>
  <tr>
    <td>並非所有維護任務都是可設定的</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Service維護任務</a></td>
    <td>您只能使用AEMas a Cloud Service設定某些維護任務。</td>
  </tr>
  <tr>
    <td>發佈存放庫的變更</td>
    <td></td>
    <td>不允許直接變更發佈用儲存庫，但/home底下的儲存庫除外。 一律建議對作者進行變更並加以發佈。 所有程式碼和設定變更都必須透過對應的Cloud Manager管道部署。</td>
  </tr>
  <tr>
    <td>Dispatcher設定和快取</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">雲端中的Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">快取管理<br></td>
    <td>Dispatcher設定必須遵循特定結構。<br>這些設定必須作為計畫碼的一部分進行管理，並透過Cloud Manager管道進行部署。</td>
  </tr>
  <tr>
    <td>備份和還原</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Service備份與還原</a></td>
    <td></td>
  </tr>
  <tr>
    <td>驗證變更</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant">AEM as a Cloud Service 的 IMS 支援</td>
    <td>如果您先前在移至Cloud Service之前在作者和發佈上使用SAML 2.0整合，主要變更為AEMas a Cloud Service作者僅與Adobe IMS整合。 不過，AEMas a Cloud Service發佈層級仍可使用SAML或其他驗證整合。 AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。IMS驗證不支援客戶網站的外部一般使用者，例如網站訪客。</td>
  </tr>
</tbody>
</table>

## 過時的功能 {#deprecated-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

建議您參閱 [已棄用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) 熟悉Experience Manageras a Cloud Service中標示為過時的功能，並瞭解對您的AEM部署有何影響。

## 規劃檢閱AEM安裝 {#review-planning}

在您習慣了AEMas a Cloud Service的變更後，現在應該開始規劃檢閱現有的安裝。 這麼做可協助您評估將它移至雲端所需的變更等級。

下圖將展示稽核階段中涉及的關鍵步驟：

![影像](/help/journey-migration/assets/planning-phaseimg1.png)

接下來，我們將詳細探索這些步驟的意義。

### 評定雲端服務整備 {#assess-cloud-readiness}

第一步是評估您是否已整備完畢，可從現有的AEM版本移至Cloud Service，並判斷需要重構才能與AEMas a Cloud Service相容的區域。

您必須根據重大變更和過時的功能，對目前的AEM原始程式碼進行全面的評估，以判斷轉換歷程中預期的投入程度。

發現專案的數量將直接影響時間表及整體專案的成功。 因此，建議您儘可能發掘內容，以規劃傳遞作業，或開始重新設計任何符合AEMas a Cloud Service最佳實務要求的自訂作業所需的對話。

**Best Practice Analyzer**

您可以針對您目前的AEM版本執行Best Practices Analyzer，以加速評估。 瞭解其運作方式，是加快評估計畫的關鍵。

您可以參閱 [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 說明檔案。

**建立雲端整備評估報告**

下一個步驟是根據目前取得的所有知識建立報告。 您可以從「階段」和「生產」執行個體產生Best Practices Analyzer報告來完成此操作。 [然後將其上傳到Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 以取得可操作專案的可消化報告。

一般報表應包含下列輸入：

* 詳細說明特定AEM安裝功能組的檔案
* AEM自訂設定和程式碼的詳細資訊
* 生產Dispatcher設定
* CDN設定（如果有的話）

**使報表社會化**

Best Practices Analyzer報表完成之後，請與相關團隊共用這些報表，以便您可以確認結果並規劃後續步驟。 您也可以使用來分配報表的列印版本（視偏好設定而定） [列印預覽](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### 檢視資源規劃 {#review-resource-planning}

一旦估計好移至Cloud Service所需的投入程度，您就應該確定資源、建立專案團隊，並規劃轉換流程的角色和責任。

### 建立 KPI {#establish-kpis}

如果您先前尚未建立關鍵績效指標(KPI)，建議您為AEM實作建立KPI，以協助您的團隊專注於最重要的事項。

另請參閱 [開發KPI](https://guided.adobe.com/welcome/aem/part6.html) 以瞭解如何為您的業務目標選擇正確的KPI。

## 下一步 {#what-is-next}

瞭解了移至AEMas a Cloud Service所需的變更範圍後，您就可以開始進行 [讓您的程式碼和內容雲端準備就緒](/help/journey-migration/implementation.md) 實際執行移轉之前。

## 其他資源 {#additional-resources}

* [Cloud Acceleration Manager快速入門](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)  — 有關如何使用Cloud Acceleration Manager以加速您向雲端移動的完整指南
* [AEMas a Cloud Service：簡介、架構和思維方式不同](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM aCloud Service首頁](/help/overview/home.md)  — 如需Experience Manageras a Cloud Service檔案的概覽，請從這裡開始。
* [AEMas a Cloud Service概述](/help/overview/home.md)  — 本指南提供Experience Manageras a Cloud Service概觀，包括簡介、術語和架構。
* [入門歷程](/help/journey-onboarding/overview.md) — 本指南提供如何開始使用Experience Manageras a Cloud Service的摘要，包括如何取得存取權和設定團隊
