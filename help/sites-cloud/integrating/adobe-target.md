---
title: 整合 Adobe Target
description: 整合 Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 0af1f7dcc330a2ee5300088f274150a3ea79efe8
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Experience Cloud的一部分，[Adobe Target](https://business.adobe.com/products/target/adobe-target.html)可讓您透過所有管道的定位和測量，增加內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時對象區段（根據行為）並自動化內容鎖定目標和線上體驗。 AEM as a Cloud Service已採用Adobe Target Standard中使用的目標定位工作流程。 如果您使用Target，您可熟悉AEM as a Cloud Service中的目標定位編輯環境。

將AEM網站與Adobe Target整合，以便個人化頁面中的內容：

* 實作內容目標定位。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將內容資料提交至Target。
* 追蹤轉換率。

>[!NOTE]
>
>沒有現有Target帳戶的客戶可以要求存取Experience Cloud適用的Target Foundation Pack。 Foundation Pack提供磁碟區有限的Target使用。

若要與Target整合，請執行下列工作：

* [執行必要工作](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html)：向Adobe Target註冊並設定AEM作者執行個體的某些方面。 您的Adobe Target帳戶必須至少具有&#x200B;**核准者**&#x200B;層級許可權。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取。

* Adobe Launch是用於使用Target功能（JS資料庫）檢測AEM網站的實用工具。 因此，將AEM as a Cloud Service與Launch和Adobe Target整合是密切相關的（請參閱以下連結）。

   * [整合Adobe的Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
   * [透過AEM整合Adobe Adobe I/O Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
   * [瞭解AEM與Adobe、Analytics和Target Launch的整合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)

>[!NOTE]
>
>已在AEM as a Cloud Service中預先設定Adobe Launch的IMS設定（技術帳戶）。 使用者不需要建立此設定。

1. [設定活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)：將您的活動與Target雲端設定建立關聯。

>[!CAUTION]
>
>在AEM as a Cloud Service中，將優惠方案與活動從AEM同步至Adobe Target的復寫代理程式預設為停用。 如果您必須重新啟用復寫代理程式，請連絡[Adobe支援](https://experienceleague.adobe.com/?support-solution=General#support)團隊。

>[!NOTE]
>
>如果您使用Target搭配自訂Proxy設定，則必須同時設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他部分則使用4.x API：
>
>* 3.x已使用[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)設定
>* 4.x已使用[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)設定
>

>[!CAUTION]
>
>保護發佈執行個體上的活動設定節點&#x200B;**cq:ActivitySettings**，使其無法正常使用者存取。 活動設定節點應該只能由處理與Adobe Target的活動同步的服務存取。
>
>如需詳細資訊，請參閱[與Adobe Target整合的必要條件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node)。

整合完成後，您可以[編寫目標內容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html)，將訪客資料傳送至Adobe Target。 頁面元件需要特定程式碼才能啟用內容目標定位。 (請參閱[針對目標內容開發](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>當您在AEM製作中鎖定元件時，元件會對Adobe Target發出一系列伺服器端呼叫，以註冊行銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈對Adobe Target發出伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEM as a Cloud Service與Adobe Target整合需要Adobe Target、AEM活動管理和AEM受眾管理的知識。 您應熟悉下列資訊：

* Adobe Target (請參閱[Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* AEM活動主控台（請參閱[管理活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)）。
* AEM對象（請參閱[管理對象](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html)）。

>[!NOTE]
>
>使用Adobe Target時，以下是行銷活動中允許的成品數目上限：
>
>* 50個位置
>* 2,000個體驗
>* 50個量度
>* 50個報表區段
