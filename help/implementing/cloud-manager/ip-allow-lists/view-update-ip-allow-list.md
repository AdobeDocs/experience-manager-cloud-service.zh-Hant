---
title: 檢視和更新- Cloud Manager中的IP允許清單
description: 檢視和更新- Cloud Manager中的IP允許清單
translation-type: tm+mt
source-git-commit: 7fdfa626147a72f3d7fb98b89a19a871fc7a13ca
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 查看和更新IP允許清單{#view-update}

您可以在下列情況下檢視和更新IP允許清單：

* 若要檢視和更新功能表，只要檢視一或多個IP允許清單的詳細資訊即可。
* 要編輯以下一個或多個內容：
   * 規則名稱定義中的IP範圍
   * IP允許清單規則的好記名稱

## 更新IP允許清單{#update-ip-allow-lists}


必須登錄「業務所有者」或「部署管理員」角色中的用戶，才能更新「IP允許清單」。

>[!NOTE]
>「檢視與更新」精靈將顯示定義規則的名稱、IP或IP範圍。 此外，它還會顯示套用規則的環境和服務。

請依照下列步驟更新IP允許清單：

1. 從&#x200B;**Environments**&#x200B;畫面導覽至&#x200B;**IP允許清單**&#x200B;頁面。
1. 標識要查看／更新的IP允許清單規則列在的行。
1. 選擇&#x200B;**...**&#x200B;選單。
1. 選擇&#x200B;**查看和更新**&#x200B;選項。
1. 變更名稱或IP，並確認您的提交。

## 添加、更新或刪除IP允許清單時的重要考慮事項{#considerations}

* 將新的IP範圍添加到IP允許清單將自動將其應用到所有相應的環境服務。
* 從「IP允許清單」中刪除IP範圍將自動從所有相應的環境服務中取消應用該範圍。
* 當先前的更新正在進行且尚未完成時，無法對「IP允許清單」進行更新。
* 如果先前的更新有任何錯誤，則無法對「IP允許清單」進行更新。 任何錯誤都必須通過嘗試重試更新來清除。
請參閱[檢查IP允許清單狀態](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)以瞭解更多資訊。