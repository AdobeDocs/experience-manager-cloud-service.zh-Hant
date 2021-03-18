---
title: 實作 AEM 連接器
description: 實作 AEM 連接器
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，您可AEM以透過[Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud)取得開發人員授權。

通用整合模式
---------------------------

是AEM一款尖端的網路體驗管理解決方案，並提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統將資料拉入AEM。 例如，從CRM匯出聯絡資訊，以便讓造訪網站的更廣AEM大觀眾使用。  實作應使用Sling的[Scheduled Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，這可保證即使容器關閉，也會執行工作。 程式碼應設計為假設工作可能會觸發多次。
* 將資料從AEM導出到外部系統。 例如，電子報訂閱設定是在支援的網AEM站上提交至CRM。
* 從擷取資AEM產。 例如，外部內容管理系統(CMS)會參照儲存在AEM Assets的資產。 或者，另一個例子是PIM系統，它連結到AEM Assets的影像。
* 將資產儲存在基礎AEM架構中。 例如，行銷資源管理(MRM)系統將已核准的資產儲存在AEM Assets。
* 設定和轉譯自訂UI元件。 例如，允許作者拖放視訊元件，並設定特定視訊以在即時網站上播放。
* 使用合作夥伴服務處理資產。 例如，在發佈頁面時，將資產傳送至視訊平台。
* 在管理控制台中分析網站、頁面AEM或資產。 例如，為現有或未發佈的頁面建立SEO建議。
* 頁面層級存取外部服務維護的使用者資料。 例如，運用人口統計資訊來個人化網站體驗。 閱讀ContextHub的相關資訊，此架構可用來儲存、控制和呈現內容資料。
* 轉換網站復本或資產中繼資料。 有關使用翻譯框架的示例代碼，請參見[AEM翻譯框架Bootstrap連接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector)AEM，該框架是翻譯連接器的首選實現。


有用的檔案
--------------------

Experience Manager作為Cloud Service[文檔](../overview/introduction.md)提供了有關開發的寶貴見解AEM。 以下是一些在實施連接器時可能會發現有用的特定技術主題和AEM參考：

* Adobe咨詢服務(ACS)[AEM Samples](http://adobe-consulting-services.github.io/acs-aem-samples/)，以取得注釋良好的程式碼，以協助開發AEM人員
* 本文「常用整合模式」一節中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案外，Adobe和社AEM群也提供資源，協助將連接器推向市場：

* Adobe社群的[AEM論壇](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html)是您的同儕提出問題並回覆的有效網站
* 特定Adobe層級提供額外的合作夥伴技術資源。 進一步瞭解[Adobe交換程式](https://partners.adobe.com/exchangeprogram/experiencecloud)。
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](http://www.adobe.com/tw/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

封裝結構規則
-----------------------

為了支援滾動部署，作AEM為一個Cloud Service包，其中連接器是示例，&quot;不可變&quot;和&quot;可變&quot;內容之間有嚴格的分隔。 應將包清晰地分開，這些包包括：

* `/apps`
* `/content`與`/conf`

連接器應遵守[本文](/help/implementing/developing/introduction/aem-project-content-package-structure.md)所述的這些包裝准則。 現有連接器也應重新構圖，以符合規定。

此外，只有Adobe才應將代碼寫入`/libs`，客戶和合作夥伴應將代碼寫入`/apps`。

還需要重構現有連接器，以便將任何可能已放置`/etc`的配置移入其他頂級資料夾，如`/conf`。 此重組作為6.5的一部分AEM完成，並在[AEM 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中介紹。

建議將大部分連接器代碼放在`/apps/connectors/<vendor>`下，以便為具有多個連接器的客戶提供乾淨的儲存庫結構。

Cloud Services配置
-----------------------------

連接器實現的一個方面是支援連接器配置的代碼。 此程式碼會在「工具>作業>Cloud Services」下方顯示連接器名稱的卡片。 按一下後，[配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)將彈出，客戶在其中選擇要包含連接器配置的父資料夾。 連接器的代碼應該生成具有必須配置的所有屬性的表單，最終將值儲存在`/conf`下的配置資料夾中。 此資料夾稍後可在「網站屬性」標籤或「資產屬性」標籤下選取。


上下文感知配置
-----------------------------

[內容感知](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 設定可跨不同資料夾(包括下方的子資料夾 `/libs`、 `/apps`和子資 `/conf` 料夾)進行圖層設定 `/conf`。它支援繼承，以便客戶可以配置全局配置，同時對每個微站點進行特定更改。 由於此功能可用於Cloud Services配置，因此連接器代碼應使用上下文感知配置API來參考配置，而不是引用特定配置節點。

如果連接器中使用了修改的配置，請構建連接器以處理將來對任何客戶配置提供的預設配置進行包括／合併任何更新的連接器。 請記住，在未經客戶警告及同意的情況下變更自訂（如客戶所變更）內容或設定，可能會中斷（或造成非預期行為）其Connector。

編碼最佳實務
----------------------

由AEM於Cloud Service是雲端原生解決方案，因此有一些准則可能會影響連接器的程式碼策略。 如需詳細資訊，請參AEM閱[作為Cloud Service開發准則。](/help/implementing/developing/introduction/development-guidelines.md)

測試連AEM接器
-------------------------

應使用本端環境開發技術建立新連接器（或修改現有連接器）。 合作夥伴團隊將為ISV合作夥伴提供沙盒環境，讓他們將AEMConnector部署至香草式應用程式，以確保其運作。
