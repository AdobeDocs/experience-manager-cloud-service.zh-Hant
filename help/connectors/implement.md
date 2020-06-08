---
title: 實作 AEM 連接器
description: 實作 AEM 連接器
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 7%

---


實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，AEM的開發人員授權可透過 [Adobe Exchange計畫取得](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。

通用整合模式
---------------------------

AEM是尖端的網頁體驗管理解決方案，提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統將資料拉入AEM。 例如，從CRM匯出聯絡資訊，以便讓造訪AEM架構網站的更廣大觀眾也能使用。  實作應使用Sling&#39;s [Scheduled Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，這可保證即使容器關閉，也會執行工作。 程式碼應設計為假設工作可能會觸發多次。
* 將資料從AEM匯出至外部系統。 例如，電子報訂閱設定已在AEM支援的網站上提交至CRM。
* 從AEM擷取資產。 例如，參照儲存在AEM資產中的資產的外部內容管理系統(CMS)。 或者，另一個範例是連結至AEM資產中影像的PIM系統。
* 將資產儲存在AEM基礎架構中。 例如，行銷資源管理(MRM)系統會在AEM資產中儲存已核准的資產。
* 設定和轉譯自訂UI元件。 例如，允許作者拖放視訊元件，並設定特定視訊以在即時網站上播放。
* 使用合作夥伴服務處理資產。 例如，在發佈頁面時，將資產傳送至視訊平台。
* 在AEM管理控制台中分析網站、頁面或資產。 例如，為現有或未發佈的頁面建立SEO建議。
* 頁面層級存取外部服務維護的使用者資料。 例如，運用人口統計資訊來個人化網站體驗。 閱讀ContextHub的相關資訊，此架構可用來儲存、控制和呈現內容資料。
* 轉換網站復本或資產中繼資料。 請參閱 [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) ，以取得使用AEM Translation Framework（偏好實作的轉譯連接器）的范常式式碼。


有用的檔案
--------------------

Experience Manager作為雲端服務檔案 [提供](../overview/introduction.md) AEM中開發的寶貴見解。 以下是一些在實作AEM連接器時可能會覺得有用的特定技術主題和參考：

* Adobe Consulting Services(ACS) [AEM範例](http://adobe-consulting-services.github.io/acs-aem-samples/) ，以取得注釋良好的程式碼，以協助教育AEM開發人員
* 本文「常用整合模式」一節中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案外，Adobe和AEM社群還提供資源，協助將連接器帶入市場：

* Adobe社群的 [AEM論壇](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) ，是一個活躍的網站，讓同儕提問並回覆問題
* 其他Adobe技術資源適用於特定合作夥伴層級。 進一步瞭解 [Adobe Exchange計畫](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](http://www.adobe.com/tw/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

封裝結構規則
-----------------------

為支援滾動部署，AEM（例如連接器）是雲端服務套件，在「不可變」和「可變」內容之間有嚴格的分隔。 應將包清晰地分開，這些包包括：

* `/apps`
* `/content`與`/conf`

連接器應遵守本文所述的這些包裝 [准則](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 現有連接器也應重新構圖，以符合規定。

此外，只有Adobe才應將程式碼寫入， `/libs`客戶和合作夥伴應將程式碼寫入 `/apps`。

可能還需要重構現有連接器，以便將任何配置移入其他頂級資料夾( `/etc` 如)中 `/conf`。 這在 [AEM檔案中說明](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

建議將大部分連接器代碼放在下面，以便為具有 `/apps/connectors/<vendor>` 多個連接器的客戶提供乾淨的儲存庫結構。

雲端服務組態
-----------------------------

連接器實現的一個方面是支援連接器配置的代碼。 此程式碼會在「工具>作業>雲端服務」下方顯示連接器名稱的資訊卡。 按一下時，會彈出一個設定瀏覽器，客戶會在其中選取要包含連接器設定的父資料夾。 連接器的代碼應生成一個包含所有必須配置的屬性的表單，最終將值儲存在下面的配置資料夾中 `/conf`。 此資料夾稍後可在「網站屬性」標籤或「資產屬性」標籤下選取。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) (Context-Aware Configurations)允許跨不同資料夾(包括下方的子資料夾 `/libs`、 `/apps`和子 `/conf` 資料夾)進行層配置 `/conf`。 它支援繼承，以便客戶可以配置全局配置，同時對每個微站點進行特定更改。 由於此功能可用於雲端服務設定，因此連接器程式碼應使用內容感知組態API來參考組態，而非參考特定組態節點。

如果連接器中使用了修改的配置，請構建連接器以處理將來對任何客戶配置提供的預設配置進行包括／合併任何更新的連接器。 請記住，在未經客戶警告及同意的情況下變更自訂（如客戶所變更）內容或設定，可能會中斷（或造成非預期行為）其Connector。

編碼最佳實務
----------------------

由於AEM是雲端服務是雲端原生解決方案，因此有一些准則可能會影響連接器的程式碼策略。 如需詳 [細資訊，請參閱AEM雲端服務開發准則](/help/implementing/developing/introduction/development-guidelines.md) 。

測試AEM Connector
-------------------------

應使用本端環境開發技術建立新連接器（或修改現有連接器）。 合作夥伴團隊將為ISV合作夥伴提供沙盒環境，讓他們可將AEM Connector部署至Vanilla應用程式，以確保其運作。
