---
title: 實施 AEM 連接器
description: 了解關於連接器、這類工具的功能，以及如何在 Experience Manager 中實作這些重要工具。
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 6%

---


實施 AEM 連接器
=============================

以下提供建立AEM聯結器的實用參考，並應透過有關[提交](submit.md)和[維護](maintain.md)聯結器的指南來閱讀。

可透過[AEM方案](https://partners.adobe.com/technologyprogram/experiencecloud.html)取得Adobe Exchange的開發人員授權。

常見整合模式
---------------------------

AEM是尖端的Web體驗管理解決方案，提供許多潛在的整合領域。 常見的整合模式包括：

* 從外部系統提取資料至AEM。 例如，從CRM匯出聯絡資訊，以供造訪AEM支援之網站的更廣泛對象使用。  實作應使用Sling的[已排程工作](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，以確保即使容器發生故障也能執行工作。 程式碼的設計應假設工作可能會觸發多次。
* 將資料從AEM匯出至外部系統。 例如，Newsletter訂閱設定會在AEM支援的網站上提交至CRM。
* 從AEM擷取資產。 例如，參考AEM Assets中儲存之資產的外部內容管理系統(CMS)。 或者，以連結至AEM Assets影像的PIM系統為例。
* 將資產儲存在AEM基礎架構中。 例如，行銷資源管理(MRM)系統將核准的資產儲存在AEM Assets中。
* 設定和呈現自訂UI元件。 例如，允許作者拖放視訊元件，並設定要在即時網站上播放的特定視訊。
* 透過合作夥伴服務對資產採取行動。 例如，在發佈頁面時傳送資產至視訊平台。
* 在AEM Admin Console中分析網站、頁面或資產。 例如，針對現有或未發佈的頁面提出SEO建議。
* 對由外部服務維護的使用者資料的頁面層級存取。 例如，使用人口統計資訊來個人化網站體驗。 閱讀有關ContextHub的資訊，這是一個用於儲存、操作和呈現內容資料的架構。
* 翻譯網站副本或資產中繼資料。 如需使用AEM Translation Framework的範常式式碼，請參閱[AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector)，這是慣用的翻譯聯結器實作。


有用的檔案
--------------------

Experience Manager as a Cloud Service [檔案](../overview/introduction.md)提供了有關在AEM中進行開發的寶貴見解。 以下是一些特定的技術主題和參考資料，您在實作AEM聯結器時可能會發現這些主題和參考資料很有用：

* 具有良好註解的程式碼的Adobe Consulting Services (ACS) [AEM範例](https://adobe-consulting-services.github.io/acs-aem-samples/)，可協助指導AEM開發人員
* 本文的「常見整合模式」一節中的各種檔案連結

社群資源
--------------------

除了上述靜態檔案之外，Adobe和AEM社群還提供資源，協助將聯結器推向市場：

* Adobe社群的[AEM論壇](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html)是同儕詢問和回答問題的作用中網站
* 為特定合作夥伴層級提供其他Adobe技術資源。 深入瞭解[Adobe Exchange方案](https://partners.adobe.com/technologyprogram/experiencecloud.html)。
* 如果貴組織想要實作協助，請考慮選擇Adobe的 [Professional Services](https://solutionpartners.adobe.com/s/directory) team，或參閱 [Solution Partner Finder](https://solutionpartners.adobe.com/s/directory/) ，以取得Adobe全球合作夥伴的清單

套件結構規則
-----------------------

為方便滾動式部署，AEM as a Cloud Service套件（例如聯結器）在「不可變」和「可變」內容之間維持嚴格的劃分。 套件應清楚組織，以包含：

* `/apps`
* `/content` 和 `/conf`

聯結器應該遵守這些封裝指導方針，這些指導方針在[AEM專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md)中說明。 現有聯結器也應重構以符合要求。

此外，只有Adobe應將程式碼寫入`/libs`，而客戶和合作夥伴則應將程式碼寫入`/apps`。

現有聯結器可能也需要重構，以將可能曾放置`/etc`的任何設定移至其他頂層資料夾，例如`/conf`。 此重組是作為AEM 6.5的一部分完成的，並在[AEM 6.5檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring)中進行了說明。

Adobe建議將大部分聯結器程式碼放在`/apps/connectors/<vendor>`下，以維持乾淨的存放庫結構，尤其是針對使用多個聯結器的客戶。

雲端服務設定
-----------------------------

聯結器實作的一個方面是支援聯結器設定的程式碼。 此程式碼會導致包含聯結器名稱的卡片出現在「工具>作業>雲端服務」下。 按一下時，會彈出一個[設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)，客戶可在此選取要包含聯結器設定的上層資料夾。 聯結器的程式碼會產生一個包含所有必須設定的屬性的表單，最終將值儲存在`/conf`下的設定資料夾中。 您稍後可以在「網站屬性」標籤或「Assets屬性」標籤下選取此資料夾。


內容感知設定
-----------------------------

[內容感知設定](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)可讓您跨不同資料夾進行階層設定，包括`/libs`、`/apps`、`/conf`以及`/conf`下的子資料夾。 它支援繼承，因此客戶可以設定全域設定，同時對每個微網站進行特定變更。 由於此功能可用於雲端服務設定，因此聯結器程式碼應使用內容感知設定API來參照設定，而非參照特定設定節點。

如果在聯結器中使用修改後的設定，則建構聯結器以處理包含/合併聯結器提供的預設設定與任何客戶設定的任何未來更新。 請記住，在未經事先通知和同意的情況下修改客戶自訂內容或設定可能會中斷或導致其聯結器中的意外行為。

編碼最佳實務
----------------------

由於AEM as a Cloud Service是雲端原生解決方案，因此有一些准則可能會影響聯結器的程式碼策略。 如需詳細資訊，請參閱[AEM as a Cloud Service開發指導方針](/help/implementing/developing/introduction/development-guidelines.md)。

測試AEM聯結器
-------------------------

應使用本機環境開發技術來建立新聯結器（或修改現有聯結器）。 合作夥伴團隊為ISV合作夥伴提供沙箱環境，他們可以在其中將AEM聯結器部署到vanilla應用程式以確保它正常工作。
