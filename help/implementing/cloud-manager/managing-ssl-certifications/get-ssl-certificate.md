---
title: 取得SSL憑證——管理SSL憑證
description: 取得SSL憑證——管理SSL憑證
translation-type: tm+mt
source-git-commit: 40119f7b3bdf36af668b79afbcb2802a0b2a6033
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 取得SSL憑證{#getting-an-ssl-certificate}

企業使用SSL憑證來保護其網站的安全，並讓客戶信任他們。 為了使用SSL協定，Web伺服器需要使用SSL證書。 Cloud Manager不提供SSL憑證或私密金鑰。 您必須向認證授權機構(CA)取得這些授權。

當實體向認證機構要求認證時，CA會完成驗證程式。 這包括驗證網域名稱控制，以及收集公司註冊檔案和訂閱者合約。 在實體的資訊經過驗證後，CA將使用CA的私密金鑰簽署其公開金鑰。 由於所有主要憑證授權機構在Web瀏覽器中都有根憑證，因此實體的憑證將透過&#x200B;*信任鏈*&#x200B;連結，而網頁瀏覽器會將其辨識為受信任的憑證。

>[!NOTE]
>AEM做為雲端服務將只接受OV（組織驗證）或EV（延伸驗證）憑證。 不接受DV（網域驗證）或自簽證書。 OV和EV憑證可為使用者提供額外、經CA驗證的資訊，供他們用來判斷網站擁有者、電子郵件寄件者或可執行程式碼或PDF檔案的數位簽章者是否可信。 DV憑證是通用且便宜的。 但是，它們不允許所有權驗證。
>此外，任何憑證都必須是來自受信任認證機構(CA)的X.509 TLS憑證，且具備相符的2048位元RSA私密金鑰。

