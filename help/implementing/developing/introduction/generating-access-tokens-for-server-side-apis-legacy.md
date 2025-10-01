---
title: 為伺服器端API產生存取權杖（舊版）
description: 瞭解如何產生安全JWT權杖，以促進第三方伺服器與AEM as a Cloud Service之間的通訊
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# 為伺服器端API產生存取權杖（舊版） {#generating-access-tokens-for-server-side-apis-legacy}

有些架構需仰賴從託管於AEM as a Cloud Service基礎架構以外之伺服器上的應用程式呼叫AEM。 例如，行動應用程式，它會呼叫伺服器，然後向AEM as a Cloud Service發出API請求。

伺服器對伺服器的流程如下所述，以及簡化的開發流程。 AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console)是用來產生驗證程式所需的權杖。

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=zh-Hant#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器對伺服器流量 {#the-server-to-server-flow}

具有IMS組織管理員角色，並且也是AEM Author上的AEM使用者或AEM管理員產品設定檔成員的使用者，可以產生AEM as a Cloud Service認證。 具有AEM as a Cloud Service環境管理員角色的使用者稍後可以擷取該認證，且應安裝在伺服器上，並且需要謹慎將其視為機密金鑰。 此JSON格式檔案包含與AEM as a Cloud Service API整合所需的所有資料。 資料可用來建立已簽署的JWT權杖，該權杖會與IMS交換以取得IMS存取權杖。 然後，可將此存取權杖用作持有者驗證權杖，以向AEM as a Cloud Service提出請求。 認證預設在一年後到期，但可視需要重新整理，請參閱[重新整理認證](#refresh-credentials)。

伺服器對伺服器流程涉及以下步驟：

* 從Developer Console擷取AEM as a Cloud Service的認證
* 在呼叫AEM as a Cloud Service的非AEM伺服器上安裝AEM的認證
* 產生JWT權杖並使用Adobe的IMS API將該權杖交換為存取權杖
* 使用存取權杖作為持有者驗證權杖呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的許可權

### 擷取AEM as a Cloud Service認證 {#fetch-the-aem-as-a-cloud-service-credentials}

有權存取AEM as a Cloud Service開發人員控制檯的使用者會看到指定環境的Developer Console中的整合功能索引標籤和兩個按鈕。 具有AEM as a Cloud Service環境管理員角色的使用者可以按一下&#x200B;**產生服務認證**&#x200B;按鈕，以產生並顯示服務認證json。 json包含非AEM伺服器所需的所有資訊，包括使用者端ID、使用者端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論Pod選取範圍為何。

![JWT產生](assets/JWTtoken3.png)

輸出類似以下內容：

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

產生認證之後，稍後可以按相同位置的&#x200B;**取得服務認證**&#x200B;按鈕來擷取認證。

>[!IMPORTANT]
>
>IMS組織管理員(通常是透過Cloud Manager布建環境的使用者)也應是AEM Author上的AEM使用者或AEM管理員產品設定檔的成員，可存取Developer Console。 接著，他們必須按一下&#x200B;**產生服務認證**&#x200B;按鈕，才能產生認證，且稍後再由具有AEM as a Cloud Service環境管理員許可權的使用者擷取。 如果IMS組織管理員尚未完成此任務，則會出現一則訊息，通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務認證 {#install-the-aem-service-credentials-on-a-non-aem-server}

呼叫AEM的非AEM應用程式應能存取AEM as a Cloud Service的認證，並將其視為秘密。

### 產生JWT權杖並將其交換為存取權杖 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

使用認證在呼叫Adobe的IMS服務中建立JWT權杖以擷取存取權杖，該權杖的有效期間為24小時。

可使用為此目的而設計的程式碼範例來交換AEM CS服務認證以換取存取權杖。 範常式式碼可從[Adobe的公用GitHub存放庫](https://github.com/adobe/aemcs-api-client-lib)取得，其中包含您可複製並調整自己專案的程式碼範例。 請注意，此存放庫包含參考的範常式式碼，不會維護為生產就緒的程式庫相依性。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
// Sample code adapted from Adobe's GitHub repository
const exchange = require("./your-local-aemcs-client"); // Copy and adapt the code from the GitHub repository

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

相同交換可以用任何能夠產生具有正確格式的已簽署JWT權杖並呼叫IMS權杖交換API的語言執行。

存取權杖會定義其到期時間，通常為24小時。 Git存放庫中有範常式式碼，可用來管理存取權杖並在其過期前重新整理。

### 呼叫AEM API {#calling-the-aem-api}

對AEM as a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「授權」標頭，請使用值`"Bearer <access_token>"`。 例如，使用`curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的許可權 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在AEM中建立技術帳戶使用者之後（在第一次具有對應存取權杖的請求之後發生），技術帳戶使用者必須在&#x200B;**AEM中獲得**&#x200B;的適當許可權。

依預設，在AEM Author服務中，技術帳戶使用者會新增至提供讀取許可權AEM的貢獻者使用者群組。

可使用一般方法，進一步布建此AEM技術帳戶使用者的許可權。

## 開發人員流程 {#developer-flow}

開發人員應使用其非AEM應用程式的開發執行個體進行測試（在他們的筆記型電腦上執行或託管），該應用程式會向開發AEM as a Cloud Service開發環境發出請求。 不過，由於開發人員不一定具備IMS管理員角色許可權，Adobe無法假設他們可以產生一般伺服器對伺服器流程中說明的JWT持有者。 因此，Adobe為開發人員提供了一種直接產生存取權杖的機制，可用於對其有權存取的AEM as a Cloud Service環境的請求。

如需使用AEM as a Cloud Service開發人員主控台所需許可權的資訊，請參閱[開發人員指引檔案](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

>[!NOTE]
>
>本機開發存取權杖的有效期最長為24小時，之後必須使用相同方法重新產生。

開發人員可使用此代號，從非AEM測試應用程式呼叫AEM as a Cloud Service環境。 開發人員通常會在自己的筆記型電腦上，將此代號與非AEM應用程式搭配使用。 此外，AEM as a Cloud通常是非生產環境。

開發人員流程涉及以下步驟：

* 從Developer Console產生存取權杖
* 使用存取權杖呼叫AEM應用程式。

開發人員也可以對其本機電腦上執行的AEM專案進行API呼叫，如此便不需要存取權杖。

### 產生存取權杖 {#generating-the-access-token}

若要產生存取權杖，請在Developer Console中按一下[取得本機開發權杖] **。**

### 使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEM as a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「授權」標頭，請使用值`"Bearer <access_token>"`。

## 重新整理認證 {#refresh-credentials}

根據預設，AEM as a Cloud Service上的認證一年後過期。 為確保服務的連續性，開發人員可以選擇重新整理憑證，將其可用性延長一年。 從Developer Console的&#x200B;**整合**&#x200B;索引標籤使用&#x200B;**重新整理服務認證**，如下所示。

![認證重新整理](assets/credential-refresh.png)

按下按鈕後，會產生一組新的認證。 您可以使用新的認證更新您的秘密儲存空間，並驗證它們是否如預期般運作。

>[!NOTE]
>
> 按一下&#x200B;**重新整理服務認證**&#x200B;按鈕後，舊認證會保持註冊狀態，直到過期為止，但任何時候都只能從Developer Console看到最新的認證組。

## 服務認證撤銷 {#service-credentials-revocation}

如果認證必須撤銷，您必須使用下列步驟向客戶支援提交請求：

1. 在使用者介面中停用Adobe Admin Console的技術帳戶使用者：
   * 在Cloud Manager中，按一下環境旁的&#x200B;**...**&#x200B;按鈕。 此動作會開啟產品設定檔頁面
   * 現在，按一下&#x200B;**AEM使用者**&#x200B;設定檔，以顯示使用者清單
   * 按一下&#x200B;**API認證**&#x200B;標籤，然後尋找適當的技術帳戶使用者並將其刪除
2. 請聯絡客戶支援，並要求刪除該特定環境的服務認證
3. 最後，您可以再次產生認證，如本檔案所述。 同時也請確定建立的新技術帳戶使用者擁有適當的許可權。
