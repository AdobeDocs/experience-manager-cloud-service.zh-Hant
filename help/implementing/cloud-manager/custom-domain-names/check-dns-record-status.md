---
title: 正在檢查DNS記錄狀態
description: 瞭解如何使用雲管理器確定DNS設定是否正確解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 正在檢查DNS記錄狀態 {#check-dns-record-status}

在雲管理器中，您可以確定域名是否正確解析到AEMas a Cloud Service網站。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. Click on **Domain Settings** in the left navigation panel.

1. 按一下 **狀態** 表徵圖。

Cloud Manager performs a DNS lookup for your domain name and displays one of the following status messages.

* **未檢測到DNS狀態**  — 在成功驗證和部署自定義域名之前，將不會檢測到DNS狀態。

   * 當您的自定義域名正在刪除過程中時，也會看到此狀態。

* **DNS Resolves Incorrectly** - This indicates that either the DNS records configuration has not resolved or is erroneous.

   * Refer to the document [Configuring DNS Settings](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) to learn more.
   * When ready, you must select the **Resolve Again** icon next to the status.

* **DNS Resolution In Progress** - The resolution is in progress.

   * 此狀態通常在您選擇 **再次解決** 表徵圖。

* **DNS Resolves Correctly** - Your DNS settings are properly configured.

   * 您的站點為訪問者提供服務。

Cloud Manager will automatically trigger a DNS lookup when your custom domain name is first successfully verified and deployed. 對於後續嘗試，必須主動選擇 **再次解決** 表徵圖。
