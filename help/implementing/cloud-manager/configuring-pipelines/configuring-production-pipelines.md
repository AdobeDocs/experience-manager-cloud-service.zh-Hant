---
title: 新增生產管道
description: 瞭解如何新增生產管道以建置計畫碼並將其部署到生產環境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 35%

---


# 新增生產管道 {#configure-production-pipeline}

瞭解如何設定生產管道以建置計畫碼並將其部署到生產環境。 生產管道會先將計畫碼部署到中繼環境。 在核准後，會將相同的程式碼部署到生產環境。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定生產管道。

>[!NOTE]
>
>在發生以下情況之前，無法設定生產管道：
>
>* 程式隨即建立。
>* Git存放庫至少有一個分支。
>* 生產和中繼環境隨即建立。

開始部署程式碼之前，請從[!UICONTROL Cloud Manager]設定您的管道設定。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增生產管道 {#adding-production-pipeline}

設定好方案並擁有至少一個使用[!UICONTROL Cloud Manager] UI的環境後，您就可以依照以下步驟著手新增生產管道了。

>[!TIP]
>
>在設定前端管道之前，請參閱[AEM Quick Site建立歷程](/help/journey-sites/quick-site/overview.md)，以透過易於使用的AEM Quick Site建立工具取得端到端指南。 此歷程可幫助您簡化AEM網站的前端開發，讓您無需AEM後端知識即可快速自訂網站。

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在&#x200B;**快速存取**&#x200B;區段中，按一下&#x200B;**Experience Manager**。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。
1. 在&#x200B;**我的程式**&#x200B;主控台上，按一下程式。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**方案總覽**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡片，然後按一下&#x200B;**新增**&#x200B;以選取&#x200B;**新增生產管道**。

   ![專案管理員概觀中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **新增生產管道**&#x200B;對話框隨即顯示。提供&#x200B;**管道名稱**&#x200B;以識別您的管道以及以下選項。按一下&#x200B;**「繼續」**。

   **部署觸發計畫** - 在定義部署觸發計畫以啟動管道時，有以下選項。

   * **手動** — 手動啟動管道。
   * **在Git變更上** — 只要將認可新增到已設定的Git分支，就會啟動CI/CD管道。 使用此選項，您仍然可以在需要時手動啟動管道。

   **重要量度失敗行為** - 在管道設定或編輯期間，**部署管理員**&#x200B;可選擇對任何品質閘道中遭遇重要失敗時的管道行為進行定義。可使用的選項包括：

   * **每次都詢問** — 預設設定。 任何重要失敗都需要手動介入。
   * **立即失敗** - 如果選取，則每當重要失敗發生時，會取消管道。此程式基本上是模擬使用者手動拒絕每次失敗。
   * **立即繼續** — 如果選取，則每當重要失敗發生時，管道會自動繼續。 此程式基本上是模擬使用者手動核准每次失敗。

   ![生產管道設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在&#x200B;**Source程式碼**&#x200B;索引標籤上，選取管道應處理的程式碼型別。

   * **[設定完整棧疊計畫碼管道](#full-stack-code)**
   * **[設定目標部署管道](#targeted-deployment)**

如需有關管道型別的詳細資訊，請參閱[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

完成建立生產流水線的步驟因所選原始計畫碼型別而異。 按照上面的連結跳到本文件的下一部分以便完成管道的設定。

### 設定完整棧疊計畫碼管道 {#full-stack-code}

完整棧疊計畫碼管道同時部署包含一個或多個AEM伺服器應用程式以及HTTPD/Dispatcher配置的後端和前端計畫碼構建。

>[!NOTE]
>
>如果所選環境已存在完整堆疊程式碼管道，則此選項會停用。

**若要設定完整棧疊計畫碼管道：**

1. 在&#x200B;**Source程式碼**&#x200B;索引標籤上，定義下列選項。

   * **存放庫** — 定義管道應該從哪個Git存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，瞭解如何在Cloud Manager中新增和管理存放庫。

   * **Git分支** — 定義選取的管道應該從哪個分支擷取程式碼。
輸入分支名稱的前幾個字元，此欄位的自動完成功能會尋找相符的分支以協助您選取。
   * **忽略 Web 層設定**- 選取後，管道不會部署您的 Web 層設定。
   * **在部署到生產之前暫停** — 在部署到生產之前暫停管道。
   * **已排程** — 讓使用者啟用已排程的生產部署。

   ![完整堆疊程式碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 按一下&#x200B;**繼續**&#x200B;進入&#x200B;**體驗稽核**&#x200B;索引標籤，您可以在其中定義應一律包含在體驗稽核中的路徑。

   ![新增體驗稽核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包含在體驗稽核中的路徑。

   * 如需詳細資訊，請參閱[體驗稽核測試](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration)。

1. 按一下&#x200B;**儲存**，即可儲存您的管道。

當管道執行時，會根據效能、協助工具、SEO、最佳實務和PWA測試，提交和評估為體驗稽核設定的路徑。 如需更多詳細資料，請參閱[瞭解體驗稽核結果](/help/implementing/cloud-manager/reports/report-experience-audit.md)。

管道已儲存，您現在可以在&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

### 設定目標部署管道 {#targeted-deployment}

目標部署只會為AEM應用程式的選定部分部署程式碼。 在這種部署中，您可以選擇&#x200B;**包含**&#x200B;下列其中一個型別的程式碼：

* **設定** — 設定AEM環境中各種功能的設定。
   * 如需支援的設定清單，請參閱[使用設定管道](/help/operations/config-pipeline.md)，其中包含記錄檔轉送、清除相關的維護工作以及各種CDN設定，並在您的存放庫中管理這些設定，以便正確部署它們。
   * 執行目標部署管道時，會部署設定，前提是這些設定會儲存至管道中定義的環境、存放庫和分支。
   * 在任何時候，每個環境只能有一個設定管道。
* **設定Edge Delivery Services設定管道** - Edge Delivery設定管道沒有獨立的開發、測試和生產環境。 在AEM as a Cloud Service中，變更會經過開發、階段和生產等層級。 相反地，Edge Delivery設定管道會直接將其設定套用至在Cloud Manager中註冊的所有Edge Delivery Sites網域。 若要深入瞭解，請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。
* **前端計畫碼** — 為AEM應用計畫的前端設定JavaScript和CSS。
   * 有了前端流水線，給前端開發者更多的獨立性，可以加快開發進程。
   * 請參閱文件[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此程序的工作原理以及需要注意的一些注意事項，以充分發揮此程序的潛力。
* **網頁層設定** — 設定Dispatcher屬性，以儲存、處理及傳送網頁給使用者端。
   * 如需詳細資訊，請參閱檔案[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所選環境存在 Web 層程式碼管道，則此選項會停用。
   * 如果您為具有現有完整棧疊管道的環境建立Web層配置管道，則忽略完整棧疊管道中的Web層配置。 此變更只會影響該環境中的Web層設定。

>[!NOTE]
>
>私人存放庫不支援 Web 層和設定管道。請參閱[在Cloud Manager中新增私人存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，以取得詳細資訊和完整的限制清單。

**若要設定目標部署管道：**

1. 選擇所需的部署型別。

![目標部署選項](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. 定義&#x200B;**合格的部署環境**。

   * 如果您的管道是部署管道，則必須選擇它應該部署到哪些環境。

1. 在&#x200B;**Source程式碼**&#x200B;下，定義下列選項：

   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，以便了解如何在 Cloud Manager 中新增和管理存放庫，

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取程式碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能。會尋找相符的分支以幫助您進行選取。
   * **程式碼位置** - 此選項會定義管道應從所選存放庫的分支中擷取程式碼的路徑。
   * **在部署到生產之前暫停** - 此選項會在部署到生產之前暫停管道。
   * **已排程** — 讓使用者啟用已排程的生產部署。 僅適用於Web層目標部署。

   ![設定管道](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以在&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

## 跳過Dispatcher套件 {#skip-dispatcher-packages}

若要在管道中建置Dispatcher套件，而不將套件發佈到建置儲存，您可以停用發佈選項。 這麼做有助於縮短管道的執行時間。

必須透過您的專案 `pom.xml` 檔案新增以下停用發佈 Dispatcher 套件的設定。環境變數可作為您在Cloud Manager建置容器中設定的標幟，以判斷何時應忽略Dispatcher套件。

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
