---
title: 編輯程式
description: 瞭解如何編輯您的生產程式和沙盒程式，以在您建立它們後調整其選項。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: d805ed744af0e5c95863a1c67439b384cc5d11b2
workflow-type: tm+mt
source-wordcount: '450'
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

1. 的 **編輯程式** 的上界。 在 **常規** 頁籤，編輯程式名稱和說明。

   * 必須為程式至少選擇一個解決方案。

   ![常規頁籤](assets/edit-program-prod1.png)

1. 在 **解決方案和附加模組** 頁籤。

   ![選擇解決方案](assets/edit-prg.png)

1. 按一下解決方案名稱前的雪佛龍，以顯示可選的附加項，如 **商業** 載入項選項 **站點**。

   ![編輯載入項](assets/edit-program-add-on.png)

1. 在 **轉到即時設定** 頁籤，修改程式的計畫上線日期。

   ![編輯即時設定](assets/edit-program-go-live.png)

   * 此日期僅供參考，並觸發程式概述頁面上的「開始使用」小部件，以及時提供到AEMas a Cloud Service最佳做法文檔的產品內連結，以與您的旅程保持一致，最終獲得成功且流暢的開始使用體驗。

1. 按一下 **更新** 以保存對程式所做的更改。

只要編輯程式（包括添加或刪除解決方案或載入項），這些更改將在下次部署後生效。

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
