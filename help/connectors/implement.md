---
title: 實作 AEM 連接器
description: 實作 AEM 連接器
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---

實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，您可以透過取得AEM的開發人員授權 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud).

常見整合模式
---------------------------

AEM是尖端的Web體驗管理解決方案，提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統提取資料至AEM。 例如，從CRM匯出聯絡資訊，以供造訪AEM支援之網站的更廣泛對象使用。  實施應使用Sling的 [排定的工作](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，可保證即使容器發生故障也能執行工作。 程式碼的設計應假設工作可能會觸發多次。
* 將資料從AEM匯出至外部系統。 例如，在AEM支援的網站上提交至CRM的Newsletter訂閱設定。
* 正在從AEM擷取資產。 例如，參考AEM Assets中儲存之資產的外部內容管理系統(CMS)。 或者，以連結至AEM Assets中影像的PIM系統為例。
* 將資產儲存在AEM基礎架構中。 例如，行銷資源管理(MRM)系統將核准的資產儲存在AEM Assets中。
* 設定和呈現自訂UI元件。 例如，允許作者拖放視訊元件，並設定要在即時網站上播放的特定視訊。
* 使用合作夥伴服務對資產採取行動。 例如，在發佈頁面時將資產傳送至視訊平台。
* 在AEM Admin Console中分析網站、頁面或資產。 例如，針對現有或未發佈的頁面提出SEO建議。
* 對由外部服務維護的使用者資料的頁面層級存取。 例如，運用人口統計資訊來個人化網站體驗。 閱讀ContextHub，這是一個用來儲存、操控和呈現內容資料的架構。
* 翻譯網站副本或資產中繼資料。 請參閱 [AEM Translation FrameworkBootstrap聯結器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) 適用於使用AEM Translation Framework的範常式式碼，這是翻譯聯結器的慣用實作。


實用檔案
--------------------

Experience Manageras a Cloud Service [檔案](../overview/introduction.md) 提供在AEM中進行開發的寶貴見解。 以下是一些特定的技術主題和參考資料，您在實作AEM聯結器時可能會發現這些主題和參考資料很有用：

* Adobe諮詢服務(ACS) [AEM範例](https://adobe-consulting-services.github.io/acs-aem-samples/) 給有良好註解的程式碼，以協助教育AEM開發人員
* 本文中常見整合模式一節中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案之外，Adobe和AEM社群還提供資源來協助將聯結器推向市場：

* Adobe社群的 [AEM論壇](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是一個使用中網站，您的同儕可透過此網站提出和回答問題
* 特定合作夥伴層級可提供額外的Adobe技術資源。 進一步瞭解 [Adobe交換計畫](https://partners.adobe.com/exchangeprogram/experiencecloud).
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](https://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

套件結構規則
-----------------------

為了支援滾動式部署，AEMas a Cloud Service套件（以聯結器為例）在「不可變」和「可變」內容之間有嚴格的區分。 套件應完全分隔為以下各項：

* `/apps`
* `/content` 和 `/conf`

聯結器應遵守以下封裝指導方針，相關說明請參閱 [本文](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 現有聯結器也應重構以符合要求。

此外，只有Adobe應將程式碼寫入 `/libs`，讓客戶和合作夥伴寫入 `/apps`.

現有聯結器可能也需要重構，以移動可能曾經放置過的任何設定 `/etc` 至其他頂層資料夾，例如 `/conf`. 此重組是作為AEM 6.5的一部分完成的，詳見 [AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

建議將大部分聯結器程式碼放在 `/apps/connectors/<vendor>` 為具有多個聯結器的客戶推廣乾淨的存放庫結構。

Cloud Services設定
-----------------------------

聯結器實作的一個方面是支援聯結器設定的程式碼。 此程式碼會使帶有聯結器名稱的卡片出現在「工具>操作>Cloud Services」下。 按一下時， [設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 客戶選取父資料夾以包含聯結器設定的位置彈出。 聯結器的程式碼應產生一個包含所有必須設定的屬性的表單，最終將值儲存在下的設定資料夾中 `/conf`. 您稍後可以在「網站屬性」標籤或「資產屬性」標籤下選取此資料夾。


內容感知設定
-----------------------------

[內容感知設定](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允許跨不同資料夾分層設定，包括 `/libs`， `/apps`， `/conf` 和下的子資料夾 `/conf`. 它支援繼承，因此客戶可以設定全域設定，同時對每個微網站進行特定變更。 由於可以在Cloud Services設定中善用此功能，聯結器程式碼應使用內容感知設定API來參照設定，而不是參照特定設定節點。

如果在聯結器中使用修改後的設定，則架構聯結器以處理包含/合併聯結器提供的預設設定與任何客戶設定的任何未來更新。 請記住，在沒有客戶警告和同意的情況下變更自訂（如客戶變更的）內容或設定可能會破壞其聯結器（或產生非預期的行為）。

編碼最佳實務
----------------------

由於AEMas a Cloud Service是雲端原生解決方案，因此有一些准則可能會影響聯結器的程式碼策略。 另請參閱 [AEMas a Cloud Service開發方針](/help/implementing/developing/introduction/development-guidelines.md) 以取得更多詳細資料。

測試AEM聯結器
-------------------------

應使用本機環境開發技術建立新聯結器（或修改現有聯結器）。 合作夥伴團隊將為ISV合作夥伴提供沙箱環境，他們可以在其中將AEM Connector部署到vanilla應用程式以確保它正常工作。
