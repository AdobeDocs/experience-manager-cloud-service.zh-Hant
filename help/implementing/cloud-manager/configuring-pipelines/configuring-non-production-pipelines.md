---
title: 配置非生產管道
description: 瞭解如何配置非生產管道以在部署到生產環境之前test代碼的質量。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---

# 配置非生產管道 {#configuring-non-production-pipelines}

瞭解如何配置非生產管道以在部署到生產環境之前test代碼的質量。

## 非生產管道 {#non-production-pipelines}

除 [生產管道](#configuring-production-pipelines.md) 通過部署到交叉和生產環境，您還可以設定非生產管道來驗證代碼。

非生產管道有兩種類型：

* **代碼質量管道**  — 這些運行代碼質量掃描git分支中的代碼，並執行生成和代碼質量步驟。
* **部署管道**  — 除了執行生成和代碼質量步驟（如代碼質量管道）外，這些管道還將代碼部署到非生產環境。

>[!NOTE]
>
>你可以 [編輯管線設定](managing-pipelines.md) 在初始設定後。

## 添加新的非生產管道 {#adding-non-production-pipeline}

一旦您設定了程式並且使用Cloud Manager UI至少擁有一個環境，您就可以通過執行以下步驟來添加非生產管道。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 訪問 **管線** 從Cloud Manager主螢幕獲取卡。 按一下 **+添加** 選擇 **添加非生產管道**。

   ![添加非生產管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **配置** 頁籤 **添加非生產管道** 對話框，選擇要添加的非生產管線類型 **代碼質量管道** 或 **部署管道**。

   ![「添加非生產管道」對話框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生產管道名稱** 以標識管線以及以下附加資訊。

   * **部署觸發器**  — 定義部署觸發器以啟動管線時，有以下選項。

      * **手動**  — 使用此選項手動啟動管線。
      * **Git更改**  — 只要將提交添加到配置的git分支中，此選項就啟動CI/CD管道。 使用此選項，您仍可根據需要手動啟動管線。

1. 按一下 **繼續**。

1. 在 **原始碼** 頁籤 **添加非生產管道** 對話框，必須選擇管道應處理的代碼類型。

   * **[前端代碼](#front-end-code)**
   * **[完整堆棧代碼](#full-stack-code)**
   * **[Web層配置](#web-tier-config)**

完成非生產管線建立的步驟取決於 **原始碼** 的上界。 按照上面的連結跳轉到本文檔的下一部分，以完成管線的配置。

### 前端代碼 {#front-end-code}

前端代碼管道部署包含一個或多個客戶端UI應用程式的前端代碼生成。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 的子菜單。

要完成前端代碼非生產流水線的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **合格的部署環境**  — 如果管道是部署管道，則必須選擇它應部署到的環境。
   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。

   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
   * **代碼位置**  — 此選項定義選定回購的分支中的路徑，管道應從中檢索代碼。

   ![前端管線](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 按一下「**儲存**」。

管線已保存，現在可 [管理管道](managing-pipelines.md) 的 **管線** 卡 **計畫概述** 的子菜單。

### 完整堆棧代碼 {#full-stack-code}

全堆棧代碼管道同時部署包含一個或多個伺服器應用程式以及HTTPD/AEMDispatcher配置的後端和前端代碼生成。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 的子菜單。

>[!NOTE]
>
>如果所選環境已存在全堆棧代碼管道，則此選擇將被禁用。

要完成全堆棧代碼非生產流水線的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **合格的部署環境**  — 如果管道是部署管道，則必須選擇它應部署到的環境。
   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。

   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
   * **忽略Web層配置** -

   ![全堆棧管線](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 按一下「**儲存**」。

管線已保存，現在可 [管理管道](managing-pipelines.md) 的 **管線** 卡 **計畫概述** 的子菜單。

### Web層配置 {#web-tier-config}

Web層配置管道部署HTTPD/Dispatcher配置。 查看文檔 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 的子菜單。

>[!NOTE]
>
>如果所選環境已存在Web層代碼管道，則此選擇將被禁用。

要完成Web層代碼非生產管道的配置，請執行以下步驟。

1. 在 **原始碼** 頁籤。

   * **合格的部署環境**  — 如果管道是部署管道，則必須選擇它應部署到的環境。
   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。

   >[!TIP]
   > 
   >查看文檔 [添加和管理儲存庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

   * **Git分支**  — 此選項定義管線中應從哪個分支檢索代碼。
   * **代碼位置**  — 此選項定義選定回購的分支中的路徑，管道應從中檢索代碼。
      * 對於Web層配置管道，這通常是包含 `conf.d`。 `conf.dispatcher.d`, `opt-in` 的子菜單。
      * 例如，如果項目結構是從 [原型AEM計畫，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 那條路是 `/dispatcher/src`。

   ![Web層管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 按一下「**儲存**」。

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
