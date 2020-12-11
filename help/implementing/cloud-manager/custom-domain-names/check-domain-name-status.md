---
title: 檢查域名狀態
description: 檢查域名狀態
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# 正在檢查域名狀態{#check-status}

您可以通過從「域設定」(Domain Settings)頁面的「環境」(Environments)表中按一下域名的「狀態」(Status)表徵圖來確定是否已成功驗證域名。

>[!NOTE]
>當您在「新增自訂網域」精靈的驗證步驟中選取「儲存」時，Cloud Manager會自動觸發TXT驗證。 對於後續的驗證，必須主動選擇狀態旁邊的&#x200B;**verify again**&#x200B;表徵圖。

Cloud Manager將通過TXT值驗證域所有權，並顯示以下狀態消息之一：

* **域驗證**
FailedTXT值缺失或檢測到錯誤。請依照指示重試。 準備就緒後，您必須選取 
*驗證* 狀態旁的「重複」圖示。

* **正在進行域驗**
證正在驗證。此狀態通常會在您選取 
*驗證* 狀態旁的「重複」圖示。

* **已驗證，部署**
FailedTXT驗證成功。但是，CDN部署失敗。 Adobe代表會自動收到通知。

* **網域已驗證和**
已部署此狀態表示您的自訂網域名稱已準備好可供使用。
   >[!NOTE]
   >此時，您的自訂網域名稱已可供測試，並可指向Cloud Manager網域名稱。 請參閱[配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以瞭解詳細資訊。

* **刪**
除自訂網域名稱正在處理中。

* **刪除**
自定義域名失敗刪除失敗。您必須重試。 請參閱[刪除自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以瞭解詳細資訊。

