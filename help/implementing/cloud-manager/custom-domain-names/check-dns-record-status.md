---
title: 正在檢查DNS記錄狀態
description: 正在檢查DNS記錄狀態
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 正在檢查DNS記錄狀態 {#check-dns-record-status}

您可以從「網域設定」頁面的「環境」表格中按一下DNS記錄的「狀態」圖示，以判斷您的網域名稱是否正確解析至AEMas a Cloud Service網站。

當您的自訂網域名稱首次成功驗證並部署時，Cloud Manager會自動觸發DNS查閱。 對於後續嘗試，必須主動選擇狀態旁的&#x200B;**resolve any**&#x200B;表徵圖。

Cloud Manager會對您的網域名稱執行DNS查閱，並顯示下列其中一個狀態訊息：

* **未檢測到**
DNS狀態在成功驗證並部署自定義域名之前，將不檢測到DNS狀態。當您的自訂網域名稱正在刪除過程中時，也會觀察到此狀態。

* **DNS解**
析不正確這表示DNS記錄配置尚未解析/指向，或錯誤。

   >[!NOTE]
   >您必須依照對應的指示來設定`CNAME`或`A-record`。 如需詳細資訊，請參閱設定DNS設定。 準備就緒後，您必須再次選取狀態旁的&#x200B;**resolve**&#x200B;圖示。

* **正在進行DNS**
解析ProgressResolution。此狀態通常會在您選取狀態旁的「再次解析」圖示後顯示。

* **DNS正確解**
析正確配置了DNS設定。您的網站正在為訪客服務。
