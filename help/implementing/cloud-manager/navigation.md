---
title: 導覽 Cloud Manager UI
description: 了解 Cloud Manager UI 的組織方式以及如何導覽以管理您的方案和環境。
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 76%

---


# 導覽 Cloud Manager UI {#navigation}

了解 Cloud Manager UI 的組織方式以及如何導覽以管理您的方案和環境。

Cloud Manager UI 主要由兩個圖形介面組成：

* [「我的程式」控制台](#my-programs-console)，您可以在其中檢視和管理所有程式。
* [「程式概觀」視窗](#program-overview)，您可以在其中管理個別程式並查看詳細資訊。

>[!TIP]
>
>另請檢視[上線檔案歷程](/help/journey-onboarding/overview.md)，以全面瞭解如何使用Cloud Manager快速上手AEM as a Cloud Service。

## 我的程式控制台 {#my-programs-console}

當您透過 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織時，您將看到「**我的程式**」控制台。

![我的方案控制台](assets/my-programs-console.png)

「我的方案」控制台提供您在所選組織中有權存取之所有方案的概觀。它由幾個部分組成。

1. [工具列](#toolbars-my-programs-toolbars)：提供組織選擇、警示和帳戶設定
1. 標籤：可讓您切換程式的目前檢視。
   * **首頁**&#x200B;檢視 (預設)：選取了「**我的程式**」檢視，其中包含所有程式的概觀
   * 存取[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)的&#x200B;**授權**。
   * 請注意，標籤預設為關閉狀態，可使用 [Cloud Manager 標頭](#cloud-manager-header)中的漢堡選單來顯示。
1. [統計資料和行動號召](#statistics)，提供您最近的活動概觀
1. [**我的程式**&#x200B;部份](#my-programs-section)：包含您所有程式的概觀
1. [快速連結](#quick-links-section)：用於輕鬆存取相關資源

>[!TIP]
>
>有關程式的詳細資訊，請參閱文件：[程式和程式類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

### 工具列 {#my-programs-toolbars}

有兩個相互重疊的工具列。

#### Cloud Manager 標頭 {#cloud-manager-header}

第一個是 Cloud Manager 標頭，當您瀏覽 Cloud Manager 時會持續出現。它是一個錨點，可讓您存取適用於 Cloud Manager 程式的設定和資訊。

![Experience Cloud 標頭](assets/experience-cloud-header.png)

1. 漢堡功能表提供存取標籤，這些標籤可帶您進入個別計畫中的特定部分，或依據內容在[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)和&#x200B;**[我的程式](#my-programs-console)**&#x200B;主控台之間切換。
1. 無論您位於 Cloud Manager 中的哪個位置，Cloud Manager 按鈕都會將您帶回 Cloud Manager 的「我的程式」控制台。
1. 點選或按一下「意見回饋」按鈕，即可向 Adobe 提供有關 Cloud Manager 的意見回饋。
1. 組織選擇器會顯示您目前登入的組織 (在本例中為 Foundation Internal)。如果您的 Adobe ID 與多個組織關聯，可點選或按一下以切換到另一個組織。
1. 點選或按一下解決方案切換器可讓您快速跳轉到其他 Experience Cloud 解決方案。
1. 說明圖示可快速存取學習和支援資源。
1. 通知圖示具有目前指派的未完成[通知](/help/implementing/cloud-manager/notifications.md)數目。
1. 選取代表您使用者的圖示以存取您的使用者設定。如果您沒有設定使用者圖片，則會隨機分配圖示。

#### 程式工具列 {#program-toolbar}

程式工具列提供了在 Cloud Manager 程式與內容相關的動作之間切換的連結。

![方案工具列](assets/program-toolbar.png)

1. 程式選擇器將會開啟一個下拉式選單，您可以在其中快速選取其他程式或採取內容相關動作，例如建立新程式
1. 透過入門連結，您可以存取[上線文件歷程](/help/journey-onboarding/overview.md)以幫助您順利執行 Cloud Manager。
1. 動作按鈕提供內容相關動作，例如建立新方案。

### 統計資料與行動號召 {#statistics}

統計資料與號召性用語區段提供您組織的彙總資料，例如，如果您已成功設定方案，會顯示過去90天的活動統計資料，包括：

* [部署](/help/implementing/cloud-manager/deploy-code.md)數量
* 已識別的[程式碼品質問題](/help/implementing/cloud-manager/code-quality-testing.md)數量
* 組建數量

或者，如果您剛開始設定您的組織，可能會有關於後續步驟或文件資源的提示。

### 我的程式部份 {#my-programs-section}

**我的程式**&#x200B;主控台的主要內容是&#x200B;**我的程式**&#x200B;區段中的程式清單。

**我的程式**&#x200B;區段列出代表每個程式的卡片。 點選或按一下卡片即可存取該程式的「**程式概觀**」頁面，以了解有關該程式的詳細資訊。

>[!NOTE]
>
>視您的權限而定，您可能無法選取某些程式。

使用排序選項可以進一步找到您需要的程式。

![排序選項](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序依據
   * 建立日期 (預設)
   * 方案名稱
   * 狀態
* 升序 (預設) / 降序
* 格點檢視 (預設)
* 清單檢視

#### 程式卡片 {#program-cards}

每個程式都由一張卡片 (或表格中的列) 表示，提供該程式的概觀以及採取行動的快速連結。

![程式卡片](assets/program-card.png)

* 方案映像 (若已設定)
* 方案名稱
* 服務類型：
   * AEM as a Cloud Service程式的&#x200B;**Experience Manager雲端**
   * [AMS程式](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)的&#x200B;**Experience Manager**
* [程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：
   * 沙箱
   * 生產
* 狀態
* 設定的解決方案:
* 建立日期

根據建立計畫時選擇的選項，生產計畫可能會有顯示其他功能的徽章。

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA徽章](assets/hipaa.png)

* [WAF-DDOS保護](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![WAF-DDOS徽章](assets/waf-ddos-protection.png)

* [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99.99% SLA徽章](assets/9999-sla.png)

透過資訊圖示，還可以快速存取有關方案的其他資訊 (在清單檢視中很實用)。

![資訊](assets/information-list-view.png)

透過省略符號圖示，您可以存取可對程式執行的其他動作。

![程式的省略符號按鈕](assets/program-ellipsis.png)

* 瀏覽至方案的特定[環境](/help/implementing/cloud-manager/manage-environments.md)
* 開啟[方案概觀](#program-overview)
* [編輯方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [刪除沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>如需有關計畫以及建立和管理計畫的詳細資訊，請參閱以下檔案。
>
>* [程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [正在建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [正在建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

### 快速連結區段 {#quick-links-section}

透過快速連結部份，您可以存取常用的相關資源。

## 程式概觀視窗 {#program-overview}

一旦您在&#x200B;**[我的程式](#my-programs-console)**&#x200B;主控台中選取程式，就會進入&#x200B;**程式總覽**&#x200B;視窗。

![程式概觀](assets/program-overview.png)

透過程式概觀，您可以存取 Cloud Manager 程式的所有詳細資訊。與&#x200B;**我的程式**&#x200B;主控台類似，它由幾個部分組成。

1. [工具列](#program-overview-toolbar)可快速跳回「我的程式」控制台以及導覽程式
1. [索引標籤](#program-tabs)可在程式的不同方面之間切換
1. 根據程式最後動作的[行動號召](#cta) 
1. 程式的[環境概觀](#environments)
1. 程式的[管道概觀](#pipelines)
1. 程式效能](#performance)的[概觀
1. [實用資源](#useful-resources)的連結

### 工具列 {#program-overview-toolbar}

程式總覽的工具列與[我的程式主控台](#my-programs-toolbars)的工具列類似。 唯一的差別說明如下。

#### Cloud Manager 標頭 {#cloud-manager-header-2}

Cloud Manager 標頭有一個漢堡選單，會自動開啟以顯示程式概觀的可導覽索引標籤。

![Cloud Manager 漢堡選單](assets/cloud-manager-hamburger.png)

點選或按一下漢堡選單圖示即可隱藏索引標籤。

#### 程式工具列 {#program-toolbar-2}

程式工具列仍能讓您快速切換到其他程式，而且還可讓您執行內容相關動作，例如新增和編輯程式。

![程式工具列](assets/cloud-manager-program-toolbar.png)

此外，如果您選擇使用漢堡選單來隱藏索引標籤，工具列始終會提供您所在的索引標籤。

### 程式索引標籤 {#program-tabs}

每個程式都有許多與之相關的選項和資料。這些資料會收集到索引標籤中，以方便導覽程式。這些索引標籤可讓您存取：

* 概觀 - 目前文件中所述的方案概觀
* [活動](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - 方案的管道執行歷史記錄
* [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - 為方案設定的所有管道
* [存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - 為方案設定的所有存放庫
* [報告](/help/implementing/cloud-manager/sla-reporting.md) - SLA 資料等量度
* [環境](/help/implementing/cloud-manager/manage-environments.md) - 為方案設定的所有環境
* [網域設定](/help/implementing/cloud-manager/custom-domain-names/introduction.md) — 管理程式的自訂網域名稱
* [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) — 管理程式的SSL憑證
* [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) — 為特定IP位址定義允許清單
* [內容集](/help/implementing/developing/tools/content-copy.md) - 為複製目的而建立的內容集合
* [複製內容活動](/help/implementing/developing/tools/content-copy.md) - 內容複製活動
* [網路基礎結構](/help/security/configuring-advanced-networking.md) — 管理程式的進階網路選項
* 學習路徑 - 有關 Cloud Manager 的其他學習資源

預設情況下，當您開啟方案時，您會到達「**概觀**」索引標籤。會醒目提示目前的索引標籤。選取另一個索引標籤即可顯示其詳細資訊。

使用 [Cloud Manager 標頭](#cloud-manager-header-2)中的漢堡選單即可隱藏索引標籤。

### 行動號召 {#cta}

行動號召部份將根據您的程式狀態為您提供有用的資訊。若是新計畫，您可能會看到提供的後續步驟以及上線日期提醒，[於計畫建立期間設定](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。

新程式的![呼叫動作](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

對於即時方案，會看到上次部署的狀態以及詳細資訊和開始新部署的連結。

![行動號召](/help/implementing/cloud-manager/assets/info-banner.png)

### 環境卡片 {#environments}

「**環境**」卡片為您提供環境的概觀以及快速動作的連結。

「**環境**」卡片只會列出三個環境。按一下「**全部顯示**」按鈕即可查看程式的所有環境。

請參閱文件：[管理環境](/help/implementing/cloud-manager/manage-environments.md)，了解有關如何管理環境的詳細資訊。

### 管道卡片 {#pipelines}

「**管道**」卡片為您提供管道的概觀以及快速動作的連結。

「**管道**」卡片只列出了三個管道。按一下「**全部顯示**」按鈕即可查看程式的所有管道。

請參閱文件：[管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，了解有關如何管理管道的詳細資訊。

### 效能卡 {#performance}

**效能**&#x200B;卡提供&#x200B;**[CDN儀表板](/help/implementing/cloud-manager/cdn-performance.md)**&#x200B;的概觀。

![效能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 實用資源 {#useful-resources}

「**實用資源**」部份提供了 Cloud Manager 的其他學習資源的連結。
