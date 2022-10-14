---
title: 檢查 DNS 記錄狀態
description: 了解如何使用 Cloud Manager 確定您的 DNS 設定是否正確解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 100%

---

# 檢查 DNS 記錄狀態 {#check-dns-record-status}

在 Cloud Manager 中，您可以確定您的網域名稱是否正確解析為 AEM as a Cloud Service 網站。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 在左側瀏覽面板中按一下&#x200B;**網域設定**。

1. 按一下網域名稱的&#x200B;**狀態**&#x200B;圖示。

Cloud Manager 對您的網域名稱執行 DNS 查找並顯示以下狀態消息之一。

* **未檢測到 DNS 狀態**- 在您的自訂網域名稱成功驗證和部署之前，不會檢測到 DNS 狀態。

   * 當您的自訂網網域名稱處於刪除過程中時，也會觀察到此狀態。

* **DNS 解析不正確**- 這表明 DNS 記錄設定尚未解析或錯誤。

   * 如需了解詳細資訊，請參閱文件：[設定 DNS 設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)。
   * 準備就緒後，必須選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示。

* **DNS 解析正在進行中**- 決議正在進行中。

   * 選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示後，通常會看到此狀態。

* **DNS 正確解析**- 您的 DNS 設定已正確配置。

   * 您的網站正在為訪客服務。

當您的自訂網域名稱首次成功驗證和部署時，Cloud Manager 將自動觸發 DNS 查找。對於後續嘗試，您必須主動選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示。
