---
title: 設定非生產管道
description: 了解如何設定非生產管道以在部署到生產環境之前測試計劃碼的品質。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 9804d9b71f082c3d4788667fdc3993af3b673588
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 100%

---

# 設定非生產管道 {#configuring-non-production-pipelines}

了解如何設定非生產管道以在部署到生產環境之前測試計劃碼的品質。

## 非生產管道 {#non-production-pipelines}

此外[生產管道](#configuring-production-pipelines.md)部署到登台和生產環境，您還可以設定非生產管道來驗證您的計劃碼。

有兩種類型的非生產管道：

* **計劃碼品質管道** - 這些會對 Git 分支中的計劃碼執行計劃碼品質掃描並執行組建和計劃碼品質步驟。
* **部署管道** - 除了執行計劃碼品質管道之類的組建和計劃碼品質步驟之外，這些管道還會將計劃碼部署到非生產環境。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增新的非生產管道 {#adding-non-production-pipeline}

設定好方案並擁有至少一個使用 Cloud Manager UI 的環境後，您就可以依照以下步驟著手新增非生產管道了。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從 Cloud Manager 首頁畫面存取&#x200B;**管道**&#x200B;卡。按一下 **+ 新增**&#x200B;並選取&#x200B;**新增非生產管道**。

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**設定**&#x200B;索引標籤 (在&#x200B;**新增非生產管道**&#x200B;對話框中) 上，選取您要建立的非生產管道類型：**計劃碼品質管道**&#x200B;或&#x200B;**部署管道**。

   ![新增非生產管道對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 在&#x200B;**非生產管道名稱**&#x200B;以識別您的管道以及以下附加資訊。

   * **部署觸發程序** - 在定義部署觸發程序以啟動管道時，有以下選項。

      * **手動** - 使用此選項以手動方式啟動管道。
      * **開啟 Git 變更** - 只要將認可新增到已設定的 Git 分支，此選項就會啟動 CI/CD 管道。使用此選項，您仍然可以在需要時手動啟動管道。

1. 按一下&#x200B;**「繼續」**。

1. 在&#x200B;**新增非生產管道**&#x200B;對話框的&#x200B;**來原始計劃碼**&#x200B;索引標籤上，您必須選擇管道應處理的計劃碼類型。

   * **[前端計劃碼](#front-end-code)**
   * **[完整堆疊計劃碼](#full-stack-code)**
   * **[網頁層設定](#web-tier-config)**

完成建立非生產流水線的步驟因所選&#x200B;**原始計劃碼**&#x200B;選項而異。按照上面的連結跳到本文件的下一部分以完成管道的設定。

### 前端計劃碼 {#front-end-code}

前端計劃碼管道部署包含一個或多個用戶端 UI 應用計劃的前端計劃碼建置。有關此類管道的更多資訊，請參閱文件 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)。

若要完成前端計劃碼非生產管道的設定，請按照以下步驟操作。

1. 在&#x200B;**原始計劃碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **符合條件的部署環境**- 如果您的管道是部署管道，您必須選擇它應該部署到哪些環境。
   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取計劃碼。

   >[!TIP]
   > 
   >如要了解如何在 Cloud Manager 中新增和管理存放庫，請參閱文件：[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)。

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取計劃碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能將會尋找相符的分支以幫助您進行選擇。
   * **計劃碼位置** - 此選項會定義管道應從所選存放庫的分支中擷取計劃碼的路徑。

   ![前端管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以在&#x200B;**計劃總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

### 完整堆疊計劃碼 {#full-stack-code}

完整堆疊計劃碼管道同時部署包含一個或多個 AEM 伺服器應用程序以及 HTTPD/Dispatcher 配置的後端和前端計劃碼構建。有關此類管道的更多資訊，請參閱文件 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)。

>[!NOTE]
>
>如果所選環境已存在完整堆疊計劃碼管道，則此選項將會停用。

若要完成完整堆疊計劃碼非生產管道的設定，請按照以下步驟操作。

1. 在&#x200B;**原始計劃碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **符合條件的部署環境**- 如果您的管道是部署管道，您必須選擇它應該部署到哪些環境。
   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取計劃碼。

   >[!TIP]
   > 
   >如要了解如何在 Cloud Manager 中新增和管理存放庫，請參閱文件：[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)。

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取計劃碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能將會尋找相符的分支以幫助您進行選擇。
   * **忽略 Web 層配置**- 選中後，管道將不會部署您的 Web 層配置。

   ![完整堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以在&#x200B;**計劃總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

### Web 層設定 {#web-tier-config}

Web 層設定管道部署 HTTPD/Dispatcher 設定。有關此類管道的更多資訊，請參閱文件 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline)。

>[!NOTE]
>
>如果所選環境已存在網頁層級計劃碼管道，則此選項將會停用。

若要完成網頁層級計劃碼非生產管道的設定，請按照以下步驟操作。

1. 在&#x200B;**原始計劃碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **符合條件的部署環境**- 如果您的管道是部署管道，您必須選擇它應該部署到哪些環境。
   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取計劃碼。

   >[!TIP]
   > 
   >如要了解如何在 Cloud Manager 中新增和管理存放庫，請參閱文件：[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)。

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取計劃碼。
   * **計劃碼位置** - 此選項會定義管道應從所選存放庫的分支中擷取計劃碼的路徑。
      * 如果是 Web 層設定管道，這通常是包含 `conf.d`、`conf.dispatcher.d` 和 `opt-in`目錄的路徑。
      * 例如，如果專案結構是從 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)產生的，則路徑將為 `/dispatcher/src`。

   ![網頁層級管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 按一下「**儲存**」。

>[!NOTE]
>
>如果您將現有的完整堆疊管道部署到環境，則為同一環境建立 Web 層設定管道將忽略完整堆疊管道中的現有 Web 層設定。

管道已儲存，您現在可以在&#x200B;**計劃總覽**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

## 跳過發送器套件 {#skip-dispatcher-packages}

如果您希望將發送器套件建置為管道的一部分，但又不希望將它們發佈到建置儲存，您可以停用發佈它們，這可能會減少管道的執行時間。

必須透過您的專案 `pom.xml` 檔案新增以下停用發佈發送器套件的設定。這會根據環境變數 (作為一個標幟)，您可以在 Cloud Manager 建置容器中設定以定義何時應忽略發送器套件。

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
