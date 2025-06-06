---
title: 新增專門的測試環境
description: 瞭解Cloud Manager中的專業測試環境如何提供專屬空間，在接近生產的條件下驗證功能，適用於壓力測試和進階部署前檢查。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期採用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: 815fb5c3-a171-4531-8727-b79183d85f06
source-git-commit: 58514d9f55eaaa35801380648831ad6d13cf1529
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 8%

---

# 新增專門的測試環境{#add-special-test-enviro}

>[!NOTE]
>
>>本文所述功能僅可透過早期採用計畫使用。 若要註冊為早期採用者，請參閱[專業測試環境](/help/implementing/cloud-manager/release-notes/current.md#specialized-test-environment)。

Specialized Testing Environment (DevXL)是您可以建立的新型Cloud Manager環境。 其設計可支援進階使用案例，例如使用者驗收測試(UAT)和效能驗證。 與傳統開發、快速開發或預備環境不同，DevXL環境會在生產部署管道之外操作。 因此，它們可為您提供更大的彈性，同時維持嚴格的隔離以防止干擾生產工作流程。

DevXL的建置可反映一般中繼環境的大小、擴充性和組態。 此方法可確保在DevXL中執行的測試產生逼真的深入分析，讓您瞭解程式碼和內容在類似生產的條件中如何執行。 此環境也支援從「生產」或「預備」直接複製內容。 此外，在部署工作流程、存取控制和網路設定方面，也能維持與開發環境的同位性。

## 主要功能與設定 {#key-features}

| 類別 | DevXL行為 |
| --- | --- |
| 用途 | UAT和效能測試。 |
| 管道類型 | 不在生產管道中。 |
| 環境大小 | 符合中繼環境。 |
| 隔離 | 與其他環境完全隔離。 |
| 程式碼管道 | 與開發環境相同（驗證、建置、部署）。 |
| 內容複製 | 允許來自生產或中繼環境。 |
| 內容還原 | 與開發環境相同。 |
| 存取記錄檔 | 與開發環境相同。 |
| Developer Console | 與開發環境相同。 |
| IP 允許清單 | 與開發環境相同。 |
| 網路 | 與開發環境相同（服務、網域名稱、SSL憑證、進階網路）。 |

另請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md)

## 新增專門的測試環境 {#add-specialized-testing-environment}

若要新增或編輯環境，使用者必須是&#x200B;**企業所有者**&#x200B;角色的成員。

**新增專門測試環境：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，按一下您要新增環境的程式。

1. 執行下列任一項作業：

   如果&#x200B;**新增環境**&#x200B;選項變暗（已停用），可能是因為缺少許可權或依賴授權的資源。

   * 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台的&#x200B;**環境**&#x200B;卡片上，按一下&#x200B;**新增環境**。

   ![環境卡](assets/no-environments.png)

   * 在左側面板上，按一下![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**，然後在「環境」頁面右上角附近，按一下&#x200B;**新增環境**。

     ![「環境」索引標籤](assets/environments-tab.png)

1. 在&#x200B;**新增環境**&#x200B;對話方塊中，執行下列動作：

   * 按一下&#x200B;**專業測試環境**。
   * 提供環境&#x200B;**名稱**。 建立環境後，便無法變更環境名稱。
   * （選用）提供環境的&#x200B;**描述**。
   * 從下拉式清單中選取&#x200B;**主要區域**。 建立後，DevXL環境的主要區域(例如&#x200B;*美國（西部）*)就會鎖定，無法變更。

   ![已選取「特殊化測試環境」選項按鈕的「新增環境」對話方塊](assets/specialized-test-environment.png)

1. 按一下「**儲存**」。

   **總覽**&#x200B;頁面現在會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。 現在您可以設定新環境的管道。
