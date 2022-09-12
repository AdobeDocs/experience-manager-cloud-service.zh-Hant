---
title: 產生伺服器端API的存取權杖
description: 了解如何產生安全的JWT代號，以便利第三方伺服器與AEMas a Cloud Service之間的通訊
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: fc49b004a61d5f981ac61cca684dc0bacf843443
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# 簡介 {#introduction}

有些架構依賴從AEM基礎架構外的伺服器上托管的應用程式對AEM進行as a Cloud Service的呼叫。 例如，呼叫伺服器的行動應用程式，接著會向AEMas a Cloud Service提出API請求。

伺服器對伺服器的流程及簡化的開發流程如下所述。 AEMas a Cloud Service [開發人員控制台](development-guidelines.md#crxde-lite-and-developer-console) 用來產生驗證程式所需的權杖。

>[!NOTE]
>
>除了本檔案外，您也可以參閱 [AEMas a Cloud Service的Token型驗證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) 和 [取得整合的登入Token](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html).

## 伺服器對伺服器流量 {#the-server-to-server-flow}

擁有IMS組織管理員角色的使用者，以及AEM作者上AEM使用者或AEM管理員產品設定檔的成員，可以產生AEMas a Cloud Service憑證。 該憑證隨後可由具有AEMas a Cloud Service環境管理員角色的使用者擷取，並應安裝在伺服器上，且需要謹慎處理為機密金鑰。 此JSON格式檔案包含與AEMas a Cloud Service API整合所需的所有資料。 資料可用來建立已簽署的JWT代號，此代號會與IMS交換以取得IMS存取代號。 然後，此存取權杖可作為承載驗證權杖，以向AEMas a Cloud Service提出請求。 憑證預設會在一年後到期，但如有需要，可依說明重新整理 [此處](#refresh-credentials).

伺服器對伺服器流程涉及下列步驟：

* 從開發人員控制台擷取AEMas a Cloud Service憑證
* 在對AEM進行呼叫的非AEM伺服器上安裝AEMas a Cloud Service憑證
* 使用Adobe的IMS API產生JWT代號，並交換存取代號的代號
* 使用存取權杖作為承載驗證權杖來呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的權限

### 擷取AEMas a Cloud Service憑證 {#fetch-the-aem-as-a-cloud-service-credentials}

具有AEMas a Cloud Service開發人員控制台存取權的使用者會在指定環境的開發人員控制台中看到整合索引標籤，以及兩個按鈕。 具有AEMas a Cloud Service環境管理員角色的使用者可以按一下 **生成服務憑據** 按鈕來產生和顯示服務憑證json，其中包含非AEM伺服器所需的所有資訊，包括用戶端id、用戶端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論選擇何種pod。

![JWT產生](assets/JWTtoken3.png)

輸出將類似於以下內容：

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

產生憑證後，稍後可按下 **獲取服務憑據** 按鈕。

>[!IMPORTANT]
>
>IMS組織管理員（通常是透過Cloud Manager布建環境的相同使用者）也應是AEM作者上AEM使用者或AEM管理員產品設定檔的成員，必須先存取開發人員主控台，然後按一下 **生成服務憑據** 按鈕，以便具有AEMas a Cloud Service環境管理權限的使用者產生並稍後擷取憑證。 如果IMS組織管理員尚未執行此動作，系統會傳送訊息通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務憑證 {#install-the-aem-service-credentials-on-a-non-aem-server}

對AEM發出呼叫的非AEM應用程式應能存取AEMas a Cloud Service憑證，並將其視為機密。

### 產生JWT代號並交換它以取得存取代號 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在呼叫Adobe的IMS服務時使用憑證建立JWT代號，以擷取有效期為24小時的存取代號。

AEM CS服務憑證可使用為此目的而設計的用戶端程式庫，以取代存取權杖。 用戶端程式庫可從 [Adobe的公用GitHub存放庫](https://github.com/adobe/aemcs-api-client-lib)，包含更詳細的指引和最新資訊。

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

同樣的交換可以以任何語言執行，這些語言能夠以正確的格式產生簽名的JWT令牌並調用IMS令牌交換API。

存取權杖會在何時過期（通常為24小時）加以定義。 Git存放庫中有范常式式碼，可管理存取權杖，並在存取權杖過期前重新整理。

### 呼叫AEM API {#calling-the-aem-api}

對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標題中的存取權杖。 因此，對於「授權」標題，請使用值 `"Bearer <access_token>"`. 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的權限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在AEM中建立技術帳戶使用者後（這會發生在具有對應存取權杖的第一個請求之後），技術帳戶使用者必須獲得適當的權限 **in** AEM。

請注意，依預設，在AEM Author服務中，技術帳戶使用者會新增至提供讀取存取權AEM的貢獻者使用者群組。

AEM中的此技術帳戶使用者可使用一般方法進一步布建權限。

## 開發人員流程 {#developer-flow}

開發人員可能會想使用其非AEM應用程式的開發例項（在筆記型電腦上執行或托管）進行測試，以向開發AEMas a Cloud Service開發環境提出請求。 不過，由於開發人員不一定擁有IMS管理員角色權限，因此我們無法假設他們可以產生一般伺服器對伺服器流程中所述的JWT承載。 因此，我們提供一種機制，讓開發人員直接產生存取權杖，該權杖可用於他們可存取的AEMas a Cloud Service環境的要求中。

請參閱 [開發人員准則檔案](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 如需使用AEMas a Cloud Service開發人員控制台所需權限的相關資訊。

>[!NOTE]
>
>本機開發存取權杖的有效期最長為24小時，之後必須使用相同的方法重新產生。

開發人員可使用此代號，從其非AEM測試應用程式對AEMas a Cloud Service環境進行呼叫。 通常，開發人員會在自己的筆記型電腦上，將此代號與非AEM應用程式搭配使用。 此外，AEM as a Cloud通常是非生產環境。

開發人員流程包含下列步驟：

* 從開發人員控制台產生存取權杖
* 使用存取權杖呼叫AEM應用程式。

開發人員也可以對在其本機電腦上執行的AEM專案進行API呼叫，在此情況下就不需要存取權杖。

### 產生存取權杖 {#generating-the-access-token}

按一下 **取得本機開發代號** 按鈕，產生存取權杖。

### 然後使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEMas a Cloud Service環境進行適當的伺服器對伺服器API呼叫，包括標題中的存取權杖。 因此，對於「授權」標題，請使用值 `"Bearer <access_token>"`.

## 刷新憑據 {#refresh-credentials}

依預設，AEMas a Cloud Service憑證會在一年後到期。 為確保服務連續性，開發人員可以選擇刷新憑據，將其可用性延長一年。

若要達成此目標，您可以使用 **刷新服務憑據** 按鈕 **整合** 標籤，如下所示。

![憑據刷新](assets/credential-refresh.png)

按下按鈕後，會產生一組新的認證。 您可以使用新憑證更新機密儲存空間，並驗證其是否正常運作。

>[!NOTE]
>
> 按一下 **刷新服務憑據** 按鈕時，舊憑證會一直註冊到過期為止，但只有最新的憑證集可供開發人員控制台隨時檢視。

## 服務憑據吊銷 {#service-credentials-revocation}

如果需要撤銷憑證，您需要使用下列步驟向客戶支援提交請求：

1. 在使用者介面中停用Adobe Admin Console的技術帳戶使用者：
   * 在Cloud Manager中，按 **...** 按鈕。 這會開啟產品設定檔頁面
   * 現在，按一下 **AEM使用者** 設定檔，以顯示使用者清單
   * 按一下 **API憑證** 頁簽，然後找到相應的技術帳戶用戶並將其刪除
2. 請連絡客戶支援，並要求刪除該特定環境的服務憑證
3. 最後，您可以再次產生憑證，如本檔案所述。 同時，請確定所建立的新技術帳戶使用者擁有適當的權限。
