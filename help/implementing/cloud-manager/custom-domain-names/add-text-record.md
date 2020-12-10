---
title: 添加TXT記錄
description: 新增自訂網域名稱
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 添加TXT記錄{#adding-txt}

DNS TXT記錄會授權網域以裝載於CDN服務中。 客戶必須在授權Cloud Manager的區域中建立DNS TXT記錄，以便將CDN服務與自訂網域部署，並將其與後端服務建立關聯。 此關聯完全由客戶控制，並強烈授權Cloud Manager將內容從服務提供至網域。 這項授權既可授予，也可撤回。

在建立TXT記錄之前，您可以先執行以下步驟：

* 能夠修改您組織網域的DNS記錄，或聯絡可以修改的適當人員。
* 如果您尚未知道，請識別您的網域主機或註冊機構。

當您啟動網域驗證時，Cloud Manager會提供您用於驗證的名稱和TXT值。 使用指定的名稱和值將TXT記錄添加到域的DNS伺服器。

1. 登入您的網域主機，並造訪DNS記錄區段。
1. 將`_aemverification.[yourdomainname]`新增為名稱，並新增TXT值。
請參閱下表中的範例。

| 網域 | 名稱 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 顯示在Cloud Manager UI中，並且特定於域和Cloud Manager環境 |
| `test.example.com` | `_aemverification.test.example.com` | 顯示在Cloud Manager UI中，並且特定於域和Cloud Manager環境 |

完成後，您可以通過運行：`dig _aemverification.[yourdomainname] -t txt`。
預期結果應顯示Cloud Manager UI中提供的TXT值。

例如，若您的網域為`example.com`，則執行：`dig TXT _aemverification.example.com -t txt`。

>[!NOTE]
>此外，還有各種[DNS查閱工具](https://www.ultratools.com/tools/dnsLookup),Google DoH可用來查閱TXT記錄項目並識別TXT記錄是否遺失或錯誤。

