---
title: '註冊、登錄和用戶配置檔案 '
description: 瞭解有關註冊、登錄、用戶資料和組同步的AEMas a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: c49a70b4048acc4e925c69b7ebbedbf8779bbbc0
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# 註冊、登錄和用戶配置檔案 {#registration-login-and-userprofile}

## 簡介 {#introduction}

Web應用程式通常提供帳戶管理功能，供最終用戶在網站上註冊，這會保留其用戶資料資訊，允許他們將來登錄，並享受一致的體驗。 本文介紹以下AEMas a Cloud Service概念：

* 註冊
* 登入
* 儲存用戶配置檔案資料
* 組成員身份
* 資料同步

>[!IMPORTANT]
>
>為了使本文中描述的功能發揮作用，必須啟用用戶資料同步功能，此時需要向客戶支援部門發出請求，以指明適當的程式和環境。 如果未啟用，則用戶資訊將僅保留一段時間（1至24小時），然後才會消失。

## 註冊 {#registration}

當最終用戶在應用程式上註冊帳戶時AEM，在AEM發佈服務上建立用戶帳戶，如在下面的用戶資源上反映的 `/home/users` 在JCR儲存庫中。

如下所述，實施登記有兩種方法。

### 托AEM管 {#aem-managed-registration}

可以編寫自定義註冊代碼，該代碼至少需要最終用戶的用戶名和密碼，並建立用戶記錄，AEM然後可在登錄過程中用於驗證用戶記錄。 通常使用以下步驟構建此註冊機制：

1. 顯示收集注AEM冊資訊的自定義元件
1. 提交時，使用正確設定的服務用戶
   1. 使用UserManager API中的一個驗證現有用戶是否不存在 `findAuthorizables()` 方法
   1. 使用UserManager API中的一個建立用戶記錄 `createUser()` 方法
   1. 保留使用可授權介面捕獲的任何配置檔案資料 `setProperty()` 方法
1. 可選流，例如要求用戶驗證其電子郵件。

### 外部 {#external-managed-registration}

在某些情況下，以前在外部的基礎架構中進行過註冊或用戶創AEM建。 在該情況下，用戶記錄在登錄AEM期間建立。

## 登入 {#login}

在AEM發佈服務上註冊最終用戶後，這些用戶可以登錄以具有經過驗證的訪問(使用授權機制AEM)並保留特定於用戶的資料，如配置檔案資料。

## 實施 {#implementation}

可以使用以下兩種方法實現登錄：

### 托AEM管 {#aem-managed-implementation}

客戶可以編寫自己的自定義元件。 要瞭解更多資訊，請考慮熟悉：

* 的 [Sling驗證框架](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 考慮 [詢問社AEM區專家會議](http://bit.ly/ATACEFeb15) 關於登錄。

### 與身份提供程式整合 {#integration-with-an-idp}

客戶可以與IdP（身份提供程式）整合，後者驗證用戶。 整合技術包括SAML和OAuth/SSO，如下所述。

**基於SAML**

客戶可以通過其首選的SAML IdP使用基於SAML的身份驗證。 當將IdP與AEM一起使用時，IdP負責驗證最終用戶的憑據並代理用戶的驗證AEM，根據需AEM要在中建立用戶記錄，以及按照SAML斷言的說明AEM管理用戶的組成員身份。

>[!NOTE]
>
>只有IdP對用戶的憑據進行初始驗證，並且只要Cookie可用，AEM就使用登AEM錄令牌Cookie執行後續請求。

有關 [SAML 2.0身份驗證處理程式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html)。

**OAuth/SSO**

查看 [單一登錄(SSO)文檔](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) 有關使用SSO驗證AEM處理程式服務的資訊。

的 `com.adobe.granite.auth.oauth.provider` 可以使用您選擇的OAuth提供程式實現介面。

### 粘滯會話和封裝的令牌 {#sticky-sessions-and-encapsulated-tokens}

AEMas a Cloud Service啟用了基於cookie的粘滯會話，這確保最終用戶在每個請求上路由到同一發佈節點。 為了提高效能，預設情況下啟用了封裝的令牌功能，因此無需在每個請求上引用儲存庫中的用戶記錄。 如果替換了最終用戶具有關聯性的發佈節點，則其用戶ID記錄將可在新發佈節點上使用，如下面的資料同步部分所述。

## 使用者設定檔 {#user-profile}

根據資料的性質，有多種方法來保存資料。

### 儲存AEM庫 {#aem-repository}

用戶配置檔案資訊可以通過兩種方式寫入和讀取：

* 與 `com.adobe.granite.security.user` 介面UserPropertiesManager介面，該介面將資料放在 `/home/users`。 確保未快取每個用戶唯一的頁面。
* 使用ContextHub的客戶端，如所述 [文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)。

### 第三方資料儲存 {#third-party-data-stores}

最終用戶資料可以發送到第三方供應商，如CRM，並在用戶登錄到用戶配置檔案節點並保留AEM（或刷新）AEM後通過API檢索，並根據需AEM要由使用。

即時訪問第三方服務以檢索配置檔案屬性是可能的，但必須確保這不會對中的請求處理產生實質性影AEM響。

## 權限（關閉的用戶組） {#permissions-closed-user-groups}

發佈層訪問策略(也稱為「已關閉用戶組」(CUG))在作者中定義AEM為 [此處](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)。 為了限制某些用戶訪問某個網站的某些部分或頁面，請使用作者根據需要應用CUGAEM，並將其複製到發佈層。

* 如果用戶通過使用SAML與身份提供程式(IdP)進行身份驗證登錄，則身份驗證處理程式將標識用戶的組成員身份（應與發佈層上的CUG匹配），並通過儲存庫記錄保持用戶與組之間的關聯
* 如果在沒有IdP整合的情況下完成登錄，則自定義代碼可以應用相同的儲存庫結構關係。

與登錄無關，自定義代碼還可以根據組織的獨特要求保留和管理用戶的組成員身份。

## 資料同步 {#data-synchronization}

網站最終用戶期望在每個網頁請求上獲得一致的體驗，甚至當他們使用不同的瀏覽器登錄時，即使他們不知道，他們也會被帶到發佈層基礎架構的不同伺服器節點。 AEMas a Cloud Service通過快速同步 `/home` 資料夾層次結構（用戶配置檔案資訊、組成員身份等）。

與其AEM他解決方案不同，在as a Cloud Service中，用戶和組成員身份同AEM步不使用點對點消息傳遞方法，而是實施不需要客戶配置的發佈訂閱方法。

>[!NOTE]
>
>預設情況下，不會啟用用戶配置檔案和組成員身份同步，因此資料不會同步到發佈層，甚至不會永久保留在發佈層上。 要啟用該功能，請向客戶支援部門發送請求，以指明適當的計畫和環境。

## 快取注意事項 {#cache-considerations}

鑑定的HTTP請求在CDN和Dispatcher上都很難快取，因為它們具有作為請求響應的一部分傳輸用戶特定狀態的可能性。 無意中快取經過身份驗證的請求並將其提供給其他請求瀏覽器可能會導致不正確的體驗，甚至洩露受保護的或用戶資料。

用於在支援用戶特定響應的同時保持請求的高快取能力的方法包括：

* Dispatcher Permissions敏AEM感快取
* 吊具動態包括
* 上AEM下文
