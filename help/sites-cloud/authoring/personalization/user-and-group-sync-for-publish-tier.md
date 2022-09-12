---
title: 註冊、登入和使用者設定檔
description: 了解AEM的註冊、登入、使用者資料和群組同步as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# 註冊、登入和使用者設定檔 {#registration-login-and-userprofile}

## 簡介 {#introduction}

網路應用程式通常提供帳戶管理功能，供一般使用者在網站上註冊，這會保存其使用者資料資訊，讓他們日後可登入，並享有一致的體驗。 本文說明AEMas a Cloud Service的下列概念：

* 註冊
* 登入
* 儲存用戶配置檔案資料
* 群組成員資格
* 資料同步

>[!IMPORTANT]
>
>為了讓本文所述的功能發揮作用，必須啟用「用戶資料同步」功能，此時需要向客戶支援部門發出請求，指明適當的程式和環境。 若未啟用，使用者資訊只會保存一段短時間（1到24小時），然後消失。

## 註冊 {#registration}

一般使用者在AEM應用程式上註冊帳戶時，會在AEM Publish服務上建立使用者帳戶，如下方的使用者資源所反映 `/home/users` 在JCR存放庫中。

執行登記有兩種辦法，如下所述。

### AEM Managed {#aem-managed-registration}

可以寫入自定義註冊代碼，最少使用最終用戶的用戶名和密碼，並在AEM中建立用戶記錄，然後用於在登錄期間對其進行身份驗證。 通常會使用下列步驟來建構此註冊機制：

1. 顯示收集註冊資訊的自訂AEM元件
1. 提交時，會使用正確布建的服務使用者
   1. 使用UserManager API的 `findAuthorizables()` 方法
   1. 使用UserManager API的其中一個 `createUser()` 方法
   1. 保留使用可授權介面擷取的任何設定檔資料 `setProperty()` 方法
1. 可選流量，例如要求使用者驗證其電子郵件。

### 外部 {#external-managed-registration}

在某些情況下，註冊或使用者建立之前發生在AEM以外的基礎架構中。 在該案例中，使用者記錄會在登入期間於AEM中建立。

## 登入 {#login}

在AEM Publish服務上註冊一般使用者後，這些使用者就能登入以取得已驗證的存取權(使用AEM授權機制)，並保存使用者專屬的資料，例如設定檔資料。

## 實施 {#implementation}

登入可透過下列兩種方法實作：

### AEM Managed {#aem-managed-implementation}

客戶可以撰寫自己的自訂元件。 若要進一步了解，請考慮熟悉：

* 此 [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 請考慮 [詢問AEM社群專家會議](https://bit.ly/ATACEFeb15) 關於登入。

### 與身分提供者整合 {#integration-with-an-idp}

客戶可與驗證使用者的IdP（身分提供者）整合。 整合技術包括SAML和OAuth/SSO，如下所述。

**基於SAML**

客戶可透過其慣用的SAML IdP，使用SAML型驗證。 將IdP與AEM搭配使用時，IdP負責驗證一般使用者的憑證，並透過AEM代理使用者的驗證、視需要在AEM中建立使用者記錄，以及按照SAML斷言的說明管理AEM中的使用者群組成員資格。

>[!NOTE]
>
>只有IdP會驗證使用者認證的初始驗證，且只要Cookie可用，後續的AEM請求就會使用AEM登入Token Cookie來執行。

如需 [SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

請參閱 [單一登入(SSO)檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) 有關使用AEM SSO驗證處理程式服務的資訊。

此 `com.adobe.granite.auth.oauth.provider` 介面可透過您選擇的OAuth提供者來實作。

### 黏著工作階段和封裝的Token {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service已啟用cookie式自黏工作階段，可確保將一般使用者路由至每個請求上的相同發佈節點。 為了提高效能，預設會啟用封裝的Token功能，因此每次請求都不需要參考存放庫中的使用者記錄。 如果取代了一般使用者與之有相關性的發佈節點，則其使用者ID記錄將可在新的發佈節點上使用，如下方資料同步一節所述。

## 使用者設定檔 {#user-profile}

根據資料的性質，持續保存資料有多種方法。

### AEM存放庫 {#aem-repository}

用戶配置檔案資訊可以通過兩種方式寫入和讀取：

* 伺服器端搭配使用 `com.adobe.granite.security.user` 介面UserPropertiesManager介面，該介面會將資料放在 `/home/users`. 請確定系統不會快取每位使用者唯一的頁面。
* 使用ContextHub的用戶端，如所述 [檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### 協力廠商資料儲存 {#third-party-data-stores}

一般使用者資料可傳送給協力廠商（例如CRM），並在使用者登入AEM時透過API擷取，並在AEM使用者的設定檔節點上保存（或重新整理），並視需要供AEM使用。

您可以即時存取第三方服務以擷取設定檔屬性，但請務必確保這不會對AEM中的請求處理造成重大影響。

## 權限（封閉的使用者群組） {#permissions-closed-user-groups}

發佈層級存取原則(又稱為封閉使用者群組(CUG))在AEM作者中定義為 [此處說明](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). 若要限制某些使用者的網站特定區段或頁面，請視需要使用AEM作者套用CUG（如此處所述），並將其複製到發佈層級。

* 如果使用者使用SAML與身分提供者(IdP)進行驗證來登入，驗證處理常式會識別使用者的群組成員資格（這應符合發佈層級的CUG），並透過存放庫記錄來保存使用者與群組之間的關聯
* 如果在不整合IdP的情況下完成登入，則自訂程式碼可套用相同的存放庫結構關係。

自訂程式碼也可以根據組織的獨特需求，以不受登入影響的方式保留及管理使用者的群組成員資格。

## 資料同步 {#data-synchronization}

網站使用者期望在每個網頁要求上，甚至在使用不同瀏覽器登入時，都能獲得一致的體驗，即使他們不知道，也會將他們帶到發佈層級基礎架構的不同伺服器節點。 AEMas a Cloud Service快速同步，借此完成此作業 `/home` 發佈層級中所有節點的資料夾階層（使用者設定檔資訊、群組成員資格等）。

與其他AEM解決方案不同，AEMas a Cloud Service中的使用者和群組成員資格同步不使用點對點傳訊方法，而是實作不需要客戶設定的發佈訂閱方法。

>[!NOTE]
>
>依預設，不會啟用使用者設定檔和群組成員資格同步，因此資料不會同步至發佈層級，甚至不會永久保存在發佈層級。 若要啟用此功能，請向客戶支援傳送要求，指出適當的方案和環境。

## 快取考量事項 {#cache-considerations}

CDN和Dispatcher上已驗證的HTTP請求可能會很難快取，因為它們可能會隨著請求回應而傳輸使用者特定狀態。 無意中快取已驗證的請求並將其提供給其他請求的瀏覽器，可能會導致不正確的體驗，或甚至洩漏受保護的或使用者資料。

在支援使用者特定回應的同時，維護要求的高快取能力的方法包括：

* AEM Dispatcher權限相關快取
* Sling Dynamic Include
* AEM ContextHub
