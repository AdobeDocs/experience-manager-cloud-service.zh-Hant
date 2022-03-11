---
title: 查看和更新 — 雲管理器中的IP允許清單
description: 查看和更新 — 雲管理器中的IP允許清單
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 查看和更新IP允許清單 {#view-update}

您可以在以下情形下查看和更新IP允許清單：

* 查看和更新菜單，只查看一個或多個IP允許清單的詳細資訊。
* 要編輯以下一項或多項：
   * 規則名稱定義中的IP範圍
   * IP允許清單規則的友好名稱

## 更新IP允許清單 {#update-ip-allow-lists}


必須登錄業務所有者或部署管理器角色中的用戶，才能更新IP允許清單。

>[!NOTE]
>「查看和更新」嚮導將顯示定義規則的名稱、IP或IP範圍。 此外，它還將顯示應用規則的環境和服務。

按照以下步驟更新IP允許清單：

1. 導航到 **IP允許清單** 的 **環境** 的上界。
1. 標識要查看/更新的IP允許清單規則所在的行。
1. 選擇 **...** 的子菜單。
1. 選擇 **查看和更新** 的雙曲餘切值。
1. 更改名稱或IP並確認提交。

## 添加、更新或刪除IP允許清單時的重要注意事項 {#considerations}

* 將新IP範圍添加到IP允許清單將自動將其應用於所有相應的環境服務。
* 從「IP允許清單」中刪除IP範圍將自動取消從所有相應的環境服務中應用它。
* 當前更新正在進行且尚未完成時，無法對IP允許清單進行更新。
* 如果先前更新中存在任何錯誤，則無法對IP允許清單進行更新。 必須通過嘗試重試更新來清除任何錯誤。
請參閱 [檢查IP允許清單狀態](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) 來瞭解更多資訊。
