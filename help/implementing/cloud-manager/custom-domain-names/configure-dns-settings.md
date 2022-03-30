---
title: '配置DNS設定 '
description: 配置DNS設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 配置DNS設定 {#configure-dns}

在成功驗證和部署自定義域名後，您準備與DNS提供程式一起更新自定義域名的DNS記錄。 這樣，您的站點就可以為訪問者提供服務。 因此，通常在開始使用前完成此活動。

## 什麼是DNS設定？ {#dns-settings}

A `CNAME` 或者，一旦設定了記錄，則會將域的所有Internet通信路由到其指向的任何位置。 如果該位置未設定為為通信服務，則將發生中斷。 如果尚未測試，則內容中可能存在錯誤。 這就是測試完成並準備好投入使用後始終執行此步驟的原因。

要配置這些設定，需要確定 `CNAME` 或必須配置Apex記錄以將您的自定義域名指向Cloud Manager域名。 以下各節將幫助您確定適合DNS配置的記錄類型。

>[!NOTE]
>
>您或組織中的相應人員必須能夠登錄或聯繫您的DNS提供商（您購買域的公司），並在DNS設定中進行更新。

## CNAME記錄 {#cname-record}

規範名稱或CNAME記錄是將別名映射到真或規範域名的DNS記錄類型。 CNAME記錄通常用於映射子域，如 `www.example.com` 到承載該子域內容的域。

登錄到域註冊器並建立 `CNAME` 記錄以將自定義域名指向目標，如下表。

| 名稱 | 自定義域名指向目標 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX唱片 {#apex-record}

頂點域是不包含子域(如 `example.com`。 頂點域配置有 `A` 。 `ALIAS` 或 `ANAME` 通過DNS提供程式進行記錄。 頂點域必須指向特定的IP地址。

添加以下所有內容 `A` 通過域提供程式記錄到域的DNS設定。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
