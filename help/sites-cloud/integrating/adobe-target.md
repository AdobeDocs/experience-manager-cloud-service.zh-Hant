---
title: 整合 Adobe Target
description: '整合 Adobe Target '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---


# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分， [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) 可讓您透過跨所有通道的鎖定和測量來提升內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時受眾細分（根據行為）並自動鎖定內容和線上體驗。 AEM作為雲端服務已採用Adobe Target Standard中使用的定位工作流程。 如果您使用Target，您將熟悉AEM中的定位編輯環境，即雲端服務。

將您的AEM網站與Adobe Target整合，以個人化頁面內容：

* 實作內容定位。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將上下文資料提交至Target。
* 追蹤轉換率。

>[!NOTE]
>
>Adobe Experience Manager是Cloud Service客戶，如果客戶目前沒有Target帳戶，可以要求存取Target Foundation Pack for Experience Cloud。  Foundation Pack提供對Target的卷有限使用。


若要與Target整合，請執行下列工作：

* [執行先決條件任務](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html): 向Adobe Target註冊，並設定AEM作者例項的某些方面。 您的Adobe Target帳戶至少必 **須擁有** 核准者層級權限。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取。

* Launch by Adobe是實際工具，可讓您使用Target功能（JS資料庫）來檢測AEM網站。 因此，將AEM整合為Cloud Service與Launch和Adobe Target可攜手進行（請參閱以下連結）。

   * [使用Adobe I/O與Adobe Target整合](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [整合Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [透過Adobe I/O將AEM與Adobe Launch整合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [瞭解AEM與Launch By Adobe、Analytics和Target的整合](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>Launch by Adobe的IMS設定（技術帳戶）已在AEM中預先設定為雲端服務。 使用者不必建立此設定。

1. [設定活動](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): 將您的活動與Target雲端設定關聯。

>[!CAUTION]
>
>在AEM中，將選件和活動從AEM同步至Adobe Target的複製代理預設會停用。 如果您需 [要重新啟用複製代理](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) ，請與Adobe支援團隊聯絡。

>[!NOTE]
>
>如果您將Target與自訂的Proxy設定搭配使用，則需要設定兩個HTTP Client Proxy設定，因為AEM的某些功能是使用3.x API，而其他部分則使用4.x API:
>
>* 3.x已設定為 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已設定為 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>您必須保護發佈例項上的活動設 **定節點cq:ActivitySettings** ，如此一般使用者便無法存取它。 處理Adobe Target活動同步的服務只能訪問活動設定節點。
>
>如需詳 [細資訊，請參閱與Adobe Target整合的必要條件](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) 。

整合完成後，您可以製作將 [訪客資料傳送](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) 至Adobe Target的目標內容。 請注意，頁面元件需要特定的程式碼才能啟用內容定位。 (請參 [閱開發目標內容](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會對Adobe Target進行一連串的伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 AEM發佈至Adobe Target時，不會進行伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEM整合為雲端服務與Adobe Target需要有Adobe Target、AEM活動管理和AEM觀眾管理的相關知識。 您應熟悉下列資訊：

* Adobe Target(請參閱 [Adobe Target檔案](https://docs.adobe.com/content/help/en/target/using/target-home.html))。
* AEM活動主控台(請參 [閱管理活動](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)。
* AEM觀眾(請參閱「管 [理觀眾」](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe Target時，下列是促銷活動中允許的最大對象數：
>
>* 50個地點
>* 2,000次體驗
>* 50個量度
>* 50個報告分部

>


