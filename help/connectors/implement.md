---
title: 實作 AEM 連接器
description: 瞭解如何建置、測試和實作AEM聯結器。 此外，您也可以瞭解常見的整合模式。
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 7%

---

實作 AEM 連接器
=============================

以下提供建立 [AEM Connectors的實用參考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，並應結合提交和維護連接器 [的指](submit.md) 南來閱讀 [](maintain.md) 。

請注意，您可以透過取得AEM的開發人員授權 [Adobe交換程式](https://partners.adobe.com/exchangeprogram/experiencecloud).

常見整合模式
---------------------------

AEM是尖端的Web體驗管理解決方案，提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統提取資料至AEM。 例如，從CRM匯出聯絡資訊，以供造訪AEM支援之網站的更廣泛對象使用。  實施應使用Sling的 [排定的工作](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，這可確保即使容器發生故障也能執行作業。 程式碼的設計應假設工作可能會觸發多次。
* 將資料從AEM匯出至外部系統。 例如，在AEM支援的網站上提交給CRM的Newsletter訂閱設定。
* 正在從AEM擷取資產。 例如，參照儲存在AEM Assets中之資產的外部內容管理系統(CMS)。 或者，以連結至AEM Assets影像的PIM系統為例。
* 將資產儲存在AEM基礎架構中。 例如，行銷資源管理(MRM)系統將核准的資產儲存在AEM Assets中。
* 設定和呈現自訂UI元件。 例如，允許作者拖放視訊元件，並設定要在即時網站上播放的特定視訊。
* 透過合作夥伴服務對資產採取行動。 例如，在發佈頁面時傳送資產至視訊平台。
* 在AEM Admin Console中分析網站、頁面或資產。 例如，針對現有或未發佈的頁面提出SEO建議。
* 對由外部服務維護的使用者資料的頁面層級存取。 例如，使用人口統計資訊來個人化網站體驗。 閱讀有關ContextHub的資訊，這是一個用於儲存、操作和呈現內容資料的架構。
* 翻譯網站副本或資產中繼資料。 請參閱 [AEM翻譯框架Bootstrap聯結器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) 適用於使用AEM Translation Framework的範常式式碼，這是偏好使用的翻譯聯結器實作。


有用的檔案
--------------------

Experience Manageras a Cloud Service [檔案](../overview/introduction.md) 提供在AEM中進行開發的寶貴見解。 以下是一些特定的技術主題和參考，您在實作AEM聯結器時會發現它們很有用：

* Adobe諮詢服務(ACS) [AEM範例](https://adobe-consulting-services.github.io/acs-aem-samples/) 已發表好評的程式碼，以協助指導AEM開發人員
* 本文的「常見整合模式」一節中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案之外，Adobe和AEM社群還提供資源，協助將聯結器推向市場：

* Adobe社群的 [AEM論壇](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是同儕提出和回應問題的作用中網站
* 為特定合作夥伴層級提供其他Adobe技術資源。 進一步瞭解 [Adobe交換程式](https://partners.adobe.com/exchangeprogram/experiencecloud).
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](https://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) ，以取得Adobe全球合作夥伴的清單

套件結構規則
-----------------------

為了支援滾動式部署，AEMas a Cloud Service套件（以聯結器為例）在「不可變」和「可變」內容之間有嚴格的區分。 套裝軟體應完全分開，包括下列專案：

* `/apps`
* `/content` 和 `/conf`

聯結器應遵守這些封裝指導方針，相關說明請參閱 [本文](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 現有聯結器也應重構以符合要求。

此外，只有Adobe應將程式碼寫入 `/libs`，由客戶和合作夥伴寫入 `/apps`.

現有聯結器可能也需要重構，才能移動可能曾經放置過的任何設定 `/etc` 至其他頂層資料夾，例如 `/conf`. 此重組是作為AEM 6.5的一部分完成的，詳見 [AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

建議將大部分聯結器程式碼放在 `/apps/connectors/<vendor>` 為擁有數個聯結器的客戶宣傳乾淨的存放庫結構。

Cloud Service設定
-----------------------------

聯結器實作的一個方面是支援聯結器設定的程式碼。 此程式碼會使帶有聯結器名稱的卡片出現在「工具>作業>Cloud Service」下。 按一下時， [設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 客戶選取上層資料夾以包含聯結器設定的位置會彈出。 聯結器的程式碼將產生一個包含所有必須設定的屬性的表單，最終將值儲存在下的設定資料夾中 `/conf`. 您稍後可以在「網站屬性」標籤或「資產屬性」標籤下選取此資料夾。


內容感知設定
-----------------------------

[內容感知設定](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允許跨不同資料夾進行圖層設定，包括 `/libs`， `/apps`， `/conf` 和子資料夾在 `/conf`. 它支援繼承，因此客戶可以設定全域設定，同時對每個微網站進行特定變更。 由於此功能可用於Cloud Service設定，因此聯結器程式碼應使用內容感知設定API來參照設定，而非參照特定設定節點。

如果在聯結器中使用修改後的設定，則建構聯結器以處理包含/合併聯結器提供的預設設定與任何客戶設定的任何未來更新。 請記住，在沒有客戶警告和同意的情況下變更自訂（如由客戶變更的）內容或設定可能會破壞其聯結器（或產生非預期行為）。

編碼最佳實務
----------------------

由於AEMas a Cloud Service是雲端原生解決方案，因此有一些准則可能會影響聯結器的程式碼策略。 另請參閱 [AEMas a Cloud Service開發指導方針](/help/implementing/developing/introduction/development-guidelines.md) 以取得更多詳細資料。

測試AEM聯結器
-------------------------

應使用本機環境開發技術來建立新聯結器（或修改現有聯結器）。 合作夥伴團隊將為ISV合作夥伴提供沙箱環境，他們可以在其中將AEM聯結器部署到vanilla應用程式以確保它正常工作。
