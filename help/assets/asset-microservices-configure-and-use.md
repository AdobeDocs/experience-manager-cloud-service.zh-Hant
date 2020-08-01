---
title: 設定並使用資產微服務進行資產處理
description: 瞭解如何設定和使用雲端原生資產微服務，以大規模處理資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a29b00ed6b216fb83f6a7c6bb7b34e1f317ffa57
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 1%

---


# 使用資產微型服務和處理設定檔 {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

資產微型服務提供可擴充且具彈性的資產處理功能，可使用雲端服務。 Adobe管理服務，以最佳化處理不同的資產類型和處理選項。

資產處理取決於處理設定檔中 **[!UICONTROL 的設定]**，此設定提供預設設定，並讓管理員新增更特定的資產處理設定。 管理員可以建立和維護後處理工作流程的設定，包括選擇性自訂。 自訂工作流程可讓您擴充性和完全自訂。

與舊版Experience Manager相比，Asset [microservices可讓您處理各種檔案類型](/help/assets/file-format-support.md) ，包括更多現成可用格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高階檢視資](assets/asset-microservices-flow.png "產處理的高階檢視")

>[!NOTE]
>
>此處所述的資產處理會取代 `DAM Update Asset` 舊版中存在的工作流程模型 [!DNL Experience Manager]。 大部分的標準轉譯產生和中繼資料相關步驟會由資產microservices處理取代，而剩下的步驟（如果有的話）則可由後處理工作流程設定取代。

## 瞭解資產處理選項 {#get-started}

Experience Manager可提供下列處理層級。

| 選項 | 說明 | 涵蓋的使用案例 |
|---|---|---|
| [預設設定](#default-config) | 它可以按原樣使用，而且不能修改。 此設定提供非常基本的轉譯產生功能。 | <ul> <li>使用者介面使 [!DNL Assets] 用的標準縮圖（48、140和319像素） </li> <li> 大型預覽（網頁轉譯- 1280 px） </li><li> 中繼資料和文字擷取。</li></ul> |
| [自訂設定](#standard-config) | 由管理員透過使用者介面設定。 延伸預設選項，提供產生轉譯的更多選項。 擴充現成可用的工作器，以提供不同的格式和轉譯。 | <ul><li>FPO轉譯。 </li> <li>變更影像的檔案格式和解析度</li> <li> 有條件地套用至已設定的檔案類型。 </li> </ul> |
| [自訂設定檔](#custom-config) | 由管理員透過使用者介面設定，以透過自訂工作者使用自訂代碼來呼叫 [!DNL Asset Compute Service]。 支援雲端原生和可擴充方式中更複雜的需求。 | 請參閱 [允許的使用案例](#custom-config)。 |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支援的檔案格式 {#supported-file-formats}

Asset microservices支援各種檔案格式，以處理、產生轉譯或擷取中繼資料。 請參 [閱支援的檔案格式](file-format-support.md) ，以取得MIME類型的完整清單以及每種類型支援的功能。

## 預設設定 {#default-config}

有些預設值已預先設定，以確保Experience Manager中所需的預設轉譯可供使用。 預設設定也可確保中繼資料擷取和文字擷取作業可供使用。 使用者可立即開始上傳或更新資產，而基本處理則預設為可用。

使用預設設定時，只會設定最基本的處理設定檔。 此類處理描述檔在使用者介面上不可見，您無法加以修改。 它一律會執行以處理上傳的資產。 此類預設處理設定檔可確保完成所有資產所需 [!DNL Experience Manager] 的基本處理。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準配置 {#standard-config}

[!DNL Experience Manager] 根據使用者的需求，提供針對常用格式產生更多特定轉譯的功能。 管理員可以建立其他 [!UICONTROL 的處理設定檔] ，以利建立這類轉譯。 然後，使用者將一或多個可用的描述檔指派給特定的檔案夾，以完成其他處理。 例如，額外的處理可產生網頁、行動裝置和平板電腦的轉譯。 以下影片說明如何建立和套用「處 [!UICONTROL 理設定檔] 」，以及如何存取已建立的轉譯。

* **轉譯寬度和高度**: 轉譯寬度和高度規格可提供所產生輸出影像的最大大小。 Asset microservices會嘗試產生最大的轉譯，其寬度和高度不會分別大於指定的寬度和高度。 外觀比例會保留，與原稿相同。 空值表示資產處理會假設原始影像的像素尺寸。

* **MIME類型包含規則**: 當處理具有特定MIME類型的資產時，會先根據轉譯規格的已排除MIME類型值檢查MIME類型。 如果符合該清單，則不會為資產（封鎖的清單）產生此特定轉譯。 否則，會根據包含的MIME類型檢查MIME類型，如果與清單匹配，則會生成格式副本（允許清單）。

* **特殊FPO轉譯**: 將大型資產放入檔案時， [!DNL Experience Manager] 創 [!DNL Adobe InDesign] 意專業人員會在放入資產後等 [待相當長時間](https://helpx.adobe.com/indesign/using/placing-graphics.html)。 同時，用戶被阻止使用 [!DNL InDesign]。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可讓檔案中暫時放置小型轉譯， [!DNL InDesign] 以開始處理，稍後可以隨選取代為完整解析度的資產。 [!DNL Experience Manager] 提供僅用於放置(FPO)的轉譯。 這些FPO轉譯檔案大小較小，但外觀比例相同。

處理設定檔可包含FPO（僅限放置）轉譯。 請參 [!DNL Adobe Asset Link] 閱文 [件](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) ，瞭解您是否需要為處理設定檔開啟它。 如需詳細資訊，請參 [閱Adobe Asset Link完整檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

### 建立標準設定檔 {#create-standard-profile}

若要建立標準處理設定檔，請遵循下列步驟：

1. 管理員可存 **[!UICONTROL 取「工具]** >資 **[!UICONTROL 產]** >處 **[!UICONTROL 理設定檔]**」。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 提供名稱，幫助您在套用至資料夾時唯一識別描述檔。
1. 若要產生FPO轉譯，請在「標準」標 **[!UICONTROL 簽上]** ，啟 **[!UICONTROL 用「建立FPO轉譯」]**。 輸入 **[!UICONTROL 1到]** 100之間的「品質」值。
1. 若要產生其他轉譯，請按一 **[!UICONTROL 下「新增]** 」並提供下列資訊：

   * 每個轉譯的檔案名稱。
   * 每個轉譯的檔案格式（PNG、JPEG或GIF）。
   * 每個轉譯的寬度和高度（以像素為單位）。 如果未指定值，則會使用原始影像的全像素大小。
   * 每個JPEG轉譯的品質百分比。
   * 包含和排除的MIME類型，以定義描述檔的適用性。

   ![processing-profiles-adding](assets/processing-profiles-adding.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自訂描述檔和使用案例 {#custom-config}

<!-- **TBD items**:

* Overall cross-linking with the extensibility content.
* Mention how to get URL of worker. Worker URL for Dev, Stage, and Prod environments.
* Mention mapping of service parameters. Link to compute service article.
* Review from flow perspective shared in Jira ticket.
-->

支 [!DNL Asset Compute Service] 援多種使用案例，例如預設處理、處理Adobe特定格式（例如Photoshop檔案），以及實作自訂或組織特定處理。 過去需要的DAM更新資產工作流程自訂，預設會處理，或透過UI上的處理設定檔設定來處理。 如果此處理不符合商業需求，Adobe建議開發並使用資產計算服務來擴充預設功能。

>[!NOTE]
>
>Adobe建議僅在業務需要無法使用預設設定或標準設定檔時使用自訂工作者。

它可將影像、視訊、檔案和其他檔案格式轉換為不同的轉譯，包括縮圖、擷取的文字和中繼資料以及封存。

開發人員可使 [!DNL Asset Compute Service] 用此工具來建立符合預先定義使用案例的專業自訂工作者。 [!DNL Experience Manager] 可以使用管理員配置的自定義配置檔案從用戶介面調用這些自定義工作器。 [!DNL Asset Compute Service] 支援以下調用外部服務的使用案例：

* 使用 [!DNL Adobe Photoshop]的 [ImageCutout API](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) ，並將結果儲存為轉譯。
* 叫用協力廠商系統以更新資料，例如PIM系統。
* 使用 [!DNL Photoshop] API以Photoshop範本產生各種轉譯。
* 使用 [Adobe Lightroom API](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) ，最佳化所擷取的資產，並將其儲存為轉譯。

>[!NOTE]
>
>您無法使用自訂工作者編輯標準中繼資料。 您只能修改自訂中繼資料。

### 建立自訂描述檔 {#create-custom-profile}

若要建立自訂描述檔，請遵循下列步驟：

1. 管理員可存 **[!UICONTROL 取「工具>資產>處理設定檔]**」。 按一下&#x200B;**[!UICONTROL 建立]**。
1. Click on **[!UICONTROL Custom]** tab. 按一 **[!UICONTROL 下新增]**。 提供所要的轉譯檔案名稱。
1. 提供下列資訊。

   * 每個轉譯的檔案名稱及支援的副檔名。
   * Firefly自訂應用程式的端點URL。 應用程式必須與Experience Manager帳戶來自相同的組織。
   * 添加 [!UICONTROL 服務參數] ，以將額外資訊或參數傳遞到自定義工作器。
   * 包含和排除的MIME類型，以定義描述檔的適用性。

   按一下&#x200B;**[!UICONTROL 「儲存」]**。

>[!CAUTION]
>
>如果Firefly應用程式和 [!DNL Experience Manager] 帳戶不來自同一個組織，則整合無法運作。

### 自訂描述檔的範例 {#custom-profile-example}

為了說明自訂描述檔的使用情形，我們考慮將一些自訂文字套用至促銷活動影像的使用案例。 您可以建立處理設定檔，以運用Photoshop API來編輯影像。

資產計算服務整合允許Experience Manager使用服務參數欄位將這些參數傳遞 [!UICONTROL 給自定義工] 。 然後，自訂工作者會叫用Photoshop API，並將這些值傳遞至API。 例如，您可以傳遞字型名稱、文字顏色、文字粗細和文字大小，將自訂文字新增至促銷活動影像。

![custom-processing-profile](assets/custom-processing-profile.png)

*圖： 使用[!UICONTROL 服務參數欄位]，將添加的資訊傳遞給構建到自定義工作器中的預定義參數。*

當促銷活動影像上傳至套用此處理設定檔的檔案夾時，會以字型文字更 `Jumanji` 新影 `Arial-BoldMT` 像。

## 使用處理設定檔來處理資產 {#use-profiles}

建立其他自訂處理設定檔並套用至特定資料夾，讓Experience Manager處理上傳至或更新至這些資料夾的資產。 預設的內建標準處理設定檔一律會執行，但在使用者介面上不可見。 如果您新增自訂的描述檔，則這兩個描述檔都會用來處理上傳的資產。

使用下列其中一種方法，將處理設定檔套用至資料夾：

* 管理員可以在「工具 **[!UICONTROL >資產]** >處理配置檔案 **[!UICONTROL 」中選擇處理配置檔案定義，]********** 然後使用「將配置檔案應用到資料夾」(s)Jaction。 它會開啟內容瀏覽器，讓您導覽至特定資料夾、選取資料夾並確認描述檔的應用程式。
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the popup list, select the correct processing profile for that folder. 若要儲存變更，請按一下「 **[!UICONTROL 儲存並關閉」]**。

>[!NOTE]
>
>只能將一個處理設定檔套用至特定資料夾。 若要產生更多轉譯，請新增更多轉譯定義至現有的處理設定檔。

將處理描述檔套用至資料夾後，會使用設定的其他處理描述檔來處理此資料夾或其子資料夾中上傳（或更新）的所有新資產。 此處理除了標準預設描述檔外，還有其他處理方式。 如果您將多個描述檔套用至資料夾，則會使用每個描述檔來處理已上傳或更新的資產。

>[!NOTE]
>
>套用至資料夾的處理描述檔適用於整個樹狀結構，但可與套用至子資料夾的其他描述檔重疊。 當資產上傳至資料夾時，Experience Manager會檢查包含資料夾的屬性以取得處理設定檔。 如果未應用任何檔案，則會檢查層次結構中的父資料夾以查找要應用的處理配置檔案。

所有產生的轉譯都可在左側導 [!UICONTROL 軌的「轉譯] 」檢視中使用。 開啟資產預覽並開啟左側導軌以存取「轉 **[!UICONTROL 譯]** 」檢視。 處理設定檔中的特定轉譯（特定資產的類型與MIME類型包含規則相符）應可見且可存取。

![其他轉譯](assets/renditions-additional-renditions.png)

*圖： 處理描述檔套用至父資料夾所產生的兩個其他轉譯範例。*

## 後處理工作流程 {#post-processing-workflows}

若是需要額外處理無法使用處理設定檔的資產，則可新增其他後處理工作流程至設定。 這允許在使用資產微服務的可配置處理之上添加完全自定義的處理。

若已設定後置處理工作流程，AEM會在微型服務處理完成後自動執行。 您不需要手動新增工作流程啟動器來觸發它們。 範例包括：

* 處理資產的自訂工作流程步驟。
* 整合，將中繼資料或屬性新增至外部系統的資產，例如產品或流程資訊。
* 由外部服務完成的額外處理。

將後處理工作流程設定新增至Experience Manager，由下列步驟組成：

* 建立一或多個工作流程模型。 檔案將它提及為後 *處理工作流程模型*，但這些是一般的Experience Manager工作流程模型。
* 將特定的工作流程步驟新增至這些模型。 這些步驟是根據工作流程模型組態對資產執行。
* 最後 [!UICONTROL 新增DAM更新資產工作流程完成] 「程式」步驟。 新增此步驟可確保Experience Manager知道處理何時結束，且資產可標示為已處理，即 *New* （新）會顯示在資產上。
* 為「自訂工作流程執行者服務」建立組態，允許依路徑（資料夾位置）或規則運算式來設定處理後工作流程模型的執行。

### 建立後處理工作流程模型 {#create-post-processing-workflow-models}

後處理工作流程模型是一般的AEM工作流程模型。 如果您需要針對不同儲存庫位置或資產類型進行不同的處理，請建立不同的模型。

應根據需求新增處理步驟。 您可以使用任何支援的步驟，以及任何自訂實作的工作流程步驟。

請確定每個後處理工作流程的最後一個步驟是 `DAM Update Asset Workflow Completed Process`。 最後一個步驟有助於確保Experience Manager知道資產處理何時完成。

### 設定後處理工作流程執行 {#configure-post-processing-workflow-execution}

若要設定在資產微型服務處理完成後，系統中上傳或更新的資產所執行的後處理工作流程模型，必須設定自訂工作流程執行者服務。

Custom Workflow Runner服務(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服務，提供兩個設定選項：

* 後處理工作流程(依路徑`postProcWorkflowsByPath`): 可以根據不同的儲存庫路徑列出多個工作流模型。 路徑和模型應以冒號分隔。 支援簡單儲存庫路徑，並應映射到路徑中的工作流 `/var` 模型。 For example: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* 後處理工作流程(依運算式`postProcWorkflowsByExpression`): 可以根據不同的規則運算式列出多個工作流程模型。 運算式和模型應以冒號分隔。 規則運算式應直接指向「資產」節點，而非其中一個轉譯或檔案。 For example: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>「自訂工作流程執行者」的設定是OSGi服務的設定。 如需 [如何部署OSGi組態的詳細資訊，請參閱部署至Experience Manager](/help/implementing/deploying/overview.md) 。
>OSGi Web主控台與AEM的內部部署和受管理服務部署不同，不直接在雲端服務部署中提供。

如需後處理工作流程中可使用哪些標準工作流程步驟的詳細資訊，請參閱開發 [人員參考中後處理工作流程中的工作流程](developer-reference-material-apis.md#post-processing-workflows-steps) 。

## 最佳實務與限制 {#best-practices-limitations-tips}

* 設計工作流程時，請考慮您對所有類型轉譯的需求。 如果您未預見未來需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長期使用後，不需要的轉譯可能會佔用大量儲存空間 [!DNL Experience Manager]。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂以 [!DNL Experience Manager] 刪除特定轉譯，或刪除資產並再次上傳這些資產。
* 目前，支援僅限於產生轉譯。 不支援產生新資產。
