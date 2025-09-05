---
title: 分割僅限階段和僅限生產的管道
description: 了解如何使用專用管道，分割中繼和生產部署。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
hide: true
hidefromtoc: true
index: false
source-git-commit: 24d78f19932a30026c0357db646124c9dd1fa759
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 49%

---

# 分割僅限階段和僅限生產的管道 {#stage-prod-only}

您可以使用專用管道來分割中繼和生產部署。

## 概觀 {#overview}

中繼環境和生產環境緊密耦合。依預設，其部署連結到單一管道。也就是同時部署到該方案中的中繼環境和生產環境的部署管道。雖然這種耦合通常是適當的，但對某些使用案例來說卻存在缺點：

* 如果您想部署到僅限中繼，您會拒絕管道中的「**提升至生產**」步驟。然而，該執行會被標記為已取消。
* 如果您想將中繼環境中的最新程式碼部署到生產環境中，則需要重新部署整個管道，包括中繼部署，即使其中的程式碼未變更。
* 部署期間無法更新環境。如果您於提升至生產前暫停流程，在中繼環境中測試幾天，則生產環境會維持鎖定狀態且無法更新。此情境會使無相依性的工作 (例如更新[環境變數](/help/implementing/cloud-manager/environment-variables.md)) 無法進行。

僅限中繼和僅限生產的管道透過提供專用部署選項為這些使用案例提供解決方案。

* **僅限中繼部署管道：**&#x200B;僅部署到中繼環境，在部署和測試完成後，執行即完成。僅限中繼管道的行為與標準耦合全端生產管道相同，但沒有生產部署步驟 (核准、排程、部署)。
* **僅限生產環境的部署管道：**&#x200B;僅透過選取最近成功的階段執行來部署到生產環境。 然後將其成品部署到生產中。僅限生產管道重複使用中繼部署成品，繞過建置階段。

當全端生產管道正在進行時，僅限中繼管道和僅限生產管道不會執行，反之亦然。如果僅限中繼和全端生產管道皆設定「**在 Git 變更時**」觸發程序，並且指向相同的分支與存放庫，則只有僅限中繼管道會自動啟動。僅限生產管道不會啟動 **`On Git Changes`**，因其沒有直接連結到存放庫。

僅限生產管道為手動觸發，因其沒有針對「**在 Git 變更時**」直接連結到存放庫。

這些專用管道提供更大的彈性，但請注意以下操作細節和建議。

>[!NOTE]
>
>僅限生產管道需始終使用僅限中繼管道中的成品。即使標準耦合生產管道同時部署了其他要中繼的內容，此流程仍然有效。
>
>* 這種情境可能會導致不必要的程式碼復原。
>* Adobe 建議在開始使用僅限生產和僅限中繼管道後，停止使用標準耦合生產管道。
>* 如果您仍然決定執行標準耦合管道和僅限中繼/僅限生產管道，請記住重複使用成品以避免程式碼回復。

## 管道建立 {#pipeline-creation}

僅限生產和僅限中繼管道的建立方式類似於標準耦合[生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。請參閱這些文件，以了解詳細資訊。

1. 在&#x200B;**管道**&#x200B;視窗中，按一下&#x200B;**新增管道**。

   * 選取&#x200B;**將非生產管道**&#x200B;新增至[建立僅限中繼的管道](#stage-only)。
   * 選取&#x200B;**將僅限生產管道**&#x200B;新增至[建立僅限生產管道](#prod-only)。

![建立僅限生產/中繼管道](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>如果對應的管道已存在，特定選項可能會呈現灰色。
>
>* 如果僅限中繼管道尚不存在，則&#x200B;**新增僅限生產管道**&#x200B;無法使用。
>* 如果標準耦合管道已存在，則&#x200B;**新增生產管道**&#x200B;無法使用。
>* 每個方案僅允許一個僅限生產管道和一個僅限中繼管道。

### 建立僅階段管道 {#stage-only}

1. 在&#x200B;**新增非生產管道**&#x200B;對話方塊的&#x200B;**組態**&#x200B;索引標籤上，為您的管道選取&#x200B;**部署管道**&#x200B;欄位。
1. 在「非生產管線名稱」欄位中，輸入任意文字的名稱。
1. 選取所需的部署選項，然後按一下[繼續]。**&#x200B;**

   在新增非生產管道對話方塊中的![設定索引標籤](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. 在&#x200B;**Source程式碼**&#x200B;索引標籤上，選取&#x200B;**完整棧疊程式碼**。 此選項會建置和部署整個AEM應用程式(後端、Dispatcher/Web層設定，以及存放庫中的任何前端模組)。

1. 在&#x200B;**合格的部署環境**&#x200B;下拉式清單中，選取&#x200B;**階段**&#x200B;環境作為您管道的部署環境。 選取階段會建立專用於階段環境的管道（生產升級會透過個別管道進行）。

1. 在各自的下拉式清單中選取您的&#x200B;**存放庫**&#x200B;和&#x200B;**Git分支**，然後按一下[繼續]&#x200B;**&#x200B;**。

   在新增非生產管道對話方塊中的![Source程式碼索引標籤](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. 在&#x200B;**體驗稽核**&#x200B;標籤上，指定的網站URL是Cloud Manager稽核頁面品質的發佈URL。

1. 在&#x200B;**頁面路徑**&#x200B;欄位中，指定要稽核的頁面，然後按一下&#x200B;**![新增圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)新增頁面**。

   體驗稽核會分析您新增的每個路徑，以檢查效能、協助工具、漸進式網頁應用程式、最佳實務、SEO和其他品質檢查。 您可以按一下![跨大小400圖示](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg)，新增多個路徑並移除任何路徑。

   在新增非生產管道對話方塊中的![體驗稽核索引標籤](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. 按一下「**儲存**」。


### 建立僅限生產環境的管線 {#prod-only}

1. 在&#x200B;**新增僅限生產的管道**&#x200B;對話方塊的&#x200B;**管道名稱**&#x200B;文字欄位中，輸入管道的自由文字名稱。
1. 在&#x200B;**管道名稱**&#x200B;欄位中，輸入您想要的名稱。
1. 在&#x200B;**生產部署選項**&#x200B;下，選取&#x200B;**在部署到生產之前暫停**。

   此選項會在生產步驟之前插入手動核准入口。 管道將停止並等待核准者（例如部署管理員或企業所有者）核准或取消生產部署。

   將此用於變更控制或最新檢查。

1. 按一下&#x200B;**儲存**&#x200B;以使用這些選項建立僅限生產的管道。

   ![建立僅限生產管道](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## 執行僅限階段和僅限生產環境的管道 {#running}

您可以像啟動任何其他管道[一樣啟動新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)。 您也可以直接從僅限中繼管道的執行詳細資訊觸發僅限生產管道。

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### 執行階段專用管道 {#stage-only-run}

在執行詳細資訊中，測試步驟之後會顯示&#x200B;**升級組建**&#x200B;按鈕。 按一下即可觸發僅限生產的管道，將此回合的階段成品部署至生產環境。 此按鈕只會在最近一次成功的僅階段執行中顯示。

![僅限中繼管道執行](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

當您按一下&#x200B;**升級組建**&#x200B;時，如果階段專用管道存在，則會開啟確認對話方塊以啟動它。 按一下&#x200B;**執行**。

![提升組建 — 執行管道對話方塊](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

如果不存在任何專案，安裝對話方塊會提示您建立一個。

![升級組建 — 沒有有效的管道對話方塊](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### 執行僅限生產環境的管道 {#prod-only-run}

對於&#x200B;**僅限生產環境**&#x200B;管道，Cloud Manager會顯示部署至生產環境的來源成品。 檢查來源執行的&#x200B;**成品準備**&#x200B;步驟，然後開啟它以檢視詳細資料和記錄。


![成品詳細資訊](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)

