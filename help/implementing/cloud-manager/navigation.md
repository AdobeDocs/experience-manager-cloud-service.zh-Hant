---
title: 瀏覽Cloud Manager UI
description: 瞭解Cloud Manager UI的組織方式以及如何導覽以管理您的程式和環境。
source-git-commit: a0f80a363cb47be9e3d8f7fa96ea3068eb077d42
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 6%

---


# 瀏覽Cloud Manger UI {#navigation}

瞭解Cloud Manager UI的組織方式以及如何導覽以管理您的程式和環境。

Cloud Manage UI主要由兩個圖形介面組成：

* [我的程式控制檯](#my-programs) 您可以在此檢視和管理所有程式。
* [計畫總覽視窗](#program-overview) 在這裡，您可以檢視詳細資訊並管理個別計畫。

>[!TIP]
>
>另請檢視 [入門檔案歷程](/help/journey-onboarding/overview.md) 有關如何使用Cloud Manager啟動和執行AEMas a Cloud Service的完整概觀。

## 我的程式主控台 {#my-programs}

當您在登入Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織，您即會到達 **我的計畫** 主控台。

![我的程式主控台](assets/my-programs-console.png)

「我的程式」主控台提供在選取組織中您有權存取的所有程式的概觀。 它由幾個部分組成。

1. [工具列](#toolbars-my-programs-toolbars) 組織選擇、警示和帳戶設定
1. [統計資料和行動號召](#statistics) 以取得您最近活動的概覽
1. [程式與授權](#programs-license) 瞭解您目前的授權狀態並管理您的程式
1. [快速連結](#quick-links) 以輕鬆存取相關資源

>[!TIP]
>
>請參閱檔案 [程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 以取得有關計畫的詳細資訊。

### 工具列 {#my-programs-toolbars}

兩個工具列彼此位於頂端。

#### Cloud Manager標題 {#cloud-manager-header}

第一個是Cloud Manager標題，會在您導覽Cloud Manager時持續保留。 這是一個錨點，可讓您存取套用至Cloud Manager程式的設定和資訊。

![Experience Cloud 標頭](assets/experience-cloud-header.png)

1. 無論您在Cloud Manager中的哪個位置，此Cloud Manager按鈕都會將您帶回Cloud Manager的「我的程式」主控台。
1. 點選或按一下「意見回饋」按鈕，向Adobe提供有關Cloud Manager的意見回饋。
1. 組織選擇器會顯示您目前登入的組織（在此範例中為Foundation Internal）。 如果您的 Adobe ID 與多個組織關聯，可點選或按一下以切換到另一個組織。
1. 點選或按一下解決方案切換器可讓您快速跳轉到其他 Experience Cloud 解決方案。
1. 說明圖示可快速存取學習和支援資源。
1. 通知圖示會出現標籤，顯示目前未完成指派的數量 [通知。](/help/implementing/cloud-manager/notifications.md)
1. 選取代表您的使用者的圖示，以存取您的使用者設定。 如果您沒有設定使用者圖片，則會隨機分配圖示。

#### 程式工具列 {#program-toolbar}

程式工具列提供了在Cloud Manager程式和適合上下文的動作之間切換的連結。

![程式工具列](assets/program-toolbar.png)

1. 方案選擇器會開啟一個下拉式清單，您可以在其中快速選取其他方案或採取適合上下文的動作，例如建立新方案
1. 快速入門連結可讓您存取 [入門檔案歷程](/help/journey-onboarding/overview.md) 以讓您啟動並執行Cloud Manager。
1. 動作按鈕提供適合上下文的動作，例如建立新方案。

### 統計資料 {#statistics}

統計資料區段提供您組織的彙總資料，例如，如果您成功設定方案，可能會顯示過去90天的活動統計資料，包括：

* 數量 [部署](/help/implementing/cloud-manager/deploy-code.md)
* 數量 [程式碼品質問題](/help/implementing/cloud-manager/code-quality-testing.md) 已識別
* 組建數目

或者，如果您正開始進行組織的設定，可能會有後續步驟或檔案資源的提示。

### 程式與授權 {#programs-license}

「我的程式」主控台的主要內容是程式清單和授權狀態。

#### 程式標籤 {#programs}

此 **計畫** 標籤會列出代表您有權存取之每個程式的卡片。 點選或按一下卡片以存取 **計畫總覽** 計畫的頁面，以取得計畫的詳細資訊。

使用排序選項以更好地尋找您需要的程式。

![排序選項](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序依據
   * 建立日期（預設）
   * 程式名稱
   * 狀態
* 遞增（預設） /遞減
* 格點檢視（預設）
* 清單檢視

每個方案由卡片（或表格中的列）表示，提供方案的概覽和採取行動的快速連結。

![程式卡](assets/program-card.png)

* 程式影像（如果已設定）
* 程式名稱
* 服務型別： **Experience Manager雲端** 針對AEM as a *Cloud Service計畫或 [**Experience Manager** 用於AMS程式](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [計畫型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：沙箱或生產
* 狀態
* 設定的解決方案
* 建立日期

根據建立計畫時選擇的選項，生產計畫可能會有顯示其他功能的徽章。

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA徽章](assets/hipaa.png)

* [WAF-DDOS保護](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![waf-DDOS徽章](assets/waf-ddos-protection.png)

* [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99.99% SLA徽章](assets/9999-sla.png)

此資訊圖示也可讓您快速存取關於方案的其他資訊（在清單檢視中很有用）。

![資訊](assets/information-list-view.png)

省略符號圖示可讓您存取可以對方案執行的其他動作。

![方案的省略符號按鈕](assets/program-ellipsis.png)

* 導覽至特定 [環境](/help/implementing/cloud-manager/manage-environments.md) 計畫的
* 開啟 [計畫總覽](#program-overview)
* [編輯方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [刪除沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>如需有關計畫以及建立和管理計畫的詳細資訊，請參閱以下檔案。
>
>* [程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### 授權標籤 {#license-tab}

此 **授權** 索引標籤可讓您快速存取 [授權儀表板。](/help/implementing/cloud-manager/license-dashboard.md)

### 快速連結 {#quick-links}

快速連結區段可讓您存取常用的相關資源。

## 計畫總覽視窗 {#program-overview}

一旦您在「我的程式」控制檯中選擇了程式，您就會進入「程式總覽」。

![計畫概觀](assets/program-overview.png)

計畫概觀可讓您存取Cloud Manager計畫的所有詳細資訊。 就像「我的程式」主控台一樣，它由幾個部分組成。

1. [工具列](#program-overview-toolbar) 快速跳回「我的程式」控制檯並瀏覽程式
1. [索引標籤](#program-tabs) 在方案的不同方面之間切換
1. A [行動號召](#cta) 根據計畫的最後動作
1. 一個 [環境概觀](#environments) 計畫的
1. 一個 [管道概觀](#pipelines) 計畫的
1. 一個 [績效概觀](#performance) 計畫的
1. 連結至 [有用的資源](#useful-resources)

### 工具列 {#program-overview-toolbar}

計畫總覽的工具列與 [我的程式主控台。](#my-programs-toolbars) 此處僅說明差異。

#### Cloud Manager標題 {#cloud-manager-header-2}

Cloud Manager標題有一個漢堡選單，會自動開啟以顯示計畫概覽的可導覽標籤。

![Cloud Manager漢堡功能表](assets/cloud-manager-hamburger.png)

點選或按一下漢堡選單圖示，以隱藏標籤。

#### 程式工具列 {#program-toolbar-2}

程式工具列仍可讓您快速切換到其他程式，但也可存取與內容相關的動作，例如新增和編輯程式。

![程式工具列](assets/cloud-manager-program-toolbar.png)

此外，如果您選擇使用漢堡選單隱藏標籤，則工具列始終提供您所在的標籤。

### 計畫標籤 {#program-tabs}

每個方案都有許多相關的選項和資料。 這些資料會收集到索引標籤中，讓瀏覽程式更簡單。 標籤可讓您存取：

* 總覽 — 方案總覽，如目前檔案所述
* [活動](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)  — 計畫的管道執行歷史記錄
* [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)  — 為計畫設定的所有管道
* [存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)  — 為方案設定的所有存放庫
* [報表](/help/implementing/cloud-manager/sla-reporting.md) - SLA資料等量度
* [環境](/help/implementing/cloud-manager/manage-environments.md)  — 為計畫設定的所有環境
* [內容集](/help/implementing/developing/tools/content-copy.md)  — 為複製目的而建立的內容集
* [複製內容活動](/help/implementing/developing/tools/content-copy.md)  — 內容複製活動
* 學習路徑 — 有關Cloud Manager的其他學習資源

根據預設，當您開啟程式時，您會到達 **概觀** 標籤。 目前的標籤會反白顯示。 選取其他標籤以顯示其詳細資訊。

使用中的漢堡選單 [Cloud Manager標題](#cloud-manager-header-2) 以隱藏標籤。

### 行動號召 {#cta}

號召性用語區段會根據您的方案狀態，提供您有用的資訊。 若為新計畫，您可能會看到後續步驟以及上線日期提醒， [在建立程式期間設定。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新方案的行動號召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

對於即時計畫，您上次部署的狀態，包含詳細資訊的連結和開始新的部署。

![行動號召](/help/implementing/cloud-manager/assets/info-banner.png)

### 環境卡 {#environments}

此 **環境** 卡片會提供您環境的概觀，以及快速動作的連結。

新環境列在&#x200B;**環境**&#x200B;卡只會列出三個環境。按一下 **全部顯示** 檢視計畫的所有環境。

請參閱檔案 [管理環境](/help/implementing/cloud-manager/manage-environments.md) 有關如何管理環境的詳細資訊。

### 管道卡 {#pipelines}

此 **管道** 卡片會提供管道的概觀，以及快速動作的連結。

此 **管道** 卡片僅列出三個管道。 按一下 **全部顯示** 檢視計畫的所有管道。

請參閱檔案 [管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) 有關如何管理管道的詳細資訊。

### 效能卡 {#performance}

此 **效能** 卡片提供 **[CDN控制面板。](/help/implementing/cloud-manager/cdn-performance.md)**

![效能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 實用資源 {#useful-resources}

此 **有用的資源** 區段提供Cloud Manager其他學習資源的連結。
