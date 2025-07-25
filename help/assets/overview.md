---
title: 介紹AEM中適用於數位資產管理的Assets as a Cloud Service
description: 介紹AEM中適用於數位資產管理的Assets as a Cloud Service
source-git-commit: 707c2125b3a5401cd5b0ebe19f3bc9c46302b697
workflow-type: tm+mt
source-wordcount: '5032'
ht-degree: 29%

---


# 介紹AEM中適用於數位資產管理的Assets as a Cloud Service {#assets-as-cloud-service-digital-asset-management-aem}

Adobe Experience Manager Assets as a Cloud Service 為企業提供一種雲端原生的 PaaS 解決方案，不僅可以快速有效地執行數位資產管理和動態媒體操作，而且還使用始終最新、可用且不斷學習之系統的下一代智慧功能 (例如 AI/ML)。

Adobe 為您提供健全的數位資產管理 (DAM) 解決方案，可供您善加利用您的數位資產。Adobe Experience Manager Assets有兩個不同的體驗，使用相同的雲端服務存放庫來符合您的需求。 如需AEM Assets以角色為基礎的體驗相關資訊，請參閱[數位資產管理可用的角色型體驗](#persona-based-experiences)。

如需AEM Assets Ultimate和AEM Assets Prime產品的相關資訊，請參閱[Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md)和[Assets as a Cloud Service Prime](/help/assets/assets-prime.md)。

Adobe數位資產管理的一些主要功能包括：

![新增標記](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB 資產擷取]

## 資產擷取 {#asset-ingestion}

使用大量匯入功能，將大量資產直接從資料來源(例如Azure、AWS、Google Cloud、Dropbox和OneDrive)匯入Assets as a Cloud Service。

您可以使用管理員檢視或Assets檢視來執行大量匯入操作。 相較於管理員檢視，Assets檢視可提供更多資料來源選項。

除了網頁瀏覽器使用者介面外，Experience Manager也支援案頭上的其他使用者端。 它們也提供上傳體驗，無需前往網頁瀏覽器。

* Adobe Asset Link可讓您在Adobe Photoshop、Adobe Illustrator和Adobe InDesign案頭應用程式中，從Experience Manager存取資產。 您可以從這些案頭應用程式內，直接從Experience Manager Asset Link使用者介面將目前開啟的檔案上傳到Adobe。

* Experience Manager案頭應用程式可簡化在案頭使用資產的工作，不受其檔案型別或處理資產的原生應用程式影響。 從本機檔案系統上傳巢狀資料夾階層的檔案會很有用，因為瀏覽器上傳僅支援上傳一般檔案清單。

使用這些連結來存取有關這些資產擷取工具的詳細檔案：

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="大量匯入工具" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong>使用大量匯入工具</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何直接從資料來源匯入大量資產</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/using">
   <img alt="使用AEM案頭應用程式" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/using">
      <strong>使用AEM案頭應用程式</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用AEM案頭應用程式，從您的本機檔案系統上傳巢狀資料夾階層的檔案。</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html">
   <img alt="使用 Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html">
      <strong>使用Adobe資產連結</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用Creative Cloud應用程式將資產上傳到Experience Manager。</em>
   </p>
</td>
</table>

>[!TAB AI支援的功能]

**智慧標籤**：智慧標籤會使用Adobe Sensei的人工智慧架構，根據您的標籤結構和商業分類訓練其影像辨識演演算法。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 依預設，AEM會自動將智慧標籤套用至已上傳的資產。

**智慧型色彩標籤與搜尋**： AEM Assets使用Adobe Sensei AI功能來區分影像中的顏色，並在擷取時自動將這些差異套用為標籤。 這些標籤會根據影像顏色組合來增強搜尋體驗。

**AI產生的中繼資料**： AEM Assets會使用AI來自動產生中繼資料，包括標題、說明和關鍵字。 這些 AI 產生的欄位能提升中繼資料準確性，讓資產更易於搜尋、分類和推薦。此方法不僅能藉由除去手動標記過程提升效率，還能確保大量數位內容的一致性和擴充性。

**AI支援的資產大量重新命名**： [Assets檢視可讓您使用人工智慧一次重新命名多個資產](/help/assets/bulk-rename-assets-view.md)。 您可以一次選取多個檔案並將它們重新命名在一起。 某些對話式重新命名提示範例包含&#x200B;*將所有檔案變更為&#39;my-file&#39;，並附加遞增數字*&#x200B;和&#x200B;*以001、002等為檔案加上前置詞。 並翻譯成英文*。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets中的智慧標籤" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>將AI智慧標籤新增至資產</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何自動將智慧標籤套用至上傳的資產。</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="新增智慧型色彩標籤" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>新增Intelligent色彩標籤</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何在擷取時自動套用顏色標籤。</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="AI產生的中繼資料" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>AI產生的中繼資料</strong>
      </a>
   </div>
   <p>
      <em>使用AI產生資產中繼資料，例如標題和說明。</em>
   </p>
</td>
</table>

**內容搜尋**： AEM Assets可讓您定義文字提示，以搜尋存放庫中的可用資產。 Experience Manager Assets 會自動轉換這些文字提示，以便搜尋篩選器並顯示搜尋結果。您可以使用「篩選窗格」來檢視及修改自動篩選，以進一步縮小搜尋結果的範圍。 某些對話式文字提示範例包括&#x200B;*高度至少為200px、寬度為100px的影像，搭配沙灘和晴朗的天空*&#x200B;和&#x200B;*我需要高度為1500和2500畫素的藍天影像，而且是在過去一個月內建立的，但是尚未過期且已核准*。

**在AEM中使用Adobe Firefly產生資產**：如果您的搜尋查詢未傳回任何結果，AEM Assets可讓您即時使用Adobe Firefly產生資產。 AEM Assets也可讓您將產生的影像從AEM Assets使用者介面上傳至AEM Assets存放庫。

**與Adobe Express整合**： AEM Assets與Adobe Express原生整合，可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。 您也可以在Express中使用Adobe Firefly Artifical Intelligence，使用簡單的文字提示來產生影像，並將它們置於Express畫布上。 然後，您就可以將新的或編輯過的內容儲存在AEM Assets存放庫中。

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="內容相關搜尋" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong>內容搜尋</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用簡單文字提示搜尋資產。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="使用Adobe Firefly產生資產" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>使用Adobe Firefly產生資產</strong>
      </a>
   </div>
   <p>
      <em>使用Adobe Firefly即時產生資產。</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="與 Adobe Express 整合" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>與Adobe Express整合</strong>
      </a>
   </div>
   <p>
      <em>在AEM Assets使用者介面中使用Adobe Express AI功能。</em>
   </p>
</td>
</table>

**智慧型影像**：智慧型影像可根據客戶的瀏覽器功能自動最佳化影像的格式和檔案大小，以提供更優異的影像資產傳遞效能。 它可搭配您現有的影像預設集使用，並在傳送時使用智慧。 此智慧功能可依據瀏覽器和網路連線速度，進一步縮小影像檔案大小。

**智慧型裁切**： Adobe Sensei AI功能，可自動偵測任何影像或視訊中的焦點，並裁切以維持焦點。 不論熒幕大小如何，都能擷取到預期的興趣點，因此省去了繁瑣的手動工作，並提供在任何裝置或熒幕上看起來都不錯的高品質、快速載入影像和視訊。

**AI產生的視訊標題**： Adobe Dynamic Media中AI產生的視訊標題，會使用人工智慧來自動產生視訊內容的標題。 透過提供準確的字幕，這項功能可改善輔助工具的效能並增強使用者體驗。註解產生自原始音訊、任何其他音軌或視訊屬性頁面的`Captions and Audio`索引標籤中提供額外的註解。 您可以在影片發佈之前審查及預覽字幕，其支援超過 60 種語言。
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="智慧型影像" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>智慧型影像處理</strong>
      </a>
   </div>
   <p>
      <em>根據使用者的瀏覽器功能和網路速度，最佳化影像的格式和檔案大小。</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
   <img alt="智慧型裁切" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
      <strong>智慧型裁切</strong>
      </a>
   </div>
   <p>
      <em>使用AI自動偵測任何影像或視訊中的焦點，並裁切以維持焦點</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="AI產生的視訊註解" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>AI產生的視訊字幕</strong>
      </a>
   </div>
   <p>
      <em>使用人工智慧為視訊內容自動產生字幕。</em>
   </p>
</td>
</table>

>[!TAB 資產探索]

## 資產探索 {#asset-discovery}

將資產匯入AEM Assets後，要從如此龐大的收藏集中快速找到合適的資產就成了挑戰。

AEM Assets提供的功能可協助您快速找到正確的資產，例如AI產生的標籤（智慧標籤）、自訂中繼資料，以及可提升搜尋體驗的功能。

**中繼資料管理**：中繼資料是開始您的資產管理歷程時最重要的方面。 資產分發給使用者後，管理員就完全無法控制管理中繼資料。 有效的資產中繼資料可確保更好的搜尋，這是任何DAM工具的最終目的地。


**中繼資料Forms**： Assets as a Cloud Service預設提供許多標準中繼資料欄位。 如果您有其他中繼資料需求，並需要更多中繼資料欄位來新增特定企業中繼資料。 中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的詳細資訊頁面。特定企業中繼資料能夠改善其資產的控管和探索。您可以從零開始建立表單，或改變現有表單的用途。

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="管理中繼資料Assets檢視" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>在Assets檢視中管理中繼資料</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用Assets檢視管理中繼資料和中繼資料表單。</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
   <img alt="中繼資料管理最佳實務" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
      <strong>中繼資料管理最佳實務</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何將資產移轉至AEM之前和之後管理中繼資料。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="使用 Adobe Asset Link" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong>在管理員檢視中管理中繼資料</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用管理員檢視管理中繼資料和中繼資料表單。</em>
   </p>
</td>
</table>

**智慧標籤**：智慧標籤會使用Adobe Sensei的人工智慧架構，根據您的標籤結構和商業分類訓練其影像辨識演演算法。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 依預設，AEM會自動將智慧標籤套用至已上傳的資產。

**搜尋資產**：當您擁有適當的中繼資料後，AEM Assets可讓您使用各種運運算元、萬用字元、進階查詢和自訂篩選器來搜尋。

**關聯式搜尋**： AEM Assets也提供關聯式搜尋功能，可讓您定義文字提示，以搜尋存放庫中可用的資產。 Experience Manager Assets 會自動轉換這些文字提示，以便搜尋篩選器並顯示搜尋結果。您可以使用篩選器窗格查看和修改自動篩選器，以進一步縮小搜尋結果範圍。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets中的智慧標籤" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>將智慧標籤新增至資產</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何自動將智慧標籤套用至上傳的資產。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="搜尋Assets檢視" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>在Assets檢視中搜尋資產</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何在Assets檢視中有效使用內容搜尋和其他搜尋功能。</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="搜尋最佳做法" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong>搜尋最佳實務</strong>
      </a>
   </div>
   <p>
      <em>描述各種案例，協助AEM使用者執行從基本到進階層級的搜尋。</em>
   </p>
</td>
</table>

>[!TAB 資產控管]

## 資產管理和治理 {#asset-management-governance}

一旦您將資產上傳到AEM Assets並設定其中繼資料以便更佳地被發現後，您就可以使用Assets檢視的使用者友好介面執行各種數位資產管理任務。

**資產管理工作**：部分基本工作包括搜尋、下載、移動、複製、重新命名、刪除、更新及編輯作業。

您也可以維護資產版本、設定資產狀態及設定資產有效期。

**我的Workspace**： Assets檢視也包含可自訂的工作區，此工作區提供Widget以便您輕鬆存取Assets使用者介面的重要區域以及與您最相關的資訊。 此頁面可用作一站式解決方案，提供工作項目的概觀並讓您快速存取關鍵工作流程。

**Content Credentials**： AEM Assets支援的另一個強大功能是Content Credentials。 各大品牌對於內容透明度、AI揭露以及防止資產竄改的關注度前所未有。 Adobe的Content Authenticity Initiative (CAI)建立的工具符合內容來源與真偽聯盟(C2PA)技術標準。 Content Credentials是一種新型加密的、可顯示竄改的中繼資料，可協助檢視者瞭解內容譜系並確保品牌資產的完整性。 資料中可包含各種來源資料，可將insight納入數位資產的歷史中。

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="資產管理任務" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>資產管理工作</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何執行一些基本和進階資產管理工作。</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="Mt Workspace" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>我的Workspace</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用我的Workspace快速存取Assets使用者介面的關鍵區域。</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Content Credentials</strong>
      </a>
   </div>
   <p>
      <em>深入瞭解使用Content Credentials的數位資產歷史記錄。</em>
   </p>
</td>
</table>

**集合**： AEM Assets也可讓您將資產組織成集合。 收藏集是Adobe Experience Manager Assets檢視中的一組資產、資料夾或其他收藏集。 使用集合在使用者之間共用資產。和檔案夾不同，集合可包含來自不同位置的資產。您可以和使用者共用多個集合。每個集合都包含資產的參考資料。資產的參考完整性會跨越集合來維護。

**通知**： Assets檢視通知可讓您監視對存放庫中可用的資產、資料夾或集合執行的操作。 您需要選取並訂閱將通知傳送給您的內容。您還可以配置通知傳送給您的類別。

**偵測重複的資產**： AEM Assets也支援偵測重複的資產。 如果DAM使用者上傳一個或多個已存在於存放庫中的資產，Experience Manager會偵測重複並通知使用者。



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="管理集合" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>管理集合</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何將您的資產組織成集合，以有效共用資產。</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="設定通知" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>設定通知</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何設定通知以監視對資產、資料夾或集合執行的操作。</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="偵測重複資產" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>偵測重複的資產</strong>
      </a>
   </div>
   <p>
      <em>偵測上傳至AEM Assets的重複資產並通知使用者。</em>
   </p>
</td>
</table>

>[!TAB 整合]

## 與Adobe和非Adobe應用程式整合 {#integration-adobe-non-adode-apps}

AEM Assets可與各種Adobe和非Adobe應用程式緊密整合。 以下是可用整合的摘要檢視：

+++**與Adobe和非Adobe應用程式整合**

* **具有OpenAPI功能的Dynamic Media**： [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)提供一組完整的[搜尋](/help/assets/search-assets-api.md)和[傳遞](/help/assets/deliver-assets-apis.md) API。 它可讓您的開發人員輕鬆將資產傳送與其應用程式整合。 這些應用程式包括 Adobe 以及第三方應用程式。它提供Micro Frontend資產選擇器使用者介面，用於搜尋和選取已核准的資產。 選擇器可以輕鬆地與任何採用 JavaScript 框架 (例如 React JS、Angular JS，和 Vanilla JS) 的應用程式整合。

* **Micro-Frontend Asset Selector**： Micro-Frontend Asset Selector提供使用者介面，可輕鬆與Experience Manager Assets存放庫整合，因此您可以瀏覽或搜尋存放庫中可用的數位資產，並在您的應用程式編寫體驗中使用這些資產。
您可以整合Asset Selector與Adobe或非Adobe應用程式。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有OpenAPI功能的Dynamic Media概觀" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有OpenAPI功能的Dynamic Media概述</strong>
      </a>
   </div>
   <p>
      <em>瞭解主要優點，以及如何啟用它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制存取 Experience Manager 中的資產" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制存取 Experience Manager 中的資產</strong>
      </a>
   </div>
   <p>
      <em>設定角色以限制對已核准資產的存取。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="資產選擇器" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>微前端資產選擇器</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何將Micro-Frontend Asset Selector與Adobe或非Adobe應用程式整合。</em>
   </p>
</td>
</table>

+++

+++**與Adobe應用程式的原生整合**

* **與Adobe Workfront整合**： [!DNL Adobe Workfront]是工作管理應用程式，可協助您在一個地方管理整個工作生命週期。 [!DNL Workfront]與[!DNL Adobe Experience Manager Assets]之間的整合可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

  Adobe提供給[整合 [!DNL Workfront] 與 [!DNL Adobe Experience Manager Assets] 原生](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html)。

* **與Figma整合**： AEM Assets與Figma原生整合，可讓設計人員從Figma使用者介面直接存取AEM Assets中儲存的資產。 您可以將 AEM Assets 內所管理的內容放置於 Figma 畫布中，然後將新的或編輯後的內容儲存在 AEM Assets 存放庫中。若要存取 Figma 社群頁面上提供的 AEM Assets 連接器，請按一下[此處](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)。

* **與Adobe Express的原生整合**： AEM Assets與Adobe Express原生整合，可讓您從Adobe Express使用者介面直接存取AEM Assets中儲存的資產。 您可以將 AEM Assets 中管理的內容放置在 Express 畫布中，然後將新的或編輯的內容儲存在 AEM Assets 存放庫中。

* **將AEM Assets連線至Creative Cloud**： Experience Manager Assets可連線至已布建至其他IMS組織的Creative Cloud權益，以便在AEM Assets中輕鬆使用最新的Creative Cloud整合，包括Express和Creative Cloud Libraries。 如果您的 Creative Cloud 產品和 AEM Assets 佈建給單獨的 IMS 組織，您可以連接到不同的 Creative Cloud 組織，以便能夠在兩個解決方案之間執行整合工作流程。

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="與 Adobe Workfront 整合" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>與Adobe Workfront整合</strong>
      </a>
   </div>
   <p>
      <em>與Adobe Workfront整合，在一個地方管理整個工作生命週期。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="與 Figma 整合" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>與Figma整合</strong>
      </a>
   </div>
   <p>
      <em>從Figma使用者介面存取儲存在AEM Assets中的資產</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="與Adobe Express的原生整合" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>與Adobe Express的原生整合</strong>
      </a>
   </div>
   <p>
      <em>將AEM Assets中可用的資產置於Express畫布上，並將更新的資產儲存至AEM。</em>
   </p>
</td>


</table>


* **與Adobe Journey Optimizer整合**：使用Adobe Experience Manager Assets將行銷和創意工作流程結合在一起。 與Adobe Journey Optimizer原生整合，存取Assets as a Cloud Service以儲存、管理、探索和散發數位資產。 它提供單一、集中的資產存放庫，供您用來填入訊息。

* **與Commerce整合**：適用於Commerce的Adobe Experience Manager (AEM) Assets整合結合了AEM as a Digital Asset Management (DAM)系統與Adobe Commerce的強大功能，以強化電子商務體驗。 這些功能是透過將Commerce專案連線到AEM強大的資產管理環境來提供，以提供一種無縫、可擴充且有效率的方式，來跨商業商店管理和提供資產。
* **整合AEM Assets與Edge Delivery Services的檔案式製作流程**：當[!DNL AEM Assets]與檔案式製作工具（例如[!DNL Microsoft Word]或[!DNL Google Docs]）整合時，它會在您的製作工具中提供資產選擇器。 使用此資產選擇器來存取[!DNL AEM Assets]，並將核准的資產插入您的內容。
如果您已有[!DNL Edge Delivery Services]網站，請參閱[[!DNL AEM Assets] 外掛程式](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)檔案，以瞭解如何將[!DNL AEM Assets]與您現有的[!DNL AEM]專案整合。

* **整合[!DNL AEM Assets]與[!DNL Universal Editor]的[!DNL Edge Delivery Services]**&#x200B;式編寫流程：設定[!DNL Universal Editor]與[!DNL AEM Assets]整合。 此整合可讓您使用[!DNL Dynamic Media with OpenAPI capabilities]傳遞資產。

   * 檢視[網站 [!DNL Edge Delivery] 中的](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)設定，瞭解如何在[!DNL Universal Editor]中新增自訂資產選擇器函式。 自訂資產選擇器可讓您將資產直接插入到[!DNL Universal Editor]內容。
   * 請參閱[擴充功能概觀](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)以瞭解如何在[!DNL AEM Assets]中撰寫時存取[!DNL Universal Editor]和插入資產。

<table>
<td>
   <a href="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="與 Adobe Journey Optimizer 整合" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>與Adobe Journey Optimizer整合</strong>
      </a>
   </div>
   <p>
      <em>使用與AJO的整合，將行銷和創意工作流程結合在一起</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
   <img alt="與Commerce整合" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
      <strong>與Commerce整合</strong>
      </a>
   </div>
   <p>
      <em>整合AEM Assets與Commerce以強化電子商務體驗。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="將AEM Assets與EDS整合" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>整合AEM Assets與EDS</strong>
      </a>
   </div>
   <p>
      <em>整合AEM Assets與檔案式及通用編輯器式撰寫流程。</em>
   </p>
</td>
</table>

+++

>[!TAB 資產啟用]

## 資產啟用 {#asset-activation}

使用Content Hub轉Dynamic Media （包括強大的OpenAPI功能），讓AEM Assets充分發揮數位資產的潛力。 AEM Assets提供全方位的解決方案套件，專門簡化資產轉換並最佳化各種管道的傳送。

+++**Content Hub**

Content Hub 作為 Experience Manager Assets as a Cloud Service 的一部分提供，以實現組織及其業務合作夥伴對品牌內容的大眾化存取。其專注於分配資產以進行大規模啟用，並建立品牌內容變體來提高行銷靈敏度。

Content Hub 提供以下主要優勢：

* **尋找並共用直覺式入口網站中可用的所有品牌核准資產**： AEM Assets可作為單一信任來源，而所有核准的資產都會以平面階層自動在Content Hub上使用，以改善搜尋體驗。

* **可設定的使用者介面**： Content Hub中最常見的屬性，例如搜尋篩選器、新增或匯入資產時可用的欄位、資產屬性、品牌化的橫幅內容，都是可設定的，管理員可依需求輕鬆設定Content Hub使用者介面。

* **讓非創意人員編輯與重新混合內容，同時保留品牌**： Content Hub可讓您使用Adobe Express建立新內容(如果您有Adobe Express許可權)。 您可以使用易於使用的工具來編輯現有內容、使用範本和品牌元素製作品牌變化版本，並使用 Adobe Firefly 的最新 GenAI 功能來建立新內容。

* **深入瞭解跨團隊如何使用內容**： [!DNL Content Hub]提供寶貴的資產深入分析，解決行銷利害關係人經常遇到的共同挑戰 — 行銷活動、管道和不同區域中使用的資產使用統計資料。 透過清楚地了解資產的效能和受歡迎程度，可以提供對於增強使用者體驗來說相當重要的可操作分析。

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Content Hub 概觀" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>Content Hub概觀</strong>
      </a>
   </div>
   <p>
      <em>進一步瞭解Content Hub、其主要優點，以及如何存取它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="設定Content Hub使用者介面" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>設定Content Hub使用者介面</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何設定Content Hub使用者介面上的可用選項。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用Adobe Express編輯" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用Adobe Express編輯</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用Adobe Express在Content Hub中編輯影像。</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

Dynamic Media可協助您隨選提供豐富的視覺化銷售和行銷資產。 此外，也能協助您建立及提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 您的資產會動態調整規模，以因應網頁、行動裝置和社交網站上的使用量。 使用影像、視訊和3D等一組主要來源資產，Dynamic Media會透過其全球性、可擴充、效能最佳化的CDN （內容傳遞網路），即時產生並傳遞這種豐富內容的多種變數。

Dynamic Media提供下列主要功能：

* **智慧型影像**：智慧型影像可根據客戶的瀏覽器功能自動最佳化影像的格式和檔案大小，以提供更優異的影像資產傳遞效能。 它可搭配您現有的影像預設集使用，並在傳送時使用智慧。 此智慧功能可依據瀏覽器和網路連線速度，進一步縮小影像檔案大小。

* **最適化視訊集**：最適化視訊集會將以不同位元速率和格式編碼的相同視訊版本分組。 您先從您上傳到系統中的原始主要視訊開始。 Dynamic Media會自動調整視訊大小，或將其轉碼為多個視訊。 然後，在傳送時，它會聰明地決定要使用的視訊畫面、品質和格式，並將它傳送到手機、平板電腦或桌上型電腦。

* **智慧型裁切**： Adobe Sensei AI功能，可自動偵測任何影像或視訊中的焦點，並裁切以維持焦點。 不論熒幕大小如何，都能擷取到預期的興趣點，因此省去了繁瑣的手動工作，並提供在任何裝置或熒幕上看起來都不錯的高品質、快速載入影像和視訊。

* **Dynamic Media範本**：使用Dynamic Media範本、WYSIWYG範本編輯器，為您的橫幅和傳單建立即時可自訂的範本。 發佈您的Dynamic Media範本，並用於下游應用程式。 Dynamic Media範本包含影像和文字圖層。 為範本的影像和文字圖層新增引數，並使用Dynamic Media URL來重新定位和調整圖層大小，以及即時更新其內容。

* **多重音訊和註解**：新增多重註解和多重音訊曲目到主要視訊。 擁有此功能代表全球觀眾都可以存取您的影片。您可以著手自訂一部已發佈的主要影片，以多種語言提供給全球觀眾，並遵守不同地理區域的無障礙指南。此外，作者還可以透過使用者介面的單一標籤管理字幕和音軌。

* **透過HTTP (DASH)支援動態自我調整資料流**： Dynamic Media支援Dynamic Media視訊傳送中的自我調整資料流（已啟用CMAF），這可確保使用者獲得更理想的視訊檢視體驗。 DASH是適用於最適化視訊串流的國際標準通訊協定，在業界被廣泛採用。

* **AI產生的視訊標題**： Adobe Dynamic Media中AI產生的視訊標題，會使用人工智慧來自動產生視訊內容的標題。 您可以在影片發佈之前審查及預覽字幕，其支援超過 60 種語言。

如需可用Dynamic Media產品的詳細資訊，請參閱[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="使用 Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>使用Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何傳遞資產，以便在網頁、行動裝置和社交網站上使用。</em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Dynamic Media歷程" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Dynamic Media歷程</strong>
      </a>
   </div>
   <p>
      <em>瞭解Dynamic Media如何為您的工作帶來價值。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="將 AEM Assets 連接到 Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Dynamic Media最佳作法</strong>
      </a>
   </div>
   <p>
      <em>使用影像、影片和檢視器時的最佳實務。</em>
   </p>
</td>
</table>

+++

+++**具有 OpenAPI 功能的 Dynamic Media**

在現今步調迅速的數位世界中，為了在競爭中保持領先，發揮品牌數位資產的全部潛力至關重要。整體數位資產管理 (DAM) 解決方案能促進資產控管、提升品牌一致性，並加速內容傳遞，同時確保品牌完整性和卓越的客戶體驗。

具有 OpenAPI 功能的 Dynamic Media 將 DAM 置於敏捷且高效之內容供應鏈生態系統的核心處，藉此確保資產控管和傳遞。

具有OpenAPI功能的Dynamic Media提供下列主要優點：

* **緊密整合**：具有 OpenAPI 功能的 Dynamic Media 提供一套全面的搜尋和傳遞 API。它可以讓您的開發人員輕鬆地[將資產傳遞與其應用程式進行整合](/help/assets/integrate-dynamic-media-open-apis.md)。這些應用程式包括 Adobe 以及第三方應用程式。它提供了一個[微前端資產選擇器使用者介面](/help/assets/overview-asset-selector.md)，用來搜尋和選取已核准的資產。選擇器可以輕鬆地與任何採用 JavaScript 框架 (例如 React JS、Angular JS，和 Vanilla JS) 的應用程式整合。

* **集中管理數位資產**：DAM 是所有數位資產的單一事實來源。您的數位資產會在 AEM Assets 集中管理，並透過使用傳遞 URL 參照來傳遞至取用的應用程式，無需複製資產二進位檔案。

* **即時更新**：對 DAM 中已核准資產所做的任何變更 (包括版本更新和中繼資料修改)，都會自動反映在傳遞 URL 中。透過內容傳遞網路為具有 OpenAPI 功能的 Dynamic Media 設定 10 分鐘的短存留時間 (TTL) 值，更新就會在 10 分鐘內顯示於所有製作中和已發佈的介面中。

* **品牌一致性**：唯有[品牌核准的資產](/help/assets/approve-assets.md)才會顯示在下游應用程式中。[品牌經理和行銷人員會對品牌資產維持嚴格控制](/help/assets/restrict-assets-delivery.md)。唯有經核准且最新版本的資產才可供使用，以確保所有管道和應用程式間的品牌一致性。

* **網路最佳化的傳遞**：數位資產以網路最佳化的格式傳遞，以增強您數位體驗的核心頁面指標。這包括支援影像的 WebP 轉譯、透過 HLS 或 DASH 通訊協定對影片進行自適應串流，以及文件的原始轉譯。

* **動態資產轉換**：我們的系統允許使用稱為影像修飾元的 URL 參數進行即時影像轉換。[例如寬度、高度、旋轉、翻轉、品質、裁切、格式和智慧裁切](/help/assets/deliver-assets-apis.md)。轉換後的轉譯是動態產生，並透過內容傳遞網路順暢傳遞。

* **安全傳遞資產**：具有 OpenAPI 功能的 Dynamic Media 提供機制來控制對您數位資產的存取權。您可以指定使用者角色或群組作為要保護之資產的中繼資料，並設定預先定義的時間範圍，在此期間[只有獲授權的使用者可以存取這些資產](/help/assets/restrict-assets-delivery.md)。在限制的期間內，未經授權的使用者無法解析受保護資產的傳遞 URL。

如需可用Dynamic Media產品的詳細資訊，請參閱[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有OpenAPI功能的Dynamic Media概觀" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有OpenAPI功能的Dynamic Media概述</strong>
      </a>
   </div>
   <p>
      <em>瞭解主要優點，以及如何啟用它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制存取 Experience Manager 中的資產" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制存取 Experience Manager 中的資產</strong>
      </a>
   </div>
   <p>
      <em>設定角色以限制對已核准資產的存取。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="將遠端 AEM Assets 與 AEM Sites 整合" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>將遠端 AEM Assets 與 AEM Sites 整合</strong>
      </a>
   </div>
   <p>
      <em>將遠端AEM Assets與AEM Sites環境整合。</em>
   </p>
</td>
</table>

+++

>[!TAB 深入分析]

## 資產 Insights {#asset-insights}

資產報告可讓管理員檢視Adobe Experience Manager Assets檢視環境的活動。 此資料提供有關使用者如何與內容和產品互動的有用資訊。所有使用者可以存取「深入分析」儀表板，且獲指派至管理員產品設定檔的使用者可以建立使用者定義的報告。

您可以產生各種型別的報表，例如上傳、下載和Dynamic Media傳送。

* **Assets檢視中的深入分析**： Assets檢視可讓您使用深入分析儀表板檢視Assets檢視環境的即時資料。 您可以檢視過去30天或過去12個月的即時事件量度。 事件包括下載、上傳、儲存空間使用情況、熱門搜尋、依大小的資產計數以及依資產型別的資產計數。

* Adobe Analytics **在管理員檢視中整合**： Assets Insights功能可讓您追蹤協力廠商網站、行銷活動及Adobe創意解決方案中所使用影像的使用者評分和使用統計資料。 它有助於提供影像效能和人氣的相關深入分析。 Assets Insights會擷取使用者活動詳細資訊，例如影像分級、點按和曝光次數（影像載入網站上的次數）。 系統會根據這些統計資料，將分數指派給影像。 您可以使用評分和效能統計資料來選取常用影像，以包含在目錄、行銷活動等中。 您甚至可以根據這些統計資料制定封存和授權更新政策。 若要讓Assets Insights顯示資產的使用狀況統計資料，請先設定功能，以從Adobe Analytics擷取報表資料。

* **Content Hub深入分析**： Content Hub提供寶貴的資產深入分析，解決行銷利害關係人經常遇到的共同挑戰 — 行銷活動、管道和各區域使用的資產使用統計資料。 透過清楚地了解資產的效能和受歡迎程度，可以提供對於增強使用者體驗來說相當重要的可操作分析。

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="在資產檢視中管理報告" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>在Assets檢視中管理報告</strong>
      </a>
   </div>
   <p>
      <em>使用Assets檢視取得關鍵成功量度的深入分析。</em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="在「管理員」檢視中管理報表" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>在管理員檢視中管理報告</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何在管理員檢視中管理Adobe Analytics整合式報告。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Content Hub中的Assets深入分析" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      在Content Hub中<strong>Assets深入分析</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何在Content Hub中檢視資產分析。</em>
   </p>
</td>
</table>

>[!ENDTABS]

## 適用於數位資產管理以角色為主的體驗 {#persona-based-experiences}

Adobe 為您提供健全的數位資產管理 (DAM) 解決方案，可供您善加利用您的數位資產。Adobe Experience Manager Assets 具有兩種使用同一雲端服務存放庫的獨立體驗：

* **管理員檢視**：現有的 Assets as a Cloud Service 使用者介面。使用管理視圖來實現所有高階數位資產管理功能，包括整合、工作流程、內容自動化、發布等。

* **資產檢視**：Adobe 的輕量型資產管理體驗，可儲存、管理、探索和使用數位資產。簡化的使用者介面包含基本的數位資產管理功能。專為輕量型 DAM 使用者設計，重點在上傳、中繼資料管理、搜尋、下載和共享。

![新增標記](assets/newui-overview.svg)

可存取管理員檢視的使用者也可以存取資產檢視。資產檢視提供簡化的使用者介面，使您可輕鬆管理、探索和分發數位資產。來自不同職能部門 (包括創意、行銷和業務線團隊) 的廣泛使用者可以進行資產共同作業，並視需要隨時地存取正確的已核准資產。許多臨時 DAM 使用者偏好使用資產檢視，因為它只包含功能的子集。該體驗的目標對象是唯讀創意資產的取用者以及輕量型 DAM 使用者。

DAM 圖書管理員、開發人員和超級使用者可以繼續使用管理員檢視或視需要切換使用者介面。您可以選擇最適合您角色的體驗。

如需了解如何存取資產檢視和管理員檢視帶來的一些簡化操作，請參閱[資產檢視簡介](/help/assets/assets-view-introduction.md)。


