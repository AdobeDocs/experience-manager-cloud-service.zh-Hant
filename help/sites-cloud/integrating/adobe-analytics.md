---
title: 整合 Adobe Analytics
description: '整合 Adobe Analytics '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 13%

---


# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

將Adobe Analytics和AEM整合為雲端服務，可讓您追蹤網頁活動：

* Adobe Analytics設定可讓AEM向Adobe Analytics驗證。
* 架構可識別傳送至Adobe Analytics報表套裝的資料。

資料包括頁面和使用者資料，例如：

* AEM元件收集的資料
* 連結點按
* 視訊使用資訊
* 來自Adobe Analytics的頁面瀏覽次數

下列頁面可協助您設定整合。 請注意，Launch by Adobe實際上是利用Analytics功能（JS資料庫）來檢測AEM網站的工具。 因此，將AEM整合為雲端服務與Launch和Adobe Analytics，將會攜手合作。

* [連線至Adobe Analytics和建立架構](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) -請注意，「Analytics架構」是AEM的舊版，其建立作業在AEM中無法運作，因為它需要Classic UI。 Launch by Adobe應改為用於變數對應和將JS程式庫部署至頁面。
* [整合Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [透過Adobe I/O將AEM與Adobe Launch整合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [瞭解AEM與Launch By Adobe、Analytics和Target的整合](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [設定Adobe Analytics的連結追蹤](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [使用Adobe Analytics屬性對應元件資料](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [設定Adobe Analytics的視訊追蹤](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分類](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager是Cloud Service客戶，如果客戶沒有現有的Analytics帳戶，可以要求存取Analytics Foundation Pack for Experience Cloud。  此Foundation Pack提供Analytics的使用量有限。

>[!NOTE]
>
>Launch by Adobe的IMS設定（技術帳戶）已在AEM中預先設定為雲端服務。 使用者不必建立此設定。

## 更多資訊 {#further-information}

請參閱：

* [擴充Adobe Analytics整合](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) ，以取得開發收集使用者資料的元件和自訂Adobe Analytics架構的相關資訊。 請注意，「Analytics架構」是AEM的舊版，而且其建立在AEM中無法當做雲端服務運作，因為它需要Classic UI。 Launch by Adobe應改為用於變數對應和將JS程式庫部署至頁面。
* 知識庫文章「 [Adobe Analytics整合——疑難排解問題](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)」，以取得有關疑難排解Adobe Analytics整合的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定：
>
>* **Day Commons HTTP Client 3.1** ，用以設定3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components Proxy Configuration** to configure the 4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


