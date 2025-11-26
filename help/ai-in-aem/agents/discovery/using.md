---
title: 探索代理程式概述
description: 瞭解如何使用Discovery Agent，透過順暢的對話提示來隨選提供相關的AEM內容，以提供精簡的免費探索體驗。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b7bdb86c3d1b537b536173b6307c486fe436636
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---


# 探索代理程式 {#discovery-agent}

Discovery Agent透過自然的對話提示隨選提供AEM內容，提供精簡的免費點閱體驗。 它會在Assets、內容片段和最適化Forms中聰明地搜尋，以傳遞相關素材，例如影像、影片、PDF檔案、文章和表單範本。 使用自然語言，您可以搜尋內容，而不需要在AEM Assets介面中建置複雜查詢或套用篩選器。 根據您的提示，代理程式會傳回已組織的結果以及資產中繼資料和傳送URL，並準備嵌入其他應用程式。

Discovery Agent的部分主要優點包括：

* **整合式內容探索**：從單一對話式介面存取所有型別的AEM內容，例如影像、影片、PDF檔案、文章和表單。

* **更快的行銷活動規劃**：快速收集跨電子郵件、網頁和社交管道行銷活動的視覺效果和表單。

* **增強的生產力**：透過自動化、意圖式搜尋，減少瀏覽儲存庫或篩選中繼資料所花費的時間。

* **一致的內容使用率**：確保重複使用核准的資產和片段，維持跨管道的品牌一致性。

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## 技能 {#skills-discovery-agent}

探索代理程式提供下列技能：

* **自然語言內容探索**\
  探索代理程式可讓使用者使用簡單的自然語言提示，在Adobe Experience Manager (AEM)中尋找相關資產、內容片段和調適型表單，而不需要複雜的搜尋查詢。

* **標籤式資產探索**

  探索代理程式會使用自然語言提示來尋找與AEM存放庫中特定標籤相關聯的資產，協助使用者快速存取依組織分類法組織或未組織的內容。

* **資料夾式內容探索：**\
  探索代理程式可透過解譯參考AEM中資料夾名稱的自然語言提示來識別資產。 使用者只需在提示中提及資料夾，無需手動導覽存放庫，即可大幅減少尋找所需內容的點按次數。

## 角色 {#personas-discovery-agent}

### 行銷活動管理員 {#campaign-managers}

Discovery Agent可讓Campaign管理員快速識別並重複使用受信任的高效能內容，以進行構想。

### 管道行銷人員 {#channel-marketers}

探索代理程式可讓管道行銷人員有效率地尋找相關資產，建立有凝聚力的多管道體驗。

### DAM程式庫管理員 {#dam-librarians}

DAM資料庫管理員可以標幟缺少組織所設定的中繼資料標準的資產，支援一致的控管，並確保資產保持完整且可跨管道使用。

### 機構和合作夥伴 {#agencies-partners}

代理商和合作夥伴可在Content Hub中輕鬆找到品牌核准的資產，並重複使用它們以加速創意工作，同時符合品牌標準。

## 如何存取探索代理程式？ {#access-discovery-agent}

您可以透過AI助理存取AEM中的代理程式。 登入experience.adobe.com，您可以使用搜尋方塊以自然語言指定提示，開始與AI助理互動：

![存取探索代理程式](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

如需有關存取探索代理程式的MCP端點的資訊，請聯絡Adobe支援。

## 常見使用案例和範例提示 {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**標籤式資產探索**

探索代理程式會使用自然語言提示來尋找與AEM存放庫中特定標籤相關聯的資產，協助使用者快速存取根據其組織分類法組織的內容。

範例提示：

顯示資料夾`office`中標籤為`WKND`的影像。

**資料夾式內容探索：**\
探索代理程式可透過解譯參考AEM中資料夾名稱的自然語言提示來識別資產。 使用者只需在提示中提及資料夾，無需手動導覽存放庫，即可大幅減少尋找所需內容的點按次數。

範例提示：

* 資料夾`WKND`中是否有任何svg？
* 顯示資料夾`Nov 1 2025`中在`WKND`之後修改的資產。
* 在資料夾`lifestyle`中列出`WKND`影像。

**解析度與格式型資產探索**

Discovery Agent可識別符合特定品質要求的資產（例如檔案格式或最低解析度），讓使用者快速找到產品視覺效果，以便跨管道進行高品質的傳送和重複使用。

範例提示：

尋找至少2000px寬的產品包裝PNG影像。

**方向型內容探索**

Discovery Agent可以辨識視覺屬性（例如人員出現和影像方向）來篩選資產。 這可讓使用者快速將內容縮小至最相關的視覺效果，而不需在AEM中手動套用多個篩選器。

範例提示：

以橫向顯示個人資產。

### 內容片段 {#discovery-agent-use-cases-content-fragments}

探索代理程式會解譯促銷活動名稱、產品品牌、出版物狀態和最近建立活動的自然語言參考，協助使用者快速找到正確的內容片段。 它可讓團隊呈現行銷活動就緒的片段並檢視品牌專屬內容，完全無須手動瀏覽資料夾或在AEM中套用多個篩選器。

範例提示：

* 顯示建立WKND選件行銷活動的內容片段。

* 顯示美式飲料的內容片段。

* 顯示WKND飲料的所有已發佈內容片段。

* 列出過去2週內建立的所有內容片段。

### Forms {#discovery-agent-use-cases-forms}

Discovery Agent可協助您使用自然語言提示快速找到最適化表單。 它會搜尋表單內容和中繼資料，以根據提示中的關鍵字尋找相符專案。 這表示即使搜尋字詞不在表單的標題或說明中，您仍可成功探索相關表單。

範例提示：

* 顯示所有貸款申請表單。
* 尋找要申請工作的表單。
* 尋找聯絡表單。
* 我正在尋找員工入職表格。
* 顯示信用卡申請表單。

注意：表單探索目前僅支援Edge Delivery Services表單，且標籤式搜尋目前不適用於表單。

## 搜尋結果 {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

Discovery Agent會傳回每個查詢的前幾個結果（依相關性排序），以確保完全符合的專案會先出現。 Agent結合中繼資料導向的查詢與語意搜尋，以組合可能符合的重點集合，然後使用LLM根據使用者意圖將其排名。 這種混合式方法可提供精確的內容感知結果，而不完全取決於直接的關鍵字比對。

每個結果都包含資產名稱以及重要的資產中繼資料，例如資產路徑、建立者、建立日期、標題、說明、格式、上次修改者、上次修改日期、檔案大小、維度、[動態媒體URL](/help/assets/dynamic-media/dynamic-media.md)和相關標籤。 如果資產處於已核准狀態，結果也會包含具有OpenAPI URL的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)。

您可以按一下資產路徑，順暢地導覽至AEM內的資產位置。

![使用探索代理程式搜尋資產](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

您可以使用這些資產詳細資料快速評估資產是否符合要求，而無需瀏覽至每個資產以檢視這些詳細資訊。

>[!NOTE]
>
>[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)欄位只有在資產已發佈且您具備有效的Dynamic Media授權時，才會顯示在搜尋結果中。 同樣地，只有當您具備有效的Dynamic Media授權且您的AEM as a Cloud Service執行個體已啟用具有OpenAPI的Dynamic Media時，才會顯示[具有OpenAPI URL的Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)欄位。

### 內容片段 {#discovery-agent-search-results-content-fragments}

探索代理程式提供內容片段的全文檢索搜尋功能，傳回最符合指定提示的前幾個結果。 每個結果都包含內容片段名稱以及關鍵中繼資料欄位，例如內容片段路徑、建立者、建立日期、變數、上次修飾詞和上次修改日期欄位。

![使用探索代理程式搜尋內容片段](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

您可以按一下內容片段路徑，順暢地導覽至AEM中的內容片段位置。

## 提示最佳實務 {#prompting-best-practices-discovery-agent}

以您的自然語言提示指定簡明的詳細資料，讓代理程式可以傳回正確且相關的結果。 您越清楚描述所要尋找的內容，代理程式就越能精簡及縮小輸出。 例如，您可以：

* 在篩選資產的提示中定義資產中繼資料，例如標籤、資料夾名稱、建立日期、發佈狀態、作者名稱。

* 使用您組織的特定中繼資料，例如，類別（跑鞋、電子產品）、季節（秋季、春季）、活動（黑色星期五、產品上市）和頻道（網路、電子郵件、列印），以進一步篩選內容。

