---
title: 管理 SSL 憑證
description: 了解如何使用 Cloud Manager 檢查 SSL 憑證的狀態以及如何編輯、取代、更新和刪除它們。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 79%

---

# 管理 SSL 憑證 {#managing-ssl-certificates}

了解如何使用 Cloud Manager 檢查 SSL 憑證的狀態以及如何編輯、取代、更新和刪除它們。

## 檢查 SSL 憑證的狀態 {#checking-status-an-ssl-certificate}

您的 SSL 憑證狀態可以從 SSL 憑證頁面一眼掌握。

* **綠色** - 此狀態代表您的憑證從目前日期起至少 60 天有效。

* **橘色** - 此狀態代表您的憑證將在 60 天內到期。
   * 現在是時候確保您有計畫更新憑證，並透過Cloud Manager使用者介面取代憑證，以避免可能的網站存取或中斷。
   * Cloud Manager 將在 UI 中定期發送通知，提醒您憑證即將到期。

* **紅色** - 此狀態代表 SSL 憑證已過期。

## 更新 SSL 憑證 {#update-ssl-certificate}

憑證過期後，與過期憑證一起使用的任何網域都將不再運作。透過以下步驟更新您的憑證可確保您的網域繼續如期運作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從&#x200B;**環境**&#x200B;畫面瀏覽到 **SSL** 憑證。
1. 您將看到一個表格，其中一列顯示已成功安裝在計畫中的每個 SSL 憑證。按一下要更新的憑證列最右側的省略符號按鈕，然後選擇&#x200B;**檢視和更新**。
1. 憑證詳細資訊隨即顯示並可進行更新。

>[!NOTE]
>
>使用者必須是 **業務負責人** 或 **部署管理員** 角色以更新Cloud Manager中的SSL憑證。

## 取代 SSL 憑證 {#replace-ssl-certificate}

可以按照[更新 SSL 憑證](#update-ssl-certificate)部分中描述的相同步驟取代 SSL 憑證。

## 刪除 SSL 憑證 {#deleting-an-ssl-certificate}

從 Cloud Manager 中移除憑證是一項無法復原的永久性動作。作為最佳實務，Adobe 建議先在本機儲存 SSL 檔案，然後才從 Cloud Manager 中刪除它們。

Cloud Manager 不允許您刪除與一個或多個網域相關聯的 SSL 憑證。在刪除 SSL 憑證之前，必須刪除所有關聯的網域。另請參閱 [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 以深入瞭解。

按照以下步驟刪除 SSL 憑證。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從&#x200B;**環境**&#x200B;畫面瀏覽到 **SSL** 憑證。
1. 您將看到一個表格，其中一列包含已成功安裝在計畫中的每個 SSL 憑證。按一下要刪除的憑證列最右側的省略符號按鈕，然後選擇&#x200B;**刪除**。
1. 在&#x200B;**刪除 SSL 憑證**&#x200B;對話框中確認刪除。

>[!NOTE]
>
>使用者必須是 **業務負責人** 或 **部署管理員** 角色以刪除Cloud Manager中的SSL憑證。

## 既有的 CDN 設定 {#pre-existing-cdn}

如果您的SSL憑證存在既有CDN設定，則 **SSL憑證** 頁面，鼓勵您透過UI新增這些設定，以便在Cloud Manager中顯示和設定它們。

使用 UI 移轉所有預先存在的環境設定後，該訊息就會消失。訊息可能需要 1-2 個工作日才能消失。

另請參閱 [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 以取得更多詳細資料。

對於具有 IP 允許清單或自訂網域名稱的既有 CDN 設定的環境，**IP 允許清單**&#x200B;和&#x200B;**環境**&#x200B;頁面上也提供了類似的訊息。
