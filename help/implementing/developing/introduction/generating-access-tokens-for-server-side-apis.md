---
title: 為伺服器端 API 產生存取權杖
description: 瞭解如何通過生成安全的JWT令牌AEM來促進第三方伺服器與as a Cloud Service之間的通信
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: dd869397feca593f93ee8ed5030828e01cc45c4d
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---

# 為伺服器端 API 產生存取權杖 {#generating-access-tokens-for-server-side-apis}

某些體系結構依賴呼叫AEMas a Cloud Service於在基礎架構之外的伺服器上承載的AEM應用程式。 例如，調用伺服器的移動應用程式，然後向AEMas a Cloud Service請求API。

下面介紹了伺服器到伺服器的流程，以及簡化的開發流程。 AEMas a Cloud Service [開發人員控制台](development-guidelines.md#crxde-lite-and-developer-console) 用於生成驗證過程所需的令牌。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器到伺服器流 {#the-server-to-server-flow}

具有IMS組織管理員角色的用戶，以及AEM作者上的AEMUsers或AEMAdministrators產品配置檔案的成員，可以生成一組as a Cloud Service憑據，每個憑據都是JSON負載，包括證書（公鑰）、私鑰和由 `clientId` 和 `clientSecret`。 這些憑據隨後可由具有AEMas a Cloud Service環境管理員角色的用戶檢索，並應安裝在非服AEM務器上，並作為密鑰仔細處理。 此JSON格式檔案包含與as a Cloud ServiceAPI整合所需的所AEM有資料。 該資料用於建立簽名的JWT令牌，該令牌與AdobeIdentity Management服務(IMS)交換以用於IMS接入令牌。 然後，此訪問令牌可用作承載驗證令牌，以向AEMas a Cloud Service請求。 預設情況下，憑據中的證書在一年後過期，但在需要時可以刷新，如所述 [這裡](#refresh-credentials)。

伺服器到伺服器流包括以下步驟：

* 從開發AEM人員控制台獲取as a Cloud Service憑據
* 在非AEM伺服器上安AEM裝as a Cloud Service憑據AEM
* 生成JWT令牌，並使用Adobe的IMS API交換該令牌作為訪問令牌
* 使用訪問AEM令牌作為承載驗證令牌調用API
* 為環境中的技術帳戶用戶設定適當的權AEM限

### 獲取AEMas a Cloud Service憑據 {#fetch-the-aem-as-a-cloud-service-credentials}

對as a Cloud Service開發人員控制AEM台具有訪問權限的用戶將看到給定環境的開發人員控制台中的整合頁籤。 具有「as a Cloud Service環境AEM管理員」角色的用戶可以建立、查看或管理憑據。

按一下 **建立新技術帳戶** 按鈕，將建立一組新的憑據，這些憑據包括客戶端id、客戶端密鑰、私鑰、證書以及環境的作者和發佈層的配置，而不管選擇什麼儲存盒。

![建立新技術帳戶](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

將開啟一個新的瀏覽器頁籤，顯示憑據。 您可以使用此視圖通過按狀態標題旁邊的下載表徵圖下載憑據：

![下載憑據](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

建立憑據後，這些憑據將出現在 **技術客戶** 的 **整合** 部分：

![查看憑據](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

用戶以後可以使用「查看」操作查看憑據。 此外，如文章後面所述，對於需要續訂或吊銷證書的情況，用戶可以通過建立新私鑰或證書來修改同一技術帳戶的憑據。

具有「AEMas a Cloud Service環境管理員」角色的用戶稍後可以為其他技術帳戶建立新憑據。 當不同的API具有不同的訪問要求時，這非常有用。 例如，讀取與讀取。

>[!NOTE]
>
>客戶可以建立最多10個技術帳戶，包括已刪除的帳戶。

>[!IMPORTANT]
>
>IMS組織管理員（通常是通過雲管理器設定環境的同一用戶），也應是AEM作者上的「用戶AEM」或AEM「管理員產品配置檔案」的成員，必須首先訪問開發人員控制台並按一下 **建立新技術帳戶** 的子菜單。 如果IMS組織管理員沒有這樣做，就會收到一條消息通知他們他們需要IMS組織管理員角色。

### 在非服AEM務器上安裝服務憑AEM據 {#install-the-aem-service-credentials-on-a-non-aem-server}

調用的應用程式AEM應能夠訪問as a Cloud Service憑據，AEM將其視為機密。

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

>[!NOTE]
>如果有多個憑據，請確保引用稍後將調用的API調用的AEM相應json檔案。

### 調用AEMAPI {#calling-the-aem-api}

對as a Cloud Service環境（包括頭中的訪問令牌）AEM進行適當的伺服器到伺服器API調用。 因此，對於「授權」標頭，使用 `"Bearer <access_token>"`。 例如，使用 `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在中為技術帳戶用戶設定適當的權AEM限 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，需要在Adobe Admin Console建立新產品配置檔案。 您可以通過以下步驟來實現此目標：

1. 去Adobe Admin Console [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. 按 **管理** 連結 **產品和服務** 列。
1. 選擇 **AEMas a Cloud Service**
1. 按 **新建配置檔案** 按鈕

   ![新建設定檔](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 命名配置檔案並按 **保存**

   ![保存配置檔案](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 從配置檔案清單中選擇剛建立的配置檔案
1. 按 **添加用戶** 按鈕

   ![新增使用者](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 添加您剛建立的技術帳戶（在本例中） `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) **保存**

   ![添加技術帳戶](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 等待10分鐘，使更改生效，並使用從新憑據生AEM成的訪問令牌調用API。 作為cURL命令，它的表示方式與以下示例類似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


進行API調用後，產品配置檔案將作為用戶組出現在AEMas a Cloud Service作者實例中，並且相應的技術帳戶將作為該組的成員。

要檢查此項，您需要：

1. 登錄到作者實例
1. 轉到 **工具** - **安全** 並按一下 **組** 卡
1. 在組清單中找到您建立的配置檔案的名稱，然後按一下：

   ![組配置檔案](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在以下窗口中，切換到 **成員** 頁籤，並檢查此處是否正確列出了技術帳戶：

   ![「成員」頁籤](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以通過對作者實例執行以下步驟來驗證技術帳戶是否出現在用戶清單中：

1. 轉到 **工具** - **安全** - **用戶**
1. 檢查您的技術帳戶是否是用戶清單，然後按一下
1. 按一下 **組** 頁籤，驗證用戶是否是與您的產品配置檔案對應的組的一部分。 此用戶也是其他幾個組（包括參與者）的成員：

   ![群組會籍](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年年中之前，在建立多個憑據之前，未指導客戶在Adobe管理控制台中建立產品配置檔案，因此技術帳戶未與as a Cloud Service實例中「參與者」以外的組AEM關聯。 為了保持一致性，建議您為此技術帳戶在Adobe Admin Console建立新的產品配置檔案，並將現有技術帳戶添加到該組。

<u>**設定適當的組權限**</u>

最後，為組配置適當的權限，以便適當調用或鎖定API。 您可以通過以下方式執行此操作：

1. 登錄到相應的作者實例並轉到 **設定** - **安全** - **權限**
1. 在左窗格中搜索與產品配置檔案對應的組名稱（在本例中為只讀API），然後按一下：

   ![搜索組](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 在以下窗口中按一下「編輯」按鈕：

   ![編輯權限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 適當修改權限並按一下 **保存**

   ![確認編輯權限](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>通過咨詢AdobeIdentity Management系統(IMS)和AEM用戶和組瞭解更多資訊 [文檔](/help/security/ims-support.md)。

## 顯影劑流 {#developer-flow}

開發人員可能希望使用其非應用程式(在其筆記型電腦上運行或托AEM管)的開發實例進行test，該實例向開發as a Cloud Service的開發環境提AEM出請求。 但是，由於開發人員不一定具有IMS管理員角色權限，因此我們不能假設他們能夠生成常規伺服器到伺服器流中描述的JWT承載。 因此，我們為開發者直接生成訪問令牌的機制，該訪問令牌可以用於他AEM們有權訪問的as a Cloud Service環境的請求。

查看 [開發人員指南文檔](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 有關使用as a Cloud Service開發者控制台所需AEM權限的資訊。

>[!NOTE]
>
>本地開發訪問令牌的有效期最長為24小時，此後必須使用相同方法重新生成該令牌。

開發人員可以使用此令牌從其非test應AEM用程式向AEMas a Cloud Service環境進行呼叫。 通常，開發人員會將此令牌與非應用程式一起AEM使用在自己的筆記型電腦上。 此外，AEM作為雲通常是非生產環境。

開發人員流包括以下步驟：

* 從開發人員控制台生成訪問令牌
* 使用訪AEM問令牌調用應用程式。

開發人員還可以對在其本AEM地電腦上運行的項目進行API調用，在這種情況下，不需要訪問令牌。

### 生成訪問令牌 {#generating-the-access-token}

1. 轉到 **本地令牌** 在 **整合**
1. 按一下 **獲取本地開發令牌** 按鈕以生成訪問令牌。

### 使用訪AEM問令牌調用應用程式 {#call-the-aem-application-with-an-access-token}

將相應的伺服器到伺服器API調用從非應用程AEM序到as a Cloud ServiceAEM環境，包括頭中的訪問令牌。 因此，對於「授權」標頭，使用 `"Bearer <access_token>"`。

## 刷新憑據 {#refresh-credentials}

預設情況下，AEMas a Cloud Service憑據將在一年後過期。 為確保服務連續性，開發人員可以選擇刷新憑據，將其可用性延長一年。

要實現此目標，您可以：

* 使用 **添加證書** 按鈕 **整合** - **技術客戶** 如下所示

   ![憑據刷新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按鈕後，將生成包含新證書的一組憑據。 在非伺服器上安裝新憑據AEM，並確保連接正常，而不刪除舊憑據 
* 確保在生成訪問令牌時使用新憑據而不是舊憑據
* （可選）撤銷（然後刪除）先前的證書，以便不再能用它來驗證AEMas a Cloud Service。

## 吊銷憑據 {#credentials-revocation}

如果私鑰被洩露，您需要使用新證書和新私鑰建立憑據。 應用程式使用新憑據生成訪問令牌後，可以撤消和刪除舊證書。

您可以按照以下步驟執行此操作：

1. 首先，添加新密鑰。 這將生成具有新私鑰和新證書的憑據。 新私鑰將在UI中標籤為 **當前** 因此，將用於此技術帳戶今後的所有新憑據。 請注意，與舊私鑰關聯的憑據在撤消之前仍然有效。 要達到此目的，請按三點(**...**)，按 **添加新私鑰**:

   ![添加新私鑰](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 按 **添加** 提示如下：

   ![確認添加新私鑰](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   將開啟一個新的瀏覽頁籤，並更新UI以顯示兩個私鑰，新的頁籤標籤為 **當前**:

   ![UI中的私鑰](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非伺服器上安裝新憑據AEM並確保連接正常。 查看 [「伺服器到伺服器流」部分](#the-server-to-server-flow) 有關如何執行此操作的詳細資訊
1. 撤消舊證書。 通過選擇三點(**...**)，並按 **撤消**:

   ![吊銷證書](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然後，通過按 **撤消** 按鈕：

   ![撤消證書確認](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後，刪除被洩露的證書。
