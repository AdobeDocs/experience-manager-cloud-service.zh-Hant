---
title: 設定CI/CD管道 — Cloud Services
description: 設定CI/CD管道 — Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# 設定 CI-CD 管線 {#configure-ci-cd-pipeline}

在Cloud Manager中，有兩種管道：

* **生產管道**:

   只有建立生產和預備環境集後，才能新增生產管道。

   請參閱 [設定生產管道](configure-pipeline.md#setting-up-the-pipeline) 以取得更多詳細資訊。

* **非生產管道**:

   可從 **概述** 頁面。

   請參閱 [僅限非生產和代碼品質的管道](configure-pipeline.md#non-production-pipelines) 以取得更多詳細資訊。

   >[!NOTE]
   >若要設定管道，您必須：
   > * 定義將啟動管道的觸發器。
   > * 定義控制生產部署的參數。
   > * 配置效能測試參數。


## 設定生產管道 {#setting-up-production-pipeline}

部署管理員負責設定生產管道。

>[!NOTE]
>程式建立完成、Git存放庫至少有一個分支，且已建立生產和預備環境集後，才能設定生產管道。

開始部署程式碼之前，您必須先從 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>可在初始設定後更改管道設定。

### 新增生產管道 {#adding-production-pipeline}

在您設定程式後，並且至少有一個環境使用 [!UICONTROL Cloud Manager] UI，您已準備好新增生產管道。

請依照下列步驟，設定生產管道的行為和偏好設定：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。
按一下 **+添加** 選取 **新增生產管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **新增生產管道** 對話框。 輸入管道名稱。

   此外，您也可以設定 **部署觸發程式** 和 **重要量度失敗行為** 從 **部署選項**. 按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   您可以定義部署觸發器以啟動管道。

   * **手動**  — 使用UI手動啟動管道。
   * **Git變更時**  — 每當有提交項新增至設定的git分支時，就會啟動CI/CD管道。 即使選取此選項，也始終可以手動啟動管道。

      在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。

      這對希望實現更自動化流程的客戶非常有用。 可用選項包括：
   您可以定義重要失敗量度行為以啟動管道。

   * **每次都問**  — 這是預設設定，需要手動干預任何「重要」故障。
   * **立即失敗**  — 如果選中，則每當出現「重要」(Important)故障時，管道將被取消。 這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現「重要」故障時，管道將自動繼續。 這實際上是在模擬使用者手動核准每個失敗。


1. 此 **新增生產管道** 對話框包含標籤為的第二個頁簽 **原始碼**. **完整堆疊程式碼** 中所有規則的URL。 您可以選擇 **存放庫** 和 **Git分支**. 選取「生產部署選項」，如下所述。 按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   生產部署選項：

   * **部署至生產環境前暫停**:此選項可讓部署在生產前暫停。
   * **已排程**:此選項可讓使用者啟用排程的生產部署。

1. 此 **新增生產管道** 對話框包含標籤為的第三個頁簽 **體驗稽核**. 此選項提供URL路徑的表格，這些路徑應一律包含在「體驗稽核」中。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >您必須按一下 **新增頁面** 來定義自訂連結。 頁面路徑的開頭必須為 `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   按一下 **新增頁面** 提供要納入體驗稽核的URL路徑。

   例如，如果您想要包含 `https://wknd.site/us/en/about-us.html` 在體驗稽核中，輸入路徑 `/us/en/about-us.html` 在此欄位中，按一下 **儲存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   表格中顯示的URL將是：

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   最多可包含25列。 如果此區段中沒有使用者提交的頁面，依預設，網站首頁會包含在體驗稽核中。

   請參閱 [了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得更多詳細資訊。

   >[!NOTE]
   > 系統會將已設定的頁面提交至服務，並根據效能、協助工具、SEO（搜尋引擎最佳化）、最佳實務和PWA（漸進式網頁應用程式）測試來評估。

1. 按一下 **儲存**. 新建立的生產管道現在會顯示在 **管道** 卡片。

   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許添加新管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **更多詳情**  — 導覽至了解CI/CD管道檔案資源。

### 編輯生產管道 {#editing-prod-pipeline}

可以從 **計畫概述** 頁面。

請依照下列步驟編輯已設定的管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **編輯**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. 此 **編輯生產管道** 對話框。

   1. 此 **設定** 索引標籤可讓您更新 **管道名稱**, **部署觸發程式**，和 **重要量度失敗行為**.

      >[!NOTE]
      >請參閱 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 此 **來源** 索引標籤提供可勾選或取消勾選的選項 **部署至生產環境前暫停** 和 **已排程** 選項 **生產部署選項**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 此 **體驗稽核** 選項可讓您更新或新增頁面。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. 按一下 **更新** 編輯管道後。

### 其他生產管道動作 {#additional-prod-actions}

#### 執行生產管道 {#run-prod}

可以從「管道」卡運行生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **執行**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### 刪除生產管道 {#delete-prod}

您可以從「管道」卡中刪除生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **刪除**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >部署管理員角色中的使用者現在可以透過 **刪除** 選項。


## 僅限非生產和代碼品質的管道 {#non-production-pipelines}

除了部署至預備和生產的主要管道外，客戶還能設定額外的管道，稱為非生產管道。
非生產管道有兩種類型：

1. 程式碼品質：在Git分支的程式碼上執行程式碼品質掃描。 此管道會執行建置和程式碼品質步驟。
1. 部署：除了執行建置和程式碼品質步驟外，此管道還會將程式碼部署至選取的非生產環境至AEMas a Cloud Service環境。

### 新增非生產管道 {#adding-non-production-pipeline}

在主螢幕上，這些管道會列在新卡中：

1. 存取 **管道** Cloud Manager主畫面中的資訊卡。 按一下 **+添加** 選取 **新增非生產管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **新增非生產管道**  對話框。 選取要建立的管線類型 **程式碼品質管道** 或 **部署管道**.

   >[!NOTE]
   >對於部署管道，必須選擇部署環境。

   此外，您也可以設定 **部署觸發程式** 和 **重要量度失敗行為** 從 **部署選項**. 按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **完整堆疊程式碼** 中所有規則的URL。 您可以選擇 **存放庫** 和 **Git分支**. 按一下 **儲存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 新建立的非生產管道現在會顯示在 **管道** 卡片。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許添加新管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **更多詳情**  — 導覽至了解CI/CD管道檔案資源。

### 編輯非生產管道 {#editing-nonprod-pipeline}

可以從 **管道卡** 從 **計畫概述** 頁面。

請依照下列步驟編輯已設定的非生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 選取非生產管道，然後按一下 **...**. 按一下 **編輯**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. 此 **編輯生產管道** 對話框。

   1. 此 **設定** 索引標籤可讓您更新 **管道名稱**, **部署觸發程式**，和 **重要量度失敗行為**.

      >[!NOTE]
      >請參閱 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. 此 **原始碼** 索引標籤會提供您更新 **存放庫** 和 **Git分支**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. 按一下 **更新** 編輯完非生產管道後。

### 其他非生產管道動作 {#additional-nonprod-actions}

#### 執行非生產管道 {#run-nonprod}

可以從「管道」卡運行生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **執行**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### 刪除非生產管道 {#delete-nonprod}

您可以從「管道」卡中刪除生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **刪除**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## 後續步驟 {#the-next-steps}

設定管道後，您需要部署程式碼。

請參閱 [部署程式碼](deploy-code.md) 以取得更多詳細資訊。
