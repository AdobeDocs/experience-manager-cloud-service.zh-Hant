---
title: 取得SSL憑證——管理SSL憑證
description: 取得SSL憑證——管理SSL憑證
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 取得SSL憑證{#getting-an-ssl-certificate}

企業使用SSL憑證來保護其網站的安全，並讓客戶信任他們。 為了使用SSL協定，Web伺服器需要使用SSL證書。 Cloud Manager不提供SSL憑證或私密金鑰。 您必須向認證授權機構(CA)取得這些授權。

當實體向認證機構(CA)要求認證時，CA完成驗證程式。 這包括驗證網域名稱控制，以及收集公司註冊檔案和訂閱者合約。

在實體的資訊經過驗證後，CA將使用CA的私密金鑰簽署其公開金鑰。 由於所有主要憑證授權機構在Web瀏覽器中都有根憑證，因此實體的憑證將透過&#x200B;*信任鏈*&#x200B;連結，而網頁瀏覽器會將其辨識為受信任的憑證。

