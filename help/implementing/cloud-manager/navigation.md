---
title: 導覽Cloud Manager UI
description: 了解 Cloud Manager UI 的組織方式以及如何導覽此 UI 來管理您的方案和環境。
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4c42888af1e846c011242af2c328e553bb811cfd
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 38%

---


# 導覽Cloud Manager UI {#navigation}

了解 Cloud Manager UI 的組織方式以及如何導覽以管理您的方案和環境。


Cloud Manager UI 主要由兩個圖形介面組成：

* [「我的方案」控制台](#my-programs-console)，您可以在其中檢視和管理所有方案。
* [「方案概觀」視窗](#program-overview)，您可以在其中管理個別方案並查看詳細資訊。

>[!TIP]
>
>另請檢視[上線檔案歷程](/help/journey-onboarding/overview.md)，以全面瞭解如何使用Cloud Manager快速上手AEM as a Cloud Service。


## AEM中的AI助理

對於具有[已完成必要條件](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)的客戶，其組織的使用者可以使用AEM中的AI助理。 檢視AEM[中的](/help/implementing/cloud-manager/ai-assistant-in-aem.md)AI小幫手。


## 我的程式控制台 {#my-programs-console}

當您透過 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織時，您將看到「**我的程式**」控制台。

![我的方案控制台](assets/my-programs-console.png)

「我的方案」控制台提供您在所選組織中有權存取之所有方案的概觀。它由幾個部分組成。

1. [工具列](#toolbars-my-programs-toolbars)：提供組織選擇、警示和帳戶設定
1. 標籤，讓您切換方案的目前視圖。
   * **首頁**&#x200B;檢視 (預設)：選取了「**我的程式**」檢視，其中包含所有程式的概觀
   * 存取&#x200B;**授權儀表板**&#x200B;的[授權](/help/implementing/cloud-manager/license-dashboard.md)。
   * 請注意，索引標籤預設為關閉，並可使用![Cloud Manager標題](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)中的[顯示功能表圖示](#cloud-manager-header)來顯示。
1. [統計資料和行動號召](#statistics)，提供您最近的活動概觀
1. [**我的方案**&#x200B;部份](#my-programs-section)：包含您所有方案的概觀
1. [快速連結](#quick-links-section)可輕鬆存取相關資源。

>[!TIP]
>
>如需更多方案的詳細資料，請參閱「[方案和方案類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)」。

### 工具列 {#my-programs-toolbars}

有兩個相互重疊的工具列。

#### Cloud Manager 標頭 {#cloud-manager-header}

第一個是 Cloud Manager 標頭，當您瀏覽 Cloud Manager 時會持續出現。它是一個錨點，可讓您存取適用於 Cloud Manager 程式的設定和資訊。

![Experience Cloud 標頭](assets/experience-cloud-header.png)

1. 按一下「![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)」（顯示或隱藏側邊功能表）可讓您存取各種標籤，這些標籤可帶您進入個別程式的特定部分。 或者，您可以根據內容在[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)和&#x200B;**[我的程式](#my-programs-console)**&#x200B;主控台之間切換。
1. 按一下Adobe Cloud Manager按鈕，無論您身在Cloud Manager何處，都會帶您返回Cloud Manager的「我的程式」主控台。
1. 按一下「**意見回饋**」，即可向 Adobe 提供有關 Cloud Manager 的意見回饋。
1. 按一下組織選擇器，會顯示您目前登入的組織（在此範例中為Foundation Internal）。 如果您的 Adobe ID 與多個組織關聯，可按一下以切換到另一個組織。
1. 按一下![應用程式圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) （解決方案切換器）以快速跳至其他Experience Cloud解決方案。
1. 按一下![說明圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Help_18_N.svg)，讓您快速存取學習與支援資源。
1. 按一下![鈴鐺圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) （[通知](/help/implementing/cloud-manager/notifications.md)）檢視通知和公告等。
1. 按一下代表使用者對您的使用者設定之存取權的圖示。 如果您沒有設定使用者圖片，則會隨機分配圖示。

#### 方案工具列 {#program-toolbar}

方案工具列提供了在 Cloud Manager 方案與內容相關的動作之間切換的連結。

![方案工具列](assets/program-toolbar.png)

1. **我的程式**&#x200B;選擇器會開啟一個下拉式清單，您可以在此快速選取其他程式，或執行適合內容的動作，例如建立新程式
1. **快速入門**&#x200B;連結可讓您存取[入門檔案歷程](/help/journey-onboarding/overview.md)，以開始使用Cloud Manager。
1. 動作按鈕提供適合上下文的動作，例如新增方案。

### 統計資料和行動號召 {#statistics}

統計資料和call-to-action區段提供您組織的彙總資料，例如，如果您成功設定方案，會顯示過去90天的活動統計資料，包括：

* [部署](/help/implementing/cloud-manager/deploy-code.md)數量
* 已識別的[程式碼品質問題](/help/implementing/cloud-manager/code-quality-testing.md)數量
* 組建數量

或者，如果您剛開始設定您的組織，可能會有關於後續步驟或文件資源的提示。

### 我的方案區段 {#my-programs-section}

**我的程式**&#x200B;主控台的主要內容是&#x200B;**我的程式**&#x200B;區段中的程式清單。

**我的程式**&#x200B;區段列出代表每個程式的卡片。 按一下卡片即可存取該方案的「**方案概觀**」頁面，了解有關該方案的詳細資訊。

>[!NOTE]
>
>依您的權限而定，您可能無法選取某些方案。


若要更輕鬆找到所需的程式，請使用排序選項。

![排序選項](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序方式：
   * **建立日期** （預設）
   * **程式名稱**
   * **狀態**
* ![向下排序圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg)遞增（預設） / ![向上排序圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg)遞減
* ![傳統格線檢檢視示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg)格線檢視（預設）
* ![檢視清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)清單檢視

#### 方案卡片 {#program-cards}

卡片（或表格中的列）代表每個方案，提供方案概覽和採取行動的快速連結。

![方案卡片](assets/program-card.png)

* 和方案相關聯的影像（如果已設定）。 上圖為「WKND」。
* 指派給計畫的名稱。 上圖顯示「SecurBank Sample」為程式名稱。
* 服務類型：
   * **Experience Manager Cloud** — 適用於AEM as a Cloud Service計畫
   * **Experience Manager** — 適用於[AMS (Adobe Managed Services)方案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/introduction)
* [程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)：
   * 沙箱
   * 生產
* 狀態。 在上圖中，狀態為「就緒」並帶有核取標籤。
* 已設定的解決方案。 在上圖中，Sites和Assets是已設定的解決方案。
* 建立日期。

生產計畫可能會有徽章，以顯示您在新增計畫時選擇的其他功能，例如：

* ![HIPAA徽章](assets/hipaa.png) [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* ![WAF-DDOS徽章](assets/waf-ddos-protection.png) [WAF-DDOS保護](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* [99.99% SLA (Service level agreement)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

透過資訊圖示，還可以快速存取有關方案的其他資訊 (在清單檢視中很實用)。

![資訊](assets/information-list-view.png)

此![更多圖示](https://spectrum.adobe.com/static/icons/workflow_22/Smock_More_22_N.svg)圖示可讓您存取可以對方案執行的其他動作。

![方案的省略符號按鈕](assets/program-ellipsis.png)

* 瀏覽至程式的特定![資料圖示](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Data_22_N.svg) [環境](/help/implementing/cloud-manager/manage-environments.md)
* 開啟![計畫總覽圖示](/help/implementing/cloud-manager/assets/program-overview.svg) [計畫總覽](#program-overview)
* ![編輯圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) [編輯程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* ![刪除圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) [刪除沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>如需有關程式以及新增和管理程式的詳細資訊，請參閱下列內容：
>
>* [程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### 快速連結區段 {#quick-links-section}

快速連結區段可讓您存取相關的常用資源。

## 計畫總覽頁面 {#program-overview}

在&#x200B;**[我的計畫](#my-programs-console)**&#x200B;主控台中選取計畫時，您會進入&#x200B;**計畫總覽**&#x200B;頁面。

![程式概觀](assets/program-overview.png)

透過程式概觀，您可以存取 Cloud Manager 程式的所有詳細資訊。與&#x200B;**我的程式**&#x200B;主控台類似，它由幾個部分組成。

1. [工具列](#program-overview-toolbar)可快速跳回[我的程式]主控台，並導覽程式
1. [索引標籤](#program-tabs)可在程式的不同方面之間切換
1. 根據程式最後動作的[行動號召](#cta) 
1. 程式的[環境概觀](#environments)
1. 程式的[管道概觀](#pipelines)
1. 程式效能[的](#performance)概觀
1. [實用資源](#useful-resources)的連結

### 工具列 {#program-overview-toolbar}

程式總覽的工具列與[我的程式主控台](#my-programs-toolbars)的工具列類似。 此處圖解僅說明差異部分。

#### Cloud Manager 標頭 {#cloud-manager-header-2}

頁面的左上角為Adobe Cloud Manager標題。 您可以按一下![側功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)來顯示或隱藏標籤側功能表到軟體的其他區域。

![Cloud Manager側邊功能表](assets/cloud-manager-hamburger.png)

按一下Adobe Cloud Manager以返回首頁。

#### 方案工具列 {#program-toolbar-2}

方案工具列同樣能讓您快速切換到其他方案，而且還可讓您執行內容相關動作，例如新增和編輯方案。

![方案工具列](assets/cloud-manager-program-toolbar.png)

即使您已使用![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)隱藏標籤，工具列仍會顯示您目前所在的標籤。

### 方案標籤 {#program-tabs}

每個方案都有許多相關聯的選項和資料。這些選項和資料會收集到索引標籤中，好讓瀏覽程式更簡單。 這些索引標籤可讓您存取：

**程式**

* ![現代格線檢檢視示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg)概觀 — 目前檔案中說明的方案概觀
* ![鈴鐺圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) [活動](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) — 計畫的管道執行歷程記錄
* ![工作流程圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) [管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) — 為方案設定的所有管道
* ![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) [存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md) — 為方案設定的所有存放庫
* ![圖形圓形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg) [報表](/help/implementing/cloud-manager/sla-reporting.md) - SLA資料之類的量度

**服務**

* ![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) [環境](/help/implementing/cloud-manager/manage-environments.md) — 針對此程式設定的所有環境
* ![網頁圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) — 管理Edge Delivery網站
* ![設定圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) [網域設定](/help/implementing/cloud-manager/custom-domain-names/introduction.md) — 管理程式的自訂網域名稱
* ![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) — 管理程式的SSL憑證
* ![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) [網域對應](/help/implementing/cloud-manager/custom-domain-names/introduction.md) — 管理網域對應
* ![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) — 為特定IP位址定義允許清單
* ![方塊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) [內容集](/help/implementing/developing/tools/content-copy.md) — 為複製目的建立的內容集
* ![歷程圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) [複製內容活動](/help/implementing/developing/tools/content-copy.md) — 內容複製活動
* ![頻道圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg) [網路基礎結構](/help/security/configuring-advanced-networking.md) — 管理程式的進階網路選項

**資源**

* ![書籍圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Book_18_N.svg)學習路徑 — 有關Cloud Manager的其他學習資源

預設情況下，當您開啟方案時，您會到達「**概觀**」索引標籤。會醒目提示目前的索引標籤。選取另一個索引標籤即可顯示其詳細資訊。

在[Cloud Manager標題](#cloud-manager-header-2)的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示或隱藏標籤的側邊功能表。

### 行動號召 {#cta}

行動號召區段會根據您的方案狀態為您提供有用的資訊。若是新程式，您可能會看到指定的後續步驟以及上線日期提醒，[設定於程式建立期間](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。

新程式的![Call-to-action](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

對於即時方案，會看到上次部署的狀態以及詳細資訊和開始新部署的連結。

![行動號召](/help/implementing/cloud-manager/assets/info-banner.png)

### 環境卡片 {#environments}

「**環境**」卡片為您提供環境的概觀和快速動作的連結。

「**環境**」卡片只會列出三個環境。按一下![工作流程圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **全部顯示**&#x200B;以檢視計畫的所有環境。

另請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md)。

### 管道資訊卡 {#pipelines}

「**管道**」卡片為您提供管道的概觀和快速動作的連結。

「**管道**」卡片只列出了三個管道。按一下![工作流程圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **全部顯示**&#x200B;以檢視方案的所有管道。

如需有關如何管理管道的詳細資訊，另請參閱[管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)。

### 效能卡 {#performance}

**效能**&#x200B;卡提供&#x200B;**[CDN儀表板](/help/implementing/cloud-manager/cdn-performance.md)**&#x200B;的概觀。

![效能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 實用資源 {#useful-resources}

「**實用資源**」部份提供了 Cloud Manager 的其他學習資源的連結。
