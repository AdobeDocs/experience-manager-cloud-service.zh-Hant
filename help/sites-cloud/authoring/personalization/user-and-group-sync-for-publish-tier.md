---
title: '註冊、登入和使用者設定檔 '
description: 瞭解發佈層的註冊、登入和使用者設定檔
translation-type: tm+mt
source-git-commit: 2c00c3723c3c84365044b5cd2fe6779de0360736
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# 註冊、登錄和用戶配置檔案{#registration-login-and-userprofile}

## 簡介 {#introduction}

Web應用程式通常提供帳戶管理功能，讓使用者可在網站上註冊，而網站會保留其使用者個人檔案資訊，讓使用者日後可登入，並享有一致的使用體驗。 本文說明：

* 註冊
* 登入
* 儲存用戶配置檔案資料
* 群組成員資格
* 資料同步

>[!IMPORTANT]
>
>為了使本文所述的功能發揮作用，必須啟用「用戶資料同步」功能，此時需要向客戶支援部門發出請求，指明適當的程式和環境。 若未啟用，則使用者資訊將僅保存一段短時間（1到24小時），然後消失。

## 註冊{#registration}

當使用者在AEM應用程式上註冊帳戶時，會在AEM Publish服務上建立使用者帳戶，如JCR儲存庫中`/home/users`下的使用者資源所反映。

實施登記有兩種方法，如下所述。

### AEM Managed {#aem-managed-registration}

您可以編寫自訂註冊代碼，至少需要使用使用者的使用者名稱和密碼，並在AEM中建立使用者記錄，然後在登入期間用來驗證。 以下步驟通常用於構建此註冊機制：

1. 顯示收集註冊資訊的自訂AEM元件
1. 提交時，會使用正確布建的服務使用者
   1. 使用UserManager API的`findAuthorizables()`方法之一，驗證現有用戶是否不存在
   1. 使用UserManager API的`createUser()`方法之一建立用戶記錄
   1. 保存使用可授權介面的`setProperty()`方法擷取的任何描述檔資料
1. 可選流量，例如要求使用者驗證其電子郵件。

### 外部 {#external-managed-registration}

在某些情況下，註冊或使用者建立之前發生在AEM以外的基礎架構中。 在該案例中，使用者記錄是在登入期間在AEM中建立。

## 登入 {#login}

在AEM Publish服務上註冊使用者後，這些使用者就可以登入以取得驗證存取權（使用AEM授權機制）並持續存取使用者特定資料，例如描述檔資料。

## 實施 {#implementation}

登入可透過下列兩種方式實作：

### AEM Managed {#aem-managed-implementation}

客戶可以自行編寫自訂元件。 若要進一步瞭解，請考慮熟悉：

* [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 請考慮[詢問AEM社群專家工作階段](http://bit.ly/ATACEFeb15)的登入資訊。

### 與身分提供者{#integration-with-an-idp}整合

客戶可以與驗證使用者身分的IdP（身分提供者）整合。 整合技術包括SAML和OAuth/SSO，如下所述。

**基於SAML**

客戶可以透過偏好的SAML IdP，使用SAML驗證。 將IdP與AEM搭配使用時，IdP負責驗證使用者的認證，並協調使用AEM的使用者驗證、視需要在AEM中建立使用者記錄，以及管理AEM中的使用者群組成員資格，如SAML斷言所述。

>[!NOTE]
>
>只有使用者認證的初始驗證才會由IdP驗證，而後續的AEM請求會使用AEM登入Token Cookie來執行，只要Cookie可用。

如需[SAML 2.0驗證處理常式](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler)的詳細資訊，請參閱檔案。

**OAuth/SSO**

如需使用AEM的SSO驗證處理常式服務的詳細資訊，請參閱[單一登入(SSO)檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)。

`com.adobe.granite.auth.oauth.provider`介面可與您選擇的OAuth提供者一起實作。

### 自黏作業和封裝的Token {#sticky-sessions-and-encapsulated-tokens}

AEM做為雲端服務已啟用Cookie式自黏作業，可確保使用者在每次請求時都會路由至相同的發佈節點。 為了提高效能，預設會啟用封裝的Token功能，因此資料庫中的使用者記錄不需要在每個請求上參考。 如果替換了最終用戶具有相關性的發佈節點，則新發佈節點上將可以使用其用戶ID記錄，如下面的資料同步部分所述。

## 使用者設定檔 {#user-profile}

根據資料的性質，有多種持續資料的方法。

### AEM Repository {#aem-repository}

用戶配置檔案資訊可以通過兩種方式編寫和讀取：

* 伺服器端與`com.adobe.granite.security.user`介面UserPropertiesManager介面搭配使用，此介面會將資料放在`/home/users`使用者節點下方。 請確定未快取每個使用者唯一的頁面。
* 使用ContextHub的用戶端，如[說明檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)所述。

### 協力廠商資料儲存{#third-party-data-stores}

使用者登入AEM後，可將使用者資料傳送至協力廠商（例如CRM），並透過API擷取，並持續（或重新整理）在AEM使用者的設定檔節點上，AEM會視需要使用。

可即時存取協力廠商服務以擷取描述檔屬性，但是，請務必確保這不會對AEM中的請求處理造成實質影響。

## 權限（已關閉的使用者群組）{#permissions-closed-user-groups}

發佈層存取政策(也稱為「已關閉的使用者群組」(CUG))在AEM作者中定義為[，如此處](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)所述。 若要限制某些使用者瀏覽某個網站的特定區段或頁面，請視需要使用AEM作者套用CUG（如此處所述），並將它們複製至發佈層。

* 如果使用者使用SAML與身分提供者(IdP)驗證登入，驗證處理常式會識別使用者的群組成員資格（應符合發佈層上的CUG），並透過儲存庫記錄保存使用者與群組之間的關聯
* 如果在未整合IdP的情況下完成登入，自訂程式碼可以套用相同的儲存庫結構關係。

自訂程式碼不受登入限制，也可以根據組織的獨特需求來保存和管理使用者的群組成員資格。

## 資料同步{#data-synchronization}

網站使用者希望每次網頁要求或使用不同瀏覽器登入時，都能獲得一致的體驗，即使他們不知情，也會被帶到發佈層基礎架構的不同伺服器節點。 AEM作為Cloud Service，可透過快速同步化發佈層所有節點的`/home`資料夾階層（使用者設定檔資訊、群組成員資格等）來達成此目的。

與其他AEM解決方案不同，AEM中的使用者和群組會籍同步化(Cloud Service)不會使用點對點傳訊方式，而是實作不需要客戶設定的發佈訂閱方式。

>[!NOTE]
>
>依預設，使用者設定檔和群組成員資格同步不會啟用，因此資料不會同步至發佈層，甚至不會永久保存在發佈層。 若要啟用此功能，請傳送要求給客戶支援，指出適當的方案和環境。

## 快取注意事項{#cache-considerations}

CDN和Dispatcher上的已驗證HTTP請求都可能會傳送使用者特定狀態作為請求回應的一部分，因此很難快取。 不慎將已驗證的請求快取，並將其提供給其他要求的瀏覽器，可能會導致不正確的體驗，甚至會洩露受保護或使用者資料。

在支援使用者特定回應的同時維持要求高快取能力的方法包括：

* AEM Dispatcher權限敏感快取
* Sling Dynamic Include
* AEM ContextHub