---
title: 自訂網域名稱簡介
description: Cloud Manager的UI可讓您新增自訂網域，以自助方式使用獨特的品牌名稱來識別您的網站。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---


# 自訂網域名稱簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自訂網域名稱"
>abstract="Cloud Manager的UI可讓您新增自訂網域，以自助方式使用獨特的品牌名稱來識別您的網站。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="新增自訂網域名稱"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="查看和更新自定義域名"

Cloud Manager的UI可讓您新增自訂網域，以自助方式使用獨特的品牌名稱來識別您的網站。 Adobe Experience Manager as a Cloud Service已布建預設網域名稱，結尾為 `*.adobeaemcloud.com`. 即使您將自訂網域名稱與網站建立關聯，此預設網域名稱仍會保留。

## 什麼是自訂網域名稱？ {#what-are-custom-domain-names}

每個網站都有一個與其相關聯的唯一、機器可讀、數值地址，例如 `184.33.123.64`. 網域名稱系統(DNS)可讓您將數位地址轉換為令人難忘的位址，例如，將自訂、品牌化的網域附加至網站 `wknd.com`.

為您的網站命名網域名稱是很好的作法，這會讓客戶難忘並反映您的品牌。

您可以向域名註冊機構、管理和銷售域名的公司或組織購買域名。 域名註冊器管理DNS伺服器上的域名。

>[!IMPORTANT]
>
>Cloud Manager不是域名註冊機構，不提供DNS服務。

## 限制 {#limitations}

搭配AEMaaCS使用自訂網域名稱有幾項限制。

* Cloud Manager支援自訂網域名稱，適用於Sites程式的發佈和預覽服務。 不支援製作端的自訂網域。
* 每個Cloud Manager環境最多可托管每個環境500個自訂網域。
* AEMas a Cloud Service不支援萬用字元網域。
* 新增自訂網域名稱之前，必須先為您的程式安裝包含自訂網域名稱的有效SSL憑證。 如需詳細資訊，請參閱新增SSL憑證。
* 當有一個當前正在運行的管道連接到這些環境時，無法將域名添加到環境中。
* 一次只能添加一個域名。
* 同一個域名不能用於多個環境。

## 工作流程 {#workflow}

新增自訂網域名稱需要DNS服務與Cloud Manager之間的互動。 因此，安裝、設定及驗證自訂網域名稱需執行許多步驟。 下表概述所需步驟，包括發生常見錯誤時應執行的動作。

| 步驟 | 說明 | 責任 | 了解更多 |
|--- |--- |--- |---|
| 1 | 將SLL憑證新增至Cloud Manager | 客戶 | [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 添加TXT記錄以驗證域 | 客戶 | [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | 查看域驗證狀態 | 客戶 | [檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | 如果域驗證失敗且狀態為 `Domain Verification Failure` | 客戶 | [檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | 如果域驗證失敗且狀態為 `Verified, Deployment Failed`，連絡Adobe | Adobe客戶服務 | [檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | 新增指向AEMas a Cloud Service的DNS CNAME或APEX記錄，以設定DNS設定 | 客戶 | [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | 檢查DNS記錄狀態 | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | 如果DNS記錄狀態失敗，為 `DNS status not detected` | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | 如果DNS記錄狀態失敗，為 `DNS resolves incorrectly` | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
