---
title: 驗證域
description: 驗證域
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 驗證域 {#verify-domain-name}

DNS TXT記錄會授權網域以裝載於CDN服務中。 客戶必須在授權Cloud Manager的區域中建立DNS TXT記錄，以便將CDN服務與自訂網域部署，並將其與後端服務建立關聯。 此關聯完全由客戶控制，並強烈授權Cloud Manager將內容從服務提供至網域。 這項授權既可授予，也可撤回。 TXT記錄是特定於域和Cloud Manager環境的。

1. 登入您的網域主機，並造訪DNS記錄區段。
1. 將TXT項目複製並貼至您自訂網域所在的DNS區域，完全如出一轍。 如果您需要輸入「名稱」，請提供該名稱 `@`。

>[!NOTE]
>各種DNS查閱工具(例如 [DNS查閱工具](https://www.ultratools.com/tools/dnsLookup)、Google DoH)都可用來查閱TXT記錄項目，並識別TXT記錄是否遺失或錯誤。
