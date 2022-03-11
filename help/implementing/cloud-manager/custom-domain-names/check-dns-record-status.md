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

通過從「域設定」頁的「環境」表中按一下DNS記錄的「狀態」表徵圖，可確定域名是否正確解析AEM到as a Cloud Service網站。

當首次成功驗證和部署自定義域名時，Cloud Manager將自動觸發DNS查找。 對於後續嘗試，必須主動選擇 **再次** 表徵圖。

Cloud Manager會為域名執行DNS查找並顯示以下狀態消息之一：

* **未檢測到DNS狀態**
在成功驗證和部署您的自定義域名之前，將不會檢測到DNS狀態。 當您的自定義域名正在刪除過程中時，也會看到此狀態。

* **DNS解析不正確**
這表示DNS記錄配置尚未解析/指向或有錯誤。

   >[!NOTE]
   >必須配置 `CNAME` 或 `A-record` 按照相應的指令。 請參閱配置DNS設定以瞭解詳細資訊。 準備好後，必須選擇 **再次** 表徵圖。

* **正在進行DNS解析**
正在解決。 通常，在您選擇狀態旁邊的「再次解決」表徵圖後會看到此狀態。

* **DNS解析正確**
您的DNS設定已正確配置。 您的站點為訪問者提供服務。
