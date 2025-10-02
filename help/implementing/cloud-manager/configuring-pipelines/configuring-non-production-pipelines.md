---
title: 新增非生產管道
description: 瞭解如何新增非生產管道，以在部署到生產環境之前測試計畫碼的品質。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 07ed9bd6d9830bc9120b59cab43f834ef8620709
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 58%

---


# 新增非生產管道 {#configuring-non-production-pipelines}

了解如何設定非生產管道以在部署到生產環境之前測試程式碼的品質。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定非生產管道。

## 非生產管道 {#non-production-pipelines}

此外[生產管道](#configuring-production-pipelines.md)部署到中繼和生產環境，您還可以設定非生產管道來驗證您的程式碼。

有兩種類型的非生產管道：

* **程式碼品質管道** - 這些管道會對 Git 分支中的程式碼執行程式碼品質掃描，並執行建置和程式碼品質步驟。
* **部署管道** — 除了執行程式碼品質管道之類的組建和程式碼品質步驟之外，這些管道還會將程式碼部署到非生產環境。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增一個全新非生產管道 {#adding-non-production-pipeline}

設定好方案並擁有至少一個使用 Cloud Manager UI 的環境後，您就可以依照以下步驟著手新增非生產管道了。

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在&#x200B;**快速存取**&#x200B;區段中，按一下&#x200B;**Experience Manager**。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。
1. 在&#x200B;**我的程式**&#x200B;主控台上，按一下程式。

1. 從 Cloud Manager 首頁畫面存取&#x200B;**管道**&#x200B;卡。按一下「**+新增**」並選取「**新增非生產管道**」。

   ![新增非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**新增非生產管道**&#x200B;對話框的&#x200B;**設定**&#x200B;索引標籤上，選取您要新增的非生產管道。

   * **程式碼品質管道** - 建立管道來建構您的程式碼、執行單元測試和評估程式碼品質但「不」部署。
   * **部署管道** - 建立管道來建構您的程式碼、執行單元測試、評估程式碼品質，並部署到環境。

   ![新增非生產管道對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 在&#x200B;**非生產管道名稱**&#x200B;以識別您的管道以及以下附加資訊。

   * **部署觸發程序** - 在定義部署觸發程序以啟動管道時，有以下選項。

      * **手動** — 使用此選項以手動方式啟動管道。
      * **在Git變更時** — 只要將認可新增到已設定的Git分支，此選項就會啟動CI/CD管道。 使用此選項，您仍然可以在需要時手動啟動管道。

1. 如果您選擇建立&#x200B;**部署管道**，您還必須定義&#x200B;**重要的量度失敗行為**。

   * **每次都詢問** - 此行為是預設設定，要求對任何重要失敗進行手動介入。
   * **立即失敗** - 如果選取，則每當重要失敗發生時，會取消管道。這基本上是模擬使用者手動拒絕每次失敗。
   * **立即持續** - 如果選取，則每當重要失敗發生時，管道會自動繼續。這基本上是模擬使用者手動核准每次失敗。

1. 按一下&#x200B;**「繼續」**。

1. 在&#x200B;**新增非生產管道**&#x200B;對話框的&#x200B;**來原始程式碼**&#x200B;索引標籤上，您必須選擇管道應處理的程式碼類型。

   * **[完整堆疊程式碼](#full-stack-code)**
   * **[目標部署](#targeted-deployment)**

如需有關管道型別的詳細資訊，請參閱[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

完成建立非生產流水線的步驟因所選原始計畫碼型別而異。 按照上面的連結跳到本文件的下一部分以便完成管道的設定。

### 完整堆疊程式碼 {#full-stack-code}

完整棧疊計畫碼管道同時部署包含一個或多個AEM伺服器應用程式以及HTTPD/Dispatcher配置的後端和前端計畫碼構建。

>[!NOTE]
>
>如果所選環境存在完整堆疊程式碼管道，則此選項會停用。

若要完成完整堆疊程式碼非生產管道的設定，請按照以下步驟操作。

1. 在&#x200B;**原始程式碼**&#x200B;索引標籤上，您必須定義以下選項。

   * **符合條件的部署環境**- 如果您的管道是部署管道，您必須選擇它應該部署到哪些環境。
   * **存放庫** - 此選項會定義管道應該從哪個 Git 存放庫擷取程式碼。

   >[!TIP]
   > 
   >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，以便了解如何在 Cloud Manager 中新增和管理存放庫，

   * **Git 分支** - 此選項會定義管道應該選取哪個分支來擷取程式碼。
      * 輸入分支名稱的前幾個字元，該欄位的自動完成功能。會尋找相符的分支以幫助您進行選取。
   * **忽略 Web 層設定**- 選取後，管道不會部署您的 Web 層設定。
   * **管道** - 如果您的管道是部署管道，您可以選擇執行測試階段。確認您希望在此階段啟用的選項。如果沒有選取任何選項，則在管道執行期間不會顯示測試階段。

      * **產品功能測試** - 針對開發環境執行[產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。
      * **自訂功能測試** - 針對開發環境執行[自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。
      * **自訂 UI 測試** - 為自訂應用程式執行[自訂 UI 測試](/help/implementing/cloud-manager/ui-testing.md)。
      * **體驗稽核** — 執行[體驗稽核](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![完整堆疊管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

管道已儲存，您現在可以在&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

### 目標部署 {#targeted-deployment}

目標部署只會為AEM應用程式的選定部分部署程式碼。 在這種部署中，您可以選擇&#x200B;**包含**&#x200B;下列其中一個型別的程式碼：

* **設定** — 設定AEM環境中各種功能的設定。
   * 如需支援的設定清單，請參閱[使用設定管道](/help/operations/config-pipeline.md)，其中包含記錄檔轉送、清除相關的維護工作以及各種CDN設定，並在您的存放庫中管理這些設定，以便正確部署它們。
   * 執行目標部署管道時，會部署設定，前提是這些設定會儲存至您在管道中定義的環境、存放庫和分支。
   * 在任何時候，每個環境只能有一個設定管道。
* **設定Edge Delivery Services設定管道** - Edge Delivery設定管道沒有獨立的開發、測試和生產環境。 在AEM as a Cloud Service中，變更會經過開發、階段和生產等層級。 相反地，Edge Delivery設定管道會直接將其設定套用至在Cloud Manager中註冊的所有Edge Delivery Sites網域。 若要深入瞭解，請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。
* **前端計畫碼** — 為AEM應用計畫的前端設定JavaScript和CSS。
   * 有了前端流水線，給前端開發者更多的獨立性，可以加快開發進程。
   * 請參閱文件[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此程序的工作原理以及需要注意的一些注意事項，以充分發揮此程序的潛力。
* **網頁層設定** — 設定Dispatcher屬性，以儲存、處理及傳送網頁給使用者端。
   * 如需詳細資訊，請參閱檔案[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所選環境存在 Web 層程式碼管道，則此選項會停用。
   * 如果完整棧疊管道已部署到環境，您仍然可以為該同一環境建立Web層配置管道。 若您這麼做，Cloud Manager會忽略完整棧疊管道中的網頁層設定。


>[!NOTE]
>
>私人存放庫不支援 Web 層和設定管道。請參閱[在Cloud Manager中新增私人存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，以取得詳細資訊和完整的限制清單。

選擇部署型別後，完成建立非生產、目標部署管道的步驟相同。

1. 選擇所需的部署型別。

![目標部署選項](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

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
   * **管道** — 對於前端非生產管道，您可以選擇啟用&#x200B;**[體驗稽核](/help/implementing/cloud-manager/reports/report-experience-audit.md)**。

   ![設定管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. 如果您已啟用體驗稽核，請按一下「**繼續**」以前往「**體驗稽核**」標籤，您可以在其中定義應一律包含在體驗稽核中的路徑。

   * 如果您已啟用&#x200B;**體驗稽核**，請參閱檔案[體驗稽核](/help/implementing/cloud-manager/reports/report-experience-audit.md)以瞭解如何設定的詳細資訊。
   * 如果您沒有這麼做，請略過此步驟。

1. 按一下&#x200B;**儲存**，即可儲存管道。

管道已儲存，您現在可以在&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡上[管理您的管道](managing-pipelines.md)。

## 跳過Dispatcher套件 {#skip-dispatcher-packages}

如果您想要在管道中建置Dispatcher套件，但未上傳到建置儲存，請停用發佈。 這樣做可以縮短管道的執行時間。

必須透過您的專案 `pom.xml` 檔案新增以下停用發佈 Dispatcher 套件的設定。在Cloud Manager建置容器中設定環境變數，以標幟何時忽略Dispatcher套件。 管道會讀取此旗標並據此忽略它們。

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
