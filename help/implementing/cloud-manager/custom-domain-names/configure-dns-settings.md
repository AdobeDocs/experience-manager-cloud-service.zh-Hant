---
title: '配置DNS設定 '
description: 配置DNS設定
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# 配置DNS設定{#configure-dns}

在您的自訂網域名稱經過成功驗證和部署後，您就可以使用DNS提供者更新自訂網域名稱的DNS記錄。 如此，您的網站便可為訪客提供服務。 因此，此活動通常在上線前完成。

>[!NOTE]
>您或貴組織中適當的個人必須能夠登入或聯絡您的DNS提供者（您向其購買網域的公司），並在您的DNS設定中進行更新。

為此，您必須確定必須將DNS設定配置為`CNAME`或將自定義域名指向Cloud Manager域名的Apex記錄。 在布建`CNAME`或A記錄後，會將網域的所有網際網路流量路由至其所指向的位置。 如果未布建該位置來提供流量，則會發生中斷。 如果尚未測試，內容中可能會有錯誤。 這就是為什麼測試完成後，客戶就可立即上線，而且始終要執行此步驟。

## CNAME記錄{#cname-record}

以下幾節將幫助您確定哪種記錄適合您的DNS配置。

標準名稱或`CNAME`記錄是一種DNS記錄，可將別名映射為真或標準域名。 CNAME記錄通常用於將子網域（例如`www.example.com`）映射至代管該子網域內容的網域。

登入您的網域註冊機構並建立CNAME記錄，將您的自訂網域名稱指向目標，如下所示：

| CNAME | 自訂網域名稱指向目標 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX記錄{#apex-record}

頂點網域是不包含子網域（例如example.com）的自訂網域。 頂點域通過您的DNS提供器配置有`A` 、 `ALIAS`或`ANAME`記錄。 Apex網域必須指向特定的IP位址。

透過網域提供者，將下列所有A記錄新增至網域的DNS設定：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
