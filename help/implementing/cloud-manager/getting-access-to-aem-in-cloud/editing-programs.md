---
title: 編輯方案
description: 了解如何編輯您的生產與沙箱方案，以在您建立方案後調整其選項。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: d805ed744af0e5c95863a1c67439b384cc5d11b2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 編輯方案 {#editing-programs}

具有必要權限的使用者可以編輯 [您組織中建立的生產程式](creating-production-programs.md) 和 [在貴組織中建立的沙箱方案。](creating-sandbox-programs.md) 通過編輯程式，您可以：

* 使用資產將Sites解決方案新增至現有計畫，反之亦然。
* 從同時具有Sites和Assets的現有程式中移除Sites或Assets。
* 將第二個未使用的解決方案權利添加到現有程式或作為新程式。
* 刪除沙箱方案。

>[!NOTE]
>
>您必須是 **業務負責人** 角色來編輯方案或刪除沙箱方案。

請依照下列步驟編輯方案。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下您要編輯的程式以顯示其詳細資訊。

1. 按一下頁面左上角的方案名稱，然後選取 **編輯程式**.

   ![編輯程式選項](assets/edit-program-overview.png)

1. 此 **編輯方案** 頁面開啟。 在 **一般** 頁簽，編輯程式名和說明。

   * 必須為程式至少選擇一個解決方案。

   ![「常規」頁簽](assets/edit-program-prod1.png)

1. 在 **解決方案和附加元件** 頁簽，修改程式的解決方案。

   ![選擇解決方案](assets/edit-prg.png)

1. 按一下解決方案名稱前的>形圖示，即可顯示選用的附加元件，例如選取 **商務** 下方的附加選項 **網站**.

   ![編輯附加元件](assets/edit-program-add-on.png)

1. 在 **前往即時設定** 頁簽，修改計畫的上線日期。

   ![編輯上線設定](assets/edit-program-go-live.png)

   * 此日期僅供參考，並會觸發計畫概述頁面上的上線介面工具集，即時提供產品內連結至AEMas a Cloud Service最佳實務檔案，以符合您的歷程，最終達成成功且順暢的上線體驗。

1. 按一下 **更新** 以保存對程式的更改。

只要編輯程式（包括新增或移除解決方案或附加元件），這些變更就會在下次部署後生效。

## 刪除沙箱方案 {#delete-sandbox-program}

刪除沙箱方案會移除與其相關聯的所有環境和管道。

>[!TIP]
>
>具有 **業務負責人** 或 **部署管理員** 角色也可以刪除其生產和預備環境，而非整個沙箱方案。

請依照下列步驟刪除沙箱方案。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下您要編輯的程式以顯示其詳細資訊。

1. 按一下頁面左上角的方案名稱，然後選取 **刪除程式**.

   ![刪除程式選項](assets/delete-sandbox1.png)

或者，您也可以從Cloud Manager概述頁面按一下程式卡上的刪節號按鈕，然後選取 **刪除程式**.

![從方案卡中刪除沙箱](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能刪除沙箱方案。 無法刪除生產程式。
