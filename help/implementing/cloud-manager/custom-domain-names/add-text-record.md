---
title: 添加TXT記錄
description: 瞭解如何添加TXT記錄以在雲管理器中添加自定義域名。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 添加TXT記錄 {#adding-txt}

DNS TXT記錄授權域在CDN服務中托管。 您必須在授權Cloud Manager將CDN服務與自定義域部署並將其與後端服務關聯的區域中建立DNS TXT記錄。 此關聯完全由您控制，並授權Cloud Manager將內容從服務提供到域。 這項授權可以授予，也可以撤回。 TXT記錄特定於域和雲管理器環境。

添加TXT記錄前必須滿足這些要求。

* 您必須能夠修改組織域的DNS記錄，或與可以聯繫的相應人員聯繫。
* 如果您尚不知道域主機或註冊器，則必須標識它。

啟動域驗證時，Cloud Manager會為您提供用於驗證的名稱和TXT值。 使用指定的名稱和值將TXT記錄添加到域的DNS伺服器。

1. 登錄到域主機並查找DNS記錄部分。
1. 添加 `_aemverification.[yourdomainname]` 的 **名稱** 值，並按照顯示的方式添加TXT值。

請參閱本表中的示例。

| 網域 | 名稱 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製Cloud Manager UI中顯示的整個值。 這特定於域和環境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 複製Cloud Manager UI中顯示的整個值。 這特定於域和環境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完成後，可以運行以下命令來驗證結果

```shell
dig _aemverification.[yourdomainname] -t txt
```

預期結果應顯示Cloud Manager UI中提供的TXT值。

例如，如果域 `example.com`，然後運行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有 [DNS查找工具](https://www.ultratools.com/tools/dnsLookup) 的下界。 GoogleDoH可用於查找TXT記錄條目並確定TXT記錄是丟失還是錯誤。
