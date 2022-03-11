---
title: 驗證域
description: 驗證域
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 驗證域 {#verify-domain-name}

DNS TXT記錄授權域在CDN服務中托管。 客戶必須在授權Cloud Manager將CDN服務與自定義域部署並將其與後端服務關聯的區域中建立DNS TXT記錄。 此關聯完全由客戶控制，並強烈授權雲管理器將內容從服務提供到域。 這項授權可予批准，也可予撤回。 TXT記錄特定於域和雲管理器環境。

1. 登錄到域主機並訪問DNS記錄部分。
1. 複製並貼上自定義域所在的DNS區域中的TXT條目，與其顯示的完全相同。 如果你需要輸入「名稱」，請輸入 `@`。

>[!NOTE]
>各種DNS查找工具，如 [DNS查找工具](https://www.ultratools.com/tools/dnsLookup),GoogleDoH可用於查找TXT記錄條目並確定TXT記錄是丟失還是錯誤。
