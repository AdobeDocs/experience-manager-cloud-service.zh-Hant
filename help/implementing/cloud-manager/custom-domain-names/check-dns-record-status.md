---
title: 正在檢查DNS記錄狀態
description: 了解如何使用Cloud Manager判斷您的DNS設定是否正確解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 正在檢查DNS記錄狀態 {#check-dns-record-status}

在Cloud Manager中，您可以判斷您的網域名稱是否正確解析至AEMas a Cloud Service網站。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 按一下 **網域設定** ，即可取得Advertising Cloud的說明。

1. 按一下 **狀態** 表徵圖。

Cloud Manager會對您的網域名稱執行DNS查閱，並顯示下列其中一個狀態訊息。

* **未檢測到DNS狀態**  — 在成功驗證並部署自定義域名之前，將不會檢測到DNS狀態。

   * 當您的自訂網域名稱正在刪除過程中時，也會觀察到此狀態。

* **DNS解析不正確**  — 這表示DNS記錄配置未解析或錯誤。

   * 請參閱檔案 [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 了解更多。
   * 準備就緒時，您必須選取 **再次解決** 表徵圖。

* **正在進行DNS解析**  — 決議正在進行中。

   * 此狀態通常會在您選取 **再次解決** 表徵圖。

* **DNS正確解析**  — 已正確配置DNS設定。

   * 您的網站正在為訪客服務。

當您的自訂網域名稱首次成功驗證並部署時，Cloud Manager會自動觸發DNS查閱。 對於後續嘗試，您必須主動選取 **再次解決** 表徵圖。
