---
title: 內容探索代理
description: 瞭解如何使用內容探索代理程式，透過天然的對話提示，隨選提供相關的AEM內容，以精簡的點選式免費探索體驗。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 45c547a0a7372e5ebe23bd6b816798cd3b225872
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 0%

---


# 內容探索代理 {#discovery-agent}

作為AEM的[內容建議程式代理程式的一部分，](/help/ai-in-aem/agents/content-advisor/overview.md)內容探索代理程式會透過自然、對話式的提示隨選提供AEM內容，以精簡的免費探索體驗。 它會在Assets、內容片段、AEM Sites頁面和最適化Forms間聰明地搜尋，以傳遞相關素材，例如影像、影片、PDF檔案、文章和表單範本。 使用自然語言，您可以搜尋內容，而不需要在AEM Assets介面中建置複雜查詢或套用篩選器。 根據您的提示，代理程式會傳回已組織的結果以及資產中繼資料和傳送URL，並準備嵌入其他應用程式。

內容探索代理程式的一些主要優點包括：

* **整合式內容探索**：從單一對話式介面存取所有型別的AEM內容，例如影像、影片、PDF檔案、文章、頁面和表單。

* **更快的行銷活動規劃**：快速收集跨電子郵件、網頁和社交管道行銷活動的視覺效果和表單。

* **增強的生產力**：透過自動化、意圖式搜尋，減少瀏覽儲存庫或篩選中繼資料所花費的時間。

* **一致的內容使用率**：確保重複使用核准的資產和片段，維持跨管道的品牌一致性。

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南。](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

## 技能 {#skills-discovery-agent}

內容探索代理程式提供下列技能：

* **自然語言內容探索**

  內容探索代理程式可讓使用者使用簡單的自然語言提示，在Adobe Experience Manager (AEM)中尋找相關資產、內容片段、調適型表單和AEM Sites頁面，而不需要複雜的搜尋查詢。

* **中繼資料型資產探索**

  內容探索代理程式會使用自然語言提示，根據AEM中資產可用的中繼資料來尋找資產。 使用者可以使用中繼資料來探索資產，例如標籤、作者或發佈者電子郵件ID、發佈或修改日期、MIME型別、資產型別、狀態、在Assets檢視或管理員檢視的中繼資料表單中定義的自訂中繼資料屬性等。 如需完整清單，請參閱[常見使用案例和範例提示](#use-cases-prompts)。

  您也可以在單一提示中合併多個中繼資料篩選器，以精簡搜尋結果。

* **資料夾式內容探索：**\
  內容探索代理程式可透過解譯參考AEM中資料夾名稱的自然語言提示來識別資產。 使用者只需在提示中提及資料夾，無需手動導覽存放庫，即可大幅減少尋找所需內容的點按次數。

## 角色 {#personas-content-discovery}

### 行銷活動管理員 {#campaign-managers}

內容探索代理程式可讓行銷活動經理快速識別並重複使用受信任的高效能內容，以利構想。

### 管道行銷人員 {#channel-marketers}

內容探索代理程式可讓管道行銷人員有效率地尋找相關資產，建立有凝聚力的多管道體驗。

### DAM程式庫管理員 {#dam-librarians}

DAM資料庫管理員可以標幟缺少組織所設定的中繼資料標準的資產，支援一致的控管，並確保資產保持完整且可跨管道使用。

### 機構和合作夥伴 {#agencies-partners}

代理商和合作夥伴可以輕鬆地在Content Hub中找到品牌核准的資產，並重複使用它們以加速創意工作，同時與品牌標準保持一致。

## 如何存取 {#access}

您可以透過AI助理存取AEM中的內容探索代理程式。 登入[`experience.adobe.com`](https://experience.adobe.com)，您可以使用搜尋方塊以自然語言指定提示，開始與AI助理互動：

![存取內容探索代理程式](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

如需有關存取內容探索代理程式的MCP端點的資訊，請聯絡Adobe支援。

## 常見使用案例和範例提示 {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**中繼資料型資產探索**

內容探索代理程式會使用自然語言提示，根據AEM中資產可用的中繼資料來尋找資產。 使用者可以使用以下中繼資料屬性探索資產：標籤、依電子郵件ID建立、依電子郵件ID修改、依電子郵件ID發佈、建立日期、修改日期、發佈日期、MIME型別、資產型別、狀態、檔案格式、檔案大小、影像寬度、影像高度，以及在單一提示內使用多個中繼資料篩選器。

內容探索代理程式也會搜尋中繼資料結構中可用的自訂屬性（用於管理員檢視）以及中繼資料表單（用於Assets檢視）。 您可以相應地修改提示，以搜尋這些自訂資產屬性中可用的值。

>[!NOTE]
>
>若要改善探索效能，請索引相關的自訂中繼資料屬性。 當使用者在提示中包含這些屬性時，索引屬性可讓代理程式更快地擷取相符內容。


範例提示：

* **根據標籤搜尋**：在資料夾`office`中顯示標籤了`WKND`的影像。
* **根據檔案格式、資產型別、資產狀態和「已依電子郵件ID發佈」進行搜尋**：以`.PNG`格式顯示`approved`和`published by <user email ID>`的影像。
* **根據檔案格式、資產型別、資產狀態和[由電子郵件ID建立]進行搜尋**：以`.mp4`格式顯示已核准和`created by <user email ID>`的視訊。
* **根據檔案格式、資產型別、資產狀態和建立日期進行搜尋**：以`.PNG`格式顯示2025年1月1日和`published by <user email ID>`之後建立的影像
* **依據MIME型別、建立日期及依電子郵件ID發佈**&#x200B;搜尋：在`image/jpeg`與`January 1, 2025`之後建立的節目`published by <user email ID>`。
* **根據檔案格式和自訂中繼資料屬性搜尋**：以`.JPEG`格式顯示具有`Product SKU ID as <SKU value>`的影像。

* **搜尋遺失中繼資料的資產**：顯示過去90天內建立的具有`<Name of metadata property including custom properties>`的資產為空白。

* **使用檔案大小、影像寬度和影像高度來搜尋資產**：顯示寬度大於2000畫素且高度大於1200畫素且大於5 MB的影像。


**資料夾式內容探索：**\
內容探索代理程式可透過解譯參考AEM中資料夾名稱的自然語言提示來識別資產。 使用者只需在提示中提及資料夾，無需手動導覽存放庫，即可大幅減少尋找所需內容的點按次數。

範例提示：

* 資料夾`WKND`中是否有任何svg？
* 顯示資料夾`Nov 1 2025`中在`WKND`之後修改的資產。
* 在資料夾`lifestyle`中列出`WKND`影像。

**啟用資料夾式內容探索的其他問題**

當提示中包含資料夾名稱（沒有完整資產路徑）時，內容探索代理程式會先檢查根路徑`/content/dam/<folder-name>`的相符資料夾。

如果在根層級找不到相符的資料夾，代理程式會建議存放庫中存在指定資料夾名稱的替代資料夾路徑。 這可幫助使用者快速識別正確的位置，而無需手動瀏覽資料夾結構。

例如，找不到路徑`/content/dam/<folder-name>`。 您是說這些嗎？

* 選項1

* 選項2

**以格式為基礎的資產探索**

內容探索代理程式可識別符合特定品質要求的資產（例如檔案格式），讓使用者快速找到產品視覺效果，以利跨管道進行高品質的傳送和重複使用。

範例提示：

尋找產品封裝PNG影像。

**方向型內容探索**

內容探索代理程式可以辨識視覺屬性（例如出現的人和影像的方向）來篩選資產。 這可讓使用者快速將內容縮小至最相關的視覺效果，而不需在AEM中手動套用多個篩選器。

範例提示：

以橫向顯示個人資產。

**正在展開搜尋結果**

內容探索代理程式會針對提示傳回每個內容型別的前20個最相關結果。 如果有其他相符結果，使用者可以輸入後續提示（例如`show me more`）來要求下一個集合。 接著，代理程式會從原始搜尋中擷取下一組結果，讓使用者能逐步探索較大的結果集，而不會縮小提示字元。

**正在尋找類似的資產**

內容探索代理程式可讓使用者尋找與搜尋結果中傳回的特定結果類似的資產。 在代理程式顯示提示的前幾個結果後，您可以透過參考結果清單中專案的位置來請求類似的資產。 例如，`find assets similar to the 3rd result`之類的提示會指示代理程式識別並傳回與該專案相關的其他相關資產。 這可幫助使用者快速探索相關內容，而無需建立新的搜尋提示。

**排序搜尋結果**

內容探索代理程式可讓使用者直接在其自然語言提示中排序搜尋結果。 使用者可以指定排序條件，例如修改日期、建立日期或資產名稱，並選擇遞增或遞減順序。

範例提示：

* 查詢按修改日期降序排序的山地影像（首先顯示最近修改的資產）。

* 顯示依名稱遞增順序排序的山地影像（顯示以字母A開頭後接B的影像名稱，依此類推）。

### AEM Sites頁面 {#content-discovery-agent-aem-sites-pages}

內容探索代理程式可解譯參考頁面主題、行銷活動或其他內容關鍵字的自然語言提示，協助使用者快速找到相關的AEM Sites頁面。 代理程式會根據提示中的關鍵字執行全文檢索搜尋，以識別AEM存放庫中的相符頁面，而不需要手動瀏覽Sites結構。

範例提示：

* 尋找夏季行銷活動的所有AEM Sites頁面。

* 尋找包含咖啡主題的AEM Sites頁面。

### 內容片段 {#discovery-agent-use-cases-content-fragments}

內容探索代理程式會解譯促銷活動名稱、產品品牌、出版物狀態和最近建立活動的自然語言參考，協助使用者快速找到正確的內容片段。 它可讓團隊呈現行銷活動就緒的片段並檢視品牌專屬內容，完全無須手動瀏覽資料夾或在AEM中套用多個篩選器。

範例提示：

* 顯示建立WKND選件行銷活動的內容片段。

* 顯示美式飲料的內容片段。

* 顯示WKND飲料的所有已發佈內容片段。

* 列出過去2週內建立的所有內容片段。

### Forms {#discovery-agent-use-cases-forms}

內容探索代理程式可協助您使用自然語言提示快速找到最適化表單。 它會搜尋表單內容和中繼資料，以根據提示中的關鍵字尋找相符專案。 這表示即使搜尋字詞不在表單的標題或說明中，您仍可成功探索相關表單。

範例提示：

* 顯示所有貸款申請表單。
* 尋找要套用至代理程式的表單。
* 尋找聯絡表單。
* 我正在尋找員工入職表格。
* 顯示信用卡申請表單。

注意：表單探索目前僅支援Edge Delivery Services表單，且標籤式搜尋目前不適用於表單。

## 搜尋結果 {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

內容探索代理程式會傳回每個查詢的前幾個結果（依相關性排序），以確保首先出現完全相符的內容。 代理程式結合中繼資料導向的查詢與語意搜尋，以組合可能符合的重點集合，然後使用LLM根據使用者意圖來排名。 這種混合式方法可提供精確的內容感知結果，而不完全取決於直接的關鍵字比對。

每個結果都包含資產名稱以及重要的資產中繼資料，例如資產路徑、建立者、建立日期、標題、說明、格式、上次修改者、上次修改日期、檔案大小、維度、[動態媒體URL](/help/assets/dynamic-media/dynamic-media.md)和相關標籤。 如果資產處於已核准狀態，結果也會包含具有OpenAPI URL的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)。

您可以按一下資產路徑，順暢地導覽至AEM內的資產位置。

![使用內容探索代理程式搜尋資產](/help/ai-in-aem/agents/content-advisor/assets/search-results-discovery-agent.png)

您可以使用這些資產詳細資料快速評估資產是否符合要求，而無需瀏覽至每個資產以檢視這些詳細資訊。

>[!NOTE]
>
>[Dynamic Media URL](/help/assets/dynamic-media/dynamic-media.md)欄位只有在資產已發佈且您具備有效的Dynamic Media授權時，才會顯示在搜尋結果中。 同樣地，只有當您具備有效的Dynamic Media授權且您的AEM as a Cloud Service執行個體已啟用具有OpenAPI的Dynamic Media時，才會顯示[具有OpenAPI URL的Dynamic Media &#x200B;](/help/assets/dynamic-media-open-apis-overview.md)欄位。

### 內容片段 {#discovery-agent-search-results-content-fragments}

內容探索代理程式提供內容片段的全文檢索搜尋功能，傳回最符合指定提示的前幾個結果。 每個結果都包含內容片段名稱以及關鍵中繼資料欄位，例如內容片段路徑、建立者、建立日期、變數、上次修飾詞和上次修改日期欄位。

![使用內容探索代理程式搜尋內容片段](/help/ai-in-aem/agents/content-advisor/assets/search-content-fragments-discovery-agent.png)

您可以按一下內容片段路徑，順暢地導覽至AEM中的內容片段位置。

## 提示最佳實務 {#prompting-best-practices-discovery-agent}

以您的自然語言提示指定簡明的詳細資料，讓代理程式可以傳回正確且相關的結果。 您越清楚描述所要尋找的內容，代理程式就越能精簡及縮小輸出。 例如，您可以：

* 在篩選資產的提示中定義資產中繼資料，例如標籤、資料夾名稱、建立日期、發佈狀態、作者名稱。

* 使用您組織的特定中繼資料，例如，類別（跑鞋、電子產品）、季節（秋季、春季）、活動（黑色星期五、產品上市）和頻道（網路、電子郵件、列印），以進一步篩選內容。

## 限制 {#limitations-discovery-agent}

* 內容探索代理程式僅支援影像和SVG格式型別的維度提示。 例如，`Find images wider than 1080px`。

* Content Hub管理員可以使用Content Hub入口網站存取內容探索代理程式，但結果只會從AEM作者執行個體擷取。 Content Hub有限的使用者目前無法取得內容探索代理程式的好處（即將推出）。

* 尋找類似功能僅適用於具有[智慧標籤增強功能](/help/assets/ai-generated-metadata-assets-view.md)的影像。
