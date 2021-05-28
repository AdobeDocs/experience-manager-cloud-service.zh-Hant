---
title: '整合 Adobe Analytics '
description: '整合 Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

將Adobe Analytics和AEM整合為Cloud Service，即可追蹤網頁活動：

* Adobe Analytics設定可讓AEM使用Adobe Analytics驗證。
* 架構可識別傳送至Adobe Analytics報表套裝的資料。

資料包括頁面和使用者資料，例如：

* AEM元件收集的資料
* 連結點按
* 視訊使用資訊
* 來自Adobe Analytics的頁面瀏覽次數

下列頁面可協助您設定整合。 請注意，Launch by Adobe是實際上用來檢測具有Analytics功能（JS資料庫）的AEM網站的工具。 因此，將AEM as aCloud Service與Launch和Adobe Analytics整合可同時進行。

* [連線Adobe Analytics和建立架構](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html)  — 請注意，「Analytics架構」是AEM的舊版，而且在AEM中無法以Cloud Service形式建立，因為需要傳統UI。請改為使用Launch by Adobe，同時用於變數對應和將JS程式庫部署至頁面。
* [整合Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [透過AEM將Adobe I/O與AdobeLaunch整合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [了解AEM與Launch by Adobe、Analytics和Target的整合](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [設定Adobe Analytics的連結追蹤](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [將元件資料與Adobe Analytics屬性對應](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [設定Adobe Analytics的視訊追蹤](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分類](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager作為沒有現有Analytics帳戶的Cloud Service客戶，可以要求存取Analytics Foundation Pack以進行Experience Cloud。  此Foundation Pack提供Analytics的有限量使用。

>[!NOTE]
>
>Launch by Adobe的IMS設定（技術帳戶）已在AEM中預先設定為Cloud Service。 使用者不需要建立此設定。

## 更多資訊 {#further-information}

請參閱：

* [擴充Adobe Analytics整](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) 合，以取得開發可收集使用者資料的元件和自訂Adobe Analytics架構的相關資訊。請注意，AEM中的「Analytics架構」是舊有的，且其建立作業無法用於AEM，因為它需要傳統UI。 請改為使用Launch by Adobe，同時用於變數對應和將JS程式庫部署至頁面。
* 知識庫文章[Adobe Analytics整合 — 疑難排解問題](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以取得疑難排解Adobe Analytics整合的相關資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定：
>
>* **Day Commons HTTP Client 3.1** 以設定3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP元件Proxy** 設定以設定4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>


