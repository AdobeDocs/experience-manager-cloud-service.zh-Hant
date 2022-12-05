---
title: 新增 TXT 記錄
description: 了解如何新增 TXT 記錄以在雲管理器中新增自訂網域名稱。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# 新增 TXT 記錄 {#adding-txt}

DNS TXT 記錄授權將域託管在 CDN 服務中。您必須在授權雲管理器使用自訂域部署 CDN 服務並將其與後端服務關聯的區域中建立 DNS TXT 記錄。此關聯完全在您的控制之下，並授權 Cloud Manager 將內容從服務提供給網域。這種授權可以被授予也可以被撤銷。TXT 記錄特定於域和 Cloud Manager 環境。

在新增 TXT 記錄之前，您必須滿足這些要求。

* 您必須能夠修改組織網域的 DNS 記錄，或聯繫可以修改的適當人員。
* 如果您還不知道您的網域名稱主機服務商或註冊商，則必須確定它。

當您啟動域驗證時，Cloud Manager 會為您提供用於驗證的名稱和 TXT 值。使用指定的名稱和值將 TXT 記錄新增到您域的 DNS 伺服器。

1. 登入您的網域主持機構並找到 DNS 記錄區段。
1. 新增`_aemverification.[yourdomainname]`作為&#x200B;**姓名**&#x200B;值，並新增 TXT 值，就像它顯示的一樣。

請參考此表的範例。

| 網域 | 名稱 | TXT 數值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製 Cloud Manager UI 中顯示的整個值。這是特定於網域和環境的。例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 複製 Cloud Manager UI 中顯示的整個值。這是特定於網域和環境的。例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完成後，您可以透過執行以下命令來驗證結果

```shell
dig _aemverification.[yourdomainname] -t txt
```

預期結果應顯示 Cloud Manager UI 中提供的 TXT 值。

例如，如果您的網域是 `example.com`，然後執行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有許多可用的 [DNS 查找工具](https://www.ultratools.com/tools/dnsLookup)。Google DoH 可用於查找 TXT 記錄項目並識別 TXT 記錄是否遺失或錯誤。
