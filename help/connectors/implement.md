---
title: 實作 AEM 連接器
description: 實作 AEM 連接器
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---

實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，可以通過AEM以下方式獲得開發人員許可證： [AdobeExchange計畫](https://partners.adobe.com/exchangeprogram/experiencecloud)。

常見整合模式
---------------------------

是AEM一種尖端的Web體驗管理解決方案，提供了許多潛在的整合領域。 常見整合模式包括：

* 將資料從外部系統拉入AEM。 例如，從CRM導出聯繫資訊，以便訪問受電網站的更AEM多受眾可用。  實施應使用Sling [計畫作業](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，這保證即使容器關閉也執行作業。 代碼應設計為假定作業可能被多次觸發。
* 將資料從AEM導出到外部系統。 例如，新聞稿訂閱設定已在AEM支援的網站上提交到CRM。
* 正在從中檢索AEM資產。 例如，外部內容管理系統(CMS)引用儲存在AEM Assets的資產。 或者，作為另一個例子，PIM系統連結到AEM Assets的影像。
* 在基礎架構中存AEM儲資產。 例如，在AEM Assets儲存批准資產的市場營銷資源管理(MRM)系統。
* 配置和呈現自定義UI元件。 例如，允許作者拖放視頻元件並配置特定視頻以在即時站點上播放。
* 使用合作夥伴服務處理資產。 例如，在發佈頁面時將資產發送到視頻平台。
* 在管理控制台中分析站點、頁面AEM或資產。 例如，為現有或未發佈頁面提供SEO建議。
* 對由外部服務維護的用戶資料的頁面級訪問。 例如，利用人口資訊來個性化站點體驗。 閱讀有關ContextHub的內容，ContextHub是用於儲存、操作和呈現上下文資料的框架。
* 正在轉換站點副本或資產元資料。 查看 [翻譯AEM框架Bootstrap連接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) 使用翻譯框AEM架的示例代碼，這是翻譯連接器的首選實現。


有用文檔
--------------------

Experience Manageras a Cloud Service [文檔](../overview/introduction.md) 為開發提供了有價值的AEM見解。 以下是一些在實施連接器時可能有用的特定技術主題和AEM參考：

* Adobe咨詢服務(ACS) [示AEM例](http://adobe-consulting-services.github.io/acs-aem-samples/) 為開發人員提供有條理AEM的代碼
* 本文「通用整合模式」部分中的各種文檔連結

社區資源
--------------------

除了上面的靜態文檔之外，Adobe和社AEM區還提供資源幫助將連接器推向市場：

* Adobe社區 [論AEM壇](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是您的同齡人提問和回答問題的活動站點
* 某些合作夥伴級別可提供其他Adobe技術資源。 瞭解有關 [AdobeExchange計畫](https://partners.adobe.com/exchangeprogram/experiencecloud)。
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](http://www.adobe.com/tw/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

包結構規則
-----------------------

為了支援滾動部署，AEMas a Cloud Service的包（例如連接器）在&quot;不可變&quot;和&quot;可變&quot;內容之間有嚴格的分隔。 應將包與包(包括：

* `/apps`
* `/content`與`/conf`

連接器應遵守這些封裝指南，如中所述 [這篇文章](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 現有連接器也應進行重構以符合要求。

此外，只有Adobe才應將代碼寫入 `/libs`與客戶和合作夥伴一起 `/apps`。

可能還需要對現有連接器進行重構以移動可能已放置過的任何配置 `/etc` 到其他頂級資料夾，如 `/conf`。 此重組作為6.5AEM的一部分進行，詳見 [AEM 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)。

建議將大多數連接器代碼置於 `/apps/connectors/<vendor>` 為具有多個連接器的客戶推廣乾淨的儲存庫結構。

Cloud Services配置
-----------------------------

連接器實現的一個方面是支援連接器配置的代碼。 此代碼使具有連接器名稱的卡顯示在「工具」>「操作」>「Cloud Services」下。 按一下時， [配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 彈出，其中客戶選擇要包含連接器配置的父資料夾。 連接器的代碼應生成包含必須配置的所有屬性的表單，最終將這些值儲存在配置資料夾中 `/conf`。 以後可以在「站點」屬性頁籤或「資產」屬性頁籤下選擇此資料夾。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允許跨不同資料夾分層配置，包括 `/libs`。 `/apps`。 `/conf` 子資料夾 `/conf`。 它支援繼承，這樣客戶就可以配置全局配置，同時對每個微站點進行特定更改。 由於可以將此功能用於Cloud Services配置，因此連接器代碼應使用上下文感知配置API引用配置，而不是引用特定配置節點。

如果連接器中使用了修改的配置，請設計連接器以處理包括/合併連接器提供的預設配置的任何將來更新以及任何客戶配置。 請記住，在未經客戶警告和同意的情況下更改自定義（如客戶更改）內容或配置可能會中斷（或建立意外行為）其連接器。

編碼最佳做法
----------------------

由AEM於as a Cloud Service是雲本機解決方案，因此有一些准則可能會影響連接器的代碼策略。 請參閱 [AEMas a Cloud Service發展指南](/help/implementing/developing/introduction/development-guidelines.md) 的子菜單。

測試連AEM接器
-------------------------

應使用本地環境開發技術建立新連接器（或修改現有連接器）。 合作夥伴團隊將為ISV合作夥伴提供沙盒環境，在該環境中，他們可以將AEMConnector部署到香草應用程式，以確保其工作正常。
