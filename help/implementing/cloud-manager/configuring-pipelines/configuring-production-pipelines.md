---
title: 設定生產管道
description: 設定生產管道
index: false
source-git-commit: 76cff84003576cf23eb1d23674ce6eaf082bbbb1
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 設定生產管道 {#configure-production-pipeline}

部署管理員負責配置生產管道。

>[!NOTE]
>程式建立完成、Git存放庫至少有一個分支，且已建立生產和預備環境集後，才能設定生產管道。

開始部署程式碼之前，您必須先從 [!UICONTROL Cloud Manager].

>[!NOTE]
>可在初始設定後更改管道設定。

## 新增生產管道 {#adding-production-pipeline}

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




