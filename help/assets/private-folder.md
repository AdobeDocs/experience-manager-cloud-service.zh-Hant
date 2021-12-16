---
title: 共用資產的私人資料夾
description: 了解如何在 [!DNL Adobe Experience Manager Assets] 並與其他使用者共用，並為其指派各種權限。
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
source-git-commit: ac8dc2a765aba5be45017cf4adbc8f64b20ff7f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 中的專用資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在 [!DNL Adobe Experience Manager Assets] 專供您使用的使用者介面。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如在資料夾內檢視資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個具有「所有者」角色的成員。
>
>若要建立私人資料夾，您需要 `Read` 和 `Modify` 對要建立私人資料夾的父資料夾的權限。 如果您不是管理員，預設不會為您啟用這些權限 `/content/dam`. 在此情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾。

## 建立和共用私人資料夾  {#create-share-private-folder}

要建立和共用私人資料夾：

1. 在 [!DNL Assets] 主控台，按一下 **[!UICONTROL 建立]** 按鈕，然後選擇 **[!UICONTROL 資料夾]** 的上界。

   ![建立資產資料夾](assets/create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入 `Title` 和 `Name` （選用）。

   選取 **[!UICONTROL 私人]** 核取方塊，按一下 **[!UICONTROL 建立]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   已建立私人資料夾。 您現在可以 [新增資產](add-assets.md#upload-assets) 與其他使用者或群組共用資料夾。 在您共用資料夾並為其指派權限之前，該資料夾不會顯示給任何其他使用者。

1. 要共用資料夾，請選擇資料夾，然後按一下 **[!UICONTROL 屬性]** 的上界。

1. 在 **[!UICONTROL 資料夾屬性]** 頁面，從 **[!UICONTROL 添加用戶]** 清單，指派角色(`Viewer`, `Editor`，或 `Owner`)，然後按一下 **[!UICONTROL 新增]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   您可以指派各種角色，例如 `Editor`, `Owner`，或 `Viewer` 共用資料夾的使用者。 若您指派 `Owner` 角色給使用者，使用者具有 `Editor` 資料夾的權限。 此外，使用者可與其他人共用資料夾。 若您指派 `Editor` 角色，則使用者可以編輯您私人資料夾中的資產。 如果您指派檢視器角色，使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾中至少有一個成員具有 `Owner` 角色。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。根據您指派的角色，當使用者登入時，系統會為使用者指派一組權限給您的私人資料夾 [!DNL Assets].
1. 按一下 **[!UICONTROL 確定]** 以關閉確認訊息。
1. 您與其共用資料夾的使用者在其使用者介面中會收到共用通知。

1. 按一下 [!UICONTROL 通知] 以開啟通知清單。

   ![通知](assets/notification-icon.png)

1. 按一下管理員共用的專用資料夾的條目以開啟該資料夾。

## 刪除私人資料夾 {#delete-private-folder}

您可以選取資料夾並選取「 」，以刪除資料夾 [!UICONTROL 刪除] 選項，或使用鍵盤上的空格鍵。

![「刪除」選項（在頂端功能表中）](assets/delete-option.png)

>[!CAUTION]
>
>如果您從CRXDE Lite中刪除私人資料夾，則存放庫中會保留多餘的使用者群組。

>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則也會刪除相關的使用者群組。
>
>不過，您可以使用從存放庫中移除現有的備援、未使用和自動產生的使用者群組 `clean` 方法（在Author例項中）`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
