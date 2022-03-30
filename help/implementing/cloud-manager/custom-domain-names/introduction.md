---
title: 自定義域名簡介
description: Cloud Manager的UI允許您添加自定義域，以自助方式使用唯一的品牌名稱來標識您的站點。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---


# 自定義域名簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自定義域名"
>abstract="Cloud Manager的UI允許您添加自定義域，以自助方式使用唯一的品牌名稱來標識您的站點。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="添加自定義域名"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="查看和更新自定義域名"

Cloud Manager的UI允許您添加自定義域，以自助方式使用唯一的品牌名稱來標識您的站點。 Adobe Experience Manager as a Cloud Service已設定預設域名，結尾為 `*.adobeaemcloud.com`。 即使將自定義域名與您的網站相關聯後，此預設域名仍然保留。

## 什麼是自定義域名？ {#what-are-custom-domain-names}

每個網站都具有與其關聯的唯一、機器可讀、數字地址，例如 `184.33.123.64`。 域名系統(DNS)允許您通過將數字地址轉換為易記地址(如 `wknd.com`。

為您的站點建立域名是一種很好的做法，它讓您的客戶印象深刻，並反映您的品牌。

您可以從域名註冊機構、管理和銷售域名的公司或組織購買域名。 域名註冊器管理DNS伺服器上的域名。

>[!IMPORTANT]
>
>雲管理器不是域名註冊器，不提供DNS服務。

## 限制 {#limitations}

使用自定義域名與AEMaaCS時存在許多限制。

* Cloud Manager中支援針對站點程式的發佈和預覽服務的自定義域名。 不支援作者端的自定義域。
* 每個Cloud Manager環境最多可承載每個環境500個自定義域。
* AEMas a Cloud Service不支援通配符域。
* 添加自定義域名之前，必須為程式安裝包含自定義域名的有效SSL證書。 請參閱添加SSL證書以瞭解詳細資訊。
* 當有當前正在運行的管道連接到這些環境時，無法將域名添加到這些環境。
* 一次只能添加一個域名。
* 同一域名不能用於多個環境。

## 工作流程 {#workflow}

添加自定義域名需要DNS服務與雲管理器之間的交互。 因此，安裝、配置和驗證自定義域名需要許多步驟。 下表概述了所需的步驟，包括在出現常見錯誤時應執行的操作。

| 步驟 | 說明 | 責任 | 了解更多 |
|--- |--- |--- |---|
| 1 | 將SLL證書添加到雲管理器 | 客戶 | [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 添加TXT記錄以驗證域 | 客戶 | [添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | 查看域驗證狀態 | 客戶 | [正在檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | 如果域驗證失敗且狀態為 `Domain Verification Failure` | 客戶 | [正在檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | 如果域驗證失敗且狀態為 `Verified, Deployment Failed`，聯繫人Adobe | Adobe客戶關懷 | [正在檢查域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | 通過添加指向as a Cloud Service的DNS CNAME或APEX記錄來配置DNS設AEM置 | 客戶 | [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | 檢查DNS記錄狀態 | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | 如果DNS記錄狀態失敗，則 `DNS status not detected` | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | 如果DNS記錄狀態失敗，則 `DNS resolves incorrectly` | 客戶 | [正在檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
