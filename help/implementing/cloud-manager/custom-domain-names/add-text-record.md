---
title: 新增TXT記錄
description: 了解如何新增TXT記錄以在Cloud Manager中新增自訂網域名稱。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 新增TXT記錄 {#adding-txt}

DNS TXT記錄會授權網域以在CDN服務中托管。 您必須在授權Cloud Manager部署CDN服務與自訂網域，並將其與後端服務建立關聯的區域中，建立DNS TXT記錄。 此關聯完全由您控制，並授權Cloud Manager將內容從服務提供至網域。 此授權可授予，也可撤回。 TXT記錄專屬於網域和Cloud Manager環境。

新增TXT記錄前，您必須先滿足這些要求。

* 您必須能夠修改組織網域的DNS記錄，或聯絡可以的適當人員。
* 如果您尚未確定域主機或註冊機構，則必須確定它。

當您啟動網域驗證時，Cloud Manager會提供您用於驗證的名稱和TXT值。 使用指定的名稱和值，將TXT記錄新增至網域的DNS伺服器。

1. 登入您的網域主機，並尋找「DNS記錄」區段。
1. 新增 `_aemverification.[yourdomainname]` 作為 **名稱** 值，並依其顯示方式新增TXT值。

請參閱此表格中的範例。

| 網域 | 名稱 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製Cloud Manager UI中顯示的整個值。 這是網域和環境專屬的。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 複製Cloud Manager UI中顯示的整個值。 這是網域和環境專屬的。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完成後，可通過運行以下命令來驗證結果

```shell
dig _aemverification.[yourdomainname] -t txt
```

預期的結果應會顯示Cloud Manager UI中提供的TXT值。

例如，如果您的網域為 `example.com`，然後執行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有 [DNS查閱工具](https://www.ultratools.com/tools/dnsLookup) 可用。 Google DoH可用來查閱TXT記錄項目，以及識別TXT記錄是否遺失或錯誤。
