---
title: 正在檢查域名狀態
description: 正在檢查域名狀態
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 正在檢查域名狀態 {#check-status}

通過從「域設定」(Domain Settings)頁的「環境」(Environments)表格中按一下域名的「狀態」(Status)表徵圖，可確定是否已成功驗證域名。

>[!NOTE]
>當您在「添加自定義域」嚮導的驗證步驟中選擇「保存」時，Cloud Manager將自動觸發TXT驗證。 對於後續驗證，必須主動選擇 **再次驗證** 表徵圖。

Cloud Manager將通過TXT值驗證域所有權，並顯示以下狀態消息之一：

* **域驗證失敗**
TXT值丟失或檢測到有錯誤。 請按照說明操作並重試。 準備好後，必須選擇 
*再次驗證* 表徵圖。

* **正在進行域驗證**
正在驗證。 此狀態通常在您選擇 
*再次驗證* 表徵圖。

* **已驗證，部署失敗**
TXT驗證成功。 但是，CDN部署失敗。 請聯繫您的Adobe代表。

* **域驗證和部署**
此狀態表示您的自定義域名已準備好使用。
   >[!NOTE]
   >此時，您的自定義域名已準備好進行測試並指向Cloud Manager域名。 請參閱 [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 來瞭解更多資訊。

* **刪除**
正在刪除自定義域名。

* **刪除失敗**
刪除自定義域名失敗。 必須重試。 請參閱 [刪除自定義域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) 來瞭解更多資訊。


## 針對自定義域名的預先存在的CDN配置 {#pre-existing-cdn}

如果客戶的環境包括IP允許清單、SSL證書或自定義域名的預先存在的CDN配置，則會在 **IP允許清單** 和 **環境** 的子菜單。 一旦客戶通過UI完全遷移了所有預先存在的環境配置，則UI上顯示的消息將消失，消息可能需要1-2個工作日才能消失。

>[!NOTE]
>為了查看和管理預先存在的配置，必須通過UI添加這些配置。 請參閱 [添加自定義域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 的子菜單。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
