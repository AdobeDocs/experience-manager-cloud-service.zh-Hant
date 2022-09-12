---
title: 配置DNS設定
description: 配置DNS設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 配置DNS設定 {#configure-dns}

成功驗證並部署自定義域名後，您就可以使用DNS提供程式更新自定義域名的DNS記錄。 如此可讓您的網站為訪客提供服務。 因此，此活動通常會在上線前完成。

## 什麼是DNS設定？ {#dns-settings}

A `CNAME` 或者，一旦布建，該域的所有Internet流量將路由到其指向的任何位置。 如果未布建該位置以提供流量，則會發生中斷。 如果尚未測試，內容中可能會有錯誤。 這就是為什麼在測試完成且您準備上線後，一律會執行此步驟。

若要設定這些設定，您必須判斷 `CNAME` 或Apex記錄必須經過設定，才能將自訂網域名稱指向Cloud Manager網域名稱。 以下幾節將幫助您確定哪種類型的記錄適合您的DNS配置。

>[!NOTE]
>
>您或組織中的適當人員必須能夠登入或聯絡您的DNS提供者（您購買網域的所在公司），並在DNS設定中進行更新。

## CNAME記錄 {#cname-record}

規範名稱或CNAME記錄是將別名映射為真或規範網域名稱的DNS記錄類型。 CNAME記錄通常用於對應子網域，例如 `www.example.com` 至托管該子網域內容的網域。

登入您的網域註冊機構，並建立 `CNAME` 記錄以將自訂網域名稱指向目標，如下表。

| CNAME | 自訂網域名稱指向Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## 阿派克斯唱片 {#apex-record}

Apex網域是不包含子網域的自訂網域，例如 `example.com`. 頂點域配置有 `A` , `ALIAS` ，或 `ANAME` 通過DNS提供程式進行記錄。 Apex網域必須指向特定IP位址。

新增下列所有項目 `A` 通過域提供程式記錄到域的DNS設定。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
