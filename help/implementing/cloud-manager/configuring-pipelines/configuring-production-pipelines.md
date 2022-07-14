---
title: 配置生產管線
description: 瞭解如何配置生產管道以構建代碼並將其部署到生產環境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# 配置生產管道 {#configure-production-pipeline}

瞭解如何配置生產管道以構建代碼並將其部署到生產環境。 生產管道首先將代碼部署到階段環境，並在批准後將相同代碼部署到生產環境。

用戶必須具有 **[部署管理器](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** 用於配置生產管道的角色。

>[!NOTE]
>
>在程式建立完成、Git儲存庫至少具有一個分支並且建立生產和登台環境集之前，無法設定生產管道。

開始部署代碼之前，必須從 [!UICONTROL 雲管理器]。

>[!NOTE]
>
>你可以 [編輯管線設定](managing-pipelines.md) 在初始設定後。

## 添加新生產管道 {#adding-production-pipeline}

一旦您設定了程式，並且至少有一個環境使用 [!UICONTROL 雲管理器] UI，您可以通過執行以下步驟添加生產管道。

>[!TIP]
>
>在配置前端管道之前，請參見 [快速AEM建立站點](/help/journey-sites/quick-site/overview.md) 通過易於使用的快速站點建立工AEM具提供端到端指南。 此路程將幫助您簡化站點的前端開發AEM，使您無需任何後端知識就可以快AEM速定制站點。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 的 **添加** 選擇 **添加生產管道**。

   ![「程式管理器」(Program Manager)概述中的「管道」(Pipelines)卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 的 **添加生產管道** 對話框。 提供 **管道名稱** 以標識管線以及以下選項。 按一下 **繼續**。

   **部署觸發器**  — 定義部署觸發器以啟動管線時，有以下選項。

   * **手動**  — 使用此選項手動啟動管線。
   * **Git更改**  — 只要將提交添加到配置的git分支中，此選項就啟動CI/CD管道。 使用此選項，您仍可根據需要手動啟動管線。

   **重要度量故障行為**  — 在管道設定或編輯期間， **部署管理器** 具有在任何質量門中遇到重要故障時定義管線行為的選項。 可用選項包括：

   * **每次詢問**  — 這是預設設定，需要對任何重要故障進行手動干預。
   * **立即失敗**  — 如果選中此選項，則每當發生重要故障時，管線將被取消。 這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當發生重要故障時，管線將自動繼續。 這實質上是模擬用戶手動批准每個故障。

   ![生產管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在 **原始碼** 頁籤，您必須定義管道應檢索其代碼的位置及其代碼的類型。

   * **[前端代碼](#front-end-code)**
   * **[完整堆棧代碼](#full-stack-code)**
   * **[Web層配置](#web-tier-config)**

完成生產管道建立的步驟取決於 **原始碼** 的上界。 按照上面的連結跳轉到本文檔的下一部分，以完成管線的配置。

### 前端代碼 {#front-end-code}

前端代碼管道部署包含一個或多個客戶端UI應用程式的前端代碼生成。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 的子菜單。

要完成前端代碼生產流水線的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。
   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將查找匹配的分支以幫助您選擇。
   * **代碼位置**  — 此選項定義選定回購的分支中的路徑，管道應從中檢索代碼。
   * **在部署到生產之前暫停**  — 此選項在部署到生產之前暫停管道。

   ![前端代碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. 按一下 **保存** 保存管道。

管線已保存，現在可 [管理管道](managing-pipelines.md) 的 **管線** 卡 **計畫概述** 的子菜單。

### 完整堆棧代碼 {#full-stack-code}

全堆棧代碼管道同時部署包含一個或多個伺服器應用程式以及HTTPD/AEMDispatcher配置的後端和前端代碼生成。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 的子菜單。

>[!NOTE]
>
>如果所選環境已存在全堆棧代碼管道，則此選擇將被禁用。

要完成全堆棧代碼生產管線的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。
   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將查找匹配的分支以幫助您選擇。
   * **代碼位置**  — 此選項定義選定回購的分支中的路徑，管道應從中檢索代碼。
   * **在部署到生產之前暫停**  — 此選項在部署到生產之前暫停管道。
   * **計畫**  — 此選項允許用戶啟用計畫生產部署。

   ![完整堆棧代碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 按一下 **繼續** 向 **經驗審計** 頁籤中，您可以定義應始終包含在「體驗審計」中的路徑。

   ![添加體驗審核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包括在體驗審計中的路徑。

   * 頁面路徑必須以開頭 `/`。
   * 例如，如果要包括 `https://wknd.site/us/en/about-us.html` 在體驗審計中，輸入路徑 `/us/en/about-us.html`。

   ![定義體驗審計的路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. 按一下 **添加頁** 路徑將自動完成並添加到路徑表中。

   ![保存表路徑](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 重複前兩個步驟，繼續根據需要添加路徑。

   * 最多可添加25條路徑。
   * 如果未定義任何路徑，則預設情況下，站點首頁將包括在「體驗審計」中。

1. 按一下 **保存** 保存管道。

為「體驗審核」配置的路徑將提交到服務，並在管道運行時根據效能、可訪問性、SEO（搜索引擎優化）、最佳實踐和PWA(Progressive Web App)test進行評估。 請參閱 [瞭解經驗審計結果](/help/implementing/cloud-manager/experience-audit-testing.md) 的子菜單。

管線已保存，現在可 [管理管道](managing-pipelines.md) 的 **管線** 卡 **計畫概述** 的子菜單。

### Web層配置 {#web-tier-config}

Web層配置管道部署HTTPD/Dispatcher配置。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 的子菜單。

要完成全堆棧代碼生產管線的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。
   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
      * 輸入分支名稱的前幾個字元，此欄位的自動完成功能將查找匹配的分支以幫助您選擇。
   * **代碼位置**  — 此選項定義選定回購的分支中的路徑，管道應從中檢索代碼。
      * 對於Web層配置管道，這通常是包含 `conf.d`。 `conf.dispatcher.d`, `opt-in` 的子菜單。
      * 例如，如果項目結構是從 [原型AEM計畫，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 那條路是 `/dispatcher/src`。
   * **在部署到生產之前暫停**  — 此選項在部署到生產之前暫停管道。
   * **計畫**  — 此選項允許用戶啟用計畫生產部署。

   ![Web層代碼](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. 按一下 **保存** 保存管道。

>[!NOTE]
>
>如果現有的全堆棧管線部署到某個環境，則為同一環境建立Web層配置管線將會忽略整個堆棧管道中的現有Web層配置。

管線已保存，現在可 [管理管道](managing-pipelines.md) 的 **管線** 卡 **計畫概述** 的子菜單。

## 跳過Dispatcher包 {#skip-dispatcher-packages}

如果希望將調度程式包作為管道的一部分生成，但不希望將其發佈到生成儲存，則可以禁用發佈它們，這可能會縮短管道運行持續時間。

必須通過項目添加以下禁用發佈調度程式包的配置 `pom.xml` 的子菜單。 它基於環境變數，該變數用作可以在Cloud Manager生成容器中設定的標誌，以定義何時應忽略調度程式包。

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
