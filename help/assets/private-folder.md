---
title: 共用資產的專用資料夾
description: 瞭解如何在 [!DNL Adobe Experience Manager Assets] 與其他用戶共用，並為其分配各種權限。
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 中的專用資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在 [!DNL Adobe Experience Manager Assets] 只供您使用的用戶介面。 您可以將此專用資料夾共用給其他用戶，並為其分配各種權限。 根據您分配的權限級別，用戶可以對資料夾執行各種任務，例如查看資料夾內的資產或編輯資產。

>[!NOTE]
>
>專用資料夾至少有一個具有所有者角色的成員。
>
>要建立專用資料夾，您需要 `Read` 和 `Modify` 對建立專用資料夾的父資料夾的權限。 如果您不是管理員，則預設情況下在 `/content/dam`。 在這種情況下，首先獲取用戶ID/組的這些權限，然後嘗試建立專用資料夾。

## 建立和共用專用資料夾  {#create-share-private-folder}

要建立和共用私有資料夾，請執行以下操作：

1. 在 [!DNL Assets] 控制台，按一下 **[!UICONTROL 建立]** 按鈕，然後選擇 **[!UICONTROL 資料夾]** 的子菜單。

   ![建立資產資料夾](assets/create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入 `Title` 和 `Name` （可選）。

   選擇 **[!UICONTROL 私人]** 複選框，然後按一下 **[!UICONTROL 建立]**。

   ![chlimage_1-413](assets/create-private-folder.png)

   建立專用資料夾。 你現在可以 [添加資產](add-assets.md#upload-assets) 與其他用戶或組共用該資料夾。 在您共用該資料夾並為其分配權限之前，該資料夾對任何其他用戶都不可見。

1. 要共用資料夾，請選擇該資料夾，然後按一下 **[!UICONTROL 屬性]** 的子菜單。

1. 在 **[!UICONTROL 資料夾屬性]** 頁，從 **[!UICONTROL 添加用戶]** 清單，分配角色(`Viewer`。 `Editor`或 `Owner`)，然後按一下 **[!UICONTROL 添加]**。

   ![分配用戶組](assets/assign-permissions-private-folder.png)

   可以指定各種角色，如 `Editor`。 `Owner`或 `Viewer` 與您共用資料夾的用戶。 如果分配 `Owner` 角色，用戶 `Editor` 資料夾的權限。 此外，用戶還可以與他人共用該資料夾。 如果分配 `Editor` 角色，用戶可以編輯您的專用資料夾中的資產。 如果您分配了查看者角色，則用戶只能查看您的專用資料夾中的資產。

   >[!NOTE]
   >
   >專用資料夾至少包含一個成員 `Owner` 角色。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。根據您分配的角色，用戶在登錄到時會為您的專用資料夾分配一組權限 [!DNL Assets]。
1. 按一下 **[!UICONTROL 確定]** 關閉確認消息。
1. 與您共用資料夾的用戶在其用戶介面中接收共用通知。

1. 按一下 [!UICONTROL 通知] 開啟通知清單。

   ![通知](assets/notification-icon.png)

1. 按一下管理員共用的專用資料夾條目以開啟該資料夾。

## 刪除專用資料夾 {#delete-private-folder}

通過選擇資料夾並選擇 [!UICONTROL 刪除] 選項，或使用鍵盤上的Backspace鍵。

![「刪除」選項在頂部菜單中](assets/delete-option.png)

>[!CAUTION]
>
>如果從CRXDE Lite中刪除專用資料夾，則儲存庫中將保留冗餘用戶組。

>[!NOTE]
>
>如果使用上述方法從用戶介面中刪除資料夾，則還會刪除關聯的用戶組。
>
>但是，現有的冗餘、未使用和自動生成的用戶組可以使用 `clean` JMX中的方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
