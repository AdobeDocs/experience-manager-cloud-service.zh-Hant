---
title: 設定非生產管道
description: 了解如何先設定非生產管道，以測試程式碼品質，再部署至生產環境。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 9804d9b71f082c3d4788667fdc3993af3b673588
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 設定非生產管道 {#configuring-non-production-pipelines}

了解如何先設定非生產管道，以測試程式碼品質，再部署至生產環境。

## 非生產管道 {#non-production-pipelines}

除 [生產管道](#configuring-production-pipelines.md) 可部署至測試和生產環境，您也可以設定非生產管道以驗證您的程式碼。

非生產管道有兩種類型：

* **程式碼品質管道**  — 這些程式會對Git分支中的程式碼執行程式碼品質掃描，並執行建置和程式碼品質步驟。
* **部署管道**  — 除了執行程式碼品質管道等建置和程式碼品質步驟外，這些管道還會將程式碼部署至非生產環境。

>[!NOTE]
>
>您可以 [編輯管道設定](managing-pipelines.md) 在初始設定後。

## 新增非生產管道 {#adding-non-production-pipeline}

設定程式並使用Cloud Manager UI至少有一個環境後，您就可以依照下列步驟新增非生產管道。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 存取 **管道** Cloud Manager主畫面中的資訊卡。 按一下 **+添加** 選取 **新增非生產管道**.

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **設定** 的 **新增非生產管道** 對話框，選擇要添加的非生產管道類型 **程式碼品質管道** 或 **部署管道**.

   ![新增非生產管道對話方塊](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生產管道名稱** 以識別管道，以及下列其他資訊。

   * **部署觸發程式**  — 定義部署觸發器以啟動管道時，您有下列選項。

      * **手動**  — 使用此選項手動啟動管道。
      * **Git變更時**  — 只要提交項新增至設定的Git分支，此選項就會啟動CI/CD管道。 使用此選項，您仍然可以根據需要手動啟動管道。

1. 按一下 **繼續**.

1. 在 **原始碼** 的 **新增非生產管道** 對話框中，必須選擇管道應處理的代碼類型。

   * **[前端代碼](#front-end-code)**
   * **[完整堆疊程式碼](#full-stack-code)**
   * **[Web層配置](#web-tier-config)**

完成建立非生產管道的步驟會依 **原始碼** 您已選取。 請依照上述連結跳至本檔案的下一節，以完成管道的設定。

### 前端代碼 {#front-end-code}

前端程式碼管道會部署包含一或多個用戶端UI應用程式的前端程式碼組建。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 以取得此類管道的詳細資訊。

要完成前端代碼非生產管道的配置，請執行以下步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **合格的部署環境**  — 如果您的管道是部署管道，則必須選取應部署它的環境。
   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。
   * **代碼位置**  — 此選項會定義所選存放庫分支中的路徑，管道應從中擷取程式碼。

   ![前端管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 按一下「**儲存**」。

管道已保存，您現在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **計畫概述** 頁面。

### 完整堆疊程式碼 {#full-stack-code}

完整堆疊程式碼管道會同時部署後端和前端程式碼組建，其中包含一或多個AEM伺服器應用程式以及HTTPD/Dispatcher設定。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 以取得此類管道的詳細資訊。

>[!NOTE]
>
>如果所選環境已存在完整堆棧代碼管道，則此選擇將被禁用。

若要完成完整堆疊程式碼非生產管道的設定，請遵循下列步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **合格的部署環境**  — 如果您的管道是部署管道，則必須選取應部署它的環境。
   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將找到匹配的分支，以幫助您選擇。
   * **忽略Web層配置**  — 若勾選此選項，管道將不會部署您的Web層組態。

   ![全堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

管道已保存，您現在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **計畫概述** 頁面。

### Web層配置 {#web-tier-config}

Web層配置管道部署HTTPD/Dispatcher配置。 請參閱檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 以取得此類管道的詳細資訊。

>[!NOTE]
>
>如果所選環境已存在Web層代碼管道，則此選擇將被禁用。

要完成Web層代碼非生產管道的配置，請執行以下步驟。

1. 在 **原始碼** 頁簽，必須定義以下選項。

   * **合格的部署環境**  — 如果您的管道是部署管道，則必須選取應部署它的環境。
   * **存放庫**  — 此選項會定義管道應從哪個Git存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱檔案 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支**  — 此選項定義管道中應從哪個分支擷取代碼。
   * **代碼位置**  — 此選項會定義所選存放庫分支中的路徑，管道應從中擷取程式碼。
      * 對於Web層配置管道，這通常是包含 `conf.d`, `conf.dispatcher.d`，和 `opt-in` 目錄。
      * 例如，如果專案結構是從 [AEM專案原型，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 那條路是 `/dispatcher/src`.

   ![Web層管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 按一下「**儲存**」。

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
