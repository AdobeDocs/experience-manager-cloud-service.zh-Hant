---
title: 為伺服器端API產生存取權杖
description: 瞭解如何產生安全JWT權杖，以促進協力廠商伺服器與AEMas a Cloud Service之間的通訊
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 0%

---

# 為伺服器端API產生存取權杖 {#generating-access-tokens-for-server-side-apis}

有些架構依賴對AEM的呼叫與AEM基礎架構以外伺服器上託管的應用程式as a Cloud Service。 例如，呼叫伺服器的行動應用程式，接著會向AEM發出as a Cloud Service的API請求。

伺服器對伺服器的流程如下所述，以及簡化的開發流程。 AEMas a Cloud Service [開發人員主控台](development-guidelines.md#crxde-lite-and-developer-console) 用於產生驗證程式所需的權杖。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器對伺服器流量 {#the-server-to-server-flow}

具有IMS組織管理員角色以及AEM Author上的AEM使用者或AEM管理員產品設定檔成員的使用者，可以從AEMas a Cloud Service產生一組認證。 每個認證都是JSON裝載，其中包含憑證（公開金鑰）、私密金鑰和由以下憑證組成的技術帳戶： `clientId` 和 `clientSecret`. 這些認證稍後可由具有AEMas a Cloud Service環境管理員角色的使用者擷取，並應安裝在非AEM伺服器上，且謹慎視為機密金鑰。 此JSON格式檔案包含與AEMas a Cloud ServiceAPI整合所需的所有資料。 資料可用來建立已簽署的JWT權杖，該權杖會與AdobeIdentity Management服務(IMS)交換以取得IMS存取權杖。 然後，可將此存取權杖用作持有者驗證權杖，以向AEM發出as a Cloud Service請求。 憑證中的憑證預設在一年後到期，但可在需要時重新整理，如上所述 [此處](#refresh-credentials).

伺服器對伺服器流程涉及以下步驟：

* 從開發人員主控台as a Cloud Service擷取AEM上的認證
* 在呼叫AEM的非AEM伺服器上安裝AEMas a Cloud Service的認證
* 產生JWT權杖並使用Adobe的IMS API將該權杖交換為存取權杖
* 使用存取權杖作為持有者驗證權杖呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的許可權

### 擷取AEMas a Cloud Service認證 {#fetch-the-aem-as-a-cloud-service-credentials}

有權存取AEMas a Cloud Service開發人員控制檯的使用者，請參閱特定環境的開發人員控制檯中的整合索引標籤。 具有AEMas a Cloud Service環境管理員角色的使用者可以建立、檢視或管理認證。

按一下 **建立新的技術帳戶**，會建立一組憑證，其中包含使用者端id、使用者端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論pod選取範圍為何。

![建立新的技術帳戶](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

隨即開啟新的瀏覽器標籤，顯示認證。 您可以按狀態標題旁的下載圖示，使用此檢視來下載認證：

![下載認證](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

建立認證後，它們會出現在 **技術帳戶** 索引標籤中的 **整合** 區段：

![檢視認證](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

使用者稍後可以使用「檢視」動作來檢視認證。 此外，如文章稍後所述，使用者可以編輯相同技術帳戶的認證。 他們透過建立私密金鑰或憑證來完成此編輯，適用於必須更新或撤銷憑證的情況。

具有AEMas a Cloud Service環境管理員角色的使用者稍後可以為其他技術帳戶建立認證。 當不同的API有不同的存取要求時，這項功能會很有用。 例如，讀取與讀寫。

>[!NOTE]
>
>客戶最多可建立10個技術帳戶，包括已刪除的帳戶。

>[!IMPORTANT]
>
>IMS組織管理員（通常是透過Cloud Manager布建環境的相同使用者）也是AEM Author上的AEM使用者或AEM管理員產品設定檔的成員，必須首先存取開發人員主控台。 然後，按一下 **建立新的技術帳戶** 供具有AEMas a Cloud Service環境管理員許可權的使用者產生及稍後擷取的認證。 如果IMS組織管理員尚未建立技術帳戶，則會出現一則訊息，通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務認證 {#install-the-aem-service-credentials-on-a-non-aem-server}

呼叫AEM的應用程式應能存取AEMas a Cloud Service的認證，將其視為機密。

### 產生JWT權杖並將其交換為存取權杖 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

使用認證在呼叫Adobe的IMS服務中建立JWT權杖以擷取存取權杖，該權杖的有效期限為24小時。

可以使用為此目的而設計的使用者端程式庫來交換AEM CS服務認證以取得存取權杖。 使用者端程式庫可從以下位置取得： [Adobe的公開GitHub存放庫](https://github.com/adobe/aemcs-api-client-lib)，其中包含更詳細的指引和最新資訊。

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

相同交換可以用任何能夠產生具有正確格式的已簽署JWT權杖並呼叫IMS權杖交換API的語言執行。

存取權杖會定義其到期時間，通常為24小時。 Git存放庫中有範常式式碼，可用來管理存取權杖並在其過期前重新整理。

>[!NOTE]
>如果有多個認證，請務必針對稍後叫用的AEM API呼叫，參考適當的json檔案。

### 呼叫AEM API {#calling-the-aem-api}

對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「Authorization」標頭，請使用值 `"Bearer <access_token>"`. 例如，使用 `curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的許可權 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，必須在Adobe Admin Console中建立新的產品設定檔。

1. 前往Adobe Admin Console，網址為 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. 按下 **管理** 連結至 **產品和服務** 欄中。
1. 選取 **AEMas a Cloud Service**.
1. 按下 **新設定檔** 按鈕。

   ![新建設定檔](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 為設定檔命名，然後按 **儲存**.

   ![儲存設定檔](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 從設定檔清單中選取您建立的設定檔。
1. 選取 **新增使用者**.

   ![新增使用者](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 新增您建立的技術帳戶（在此案例中） `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`)，然後按一下 **儲存**.

   ![新增技術帳戶](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 請等待10分鐘，讓變更生效，並使用新認證產生的存取權杖向AEM發出API呼叫。 cURL指令的顯示方式與以下範例類似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


進行API呼叫後，產品設定檔會在AEMas a Cloud Service製作例項中顯示為使用者群組，而適當的技術帳戶會顯示為該群組的成員。

若要檢查此資訊，請執行下列動作：

1. 登入編寫執行個體。
1. 前往 **工具** > **安全性**，然後按一下 **群組** 卡片。
1. 在群組清單中找出您建立的設定檔名稱，然後按一下該設定檔：

   ![群組設定檔](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在下列視窗中，切換至 **成員** 索引標籤並檢查此處是否正確列出技術帳戶：

   ![「成員」標籤](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以透過在作者執行個體上執行以下步驟來驗證技術帳戶是否出現在使用者清單中：

1. 前往 **工具** > **安全性** > **使用者**.
1. 檢查您的技術帳戶是否為使用者清單，然後選取它。
1. 按一下 **群組** 標籤，以便您確認使用者屬於與產品設定檔相對應的群組。 此使用者也是少數其他群組的成員，包括「貢獻者」：

   ![群組會籍](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年中之前，在可以建立多個憑證之前，沒有引導客戶在Adobe Admin Console中建立產品設定檔。 因此，技術帳戶並未與AEMas a Cloud Service執行個體中「貢獻者」以外的群組建立關聯。 為了保持一致性，建議您針對此技術帳戶，在Adobe Admin Console中建立上述的產品設定檔，並將現有技術帳戶新增至該群組。

<u>**設定適當的群組許可權**</u>

最後，以必要的適當許可權設定群組，讓您可以適當叫用或鎖定API。

1. 登入適當的作者執行個體，並導覽至 **設定** > **安全性** > **許可權**
1. 在左側窗格中，搜尋與產品設定檔相對應的群組名稱（在此案例中為「唯讀API」），然後選取它：

   ![搜尋群組](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 在下列視窗中按一下「編輯」按鈕：

   ![編輯權限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 適當修改許可權，然後按一下 **儲存**

   ![確認編輯許可權](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>進一步瞭解AdobeIdentity Management System (IMS)和AEM使用者和群組。 請參閱 [檔案](/help/security/ims-support.md).

## 開發人員流程 {#developer-flow}

開發人員可能想要使用非AEM應用程式的開發執行個體進行測試（在他們的筆記型電腦上執行或託管），該應用程式會向開發AEMas a Cloud Service開發環境發出請求。 不過，由於開發人員不一定具備IMS管理員角色許可權，因此Adobe不能假設他們可以產生一般伺服器對伺服器流程中說明的JWT持有者。 因此，Adobe為開發人員提供了一種直接產生存取權杖的機制，可用於對AEMas a Cloud Service上他們有權存取的環境的請求。

請參閱 [開發人員指南檔案](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 以取得使用AEMas a Cloud Service開發人員控制檯所需許可權的相關資訊。

>[!NOTE]
>
>本機開發存取權杖的有效期最長為24小時，之後必須使用相同方法重新產生。

開發人員可使用此代號，從非AEM測試應用程式呼叫AEMas a Cloud Service環境。 開發人員通常會在自己的筆記型電腦上，將此Token與非AEM應用程式搭配使用。 此外，AEM as a Cloud通常是非生產環境。

開發人員流程涉及以下步驟：

* 從開發人員控制檯產生存取權杖
* 使用存取權杖呼叫AEM應用程式。

開發人員也可以對其本機電腦上執行的AEM專案進行API呼叫，這種情況下不需要存取權杖。

### 產生存取權杖 {#generating-the-access-token}

1. 前往 **本機權杖** 在 **整合**
1. 按一下 **取得本機開發權杖** ，以便產生存取權杖。

### 使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「Authorization」標頭，請使用值 `"Bearer <access_token>"`.

## 重新整理認證 {#refresh-credentials}

根據預設，AEMas a Cloud Service上的認證在一年後過期。 為確保服務的連續性，開發人員可以選擇重新整理憑證，將其可用性延長一年。

若要達到此重新整理擴充功能，請執行下列動作：

* 使用 **新增憑證** 按鈕在 **整合** - **技術帳戶** 在開發人員控制檯中，如下所示

  ![認證重新整理](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按鈕後，會產生一組包含新憑證的認證。 在off-AEM伺服器上安裝新憑證，並確保如預期般連線，而不移除舊憑證。
* 產生存取權杖時，請務必使用新憑證，而非舊憑證。
* 選擇性地撤銷（然後刪除）先前的憑證，使其無法再用來向AEMas a Cloud Service進行驗證。

## 認證撤銷 {#credentials-revocation}

如果私密金鑰遭到破壞，您必須使用新的憑證和新的私密金鑰來建立認證。 應用程式使用新認證來產生存取權杖後，您可以執行下列動作來撤銷和刪除舊憑證：

1. 首先，新增金鑰。 此金鑰會產生具有新私密金鑰和新憑證的認證。 新的私密金鑰在使用者介面中標示為 **目前** 因此，和將用於此技術帳戶日後的所有新憑證。 與舊版私密金鑰關聯的認證在撤銷前仍然有效。 若要達成此撤銷，請選取三個點(**...**)，然後選取「 」 **新增私人金鑰**：

   ![新增私人金鑰](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 選取 **新增** 出現以下提示時：

   ![確認新增新的私密金鑰](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   具有新憑證的新瀏覽標籤隨即開啟，且使用者介面會更新，以顯示具有標籤為的新私密金鑰的兩個私密金鑰 **目前**：

   ![UI中的私密金鑰](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM伺服器上安裝新認證，並確保連線正常運作。 另請參閱 [伺服器對伺服器流量區段](#the-server-to-server-flow) 以取得詳細資訊。
1. 選取三個點(**...**)，然後選取 **撤銷**：

   ![撤銷憑證](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然後，在下列提示中按下 **撤銷** 按鈕：

   ![撤銷憑證確認](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後，刪除已洩漏的憑證。
