---
title: 為伺服器端API生成訪問令牌
description: 瞭解如何通過生成安全的JWT令牌AEM來促進第三方伺服器與as a Cloud Service之間的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: fc49b004a61d5f981ac61cca684dc0bacf843443
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# 簡介 {#introduction}

某些體系結構依賴呼叫AEMas a Cloud Service於在基礎架構之外的伺服器上承載的AEM應用程式。 例如，調用伺服器的移動應用程式，然後向AEMas a Cloud Service請求API。

下面介紹了伺服器到伺服器的流程，以及簡化的開發流程。 AEMas a Cloud Service [開發人員控制台](development-guidelines.md#crxde-lite-and-developer-console) 用於生成驗證過程所需的令牌。

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html).

## 伺服器到伺服器流 {#the-server-to-server-flow}

具有IMS組織管理員角色，並且還是AEM作者上的「用戶」或「管理員AEM產品配置文AEM件」的成員的用戶可以生成AEMas a Cloud Service憑據。 隨後，具有AEMas a Cloud Service環境管理員角色的用戶可以檢索該憑據，並應安裝在伺服器上，需要將其作為密鑰加以仔細處理。 此JSON格式檔案包含與as a Cloud ServiceAPI整合所需的所AEM有資料。 該資料用於建立與IMS交換的簽名JWT令牌，以用於IMS訪問令牌。 然後，此訪問令牌可用作承載驗證令牌，以向AEMas a Cloud Service請求。 預設情況下，憑據將在一年後過期，但在需要時可以刷新，如所述 [這裡](#refresh-credentials)。

伺服器到伺服器流包括以下步驟：

* 從開發AEM人員控制台獲取as a Cloud Service憑據
* 在非AEM伺服器上安AEM裝as a Cloud Service憑據AEM
* 生成JWT令牌，並使用Adobe的IMS API交換該令牌作為訪問令牌
* 使用訪問AEM令牌作為承載驗證令牌調用API
* 為環境中的技術帳戶用戶設定適當的權AEM限

### 獲取AEMas a Cloud Service憑據 {#fetch-the-aem-as-a-cloud-service-credentials}

對as a Cloud Service開發人員控AEM制台具有訪問權限的用戶將看到給定環境的開發人員控制台中的整合頁籤以及兩個按鈕。 A user with the AEM as a Cloud Service Environment administrator role can click the **Generate Service Credentials** button to generate and display the service credentials json, which will contain all the information required for the non AEM server, including client id, client secret, private key, certificate, and configuration for author and publish tiers of the environment, regardless of the pod selection.

![JWT Generation](assets/JWTtoken3.png)

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

在生成後，可以通過按 **獲取服務憑據** 按鈕。

>[!IMPORTANT]
>
>IMS組織管理員（通常是通過雲管理器設定環境的同一用戶），也應是AEM作者上的「用戶AEM」或AEM「管理員產品配置檔案」的成員，必須首先訪問開發人員控制台並按一下 **生成服務憑據** 的子菜單。 If the IMS org administrator has not done this, a message will inform them that they need the IMS org Administrator role.

### 在非服AEM務器上安裝服務憑AEM據 {#install-the-aem-service-credentials-on-a-non-aem-server}

The non-AEM application making calls to AEM should be able to access the AEM as a Cloud Service credentials, treating it as a secret.

### 生成JWT令牌，並將其交換為訪問令牌 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

使用憑據在呼叫Adobe的IMS服務時建立JWT令牌，以檢索有效期為24小時的訪問令牌。

CS服AEM務憑據可以使用為此目的設計的客戶端庫交換為訪問令牌。 客戶端庫可從 [Adobe的公共GitHub儲存庫](https://github.com/adobe/aemcs-api-client-lib)，其中包含更詳細的指導和最新資訊。

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

可以用能夠生成具有正確格式的簽名JWT令牌並調用IMS令牌交換API的任何語言執行相同的交換。

訪問令牌將定義何時過期，通常為24小時。 Git儲存庫中有示例代碼，用於管理訪問令牌並在其過期之前刷新它。

### 調用AEMAPI {#calling-the-aem-api}

對as a Cloud Service環境（包括頭中的訪問令牌）AEM進行適當的伺服器到伺服器API調用。 因此，對於「授權」標頭，使用 `"Bearer <access_token>"`。 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在中為技術帳戶用戶設定適當的權AEM限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

在中建立技術帳戶用戶(AEM這發生在具有相應訪問令牌的第一個請求之後)後，必須正確地對技術帳戶用戶進行許可 **在** AEM。

請注意，預設情況下，在AEM Author服務上，技術帳戶用戶將添加到提供讀取訪問權限的「參與者」用戶AEM組。

中的此技術帳戶用AEM戶可以使用通常的方法進一步設定權限。

## 顯影劑流 {#developer-flow}

Developers will likely want to test using a development instance of their non-AEM application (either running on their laptop or hosted) that makes requests to a development AEM as a Cloud Service dev environment. 但是，由於開發人員不一定具有IMS管理員角色權限，因此我們不能假設他們能夠生成常規伺服器到伺服器流中描述的JWT承載。 因此，我們為開發者直接生成訪問令牌的機制，該訪問令牌可以用於他AEM們有權訪問的as a Cloud Service環境的請求。

查看 [開發人員指南文檔](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 有關使用as a Cloud Service開發者控制台所需AEM權限的資訊。

>[!NOTE]
>
>本地開發訪問令牌的有效期最長為24小時，此後必須使用相同方法重新生成該令牌。

開發人員可以使用此令牌從其非test應AEM用程式向AEMas a Cloud Service環境進行呼叫。 通常，開發人員會將此令牌與非應用程式一起AEM使用在自己的筆記型電腦上。 Also, the AEM as a Cloud is typically a non-production environment.

開發人員流包括以下步驟：

* 從開發人員控制台生成訪問令牌
* 使用訪AEM問令牌調用應用程式。

開發人員還可以對在其本AEM地電腦上運行的項目進行API調用，在這種情況下，不需要訪問令牌。

### 生成訪問令牌 {#generating-the-access-token}

按一下 **獲取本地開發令牌** 按鈕以生成訪問令牌。

### 然後使用訪AEM問令牌調用應用程式 {#call-the-aem-application-with-an-access-token}

將相應的伺服器到伺服器API調用從非應用程AEM序到as a Cloud ServiceAEM環境，包括頭中的訪問令牌。 因此，對於「授權」標頭，使用 `"Bearer <access_token>"`。

## 刷新憑據 {#refresh-credentials}

預設情況下，AEMas a Cloud Service憑據將在一年後過期。 為確保服務連續性，開發人員可以選擇刷新憑據，將其可用性延長一年。

要達到此目的，可使用 **刷新服務憑據** 按鈕 **整合** 頁籤，如下所示。

![憑據刷新](assets/credential-refresh.png)

按下按鈕後，將生成一組新的憑據。 您可以使用新憑據更新機密儲存，並驗證它們是否按應用方式工作。

>[!NOTE]
>
> 按一下 **刷新服務憑據** 按鈕，舊憑據將一直註冊到過期，但只有最近的憑據集可以在任何時候從開發人員控制台查看。

## Service Credentials Revocation {#service-credentials-revocation}

如果需要撤銷憑據，您需要使用以下步驟向客戶支援提交請求：

1. 在用戶介面中禁用Adobe Admin Console的技術帳戶用戶：
   * 在雲管理器中，按 **...** 按鈕。 這將開啟產品配置檔案頁
   * 現在，按一下 **用AEM戶** 配置檔案，顯示用戶清單
   * 按一下 **API憑據** 頁籤，然後查找相應的技術帳戶用戶並將其刪除
2. 聯繫客戶支援，並請求刪除該特定環境的服務憑據
3. 最後，您可以再次生成憑據，如本文檔中所述。 另請確保建立的新技術帳戶用戶具有相應的權限。
