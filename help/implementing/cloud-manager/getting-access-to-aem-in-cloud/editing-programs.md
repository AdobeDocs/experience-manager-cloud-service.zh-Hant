---
title: 編輯計畫
description: 了解如何編輯您的生產和沙箱計畫，以在建立計畫後調整其選項。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 89%

---

# 編輯計畫 {#editing-programs}

具有必要權限的使用者可以編輯[在您組織中建立的生產計畫](creating-production-programs.md)和[在您組織中建立的沙箱計畫。](creating-sandbox-programs.md)透過編輯計畫，您可以：

* 將 Sites 解決方案新增到有 Assets 現有方案中，反之亦然。
* 從包含 Sites 和 Assets 的現有計畫中移除 Sites 或 Assets。
* 將第二個未使用的解決方案權利新增到現有計畫，或作為新計畫。
* 刪除沙箱計畫。

## 權限 {#permissions}

您必須擁有&#x200B;**業務負責人**&#x200B;角色才能編輯計畫或刪除沙箱計畫。

## 編輯方案 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要編輯的計畫，顯示其詳細資訊。

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

   * HIPAA之後無法啟用或停用 [程式建立。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [深入了解](https://www.adobe.com/go/hipaa-ready_tw) Adobe 的 HIPAA 就緒解決方案實作方式。
   * 一旦啟動，就可以設定WAF-DDOS保護 [非生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

1. 按一下「**更新**」，儲存計畫的變更。

只要編輯計畫 (包括新增或移除解決方案或附加元件)，這些變更就會在下次部署後生效。

## 刪除沙箱計畫 {#delete-sandbox-program}

刪除沙箱計畫會移除與其關聯的所有環境和管道。

>[!TIP]
>
>具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色也可以刪除其生產和中繼環境，而非整個沙箱計畫。

若要刪除沙箱計畫，請依照以下步驟進行。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要編輯的計畫，顯示其詳細資訊。

1. 按一下頁面左上角的計畫名稱，然後選擇&#x200B;**刪除計畫**。

   ![刪除計畫選項](assets/delete-sandbox1.png)

您也可以在 Cloud Manager 概觀頁面按一下計畫卡上的省略符號按鈕，然後選擇&#x200B;**刪除計畫**。

![從計畫卡中刪除沙箱](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能刪除沙箱計畫。不能刪除生產計畫。
