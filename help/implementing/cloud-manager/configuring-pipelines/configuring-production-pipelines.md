---
title: 設定生產管道
description: 了解如何設定生產管道以建置程式碼並將其部署到生產環境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 04c65018734f95e8245a6922d5a05c5486a4ffa4
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 72%

---


# 設定生產管道 {#configure-production-pipeline}

瞭解如何設定生產管道以建置計畫碼並將其部署到生產環境。 生產管道會先將計畫碼部署到中繼環境，並在獲得核准後將相同的計畫碼部署到生產環境。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定生產管道。

>[!NOTE]
>
>直到計畫建立完成，Git存放庫至少有一個分支，並建立生產和測試環境集後，才能設定生產管道。

在開始部署程式碼之前，您必須從 [!UICONTROL Cloud Manager] 設定管道設定。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增生產管道 {#adding-production-pipeline}

設定好計畫並擁有至少一個使用 [!UICONTROL Cloud Manager] UI 的環境後，您就可以依照以下步驟著手新增非生產管道了。

>[!TIP]
>
>在設定前端管道之前，請參閱 [AEM Quick Site 建立歷程](/help/journey-sites/quick-site/overview.md)，以透過易於使用的 AEM Quick Site 建立工具取得端到端指南。此歷程可幫助您簡化 AEM 網站的前端開發，讓您無需 AEM 後端知識即可快速自訂網站。

1. 登入Cloud Manager於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織

1. 在 **[我的計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 畫面，選取程式。

1. 導覽至 **管道** 卡來自 **計畫總覽** 頁面並按一下 **新增** 以選取 **新增生產管道**.

   ![計畫管理員概觀中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **新增生產管道**&#x200B;對話框隨即顯示。提供&#x200B;**管道名稱**&#x200B;以識別您的管道以及以下選項。按一下&#x200B;**「繼續」**。

   **部署觸發計畫** - 在定義部署觸發計畫以啟動管道時，有以下選項。

   * **手動** - 使用此選項以手動方式啟動管道。
   * **開啟 Git 變更** - 只要將認可新增到已設定的 Git 分支，此選項就會啟動 CI/CD 管道。使用此選項，您仍然可以在需要時手動啟動管道。

   **重要量度失敗行為** - 在管道設定或編輯期間，**部署管理員**&#x200B;可選擇對任何品質閘道中遭遇重要失敗時的管道行為進行定義。可使用的選項包括：

   * **每次都詢問** - 這是預設設定，要求對任何重要失敗進行手動介入。
   * **立即失敗** - 如果選取，則每當重要失敗發生時，會取消管道。這基本上是模擬使用者手動拒絕每次失敗。
   * **立即持續** - 如果選取，則每當重要失敗發生時，管道將自動繼續。這基本上是模擬使用者手動核准每次失敗。

   ![生產管道設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在 **原始碼** 索引標籤您必須選取管道應處理的程式碼型別。

   * **[完整堆疊程式碼](#full-stack-code)**
   * **[目標部署](#targeted-deployment)**

另請參閱 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 有關管道型別的詳細資訊。

完成建立生產流水線的步驟因所選原始計畫碼型別而異。 按照上面的連結跳到本文件的下一部分以便完成管道的設定。

### 完整堆疊程式碼 {#full-stack-code}

完整棧疊計畫碼管道同時部署包含一個或多個AEM伺服器應用程式以及HTTPD/Dispatcher配置的後端和前端計畫碼構建。

>[!NOTE]
>
>如果所選環境已存在完整堆疊程式碼管道，則此選項會停用。

若要完成完整堆疊程式碼生產管道的設定，請按照以下步驟操作。

1. 在&#x200B;**原始程式碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取程式碼。

   >[!TIP]
   > 
   >如要了解如何在 Cloud Manager 中新增和管理存放庫，請參閱文件：[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)。

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取程式碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能將會尋找相符的分支以幫助您進行選擇。
   * **忽略 Web 層設定**- 選取後，管道不會部署您的 Web 層設定。
   * **在部署到生產之前暫停** - 此選項會在部署到生產之前暫停管道。
   * **已排程** - 此選項可讓使用者啟用已排程的產生部署。

   ![完整堆疊程式碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 按一下&#x200B;**繼續**&#x200B;進入&#x200B;**體驗稽核**&#x200B;索引標籤，您可以在其中定義應一律包含在體驗稽核中的路徑。

   ![新增體驗稽核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包含在體驗稽核中的路徑。

   * 路徑的開頭必須是 `/`。
   * 例如，如果您想將 `https://wknd.site/us/en/about-us.html` 納入體驗稽核中，請輸入路徑 `/us/en/about-us.html`。

   ![定義體驗稽核的路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. 按一下「**新增頁面**」，路徑會使用您的環境地址自動完成並新增到路徑表中。

   ![儲存表格的路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 重複前兩個步驟根據需要繼續新增路徑。

   * 您最多可以新增 25 個路徑。
   * 如果您未定義任何路徑，則預設情況下該網站的首頁會包含在體驗稽核中。

1. 按一下&#x200B;**儲存**，即可儲存您的管道。

為體驗稽核設定的路徑會提交給服務，並在管道執行時根據效能、協助工具、SEO (搜尋引擎最佳化)、最佳實務和 PWA (漸進式 Web 應用程式) 測試進行評估。如需更多詳細資訊，請參閱[了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md)。

管道已儲存，您現在可以在&#x200B;**計畫概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

### 目標部署 {#targeted-deployment}

目標部署只會為AEM應用程式的選定部分部署程式碼。 在這樣的部署中，您可以選擇 **包含** 下列其中一種程式碼型別：

* **設定**  — 在您的AEM環境中設定流量篩選規則的設定。
   * 檢視檔案 [包含WAF規則的流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) 以瞭解如何管理存放庫中的設定，以便正確部署。
   * 執行目標部署管道時， [WAF設定](/help/security/traffic-filter-rules-including-waf.md) 將部署，前提是它們會儲存到您在管道中定義的環境、存放庫和分支。
   * 在任何時候，每個環境只能有一個設定管道。
* **前端計畫碼**  — 為AEM應用程式的前端設定JavaScript和CSS。
   * 有了前端流水線，給前端開發者更多的獨立性，可以加快開發進程。
   * 請參閱文件[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此程序的工作原理以及需要注意的一些注意事項，以充分發揮此程序的潛力。
* **Web層設定**  — 設定Dispatcher屬性以儲存、處理並傳送網頁給使用者端。
   * 檢視檔案 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 以取得更多詳細資料。
   * 如果所選環境存在 Web 層程式碼管道，則此選項會停用。
   * 如果您將現有的完整堆疊管道部署到環境，則為同一環境建立 Web 層設定管道將忽略完整堆疊管道中的現有 Web 層設定。

選擇部署型別後，完成建立生產、目標部署管道的步驟相同。

1. 選擇所需的部署型別。

![目標部署選項](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. 定義 **符合資格的部署環境**.

   * 如果您的管道是部署管道，則必須選擇它應該部署到哪些環境。

1. 在 **原始碼**，定義下列選項：

   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)，以便了解如何在 Cloud Manager 中新增和管理存放庫，

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取程式碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能。會尋找相符的分支以幫助您進行選取。
   * **程式碼位置** - 此選項會定義管道應從所選存放庫的分支中擷取程式碼的路徑。
   * **在部署到生產之前暫停** - 此選項會在部署到生產之前暫停管道。
   * **已排程**  — 此選項可讓使用者啟用已排程的生產部署。 僅適用於Web層目標部署。

   ![設定管道](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以在&#x200B;**計畫概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

## 跳過發送器套件 {#skip-dispatcher-packages}

如果您希望將 Dispatcher 套件建置為管道的一部分，但又不希望將它們發佈到建置儲存，您可以停用發佈它們，這可能會減少管道的執行時間。

必須透過您的專案 `pom.xml` 檔案新增以下停用發佈 Dispatcher 套件的設定。這會根據環境變數 (作為一個標幟)，您可以在 Cloud Manager 建置容器中設定以定義何時應忽略 Dispatcher 套件。

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
