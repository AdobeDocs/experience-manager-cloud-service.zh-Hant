---
title: 檢查DNS記錄狀態
description: 檢查DNS記錄狀態
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 檢查DNS記錄狀態{#check-dns-record-status}

您可以從「網域設定」頁面的「環境」表格中，按一下DNS記錄的「狀態」圖示，判斷您的網域名稱是否正確解析為AEM雲端服務網站。

>[!NOTE]
>當您的自訂網域名稱首次成功驗證並部署時，Cloud Manager會自動觸發DNS查閱。 對於後續嘗試，您必須主動選擇狀態旁邊的&#x200B;**resolve again**&#x200B;圖示。

Cloud Manager會針對您的網域名稱執行DNS查閱，並顯示下列其中一條狀態訊息：

* **未檢測到DNS**
狀態在您的自定義域名成功驗證並部署後，將無法檢測到DNS狀態。當您的自訂網域名稱正在刪除時，也會觀察到此狀態。

* **DNS解析不**
正確這表示DNS記錄配置尚未解析／指向，或是錯誤。Adobe代表會自動收到通知。

   >[!NOTE]
   >您必須按照相應的說明配置`CNAME`或`A-record`。 請參閱「設定DNS設定」以瞭解詳細資訊。 準備就緒後，必須再次選擇狀態旁的&#x200B;**resolve**&#x200B;表徵圖。

* **正在進行DNS解**
析正在進行解析。此狀態通常會在您選取狀態旁的「再次解析」圖示後顯示。

* **DNS正確解**
析您的DNS設定已正確設定。您的網站為訪客提供服務。
