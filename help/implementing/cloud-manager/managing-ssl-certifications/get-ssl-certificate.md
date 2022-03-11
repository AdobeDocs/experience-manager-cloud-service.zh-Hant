---
title: 獲取SSL證書 — 管理SSL證書
description: 獲取SSL證書 — 管理SSL證書
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 獲取SSL證書 {#getting-an-ssl-certificate}

企業使用SSL證書來保護其網站，並允許其客戶信任他們。 為了使用SSL協定，Web伺服器需要使用SSL證書。 雲管理器不提供SSL證書或私鑰。 必須從認證機構(CA)獲得。

當實體從證書頒發機構請求證書時，CA將完成驗證過程。 這可以從驗證域名控制到收集公司註冊文檔和訂閱者協定。 一旦驗證了實體的資訊，CA將使用CA的私鑰簽名其公鑰。 由於所有主要證書頒發機構在Web瀏覽器中都有根證書，因此將通過 *信任鏈* 而Web瀏覽器會將其識別為可信證書。

>[!NOTE]
>AEMas a Cloud Service只接受OV（組織驗證）或EV（擴展驗證）證書。 不接受DV（域驗證）或自簽名證書。 OV和EV證書為用戶提供額外的、經CA驗證的資訊，他們可以使用這些資訊來確定網站的所有者、電子郵件的發送者或可執行代碼或PDF文檔的數字簽字者是否可信。 DV證書是通用的，價格便宜。 但是，它們不允許所有權驗證。
>此外，任何證書都必須是來自受信任證書頒發機構(CA)的X.509 TLS證書，其中具有匹配的2048位RSA私鑰。
