---
title: 體驗稽核儀表板
description: 探索體驗稽核如何驗證您的部署流程，確保變更符合效能、協助工具、最佳實務和SEO的基準標準。 它提供清楚且資訊豐富的儀表板介面，以便追蹤這些量度。
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---


# 體驗稽核控制面板 {#experience-audit-dashboard}

<!-- Engineer architect over this feature was Bogdan Anton; scrum master Alexandru Nica -->

探索體驗稽核如何驗證您的部署流程，確保變更符合效能、協助工具、最佳實務和SEO （搜尋引擎最佳化）的基準標準。 它提供清楚且資訊豐富的儀表板介面，以便追蹤這些量度。

## 概觀 {#overview}

體驗稽核會驗證部署流程，並協助確保已部署變更：

1. 符合效能、協助工具、最佳實務及SEO的基準標準。
1. 不要引入迴歸。

Cloud Manager中的體驗稽核可確保使用者在網站上的體驗達到最高標準。

稽核結果會提供資訊，可讓部署管理員查看目前和先前分數之間的分數和變更。此深入分析對於判斷是否有會於目前部署引入的迴歸十分有用。

體驗稽核由[Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) (Google的開放原始碼工具)提供技術支援，並在所有Cloud Manager生產管道中啟用。

## 可用性 {#availability}

體驗稽核適用於Cloud Manager：

* （預設） Sites生產管道。
* （選用）開發完整棧疊管道。
* （可選）開發前端管道。

請參閱[設定區段](#configuration)，以取得如何為選擇性環境設定稽核的詳細資訊。

稽核會在管道中執行。 稽核也可以是在管道外部[隨選執行](#on-demand)。

## 設定 {#configuration}

生產管道預設會提供體驗稽核。 可以選擇啟用它來開發完整棧疊和前端管道。 在所有情況下，您需要定義在管道執行期間評估哪些內容路徑。

1. 根據您要設定的管道型別，執行下列操作之一：

   * [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)以定義您要稽核評估的路徑。
   * [如果您要在前端或開發完整棧疊管道上啟用稽核，請新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。
   * [編輯現有管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，並更新現有選項。

1. 若要在新增或編輯非生產管道時使用體驗稽核，請選取&#x200B;**體驗稽核**&#x200B;核取方塊。 您可以在&#x200B;**Source代碼**&#x200B;標籤上找到此選項。

   ![正在啟用體驗稽核](/help/implementing/cloud-manager/reports/assets/experience-audit-enable.jpg)

   * 僅對於非生產管道是必要的。
   * 選取核取方塊時，**體驗稽核**&#x200B;索引標籤就會顯示。

1. 對於生產和非生產管道，您定義應包含在&#x200B;**體驗稽核**&#x200B;標籤上的體驗稽核中的路徑。

   * 頁面路徑必須以`/`開頭，且相對於您的網站。
   * 例如，如果您的網站是`wknd.site`且想要在體驗稽核中包含`https://wknd.site/us/en/about-us.html`，請輸入路徑`/us/en/about-us.html`。

   ![定義體驗稽核的路徑](/help/implementing/cloud-manager/reports/assets/experience-audit-add-page.png)

1. 按一下「**新增頁面**」，路徑會使用您的環境地址自動完成並新增到路徑表中。

   ![儲存表格的路徑](/help/implementing/cloud-manager/reports/assets/experience-audit-page-added.png)

1. 重複前兩個步驟根據需要繼續新增路徑。

   * 您最多可以新增 25 個路徑。
   * 如果您未定義任何路徑，則預設情況下該網站的首頁會包含在體驗稽核中。

1. 按一下&#x200B;**儲存**。

## 體驗稽核結果 {#results}

透過&#x200B;**生產管道執行頁面**，體驗稽核的結果會顯示在生產管道的[階段測試](/help/implementing/cloud-manager/deploy-code.md)階段。

![管道中的儀表板](/help/implementing/cloud-manager/reports/assets/experience-audit-dashboard.png)

體驗稽核提供[已設定頁面](#configuration)的Google Lighthouse分數中位數，以及與上次掃描的分數差異。

從管道的&#x200B;**階段測試**&#x200B;階段的這個摘要檢視中，您有兩個選項：

* **[檢視最慢的頁面](#view-slowest-pages)**
* **[檢視完整報告](#view-full-report)**

您可以按一下Cloud Manager儀表板中的&#x200B;**報表**&#x200B;索引標籤，以存取完整的稽核結果。 除了管道執行詳細資訊中顯示的摘要之外，您還可以直接檢視[完整報告](#view-full-report)。

>[!TIP]
>
>以下各節將說明如何檢視體驗稽核的結果。
>
>* 若要瞭解稽核運作方式的詳細資訊，請參閱[體驗稽核評估詳細資料](#details)。
>* 若要瞭解如何隨選執行體驗稽核，請參閱[隨選稽核報表](#on-demand)。
>* 如果您遇到稽核的問題，請參閱[體驗稽核遇到問題](#issues)。

### 檢視最慢的頁面 {#view-slowest-pages}

按一下&#x200B;**檢視最慢的頁面**&#x200B;以開啟&#x200B;**最慢的5個頁面**&#x200B;對話方塊。 將顯示您[設定為稽核](#configuration)的五個效能最低的頁面。

![最慢的五個](/help/implementing/cloud-manager/reports/assets/experience-audit-slowest-five.png)

Cloud Manager會依&#x200B;**效能**、**協助工具**、**最佳實務**&#x200B;及&#x200B;**SEO**&#x200B;來劃分分數，並顯示每個量度與先前稽核的偏差。

依預設，會開啟對話方塊，其中包含行動裝置的分數。 您可以在對話方塊頂端附近使用&#x200B;**裝置**&#x200B;切換功能來檢視案頭分數。

此對話方塊的用途是提供快速概覽。 如需完整詳細資訊，請按一下&#x200B;**檢視完整報告**。

### 檢視完整報告 {#view-full-report}

您可以執行下列操作來檢視完整的體驗稽核報表：

* 在&#x200B;**`View full report`**&#x200B;最慢的5頁&#x200B;**[對話方塊中按一下](#view-slowest-pages)**。
* 檢視管道&#x200B;**`View full report`**&#x200B;的[執行時，請按一下](#results)。
* 按一下Cloud Manager中的&#x200B;**報表**&#x200B;索引標籤。

Cloud Manager的&#x200B;**報告**&#x200B;標籤已開啟，顯示&#x200B;**體驗稽核**。

![體驗稽核報告](/help/implementing/cloud-manager/reports/assets/experience-audit-reports.png)

報告分為兩個區域：

* **[頁面分數 — 趨勢](#trend)**
* **[體驗稽核掃描結果](#results)**

#### 頁面分數 — 趨勢 {#trend}

根據預設，**頁面分數的選取檢視 — 趨勢**&#x200B;是去年&#x200B;**的**&#x200B;中位數分數&#x200B;**個**。

您可以按一下圖例中的類別名稱，選擇檢視特定Lighthouse類別的趨勢。

![趨勢可選擇](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-selectable.png)

使用圖表頂端的下拉式清單&#x200B;**選取**&#x200B;以選取特定頁面的詳細資料，而底部的&#x200B;**檢視**&#x200B;和&#x200B;**觸發器**&#x200B;下拉式清單則分別選取不同的時間範圍和觸發器型別。

**檢視**&#x200B;下拉式清單可讓您選取預設的時間範圍，或選取更特定檢視的自訂間隔。

![趨勢檢視](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-view.png)

將滑鼠移到圖表上時，工具提示會在特定時間點顯示Google Lighthouse類別的值。

![趨勢詳細資料](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-details.png)

如果您在某個時間點按一下圖表，則會開啟包含該掃描詳細資訊的快顯視窗。 按一下&#x200B;**開啟體驗稽核掃描**，將該掃描結果載入&#x200B;**[體驗稽核掃描結果](#scan-results)**&#x200B;區段。

![選取不同的掃描](/help/implementing/cloud-manager/reports/assets/experience-audit-open-scan.png)

#### 體驗稽核掃描結果 {#scan-results}

**體驗稽核掃描結果**&#x200B;區段提供所有掃描頁面上分數的詳細資料。 使用&#x200B;**上一頁**&#x200B;和&#x200B;**下一頁**&#x200B;按鈕來逐頁瀏覽結果，並選擇顯示應分頁的數量。

![掃描的頁面](/help/implementing/cloud-manager/reports/assets/experience-audit-scanned-pages.png)

按一下特定頁面的連結，會更新&#x200B;**頁面分數 — 趨勢**&#x200B;區段&#x200B;[**的篩選器**&#x200B;選取](#trend)，並顯示&#x200B;**原始報告**&#x200B;索引標籤，該索引標籤會提供您每個頁面稽核的分數。 按一下&#x200B;**Lighthouse報表**&#x200B;欄中的報表日期，以擷取原始資料的JSON檔案。

![原始報告](/help/implementing/cloud-manager/reports/assets/experience-audit-raw-reports.png)

在瀏覽器中開啟的新標籤會將您導向至`https://googlechrome.github.io/lighthouse/viewer/`。 它會針對選取的頁面，自動載入包含Lighthouse原始JSON報告的已簽署URL，以允許詳細檢查。

![檢視原始報告](/help/implementing/cloud-manager/reports/assets/experience-audit-view-raw-report.png)

## 隨選掃描稽核報告 {#on-demand}

除了在管道執行期間執行外，還可以隨選產生體驗稽核報告。 此選項是快速掃描頁面的理想解決方案，您不必執行管道。

若要執行隨選掃描，請瀏覽至&#x200B;**報告**&#x200B;標籤，以便檢視完整的稽核報告，然後按一下&#x200B;**執行掃描**&#x200B;按鈕。

![隨選掃描](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand.png)

當隨選掃描已執行時，**執行掃描**&#x200B;按鈕會變成無法使用，且會以時鐘圖示標籤。

![正在執行隨選掃描](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-running.png)

隨選掃描會觸發針對最新25個[已設定頁面](#configuration)的體驗稽核，通常會在幾分鐘內完成。

完成時，分數圖表會自動更新，您可以檢查結果，就像管道執行掃描一樣。

您可以使用&#x200B;**觸發器**&#x200B;選擇器，根據觸發器型別篩選分數圖表。

![觸發篩選器](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>只有在未刪除環境且相同環境中沒有其他擱置掃描時，才能啟動隨選掃描。

## 體驗稽核遇到問題 {#issues}

如果您設定為要稽核的[頁面](#configuration)無法使用或稽核中有其他錯誤，則體驗稽核會反映此事實。

管道會顯示可展開的錯誤區段，以檢視它無法存取的相對URL路徑。

![體驗稽核遇到的問題](/help/implementing/cloud-manager/reports/assets/experience-audit-issues.png)

如果檢視完整報告，詳細資訊會顯示在&#x200B;**[體驗稽核掃描結果](#results)**&#x200B;區段中，此區段也是可展開的。

![完整報告問題](/help/implementing/cloud-manager/reports/assets/experience-audit-issues-report.png)

無法使用頁面的部分原因包括：

* 設定會封鎖存取。
* 頁面不存在。
* 頁面重新導向，需要基本驗證以外的驗證。
* 發生內部問題。

>[!TIP]
>
>[存取頁面的原始報告](#scan-results)可提供無法稽核頁面的詳細資訊。

## 體驗稽核評估詳細資料 {#details}

下列詳細資料提供體驗稽核如何評估您的網站的其他資訊。 這些不是功能一般使用的必要專案，此處提供這些專案是為了完整起見。

* 稽核會從發行者的`.com`已設定的體驗稽核頁面路徑[掃描來源(](#configuration))網域，以模擬真實的使用者體驗，協助您針對管理和最佳化網站做出更好的決策。
* 在生產完整棧疊管道中，會掃描中繼環境。 為了確保稽核在稽核期間提供相關的詳細資訊，中繼環境的內容應儘可能接近生產環境。
* 在&#x200B;**頁面分數 — 趨勢**&#x200B;區段&#x200B;[**的下拉式清單** Select](#trend)中顯示的頁面都是體驗稽核過去掃描過的已知頁面。
