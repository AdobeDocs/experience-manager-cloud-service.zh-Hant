---
title: '註冊、登入和使用者設定檔 '
description: 瞭解註冊、登錄、用戶資料和組同步，AEM作為Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
translation-type: tm+mt
source-git-commit: 4d76d8bac41e19168abb1819841dfc62be07ea0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# 註冊、登錄和用戶配置檔案{#registration-login-and-userprofile}

## 簡介 {#introduction}

Web應用程式通常提供帳戶管理功能，讓使用者可在網站上註冊，而網站會保留其使用者資料資訊，讓使用者日後可登入，並享有一致的體驗。 本文將以下概念AEM說明為Cloud Service:

* 註冊
* 登入
* 儲存用戶配置檔案資料
* 群組成員資格
* 資料同步

>[!IMPORTANT]
>
>為了使本文所述的功能發揮作用，必須啟用「用戶資料同步」功能，此時需要向客戶支援部門發出請求，指明適當的程式和環境。 若未啟用，則使用者資訊將僅保存一段短時間（1到24小時），然後消失。

## 註冊{#registration}

當使用者在應用程式上註冊帳戶時AEM，會在AEM Publish服務上建立使用者帳戶，如JCR儲存庫中`/home/users`下的使用者資源所反映。

實施登記有兩種方法，如下所述。

### 受AEM管{#aem-managed-registration}

自訂註冊碼可以撰寫，至少需要使用使用者的使用者名稱和密碼，並建立使用者記錄，AEM然後在登入期間用來驗證。 以下步驟通常用於構建此註冊機制：

1. 顯示收集注AEM冊資訊的自訂元件
1. 提交時，會使用正確布建的服務使用者
   1. 使用UserManager API的`findAuthorizables()`方法之一，驗證現有用戶是否不存在
   1. 使用UserManager API的`createUser()`方法之一建立用戶記錄
   1. 保存使用可授權介面的`setProperty()`方法擷取的任何描述檔資料
1. 可選流量，例如要求使用者驗證其電子郵件。

### 外部 {#external-managed-registration}

在某些情況下，註冊或用戶建立以前發生在外部的基礎架構中AEM。 在該案例中，使用者記錄是在登入時AEM建立的。

## 登入 {#login}

在AEM Publish服務上註冊使用者後，這些使用者就可以登入以取得驗證存取權(使用授權機制AEM)並持續存取使用者特定資料，例如描述檔資料。

## 實施 {#implementation}

登入可透過下列兩種方式實作：

### 受AEM管{#aem-managed-implementation}

客戶可以自行編寫自訂元件。 若要進一步瞭解，請考慮熟悉：

* [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 請考慮[詢問社群專AEM家工作階段](http://bit.ly/ATACEFeb15)的登入資訊。

### 與身分提供者{#integration-with-an-idp}整合

客戶可以與驗證使用者身分的IdP（身分提供者）整合。 整合技術包括SAML和OAuth/SSO，如下所述。

**基於SAML**

客戶可以透過偏好的SAML IdP，使用SAML驗證。 使用IdP與時AEM,IdP負責驗證使用者的認證，並透過AEM中介使用者的驗證、視需要建立使用者記AEM錄，以及依SAML斷言所述，在中管AEM理使用者群組成員資格。

>[!NOTE]
>
>只有使用者認證的初始驗證才會由IdP驗證，且只要CookieAEM可用AEM，就會使用登入Token Cookie來執行後續的要求。

如需[SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler)的詳細資訊，請參閱檔案。

**OAuth/SSO**

如需使用SSO驗證處理常式服務的相關資訊，請參閱[單一登入(SSO)檔案&lt;a1/AEM>。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)

`com.adobe.granite.auth.oauth.provider`介面可與您選擇的OAuth提供者一起實作。

### 自黏作業和封裝的Token {#sticky-sessions-and-encapsulated-tokens}

由AEM於Cloud Service已啟用Cookie型自黏工作階段，因此可確保使用者在每次請求時都會路由至相同的發佈節點。 為了提高效能，預設會啟用封裝的Token功能，因此資料庫中的使用者記錄不需要在每個請求上參考。 如果替換了最終用戶具有相關性的發佈節點，則新發佈節點上將可以使用其用戶ID記錄，如下面的資料同步部分所述。

## 使用者設定檔 {#user-profile}

根據資料的性質，有多種持續資料的方法。

### AEM儲存庫{#aem-repository}

用戶配置檔案資訊可以通過兩種方式編寫和讀取：

* 伺服器端與`com.adobe.granite.security.user`介面UserPropertiesManager介面搭配使用，此介面會將資料放在`/home/users`使用者節點下方。 請確定未快取每個使用者唯一的頁面。
* 使用ContextHub的用戶端，如[說明檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)所述。

### 協力廠商資料儲存{#third-party-data-stores}

使用者登入使用者的描述檔節點並持續（或重新整理）在使用者的描述檔節點上，並視需要使用，您可以將使用者資料傳送至協力廠商（例如CRM）,AEM並透過APIAEM來擷取。

可即時存取協力廠商服務以擷取描述檔屬性，但是，請務必確保這不會對中的要求處理產生實質影響AEM。

## 權限（已關閉的使用者群組）{#permissions-closed-user-groups}

發佈層訪問策略(也稱為「已關閉的用戶組」(CUG))在作者中AEM定義為[，如此處](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)所述。 為了限制某些使用者瀏覽某網站的特定區段或頁面，請視需要使用作者套用CUG(如AEM此所述)，並將它們複製至發佈層。

* 如果使用者使用SAML與身分提供者(IdP)驗證登入，驗證處理常式會識別使用者的群組成員資格（應符合發佈層上的CUG），並透過儲存庫記錄保存使用者與群組之間的關聯
* 如果在未整合IdP的情況下完成登入，自訂程式碼可以套用相同的儲存庫結構關係。

自訂程式碼不受登入限制，也可以根據組織的獨特需求來保存和管理使用者的群組成員資格。

## 資料同步{#data-synchronization}

網站使用者希望每次網頁要求或使用不同瀏覽器登入時，都能獲得一致的體驗，即使他們不知情，也會被帶到發佈層基礎架構的不同伺服器節點。 作AEM為Cloud Service，可快速同步發佈層所有節點的`/home`資料夾階層（使用者描述檔資訊、群組成員資格等），以達成此目的。

與其他AEM解決方案不同，Cloud Service中的用戶和群組成員AEM同步不使用點對點傳訊方式，而是實作不需要客戶設定的發佈訂閱方式。

>[!NOTE]
>
>依預設，使用者設定檔和群組成員資格同步不會啟用，因此資料不會同步至發佈層，甚至不會永久保存在發佈層。 若要啟用此功能，請傳送要求給客戶支援，指出適當的方案和環境。

## 快取注意事項{#cache-considerations}

CDN和Dispatcher上的已驗證HTTP請求都可能會傳送使用者特定狀態作為請求回應的一部分，因此很難快取。 不慎將已驗證的請求快取，並將其提供給其他要求的瀏覽器，可能會導致不正確的體驗，甚至會洩露受保護或使用者資料。

在支援使用者特定回應的同時維持要求高快取能力的方法包括：

* AEM Dispatcher Permissions sensitive caching
* Sling Dynamic Include
* ContextHub
