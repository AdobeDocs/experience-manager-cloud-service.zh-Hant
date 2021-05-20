---
title: Adobe Experience Manager的Cookie支援與Cloud Service相同
description: Adobe Experience Manager的Cookie支援與Cloud Service相同
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Adobe Experience Manager與Cloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}的相同網站Cookie支援

自80版、Chrome和更新版Safari推出Cookie安全性新模型。 此模式旨在透過名為`SameSite`的設定，對協力廠商網站Cookie的可用性引入安全控制。 如需詳細資訊，請參閱這篇[文章](https://web.dev/samesite-cookies-explained/)。

此設定的預設值(`SameSite=Lax`)可能會導致AEM執行個體或服務之間的驗證無法運作。 這是因為這些服務的網域或URL結構可能不受此Cookie原則的限制。

為了解決此問題，您需要為登入Token將SameSite Cookie屬性設為`None`。

您可以依照下列步驟來執行此操作：

1. 在本機安裝AEM SDK Quickstart版本
1. 前往`http://serveraddress:serverport/system/console/configMgr`的Web主控台
1. 搜尋並按一下&#x200B;**AdobeGranite代號驗證處理常式**
1. 將登入代號Cookie **的** SameSite屬性設為`None`，如下圖所示
   ![samesite](/help/security/assets/samesite1.png)
1. 按一下儲存
1. 依照使用AEM SDK Quickstart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)產生OSGi設定中概述的步驟，為此特定設定產生JSON格式設定[
1. 請依照[Cloud Manager API For Setting Properties](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi檔案中的步驟，套用設定。

更新此設定並重新登出使用者後，`login-token` Cookie即會設定`None`屬性，並納入跨網站請求中。
