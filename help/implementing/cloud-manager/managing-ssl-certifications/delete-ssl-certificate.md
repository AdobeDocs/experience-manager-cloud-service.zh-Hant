---
title: 刪除SSL證書 — 管理SSL證書
description: 刪除SSL證書 — 管理SSL證書
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 刪除SSL證書 {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>從雲管理器中刪除證書是無法撤消的永久操作。 最佳做法是，在Cloud Manager用戶介面中刪除任何必要的SSL檔案之前，將其保存在本地。

用戶必須處於業務所有者或部署管理器角色中，才能刪除雲管理器中的SSL證書。 Cloud Manager不允許您刪除具有一個或多個與其關聯的域的SSL證書。  刪除SSL證書之前必須刪除所有關聯的域。 請參閱 [刪除自定義域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) 來瞭解更多資訊。

按照以下步驟刪除SSL證書：

1. 導航到 **SSL證書** 螢幕 **環境** 的子菜單。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 標識要刪除的SSL證書名稱所在的行。
1. 選擇 **...** 的子菜單。
1. 選擇 **刪除**。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. 確認您的提交 **刪除SSL證書** 對話框。
