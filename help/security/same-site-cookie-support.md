---
title: Adobe Experience Manager as a Cloud Service的相同網站Cookie支援
description: Adobe Experience Manager as a Cloud Service的相同網站Cookie支援
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: e1234e90e276a6274fc4dc9de0ae577219669ecf
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service的相同網站Cookie支援 {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

自80版、Chrome和更新版Safari推出Cookie安全性新模型。 此模式的設計目的，是透過以下的設定，對協力廠商網站的Cookie可用性引入安全控制： `SameSite`. 如需詳細資訊，請參閱 [文章](https://web.dev/samesite-cookies-explained/).

此設定的預設值(`SameSite=Lax`)可能會導致AEM例項或服務之間的驗證無法運作。 這是因為這些服務的網域或URL結構可能不受此Cookie原則的限制。

若要解決此問題，您必須將SameSite Cookie屬性設為 `None` 登入Token。

>[!CAUTION]
>
>此 `SameSite=None` 只有在通訊協定安全(HTTPS)時，才會套用設定。
>
>如果通訊協定不安全(HTTP)，則會忽略設定，而伺服器會顯示此WARN訊息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以依照下列步驟來新增設定：

1. 在本機安裝AEM SDK Quickstart版本
1. 前往Web主控台： `http://serveraddress:serverport/system/console/configMgr`
1. 搜尋並按一下 **AdobeGranite代號驗證處理常式**
1. 設定 **登入代號Cookie的SameSite屬性** to `None`，如下圖所示
   ![samesite](/help/security/assets/samesite1.png)
1. 按一下儲存
1. 依照 [使用AEM SDK快速入門產生OSGi設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. 請依照 [用於設定屬性的Cloud Manager API格式](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi檔案。

更新此設定並將使用者登出並重新登入後， `login-token` cookie會 `None` 屬性集和將包含在跨網站請求中。
