---
title: AEM as a Cloud Service 安全性注意事項
description: 了解使用 AEM as a Cloud Service 時的重要安全性注意事項
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 93%

---

# AEM as a Cloud Service 安全性注意事項 {#security-considerations}

## AEM Trust Store {#aem-trust-store}

為了支援非對稱的密碼編譯操作，AEM會將憑證儲存在全域信任存放區的內容存放庫中。 其內容是公開的，根據預設，發佈者執行個體上的所有人都可以匿名存取。

### Trust Store 的特色 {#truststore-characteristics}

* Trust-store 於 `/etc/truststore` 下方，由 Java keystore 檔案、keystore 密碼和存放庫中繼資料組成。請注意，由於技術原因，密碼和 keystore 本身都已加密，即使根據預設，所有人都可以透過 API 存取包含的憑證
* 現成的憑證僅用於 HTTPS 和 SAML 支援，必須先手動建立存放區
* 客戶可以透過 [keystore API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-) 在自己的程式碼中使用它
* 可透過&#x200B;**工具** - **安全性** - **Trust Store**，或存取 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`* 來管理 trust-store，如下所示：

  ![Trust Store 管理](/help/security/assets/global-trust-store-modified.png)

* 根據使用案例，可以透過存放庫存取控制進一步限制對 trust-store 的存取權。

>[!NOTE]
>
>Adobe 建議對 Trust Store 使用預設存取控制，這代表它仍然可以公開存取。如需最安全的設定，您可以對所有人使用拒絕 jcr:all 的原則。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
