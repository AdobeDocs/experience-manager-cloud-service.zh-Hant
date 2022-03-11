---
title: 整合 Adobe Target
description: 整合 Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 65e1ede4cdc8035657e8b37fe206ebed4ab7bb24
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分， [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) 允許您通過針對所有渠道進行定位和測量來提高內容相關性。 Adobe Target被營銷人員用於設計和執行線上test、建立即時（基於行為）受眾群，以及自動確定內容和線上體驗的目標。 AEMas a Cloud Service採用了Adobe Target標準的目標工作流程。 如果使用「目標」，您將熟悉as a Cloud Service中的目標編輯環AEM境。

將您的站AEM點與Adobe Target整合，以個性化頁面中的內容：

* 實施內容目標。
* 使用目標受眾建立個性化體驗。
* 訪問者與您的頁面交互時，將上下文資料提交到目標。
* 跟蹤轉換率。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客戶如果沒有現有目標帳戶，可以請求訪問Target Foundation Pack以進行Experience Cloud。  Foundation Pack提供了對目標的卷限制使用。


要與目標整合，請執行以下任務：

* [執行必備任務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html):向Adobe Target註冊並配置作者實例的AEM某些方面。 你的Adobe Target帳戶 **批准者** 至少級別權限。 此外，必須保護發佈節點上的活動設定，以便用戶無法訪問該活動設定。

* Launch by Adobe是實際工具，用於檢AEM測具有目標功能（JS庫）的站點。 因此，AEM將as a Cloud Service與Launch和Adobe Target結合起來是一回事（請參見以下連結）。

   * [使用Adobe I/O與Adobe Target整合](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [整合Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [通過AEMAdobe I/O與Adobe發佈整合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [了AEM解與Launch by Adobe、分析和目標的整合](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>用於Launch by Adobe的IMS配置（技術帳戶）在as a Cloud Service中預配置AEM。 用戶不必建立此配置。

1. [配置活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html):將活動與目標雲配置關聯。

>[!CAUTION]
>
>在AEMas a Cloud Service中，預設禁用將優惠和活動AEM從Adobe Target同步的複製代理。 請聯繫 [Adobe支援](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) 組。

>[!NOTE]
>
>如果將目標與自定義代理配置一起使用，則需要配置兩個HTTP客戶端代理配置AEM，因為其中的某些功能使用3.x API，而其他功能則使用4.x API:
>
>* 3.x配置 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>必須保護活動設定節點的安全 **cq：活動設定** 在發佈實例上，以便普通用戶無法訪問。 活動設定節點只能由處理與Adobe Target的活動同步的服務訪問。
>
>請參閱 [與Adobe Target整合的先決條件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) 的上界。

整合完成後，您可以 [作者目標內容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) 把訪問者資料發送到Adobe Target。 請注意，頁面元件需要特定代碼才能啟用內容目標。 (請參閱 [為目標內容開發](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>當您針對作者中的元件AEM時，該元件會向Adobe Target發出一系列伺服器端呼叫，以註冊市場活動、設定優惠和檢索Adobe Target段（如果已配置）。 發佈到Adobe Target時不會進行AEM伺服器端呼叫。

## 背景資訊源 {#background-information-sources}

將AEMas a Cloud Service與Adobe Target整合需要瞭解Adobe Target、AEM活動管理和AEM受眾管理。 您應熟悉以下資訊：

* Adobe Target(請參閱 [Adobe Target文檔](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* 活AEM動控制台(請參閱 [管理活動](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)。
* 觀AEM眾(請參閱 [管理受眾](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe Target時，以下是市場活動中允許的最大工件數：
>
>* 50個地點
>* 2,000次經驗
>* 50個指標
>* 50個報告分部

