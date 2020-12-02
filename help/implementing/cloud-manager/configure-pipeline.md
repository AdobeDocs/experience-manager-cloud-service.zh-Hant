---
title: 配置CI/CD管線——雲服務
description: 配置CI/CD管線——雲服務
translation-type: tm+mt
source-git-commit: 4d5ad99e44446ac40d9798df1c7fabb862065495
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# 設定 CI-CD 管線 {#configure-ci-cd-pipeline}

在Cloud Manager中，有兩種類型的管道：

* **生產管道**:

   只有建立生產和舞台環境集後，才可添加生產管線。

   有關詳細資訊，請參閱[設定生產管線](configure-pipeline.md#setting-up-the-pipeline)。

* **非生產管道**:

   從Cloud Manager的使用者介面的&#x200B;**概述**&#x200B;頁面新增非生產管道。

   如需詳細資訊，請參閱[非生產與程式碼品質專用管道](configure-pipeline.md#non-production-pipelines)。

>[!NOTE]
>要配置管線，您必須：
> * 定義將啟動管線的觸發器。
> * 定義控制生產部署的參數。
> * 配置效能測試參數。


## 設定生產管線{#setting-up-production-pipeline}

部署管理員負責設定生產管道。

>[!NOTE]
>在程式建立完成、Git儲存庫至少具有一個分支並且建立了「生產」和「階段」環境集之前，不能設定「生產管線」。

在開始部署代碼之前，您必須從[!UICONTROL 雲端管理器]配置管道設定。

>[!NOTE]
>
>可在初始設定後更改管線設定。

## 從[!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}配置管線設定

一旦您設定了程式，並且使用[!UICONTROL Cloud Manager] UI建立了至少一個環境，您就可以設定部署管道了。

請依照下列步驟來設定管道的行為和偏好設定：

1. 按一下「設定管線」(Setup Pipeline)「**」(&lt;a0/>)以設定和配置管線。**

   ![](assets/set-up-pipeline1.png)

1. 將顯示&#x200B;**設定管線**&#x200B;螢幕。 選擇分支並按一下&#x200B;**Next**。

   ![](assets/setup-1.png)

1. 設定您的部署選項。

   ![](assets/setup-2.png)

   可定義觸發器以啟動管線：

   * **手動** -使用UI手動啟動管線。
   * **On Git Changes** -每當有提交添加到配置的git分支時，啟動CI/CD管線。即使選取此選項，也始終可以手動啟動管線。

   在管線設定或編輯期間，「部署管理器」(Deployment Manager)可以選擇在任何質量門中遇到重要故障時定義管線的行為。

   這對希望實現更自動化流程的客戶非常有用。 可用的選項包括：

   * **每次詢問** -這是預設設定，需要手動干預任何重要故障。
   * **立即失敗** -如果選中此選項，當出現「重要」(Impertient)故障時，管線將被取消。這實際上是模擬使用者手動拒絕每個失敗。
   * **立即繼續** -如果選中此選項，當出現「重要」(Importent)故障時，管線將自動繼續。這實際上是在模擬用戶手動批准每個故障。


1. 生產管線設定包含標示為&#x200B;**體驗稽核**&#x200B;的第三個標籤。 此選項提供應一律包含在「體驗稽核」中的URL路徑表格。

   >[!NOTE]
   >您必須按一下「新增頁面&#x200B;**」來定義您自己的自訂連結。**

   ![](assets/setup-3.png)

   按一下「新增頁面」，提供要包含在「體驗稽核」中的URL路徑。****

   例如，如果您想要在「體驗稽核」中加入`https://wknd.site/us/en/about-us.html`，請在此欄位中輸入路徑`us/en/about-us.html`，然後按一下「儲存&#x200B;**」。**

   ![](assets/exp-audit4.png)

   表格中顯示的URL將是：

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   最多可包含25列。 如果使用者在此區段中未提交任何頁面，預設會將網站的首頁納入「體驗稽核」中。

   如需詳細資訊，請參閱[瞭解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md)。

   >[!NOTE]
   > 設定的頁面會提交至服務，並根據效能、協助工具、搜尋引擎最佳化(SEO)、最佳實務和PWA（漸進式網頁應用程式）測試進行評估。

1. 從&#x200B;**編輯管線**&#x200B;畫面按一下「儲存&#x200B;**a1/>」。****概述**&#x200B;頁面現在會顯示&#x200B;**部署您的Program**&#x200B;卡。 按一下&#x200B;**Deploy**&#x200B;按鈕以部署程式。

   ![](assets/configure-pipeline5.png)


## 僅限非生產和代碼質量管線{#non-production-pipelines}

除了部署到生產階段的主管道外，客戶還可以設定額外的管道，稱為&#x200B;**非生產管道**。 這些管線始終執行構建和代碼質量步驟。 他們也可以選擇性地部署至Adobe Managed Services環境。

在主螢幕上，新卡中列出了以下管線：

1. 從Cloud Manager主螢幕訪問&#x200B;**非生產管線**&#x200B;表徵圖。

   ![](assets/configure-pipeline6.png)

1. 按一下&#x200B;**添加**&#x200B;按鈕，以指定管線名稱、管線類型和Git分支。

   此外，還可以從Pipeline Options中設定部署觸發器和重要故障行為。

   ![](assets/non-prod-pipe1.png)

1. 按一下&#x200B;**Save** ，主螢幕上的卡上將顯示管線，其中有三個操作，如下所示：

   ![](assets/configure-pipeline8.png)

   * **編輯** -允許編輯管線設定
   * **Build**  —— 導航到執行頁，可從中執行管線
   * **Manage Git**  —— 允許用戶獲取訪問Cloud Manager Git儲存庫所需的資訊

## 後續步驟{#the-next-steps}

在設定管道後，您需要部署程式碼。

如需詳細資訊，請參閱[部署您的程式碼](deploy-code.md)。
