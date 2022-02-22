---
title: 編輯程式
description: 瞭解如何編輯您的生產程式和沙盒程式，以在您建立它們後調整其選項。
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# 編輯程式 {#editing-programs}

具有必需權限的用戶可以編輯 [在您的組織中建立的生產程式](creating-production-programs.md) 以及 [在您的組織中建立的沙盒程式。](creating-sandbox-programs.md) 通過編輯程式，您可以：

* 將站點解決方案添加到具有資產的現有計畫，反之亦然。
* 從具有站點和資產的現有程式中刪除站點或資產。
* 將第二個未使用的解決方案權利添加到現有程式或作為新程式。
* 刪除沙盒程式。

>[!NOTE]
>
>您必須是 **業務所有者** 用於編輯程式或刪除沙盒程式的角色。

按照以下步驟編輯程式。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要編輯的程式以顯示其詳細資訊。

1. 按一下頁面左上角的程式名稱，然後選擇 **編輯程式**。

   ![編輯程式選項](assets/edit-program-overview.png)

1. 的 **編輯程式** 頁面顯示兩個頁籤： **常規** 和 **解決方案和附加模組**。 選擇 **常規** 頁籤。

   * 必須為程式至少選擇一個解決方案。

   ![常規頁籤](assets/edit-program-prod1.png)

1. 選擇 **解決方案和附加模組** 頁籤

   ![選擇解決方案](assets/edit-prg.png)

1. 按一下解決方案名稱前的雪佛龍，以顯示可選的附加項，如 **商業** 載入項選項 **站點**。

   ![編輯載入項](assets/edit-program-add-on.png)

1. 按一下 **更新** 以保存對程式所做的更改。

更新完成後，如果選定的解決方案已更改，則這些更改將在下次部署後生效。

## 刪除沙盒程式 {#delete-sandbox-program}

刪除沙盒程式將刪除與其關聯的所有環境和管道。

>[!TIP]
>
>具有 **業務所有者** 或 **部署管理器** 角色也可以刪除其生產環境和階段環境，而不是整個沙盒程式。

按照以下步驟刪除沙盒程式。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要編輯的程式以顯示其詳細資訊。

1. 按一下頁面左上角的程式名稱，然後選擇 **刪除程式**。

   ![刪除程式選項](assets/delete-sandbox1.png)

或者，您也可以從Cloud Manager概述頁面按一下程式卡上的省略號按鈕，然後選擇 **刪除程式**。

![從程式卡中刪除沙盒](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能刪除沙盒程式。 無法刪除生產程式。