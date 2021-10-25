---
title: '配置DNS設定 '
description: 配置DNS設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 0b24f8c8b88f476a0d1073e873e46441b1b8b821
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 配置DNS設定 {#configure-dns}

成功驗證並部署自定義域名後，您就可以使用DNS提供程式更新自定義域名的DNS記錄。 如此可讓您的網站為訪客提供服務。 因此，此活動通常會在上線前完成。

>[!NOTE]
>您或組織中的適當人員必須能夠登入或聯絡您的DNS提供者（您購買網域的公司），並在DNS設定中進行更新。

要執行此操作，您必須判斷您是否必須將DNS設定 `CNAME` 或Apex記錄將您的自訂網域名稱指向Cloud Manager網域名稱。 A `CNAME` 或者，一旦布建，該域的所有Internet流量將路由到其指向的任何位置。 如果未布建該位置以提供流量，則會發生中斷。 如果尚未測試，內容中可能會有錯誤。 這就是為什麼在測試完成且客戶已準備好上線後，一律會執行此步驟。

必須依照下表所述完成下列步驟：

| 步驟 |  | 責任 | 了解更多 |
|--- |--- |--- |---|
| 添加SLL證書 | 添加SLL證書 | 客戶 | [新增SSL憑證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域驗證 | 新增TXT記錄 | 客戶 | [新增TXT記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域驗證狀態 |  | 客戶 |  |
|  | 狀態：域驗證失敗 | 客戶 | [檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 狀態：已驗證，部署失敗 | 聯絡Adobe代表 | [檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 新增CNAME或APEX記錄，以新增指向AEMas a Cloud Service的DNS記錄 | 配置DNS設定 | 客戶 | [配置DNS設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 檢查DNS記錄狀態 |  | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：未檢測到DNS狀態 | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：DNS解析不正確 | 客戶 |  |


## CNAME記錄 {#cname-record}

以下幾節將幫助您確定哪種類型的記錄適合您的DNS配置。

標準名稱或 `CNAME` 記錄是一種DNS記錄，將別名映射為真或規範的域名。 CNAME記錄通常用於對應子網域，例如 `www.example.com`  至托管該子網域內容的網域。

登入您的網域註冊機構並建立CNAME記錄，將自訂網域名稱指向目標，如下所示：

| CNAME | 自訂網域名稱指向Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## 阿派克斯唱片 {#apex-record}

Apex網域是不包含子網域的自訂網域，例如example.com。 頂點域配置有 `A` , `ALIAS` ，或 `ANAME` 通過DNS提供程式進行記錄。 Apex網域必須指向特定IP位址。

透過網域提供者，將下列所有A記錄新增至您網域的DNS設定：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
