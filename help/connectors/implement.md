---
title: 實作 AEM 連接器
description: 實作 AEM 連接器
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---

實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，您可透過 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud).

常見整合模式
---------------------------

AEM是頂尖的網頁體驗管理解決方案，提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統提取資料至AEM。 例如，從CRM匯出連絡資訊，以便讓造訪AEM支援網站的更廣大受眾使用。  實作應使用Sling的 [排程作業](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，即使容器關閉，也能確保執行工作。 程式碼的設計應假設工作可能觸發多次。
* 將資料從AEM匯出至外部系統。 例如，電子報訂閱設定已在AEM支援的網站上提交至CRM。
* 從AEM擷取資產。 例如，外部內容管理系統(CMS)會參考儲存在AEM Assets中的資產。 或者，作為另一個範例，連結至AEM Assets中影像的PIM系統。
* 將資產儲存在AEM基礎架構中。 例如，行銷資源管理(MRM)系統會在AEM Assets中儲存已核准資產。
* 設定和轉譯自訂UI元件。 例如，允許作者拖放視訊元件，並設定特定視訊以在即時網站上播放。
* 使用合作夥伴服務對資產採取行動。 例如，發佈頁面時傳送資產至視訊平台。
* 在AEM Admin Console中分析網站、頁面或資產。 例如，為現有或未發佈的頁面提出SEO建議。
* 對外部服務所維護的使用者資料的頁面層級存取。 例如，運用人口統計資訊來個人化網站體驗。 閱讀ContextHub的相關資訊，ContextHub是儲存、操控和呈現內容資料的架構。
* 轉譯網站副本或資產中繼資料。 請參閱 [AEM Translation FrameworkBootstrap連接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) 適用於使用AEM翻譯架構的范常式式碼，這是翻譯連接器的偏好實作。


實用檔案
--------------------

Experience Manageras a Cloud Service [檔案](../overview/introduction.md) 提供在AEM中開發的寶貴見解。 以下是實作AEM連接器時您可能會覺得有用的一些特定技術主題和參考：

* Adobe咨詢服務(ACS) [AEM範例](https://adobe-consulting-services.github.io/acs-aem-samples/) 以取得良好評論的程式碼，協助教育AEM開發人員
* 本文「常見整合模式」區段中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案，Adobe和AEM社群也提供資源，協助將連接器推向市場：

* Adobe社群 [AEM論壇](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是同儕提問和回答問題的活躍網站
* 特定合作夥伴層級提供其他Adobe技術資源。 深入了解 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud).
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](https://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

封裝結構規則
-----------------------

為了支援滾動部署，AEMas a Cloud Service套件（其中連接器為範例）在「不可變」和「可變」內容之間有嚴格的區隔。 應將包幹淨地分開，這些包包括：

* `/apps`
* `/content` 和 `/conf`

連接器應遵守這些封裝准則，相關說明請參閱 [這篇文章](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 現有連接器也應重構以符合要求。

此外，只有Adobe才應將程式碼寫入 `/libs`，客戶和合作夥伴可以透過 `/apps`.

可能還需要重構現有連接器，才能移動原本可能已放置的任何配置 `/etc` 放入其他頂層資料夾，例如 `/conf`. 此重新調整屬於AEM 6.5的一部分，相關說明請參閱 [AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

建議將大部分的連接器代碼放置在 `/apps/connectors/<vendor>` 若要提升具有數個連接器之客戶的乾淨存放庫結構。

Cloud Services配置
-----------------------------

連接器實施的一個方面是支援連接器配置的代碼。 此代碼會使帶有連接器名稱的卡片顯示在「工具」>「操作」>「Cloud Services」下。 按一下後， [配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 彈出，客戶在其中選取要包含連接器配置的父資料夾。 連接器的程式碼應會產生包含所有必須設定的屬性的表單，最終將這些值儲存在下的設定資料夾中 `/conf`. 您稍後可以在Sites屬性標籤或Assets屬性標籤下選取此資料夾。


內容感知配置
-----------------------------

[內容感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 可跨不同資料夾進行層配置，包括 `/libs`, `/apps`, `/conf` 位於下方的子資料夾 `/conf`. 它支援繼承，讓客戶可以在為每個微網站進行特定變更時設定全域設定。 因為此功能可用於Cloud Services設定，連接器程式碼應使用內容感知設定API參考設定，而非參考特定設定節點。

如果連接器中使用了修改的配置，請架構連接器以處理包括/合併連接器提供的預設配置的任何未來更新以及任何客戶配置。 請記住，若變更自訂（如客戶所變更）內容或設定而未經客戶警告及同意，其Connector可能會中斷（或產生非預期的行為）。

編寫最佳實務
----------------------

由於AEMas a Cloud Service是雲端原生解決方案，因此有些准則可能會影響連接器的程式碼策略。 請參閱 [AEMas a Cloud Service開發准則](/help/implementing/developing/introduction/development-guidelines.md) 以取得更多詳細資訊。

測試AEM Connector
-------------------------

應使用本機環境開發技術建立新連接器（或修改現有連接器）。 合作夥伴團隊將為ISV合作夥伴提供沙箱環境，讓他們將其AEM Connector部署至Vanilla應用程式，以確保其可正常運作。
