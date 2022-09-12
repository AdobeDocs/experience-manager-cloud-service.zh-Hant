---
title: 管理SSL憑證
description: 了解如何使用Cloud Manager檢查SSL憑證的狀態，以及如何編輯、取代、更新和刪除SSL憑證。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 管理SSL憑證 {#managing-ssl-certificates}

了解如何使用Cloud Manager檢查SSL憑證的狀態，以及如何編輯、取代、更新和刪除SSL憑證。

## 檢查SSL憑證的狀態 {#checking-status-an-ssl-certificate}

您可從SSL憑證頁面一覽即可了解SSL憑證的狀態。

* **綠色**  — 此狀態表示您的證書至少從當前日期開始60天內有效。

* **橙色**  — 此狀態表示您的憑證將在60天內到期。
   * 您可以確定有計畫續約憑證，並透過Cloud Manager UI加以取代，以避免可能的網站存取或中斷。
   * Cloud Manager會在UI中傳送定期通知，提醒您憑證即將到期。

* **紅色**  — 此狀態表示SSL憑證已過期。

## 更新SSL憑證 {#update-ssl-certificate}

當憑證過期時，任何與過期憑證搭配使用的網域都將無法繼續運作。 透過下列步驟更新憑證，以確保您的網域可繼續正常運作。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。
1. 導覽至 **環境** 螢幕 **概述** 頁面。
1. 導覽至 **SSL憑證** 螢幕 **環境** 螢幕。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。 按一下要更新的憑證列右側的刪節號按鈕，然後選取 **檢視與更新**.
1. 會顯示憑證詳細資料，且可以更新。

>[!NOTE]
>
>使用者必須是 **業務負責人** 或 **部署管理員** 角色，以更新Cloud Manager中的SSL憑證。

## 取代SSL憑證 {#replace-ssl-certificate}

您可以依照一節所述的相同步驟來取代SSL憑證 [更新SSL憑證。](#update-ssl-certificate)

## 刪除SSL憑證 {#deleting-an-ssl-certificate}

從Cloud Manager移除憑證是無法還原的永久性動作。 Adobe建議您先將SSL檔案儲存在本機，再在Cloud Manager中刪除SSL檔案，此為最佳作法。

Cloud Manager不會允許您刪除與一或多個網域相關聯的SSL憑證。 刪除SSL憑證之前，必須先刪除所有相關網域。 請參閱該文檔 [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 了解更多。

請依照下列步驟刪除SSL憑證。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。
1. 導覽至 **環境** 螢幕 **概述** 頁面。
1. 導覽至 **SSL憑證** 螢幕 **環境** 螢幕。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。 按一下要刪除的憑證列右側的刪節號按鈕，然後選取 **刪除**.
1. 在 **刪除SSL憑證** 對話框。

>[!NOTE]
>
>使用者必須是 **業務負責人** 或 **部署管理員** 角色，以刪除Cloud Manager中的SSL憑證。

## 預先存在的CDN設定 {#pre-existing-cdn}

如果您的SSL憑證已有CDN設定，則會在 **SSL憑證** 頁面，鼓勵您透過UI新增這些設定，以便在Cloud Manager中顯示和設定這些設定。

使用UI移轉所有預先存在的環境設定後，訊息會消失。 訊息可能需要1到2個工作天才會消失。

請參閱該文檔 [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 以取得更多詳細資訊。

也會在 **IP允許清單** 和 **環境** IP的CDN設定已預先存在，環境的頁面會允許清單或自訂網域名稱。
