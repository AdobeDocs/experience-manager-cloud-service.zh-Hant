---
title: AEM as a Cloud Service 安全性注意事項
description: 瞭解使用AEMas a Cloud Service時的重要安全性考量事項。
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 678e81eb22cc1d7c239ac7a2594b39a3a60c51e2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 58%

---

# AEM as a Cloud Service 安全性注意事項 {#security-considerations}

## AEM Trust Store {#aem-trust-store}

為了支援非對稱式加密作業，AEM 將憑證儲存在內容存放庫的全域 trust-store 中。其內容是公開的，根據預設，發佈者執行個體上的所有人都可以匿名存取。

### Trust Store 的特色 {#truststore-characteristics}

* 信任存放區位於下方 `/etc/truststore` 和包含Java™金鑰庫檔案、金鑰庫密碼和存放庫中繼資料。 由於技術原因，即使預設透過API每個人都可存取包含的憑證，密碼和金鑰庫都經過加密
* 現成的憑證僅用於 HTTPS 和 SAML 支援，必須先手動建立存放區
* 客戶可以透過 [keystore API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-) 在自己的程式碼中使用它
* 可透過&#x200B;**工具** - **安全性** - **Trust Store**，或存取 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`* 來管理 trust-store，如下所示：

  ![Trust Store 管理](/help/security/assets/global-trust-store-modified.png)

* 根據使用案例，可以透過存放庫存取控制進一步限制對 trust-store 的存取權。

>[!NOTE]
>
>Adobe建議將預設存取控制項用於信任存放區，這表示它仍可公開存取。 對於最安全的設定，您可以使用拒絕原則 `jcr:all` 適用於所有人。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
