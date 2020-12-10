---
title: 刪除SSL憑證——管理SSL憑證
description: 刪除SSL憑證——管理SSL憑證
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# 刪除SSL證書{#deleting-an-ssl-certificate}

>[!IMPORTANT]
>從Cloud Manager移除憑證是無法復原的永久動作。 最佳實務是，在Cloud Manager使用者介面中刪除任何必要的SSL檔案之前，先將它們儲存在本機。

用戶必須是「業務擁有者」或「部署管理員」角色，才能刪除Cloud Manager中的SSL憑證。 Cloud Manager將不允許您刪除具有一或多個相關網域的SSL憑證。  刪除SSL憑證之前，必須先刪除所有相關的網域。 請參閱[刪除自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以瞭解詳細資訊。

請依照下列步驟刪除SSL憑證：

1. 從&#x200B;**環境**&#x200B;頁面導覽至&#x200B;**SSL憑證**畫面。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 識別您要刪除的SSL憑證名稱所列的列。
1. 選擇&#x200B;**...**&#x200B;選單。
1. 選擇&#x200B;**刪除**。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. 從&#x200B;**刪除SSL憑證**&#x200B;對話方塊確認您的提交。
