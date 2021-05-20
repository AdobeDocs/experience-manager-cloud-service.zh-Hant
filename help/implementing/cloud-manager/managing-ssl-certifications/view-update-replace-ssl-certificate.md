---
title: '檢視更新和取代SSL憑證 — 管理SSL '
description: 檢視更新和取代SSL憑證 — 管理SSL憑證
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 查看和更新和替換SSL證書{#view-update-replace-ssl-certificate}

## 查看和更新SSL證書{#view-update}

何時要在Cloud Manager UI中使用這些選項：

* 現有憑證即將過期。 使用者已與憑證供應商續約憑證，並想要取代即將過期的現有憑證。 注意：只有具有適當權限的使用者才能進行更新。
* 使用&#x200B;**檢視與更新**&#x200B;功能表，只需檢視SSL憑證詳細資訊即可。
* 或者，您也可以變更已用來從此畫面參考憑證的名稱。
* 只有具有適當權限的使用者才能進行更新。


## 更新SSL憑證即將過期{#update-ssl-certificate}

當憑證過期時，任何與過期憑證搭配使用的網域都將無法繼續運作。 若要更新過期的憑證，您必須依照下列步驟操作。 這將確保您的網域可繼續正常運作。 新增憑證後，網域才能正常運作，必須以新憑證更新自訂網域名稱。 如需詳細資訊，請參閱[檢視和更新及取代自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) 。

請依照下列步驟更新SSL憑證：

>[!NOTE]
>使用者必須處於業務擁有者或部署管理員角色中，才能更新Cloud Manager中的SSL憑證。

1. 從&#x200B;**Environments**&#x200B;頁面導覽至「SSL憑證」畫面。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。
1. 可通過選擇感興趣行最右端的三個按鈕來訪問每行的菜單選項。
1. 選擇&#x200B;**查看和更新**。 您可從此處檢視憑證詳細資訊。

## 替換SSL證書{#replace-ssl-certificate}

請依照下列步驟取代SSL憑證：

1. 從&#x200B;**Environments**&#x200B;頁面導覽至「SSL憑證」畫面。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。
1. 可通過選擇感興趣行最右端的三個按鈕來訪問每行的菜單選項。
1. 選擇&#x200B;**查看和更新**。
1. 若要取代憑證，請將新內容貼入適當的輸入欄位，然後按一下「**儲存**」。 您需要解決任何可能出現的錯誤。

   請參閱[憑證錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error)以處理常見的問題。
