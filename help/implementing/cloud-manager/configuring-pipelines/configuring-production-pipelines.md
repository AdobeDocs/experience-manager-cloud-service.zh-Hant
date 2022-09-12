---
title: 設定生產管道
description: 了解如何設定生產管道，以建立程式碼並部署至生產環境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# 設定生產管道 {#configure-production-pipeline}

了解如何設定生產管道，以建立程式碼並部署至生產環境。 生產管道會先將程式碼部署至預備環境，然後在核准後再將相同的程式碼部署至生產環境。

使用者必須 **[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** 角色來設定生產管道。

>[!NOTE]
>
>在程式建立完成、Git存放庫至少有一個分支，且已建立生產與測試環境集之前，無法設定生產管道。

開始部署程式碼之前，您必須先從 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>您可以 [編輯管道設定](managing-pipelines.md) 在初始設定後。

## 新增生產管道 {#adding-production-pipeline}

設定程式後，請使用 [!UICONTROL Cloud Manager] UI，您已準備好依照下列步驟新增生產管道。

>[!TIP]
>
>配置前端管道之前，請參閱 [AEM快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 以取得易於使用的AEM快速網站建立工具的端對端指南。 此歷程將協助您簡化AEM網站的前端開發，讓您無需AEM後端知識即可快速自訂網站。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，然後按一下 **新增** 選擇 **新增生產管道**.

   ![計畫管理員上的管道卡概述](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 此 **新增生產管道** 對話框。 提供 **管道名稱** 以識別管道及下列選項。 按一下 **繼續**.

   **部署觸發程式**  — 定義部署觸發器以啟動管道時，您有下列選項。

   * **手動**  — 使用此選項手動啟動管道。
   * **Git變更時**  — 只要提交項新增至設定的Git分支，此選項就會啟動CI/CD管道。 使用此選項，您仍然可以根據需要手動啟動管道。

   **重要量度失敗行為**  — 在管道設定或編輯期間， **部署管理員** 具有在任何質量門中遇到重要故障時定義管道行為的選項。 可用選項包括：

   * **每次都問**  — 此為預設設定，需要手動干預任何重要故障。
   * **立即失敗**  — 如果選中，則每當發生重要故障時，管道將被取消。 這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現重要故障時，管道將自動繼續。 這實際上是在模擬使用者手動核准每個失敗。

   ![生產管道設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在 **原始碼** 索引標籤，您必須定義管道應擷取其程式碼的位置，及其程式碼類型。

   * **[前端代碼](#front-end-code)**
   * **[完整堆疊程式碼](#full-stack-code)**
   * **[Web層配置](#web-tier-config)**

完成生產管道建立的步驟因 **原始碼** 您已選取。 請依照上述連結跳至本檔案的下一節，以完成管道的設定。

### 前端代碼 {#front-end-code}

前端程式碼管道會部署包含一或多個用戶端UI應用程式的前端程式碼組建。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 以取得此類管道的詳細資訊。

要完成前端代碼生產管道的配置，請執行以下步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。
   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。
   * **代碼位置**  — 此選項會定義所選存放庫分支中的路徑，管道應從中擷取程式碼。
   * **部署至生產環境前暫停**  — 此選項會在部署至生產環境之前暫停管道。

   ![前端代碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. 按一下 **儲存** 來儲存管道。

管道已保存，您現在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **計畫概述** 頁面。

### 完整堆疊程式碼 {#full-stack-code}

完整堆疊程式碼管道會同時部署後端和前端程式碼組建，其中包含一或多個AEM伺服器應用程式以及HTTPD/Dispatcher設定。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 以取得此類管道的詳細資訊。

>[!NOTE]
>
>如果所選環境已存在完整堆棧代碼管道，則此選擇將被禁用。

若要完成完整堆疊程式碼生產管道的設定，請遵循下列步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。
   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。
   * **代碼位置**  — 此選項會定義所選存放庫分支中的路徑，管道應從中擷取程式碼。
   * **部署至生產環境前暫停**  — 此選項會在部署至生產環境之前暫停管道。
   * **已排程**  — 此選項可讓使用者啟用排程的生產部署。

   ![完整堆疊程式碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 按一下 **繼續** 向 **體驗稽核** 標籤中，您可以定義「體驗稽核」中應一律包含的路徑。

   ![新增體驗稽核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要納入體驗稽核的路徑。

   * 頁面路徑的開頭必須為 `/`.
   * 例如，如果您想要包含 `https://wknd.site/us/en/about-us.html` 在體驗稽核中，輸入路徑 `/us/en/about-us.html`.

   ![定義體驗稽核的路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. 按一下 **新增頁面** 且路徑將會以您環境的位址自動完成，並新增至路徑表。

   ![保存表的路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 重複前兩個步驟，視需要繼續新增路徑。

   * 最多可新增25個路徑。
   * 如果您未定義任何路徑，依預設，網站首頁會包含在體驗稽核中。

1. 按一下 **儲存** 來儲存管道。

為體驗稽核設定的路徑將提交至服務，並在管道執行時根據效能、協助工具、SEO（搜尋引擎最佳化）、最佳實務和PWA（漸進式網頁應用程式）測試進行評估。 請參閱 [了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得更多詳細資訊。

管道已保存，您現在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **計畫概述** 頁面。

### Web層配置 {#web-tier-config}

Web層配置管道部署HTTPD/Dispatcher配置。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 以取得此類管道的詳細資訊。

若要完成完整堆疊程式碼生產管道的設定，請遵循下列步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。
   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。
   * **代碼位置**  — 此選項會定義所選存放庫分支中的路徑，管道應從中擷取程式碼。
      * 對於Web層配置管道，這通常是包含 `conf.d`, `conf.dispatcher.d`，和 `opt-in` 目錄。
      * 例如，如果專案結構是從 [AEM專案原型，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 那條路是 `/dispatcher/src`.
   * **部署至生產環境前暫停**  — 此選項會在部署至生產環境之前暫停管道。
   * **已排程**  — 此選項可讓使用者啟用排程的生產部署。

   ![網層代碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. 按一下 **儲存** 來儲存管道。

>[!NOTE]
>
>如果您有將現有的完整堆疊管道部署至某個環境，則為相同環境建立網頁層設定管道時，將會忽略完整堆疊管道中的現有網頁層設定。

管道已保存，您現在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **計畫概述** 頁面。

## 略過Dispatcher套件 {#skip-dispatcher-packages}

如果您想要在管道中建置Dispatcher套件，但不想將其發佈至建置儲存，則可停用發佈，這可能會縮短管道執行期間。

您必須透過專案新增下列設定，以停用發佈Dispatcher套件 `pom.xml` 檔案。 它以環境變數為基礎，而環境變數可做為標幟，供您在Cloud Manager建置容器中設定，以定義應忽略Dispatcher套件的時間。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
