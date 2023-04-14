---
title: AEMas a Cloud Service安全性考量事項
description: 了解使用AEM時的重要安全性考量事項as a Cloud Service
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# AEMas a Cloud Service安全性考量事項 {#security-considerations}

## AEM信任存放區 {#aem-trust-store}

為了支援非對稱的加密操作，AEM將憑證儲存在內容存放庫內的全域信任存放區中。 其內容為公開，依預設，發佈者執行個體上的每個人都可匿名存取。

### 信任儲存的特性 {#truststore-characteristics}

* 信任存放區位於下方 `/etc/truststore` 和包含Java金鑰存放區檔案、金鑰存放區密碼和存放庫中繼資料。 請注意，密碼和金鑰存放區本身都因技術原因而加密，即使包含的憑證預設可透過API供所有人存取
* 憑證會立即用於HTTPS和SAML支援，且必須先手動建立存放區
* 客戶可透過 [金鑰存放區API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* 信任存放區可透過UI進行管理，位於 **工具** - **安全性** - **信任儲存** 或 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*，如下所示：

   ![信任儲存管理](/help/security/assets/global-trust-store-modified.png)

* 根據使用案例，存放庫存取控制可進一步限制對信任存放區的存取。

>[!NOTE]
>
>Adobe建議對信任儲存區使用預設訪問控制，這表示它仍可以公開訪問。 為了獲得最安全的配置，可以對每個人使用deny jcr:all策略。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
