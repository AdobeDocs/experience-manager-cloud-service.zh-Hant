---
title: 設定和使用資產微服務
description: 設定並使用雲端原生資產微服務，以大規模處理資產。
contentOwner: AG
feature: Asset Compute Microservices, Asset Processing, Asset Management
role: Architect, Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '2891'
ht-degree: 2%

---

# 使用資產微服務和處理設定檔 {#get-started-using-asset-microservices}

資產微服務可使用雲端原生應用程式（也稱為背景工作），提供可擴充及彈性的資產處理功能。 Adobe會管理服務，以最佳化方式處理不同的資產型別和處理選項。

資產微服務可讓您處理[多種檔案型別](/help/assets/file-format-support.md)，涵蓋比舊版[!DNL Experience Manager]更多的現成格式。 例如，現在可以擷取PSD和PSB格式的縮圖，但先前需要協力廠商解決方案，例如[!DNL ImageMagick]。

資產處理依賴於&#x200B;**[!UICONTROL 處理設定檔]**&#x200B;中的組態。 Experience Manager提供基本的預設設定，並可讓管理員新增更具體的資產處理設定。 管理員可建立、維護和修改後處理工作流程的設定，包括可選的自訂。 自訂工作流程可讓開發人員擴充預設供應專案。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高階檢視](assets/asset-microservices-flow.png "資產處理的高階檢視")

>[!NOTE]
>
>此處說明的資產處理會取代舊版[!DNL Experience Manager]中的`DAM Update Asset`工作流程模型。 資產微服務處理會取代大部分的標準轉譯產生和中繼資料相關步驟，而後續處理工作流程設定可以取代剩餘步驟（如有）。

## 瞭解資產處理選項 {#get-started}

[!DNL Experience Manager]允許下列處理層級。

| 選項 | 說明 | 涵蓋的使用案例 |
|---|---|---|
| [預設組態](#default-config) | 目前可用，且無法修改。 此設定提供基本轉譯產生功能。 | <ul> <li>[!DNL Assets]使用者介面（48、140和319畫素）使用的標準縮圖 </li> <li> 大型預覽（Web轉譯 — 1280畫素） </li><li> 中繼資料和文字擷取。</li></ul> |
| [自訂組態](#standard-config) | 由管理員透過使用者介面進行設定。 透過擴充預設選項，為產生轉譯提供更多選項。 擴充現成可用的選項，以提供不同的格式和轉譯。 | <ul><li>FPO （僅供刊登）轉譯。 </li> <li>變更檔案格式和影像解析度</li> <li> 有條件地套用至已設定的檔案型別。 </li> </ul> |
| [自訂設定檔](#custom-config) | 管理員透過使用者介面設定為透過自訂應用程式使用自訂程式碼來呼叫[Asset Compute服務](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/introduction)。 以雲端原生且可擴充的方法支援更複雜的需求。 | 請參閱[允許的使用案例](#custom-config)。 |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支援的檔案格式 {#supported-file-formats}

資產微服務可支援多種檔案格式，以處理、產生轉譯或擷取中繼資料。 如需MIME型別的完整清單和每種型別支援的功能，請參閱[支援的檔案格式](file-format-support.md)。

## 預設設定 {#default-config}

已預先設定部分預設值，以確保Experience Manager中所需的預設轉譯可供使用。 預設設定也可確保中繼資料擷取和文字擷取作業可供使用。 使用者可以立即開始上傳或更新資產，並且預設提供基本處理功能。

使用預設設定時，只會設定最基本的處理設定檔。 使用者介面上看不到此類處理設定檔，且您無法對其進行修改。 它一律會執行以處理上傳的資產。 此類預設處理設定檔可確保[!DNL Experience Manager]所需的基本處理在所有資產上完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準設定 {#standard-config}

[!DNL Experience Manager]提供依據使用者需求，為一般格式產生更特定轉譯的功能。 管理員可以建立其他[!UICONTROL 處理設定檔]，以方便建立這類轉譯。 然後，使用者將一個或多個可用的設定檔指派給特定資料夾，以完成其他處理。 舉例來說，其他處理作業可產生網頁、行動裝置和平板電腦的轉譯。 下列影片說明如何建立和套用[!UICONTROL 處理設定檔]，以及如何存取建立的轉譯。

* **轉譯寬度和高度**：轉譯寬度和高度規格提供產生之輸出影像的大小上限。 資產微服務會嘗試產生最大可能的轉譯，其寬度和高度分別不會大於指定的寬度和高度。 外觀比例會保留，與原始外觀比例相同。 空白值表示資產處理會假設原始資產的畫素尺寸。

* **MIME型別包含規則**：處理具有特定MIME型別的資產時，會先根據轉譯規格的排除MIME型別值檢查MIME型別。 如果符合該清單，則不會為資產（封鎖清單）產生此特定轉譯。 否則，會根據包含的MIME型別檢查MIME型別，如果它符合清單，則會產生轉譯（允許清單）。

* **特殊FPO轉譯**：將來自[!DNL Experience Manager]的大型資產放入[!DNL Adobe InDesign]份檔案時，創意專業人士會在[放置資產](https://helpx.adobe.com/tw/indesign/using/placing-graphics.html)後等待相當長的時間。 同時，使用者被封鎖無法使用[!DNL InDesign]。 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe可暫時將小型轉譯放入[!DNL InDesign]份檔案，稍後可隨選以全解析度資產取代。 [!DNL Experience Manager]提供僅用於放置的轉譯。 這些FPO轉譯的檔案大小較小，但外觀比例相同。

處理設定檔可包含FPO （僅供刊登）轉譯。 請參閱[!DNL Adobe Asset Link] [檔案](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)以瞭解是否需要為您的處理設定檔開啟它。 如需詳細資訊，請參閱[Adobe Asset Link完整檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

### 建立標準設定檔 {#create-standard-profile}

1. 管理員存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]**。 按一下「**[!UICONTROL 建立]**」。
1. 提供可協助您在套用至資料夾時唯一識別設定檔的名稱。
1. 若要產生FPO轉譯，請在&#x200B;**[!UICONTROL 影像]**&#x200B;索引標籤上啟用&#x200B;**[!UICONTROL 建立FPO轉譯]**。 輸入1-100的&#x200B;**[!UICONTROL 品質]**&#x200B;值。
1. 若要產生其他轉譯，請按一下[新增] **&#x200B;**，並提供下列資訊：

   * 每個轉譯的檔案名稱。
   * 每個轉譯的檔案格式(PNG、JPEG、GIF或WebP)。
   * 每個轉譯的寬度和高度（畫素）。 如果未指定值，則會使用原始影像的完整畫素大小。
   * 每個JPEG和WebP轉譯的品質（百分比）。
   * 包含和排除MIME型別以定義設定檔的適用性。

   ![正在處理設定檔 — 新增](assets/processing-profiles-image.png)

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自訂設定檔和使用案例 {#custom-config}

[!DNL Asset Compute Service]支援多種使用案例，包括預設處理和處理Adobe專用格式，例如Photoshop檔案。 它也允許實作自訂或組織特定的處理。 過去所需的DAM更新資產工作流程自訂可自動處理，或透過處理設定檔設定方式處理。 如果這些處理選項不符合您的業務需求，Adobe建議開發並使用[!DNL Asset Compute Service]來擴充預設功能。 如需概觀，請參閱[瞭解擴充功能及使用時機](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/understand-extensibility)。

>[!NOTE]
>
>Adobe建議，只有在無法使用預設設定或標準設定檔滿足業務需求時，才使用自訂應用程式。

它可以將影像、視訊、檔案和其他檔案格式轉換為不同的轉譯，包括縮圖、擷取的文字和中繼資料以及封存。

開發人員可針對支援的使用案例使用[!DNL Asset Compute Service]來[建立自訂應用程式](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/develop-custom-application)。 [!DNL Experience Manager]可以使用管理員設定的自訂設定檔，從使用者介面呼叫這些自訂應用程式。 [!DNL Asset Compute Service]支援以下叫用外部服務的使用案例：

* 使用[!DNL Adobe Photoshop]的[ImageCutout API](https://developer.adobe.com/photoshop/photoshop-api-docs/)並將結果儲存為轉譯。
* 呼叫協力廠商系統以進行變更，例如PIM系統。
* 使用[!DNL Photoshop] API根據Photoshop範本產生各種轉譯。
* 使用[Adobe Lightroom API](https://developer.adobe.com/photoshop/photoshop-api-docs/)將擷取的資產最佳化，並將其儲存為轉譯。

>[!NOTE]
>
>您無法使用自訂應用程式編輯標準中繼資料。 您只能修改自訂中繼資料。

### 建立自訂設定檔 {#create-custom-profile}

1. 管理員存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]** > **[!UICONTROL 建立]**。
1. 在處理設定檔頁面上，按一下&#x200B;**[!UICONTROL 自訂]**&#x200B;標籤，然後按一下&#x200B;**[!UICONTROL 新增]**。
1. 在「名稱」文字欄位中，輸入所需的轉譯檔案名稱，然後提供下列資訊。

   * 每個轉譯的檔案名稱和支援的副檔名。
   * [App Builder自訂應用程式的端點URL](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/deploy-custom-application)。 應用程式必須來自與Experience Manager帳戶相同的組織。
   * 新增服務引數至[傳遞額外的資訊或引數至自訂應用程式](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/develop-custom-application#extend)。
   * 包含和排除MIME型別，以將處理限製為少數特定檔案格式。

1. 在頁面的右上角附近，按一下「儲 **[!UICONTROL 存」]**。

自訂應用程式是Headless [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/)應用程式。 如果您的自訂應用程式已設定處理設定檔，則會取得所有提供的檔案。 應用程式必須篩選檔案。

>[!CAUTION]
>
>如果App Builder應用程式和[!DNL Experience Manager]帳戶並非來自相同組織，則整合無法運作。

### 自訂設定檔的範例 {#custom-profile-example}

為了說明自訂設定檔的使用情況，讓我們考慮使用案例，將一些自訂文字套用至行銷活動影像。 您可以建立使用Photoshop API編輯影像的處理設定檔。

Asset Compute服務整合可讓Experience Manager使用[!UICONTROL 服務引數]欄位將這些引數傳遞給自訂應用程式。 自訂應用程式接著會呼叫Photoshop API，並將這些值傳遞至API。 例如，您可以傳遞字型名稱、文字顏色、文字粗細和文字大小，以將自訂文字新增至行銷活動影像。

<!-- TBD: Check screenshot against the interface. -->

![自訂處理設定檔](assets/custom-processing-profile.png)

*圖：使用[!UICONTROL 服務引數]欄位將新增的資訊傳遞給預先定義的引數建置到自訂應用程式。 在此範例中，當上傳行銷活動影像時，影像會以`Arial-BoldMT`字型中的`Jumanji`文字更新。*

## 使用處理設定檔來處理資產 {#use-profiles}

建立其他自訂處理設定檔並套用至特定資料夾。 此工作流程可讓Experience Manager處理上傳至這些資料夾或更新之資產。 系統會一律執行預設的內建標準處理設定檔，但使用者介面不會顯示設定檔。 如果您新增自訂設定檔，則會使用兩個設定檔來處理上傳的資產。

使用下列其中一種方法，將處理設定檔套用至資料夾：

* 管理員可以在&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 處理設定檔]**&#x200B;中選取處理設定檔定義，並使用&#x200B;**[!UICONTROL 將設定檔套用至資料夾]**&#x200B;動作。 它會開啟內容瀏覽器，讓您導覽至特定資料夾並加以選取，然後確認設定檔的應用程式。
* 使用者可以在Assets使用者介面中選取資料夾，並使用&#x200B;**[!UICONTROL 屬性]**&#x200B;動作開啟資料夾屬性畫面。 在&#x200B;**[!UICONTROL 資產處理]**&#x200B;索引標籤上，他們可以從[!UICONTROL 處理設定檔]清單中為該資料夾選取適當的處理設定檔。 若要儲存變更，請按一下[儲存並關閉]。**&#x200B;**
  ![從[資產屬性]索引標籤](assets/folder-properties-processing-profile.png)將處理設定檔套用至資料夾

* 使用者可以在Assets使用者介面中選取資料夾或特定資產，以套用處理設定檔，然後從上方的可用選項中選取![資產重新處理圖示](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL 重新處理Assets]**&#x200B;選項。

>[!TIP]
>
>一個資料夾只能套用一個處理設定檔。 若要產生更多轉譯，請將更多轉譯定義新增至現有的處理設定檔。

在處理設定檔套用至資料夾後，此資料夾或其任何子資料夾中上傳（或更新）的所有新資產都會使用設定的其他處理設定檔來處理。 此處理是標準預設設定檔的補充。

>[!NOTE]
>
>套用至資料夾的處理設定檔適用於整個樹狀結構，但可以用套用至子資料夾的其他設定檔加以覆寫。 將資產上傳至資料夾時，Experience Manager會檢查所包含資料夾的屬性，以取得處理設定檔。 如果未套用任何設定檔，則會檢查階層中的父資料夾以找出要套用的處理設定檔。

若要確認資產已處理，請在左側邊欄的[!UICONTROL 轉譯]檢視中預覽產生的轉譯。 開啟資產預覽並開啟左側邊欄以存取&#x200B;**[!UICONTROL 轉譯]**&#x200B;檢視。 處理設定檔中的特定轉譯應該可見且可存取，因為其特定資產型別符合MIME型別包含規則。

![其他轉譯](assets/renditions-additional-renditions.png)

*圖：由套用至父資料夾的處理設定檔產生的兩個額外轉譯範例。*

## 後處理工作流程 {#post-processing-workflows}

若需要額外處理資產，而使用處理設定檔無法達成的情況，可以將其他後處理工作流程新增到設定中。 後處理可讓您在使用資產微服務的可設定處理之上新增完全自訂處理。

微服務處理完成後，[!DNL Experience Manager]會自動執行後處理工作流程，或是[自動啟動工作流程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/configuring/auto-start-workflows) （如果已設定）。 不需要手動新增工作流程啟動器來觸發工作流程。 範例包括：

* 處理資產的自訂工作流程步驟。
* 整合以將中繼資料或屬性從外部系統新增至資產，例如產品或程式資訊。
* 其他處理作業由外部服務完成。

若要將後處理工作流程組態新增至[!DNL Experience Manager]，請遵循下列步驟：

* 建立一或多個工作流程模型。 在本檔案中，這些自訂模型稱為&#x200B;*後處理工作流程模型*。 它們是一般[!DNL Experience Manager]工作流程模型。
* 將所需的工作流程步驟新增至這些模型。 檢閱預設工作流程的步驟，並將所有必要的預設步驟新增到自訂工作流程中。 這些步驟會根據工作流程模型設定在資產上執行。 例如，如果您想在資產上傳時自動進行智慧標籤，請將步驟新增至您的自訂後處理工作流程模型。
* 在結尾新增[!UICONTROL DAM更新資產工作流程已完成程式]步驟。 新增此步驟可確保Experience Manager知道處理何時結束，並且資產可標示為已處理，亦即&#x200B;*資產上會顯示新的*。
* 建立「自訂工作流程執行器」服務的設定，可讓您透過路徑（資料夾位置）或規則運算式來設定後處理工作流程模型的執行。

如需後期處理工作流程中可以使用哪些標準工作流程步驟的詳細資訊，請參閱開發人員參考中的後期處理工作流程[&#128279;](developer-reference-material-apis.md#post-processing-workflows-steps)中的工作流程步驟。

### 建立後處理工作流程模型 {#create-post-processing-workflow-models}

後處理工作流程模型是一般[!DNL Experience Manager]工作流程模型。 如果您需要對不同的存放庫位置或資產型別進行不同的處理，請建立不同的模型。

處理步驟會視需要新增。 您既可以使用可用的支援步驟，也可以使用任何自訂實作的工作流程步驟。

確定每個後處理工作流程的最後一步為`DAM Update Asset Workflow Completed Process`。 最後一個步驟是確保Experience Manager在資產處理完成時辨識。

### 設定後處理工作流程執行 {#configure-post-processing-workflow-execution}

資產微服務完成上傳資產的處理之後，您可以定義後處理工作流程以進一步處理資產。 若要使用工作流程模型設定後續處理，您可以執行下列任一項作業：

* [在資料夾「屬性」](#apply-workflow-model-to-folder)中套用工作流程模型。
* [設定自訂工作流程執行器服務](#configure-custom-workflow-runner-service)。

#### 將工作流程模型套用至資料夾 {#apply-workflow-model-to-folder}

對於典型的後續處理使用案例，請考慮使用將工作流程套用至資料夾的方法。 若要在資料夾[!UICONTROL 屬性]中套用工作流程模型，請執行下列步驟：

1. 建立工作流程模型。
1. 選取資料夾，按一下工具列中的&#x200B;**[!UICONTROL 屬性]**，然後按一下&#x200B;**[!UICONTROL Assets處理]**&#x200B;索引標籤。
1. 在&#x200B;**[!UICONTROL 自動啟動工作流程]**&#x200B;下，選取所需的工作流程，提供工作流程的標題，然後儲存變更。

   ![套用後續處理工作流程至其屬性中的資料夾](assets/post-processing-profile-workflow-for-folders.png)

#### 設定自訂工作流程執行器服務 {#configure-custom-workflow-runner-service}

您可以為進階設定設定「自訂工作流程執行器服務」，這些設定無法透過將工作流程套用至資料夾來輕鬆完成。 例如，使用規則運算式的工作流程。 Adobe CQ DAM自訂工作流程執行器(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服務。 它提供下列兩個設定選項：

* 依路徑(`postProcWorkflowsByPath`)的後處理工作流程：可以根據不同的存放庫路徑列出多個工作流程模型。 使用冒號分隔路徑和模型。 支援簡單的存放庫路徑。 將它們對應至`/var`路徑中的工作流程模型。 例如：`/content/dam/my-brand:/var/workflow/models/my-workflow`。
* 依運算式(`postProcWorkflowsByExpression`)後處理工作流程：根據不同的規則運算式，可以列出多個工作流程模型。 使用冒號分隔運算式和模型。 將規則運算式直接指向資產節點，而非轉譯或檔案之一。 例如：`/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`。

若要瞭解如何部署OSGi設定，請參閱[部署至 [!DNL Experience Manager]](/help/implementing/deploying/overview.md)。

#### 停用後處理工作流程執行

不需要後續處理時，請在&#x200B;**自動啟動工作流程**&#x200B;選取範圍中建立並使用「空白」工作流程模型。

##### 建立停用的自動啟動工作流程模型

1. 導覽至&#x200B;**工具** > **工作流程** > **模型**。
1. 按一下頂端動作列中的&#x200B;**建立** > **建立模型**。
1. 提供新工作流程模型的標題和名稱，例如：
   * 標題：停用自動啟動工作流程
   * 名稱： disable-auto-start-workflow
1. 按一下&#x200B;**完成**&#x200B;以建立工作流程模型。
1. 選取並編輯建立的工作流程模型
1. 在工作流程模型編輯器中，按一下模型定義中的&#x200B;**步驟1**&#x200B;並刪除它。
1. 從側面板按一下&#x200B;**步驟**。
1. 將&#x200B;**DAM更新資產工作流程已完成**&#x200B;步驟拖曳至模型定義中。
1. 按一下&#x200B;**頁面資訊** （在&#x200B;**側面板**&#x200B;切換旁邊），然後按一下&#x200B;**開啟屬性**。
1. 在「基本」標籤下，按一下&#x200B;**暫時性工作流程**。
1. 從頂端動作列按一下&#x200B;**儲存並關閉**。
1. 在頂端動作列中，按一下&#x200B;**同步**。
1. 關閉工作流程模型編輯器。

##### 套用停用的自動啟動工作流程模型

遵循[中概述的步驟，將工作流程模型套用至資料夾](#apply-workflow-model-to-folder)，並將&#x200B;**停用自動啟動工作流程**&#x200B;設定為不需要資產後續處理的資料夾的&#x200B;**自動啟動工作流程**。

## 最佳作法和限制 {#best-practices-limitations-tips}

* 設計工作流程時，請考慮您對所有型別轉譯的需求。 如果您預計未來不需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長時間使用[!DNL Experience Manager]後，不想要的轉譯可能會佔用大量的儲存空間。 若為個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂[!DNL Experience Manager]以刪除特定轉譯，或刪除資產並重新上傳。
* 目前，支援僅限於產生轉譯。 不支援產生新資產。
* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳非常大的資產時，有時中繼資料擷取作業會失敗。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Asset Compute服務簡介](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/introduction)。
>* [瞭解擴充功能及使用時機](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/understand-extensibility)。
>* [如何建立自訂應用程式](https://experienceleague.adobe.com/zh-hant/docs/asset-compute/using/extend/develop-custom-application)。
>* [各種使用案例支援的MIME型別](/help/assets/file-format-support.md)。

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
