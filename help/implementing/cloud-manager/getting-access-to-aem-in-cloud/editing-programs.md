---
title: 管理和編輯程式
description: 了解如何編輯您的生產和沙箱計畫，以在建立計畫後調整其選項。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 43%

---


# 管理和編輯程式 {#editing-programs}

此 **我的計畫** 頁面提供您有權存取之所有程式的概觀。 選取個別方案時， **計畫總覽** 頁面提供一目瞭然的方案詳細資訊。

從 **計畫總覽**，具有必要許可權的使用者可以編輯 [在您的組織中建立的生產計畫](creating-production-programs.md) 和 [在您的組織中建立的沙箱計畫。](creating-sandbox-programs.md)透過編輯計畫，您可以：

* 將 Sites 解決方案新增到有 Assets 現有方案中，反之亦然。
* 從包含 Sites 和 Assets 的現有計畫中移除 Sites 或 Assets。
* 將第二個未使用的解決方案權利新增到現有計畫，或作為新計畫。
* 刪除沙箱計畫。

## 權限 {#permissions}

您必須是 **企業所有者** 編輯計畫或刪除沙箱計畫以及存取授權儀表板的角色。

## 我的計畫 {#my-programs}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 此 **我的計畫** 頁面顯示您以圖磚方式存取的所有程式清單。

![我的程式頁面](/help/implementing/cloud-manager/assets/my-programs.png)

### 行動號召 {#cta}

頁面頂端是與組織狀態相關的行動號召。 例如，如果您已成功設定方案，您過去90天的活動統計資料可能會顯示，包括：

* 數量 [部署](/help/implementing/cloud-manager/deploy-code.md)
* 數量 [程式碼品質問題](/help/implementing/cloud-manager/code-quality-testing.md) 已識別
* 組建數目

或者，如果您正開始進行組織的設定，可能會有後續步驟或檔案資源的提示。

### 程式標籤 {#programs-tab}

此 **計畫** 標籤會列出代表您有權存取之每個程式的卡片。 點選或按一下卡片以存取 **計畫總覽** 計畫的頁面，以取得計畫的詳細資訊。

使用排序選項以更好地尋找您需要的程式。

![排序選項](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 排序方式
   * 建立日期（預設）
   * 計畫名稱
   * 狀態
* 遞增（預設） /遞減
* 格點檢視（預設）
* 清單檢視

### 授權標籤 {#license-tab}

此 **授權** 索引標籤可讓您快速存取 [授權儀表板。](/help/implementing/cloud-manager/license-dashboard.md)

## 計畫總覽 {#program-overview}

一旦您從 **[我的計畫](#my-programs)** 頁面，Cloud Manager會開啟 **計畫總覽** 所選方案的頁面。

![計畫總覽頁面](/help/implementing/cloud-manager/assets/program-overview.png)

點選或按一下頁面左上角的計畫名稱，以快速切換到另一個計畫或返回 **[我的計畫](#my-programs)** 頁面。 您也可以 [編輯選取的方案](#editing) 或 [新增程式。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

![計劃切換器](/help/implementing/cloud-manager/assets/program-switcher.png)

頂端的號召性用語會根據您的方案狀態，為您提供有用的資訊。 若為新計畫，您可能會看到後續步驟以及上線日期提醒， [在建立程式期間設定。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新方案的行動號召](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

對於即時計畫，您上次部署的狀態，包含詳細資訊的連結和開始新的部署。

![行動號召](/help/implementing/cloud-manager/assets/info-banner.png)

**環境** 和 **管道** 卡片可讓您快速概覽所選方案中的這兩者。

![卡片](/help/implementing/cloud-manager/assets/environments-pipelines.png)

此 **效能** 卡片提供 **[CDN控制面板。](/help/implementing/cloud-manager/cdn-performance.md)**

![效能卡](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

## 編輯方案 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](#my-programs)** 頁面上，按一下您要編輯的方案以顯示其詳細資訊。

1. 按一下頁面左上角的計畫名稱，然後選擇&#x200B;**編輯計畫**。

   ![編輯計畫選項](assets/edit-program-overview.png)

1. **編輯計畫**&#x200B;頁面隨即開啟。在&#x200B;**一般**&#x200B;索引標籤，編輯計畫名稱和描述。

   * 必須為計畫選擇至少一種解決方案。

   ![「一般」索引標籤](assets/edit-program-prod1.png)

1. 在&#x200B;**解決方案和附加元件**&#x200B;索引標籤，修改計畫的解決方案。

   ![選取解決方案](assets/edit-prg.png)

1. 按一下解決方案名稱前的 > 形圖示，即可顯示選用的附加元件，例如選擇&#x200B;**商務**&#x200B;下的附加選項 **Sites**。

   ![編輯附加元件](assets/edit-program-add-on.png)

1. 在&#x200B;**上線設定**&#x200B;索引標籤，修改計畫的上線日期。

   ![編輯上線設定](assets/edit-program-go-live.png)

   * 此日期僅供參考。這會觸發計劃概述頁面上的上線小工具。然後，小工具會提供至 Adobe Experience Manager (AEM) as a Cloud Service 最佳實務的產品內連結，以便貼近您的歷程進而為您帶來成功的上線體驗。
   * 沙箱計畫沒有此索引標籤。

1. 如果方案有所需的權益，則 **安全性** 標籤會顯示您可以在何處修改程式的安全性選項。

   ![編輯安全性設定](assets/edit-program-security.png)

   * HIPAA無法在之後啟用或停用 [程式建立。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [深入了解](https://www.adobe.com/go/hipaa-ready_tw) Adobe 的 HIPAA 就緒解決方案實作方式。
   * 一旦啟動，就可以設定WAF-DDOS保護 [非生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. 按一下「**更新**」，儲存計畫的變更。

只要編輯計畫 (包括新增或移除解決方案或附加元件)，這些變更就會在下次部署後生效。

## 刪除沙箱計畫 {#delete-sandbox-program}

刪除沙箱計畫會移除與其關聯的所有環境和管道。

>[!TIP]
>
>具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色也可以刪除其生產和中繼環境，而非整個沙箱計畫。

若要刪除沙箱計畫，請依照以下步驟進行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](#my-programs)** 頁面上，按一下您要編輯的方案以顯示其詳細資訊。

1. 按一下頁面左上角的計畫名稱，然後選擇 **刪除程式**.

   ![刪除計畫選項](assets/delete-sandbox1.png)

您也可以在 Cloud Manager 概觀頁面按一下計畫卡上的省略符號按鈕，然後選擇&#x200B;**刪除計畫**。

![從計畫卡中刪除沙箱](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能刪除沙箱計畫。不能刪除生產計畫。
