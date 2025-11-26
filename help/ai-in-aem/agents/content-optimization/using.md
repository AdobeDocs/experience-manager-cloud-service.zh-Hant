---
title: 內容最佳化代理程式
description: 瞭解如何使用內容最佳化代理程式，透過套用自然語言指示建立通道就緒的變數，轉變使用者如何調整及調整資產。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b7bdb86c3d1b537b536173b6307c486fe436636
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---


# 內容最佳化代理程式 {#content-optimization-agent}

內容最佳化代理程式可套用自然語言指示，建立可上線的變數，以轉換使用者如何調整及調整資產。 無論是為特定數位頻道產生新轉譯、調整視覺屬性、變更背景或準備資產，代理程式都會自動解譯使用者意圖並執行複雜的編輯工作。 它與Discovery Agent緊密合作，運用其找到的資產，並使用核心[Dynamic Media （具有OpenAPI功能](/help/assets/dynamic-media-open-apis-overview.md)）產生最佳化的變數，以符合品牌、頻道和行銷活動需求，無需手動設計。

內容最佳化的部分主要優點包括：

* **輕鬆轉換資產**：將簡單、對話式的提示轉換為精確的影像作業，例如調整大小、銳利化、鏡射或重新著色，不需要專門的編輯工具。

* **頻道最佳化輸出**：快速產生為特定平台量身打造的轉譯，例如Instagram故事、網頁橫幅或其他行銷接觸點，確保資產可立即使用。

* **大規模的Creative增強功能**：套用視覺調整與增強功能，例如背景變更或圖形覆蓋，以支援大量創意工作流程，而不會減慢團隊速度。

* **[與Discovery Agent緊密合作](/help/ai-in-aem/agents/discovery/using.md)**：建立在Discovery Agent所識別的資產上，透過自然對話實現端對端資產擷取和最佳化。

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## 先決條件 {#prerequisites-content-optimization-agent}

產生影像資產的變體或最佳化： 您必須擁有：

* 有效的Dynamic Media授權

* 在AEM as a Cloud Service環境中啟用OpenAPI的Dynamic Media 。

* 在您的AEM as a Cloud Service環境中，處於[核准狀態](/help/assets/manage-organize-assets-view.md#manage-asset-status)的資產。


## 技能 {#skills-content-optimization-agent}

內容最佳化代理程式提供下列技能：

* **透過自然語言瞭解意圖**

  內容最佳化代理程式會從自然語言提示、頻道、行銷活動和對象內容等解釋使用者意圖，以決定最相關的最佳化動作。

* **產生動態內容變體**

  內容最佳化代理程式會建立最佳化的變體，作為針對不同管道和格式型別量身打造的動態URL。

* **最佳化影像內容**

  「內容最佳化代理程式」會套用格式轉換、解析度調整、裁切和銳利化等增強功能來改善影像品質。

* **多變體資產最佳化**

  內容最佳化代理程式可以使用單一自然語言提示，從探索代理程式傳回的資產中產生多個最佳化影像變化，讓使用者能夠快速並有效率地產生適用於頻道的轉譯。

## 角色 {#personas-content-optimization-agent}

管道行銷人員是內容最佳化代理程式的關鍵角色，他們可以選取正確的高解析度來源內容，並請求根據其管道和受眾區段量身打造的最佳化格式。

地區行銷人員和機構職員也可以使用內容最佳化代理程式，快速產生適用於管道的影像變化，以支援更快、更一致的內容製作。

## 如何存取Content Optimization Agent？ {#access-content-optimization-agent}

您可以透過AI助理存取AEM中的代理程式。 登入experience.adobe.com，您可以使用`Ask AI Assistant anything`欄位以自然語言指定提示，開始與AI助理互動：

![存取探索代理程式](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## 常見使用案例和範例提示 {#use-cases-prompts}

透過[探索代理程式](/help/ai-in-aem/agents/discovery/using.md)搜尋正確的資產，以使用內容最佳化提示。 浮現相關影像後，使用者可以直接從搜尋結果產生一或多個資產的最佳化或通道特定變體。 此工作流程可確保高品質的輸入資料，並持續提供更佳的最佳化結果。 [檢視可用最佳化的完整清單](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/?lang=zh-Hant)。

* **高解析度轉譯建立**

  代理程式可產生具有指定解析度和品質層級的資產新轉譯，讓您無需手動編輯即可輕鬆準備可上線的變化。


  範例提示：

  以`2000px`品質建立`JPEG`轉譯為`80%`。

  使用[探索代理程式](/help/ai-in-aem/agents/discovery/using.md)搜尋正確的資產，然後在有多個搜尋結果時使用下列提示：

  針對第3個搜尋結果，建立`2000px`轉譯為`JPEG`，品質為`80%`。

  或者

  針對`Asset ID`，產生2000px轉譯為`JPEG`，品質為`80%`

* **影像增強功能**

  代理程式可套用視覺化改善（例如銳利化），以確保資產在用於各種行銷活動之前看起來清晰且定義清楚。

  範例提示：

  銳利化影像。


* **背景色彩調整**

  代理程式可以更新或取代透明資產中的背景顏色，支援品牌特定的色彩配置或行銷活動導向的視覺主題。

  範例提示：

  將`PNG`的背景顏色變更為`#ff8932`。

* **方向轉換**

  該代理程式可以翻轉或映象視覺效果，以符合版面需求或創意方向，而無需外部編輯工具。

  範例提示：

  水準映象影像。

* **頻道最佳化的轉譯**

  代理程式可針對特定平台需求（例如Instagram劇本）產生量身打造的轉譯，確保資產自動符合格式、比例和品質准則。

  範例提示：

  建立`Instagram`劇本的轉譯。

* **品牌覆蓋和複合層代**

  代理程式可透過精確放置將促銷圖形、覆蓋圖或徽章套用至現有資產，以支援快速建立行銷活動可用的複合專案。

  範例提示：

  將含有`30%`折扣圖形的影像覆蓋在促銷橫幅上，從中心放置`100px`。

  >[!NOTE]
  >
  >覆蓋圖位置可能不準確。


## 最佳化結果 {#content-optimization-agent-results}

當您指定最佳化提示時，內容最佳化代理程式會傳回增強型資產，以及根據資產型別提供的便利存取選項：

* **影像**：回應包含縮圖預覽和開啟Dynamic Media URL或下載最佳化影像的選項。

* **PDF檔案**：回應包含縮圖預覽以及開啟Dynamic Media URL或下載最佳化檔案的選項。

* **影片**：回應提供開啟Dynamic Media URL或下載最佳化影片的相關選項。

![內容最佳化結果](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

這些結果可讓您輕鬆檢閱最佳化的輸出，並立即用於下游管道或工作流程。

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
