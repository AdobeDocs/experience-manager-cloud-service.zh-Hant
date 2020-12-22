---
title: 產生伺服器端API的存取Token
description: 瞭解如何透過產生安全的JWT Token，以促進協力廠商伺服器與AEM之間的雲端服務通訊
translation-type: tm+mt
source-git-commit: 7ca7cd458ea5152d56754bf1e6a500b2c04d0039
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# 簡介 {#introduction}

>[!IMPORTANT]
>
>此功能尚未提供。 如需功能的最新清單，請參閱[發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

有些架構依賴於從AEM基礎架構以外伺服器上裝載的應用程式，以雲端服務的形式呼叫AEM。 例如，呼叫伺服器的行動應用程式，接著會以雲端服務的形式向AEM提出API要求。

伺服器對伺服器的流程說明如下，以及簡化的開發流程。 AEM(Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console))可用來產生驗證程式所需的Token。

## 伺服器到伺服器流{#the-server-to-server-flow}

具有管理員角色的使用者可以產生AEM做為Cloud Service憑證，此憑證應安裝在伺服器上，並應謹慎視為機密金鑰。 此JSON格式檔案包含與AEM整合為雲端服務API所需的所有資料。 該資料用於建立與IMS交換的已簽名JWT令牌，以用於IMS訪問令牌。 接著，此存取Token可用作「載體」驗證Token，以Cloud Service的身分向AEM提出請求。

伺服器對伺服器的流程包含下列步驟：

* 從Developer Console擷取AEM做為Cloud Service憑證
* 將AEM安裝為對AEM進行呼叫的非AEM伺服器上的雲端服務憑證
* 產生JWT Token，並使用Adobe的IMS API將該Token交換為存取Token。
* 以存取Token作為承載驗證Token呼叫AEM API

### 將AEM擷取為雲端服務憑證{#fetch-the-aem-as-a-cloud-service-credentials}

具有IMS組織管理員角色的使用者，將會在特定環境的「開發人員主控台」中看到整合標籤，以及兩個按鈕。 按一下「取得服務認證&#x200B;**」按鈕，將會產生服務認證json，其中包含非AEM伺服器所需的所有資訊，包括用戶端ID、用戶端密碼、私密金鑰、憑證，以及環境作者與發佈層的設定，不論選擇何種pod。**

![JWT Generation](assets/JWTtoken3.png)

輸出將類似於：

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

### 在非AEM伺服器{#install-the-aem-service-credentials-on-a-non-aem-server}上安裝AEM服務認證

呼叫AEM的非AEM應用程式應能以雲端服務認證的形式存取AEM，將其視為機密。

### 產生JWT Token並將它交換為存取Token{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在呼叫Adobe IMS服務時，使用認證來建立JWT Token，以擷取有效期為24小時的存取Token。

AEM-CS服務認證可使用專為此目的而設計的用戶端程式庫，來交換為存取Token。 用戶端程式庫可從[Adobe的公用GitHub存放庫](https://github.com/adobe/aemcs-api-client-lib)取得，其中包含更詳細的指引和最新資訊。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

同樣的交換可以用任何能夠生成具有正確格式的簽名的JWT令牌並調用IMS令牌交換API的語言來執行。

存取Token會在過期時定義，通常為12h。 Git儲存庫中有范常式式碼，可管理存取Token並在存取Token過期前加以重新整理。

### 呼叫AEM API {#calling-the-aem-api}

將適當的伺服器對伺服器API呼叫作為雲端服務環境，包括標題中的存取Token。 因此，對於「授權」標題，請使用值`"Bearer <access_token>"`。 例如，使用`curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

## 開發人員流程{#developer-flow}

開發人員可能會想要使用其非AEM應用程式的開發執行個體進行測試（可在其膝上型電腦或代管上執行），以要求將開發AEM當成雲端服務開發環境。 但是，由於開發人員不一定擁有AEM的管理員角色存取權，因此我們無法假設他們可以產生一般伺服器對伺服器流程中所述的JWT載體。 因此，我們提供一種機制，讓開發人員直接產生存取Token，以便在對AEM的要求（即他們可存取的雲端服務環境）中使用。 如需將AEM用作雲端服務開發人員主控台的必要權限，請參閱[開發人員准則檔案](/help/implementing/developing/introduction/development-guidelines.md)。

>[!NOTE]
>
>代號的有效期為24小時，之後必須使用相同的方法重新產生。

開發人員可使用此Token，從其非AEM測試應用程式，以雲端服務環境的形式呼叫AEM。 通常，開發人員會將此Token與非AEM應用程式搭配使用於其膝上型電腦。 此外，AEM as a Cloud通常是非生產環境。

開發人員流程包含下列步驟：

* 從Developer Console產生存取Token
* 使用存取Token呼叫AEM應用程式。

開發人員也可以對在本機電腦上執行的AEM專案進行API呼叫，在此情況下不需要存取Token。

### 產生存取Token {#generating-the-access-token}

按一下「開發人員主控台」中的「取得本機開發Token **」按鈕，產生存取Token。**

### 然後使用存取Token {#call-the-aem-application-with-an-access-token}呼叫AEM應用程式

將非AEM應用程式的伺服器對伺服器API呼叫，以雲端服務環境的形式傳送至AEM，包括標題中的存取Token。 因此，對於「授權」標題，請使用值`"Bearer <access_token>"`。

## 服務憑據撤銷{#service-credentials-revocation}

如果JWT承載權杖需要撤銷，請向客戶支援提交請求。