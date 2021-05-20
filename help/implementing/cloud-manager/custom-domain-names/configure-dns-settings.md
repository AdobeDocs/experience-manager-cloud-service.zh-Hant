---
title: '配置DNS設定 '
description: 配置DNS設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 配置DNS設定{#configure-dns}

成功驗證並部署自定義域名後，您就可以使用DNS提供程式更新自定義域名的DNS記錄。 如此可讓您的網站為訪客提供服務。 因此，此活動通常會在上線前完成。

>[!NOTE]
>您或組織中的適當人員必須能夠登入或聯絡您的DNS提供者（您購買網域的公司），並在DNS設定中進行更新。

要執行此操作，您必須確定您必須將DNS設定配置為`CNAME`或Apex記錄，將自訂網域名稱指向Cloud Manager網域名稱。 `CNAME`或A記錄一旦布建，該域的所有Internet流量將路由到它指向的任何位置。 如果未布建該位置以提供流量，則會發生中斷。 如果尚未測試，內容中可能會有錯誤。 這就是為什麼在測試完成且客戶已準備好上線後，一律會執行此步驟。

## CNAME記錄{#cname-record}

以下幾節將幫助您確定哪種類型的記錄適合您的DNS配置。

規範名稱或`CNAME`記錄是一種DNS記錄，將別名映射為真或規範域名。 CNAME記錄通常用於將子網域（例如`www.example.com`）對應至托管該子網域內容的網域。

登入您的網域註冊機構並建立CNAME記錄，將自訂網域名稱指向目標，如下所示：

| CNAME | 自訂網域名稱指向Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX記錄{#apex-record}

Apex網域是不包含子網域的自訂網域，例如example.com。 Apex網域會透過您的DNS提供者以`A` 、 `ALIAS`或`ANAME`記錄來設定。 Apex網域必須指向特定IP位址。

透過網域提供者，將下列所有A記錄新增至您網域的DNS設定：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
