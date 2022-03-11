---
title: '查看更新和替換SSL證書 — 管理SSL '
description: 查看更新和替換SSL證書 — 管理SSL證書
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 查看、更新和替換SSL證書  {#view-update-replace-ssl-certificate}

## 查看和更新SSL證書 {#view-update}

何時在雲管理器UI中使用這些選項：

* 現有證書即將過期。 用戶已使用證書供應商續訂證書，並希望替換即將過期的現有證書。 注意：只有具有相應權限的用戶才能進行更新。
* 使用 **查看和更新** 的子菜單。
* 或者，可以更改已用於從此螢幕引用證書的名稱。
* 只有具有相應權限的用戶才能進行更新。


## 正在更新SSL證書即將過期 {#update-ssl-certificate}

當證書過期時，任何與過期證書一起使用的域將不再工作。 要更新過期的證書，必須遵循下面列出的步驟。 這將確保您的域繼續按需要工作。 添加新證書將需要使用新證書更新自定義域名，然後域才能按需要工作。 請參閱 [查看、更新和替換自定義域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) 的子菜單。

按照以下步驟更新SSL證書：

>[!NOTE]
>用戶必須處於業務所有者或部署管理器角色中，才能更新雲管理器中的SSL證書。

1. 從導航到「SSL證書」螢幕 **環境** 的子菜單。
1. 您將看到一個表，其中每個SSL證書都已成功安裝在您的程式中。
1. 通過選擇感興趣行最右端的三個按鈕，可以訪問每行的菜單選項。
1. 選擇 **查看和更新**。 可以從此處查看證書詳細資訊。

## 替換SSL證書 {#replace-ssl-certificate}

按照以下步驟替換SSL證書：

1. 從導航到「SSL證書」螢幕 **環境** 的子菜單。
1. 您將看到一個表，其中每個SSL證書都已成功安裝在您的程式中。
1. 通過選擇感興趣行最右端的三個按鈕，可以訪問每行的菜單選項。
1. 選擇 **查看和更新**。
1. 要替換證書，請將新內容貼上到相應的輸入欄位中，然後按一下 **保存**。 您需要解決可能出現的任何錯誤。

   請參閱 [證書錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) 解決常見問題。
