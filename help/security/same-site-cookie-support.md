---
title: Adobe Experience Manager as a Cloud Service 的同網站 Cookie 支援
description: Adobe Experience Manager as a Cloud Service 的同網站 Cookie 支援
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: e1234e90e276a6274fc4dc9de0ae577219669ecf
workflow-type: ht
source-wordcount: '287'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 的同網站 Cookie 支援 {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

從 80 版本開始，Chrome 和之後的 Safari 引入了一種新的 cookie 安全性模型。 此模式旨在透過稱為 `SameSite` 的設定在第三方網站的 Cookie 可用性方面引入安全性控制項。如需詳細資訊，請參閱本[文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值 (`SameSite=Lax`) 可能會導致 AEM 執行個體或服務之間的驗證無法運作。這是因為這些服務的網域或 URL 結構可能不受此 cookie 原則的約束。

為了解決這個問題，您需要針對登入權杖將 SameSite cookie 屬性設為 `None`。

>[!CAUTION]
>
>`SameSite=None` 設定僅在通訊協定安全 (HTTPS) 時套用。
>
>如果通訊協定不安全 (HTTP)，則將忽略該設定並且伺服器將顯示此警告訊息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以依照下列步驟新增設定：

1. 在本機安裝 AEM SDK 快速入門版本
1. 前往 Web 主控台，位於 `http://serveraddress:serverport/system/console/configMgr`
1. 搜尋並按一下 **Adobe Granite 權杖驗證處理常式**
1. 將&#x200B;**登入權杖 cookie 的 SameSite 屬性**&#x200B;設定為 `None`，如下圖所示
   ![samesite](/help/security/assets/samesite1.png)
1. 按一下「儲存」
1. 按照[使用 AEM SDK 快速入門產生 OSGi 設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)中概述的步驟為此特定設定產生 JSON 格式設定
1. 按照[用於設定屬性的 Cloud Manager API 格式](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi 文件中步驟來套用設定。

此設定一更新且使用者登出並再次登入後，`login-token` cookie 就會有 `None` 屬性集，並將包含在跨網站請求中。
