---
title: 編輯計畫
description: 了解如何編輯您的生產和沙箱計畫，以在建立計畫後調整其選項。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 401f853b197e67a6c54e4bf168081dc8165bd505
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 53%

---


# 編輯計畫 {#editing-programs}

若要管理和編輯程式，請從 [**我的計畫** 主控台。](/help/implementing/cloud-manager/navigation.md) 此 **我的計畫** 頁面提供您有權存取之所有程式的概觀。 選取個別方案時， **計畫總覽** 頁面提供一目瞭然的方案詳細資訊。

從 **計畫總覽**，具有必要許可權的使用者可以編輯 [在您的組織中建立的生產計畫](creating-production-programs.md) 和 [在您的組織中建立的沙箱計畫。](creating-sandbox-programs.md)透過編輯計畫，您可以：

* 將 Sites 解決方案新增到有 Assets 現有方案中，反之亦然。
* 從包含 Sites 和 Assets 的現有計畫中移除 Sites 或 Assets。
* 將第二個未使用的解決方案權利新增到現有計畫，或作為新計畫。
* 刪除沙箱計畫。

## 權限 {#permissions}

您必須是 **企業所有者** 編輯計畫或刪除沙箱計畫以及存取授權儀表板的角色。

## 編輯方案 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](#my-programs)** 頁面上，按一下您要編輯的方案以顯示其詳細資訊。

1. 按一下頁面左上角的計畫名稱，然後選擇&#x200B;**編輯計畫**。

   ![編輯計畫選項](assets/edit-program-overview.png)

1. 此 **編輯計畫** 頁面開啟至 **一般** 標籤。

   ![「一般」索引標籤](assets/edit-program-prod1.png)

1. 可用於編輯方案的選項與建立方案時的選項相同。
   * 請參閱檔案 [建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 和 [建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 個別選項的詳細資訊。
   * [其他選項](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) 根據您組織的權益，生產計畫可能適合使用。

1. 按一下「**更新**」，儲存計畫的變更。

將會儲存對計畫的變更。

>[!NOTE]
>
>只要編輯計畫 (包括新增或移除解決方案或附加元件)，這些變更就會在下次部署後生效。

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
