---
title: 驗證域
description: 驗證域
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 驗證域{#verify-domain-name}

DNS TXT記錄會授權網域以在CDN服務中托管。 客戶必須在授權Cloud Manager部署CDN服務與自訂網域，並將其與後端服務建立關聯的區域中建立DNS TXT記錄。 此關聯完全由客戶控制，並強烈授權Cloud Manager將內容從服務提供至網域。 該授權可被授予，也可被撤回。 TXT記錄專屬於網域和Cloud Manager環境。

1. 登入您的網域主機，並造訪DNS記錄區段。
1. 複製TXT項目並貼到自訂網域所在的DNS區域，與其顯示完全相同。 如果條目需要「name」，請將其`@`。

>[!NOTE]
>各種DNS查閱工具，例如[DNS查閱工具](https://www.ultratools.com/tools/dnsLookup)、Google DoH，可用來查閱TXT記錄項目，並識別TXT記錄是否遺失或錯誤。
