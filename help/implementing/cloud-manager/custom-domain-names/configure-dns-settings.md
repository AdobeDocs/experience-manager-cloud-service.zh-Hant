---
title: 正在設定 DNS 設定
description: 瞭解如何為自訂網域名稱設定DNS設定，讓您的網站可為訪客提供服務。
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 49%

---


# 正在設定 DNS 設定 {#configure-dns}

在您的自訂網域名稱成功[驗證和部署後，](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)您就可以使用DNS提供者更新自訂網域名稱的DNS記錄了。 這樣做可以讓您的網站為訪客提供服務。因此，此活動通常在入門之前完成。

## 什麼是 DNS 設定？ {#dns-settings}

`CNAME`或記錄一旦布建，就會將網域的所有網際網路流量路由到它指向的任何地方。 如果未佈建該位置來處理流量，則會發生中斷。如果未經測試，內容可能會存在錯誤。這就是為什麼這個步驟總是在完成測試且準備好上線之後才完成。

若要設定這些設定，您必須確定是否必須設定`CNAME`或Apex記錄以將您的自訂網域名稱指向Cloud Manager網域名稱。 本檔案的下列章節將幫助您確定適合您的DNS設定的記錄型別。

## 要求 {#requirements}

在設定DNS記錄之前，您必須滿足這些要求。

* 如果您還不知道您的網域名稱主機服務商或註冊商，則必須確定它。
* 您必須能夠編輯組織網域的DNS記錄，或聯絡可以編輯的適當人員。
* 您必須已驗證您設定的自訂網域名稱，如檔案[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述。

## CNAME 記錄 {#cname-record}

正式名稱或 CNAME 記錄是一種將別名對應到真實或正式網域名稱的 DNS 記錄。CNAME 記錄通常用於將子網域 (例如 `www.example.com`) 對應到託管該子網域內容的網域。

登入您的網域註冊機構並建立 `CNAME` 記錄，將您的自訂網域名稱指向目標，如下表所示。

| CNAME | 自訂網域名稱指向目標 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX 記錄 {#apex-record}

Apex 網域是不包含子網域的自訂網域，例如`example.com`。Apex 網域是透過您的 DNS 提供者使用 `A`、`ALIAS` 或 `ANAME`記錄設定的。Apex 網域必須指向特定的 IP 位址。

透過您的網域提供者將下列`A`記錄新增到您網域的DNS設定中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## 後續步驟 {#next-steps}

為自訂網域名稱設定DNS記錄後，您需要在Cloud Manager中驗證這些設定。 繼續檔案[檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)以完成您的自訂網域名稱。
