---
title: 刪除SSL憑證 — 管理SSL憑證
description: 刪除SSL憑證 — 管理SSL憑證
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 刪除SSL證書{#deleting-an-ssl-certificate}

>[!IMPORTANT]
>從Cloud Manager移除憑證是無法還原的永久性動作。 最佳作法是先將任何必要的SSL檔案儲存在本機，再在Cloud Manager使用者介面中刪除。

使用者必須處於業務擁有者或部署管理員角色中，才能刪除Cloud Manager中的SSL憑證。 Cloud Manager不會允許您刪除與一或多個網域相關聯的SSL憑證。  刪除SSL憑證之前，必須先刪除所有相關網域。 請參閱[刪除自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以深入了解。

請依照下列步驟刪除SSL憑證：

1. 從&#x200B;**Environments**&#x200B;頁面導覽至&#x200B;**SSL憑證**畫面。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 識別列出您要刪除之SSL憑證名稱的列。
1. 選擇&#x200B;**...**&#x200B;功能表。
1. 選擇&#x200B;**Delete**。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. 從&#x200B;**刪除SSL憑證**&#x200B;對話方塊確認您的提交。
