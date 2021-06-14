---
title: 檢查域名狀態
description: 檢查域名狀態
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 417939cb7a206d2b98b5e631a09307edc6724c17
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 正在檢查域名狀態{#check-status}

您可以通過從「域設定」(Domain Settings)頁面的「環境」(Environments)上的表中按一下域名的「狀態」(Status)表徵圖來確定是否已成功驗證域名。

>[!NOTE]
>當您在「新增自訂網域」精靈的驗證步驟中選取「儲存」時，Cloud Manager會自動觸發TXT驗證。 對於後續驗證，必須主動選擇狀態旁的&#x200B;**revify analy**&#x200B;表徵圖。

Cloud Manager會透過TXT值驗證網域擁有權，並顯示下列其中一個狀態訊息：

* **缺少域**
驗證FailedTXT值，或檢測到有錯誤。請按照說明重試。 準備就緒時，您必須選取 
*驗* 證狀態旁的重新圖示。

* **正在進行域**
驗證正在進行。此狀態通常會在您選取 
*驗* 證狀態旁的重新圖示。

* **已驗證，部**
署失敗TXT驗證成功。但CDN部署失敗。 Adobe代表會自動收到通知。

* **域已驗證和**
已部署此狀態表示您的自定義域名已準備好使用。
   >[!NOTE]
   >此時，您的自訂網域名稱已準備好進行測試，並指向Cloud Manager網域名稱。 請參考[配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以了解更多資訊。

* ****
正在刪除自定義域名。

* **刪除**
失敗刪除自定義域名失敗。您必須重試。 請參閱[刪除自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以深入了解。


## 自訂網域名稱{#pre-existing-cdn}的現有CDN設定

若環境中包含IP允許清單、SSL憑證或自訂網域名稱的現有CDN設定，則客戶會在&#x200B;**IP允許清單**&#x200B;和&#x200B;**環境**&#x200B;詳細資訊頁面中看到下列訊息。 當客戶透過UI完全移轉所有預先存在的環境設定後，UI上顯示的訊息就會消失，而訊息可能需要1到2個工作天才會消失。

>[!NOTE]
>若要查看及管理預先存在的設定，必須透過UI新增這些設定。 如需詳細資訊，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
