---
title: 新增TXT記錄
description: 新增自訂網域名稱
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 26ac0c63e4fba167206f43f64f046452c922c10e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 新增TXT記錄 {#adding-txt}

DNS TXT記錄會授權網域以在CDN服務中托管。 客戶必須在授權Cloud Manager部署CDN服務與自訂網域，並將其與後端服務建立關聯的區域中建立DNS TXT記錄。 此關聯完全由客戶控制，並強烈授權Cloud Manager將內容從服務提供至網域。 該授權可被授予，也可被撤回。

建立TXT記錄前，您可以先依照下列步驟操作：

* 能夠修改組織網域的DNS記錄，或聯絡可以的適當人員。
* 如果您尚不知道域主機或註冊器，請確定它。

當您啟動網域驗證時，Cloud Manager會提供您用於驗證的名稱和TXT值。 使用指定的「名稱」和「值」將TXT記錄添加到域的DNS伺服器。

1. 登入您的網域主機，並造訪DNS記錄區段。
1. 新增 `_aemverification.[yourdomainname]` 以「名稱」(Name)形式，並新增TXT值，使其與其顯示完全相同。
請參閱下表中的範例。

| 網域 | 名稱 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製Cloud Manager UI中顯示的整個值。 這是網域和環境專屬的。 `Ex:adobe-aem-verification=example.com/[program]/[env]/..` |
| `test.example.com`<br>`www.example.com` | `_aemverification.www.example.com` | 複製Cloud Manager UI中顯示的整個值。 這是網域和環境專屬的。 `Ex:adobe-aem-verification=www.example.com/[program]/[env]/..` |

完成後，您可以執行以下程式來驗證結果： `dig _aemverification.[yourdomainname] -t txt`.
預期的結果應會顯示Cloud Manager UI中提供的TXT值。

例如，如果您的網域為 `example.com`，然後執行： `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>此外， [DNS查閱工具](https://www.ultratools.com/tools/dnsLookup), Google DoH可用來查閱TXT記錄項目，以及識別TXT記錄是否遺失或錯誤。
