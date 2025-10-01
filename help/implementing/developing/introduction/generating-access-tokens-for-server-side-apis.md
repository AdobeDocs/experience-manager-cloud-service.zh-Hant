---
title: 為伺服器端API產生存取權杖
description: 瞭解如何產生安全JWT權杖，以促進第三方伺服器與AEM as a Cloud Service之間的通訊
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# 為伺服器端API產生存取權杖 {#generating-access-tokens-for-server-side-apis}

有些架構需仰賴從託管於AEM as a Cloud Service基礎架構以外之伺服器上的應用程式呼叫AEM。 例如，行動應用程式，它會呼叫伺服器，然後向AEM as a Cloud Service發出API請求。

伺服器對伺服器的流程如下所述，以及簡化的開發流程。 AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console)是用來產生驗證程式所需的權杖。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=zh-Hant#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器對伺服器流量 {#the-server-to-server-flow}

具有IMS組織管理員角色以及AEM Author上AEM使用者或AEM管理員產品設定檔成員的使用者，可以從AEM as a Cloud Service產生一組認證。 每個認證都是JSON裝載，其中包含憑證（公開金鑰）、私密金鑰以及包含`clientId`和`clientSecret`的技術帳戶。 這些認證稍後可由具有AEM as a Cloud Service環境管理員角色的使用者擷取，並應安裝在非AEM伺服器上，且仔細視為機密金鑰。 此JSON格式檔案包含與AEM as a Cloud Service API整合所需的所有資料。 資料可用來建立已簽署的JWT權杖，該權杖會與Adobe Identity Management Services (IMS)交換，以取得IMS存取權杖。 然後，可將此存取權杖用作持有者驗證權杖，以向AEM as a Cloud Service提出請求。 認證中的憑證預設在一年後到期，但可在需要時重新整理，請參閱[重新整理認證](#refresh-credentials)。

伺服器對伺服器流程涉及以下步驟：

* 從Developer Console在AEM as a Cloud Service上擷取認證
* 在呼叫AEM as a Cloud Service的非AEM伺服器上安裝AEM的認證
* 產生JWT權杖並使用Adobe的IMS API將該權杖交換為存取權杖
* 使用存取權杖作為持有者驗證權杖呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的許可權

### 擷取AEM as a Cloud Service認證 {#fetch-the-aem-as-a-cloud-service-credentials}

有權存取AEM as a Cloud Service開發人員控制檯的使用者可檢視Developer Console中特定環境的整合索引標籤。 具有AEM as a Cloud Service環境管理員角色的使用者可以建立、檢視或管理認證。

按一下&#x200B;**建立新的技術帳戶**，即會建立一組認證，其中包含使用者端識別碼、使用者端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論Pod選取範圍為何。

![建立新的技術帳戶](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

隨即開啟新的瀏覽器標籤，顯示認證。 您可以按狀態標題旁的下載圖示，使用此檢視來下載認證：

![下載認證](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

建立認證後，它們會出現在&#x200B;**整合**&#x200B;區段的&#x200B;**技術帳戶**&#x200B;標籤下：

![檢視認證](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

使用者稍後可以使用「檢視」動作來檢視認證。 此外，如文章稍後所述，使用者可以編輯相同技術帳戶的認證。 他們透過建立私密金鑰或憑證來完成此編輯，適用於必須更新或撤銷憑證的情況。

具有AEM as a Cloud Service環境管理員角色的使用者稍後可以為其他技術帳戶建立認證。 當不同的API有不同的存取要求時，這項功能會很有用。 例如，讀取與讀寫。

>[!NOTE]
>
>客戶最多可建立10個技術帳戶，包括已刪除的帳戶。

>[!IMPORTANT]
>
>IMS組織管理員(通常是透過Cloud Manager布建環境的相同使用者)也是AEM Author上的AEM使用者或AEM管理員產品設定檔的成員，必須首先存取Developer Console。 接著，按一下&#x200B;**建立新的技術帳戶**，即可產生認證，並由具有AEM as a Cloud Service環境管理員許可權的使用者於稍後擷取。 如果IMS組織管理員尚未建立技術帳戶，則會出現一則訊息，通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務認證 {#install-the-aem-service-credentials-on-a-non-aem-server}

呼叫AEM的應用程式應能存取AEM as a Cloud Service的認證，將其視為秘密。

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

>[!NOTE]
>如果有多個認證，請務必針對稍後叫用的AEM API呼叫，參考適當的json檔案。

### 呼叫AEM API {#calling-the-aem-api}

對AEM as a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「授權」標頭，請使用值`"Bearer <access_token>"`。 例如，使用`curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的許可權 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，必須在Adobe Admin Console中建立新的產品設定檔。

1. 前往[https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)的Adobe Admin Console。
1. 按左側&#x200B;**產品和服務**&#x200B;欄下的&#x200B;**管理**&#x200B;連結。
1. 選取&#x200B;**AEM as a Cloud Service**。
1. 按&#x200B;**新設定檔**&#x200B;按鈕。

   ![新設定檔](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 為設定檔命名，然後按&#x200B;**儲存**。

   ![儲存設定檔](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 從設定檔清單中選取您建立的設定檔。
1. 選取&#x200B;**新增使用者**。

   ![新增使用者](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 新增您建立的技術帳戶（在此案例中為`84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`），然後按一下[儲存]。**&#x200B;**

   ![新增技術帳戶](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 請等待10分鐘，讓變更生效，並使用新認證產生的存取權杖向AEM發出API呼叫。 cURL指令的顯示方式與以下範例類似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


進行API呼叫後，產品設定檔會在AEM as a Cloud Service作者例項中顯示為使用者群組，而適當的技術帳戶會顯示為該群組的成員。

若要檢查此資訊，請執行下列動作：

1. 登入製作執行個體。
1. 移至&#x200B;**工具** > **安全性**，然後按一下&#x200B;**群組**&#x200B;卡片。
1. 在群組清單中找出您建立的設定檔名稱，然後按一下該設定檔：

   ![群組設定檔](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在下列視窗中，切換至&#x200B;**成員**&#x200B;標籤，並檢查技術帳戶是否正確列於此處：

   ![成員標籤](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以透過在作者執行個體上執行以下步驟來驗證技術帳戶是否出現在使用者清單中：

1. 移至&#x200B;**工具** > **安全性** > **使用者**。
1. 檢查您的技術帳戶是否為使用者清單，然後選取它。
1. 按一下「**群組**」標籤，以確認使用者屬於與您的產品設定檔相對應的群組。 此使用者也是少數其他群組的成員，包括「貢獻者」：

   ![群組成員資格](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年中之前，在可以建立多個憑證之前，沒有引導客戶在Adobe Admin Console中建立產品設定檔。 因此，技術帳戶並未與AEM as a Cloud Service例項中「貢獻者」以外的群組建立關聯。 為了保持一致性，建議您針對此技術帳戶，在Adobe Admin Console中建立上述的產品設定檔，並將現有技術帳戶新增至該群組。

<u>**設定適當的群組許可權**</u>

最後，以必要的適當許可權設定群組，讓您可以適當叫用或鎖定API。

1. 登入適當的作者執行個體，並瀏覽至&#x200B;**設定** > **安全性** > **許可權**
1. 在左側窗格中，搜尋與產品設定檔相對應的群組名稱（在此案例中為「唯讀API」），然後選取它：

   ![搜尋群組](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 在下列視窗中按一下「編輯」按鈕：

   ![編輯許可權](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 適當地修改許可權，然後按一下&#x200B;**儲存**

   ![確認編輯許可權](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>進一步瞭解Adobe Identity Management System (IMS)和AEM使用者和群組。 請參閱[檔案](/help/security/ims-support.md)。

## 開發人員流程 {#developer-flow}

開發人員可能想要使用非AEM應用程式的開發執行個體進行測試（在他們的筆記型電腦上執行或託管），該應用程式會向開發AEM as a Cloud Service開發環境發出請求。 不過，由於開發人員不一定具備IMS管理員角色許可權，Adobe無法假設他們可以產生一般伺服器對伺服器流程中說明的JWT持有者。 因此，Adobe為開發人員提供了一種直接產生存取權杖的機制，可用於對AEM as a Cloud Service上他們有權存取的環境的請求。

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

1. 移至&#x200B;**整合**&#x200B;下的&#x200B;**本機權杖**
1. 按一下Developer Console中的「取得本機開發權杖&#x200B;**」，以產生存取權杖。**

### 使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEM as a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「授權」標頭，請使用值`"Bearer <access_token>"`。

## 重新整理認證 {#refresh-credentials}

根據預設，AEM as a Cloud Service上的憑證會在一年後過期。 為確保服務的連續性，開發人員可以選擇重新整理憑證，將其可用性延長一年。

若要達到此重新整理擴充功能，請執行下列動作：

* 使用Developer Console中&#x200B;**整合** - **技術帳戶**&#x200B;下的&#x200B;**新增憑證**&#x200B;按鈕，如下所示

  ![認證重新整理](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按鈕後，會產生一組包含新憑證的認證。 在AEM以外的伺服器上安裝新憑證，並確保如預期般連線，不會移除舊憑證。
* 產生存取權杖時，請務必使用新憑證，而非舊憑證。
* 選擇性地撤銷（然後刪除）先前的憑證，使其無法再用來向AEM as a Cloud Service進行驗證。

## 認證撤銷 {#credentials-revocation}

如果私密金鑰遭到破壞，您必須使用新的憑證和新的私密金鑰來建立認證。 應用程式使用新認證來產生存取權杖後，您可以執行下列動作來撤銷和刪除舊憑證：

1. 首先，新增金鑰。 此金鑰會產生具有新私密金鑰和新憑證的認證。 新的私密金鑰在使用者介面中標示為&#x200B;**目前**，因此會用於此技術帳戶日後的所有新認證。 與舊版私密金鑰關聯的認證在撤銷前仍然有效。 若要完成此撤銷，請在您目前的技術帳戶下選取三個點(**...**)，然後選取&#x200B;**新增私密金鑰**：

   ![新增私密金鑰](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 在下列提示處選取&#x200B;**新增**：

   ![確認新增新的私密金鑰](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   具有新認證的新瀏覽標籤會開啟，且使用者介面會更新，以顯示具有標籤為&#x200B;**目前**&#x200B;之新私密金鑰的兩個私密金鑰：

   UI中的![私密金鑰](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM伺服器上安裝新憑證，並確保連線能力如預期般運作。 如需詳細資訊，請參閱[伺服器對伺服器流量區段](#the-server-to-server-flow)。
1. 選取憑證右側的三個點(**...**)，並選取&#x200B;**撤銷**，以撤銷舊憑證：

   ![撤銷憑證](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然後，按下&#x200B;**撤銷**&#x200B;按鈕，在下列提示中確認撤銷：

   ![撤銷憑證確認](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後，刪除已洩漏的憑證。
