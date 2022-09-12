---
title: 準備階段
description: 了解您需要採取哪些步驟，才能確定您的AEM安裝已準備好移至雲端
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 6%

---

# 準備階段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="規劃您的轉變"
>abstract="在展開轉換至 Cloud Service 的過程前，您應該先熟悉 AEM as a Cloud Service、檢視針對其採取的重大變更，並檢視已遭取代或淘汰的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

在AEMas a Cloud Service移轉歷程的這個階段，您將熟悉AEMas a Cloud Service、檢閱其所推出的重大變更，並了解成功移轉至雲端所需的計畫。

## 迄今為止的故事 {#story-so-far}

上一份檔案， [開始移轉至AEMas a Cloud Service](/help/journey-migration/getting-started.md)，概述移轉至AEM as a Cloud Service所需執行的階段清單，以及移轉至Analytics的好處。

## 目標 {#objective}

本檔案可協助您了解您必須考慮哪些因素，才能確定您的AEM安裝已準備好移至雲端：

* 了解重大變更和已棄用的功能
* 了解如何規劃移轉至AEM的as a Cloud Service

## 檢閱AEMas a Cloud Service架構的重大變更 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service 提供許多管理 AEM 專案的新功能，並帶來許多可能性。

除了這些改善項目，AEM和Adobe Managed Services的內部部署安裝與AEMas a Cloud Service之間也有幾項差異。

下表中的項目清單是與移轉至AEM as a Cloud Service最相關的變更子集。 您可以查閱重要變更的完整清單 [此處](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>變更為何？</th>
    <th>引用</th>
    <th>主要優點</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>將可變和不可變篩選器分隔到相應的包中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEMas a Cloud Service重大變更</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM專案結構(AEMas a Cloud Service)</a></td>
    <td>可部署至AEMas a Cloud Service的單一套件可以有子套件，主要包含分隔至其專屬套件中的可變和不可變內容。</td>
  </tr>
  <tr>
    <td>存放庫初始化</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit檔案</a></td>
    <td>重新指向指令碼是建立任何初始節點結構、用戶、組或服務用戶的最佳做法。 由於這些指令碼可以通過運行模式進行定位，也可通過代碼包部署進行管理，因此它們提供了實現儲存庫初始化任務的極大靈活性。</td>
  </tr>
  <tr>
    <td>不允許自訂執行模式</td>
    <td></td>
    <td>僅支援隨AEMas a Cloud Service提供的現成執行模式。<br>新增其他開發環境時，所有環境都會系結至「開發」執行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道執行是部署的唯一方式</td>
    <td></td>
    <td>在AEMas a Cloud Service中，不允許存取/system/console，因此所有OSGi設定都必須是程式碼的一部分，且應以程式碼的形式部署。<br>OSGi設定以唯讀模式提供，可透過Cloud Manager的開發人員控制台檢視</td>
  </tr>
  <tr>
    <td>復寫代理由Sling Content Distribution取代</td>
    <td></td>
    <td>復寫代理的概念會由「使用內容發佈」取代。 如果有使用復寫代理的自訂項目，則必須重新設計。<br>不支援反向複製</td>
  </tr>
  <tr>
    <td>CRX/DE和套件管理器</td>
    <td></td>
    <td>CRX/DE僅可在開發環境中使用。<br>套件管理器可在所有製作執行個體上存取，但即將部署的套件必須僅包含可變內容(例如：/content或/conf)</td>
  </tr>
  <tr>
    <td>內建CDN並取得您自己的CDN</td>
    <td></td>
    <td>AEM as a Cloud Service包含適用於所有環境的CDN，這些環境已針對大部分使用案例進行最佳化。<br>如果您想要設定自己的CDN，必須向Adobe支援提交要核准的請求。<br>如果核准，CDN會以「快速」指向，而非任何環境中的AEM例項。</td>
  </tr>
  <tr>
    <td>長時間運行的作業</td>
    <td></td>
    <td>避免執行長時間執行的作業，例如Sling排程器或Cron作業，因為容器中執行的AEM例項隨時都可能來回執行。<br>重新思考這些功能，將其卸載至Adobe I/O。</td>
  </tr>
  <tr>
    <td>切換到非同步操作</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">配置非同步操作</a></td>
    <td>為了改善環境的整體效能，某些操作會以非同步模式執行。 當系統資源可用時，非同步作業將會排入佇列並執行。</td>
  </tr>
  <tr>
    <td>代號式驗證和整合策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">產生伺服器端API的存取權杖</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Token式驗證教學課程</a></td>
    <td>AEM外部系統通常會嘗試在AEM內執行HTTP作業。<br>建議的方法是實作此處概述的策略，而非依賴在AEM中使用密碼建立本機使用者名稱。</td>
  </tr>
  <tr>
    <td>檔案IO/磁碟使用</td>
    <td></td>
    <td>由於無法保證分配了多少磁碟空間以及容器中的實例進出，因此不建議使用檔案I/O操作來寫入或讀取連接到AEM實例的磁碟。</td>
  </tr>
  <tr>
    <td>DAM更新資產工作流程</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">asset compute服務</a></td>
    <td>屬於DAM更新資產工作流程的媒體處理步驟現在會由Asset compute服務取代</td>
  </tr>
  <tr>
    <td>AEM as a Cloud Service中的資產上傳方法和支援的工作流程處理步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">上傳API比較和支援的WF處理步驟</a></td>
    <td>在AEMas a Cloud Service中，在上傳或下載資產期間，資產會直接流入或流出二進位儲存。</br>AEMaaCS並非支援所有工作流程處理步驟。</td>
  </tr>
  <tr>
    <td>工作流程啟動器</td>
    <td></td>
    <td>從您的程式碼中移除任何觸發OOTB或自訂DAM更新資產工作流程的工作流程啟動器。</br>上傳至AEMas a Cloud Service的所有資產將由資產處理服務處理。 有關自定義步驟，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 後置處理工作流程</a> 關於如何設定和設定後置處理工作流程。</td>
  </tr>
  <tr>
    <td>自訂轉譯步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">處理設定檔</a></td>
    <td>任何自訂轉譯產生、影像轉換或視訊編碼都必須透過建立對應的處理設定檔，將卸載至資產處理服務。</td>
  </tr>
  <tr>
    <td>內容搜尋與索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">內容搜尋和索引變更</a></td>
    <td>索引的基礎處理以及它何時開始運作都發生了很大變化。<br>在您要部署的程式碼中管理Oak索引之前，請先完全了解並重新調整索引。</td>
  </tr>
  <tr>
    <td>並非所有維護任務都可配置</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Service維護任務</a></td>
    <td>您只能使用AEM as a Cloud Service來設定特定維護任務。</td>
  </tr>
  <tr>
    <td>對發佈儲存庫的更改</td>
    <td></td>
    <td>除了/home下的變更外，禁止直接變更發佈用存放庫。 建議一律對作者進行變更並加以分發。 所有程式碼和設定變更都必須透過對應的Cloud Manager管道部署。</td>
  </tr>
  <tr>
    <td>Dispatcher設定和快取</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">雲端中的Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">快取管理<br></td>
    <td>Dispatcher設定必須遵循特定結構。<br>配置必須作為程式碼的一部分進行管理，並透過Cloud Manager管道部署。</td>
  </tr>
  <tr>
    <td>備份和還原</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Service備份和恢復</a></td>
    <td></td>
  </tr>
  <tr>
    <td>驗證的變更</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en">AEM as a Cloud Service 的 IMS 支援</td>
    <td>如果您先前在移至Cloud Service前同時在製作和發佈上使用SAML 2.0整合，主要變更是AEMas a Cloud Service製作僅與Adobe IMS整合。 不過，AEMas a Cloud Service發佈層級仍可運用SAML或其他驗證整合。 AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。IMS驗證不支援客戶網站的外部使用者，例如網站訪客。</td>
  </tr>
</tbody>
</table>

## 過時的功能 {#deprecated-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

建議您參閱 [過時的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) 請熟悉「Experience Manageras a Cloud Service」中標示為過時的功能，並了解對AEM部署有何影響。

## 計畫審核AEM安裝 {#review-planning}

在您習慣了AEM as a Cloud Service所推出的變更後，您就可以開始針對現有安裝進行規劃以評估所需的變更等級，以便將其移至雲端。

下圖將展示審核階段中涉及的關鍵步驟：

![影像](/help/journey-migration/assets/planning-phaseimg1.png)

接下來，我們將詳細探討這些步驟的意義。

### 評定雲端服務整備 {#assess-cloud-readiness}

第一步是評估您是否已準備好從現有的AEM版本移至Cloud Service，並判斷需要重構以便與AEMas a Cloud Service相容的區域。

您需要針對重大變更和已棄用的功能，對目前的AEM原始碼進行全面評估，以判斷轉換歷程中預期的投入程度。

調查結果的數量將直接影響時間表和項目總體成功。 因此，建議您盡可能發現要規劃傳送內容，或開始必要的對話，以重新設計任何必要的自訂內容，以符合AEMas a Cloud Service最佳實務。

**Best Practice Analyzer**

您可以針對當前的AEM版本運行Best Practices Analyzer來加快評估。 了解其工作方式對於加快評估規劃至關重要。

您可以諮詢 [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 檔案。

**建立雲準備情況評估報表**

下一步是根據迄今獲得的所有知識建立報告。 您可以從Stage和Production例項產生Best Practices Analyzer報表，以執行此作業。 [然後將其上傳至Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) ，以取得可操作的項目的可數字報表。

一般報表應包含下列輸入：

* 詳細說明特定AEM安裝功能集的檔案
* AEM自訂設定和程式碼的詳細資訊
* 生產Dispatcher設定
* CDN設定（如果有的話）

**將報表社會化**

完成Best Practices Analyzer報表後，請與相關團隊共用這些報表，以確認您的發現並規劃後續步驟。 您也可以根據偏好，使用 [打印預覽](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### 檢視資源規劃 {#review-resource-planning}

一旦您估計了移至Cloud Service所需的工作量，您就應該確定資源、建立團隊，以及為轉換過程分配角色和責任。

### 建立 KPI {#establish-kpis}

如果您先前尚未建立關鍵績效指標(KPI)，建議您為AEM實作建立KPI，以協助您的團隊專注於最重要的事項。

請參閱 [開發KPI](https://guided.adobe.com/welcome/aem/part6.html) 了解如何為您的業務目標選擇正確的KPI。

## 下一步 {#what-is-next}

了解移轉至AEMas a Cloud Service所需變更的範圍後，您就可以開始 [讓您的程式碼和內容雲端準備就緒](/help/journey-migration/implementation.md) 執行移轉之前。

## 其他資源 {#additional-resources}

* [Cloud Acceleration Manager快速入門](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)  — 使用Cloud Acceleration Manager加快雲端移動的完整指南
* [AEMas a Cloud Service:引言、架構和思維方式不同](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEMCloud Service首頁](/help/overview/home.md)  — 如需Experience Manageras a Cloud Service檔案的概觀，請從這裡開始。
* [AEMas a Cloud Service概述](/help/overview/home.md)  — 本指南提供Experience Manager as a Cloud Service的概觀，包括簡介、術語和架構。
* [入門歷程](/help/journey-onboarding/overview.md) — 本指南提供如何開始使用Experience Manageras a Cloud Service的摘要，包括如何取得存取權並設定您的團隊
