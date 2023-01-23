---
title: 為伺服器端 API 產生存取權杖
description: 了解如何產生安全的JWT代號，以便利第三方伺服器與AEMas a Cloud Service之間的通訊
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 41458eb1fba12e8ef45a32d3bb6fc5dd732f78ec
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 1%

---

# 為伺服器端 API 產生存取權杖 {#generating-access-tokens-for-server-side-apis}

>[!AVAILABILITY]
>
>Adobe正在逐步推出本文所述的新的多證書和憑據撤銷功能。 如果您在組織的AEM開發人員控制台中勾選整合標籤時，發現畫面外觀與下方的螢幕擷取畫面不同，這表示新變更尚未推出給您的組織。 在此情況下，請參閱 [舊版檔案](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis-legacy.md).

有些架構依賴從AEM基礎架構外的伺服器上托管的應用程式對AEM進行as a Cloud Service的呼叫。 例如，呼叫伺服器的行動應用程式，接著會向AEMas a Cloud Service提出API請求。

伺服器對伺服器的流程及簡化的開發流程如下所述。 AEMas a Cloud Service [開發人員控制台](development-guidelines.md#crxde-lite-and-developer-console) 用來產生驗證程式所需的權杖。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器對伺服器流量 {#the-server-to-server-flow}

擁有IMS組織管理員角色的使用者，以及AEM作者上AEM使用者或AEM管理員產品設定檔的成員，可以產生一組AEMas a Cloud Service憑證，每個憑證都是JSON裝載，其中包含憑證（公開金鑰）、私密金鑰，以及由 `clientId` 和 `clientSecret`. 具有AEMas a Cloud Service環境管理員角色的使用者隨後可擷取這些憑證，且應安裝在非AEM伺服器上，並謹慎視為機密金鑰。 此JSON格式檔案包含與AEMas a Cloud Service API整合所需的所有資料。 資料可用來建立已簽署的JWT代號，此代號會與AdobeIdentity Management服務(IMS)交換以取得IMS存取代號。 然後，此存取權杖可作為承載驗證權杖，以向AEMas a Cloud Service提出請求。 憑證中的憑證預設會在一年後到期，但如有需要，可依說明重新整理 [此處](#refresh-credentials).

伺服器對伺服器流程涉及下列步驟：

* 從開發人員控制台擷取AEMas a Cloud Service憑證
* 在對AEM進行呼叫的非AEM伺服器上安裝AEMas a Cloud Service憑證
* 使用Adobe的IMS API產生JWT代號，並交換存取代號的代號
* 使用存取權杖作為承載驗證權杖來呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的權限

### 擷取AEMas a Cloud Service憑證 {#fetch-the-aem-as-a-cloud-service-credentials}

擁有AEMas a Cloud Service開發人員控制台存取權的使用者，會在指定環境的開發人員控制台中看到整合索引標籤。 具有AEMas a Cloud Service環境管理員角色的使用者可以建立、檢視或管理憑證。

按一下 **建立新技術帳戶** 按鈕時，將建立一組新憑證，其中包含用戶端id、用戶端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論選擇何種pod。

![建立新技術帳戶](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

將開啟顯示憑證的新瀏覽器標籤。 您可以按狀態標題旁的下載圖示，使用此檢視來下載憑證：

![下載憑證](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

建立憑證後，這些憑證會顯示在 **技術帳戶** 標籤 **整合** 小節：

![查看憑據](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

用戶以後可以使用「查看」操作查看憑據。 此外，如文章後面所述，對於需要續訂或撤銷證書的情況，用戶可以通過建立新的私鑰或證書來修改同一技術帳戶的證書。

具有AEMas a Cloud Service環境管理員角色的使用者稍後可以建立其他技術帳戶的新憑證。 當不同API的存取需求不同時，這個用法就很實用。 例如，讀取與讀取。

>[!NOTE]
>
>客戶最多可建立10個技術帳戶，包括已刪除的帳戶。

>[!IMPORTANT]
>
>IMS組織管理員（通常是透過Cloud Manager布建環境的相同使用者）也應是AEM作者上AEM使用者或AEM管理員產品設定檔的成員，必須先存取開發人員主控台，然後按一下 **建立新技術帳戶** 按鈕，以便具有AEMas a Cloud Service環境管理權限的使用者產生並稍後擷取憑證。 如果IMS組織管理員尚未執行此動作，系統會傳送訊息通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務憑證 {#install-the-aem-service-credentials-on-a-non-aem-server}

向AEM發出呼叫的應用程式應能存取AEMas a Cloud Service憑證，並將其視為機密。

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

>[!NOTE]
>如果有多個憑證，請務必參考適當的json檔案，以供稍後將叫用的AEM API呼叫。

### 呼叫AEM API {#calling-the-aem-api}

對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標題中的存取權杖。 因此，對於「授權」標題，請使用值 `"Bearer <access_token>"`. 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的權限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，需要在Adobe Admin Console中建立新的產品設定檔。 您可以依照下列步驟來達成此目標：

1. 前往Adobe Admin Console，網址為 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. 按下 **管理** 連結 **產品和服務** 欄。
1. 選擇 **AEMas a Cloud Service**
1. 按下 **新設定檔** 按鈕

   ![新建設定檔](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 為設定檔命名，然後按 **儲存**

   ![儲存設定檔](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 從設定檔清單中選取您剛建立的設定檔
1. 按下 **添加用戶** 按鈕

   ![新增使用者](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 新增您剛建立的技術帳戶(在此例中為 `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`)和按 **儲存**

   ![新增技術帳戶](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 等待10分鐘，讓變更生效，並使用新憑證產生的存取權杖，對AEM進行API呼叫。 以cURL命令的形式表示，會類似於以下範例：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


發出API呼叫後，產品設定檔會在AEMas a Cloud Service製作例項中顯示為使用者群組，且會有適當的技術帳戶作為該群組的成員。

若要檢查此項，您必須：

1. 登入製作例項
1. 前往 **工具** - **安全性** 並按一下 **群組** 卡片
1. 在群組清單中找出您建立之設定檔的名稱，然後按一下：

   ![群組設定檔](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在以下視窗中，切換至 **成員** 標籤，並檢查技術帳戶是否已正確列出：

   ![成員頁簽](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以在製作執行個體上執行下列步驟，以確認技術帳戶出現在使用者清單中：

1. 前往 **工具** - **安全性** - **使用者**
1. 檢查您的技術帳戶是否為使用者清單，然後按一下
1. 按一下 **群組** 標籤，確認使用者是與您的產品設定檔對應的群組的一部分。 此使用者也是其他少數群組的成員，包括貢獻者：

   ![群組成員資格](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年年中之前，在可以建立多個憑證之前，並未引導客戶在「Adobe管理控制台」中建立產品設定檔，因此技術帳戶沒有與AEMas a Cloud Service例項中的「貢獻者」以外的群組建立關聯。 為了一致性，建議您針對此技術帳戶，如上所述，在Adobe Admin Console中建立新的產品設定檔，並將現有技術帳戶新增至該群組。

<u>**設定適當的群組權限**</u>

最後，以適當的權限設定群組，以適當叫用或鎖定API。 您可以透過下列方式執行此作業：

1. 登入適當的製作例項，然後前往 **設定** - **安全性** - **權限**
1. 在左側窗格中搜尋與產品設定檔對應的群組名稱（在此例中為唯讀API），然後按一下：

   ![搜尋群組](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 按一下以下視窗中的「編輯」按鈕：

   ![編輯權限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 適當修改權限，然後按一下 **儲存**

   ![確認編輯權限](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>請諮詢以下Adobe，進一步了解Identity Management系統(IMS)和AEM使用者和群組 [檔案](/help/security/ims-support.md).

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

1. 前往 **本機代號** 在 **整合**
1. 按一下 **取得本機開發代號** 按鈕，產生存取權杖。

### 使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEMas a Cloud Service環境進行適當的伺服器對伺服器API呼叫，包括標題中的存取權杖。 因此，對於「授權」標題，請使用值 `"Bearer <access_token>"`.

## 刷新憑據 {#refresh-credentials}

依預設，AEMas a Cloud Service憑證會在一年後到期。 為確保服務連續性，開發人員可以選擇刷新憑據，將其可用性延長一年。

若要達成此目標，您可以：

* 使用 **新增憑證** 按鈕 **整合** - **技術帳戶** ，如下所示

   ![憑據刷新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按鈕後，會產生一組包含新憑證的憑證。 在離AEM伺服器上安裝新憑證，並確保連線如預期，而不需移除舊憑證 
* 產生存取權杖時，請確定已使用新憑證，而非舊憑證
* 可選擇撤銷（然後刪除）先前的憑證，以便不再能用於透過AEM as a Cloud Service驗證。

## 憑據吊銷 {#credentials-revocation}

如果私密金鑰被洩露，您需要使用新證書和新私鑰建立憑據。 在您的應用程式使用新憑證來產生存取權杖後，您可以撤銷和刪除舊憑證。

您可以按照以下步驟執行此操作：

1. 首先，新增金鑰。 這會產生具有新私密金鑰和新憑證的憑證。 新的私密金鑰在UI中會標示為 **電流** 因此，此技術帳戶的所有新憑證將會使用和。 請注意，在撤銷之前，與舊私鑰關聯的憑據仍有效。 若要完成此操作，請按三個點(**...**)，按 **新增私密金鑰**:

   ![新增私密金鑰](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Press **新增** 提示如下：

   ![確認新私鑰的添加](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   將開啟包含新目錄的新瀏覽標籤，並更新UI以顯示兩個私密金鑰，新索引標籤標示為 **電流**:

   ![UI中的私密金鑰](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM伺服器上安裝新憑證，並確保連線正常運作。 請參閱 [「伺服器到伺服器流」部分](#the-server-to-server-flow) 以取得如何執行此動作的詳細資訊
1. 撤銷舊證書。 您可以選取三個點(**...**)，然後按 **撤銷**:

   ![撤銷證書](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然後，按下 **撤銷** 按鈕：

   ![撤消證書確認](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後，刪除妥善的憑證。
