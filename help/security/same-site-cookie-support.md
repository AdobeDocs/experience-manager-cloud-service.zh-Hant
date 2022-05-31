---
title: 同一站點Cookie支援Adobe Experience Manager as a Cloud Service
description: 同一站點Cookie支援Adobe Experience Manager as a Cloud Service
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: e1234e90e276a6274fc4dc9de0ae577219669ecf
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 同一站點Cookie支援Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

自80版、Chrome和更新版Safari以來，Cookie安全性引入了新型號。 此模式旨在通過名為 `SameSite`。 有關詳細資訊，請參閱 [文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值(`SameSite=Lax`)可能導致實例AEM或服務之間的身份驗證無效。 這是因為這些服務的域或URL結構可能不在此cookie策略的約束下。

為了繞過此問題，您需要將SameSite Cookie屬性設定為 `None` 的下界。

>[!CAUTION]
>
>的 `SameSite=None` 僅當協定安全(HTTPS)時才應用設定。
>
>如果協定不安全(HTTP)，則忽略該設定，伺服器將顯示以下WARN消息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以通過以下步驟添加設定：

1. 在本地安裝SDK快AEM速啟動版本
1. 轉到Web控制台，位於 `http://serveraddress:serverport/system/console/configMgr`
1. 搜索並按一下 **Adobe花崗岩令牌驗證處理程式**
1. 設定 **登錄令牌Cookie的SameSite屬性** 至 `None`，如下圖所示
   ![三元](/help/security/assets/samesite1.png)
1. 按一下「保存」
1. 按照中概述的步驟生成此特定設定的JSON格式配置 [使用SDK快速啟動生成AEMOSGi配置](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. 按照中的步驟應用設定 [用於設定屬性的Cloud Manager API格式](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi文檔。

更新此設定並重新註銷用戶後， `login-token` 曲奇餅 `None` 屬性集，並將包含在跨站點請求中。
