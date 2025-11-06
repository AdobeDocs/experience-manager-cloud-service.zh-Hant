---
title: 管理 IP 允許清單
description: 瞭解如何在Cloud Manager中檢視、編輯、刪除和檢查IP允許清單的狀態。
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 19%

---

# 管理 IP 允許清單 {#manage-ip-allow-lists}

瞭解如何在Cloud Manager中檢視、編輯、刪除和檢查IP允許清單的狀態。

## 檢視和更新IP允許清單 {#update-ip-allow-lists}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟檢視和更新IP允許清單。

**若要檢視和更新IP允許清單：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**總覽**&#x200B;頁面，在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允許清單**。
1. 識別您要檢視或更新之IP允許清單的列。
1. 按一下該列右端的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 從下拉式功能表，按一下&#x200B;**檢視和更新**。
**檢視和更新IP允許清單**&#x200B;對話方塊會顯示定義規則的名稱、IP位址（或範圍），以及套用規則的環境和服務。
1. 視需要變更名稱或IP地址。

   將新IP範圍新增至IP允許清單或從中移除時，會自動將其套用/取消套用至先前已套用至的所有對應環境/服務。

   在進行先前的更新且尚未完成時，無法更新IP允許清單。

1. 按一下&#x200B;**更新**。

## 檢查IP允許清單的狀態 {#check-allow-list-status}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**總覽**&#x200B;頁面，在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允許清單**。

1. 在IP允許清單表格的&#x200B;**狀態**&#x200B;欄中，將滑鼠指標停留在綠色（使用中）的IP允許清單上，以檢視套用至它的一或多個服務。

   表格中所顯示的狀態值具有下列意義：

   | IP允許清單的狀態 | 說明 |
   | --- | --- |
   | 已應用 | IP允許清單已成功套用至一個或多個環境。 |
   | 更新中 | 正在更新IP允許清單，可能包括清單的一個或多個應用計畫或取消應用計畫。 每個套用/取消套用都會列出，其狀態為&#x200B;**未開始**、**進行中**、**完成**，或&#x200B;**失敗**。 |
   | 失敗 | 更新的一個或多個應用計畫或取消應用計畫流程失敗。<br>·列出每個應用程式和取消應用程式及其狀態。<br>·如果更新中的一個應用程式/取消應用程式失敗，則狀態為&#x200B;**失敗**。 狀態會保持為&#x200B;**失敗**&#x200B;直到清除所有失敗。<br>·按一下狀態旁的&#x200B;**重試**&#x200B;圖示，以便您清除失敗。<br>·您無法更新或刪除狀態為&#x200B;**失敗**&#x200B;的IP允許清單。 |
   | 刪除中 | 正在刪除IP允許清單。<br>·刪除涉及從所有服務中取消套用清單。<br>·每個取消應用程式都會列出，其狀態為&#x200B;**未啟動**、**進行中**、**完成**&#x200B;或&#x200B;**失敗**。<br>·刪除作業完成後，IP允許清單不會出現在IP允許清單表格中。 此外，IP允許清單不會套用至Cloud Manager程式中的任何服務。 |
   | 刪除失敗 | 一個或多個取消應用計畫在刪除操作期間失敗。<br>·每個取消應用程式都與狀態&#x200B;**完成**&#x200B;或&#x200B;**失敗**&#x200B;一起列出。<br>·若取消應用程式失敗，狀態會變成&#x200B;**刪除失敗**。 狀態保持為&#x200B;**刪除失敗**，直到清除所有失敗為止。 在表格列的最右側，按一下![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後在下拉式功能表中按一下&#x200B;**刪除**&#x200B;以清除任何失敗。<br>·當狀態為&#x200B;**失敗**&#x200B;時，您無法更新IP允許清單。 |

## 刪除IP允許清單 {#delete-allow-list}

刪除IP允許清單時，會自動從所有服務中取消套用清單，並將其從IP允許清單表中刪除。

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟檢視和更新IP允許清單。

**若要刪除IP允許清單：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**總覽**&#x200B;頁面，在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允許清單**。
1. 識別要刪除之IP允許清單的列，然後按一下該列右端的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**刪除**。
1. 在&#x200B;**刪除IP允許清單**&#x200B;對話方塊中，按一下&#x200B;**刪除**。

## 既有的CDN設定 {#pre-existing-cdn}

如果您的IP允許清單存在既有CDN （內容傳遞網路）設定，**IP允許清單**&#x200B;頁面上會有資訊訊息。 此訊息鼓勵您透過使用者介面新增這些設定，以便在 Cloud Manager 中顯示和設定它們。

使用 UI 移轉所有預先存在的環境設定後，該訊息就會消失。訊息可能需要 1-2 個工作日才能消失。

如需詳細資訊，請參閱[新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)。

對於具有 SSL 憑證或自訂網域名稱的既有 CDN 設定的環境，**SSL 憑證**&#x200B;和&#x200B;**環境**&#x200B;頁面上也提供了類似的訊息。
