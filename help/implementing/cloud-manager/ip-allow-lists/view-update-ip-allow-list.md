---
title: 檢視和更新 — Cloud Manager中的IP允許清單
description: 檢視和更新 — Cloud Manager中的IP允許清單
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 查看和更新IP允許清單{#view-update}

在下列情況下，您可以檢視並更新IP允許清單：

* 查看和更新菜單，只查看一個或多個IP允許清單的詳細資訊。
* 要編輯以下一個或多個內容：
   * 規則名稱定義中的IP範圍
   * IP允許清單規則的易記名稱

## 更新IP允許清單{#update-ip-allow-lists}


必須登錄業務所有者或部署管理員角色中的用戶，才能更新IP允許清單。

>[!NOTE]
>「檢視與更新」精靈將顯示定義規則的名稱、IP或IP範圍。 此外，它還會顯示套用規則的環境和服務。

請依照下列步驟更新IP允許清單：

1. 從&#x200B;**Environments**&#x200B;畫面導覽至&#x200B;**IP允許清單**&#x200B;頁面。
1. 識別您要檢視/更新的IP允許清單規則所列的列。
1. 選擇&#x200B;**...**&#x200B;功能表。
1. 選擇&#x200B;**View &amp; Update**&#x200B;選項。
1. 變更名稱或IP，並確認您的提交。

## 新增、更新或移除IP允許清單時的重要考量 {#considerations}

* 將新IP範圍新增至IP允許清單會自動套用至所有對應的環境服務。
* 從「IP允許清單」中移除IP範圍會自動從所有對應的環境服務中取消套用該範圍。
* 在進行先前的更新且尚未完成時，無法對IP允許清單進行更新。
* 如果先前的更新有任何錯誤，則無法更新IP允許清單。 必須通過嘗試重試更新來清除任何錯誤。
請參閱[檢查IP允許清單狀態](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)以了解詳細資訊。
