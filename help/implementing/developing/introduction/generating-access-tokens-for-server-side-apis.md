---
title: 產生伺服器端API的存取Token
description: 瞭解如何透過產生安全的JWT Token，以促進協力廠商伺服器與AEM之間的雲端服務通訊
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# 簡介 {#introduction}

>[!IMPORTANT]
>
>此功能尚未提供。 如需功能的最新清單，請參閱[發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

有些架構依賴於從AEM基礎架構以外伺服器上裝載的應用程式，以雲端服務的形式呼叫AEM。 例如，呼叫伺服器的行動應用程式，接著會以雲端服務的形式向AEM提出API要求。

伺服器對伺服器的流程說明如下，以及簡化的開發流程。 AEM(Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console))可用來產生驗證程式所需的Token。

## 伺服器到伺服器流{#the-server-to-server-flow}

具有管理員角色的使用者可產生JWT承載Token，此Token應安裝在伺服器上，並應謹慎視為機密金鑰。 JWT載體Token應與IMS交換以取得存取Token，此存取Token應包含在對AEM的雲端服務要求中。

伺服器對伺服器的流程包含下列步驟：

* 從開發人員主控台產生JWT承載Token
* 在非AEM伺服器上安裝Token，以呼叫AEM
* 使用Adobe的IMS API，將JWT載體Token交換為存取Token
* 呼叫AEM API

### 生成JWT承載令牌{#generating-the-jwt-bearer-token}

具有組織管理員角色的使用者，將會在特定環境的開發人員主控台中看到整合標籤，以及兩個按鈕。 按一下&#x200B;**獲取服務憑據**&#x200B;按鈕將生成私鑰、證書和配置。

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

### 在非AEM伺服器上安裝Token {#install-the-token-on-a-non-aem-server}

呼叫AEM的非AEM應用程式應安裝JWT記載權杖，將它視為機密。

### 將JWT Token交換為存取Token {#exchange-the-jwt-token-for-an-access-token}

將JWT Token加入Adobe IMS服務的呼叫中，以擷取有效期為24小時的存取Token。

### 呼叫AEM API {#calling-the-aem-api}

將適當的伺服器對伺服器API呼叫作為雲端服務環境，包括標題中的存取Token。 因此，對於「授權」標題，請使用值`"Bearer <access_token>"`。

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

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

## JWT Bearer Token Revocation {#jwt-bearer-token-revocation}

如果JWT承載權杖需要撤銷，請向客戶支援提交請求。