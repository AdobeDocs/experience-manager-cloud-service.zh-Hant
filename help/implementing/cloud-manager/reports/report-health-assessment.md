---
title: 生產和中繼環境的健康狀態評估
description: 瞭解如何使用Cloud Manager的健康狀態評估。 您可以掃描AEM環境、執行及檢閱報告、檢視問題詳細資訊、匯出PDF及管理過去執行。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 9%

---


# 健康情況評估 {#about-health-assessment}

健康評估是對AEM as a Cloud Service中Cloud Manager的生產和中繼環境進行的自動化、非侵入式掃描。 它會評估內容、程式碼和設定，以找出反模式並偏離最佳實務，進而改善安全性和效能。

健康狀態評估服務會執行下列動作：

* 掃描環境並暴露效能瓶頸、低效和風險。
* 分析內容結構，例如Blueprint、即時副本和客戶設定。
* 偵測過時的相依性，包括AEM SDK和協力廠商程式庫。
* 標示程式碼品質問題，例如不正確的註解和無效的模式。
* 在儀表板（例如動作中心）中提供可操作的指引。
* 推動主動式修復，提升系統效能。

每次執行都會依嚴重程度列出問題、提供指引和建議修正的連結，並支援報表的PDF匯出。 您可以使用目前狀態的&#x200B;**最新報告**&#x200B;檢視和&#x200B;**過去報告**&#x200B;來比較執行。

另請參閱[健康狀態評估模式](#ha-patterns)以取得規則定義和修正詳細資料。

## 存取「健康狀態評估」頁面 {#access-health-assessment}

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在「**快速存取**」區段中，按一下「**Experience Manager**」。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。 下圖是插圖。 選取您自己的組織名稱。

   ![在Cloud Manager中選取組織](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. 在&#x200B;**我的程式**&#x200B;主控台上，按一下您要檢視其報告的程式。

1. 執行下列其中一項：
   * 在&#x200B;**環境**&#x200B;卡片中，按一下環境名稱右邊的![省略符號圖示或「更多」圖示](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然後從功能表選擇&#x200B;**健康狀態評估**。

     ![從環境卡中的省略符號選單選取健康狀態評估](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * 從左側功能表的&#x200B;**服務**&#x200B;下方，按一下![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**。 在環境頁面上，按一下環境名稱右邊的![省略符號圖示或「更多」圖示](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然後從功能表選擇&#x200B;**健康狀態評估**。

     ![從環境頁面的省略符號選單中選取健康狀態評估](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## 針對選取的環境執行新報告 {#run-report}

1. [存取健康狀態評估頁面](#access-health-assessment)。
1. 在&#x200B;**健康狀態評估**&#x200B;頁面的右上角，確認您即將評估的目標環境。

   如果環境不正確，請按一下![V形下拉式功能表或下拉式功能表，選取不同的環境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)，從清單中選擇正確的環境。

1. 按一下&#x200B;**「執行報表」**。

   ![按一下[健康情況評估]頁面上的[產生新報告]按鈕](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   針對選取的環境執行報告時，**執行報告**&#x200B;會一直停用，直到它完成為止。

   ![報告正在執行](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   報告完成時，報告會顯示在&#x200B;**健康狀態評估**&#x200B;頁面的&#x200B;**最新報告**&#x200B;區段中。

## 檢視最新報告 {#view-latest-report}

* 在&#x200B;**健康狀態評估**&#x200B;頁面上，檢閱&#x200B;**最新報告**&#x200B;區段以取得下列資訊：

   * 最近執行的結果。
   * 執行日期和時間。
   * 問題總數。
   * 重點說明最關鍵的問題。
   * 動作：檢視詳細資料&#x200B;**[或](#view-report-details)**&#x200B;下載所有問題的PDF **[。](#download-pdf-report)**

  ![針對選取的環境產生新報告後的最新評估頁面](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### 檢視最新報告詳細資料 {#view-report-details}

* 在&#x200B;**健康狀態評估**&#x200B;頁面的&#x200B;**最新報告**&#x200B;標題右側，按一下![省略符號圖示或「更多」圖示](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然後按一下&#x200B;**檢視詳細資料**&#x200B;或&#x200B;**下載**。

  **檢視詳細資料**&#x200B;選項會顯示下列專案：

   * 完整的問題清單。
   * 可檢視發現和問題說明。
   * 能夠檢視包含潛在修正的檔案。

     ![問題說明和結果](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * **下載**&#x200B;選項可讓您在PDF中下載個別問題報告。

     ![下載個別問題報告的PDF](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### 下載整個報表的PDF {#download-pdf-report}

* 在報表頁面的右上角附近，按一下&#x200B;**下載**。

  產生的ZIP檔案會包含該報告中偵測到的所有問題的PDF。

  ![下載在報告中發現的所有問題的PDF](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## 檢閱過去的報告 {#review-past-reports}

在&#x200B;**健康狀態評估**&#x200B;頁面上，檢閱&#x200B;**過去報告**&#x200B;區段以取得下列資訊：

* 檢視任何先前報告的詳細資料。
* 檢視每次執行的日期。
* 下載適用於任何報表的PDF。
* 依日期、問題計數或環境排序。

![檢閱過去的報告](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* 在&#x200B;**過去報告**&#x200B;標題的右側，按一下![V形下拉式功能表或下拉式功能表，以選取不同的環境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)來依日期排序過去報告。
* 在報表的最右側，按一下![省略符號圖示或「更多」圖示](https://spectrum.adobe.com/static/icons/ui_18/More.svg)，然後按一下&#x200B;**檢視詳細資料**&#x200B;或&#x200B;**下載**。


## 健康狀態評估模式 {#ha-patterns}

以下為健康評估在AEM as a Cloud Service中偵測到的反模式及問題的完整清單。 此表格將專案分組為三種型別：內容分析、程式碼分析和Cloud Service Optimizer反模式，並針對每種型別提供說明。

| 圖樣名稱 | 類別 | 類型 | 說明 | 影響 | 自動修正？ |
| --- | --- | --- | --- | --- | --- |
| 包含直接使用者新增的自訂AEM群組 | 安全性 | 內容分析 | 使用者直接新增至AEM群組，而非將IMS群組新增為成員。 | 許可權管理和安全性控管可能會變得複雜。 [IMS支援](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/ims-support) | 否 |
| 頁面中缺少JCR內容節點 | 存放庫結構 | 內容分析 | 頁面中遺失`jcr:content`節點。 | Experience Manager as a Cloud Service的功能限制。 [圖樣偵測 — ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | 否 |
| 頁面中缺少Sling資源型別 | 存放庫結構 | 內容分析 | 頁面中遺失`sling:resourceType`。 | Experience Manager as a Cloud Service的功能限制。 [圖樣偵測 — ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | 否 |
| 節點計數過多的頁面 | 效能 | 內容分析 | 頁面結構中有大量節點。 | 頁面載入時間緩慢和使用者體驗不佳。 [模式偵測 — PCX](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | 否 |
| 過多正在執行的工作流程例項 | 效能 | 內容分析 | 正在執行的工作流程例項太多。 | 整體系統效能降低。 [維護任務](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/operations/maintenance) | 否 |
| 未永久刪除的已完成工作流程例項 | 效能 | 內容分析 | 不會清除較舊的已完成工作流程例項。 | 降低系統效率並增加儲存成本。 [維護任務](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/operations/maintenance) | 否 |
| 內容片段使用統計資料 | 統計資料 | 內容分析 | 追蹤使用中的內容片段數量。 | N/A | N/A |
| 內容片段模型使用統計資料 | 統計資料 | 內容分析 | 追蹤使用中的內容片段模型數量。 | N/A | N/A |
| MSM大量藍圖 | 統計資料 | 內容分析 | 追蹤Blueprint的數量。 | 這會增加管理複雜性，並使內容控管更困難。 | 不適用 |
| 每個Blueprint的MSM頁面數 | 統計資料 | 內容分析 | 追蹤每個Blueprint的頁數。 | 這會增加管理複雜性，並使內容控管更困難。 | 不適用 |
| MSM過多的即時副本 | 統計資料 | 內容分析 | 追蹤即時副本的數量。 | 這可能會導致轉出期間的效能問題並使得內容同步化複雜化。 | 不適用 |
| 每個Blueprint的MSM過多即時副本 | 統計資料 | 內容分析 | 追蹤每個Blueprint的即時副本數。 | 這可能會導致轉出期間的效能問題並使得內容同步化複雜化。 | 不適用 |
| Assets數量 | 統計資料 | 內容分析 | 追蹤資產數量。 | N/A | N/A |
| 網站數量 | 統計資料 | 內容分析 | 追蹤網站數量。 | N/A | N/A |
| Forms數量 | 統計資料 | 內容分析 | 追蹤表單數量。 | N/A | N/A |
| 表單片段 | 統計資料 | 內容分析 | 追蹤表單片段的數量。 | N/A | N/A |
| 互動通訊 | 統計資料 | 內容分析 | 追蹤表單通訊互動的數量。 | N/A | N/A |
| FDM | 統計資料 | 內容分析 | 追蹤表單資料模型的數量。 | N/A | N/A |
| 過時的相依性 | 相依性 | 程式碼分析 | 醒目提示客戶存放庫中的過時相依性。 | 與較新AEM版本不相容；可能有安全性漏洞。 | 否 |
| AEM SDK版本不相符 | 相依性 | 程式碼分析 | 舊版(n-2)與Cloud Manager環境版本的比較。 | 這可能會導致在Cloud Manager中發生建置錯誤，以及本機開發環境中的問題。 | 否 |
| 過時的Mockito核心相依性 | 相依性 | 程式碼分析 | 在AEM as a Cloud Service中，4.x.x以下的版本會被視為過時。 | 這可能會導致在Cloud Manager中發生建置錯誤，以及本機開發環境中的問題。 | 否 |
| 不支援的註解 | 相依性 | 程式碼分析 | 客戶的Cloud Manager存放庫中有不支援的註解。 | 潛在的應用程式失敗和效能降低。 | 否 |
| 在Sling模型中新@Inject附註 | 相依性 | 程式碼分析 | 已棄用`@Inject`註解。 | 由於插入式解析度的額外負荷，導致應用程式效能降低。 | 否 |
| 傳出HTTP請求 | 效能 | Cloud Service Optimizer反模式 | 在要求內容、高逾時或未關閉連線中的使用發生問題。 | 整體系統效能降低和可能的中斷。 | 是 |
| 緩慢查詢 | 效能 | Cloud Service Optimizer反模式 | 客戶程式碼中的查詢速度緩慢。 | 系統效能降低和可能的逾時。 | 是 |

### 類別 {#ha-patterns-categories}

| 類別 | 說明 |
| --- | --- |
| 安全性 | 與安全實務、使用者管理和存取控制相關的模式。 |
| 效能 | 影響應用程式和系統效能的模式。 |
| 存放庫結構 | 與JCR存放庫組織和結構相關的模式。 |
| 相依性 | 與程式碼相依性和版本管理相關的模式。 |
| 統計資料 | 代表使用狀況統計資料和量度的模式。 |



