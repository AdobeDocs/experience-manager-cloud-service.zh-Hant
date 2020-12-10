---
title: '查看更新和替換SSL證書——管理SSL '
description: 查看更新和替換SSL證書——管理SSL證書
translation-type: tm+mt
source-git-commit: d5a119921a06ea06cbf2b95353083aa987869629
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 查看和更新並替換SSL證書{#view-update-replace-ssl-certificate}

## 查看和更新SSL證書{#view-update}

在Cloud Manager UI中使用這些選項的時機：

* 現有證書即將過期。 使用者已使用憑證供應商更新憑證，並希望取代即將到期的現有憑證。 注意：只有具有適當權限的使用者才能進行更新。
* 使用&#x200B;**檢視與更新**&#x200B;功能表，只要檢視SSL憑證詳細資訊即可。
* 或者，您也可以變更此畫面中用來參考憑證的名稱。
* 只有具備適當權限的使用者才能進行更新。


## 更新SSL憑證即將過期{#update-ssl-certificate}

當憑證過期時，與過期憑證一起使用的任何網域將無法再運作。 若要更新過期的憑證，您必須遵循下列步驟。 這可確保您的網域繼續視需要運作。 新增憑證後，網域必須使用新憑證更新自訂網域名稱，才能視需要運作。 有關詳細資訊，請參閱[查看和更新和替換自定義域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

請依照下列步驟更新SSL憑證：

>[!NOTE]
>用戶必須是「業務擁有者」或「部署管理員」角色，才能更新Cloud Manager中的SSL憑證。

1. 從&#x200B;**環境**&#x200B;頁面導覽至「SSL憑證」畫面。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。
1. 通過選擇感興趣行最右端的三個按鈕，可以訪問每行的菜單選項。
1. 選擇&#x200B;**查看和更新**。 您可從這裡檢視憑證詳細資訊。

## 取代SSL憑證{#replace-ssl-certificate}

請依照下列步驟來取代SSL憑證：

1. 從&#x200B;**環境**&#x200B;頁面導覽至「SSL憑證」畫面。
1. 您會看到一個表格，其中列顯示已成功安裝在程式中的每個SSL憑證。
1. 通過選擇感興趣行最右端的三個按鈕，可以訪問每行的菜單選項。
1. 選擇&#x200B;**查看和更新**。
1. 若要取代憑證，請將新內容貼入適當的輸入欄位，然後按一下「儲存」。 ****&#x200B;您需要解決可能發生的任何錯誤。

   請參閱[憑證錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error)以處理常見問題。