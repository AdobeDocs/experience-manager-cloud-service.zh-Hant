---
title: 檢查 DNS 記錄狀態
description: 了解如何使用 Cloud Manager 確定您的 DNS 設定是否正確解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 60%

---


# 檢查 DNS 記錄狀態 {#check-dns-record-status}

了解如何使用 Cloud Manager 確定您的 DNS 設定是否正確解析。

## DNS記錄狀態 {#status}

在DNS正確解析之前，自訂網域名稱無法提供即時流量。 在 Cloud Manager 中，您可以確定您的網域名稱是否正確解析為 AEM as a Cloud Service 網站。

## 要求 {#requirements}

在使用Cloud Manager檢查DNS記錄狀態之前，您必須滿足這些要求。

* 您必須已經設定自訂網域名稱的DNS設定，如檔案[設定DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)中所述。

## 如何檢查DNS記錄狀態 {#how-to}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 按一下左側導覽面板中的&#x200B;**網域設定**。

1. 按一下網域名稱的&#x200B;**狀態**&#x200B;圖示。

Cloud Manager會針對您的網域名稱執行DNS查詢，並顯示其[目前狀態](#statuses)。

當您的自訂網域名稱首次成功驗證和部署時，Cloud Manager 將自動觸發 DNS 查找。對於後續嘗試，您必須主動選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示。

## Cloud Manager中的DNS狀態 {#statuses}

自訂網域在Cloud Manager中可以有下列其中一種狀態。

* **未檢測到 DNS 狀態**- 在您的自訂網域名稱成功驗證和部署之前，不會檢測到 DNS 狀態。

   * 當您的自訂網域名稱處於刪除過程中時，也會觀察到此狀態。

* **DNS 解析不正確**- 這表明 DNS 記錄設定尚未解析或錯誤。

   * 如需更多資訊，請參閱 [設定 DNS 設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)。
   * 準備就緒後，必須選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示。

* **DNS 解析正在進行中**- 決議正在進行中。

   * 選擇狀態旁邊的&#x200B;**再次解析**&#x200B;圖示後，通常會看到此狀態。

* **DNS 正確解析**- 您的 DNS 設定已正確配置。

   * 您的網站正在為訪客服務。

## 後續步驟 {#next-steps}

恭喜！您已成功設定自訂網域以與Cloud Manager搭配使用。 如需有關如何使用Cloud Manager管理自訂網域名稱的詳細資訊，請參閱檔案[管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)。
