---
title: 檢查域名狀態
description: 檢查域名狀態
translation-type: tm+mt
source-git-commit: e99c8552e2afff677c08c859dd1044287053a40e
workflow-type: tm+mt
source-wordcount: '343'
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


## IP允許清單{#pre-existing-cdn}的預先存在的CDN設定

具備IP允許清單、SSL憑證或自訂網域名稱之CDN預先存在組態的客戶，將會在&#x200B;**IP允許清單**&#x200B;和&#x200B;**環境**&#x200B;詳細資訊頁面中看到下列訊息。 當客戶透過UI完全移轉所有預先存在的環境設定後，UI上顯示的訊息將會消失，而且訊息可能需要1-2個工作天才能消失。

>[!NOTE]
>若要查看並管理預先存在的組態，必須透過UI加入。 如需詳細資訊，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
