---
title: 體驗稽核儀表板
description: 瞭解體驗稽核如何驗證您的部署流程，並透過清晰、資訊豐富的儀表板介面，協助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 8%

---


# 體驗稽核儀表板 {#experience-audit-dashboard}

瞭解體驗稽核如何驗證您的部署流程，並透過清晰、資訊豐富的儀表板介面，協助確保部署的變更符合效能、協助工具、最佳實務和SEO的基準標準。

>[!NOTE]
>
>此功能僅適用於[早期採用者方案。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>如需AEMas a Cloud Service現有體驗稽核功能的詳細資訊，請參閱此檔案 [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

## 概觀 {#overview}

體驗稽核會驗證部署流程，並幫助確保已部署變更：

1. 符合效能、協助工具、最佳實務、SEO (搜尋引擎最佳化) 和 PWA (漸進式 Web 應用程式) 的基線標準。

1. 不要引入迴歸。

Cloud Manager中的體驗稽核可確保使用者在網站上的體驗達到最高標準。

稽核結果會提供資訊，可讓部署管理員查看目前和先前分數之間的分數和變更。此深入分析對於判斷是否有會於目前部署引入的迴歸十分有用。

體驗稽核由提供技術支援 [Google燈塔](https://developer.chrome.com/docs/lighthouse/overview/)，Google中的開放原始碼工具，並在所有Cloud Manager生產管道中啟用。

## 可用性 {#availability}

體驗稽核適用於Cloud Manager：

* 網站生產管道，預設為
* 開發完整棧疊管道（可選）
* 開發前端管道（可選）

請參閱 [設定區段](#configuration) 有關如何為選用環境設定稽核的詳細資訊。

稽核會在管道中執行。 稽核也可以是 [隨選執行](#on-demand) 位於管線之外。

## 設定 {#configuration}

生產管道預設會提供體驗稽核。 您可以選擇啟用它來開發完整棧疊和前端管道。 在所有情況下，您需要定義在管道執行期間評估哪些內容路徑。

1. 根據您要設定的管線型別，請遵循以下指示：

   * 新增 [生產管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 如果要定義稽核要評估的路徑。
   * 新增 [非生產管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 如果您想要在前端或開發完整棧疊管道上啟用稽核。
   * 或者，您可以 [編輯現有管道，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) 並更新現有選項。

1. 如果您要新增或編輯要使用體驗稽核的非生產管道，則必須選取 **體驗稽核** 上的核取方塊 **原始碼** 標籤。

   ![啟用體驗稽核](assets/experience-audit-enable.jpg)

   * 這僅對非生產管道是必要的。
   * 此 **體驗稽核** 核取方塊選取時，標籤隨即顯示。

1. 對於生產和非生產管道，您可以定義應包含在上的體驗稽核中的路徑 **體驗稽核** 標籤。

   * 頁面路徑的開頭必須是 `/` 和是相對於您的網站。
   * 例如，若您的網站為 `wknd.site` 並且想要包含 `https://wknd.site/us/en/about-us.html` 在體驗稽核中，輸入路徑 `/us/en/about-us.html`.

   ![定義體驗稽核的路徑](assets/experience-audit-add-page.png)

1. 點選或按一下 **新增頁面** 路徑會使用您環境的地址自動完成，並新增至路徑表中。

   ![儲存表格的路徑](assets/experience-audit-page-added.png)

1. 重複前兩個步驟根據需要繼續新增路徑。

   * 您最多可以新增 25 個路徑。
   * 如果您未定義任何路徑，則預設情況下該網站的首頁會包含在體驗稽核中。

1. 按一下&#x200B;**儲存**，即可儲存您的管道。

## 體驗稽核結果 {#results}

體驗稽核的結果會顯示在生產管道的&#x200B;**中繼測試**&#x200B;階段中 (經由[生產管道執行頁面)。](/help/implementing/cloud-manager/deploy-code.md)

![管道中的儀表板](assets/experience-audit-dashboard.jpg)

體驗稽核提供以下專案的Google Lighthouse分數中位數： [已設定的頁面](#configuration) 和上次掃描的分數差異。

從這個摘要檢視 **中繼測試** 管路的階段，您有兩個選項：

* **[檢視最慢的頁面](#view-slowest-pages)**
* **[檢視完整報告](#view-full-report)**

除了在管道執行的詳細資訊中顯示的摘要之外，您還可以使用直接存取稽核的完整結果 **報表** 要存取的Cloud Manager控制面板的標籤 [完整報告](#view-full-report) 直接。

>[!TIP]
>
>以下各節將說明如何檢視體驗稽核的結果。
>
>* 如果您想取得稽核運作方式的詳細資訊，請參閱區段 [體驗稽核評估詳細資料。](#details)
>* 如果您想瞭解如何隨選執行體驗稽核，請參閱區段 [隨選稽核報表。](#on-demand)
>* 如果您遇到稽核的問題，請參閱區段 [體驗稽核遇到問題。](#issues)
>* 如需一般效能提示，請參閱區段 [一般效能秘訣。](#performance-tips)

### 檢視最慢的頁面 {#view-slowest-pages}

點選或按一下 **檢視最慢的頁面** 開啟 **最慢的5頁** 對話方塊，顯示您目前執行效能最低的五個頁面 [設定為稽核。](#configuration)

![最慢的五](assets/experience-audit-slowest-five.jpg)

分數劃分依據 **效能**， **協助工具**， **最佳實務**、和 **SEO** 以及每個量度與上次稽核的差異。

預設情況下，對話方塊會開啟，其中包含行動裝置的分數。 您可以使用將此變更為案頭分數 **裝置** 在對話方塊頂端切換。

此對話方塊旨在提供快速概覽。 如需完整詳細資訊，請點選或按一下 **檢視完整報告**.

### 檢視完整報告 {#view-full-report}

您可以透過以下方式檢視完整的體驗稽核報表：

* 點選或按一下 **檢視完整報告** 在 **[最慢的5頁](#view-slowest-pages)** 對話方塊。
* 點選或按一下 **檢視完整報告** 檢視 [管道的執行。](#results)
* 點選或按一下 **報表** 索引標籤來識別。

此 **報表** Cloud Manager的索引標籤已開啟，並顯示 **體驗稽核**.

![體驗稽核報表](assets/experience-audit-reports.png)

報告分為兩個區域：

* **[頁面分數 — 趨勢](#trend)**
* **[體驗稽核掃描結果](#results)**

#### 頁面分數 - 趨勢 {#trend}

依預設，選取的檢視 **頁面分數 — 趨勢** 是 **中位數分數** 針對 **過去6個月**.

使用 **選取** 和 **檢視** 圖表按鈕頂部和底部的下拉式清單，分別選取頁面特定詳細資訊和不同的時間範圍。 點選或按一下，然後 **更新趨勢** 按鈕以套用選取專案並重新整理圖表。

將滑鼠移到圖表上時，工具提示會在特定時間點顯示Google Lighthouse類別的值。

![趨勢詳細資料](assets/experience-audit-trend-details.png)

如果您在某個時間點點選或按一下圖表，則會開啟彈出視窗，其中包含該掃描的詳細資訊。 點選或按一下 **開啟體驗稽核掃描** 將掃描結果載入到 **[體驗稽核掃描結果](#scan-results)** 區段。

![選取不同的掃描](assets/experience-audit-open-scan.png)

#### 體驗稽核掃描結果 {#scan-results}

此 **體驗稽核掃描結果** 區段提供如何改善分數的建議，以及所有掃描頁面的詳細資訊。 它分為兩個部分：

* **[Recommendations](#recommendations)**
* **[掃描的頁面](#scanned-pages)**

##### 建議 {#recommendations}

此 **Recommendations** 區段會顯示一組彙總的深入分析。 根據預設，建議用於 **績效** 都會顯示。 使用「 」旁的下拉式清單 **Recommendations** 標題以變更為其他類別。

![Recommendations](assets/experience-audit-recommendations.png)

點選或按一下任何建議的>形箭號，即可顯示相關詳細資訊。

![建議詳細資料](assets/experience-audit-recommendation-details.png)

可用時，擴充的建議詳細資料也包含建議影響的百分比，以協助聚焦於最具影響力的變更。

點選或按一下 **檢視頁面** 詳細資料檢視中的連結，以檢視套用建議的頁面。

![建議詳細資訊的頁面](assets/experience-audit-details-pages.png)

##### 掃描的頁面 {#scanned-pages}

此 **掃描的頁面** 區段提供所有掃描頁面的詳細資訊分數。 您可以使用 **前一個** 和 **下一個** 按鈕來逐頁瀏覽結果，並選擇顯示的頁面數量。

![掃描的頁面](assets/experience-audit-scanned-pages.png)

點選或按一下特定頁面的連結會更新 **選取** 的篩選器 [**頁面分數 — 趨勢** 區段](#trend) 並顯示 **分數和建議** 頁簽來選取頁面。

![頁面結果](assets/experience-audit-page-results.png)

此 **原始報表** 標籤會提供您每個頁面稽核的分數。 點選或按一下 **下載** 圖示以擷取原始資料的JSON檔案。

![原始報告](assets/experience-audit-raw-reports.png)

這會在您的瀏覽器中開啟一個新索引標籤，指向 `https://googlechrome.github.io/lighthouse/viewer/` 以及所選頁面之Lighthouse原始JavaScript物件標籤法(JSON)報告的已簽署URL，該報告會自動開啟供您詳細檢查

![檢視原始報表](assets/experience-audit-view-raw-report.png)

## 隨選稽核報表 {#on-demand}

除了在管道執行期間執行外，還可以隨選產生體驗稽核報表。 這是快速掃描頁面的好解決方案，不必執行管道。

若要執行隨選掃描，請瀏覽至  **報表** 標籤以檢視完整的稽核報表，然後點選或按一下 **執行掃描** 按鈕。

![隨選掃描](assets/experience-audit-on-demand.png)

隨選掃描會觸發最新25個體驗的稽核 [已設定的頁面](#configuration) 而且通常會在幾分鐘內完成。

完成時，分數圖表將自動更新，您可以檢查與管道執行掃描完全相同的結果。

您可以使用來根據觸發程式型別篩選分數圖表。 **觸發** 選擇器。

![觸發篩選器](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>只有在未刪除環境且相同環境中沒有其他擱置掃描時，才能啟動隨選掃描。

## 體驗稽核遇到的問題 {#issues}

如果 [您設定的頁面](#configuration) 將無法使用要稽核的，體驗稽核會反映這一點。

管道會顯示可展開的錯誤區段，以檢視它無法存取的相對URL路徑。

![體驗稽核遇到的問題](assets/experience-audit-issues.jpg)

如果檢視完整報告，詳細資料會顯示在 **[體驗稽核掃描結果](#results)** 區段。

![完整報告問題](assets/experience-audit-issues-reports.jpeg)

無法使用頁面的部分原因包括：

* 設定會封鎖存取。
* 頁面不存在。
* 頁面重新導向，需要基本驗證以外的驗證。
* 發生內部問題。
* 等等

>[!TIP]
>
>[存取原始報表](#scanned-pages) 對於頁面，可提供無法稽核頁面的詳細原因。

## 一般效能提示 {#performance-tips}

容易修正的兩個最常見具影響力問題與「累積版面位移(CLS)」和「最大內容繪製(LCP)」有關。

這些可透過以下方式改善：

* 請勿延遲載入摺頁上方的影像（瀏覽器中顯示的內容，不需要向下捲動）。
* 適當地排定載入資源的優先順序（例如，在檔案載入後，以非同步方式載入摺頁下方的影像）。
* 預先擷取用於呈現摺疊上方內容的JavaScript和CSS檔案（如有必要）。
* 將外觀比例指定給緩慢載入或稍後呈現的容器，以保留垂直空間。
* 將影像轉換為WebP格式以縮小其大小。
* 使用 `<picture>` 和影像 `srcset` 不同檢視區大小有不同的影像大小（並確保調整大小有效）。

## 體驗稽核評估詳細資料 {#details}

下列詳細資料提供體驗稽核如何評估您的網站的其他資訊。 這些不是功能一般使用的必要專案，此處提供這些專案是為了完整起見。

* 雖然 [設定的體驗稽核頁面路徑](#configuration) 顯示 `.com` 發行者的網域，稽核會掃描來源(`.net`)網域，以確保偵測到開發期間發生的問題。
   * 此 `.com` 網域使用CDN且可能產生更好的分數或包含快取的結果。
* 在生產完整棧疊管道中，會掃描中繼環境。
   * 為確保稽核在稽核期間提供相關詳細資訊，中繼環境的內容應儘可能接近生產環境。
* 顯示在中的頁面 **選取** 中的下拉式清單 [**頁面分數 — 趨勢** 區段](#trend) 是體驗稽核過去掃描過的所有已知頁面。
* [建議](#recommendations) 可能會有潛在增益，而且與先前的掃描有所差異。
   * 體驗稽核會藉由處理每個頁面的原始報表，並將浪費的位元組或毫秒與對效能分數具有加權影響的分析建立關聯，來估計潛在的增益。
   * 稽核會提供這項資訊（以及受影響的頁面），協助您決定要遵循哪個建議。
   * 如需詳細資訊，請參閱 [一般效能提示段落](#performance-tips)
* 鑑於前端管道可部署到現有環境（或可能有多個前端管道以相同環境為目標），並且掃描結果會在環境層級彙總，無論觸發掃描的管道執行為何操作，分數、趨勢和建議都會顯示在相同的選定環境中。
