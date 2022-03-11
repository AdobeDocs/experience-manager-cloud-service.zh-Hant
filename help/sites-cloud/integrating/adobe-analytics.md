---
title: '整合 Adobe Analytics '
description: '整合 Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe AnalyticsAEM和as a Cloud Service允許您跟蹤網頁活動：

* Adobe Analytics配置可AEM以向Adobe Analytics驗證。
* 框架標識發送到您的Adobe Analytics報告套件的資料。

資料包括頁面和用戶資料，例如：

* 元件收AEM集的資料
* 連結按一下
* 視頻使用資訊
* Adobe Analytics的頁面訪問次數

下面列出的頁面可幫助您配置整合。 需要注意的是，Launch by Adobe是使用分析功能（JS庫）AEM檢測站點的實際工具。 因此，AEM將as a Cloud Service與元徵和Adobe Analytics聯合起來。

* [連接到Adobe Analytics並建立框架](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html)  — 請注意，「分析框架」在中是舊版本AEM，其建立在as a Cloud Service中不起作用，因AEM為它需要經典UI。 應將Launch by Adobe用於變數映射和將JS庫部署到頁面。
* [整合Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [通過AEMAdobe I/O與Adobe發佈整合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [了AEM解與Launch by Adobe、分析和目標的整合](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [為Adobe Analytics配置鏈路跟蹤](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [使用Adobe Analytics屬性映射元件資料](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [為Adobe Analytics配置視頻跟蹤](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分類](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager as a Cloud Service客戶如果沒有現有的Analytics帳戶，可以請求訪問Analytics Foundation Pack以進行Experience Cloud。  此Foundation Pack提供了分析的有限量使用。

>[!NOTE]
>
>用於Launch by Adobe的IMS配置（技術帳戶）在as a Cloud Service中預配置AEM。 用戶不必建立此配置。

## 更多資訊 {#further-information}

請參閱：

* [擴大Adobe Analytics一體化](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) 有關開發收集用戶資料和自定義Adobe Analytics框架的元件的資訊。 請注意，「分析框架」在中是舊版本AEM，其建立在as a Cloud Service中不起作用，因AEM為它需要經典UI。 應將Launch by Adobe用於變數映射和將JS庫部署到頁面。
* 知識庫文章， [Adobe Analytics整合 — 故障排除](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以獲取有關診斷您的Adobe Analytics整合的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定：
>
>* **Day Commons HTTP Client 3.1** 配置3.x API;
   >  比如說， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP元件代理配置** 配置4.x API;
   >  比如說， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

