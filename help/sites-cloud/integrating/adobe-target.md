---
title: 整合 Adobe Target
description: 整合 Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: e6fc31a5c4b3bb62f7d6e639eae7e1f222b2f5ed
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 2%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分， [Adobe Target](https://www.adobe.com/solutions/testing-targeting/testandtarget.html) 可讓您透過鎖定目標和測量所有管道，來提升內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時受眾區段（根據行為），以及自動鎖定內容和線上體驗。 AEM as a Cloud Service已採用Adobe Target Standard中使用的鎖定工作流程。 如果您使用Target，您將熟悉AEM as a Cloud Service中的目標編輯環境。

將您的AEM網站與Adobe Target整合，以個人化您頁面中的內容：

* 實作內容鎖定目標。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將內容資料提交至Target。
* 追蹤轉換率。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客戶若沒有現有的Target帳戶，可以要求存取Target Foundation Pack以進行Experience Cloud。  Foundation Pack提供對Target的卷有限使用。


若要與Target整合，請執行下列工作：

* [執行先決條件任務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html):向Adobe Target註冊，並設定AEM製作例項的某些方面。 您的Adobe Target帳戶必須 **核准者** 至少級別權限。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取該設定。

* Launch by Adobe是實際上用來檢測具有Target功能（JS資料庫）的AEM網站的工具。 因此，將AEMas a Cloud Service與Launch和Adobe Target整合可同時進行（請參閱下列連結）。

   * [與Adobe Target整合，使用Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims-adobe-io.html)
   * [整合Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [透過AEM將Adobe I/O與AdobeLaunch整合](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [了解AEM與Launch by Adobe、Analytics和Target的整合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)

>[!NOTE]
>
>Launch by Adobe的IMS設定（技術帳戶）已在AEMas a Cloud Service中預先設定。 使用者不需要建立此設定。

1. [設定活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html):將活動與Target雲端設定建立關聯。

>[!CAUTION]
>
>在AEMas a Cloud Service中，將選件和活動從AEM同步至Adobe Target的復寫代理預設為停用。 請聯繫 [Adobe支援](https://experienceleague.adobe.com/?support-solution=General#support) 團隊（如果需要重新啟用復寫代理）。

>[!NOTE]
>
>如果您使用Target搭配自訂的代理設定，您需要設定兩個HTTP用戶端代理設定，因為AEM的某些功能使用3.x API，而其他一些則使用4.x API:
>
>* 3.x的設定 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x的設定 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>您必須保護活動設定節點的安全 **cq:ActivitySettings** 發佈例項，使一般使用者無法存取。 處理活動同步至Adobe Target的服務只應能存取活動設定節點。
>
>請參閱 [與Adobe Target整合的必要條件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) 以取得詳細資訊。

整合完成時，您可以 [作者目標內容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) 會將訪客資料傳送至Adobe Target。 請注意，頁面元件需要特定的程式碼才能啟用內容鎖定目標。 (請參閱 [針對目標內容開發](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會向Adobe Target發出一系列伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈至Adobe Target進行伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEMas a Cloud Service與Adobe Target整合需要Adobe Target、AEM活動管理和AEM對象管理的相關知識。 您應熟悉下列資訊：

* Adobe Target(請參閱 [Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* AEM活動主控台(請參閱 [管理活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html))。
* AEM對象(請參閱 [管理對象](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html))。

>[!NOTE]
>
>使用Adobe Target時，以下是促銷活動中允許的成品數量上限：
>
>* 50個地點
>* 2,000個體驗
>* 50個量度
>* 50個報告區段

