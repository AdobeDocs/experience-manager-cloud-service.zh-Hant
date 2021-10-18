---
title: 設定CI/CD管道 — Cloud Services
description: 設定CI/CD管道 — Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 01cd4efc920515996c928a8cb455bb44d4f722f2
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---

# 設定 CI-CD 管線 {#configure-ci-cd-pipeline}

在Cloud Manager中，有兩種管道：

* **生產管道**:

   只有建立生產和預備環境集後，才能新增生產管道。

   如需詳細資訊，請參閱[設定生產管道](configure-pipeline.md#setting-up-the-pipeline) 。

* **非生產管道**:

   您可以從Cloud Manager使用者介面的&#x200B;**概述**&#x200B;頁面新增非生產管道。

   如需詳細資訊，請參閱[僅限非生產與程式碼品質管道](configure-pipeline.md#non-production-pipelines)。

   >[!NOTE]
   >若要設定管道，您必須：
   > * 定義將啟動管道的觸發器。
   > * 定義控制生產部署的參數。
   > * 配置效能測試參數。


## 設定生產管道 {#setting-up-production-pipeline}

部署管理員負責設定生產管道。

>[!NOTE]
>程式建立完成、Git存放庫至少有一個分支，且已建立生產和預備環境集後，才能設定生產管道。

開始部署代碼之前，必須從[!UICONTROL Cloud Manager]配置管道設定。

>[!NOTE]
>
>可在初始設定後更改管道設定。

### 新增生產管道 {#adding-production-pipeline}

設定程式並使用[!UICONTROL Cloud Manager] UI至少有一個環境後，您就可以新增生產管道了。

請依照下列步驟，設定生產管道的行為和偏好設定：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**卡片。
按一下**+Add**&#x200B;並選擇&#x200B;**添加生產管道**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **新增生產** 管道對話方塊隨即顯示。輸入管道名稱。

   此外，您也可以從&#x200B;**部署選項**&#x200B;設定&#x200B;**部署觸發器**&#x200B;和&#x200B;**重要度量失敗行為**。 按一下&#x200B;**繼續**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   您可以定義部署觸發器以啟動管道。

   * **手動**  — 使用UI手動啟動管道。
   * **On Git Changes**  — 每當有提交項新增至設定的Git分支時，就會啟動CI/CD管道。即使選取此選項，也始終可以手動啟動管道。

      在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。

      這對希望實現更自動化流程的客戶非常有用。 可用選項包括：
   您可以定義重要失敗量度行為以啟動管道。

   * **每次詢問**  — 此為預設設定，需要手動干預任何「重要」失敗。
   * **立即失敗**  — 如果選中此選項，則每當出現「重要」故障時，管道都將被取消。這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現「重要」故障時，管道將自動繼續。這實際上是在模擬使用者手動核准每個失敗。


1. **添加生產管道**&#x200B;對話框包含標籤為&#x200B;**原始碼**&#x200B;的第二個頁簽。 **已選擇完** 整堆棧代碼。您可以選擇&#x200B;**Repository**&#x200B;和&#x200B;**Git分支**。 選取「生產部署選項」，如下所述。 按一下&#x200B;**繼續**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   生產部署選項：

   * **部署至生產環境前暫停**:此選項可讓部署在生產前暫停。
   * **已排程**:此選項可讓使用者啟用排程的生產部署。

1. **新增生產管道**&#x200B;對話方塊包含標示為&#x200B;**體驗稽核**&#x200B;的第三個索引標籤。 此選項提供URL路徑的表格，這些路徑應一律包含在「體驗稽核」中。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >您必須按一下&#x200B;**新增頁面**&#x200B;以定義您自己的自訂連結。 頁面路徑的開頭必須為`/`。
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   按一下「**新增頁面**」 ，提供要納入體驗稽核的URL路徑。

   例如，如果您想要在體驗稽核中加入`https://wknd.site/us/en/about-us.html`，請在此欄位中輸入路徑`/us/en/about-us.html`，然後按一下&#x200B;**儲存**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   表格中顯示的URL將是：

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   最多可包含25列。 如果此區段中沒有使用者提交的頁面，依預設，網站首頁會包含在體驗稽核中。

   如需詳細資訊，請參閱[了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md) 。

   >[!NOTE]
   > 系統會將已設定的頁面提交至服務，並根據效能、協助工具、SEO（搜尋引擎最佳化）、最佳實務和PWA（漸進式網頁應用程式）測試來評估。

1. 按一下&#x200B;**Save**。 新建立的生產管道現在會顯示在&#x200B;**管道**&#x200B;卡中。

   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許新增管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **了解更多**  — 導覽至了解CI/CD管道檔案資源。

### 編輯生產管道 {#editing-prod-pipeline}

您可以從&#x200B;**程式概述**&#x200B;頁面編輯管道設定。

請依照下列步驟編輯已設定的管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**編輯**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. 隨即顯示&#x200B;**編輯生產管道**&#x200B;對話方塊。

   1. **Configuration**&#x200B;標籤允許您更新&#x200B;**Pipeline Name**、**Deployment Trigger**&#x200B;和&#x200B;**Important Metrics Failure Behavior**。

      >[!NOTE]
      >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，了解如何在Cloud Manager中新增和管理存放庫。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. **Source**&#x200B;索引標籤提供選項，可在部署至生產&#x200B;**之前勾選或取消勾選**&#x200B;暫停，以及從&#x200B;**生產部署選項**&#x200B;排程&#x200B;**選項。**

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. **體驗稽核**&#x200B;選項可讓您更新或新增頁面。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. 編輯管道後，按一下&#x200B;**更新**。

### 其他生產管道動作 {#additional-prod-actions}

#### 執行生產管道 {#run-prod}

可以從「管道」卡運行生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**運行**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### 刪除生產管道 {#delete-prod}

您可以從「管道」卡中刪除生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...從**&#x200B;管道&#x200B;**卡中按一下**&#x200B;刪除&#x200B;**，如下圖所示。**

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >部署管理員角色中的使用者現在可以透過管道卡中的&#x200B;**Delete**&#x200B;選項，以自助方式刪除生產管道。


## 僅限非生產和代碼品質的管道 {#non-production-pipelines}

除了部署到預備和生產的主管道外，客戶還可以設定其他管道，稱為&#x200B;**非生產管道**。 這些管道一律會執行建置和程式碼品質步驟。 他們也可選擇部署至AEMas a Cloud Service環境。

### 新增非生產管道 {#adding-non-production-pipeline}

在主螢幕上，這些管道會列在新卡中：

1. 從Cloud Manager主畫面存取&#x200B;**管道**&#x200B;卡片。 按一下&#x200B;**+Add**&#x200B;並選擇&#x200B;**添加非生產管道**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **添加非生產管道**  對話框隨即顯示。選取您要建立的管道類型，可以是&#x200B;**代碼品質管道**&#x200B;或&#x200B;**部署管道**。

   此外，您也可以從&#x200B;**部署選項**&#x200B;設定&#x200B;**部署觸發器**&#x200B;和&#x200B;**重要度量失敗行為**。 按一下&#x200B;**繼續**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **已選擇完** 整堆棧代碼。您可以選擇&#x200B;**Repository**&#x200B;和&#x200B;**Git分支**。 按一下&#x200B;**Save**。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 新建立的非生產管道現在顯示在&#x200B;**管道**&#x200B;卡中。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許新增管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **了解更多**  — 導覽至了解CI/CD管道檔案資源。

### 編輯非生產管道 {#editing-nonprod-pipeline}

您可以從&#x200B;**程式概述**&#x200B;頁面的&#x200B;**管道卡**&#x200B;編輯管道配置。

請依照下列步驟編輯已設定的非生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 選擇非生產管道，然後按一下&#x200B;**...**。 按一下&#x200B;**Edit**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. 隨即顯示&#x200B;**編輯生產管道**&#x200B;對話方塊。

   1. **Configuration**&#x200B;標籤允許您更新&#x200B;**管道名稱**、**部署觸發器**&#x200B;和&#x200B;**重要度量失敗行為**。

      >[!NOTE]
      >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，了解如何在Cloud Manager中新增和管理存放庫。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. **原始碼**&#x200B;標籤提供您更新&#x200B;**Repository**&#x200B;和&#x200B;**Git分支**。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. 編輯完非生產管道後，按一下「**更新**」。

### 其他非生產管道動作 {#additional-nonprod-actions}

#### 執行非生產管道 {#run-nonprod}

可以從「管道」卡運行生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**運行**，如下圖所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### 刪除非生產管道 {#delete-nonprod}

您可以從「管道」卡中刪除生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...從**&#x200B;管道&#x200B;**卡中按一下**&#x200B;刪除&#x200B;**，如下圖所示。**

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## 後續步驟 {#the-next-steps}

設定管道後，您需要部署程式碼。

如需詳細資訊，請參閱[部署程式碼](deploy-code.md) 。
