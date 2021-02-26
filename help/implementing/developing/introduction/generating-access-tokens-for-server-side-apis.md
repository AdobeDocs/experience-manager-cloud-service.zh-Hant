---
title: 產生伺服器端API的存取Token
description: 瞭解如何透過產生安全的JWT Token，促進協AEM力廠商伺服器與Cloud Service之間的通訊
translation-type: tm+mt
source-git-commit: 41b4bb3a63089c05750a40e910ee7578727d8b15
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---


# 簡介 {#introduction}

有些架構依賴於從位於基礎架AEM構外部伺服器上的應用程式，以Cloud Service的形式呼叫AEM。 例如，呼叫伺服器的行動應用程式，接著會以Cloud Service的形AEM式提出API要求。

伺服器對伺服器的流程說明如下，以及簡化的開發流程。 作AEM為Cloud Service[開發人員控制台](development-guidelines.md#crxde-lite-and-developer-console)用於生成驗證過程所需的令牌。

>[!NOTE]
>
>除了本檔案外，您也可以參閱[Token型驗證的教學課程，以AEM做為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)。

## 伺服器到伺服器流{#the-server-to-server-flow}

具有IMS組織管理員角色的用戶可以生成作為Cloud Service憑據的用戶，該證書隨後可由具有AEMCloud Service環境管理員角色的用戶檢索，並且應該安裝在伺服器上，並需要謹慎地作為密鑰處理。 此JSON格式檔案包含與Cloud ServiceAPI整合所需AEM的所有資料。 該資料用於建立與IMS交換的已簽名JWT令牌，以用於IMS訪問令牌。 然後，此存取Token可用作「承載」驗證Token，以AEM做為Cloud Service。

伺服器對伺服器的流程包含下列步驟：

* 從Developer ConsoleAEM擷取Cloud Service憑證
* 在非伺服AEM器上，以Cloud Service憑證的形式安AEM裝至
* 產生JWT Token，並使用Adobe的IMS API將該Token交換為存取Token。
* 以存取AEMToken作為承載驗證Token呼叫API
* 為環境中的技術帳戶用戶設定適當的權AEM限

### 將AEM作為Cloud Service憑據{#fetch-the-aem-as-a-cloud-service-credentials}

以Cloud Service開發人員主控AEM台身分存取的使用者，將會看到「開發人員主控台」中針對特定環境的整合標籤，以及兩個按鈕。 具有「Cloud Service環境管理員」角色的用戶可以按一下「獲取服務憑據」按鈕來顯示服務憑據json，該憑據將包含非伺服器所需的所有資訊（包括客戶端ID、客戶機密鑰、私鑰、證書和環境的作者和發佈層的配置），而不考慮選擇Pod。****

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

>[!IMPORTANT]
>
>IMS組織管理員（通常是透過Cloud Manager布建環境的相同使用者）必須先存取Developer Console，然後按一下「取得服務認證」按鈕，才能產生認證，然後由具有Cloud Service環境管理權限的使用者AEM擷取。 ****&#x200B;如果IMS組織管理員尚未執行此動作，會收到訊息通知他們需要IMS組織管理員角色。

### 在非服AEM務器&lt;a0/AEM>上安裝服務憑據{#install-the-aem-service-credentials-on-a-non-aem-server}

呼叫的非AEM應用程式應AEM該能夠以Cloud Service憑證AEM的形式存取，將其視為機密。

### 產生JWT Token並將它交換為存取Token{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在呼叫Adobe的IMS服務時，使用憑證來建立JWT Token，以擷取存取Token，此Token的有效期為24小時。

CSAEM服務認證可使用為此目的而設計的用戶端程式庫來交換為存取Token。 客戶端庫可從[Adobe的公共GitHub儲存庫](https://github.com/adobe/aemcs-api-client-lib)獲得，其中包含更詳細的指導和最新資訊。

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

存取Token會定義其過期的時間，通常為24小時。 Git儲存庫中有范常式式碼，可管理存取Token並在存取Token過期前加以重新整理。

### 呼叫AEMAPI {#calling-the-aem-api}

將適當的伺服器對伺服器API呼叫當做AEMCloud Service環境，包括標題中的存取Token。 因此，對於「授權」標題，請使用值`"Bearer <access_token>"`。 例如，使用`curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在{#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}中為技術帳戶用戶設定AEM適當的權限

在中建立技術帳戶使用者(這發生在第一個具有AEM相應存取Token的請求之後)後，技術帳戶使用者必須在&#x200B;**中獲得適當的權限AEM。**

請注意，在AEM Author服務中，技術帳戶使用者依預設會新增至提供讀取存取權的「參與者」使用者群AEM組。

中的此技術帳戶使AEM用者可使用一般方法，以權限進一步付費。

## 開發人員流程{#developer-flow}

開發人員可能會想要使用其非應用程式的開發執行個體AEM（在其膝上型電腦或代管上執行）進行測試，以要求將開發當成AEMCloud Service開發環境。 但是，由於開發人員不一定擁有IMS管理員角色權限，因此我們不能假設他們可以產生一般伺服器對伺服器流程中所描述的JWT載體。 因此，我們提供一種機制，讓開發人員直接產生存取Token，該存取Token可用於要求，AEM做為他們可存取的Cloud Service環境。

如需使用Cloud Service開發人員主控台所需權限的詳細資訊，請參閱[開發人員指南檔案&lt;a1/AEM>。](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)

>[!NOTE]
>
>本機開發存取Token的有效期上限為24小時，之後必須使用相同的方法重新產生。

開發人員可使用此Token，從其非測試應用程AEM式呼叫AEM至Cloud Service環境。 通常，開發人員會將此Token與非應用程式搭配使用AEM在自己的筆記型電腦上。 此外，AEM雲通常是非生產環境。

開發人員流程包含下列步驟：

* 從Developer Console產生存取Token
* 使用存取AEMToken呼叫應用程式。

開發人員也可以對在本機AEM電腦上執行的專案進行API呼叫，在此情況下不需要存取Token。

### 產生存取Token {#generating-the-access-token}

按一下「開發人員主控台」中的「取得本機開發Token **」按鈕，產生存取Token。**

### 然後呼AEM叫使用存取Token {#call-the-aem-application-with-an-access-token}的應用程式

將非應用程式的伺服器對伺服器API呼AEM叫作Cloud ServiceAEM環境，包括標題中的存取Token。 因此，對於「授權」標題，請使用值`"Bearer <access_token>"`。

## 服務憑據撤銷{#service-credentials-revocation}

如果需要撤銷憑證，您需要使用下列步驟向客戶支援提交請求：

1. 在用戶介面中禁用Adobe Admin Console的技術帳戶用戶：
   * 在Cloud Manager中，按&#x200B;**...**&#x200B;按鈕。 這會開啟產品設定檔頁面
   * 現在，按一下&#x200B;**AEM Users**&#x200B;設定檔，以顯示使用者清單
   * 按一下「**API認證**」標籤，然後尋找適當的技術帳戶使用者並加以刪除
2. 聯絡客戶支援，並要求刪除該特定環境的服務認證
3. 最後，您可以再次產生憑證，如本檔案所述。 同時，請確定所建立的新技術帳戶使用者擁有適當的權限。