---
title: 取得SSL憑證 — 管理SSL憑證
description: 取得SSL憑證 — 管理SSL憑證
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 取得SSL憑證{#getting-an-ssl-certificate}

企業使用SSL憑證來保護其網站的安全，並讓客戶信任他們。 若要使用SSL通訊協定，Web伺服器需要使用SSL憑證。 Cloud Manager不提供SSL憑證或私密金鑰。 必須從認證機構(CA)取得。

當實體向證書頒發機構請求證書時，CA將完成驗證過程。 從驗證域名控制到收集公司註冊文檔和訂閱者協定，都可以。 一旦實體的資訊被驗證後，CA將使用CA的私鑰簽署其公鑰。 因為所有主要憑證授權單位在Web瀏覽器中都有根憑證，實體的憑證將透過&#x200B;*信任鏈*&#x200B;連結，而Web瀏覽器會將其識別為信任憑證。

>[!NOTE]
>AEM as aCloud Service只會接受OV（組織驗證）或EV（延伸驗證）憑證。 不接受DV（域驗證）或自簽名證書。 OV和EV證書為用戶提供了經過CA驗證的額外資訊，用戶可以用這些資訊來判斷網站的所有者、電子郵件的發送者，或可執行代碼或PDF文檔的數字簽字者是否值得信賴。 DV證書是通用且便宜的。 但是，它們不允許進行所有權驗證。
>此外，任何證書都必須是來自受信任認證機構(CA)的X.509 TLS證書，且具有相符的2048位RSA私鑰。
