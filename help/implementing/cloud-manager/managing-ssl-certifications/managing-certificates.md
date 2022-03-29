---
title: 管理SSL證書
description: 瞭解如何使用雲管理器檢查SSL證書的狀態，以及如何編輯、替換、更新和刪除這些證書。
source-git-commit: 95539851590456b6b5ecbfeb0df8fc7bc7dde74b
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 管理SSL證書 {#managing-ssl-certificates}

瞭解如何使用雲管理器檢查SSL證書的狀態，以及如何編輯、替換、更新和刪除這些證書。

## 檢查SSL證書的狀態 {#checking-status-an-ssl-certificate}

您的SSL證書的狀態可以從SSL證書頁面一覽而知。

* **綠色**  — 此狀態表示證書在當前日期起至少60天內有效。

* **橙色**  — 此狀態表示您的證書將在60天內過期。
   * 現在是時候確保您有計畫續訂證書並通過Cloud Manager UI替換它，以避免可能的站點訪問或中斷。
   * Cloud Manager將在UI中發送定期通知，以提醒您即將到期的證書。

* **紅色**  — 此狀態表示SSL證書已過期。

## 預先存在的CDN配置 {#pre-existing-cdn}

如果SSL證書的CDN配置已預先存在，則 **SSL證書** 頁面，鼓勵您通過UI添加這些配置，以便它們在雲管理器中可見且可配置。

使用UI遷移所有預先存在的環境配置後，消息將消失。 消息可能需要1-2個工作日才能消失。

請參閱文檔 [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 的子菜單。

此外，在 **IP允許清單** 和 **環境** IP的CDN配置已預先存在的環境的頁面允許清單或自定義域名。

## 更新SSL證書 {#update-ssl-certificate}

當證書過期時，任何與過期證書一起使用的域將不再工作。 通過以下步驟更新證書可確保域繼續按需要工作。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。
1. 導航到 **環境** 螢幕 **概述** 的子菜單。
1. 導航到 **SSL證書** 螢幕 **環境** 的上界。
1. 您將看到一個表，其中每個SSL證書都已成功安裝在您的程式中。 按一下要更新的證書行中最右側的省略號按鈕，然後選擇 **查看和更新**。
1. 將顯示證書詳細資訊，並可以更新。

>[!NOTE]
>
>用戶必須是 **業務所有者** 或 **部署管理器** 角色，以更新雲管理器中的SSL證書。

## 替換SSL證書 {#replace-ssl-certificate}

可以按照一節中所述的步驟替換SSL證書 [正在更新SSL證書。](#update-ssl-certificate)

## 刪除SSL證書 {#deleting-an-ssl-certificate}

從雲管理器中刪除證書是無法撤消的永久操作。 作為最佳做法，Adobe建議在Cloud Manager中刪除SSL檔案之前將其保存在本地。

Cloud Manager不允許您刪除具有一個或多個與其關聯的域的SSL證書。 刪除SSL證書之前必須刪除所有關聯的域。 請參閱文檔 [刪除自定義域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) 來瞭解更多資訊。

按照以下步驟刪除SSL證書。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。
1. 導航到 **環境** 螢幕 **概述** 的子菜單。
1. 導航到 **SSL證書** 螢幕 **環境** 的上界。
1. 您將看到一個表，其中每個SSL證書都已成功安裝在您的程式中。 按一下要刪除的證書行中最右側的省略號按鈕，然後選擇 **刪除**。
1. 確認刪除 **刪除SSL證書** 對話框。

>[!NOTE]
>
>用戶必須是 **業務所有者** 或 **部署管理器** 角色，以刪除雲管理器中的SSL證書。