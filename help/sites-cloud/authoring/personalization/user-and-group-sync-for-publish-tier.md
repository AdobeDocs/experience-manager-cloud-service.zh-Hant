---
title: 註冊、登入和使用者個人資料
description: 瞭解AEM as a Cloud Service的註冊、登入、使用者資料和群組同步
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---

# 註冊、登入和使用者個人資料 {#registration-login-and-userprofile}

## 簡介 {#introduction}

Web應用程式通常提供帳戶管理功能，讓使用者可在網站上註冊，持續儲存其使用者資料資訊，以便日後登入並享有一致的體驗。 本文說明AEM as a Cloud Service的下列概念：

* 註冊
* 登入
* 儲存使用者設定檔資料
* 群組成員資格
* 資料同步

## 註冊 {#registration}

當一般使用者在AEM應用程式上註冊帳戶時，會在AEM Publish服務上建立使用者帳戶，這反映在JCR存放庫中`/home/users`下的使用者資源上。

實作註冊的方法有兩種，如下所述。

### AEM已管理 {#aem-managed-registration}

您可以撰寫自訂註冊代碼，至少需要使用者的使用者名稱和密碼，並在AEM中建立使用者記錄，之後可在登入期間用於驗證。 以下步驟通常用於建構此註冊機制：

1. 顯示收集註冊資訊的自訂AEM元件
1. 提交後，系統會使用適當布建的服務使用者，
   1. 使用UserManager API的`findAuthorizables()`方法之一來確認現有的使用者不存在
   1. 使用UserManager API的`createUser()`方法之一建立使用者記錄
   1. 儲存使用可授權介面的`setProperty()`方法擷取的任何設定檔資料
1. 選擇性流程，例如要求使用者驗證其電子郵件。

**先決條件：**

若要讓上述邏輯正確運作，請透過提交來啟用[資料同步處理](#data-synchronization-data-synchronization)
向客戶支援提出請求，說明適當的計畫和環境。

### 外部 {#external-managed-registration}

在某些情況下，註冊或使用者建立之前都發生在AEM之外的基礎結構中。 在這種情況下，使用者記錄會在登入期間在AEM中建立。

## 登入 {#login}

一旦終端使用者在AEM Publish服務上註冊，這些使用者就可以登入以獲得已驗證的存取權(使用AEM授權機制)並儲存使用者特有的資料，例如設定檔資料。

## 實作 {#implementation}

可透過下列兩種方法實作登入：

### AEM已管理 {#aem-managed-implementation}

客戶可以編寫自己的自訂元件。 若要進一步瞭解，請考慮熟悉：

* [Sling驗證架構](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 並考慮[向AEM Community Experts座談會](https://bit.ly/ATACEFeb15)詢問登入的相關資訊。

**先決條件：**

若要讓上述邏輯正確運作，請透過提交來啟用[資料同步處理](#data-synchronization-data-synchronization)
向客戶支援提出請求，說明適當的計畫和環境。

### 與身分提供者整合 {#integration-with-an-idp}

客戶可以與IdP （身分提供者）整合，以便驗證使用者。 整合技術包括SAML和OAuth/SSO，如下所述。

以&#x200B;**SAML為基礎**

客戶可透過其偏好的SAML IdP使用SAML型驗證。 搭配AEM使用IdP時，IdP會負責驗證使用者的認證並代理使用者與AEM的驗證、視需要在AEM中建立使用者記錄，以及管理AEM中的使用者群組成員資格，如SAML判斷提示所述。

>[!NOTE]
>
>IdP只會驗證使用者認證的初始驗證，而只要AEM有Cookie可用，後續對AEM的請求就會使用登入權杖Cookie執行。

請參閱檔案以取得有關[SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=zh-Hant)的詳細資訊。

**OAuth/SSO**

請參閱[單一登入(SSO)檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html?lang=zh-Hant)，以取得使用AEM SSO驗證處理常式服務的相關資訊。

您可以使用您選擇的OAuth提供者實作`com.adobe.granite.auth.oauth.provider`介面。

**先決條件：**

依據最佳做法的要求，在儲存使用者特定資料時，請一律依賴idP （身分提供者）當作單一信任點。 如果其他使用者資訊儲存在本機存放庫中（不是idP的一部分），請透過提交要求給客戶支援，指出適當的程式和環境，以啟用[資料同步處理](#data-synchronization-data-synchronization)。 除了[資料同步處理](#data-synchronization-data-synchronization)，在SAML驗證提供者的情況下，請確定已啟用[動態群組成員資格](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)。

### 粘性工作階段和封裝的Token {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service會啟用Cookie式粘性工作階段，確保每個請求都會將一般使用者路由至相同的發佈節點。 在特殊情況下（例如使用者流量尖峰），封裝代號功能可能會提高效能，因此不需要在每次請求時參照存放庫中的使用者記錄。 如果一般使用者具有相似性的發佈節點被取代，則其使用者ID記錄可在新的發佈節點上使用，如下面的[資料同步](#data-synchronization-data-synchronization)區段所述。

若要利用封裝的Token功能，請向客戶支援提交請求，並指明適當的計畫和環境。 更重要的是，封裝的Token無法在沒有[資料同步處理](#data-synchronization-data-synchronization)的情況下啟用，而且必須同時啟用。 因此，在啟用之前請仔細檢閱使用案例，並確保該功能至關重要。

## 使用者設定檔 {#user-profile}

根據資料的性質，有多種方法可持續儲存資料。

### AEM存放庫 {#aem-repository}

使用者設定檔資訊的寫入和讀取方式有兩種：

* 伺服器端使用搭配`com.adobe.granite.security.user` Interface UserPropertiesManager介面，這會將資料放在`/home/users`的使用者節點下。 確保不快取每位使用者不重複的頁面。
* 使用ContextHub的使用者端，如[檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=zh-Hant#personalization)所述。

**先決條件：**

若要讓伺服器端使用者設定檔持續性邏輯正確運作，請透過提交來啟用[資料同步處理](#data-synchronization-data-synchronization)
向客戶支援提出請求，說明適當的計畫和環境。

### 協力廠商資料存放區 {#third-party-data-stores}

一般使用者資料可傳送給第三方廠商（例如CRM），並在使用者登入AEM時透過API擷取，並在AEM使用者的設定檔節點上保留（或更新），並視需要供AEM使用。

可以即時存取協力廠商服務以擷取設定檔屬性，但請務必確保這不會對AEM中的請求處理造成重大影響。

**先決條件：**

若要讓上述邏輯正確運作，請透過提交來啟用[資料同步處理](#data-synchronization-data-synchronization)
向客戶支援提出請求，說明適當的計畫和環境。

## 許可權（已關閉的使用者群組） {#permissions-closed-user-groups}

Publish層存取原則(也稱為封閉式使用者群組(CUG))是在AEM作者中定義的，請參閱[建立封閉式使用者群組](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=zh-Hant#applying-your-closed-user-group-to-content-pages)。 若要限制某些使用者存取網站的某些區段或頁面，請視需要使用AEM作者套用CUG （如此處所述），並將它們復寫至發佈階層。

* 如果使用者透過使用SAML向身分提供者(IdP)進行驗證來登入，驗證處理常式將識別使用者的群組成員資格（應與發佈層上的CUG相符），並透過存放庫記錄保留使用者與群組之間的關聯
* 如果在沒有IdP整合的情況下完成登入，則自訂程式碼可以套用相同的存放庫結構關係。

獨立於登入，自訂程式碼也可以根據組織的獨特要求保留和管理使用者的群組成員資格。

## 資料同步 {#data-synchronization}

網站一般使用者期望在每個網頁請求上獲得一致的體驗，甚至當他們使用不同的瀏覽器登入時，即使他們不知道，也會被帶到發佈層級基礎架構的不同伺服器節點。 AEM as a Cloud Service透過在發佈層級的所有節點之間快速同步`/home`資料夾階層（使用者設定檔資訊、群組成員資格等）來完成此操作。

與其他AEM解決方案不同，AEM as a Cloud Service中的使用者和群組成員資格同步化不使用點對點傳訊方法，而是實作不需要客戶設定的發佈 — 訂閱方法。

>[!NOTE]
>
>依預設，使用者設定檔和群組成員資格同步不會啟用，因此資料不會同步至發佈層，甚至不會永久儲存至發佈層。 若要啟用此功能，請傳送要求給客戶支援，指出適當的方案和環境。

>[!IMPORTANT]
>
>在生產環境中啟用資料同步之前，請先大規模測試實作。 視使用案例和儲存的資料而定，可能會發生一些一致性和延遲問題。

## 快取注意事項 {#cache-considerations}

已驗證的HTTP請求可能很難在CDN和Dispatcher上快取，因為它們可能會將使用者特定的狀態當作請求回應的一部分來傳輸。 不小心快取已驗證的請求並將它們提供給其他請求瀏覽器可能會導致不正確的體驗，甚至洩露受保護或使用者的資料。

在支援使用者特定回應的同時維持請求的高快取能力的方法包括：

* AEM Dispatcher許可權敏感型快取
* Sling動態包含
* AEM ContextHub
