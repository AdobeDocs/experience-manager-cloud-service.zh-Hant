---
title: 添加TXT記錄
description: 添加自定義域名
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: f7688559a791281d0e157dd1d48a5f63568914f5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 添加TXT記錄 {#adding-txt}

DNS TXT記錄授權域在CDN服務中托管。 客戶必須在授權Cloud Manager將CDN服務與自定義域部署並將其與後端服務關聯的區域中建立DNS TXT記錄。 此關聯完全由客戶控制，並強烈授權雲管理器將內容從服務提供到域。 這項授權可予批准，也可予撤回。

在建立TXT記錄之前，您可以按照以下步驟操作：

* 能夠修改組織域的DNS記錄，或聯繫可以這樣做的適當人員。
* 如果您尚不知道域主機或註冊器，請確定它。

啟動域驗證時，Cloud Manager會為您提供用於驗證的名稱和TXT值。 使用指定的名稱和值將TXT記錄添加到域的DNS伺服器。

1. 登錄到域主機並訪問DNS記錄部分。
1. 添加 `_aemverification.[yourdomainname]` 作為「名稱」(Name)，並按照顯示的方式添加TXT值。
請參閱下表中的示例。

| 網域 | 名稱 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製Cloud Manager UI中顯示的整個值。 這特定於域和環境。 例如：<br>*adobe-aem-verification=<br>示例.com/[程式]/[環境]/..* |
| `www.example.com` | `_aemverification.www.example.com` | 複製Cloud Manager UI中顯示的整個值。 這特定於域和環境。 例如：<br>*adobe-aem-verification=<br>www.example.com[程式]/[環境]/..* |

完成後，可以通過運行以下命令來驗證結果： `dig _aemverification.[yourdomainname] -t txt`。
預期結果應顯示Cloud Manager UI中提供的TXT值。

例如，如果域 `example.com`，然後運行： `dig TXT _aemverification.example.com -t txt`。

>[!NOTE]
>還有各種各樣的 [DNS查找工具](https://www.ultratools.com/tools/dnsLookup),GoogleDoH可用於查找TXT記錄條目並確定TXT記錄是丟失還是錯誤。
