---
title: 對Adobe Experience Manager網站的Cookie支援與Cloud Service相同
description: 對Adobe Experience Manager網站的Cookie支援與Cloud Service相同
translation-type: tm+mt
source-git-commit: 4f25aa54bd40644912e0e430a81f1a17d545e3f8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 與Cloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}相同的Adobe Experience Manager網站Cookie支援

自從第80版、Chrome和更新版Safari推出Cookie安全性的新模型。 此模式旨在透過名為`SameSite`的設定，對協力廠商網站的Cookie可用性引入安全性控制。 如需詳細資訊，請參閱此[文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值(`SameSite=Lax`)可能會導致例項或服務之AEM間的驗證無法運作。 這是因為這些服務的網域或URL結構可能不受此Cookie原則的限制。

為避免此問題，您必須將登入Token的SameSite Cookieattribe設定為`None`。

您可依照下列步驟執行：

1. 在本機安裝AEMSDK Quickstart版本
1. 轉至`http://serveraddress:serverport/system/console/configMgr`的Web控制台
1. 搜索並按一下&#x200B;**Adobe花崗岩令牌驗證處理程式**
1. 將login-token Cookie **的** SameSite屬性設為`None`，如下圖所示
   ![samesite](/help/security/assets/samesite1.png)
1. 按一下「儲存」
1. 請依照使用SDK快速入門(Quickstart)[「產生OSGi設定」中所述的步驟，產生此AEM特定設定的JSON格式設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. 按照[Cloud Manager API Format for Setting Properties](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi文檔中的步驟應用設定。

更新此設定後，使用者登出並再次登入，`login-token` Cookie就會設定`None`屬性，並包含在跨網站請求中。