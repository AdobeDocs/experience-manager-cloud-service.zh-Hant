---
title: 就緒階段
description: 瞭解您需要採取哪些步驟以確保AEM您的安裝已準備好移至雲
source-git-commit: 8988f184b7a2153ff32aa3bdc26283f9a7b414b8
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 5%

---

# 就緒階段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="規劃過渡"
>abstract="在展開轉換至 Cloud Service 的過程前，您應該先熟悉 AEM as a Cloud Service、檢視針對其採取的重大變更，並檢視已遭取代或淘汰的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="最佳做法分析器"

在as a Cloud Service遷移AEM之旅的這一階段，您將熟悉as a Cloud Service、回顧其引入的顯著變AEM化，並瞭解成功遷移到雲所需的計畫。

## 到目前為止的故事 {#story-so-far}

上一份檔案， [開始轉到AEMas a Cloud Service](/help/journey-migration/getting-started.md)，概述了遷移到as a Cloud Service所需要經歷的階AEM段的清單，以及遷移到所帶來的好處。

## 目標 {#objective}

本文檔可幫助您瞭解為確保安裝已準備好移AEM動到雲，必須考慮哪些因素：

* 瞭解顯著更改和不建議使用的功能
* 瞭解如何規劃遷移到AEMas a Cloud Service

## 回顧as a Cloud Service架構中的AEM顯著變化 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service 提供許多管理 AEM 專案的新功能，並帶來許多可能性。

除了這些改進外，在Adobe Managed Services和Adobe Managed Services的內部安裝AEM與as a Cloud Service之間引入了幾種AEM差異。

下表中的項清單是與遷移到AEMas a Cloud Service相關的更改的子集。 您可以查閱顯著更改的完整清單 [這裡](/help/release-notes/aem-cloud-changes.md)。

<table>
<thead>
  <tr>
    <th>有什麼變化？</th>
    <th>引用</th>
    <th>關鍵要點</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>將可變篩選器和不可變篩選器分離到相應的包中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEMas a Cloud Service顯著變化</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">用AEM於as a Cloud Service的項目結AEM構</a></td>
    <td>可部署到as a Cloud Service中的單個包可AEM以具有子包，主要用於包含可變和不可變內容，這些內容被分隔到它們自己的包中。</td>
  </tr>
  <tr>
    <td>回購初始化</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit文檔</a></td>
    <td>重新點擊指令碼是建立任何初始節點結構、用戶、組或服務用戶的最佳做法。 由於這些指令碼可以通過運行模式進行目標操作，並可通過代碼包部署進行管理，因此它們提供了實現儲存庫初始化任務的極大靈活性。</td>
  </tr>
  <tr>
    <td>不允許使用自定義運行模式</td>
    <td></td>
    <td>僅支援出廠時提供的帶AEM有as a Cloud Service的運行模式。<br>添加其他開發環境時，所有環境都與「開發」運行模式相關。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道執行是部署的唯一方法</td>
    <td></td>
    <td>在AEMas a Cloud Service中，不允許訪問/system/console，因此所有OSGi配置都必須是代碼的一部分，並應作為代碼部署。<br>OSGi配置以只讀模式提供，可通過雲管理器通過開發人員控制台查看</td>
  </tr>
  <tr>
    <td>複製代理被Sling內容分發替換</td>
    <td></td>
    <td>複製代理的概念被Sing內容分發取代。 如果有利用複製代理的自定義項，則必須重新設計這些自定義項。<br>不支援反向複製</td>
  </tr>
  <tr>
    <td>CRX/DE和包管理器</td>
    <td></td>
    <td>CRX/DE僅允許在開發環境中使用。<br>包管理器可在所有作者實例上訪問，但要部署的包必須只包含可變內容(例如：/content或/conf</td>
  </tr>
  <tr>
    <td>內置CDN並獲取您自己的CDN</td>
    <td></td>
    <td>AEMas a Cloud Service包括針對大多數使用案例優化的所有環境的CDN。<br>如果要設定自己的CDN，則必須將請求提交給Adobe支援，以便獲得批准。<br>如果CDN被批准，則CDN將指向Rebisty，而不指向任何AEM環境中的實例。</td>
  </tr>
  <tr>
    <td>長時間運行的作業</td>
    <td></td>
    <td>避免執行長時間運行的作業（如Sling調度程式或Cron作業）,AEM因為在容器中執行的實例可以在任何時間點來來去。<br>重新思考這些功能，將它們卸載到Adobe I/O。</td>
  </tr>
  <tr>
    <td>切換到非同步操作</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">配置非同步操作</a></td>
    <td>為了提高環境的整體效能，某些操作會以非同步模式執行。 當系統資源可用時，非同步作業將排隊並執行。</td>
  </tr>
  <tr>
    <td>基於令牌的認證和整合策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">為伺服器端API生成訪問令牌</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">基於令牌的身份驗證教程</a></td>
    <td>外部系統嘗試在AEM內執行HTTP操作是常見AEM的。<br>建議的方法是實施此處概述的策略，而不是依賴使用中的密碼建立本地用戶AEM名。</td>
  </tr>
  <tr>
    <td>檔案IO/磁碟使用情況</td>
    <td></td>
    <td>由於無法保證分配了多少磁碟空間，並且容器中的實例會來回移動，因此建議不使用檔案I/O操作來寫入或讀取連接到實例的磁AEM盤。</td>
  </tr>
  <tr>
    <td>DAM更新資產工作流</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">asset compute服務</a></td>
    <td>屬於DAM更新資產工作流的媒體處理步驟現在由Asset compute服務替換</td>
  </tr>
  <tr>
    <td>資產上載方法和as a Cloud Service中支援的工作流流程AEM步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">上載API比較和支援的WF流程步驟</a></td>
    <td>在AEMas a Cloud Service中，在上載或下載資產期間，資產流直接進入或流出二進位儲存。</br>AEMaaCS中並不支援所有工作流進程步驟。</td>
  </tr>
  <tr>
    <td>工作流程啟動器</td>
    <td></td>
    <td>從代碼中刪除正在觸發OOTB或自定義DAM更新資產工作流的任何工作流啟動程式。</br>所有上傳到AEMas a Cloud Service的資產將由資產處理處處理。 有關自定義步驟，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 後處理工作流</a> 有關如何設定和配置後處理工作流。</td>
  </tr>
  <tr>
    <td>自定義格式副本步驟</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">處理設定檔</a></td>
    <td>任何自定義格式副本生成、影像轉換或視頻編碼都必須通過建立相應的處理配置檔案卸載到資產處理服務。</td>
  </tr>
  <tr>
    <td>內容搜尋與索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">內容搜索和索引更改</a></td>
    <td>索引的基礎處理以及它何時開始運行都發生了很大變化。<br>在將要部署的代碼中管理Oak索引之前，請完全瞭解並重新構建索引。</td>
  </tr>
  <tr>
    <td>並非所有維護任務都可配置</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Service維護任務</a></td>
    <td>您只能配置某些維護任務，但AEM有as a Cloud Service。</td>
  </tr>
  <tr>
    <td>對發佈儲存庫的更改</td>
    <td></td>
    <td>不允許直接更改「發佈」儲存庫，但/home下的除外。 始終建議對作者進行更改並分發。 所有代碼和配置更改都必須通過相應的Cloud Manager管道部署。</td>
  </tr>
  <tr>
    <td>Dispatcher配置和快取</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">雲中的調度程式</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">快取管理<br></td>
    <td>Dispatcher配置必須遵循特定結構。<br>配置必須作為代碼的一部分進行管理，並通過Cloud Manager管道進行部署。</td>
  </tr>
  <tr>
    <td>備份和還原</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Service備份和恢復</a></td>
    <td></td>
  </tr>
</tbody>
</table>

## 過時的功能 {#deprecated-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

我們建議你參考 [不建議使用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) 熟悉在Experience Manageras a Cloud Service中標籤為已棄用的功能和功能，並瞭解對部署的AEM影響。

## 計畫審查安裝AEM {#review-planning}

一旦您習慣了使用AEMas a Cloud Service引入的更改，就應開始規劃對現有安裝的審查，以便衡量將其移動到雲所需的更改級別。

下圖顯示了在審查階段涉及的關鍵步驟：

![影像](/help/journey-migration/assets/planning-phaseimg1.png)

接下來，我們將詳細探討這些步驟中的每一步意味著什麼。

### 評定雲端服務整備 {#assess-cloud-readiness}

第一步是評估您從現有版本到Cloud Service的AEM準備情況，並確定需要重構的區域，以便與as a Cloud Service兼AEM容。

您需要根據顯著更改和不建議使用的功能AEM對當前原始碼進行全面評估，以確定過渡過程中預期的工作量。

調查結果的數量將直接影響時間安排和項目總體成功。 因此，建議盡可能地發現計畫交付或啟動重新設計符合as a Cloud Service最佳做法所需的任何自定義項所需AEM的對話。

**最佳做法分析器**

通過針對當前版本運行最佳做法分析器，可以加快評AEM估。 要加快評估規劃，必須充分瞭解其工作原理。

你可以通過咨詢 [最佳做法分析器](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 文檔。

**建立雲就緒性評估報告**

下一步是根據迄今獲得的所有知識建立報告。 您可以通過從階段和生產實例生成最佳做法分析器報告來做到這一點， [然後將它們上載到雲加速管理器](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 可操作項目的可消化報告。

典型報告應包含以下輸入：

* 詳細說明特定安裝功能集的文AEM檔
* 有關自定義配AEM置和代碼的詳細資訊
* 生產調度程式配置
* CDN配置（如果有）

**將報告社交**

在最佳做法分析器報告完成後，請與相關團隊共用這些報告，以確認您的發現並規劃您的後續步驟。 根據首選項的不同，您還可以使用 [打印預覽](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam)。

### 檢視資源規劃 {#review-resource-planning}

一旦您估計了移至Cloud Service所需的工作量級別，您就應確定資源、建立團隊，並為過渡流程划出角色和責任。

### 建立 KPI {#establish-kpis}

如果您以前沒有建立主要績效指標(KPI)，建議為實施建立KPIAEM，以幫助您的團隊將精力集中在最重要的方面。

請參閱 [開發KPI](https://guided.adobe.com/welcome/aem/part6.html) 瞭解如何為業務目標選擇正確的KPI。

## 下一步是什麼 {#what-is-next}

一旦您瞭解了移動到as a Cloud Service所需的更AEM改範圍，就該 [使您的代碼和內容雲準備就緒](/help/journey-migration/implementation.md) 執行遷移之前。

## 其他資源 {#additional-resources}

* [雲加速管理器入門](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)  — 有關如何使用Cloud Acceleration Manager加快您向雲移動的全面指南
* [AEMas a Cloud Service:導論、建築與思維的異化](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEMCloud Service](/help/overview/home.md)  — 有關Experience Manageras a Cloud Service文檔的概述，請從此處開始。
* [AEMas a Cloud Service概述](/help/overview/home.md)  — 本指南概述了Experience Manager作為雲服務，包括簡介、術語和體系結構。
* [登機](/help/onboarding/home.md) — 本指南提供了如何開始使用Experience Manageras a Cloud Service的摘要，包括如何獲得訪問權限和設定您的團隊
