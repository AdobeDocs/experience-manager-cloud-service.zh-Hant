---
title: 正在設定 DNS 設定
description: 正在設定 DNS 設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 100%

---

# 正在設定 DNS 設定 {#configure-dns}

成功驗證和部署自訂網域名稱後，您就可以使用 DNS 提供者更新自訂網域名稱的 DNS 記錄了。這樣做可以讓您的網站為訪客提供服務。因此，此活動通常在入門之前完成。

## 什麼是 DNS 設定？ {#dns-settings}

一個 `CNAME` 或一則記錄，部署後將把網域的所有網際網路流量路由到它指向的任何地方。如果未佈建該位置來處理流量，則會發生中斷。如果未經測試，內容可能會存在錯誤。這就是為什麼這個步驟總是在完成測試且準備好上線之後才完成。

為了設定這些設定，您需要確定是否必須設定 `CNAME` 或 Apex 記錄以將您的自訂網域名稱指向 Cloud Manager 網域名稱。以下區段將幫助您確定適合您的 DNS 設定的記錄類型。

>[!NOTE]
>
>您或您組織中適當的個人必須能夠登入或聯絡您的 DNS 提供者 (您購買網域的公司) 並在您的 DNS 設定中進行更新。

## CNAME 記錄 {#cname-record}

正式名稱或 CNAME 記錄是一種將別名對應到真實或正式網域名稱的 DNS 記錄。CNAME 記錄通常用於將子網域 (例如 `www.example.com`) 對應到託管該子網域內容的網域。

登入您的網域註冊機構並建立 `CNAME` 記錄，將您的自訂網域名稱指向目標，如下表所示。

| CNAME | 自訂網域名稱指向目標 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX 記錄 {#apex-record}

Apex 網域是不包含子網域的自訂網域，例如`example.com`。Apex 網域是透過您的 DNS 提供者使用 `A`、`ALIAS` 或 `ANAME`記錄設定的。Apex 網域必須指向特定的 IP 位址。

透過您的網域提供者將以下所有 `A` 記錄新增到您網域的 DNS 設定中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
