---
title: 整合 Adobe Target
description: 整合 Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: f40a2db6616aeaaf13f8ae19ab429a7301e6c05a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 2%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

身為Adobe Marketing Cloud的一部分， [Adobe Target](https://www.adobe.com/solutions/testing-targeting/testandtarget.html) 可讓您透過所有管道的目標定位和測量，提高內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時受眾區段（根據行為）以及自動化內容和線上體驗的鎖定目標。 AEMas a Cloud Service已採用Adobe Target Standard中使用的目標定位工作流程。 如果您使用Target，您將熟悉AEMas a Cloud Service中的目標定位編輯環境。

將AEM網站與Adobe Target整合，以個人化頁面中的內容：

* 實作內容目標定位。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將內容資料提交至Target。
* 追蹤轉換率。

>[!NOTE]
>
>沒有現有Target帳戶的Adobe Experience Manager as a Cloud Service客戶可以要求存取Target Foundation Pack以進行Experience Cloud。  Foundation Pack提供磁碟區有限的Target使用。


若要與Target整合，請執行下列工作：

* [執行先決條件任務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html)：向Adobe Target註冊並設定AEM編寫執行個體的某些方面。 您的Adobe Target帳戶必須具有 **核准者** 至少需要層級許可權。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取。

* Launch by Adobe是用於使用Target功能（JS資料庫）檢測AEM網站的實體工具。 因此，將AEMas a Cloud Service與Launch和Adobe Target整合是密切相關的（請參閱以下連結）。

   * [使用Adobe I/O與Adobe Target整合](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims-adobe-io.html)
   * [整合Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [透過Adobe I/O整合AEM與AdobeLaunch](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [瞭解AEM與Launch by Adobe、Analytics和Target的整合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)

>[!NOTE]
>
>Launch by Adobe的IMS設定（技術帳戶）已在AEMas a Cloud Service中預先設定。 使用者不必建立此設定。

1. [設定活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)：將您的活動與Target雲端設定建立關聯。

>[!CAUTION]
>
>在AEMas a Cloud Service中，將選件和活動從AEM同步至Adobe Target的復寫代理預設為停用。 請聯絡 [Adobe支援](https://experienceleague.adobe.com/?support-solution=General#support) 群組（如果您需要重新啟用復寫代理）。

>[!NOTE]
>
>如果您使用具有自訂Proxy設定的Target，則需要設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他功能則使用4.x API：
>
>* 3.x已設定為 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已設定為 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>您必須保護活動設定節點 **cq：ActivitySettings** ，讓一般使用者無法存取。 活動設定節點應該只能由處理活動同步至Adobe Target的服務存取。
>
>另請參閱 [與Adobe Target整合的必要條件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) 詳細資訊。

整合完成後，您可以 [作者目標內容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) 將訪客資料傳送至Adobe Target的功能。 請注意，頁面元件需要特定程式碼才能啟用內容目標定位。 (請參閱 [針對目標內容開發](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>當您在AEM作者中鎖定元件時，該元件會對Adobe Target發出一系列伺服器端呼叫，以註冊行銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈對Adobe Target發出伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEMas a Cloud Service與Adobe Target整合需要Adobe Target、AEM活動管理和AEM受眾管理的知識。 您應熟悉下列資訊：

* Adobe Target (請參閱 [Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* AEM活動主控台(請參閱 [管理活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html))。
* AEM對象(請參閱 [管理對象](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html))。

>[!NOTE]
>
>使用Adobe Target時，以下是行銷活動中允許的成品數目上限：
>
>* 50個位置
>* 2,000個體驗
>* 50個量度
>* 50個報表區段

