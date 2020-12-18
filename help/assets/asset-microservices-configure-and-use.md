---
title: 配置和使用資產微服務
description: 設定並使用雲端原生資產微服務，以大規模處理資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 744f63306187b991a11acee2071b9266d11e1a21
workflow-type: tm+mt
source-wordcount: '2532'
ht-degree: 1%

---


# 使用資產微服務和處理配置檔案{#get-started-using-asset-microservices}

資產微服務可讓您使用雲端原生應用程式（又稱為工人），對資產進行可擴充且具彈性的處理。 Adobe管理服務，以最佳化處理不同的資產類型和處理選項。

資產微服務可讓您處理廣泛種類的[檔案類型](/help/assets/file-format-support.md)，其中涵蓋比舊版[!DNL Experience Manager]更多的現成格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。

資產處理取決於&#x200B;**[!UICONTROL 處理配置式]**&#x200B;中的配置。 Experience Manager提供基本預設設定，讓管理員新增更多特定的資產處理設定。 管理員可建立、維護和修改後處理工作流程的設定，包括選擇性自訂。 自訂工作流程可讓開發人員擴充預設產品。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高階檢視資](assets/asset-microservices-flow.png "產處理的高階檢視")

>[!NOTE]
>
>此處所述的資產處理會取代[!DNL Experience Manager]舊版中存在的`DAM Update Asset`工作流程模型。 大部分的標準轉譯產生和中繼資料相關步驟會由資產microservices處理取代，而剩下的步驟（如果有的話）則可由後處理工作流程設定取代。

## 瞭解資產處理選項{#get-started}

Experience Manager可提供下列處理層級。

| 選項 | 說明 | 涵蓋的使用案例 |
|---|---|---|
| [預設設定](#default-config) | 它可以按原樣使用，而且不能修改。 此設定提供非常基本的轉譯產生功能。 | <ul> <li>[!DNL Assets]使用者介面使用的標準縮圖（48、140和319像素） </li> <li> 大型預覽（網頁轉譯- 1280像素） </li><li> 中繼資料和文字擷取。</li></ul> |
| [自訂設定](#standard-config) | 由管理員透過使用者介面設定。 延伸預設選項，提供產生轉譯的更多選項。 擴充現成可用的選項，以提供不同的格式和轉譯。 | <ul><li>FPO轉譯。 </li> <li>變更影像的檔案格式和解析度</li> <li> 有條件地套用至已設定的檔案類型。 </li> </ul> |
| [自訂設定檔](#custom-config) | 由管理員透過使用者介面設定，以透過自訂應用程式使用自訂程式碼，以呼叫[Asset Compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html)。 支援雲端原生和可擴充方式中更複雜的需求。 | 請參閱[允許的使用案例](#custom-config)。 |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支援的檔案格式 {#supported-file-formats}

Asset microservices支援各種檔案格式，以處理、產生轉譯或擷取中繼資料。 有關MIME類型的完整清單以及每種類型支援的功能，請參見[支援的檔案格式](file-format-support.md)。

## 預設設定 {#default-config}

有些預設值已預先設定，以確保Experience Manager中所需的預設轉譯可供使用。 預設設定也可確保中繼資料擷取和文字擷取作業可供使用。 使用者可立即開始上傳或更新資產，而基本處理則預設為可用。

使用預設設定時，只會設定最基本的處理設定檔。 此類處理描述檔在使用者介面上不可見，您無法加以修改。 它一律會執行以處理上傳的資產。 此類預設處理設定檔可確保[!DNL Experience Manager]所需的基本處理已在所有資產上完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準配置{#standard-config}

[!DNL Experience Manager] 根據使用者的需求，提供針對常用格式產生更多特定轉譯的功能。管理員可以建立額外的[!UICONTROL 處理配置檔案]以便建立此類轉譯。 然後，使用者將一或多個可用的描述檔指派給特定的檔案夾，以完成其他處理。 例如，額外的處理可產生網頁、行動裝置和平板電腦的轉譯。 以下視訊說明如何建立和套用「處理設定檔」[!UICONTROL ，以及如何存取已建立的轉譯。]

* **轉譯寬度和高度**:轉譯寬度和高度規格可提供所產生輸出影像的最大大小。Asset microservices會嘗試產生最大的轉譯，其寬度和高度不會分別大於指定的寬度和高度。 外觀比例會保留，與原稿相同。 空值表示資產處理會假設原始影像的像素尺寸。

* **MIME類型包含規則**:當處理具有特定MIME類型的資產時，會先根據轉譯規格的已排除MIME類型值檢查MIME類型。如果符合該清單，則不會為資產（封鎖的清單）產生此特定轉譯。 否則，會根據包含的MIME類型檢查MIME類型，如果與清單匹配，則會生成格式副本（允許清單）。

* **特殊FPO轉譯**:當將大型資產放入 [!DNL Experience Manager] 文 [!DNL Adobe InDesign] 件時，創意專業人員會等待大量 [時間](https://helpx.adobe.com/indesign/using/placing-graphics.html)。同時，用戶被阻止使用[!DNL InDesign]。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可以暫時將小型轉譯置於[!DNL InDesign]檔案中，開始使用，稍後可以以隨選取代為完整解析度的資產。 [!DNL Experience Manager] 提供僅用於放置(FPO)的轉譯。這些FPO轉譯檔案大小較小，但外觀比例相同。

處理設定檔可包含FPO（僅限放置）轉譯。 請參閱[!DNL Adobe Asset Link] [說明檔案](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)瞭解您是否需要為處理設定檔開啟它。 如需詳細資訊，請參閱[Adobe Asset Link完整檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

### 建立標準配置檔案{#create-standard-profile}

若要建立標準處理設定檔，請遵循下列步驟：

1. 管理員可存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 提供名稱，幫助您在套用至資料夾時唯一識別描述檔。
1. 要生成FPO轉譯，請在&#x200B;**[!UICONTROL Standard]**&#x200B;標籤上啟用&#x200B;**[!UICONTROL 建立FPO轉譯]**。 輸入介於1和100之間的&#x200B;**[!UICONTROL Quality]**&#x200B;值。
1. 若要產生其他轉譯，請按一下「新增&#x200B;**[!UICONTROL 」並提供下列資訊：]**

   * 每個轉譯的檔案名稱。
   * 每個轉譯的檔案格式（PNG、JPEG、GIF或WebP）。
   * 每個轉譯的寬度和高度（以像素為單位）。 如果未指定值，則會使用原始影像的全像素大小。
   * 每個JPEG和WebP轉譯的品質百分比。
   * 包含和排除的MIME類型，以定義描述檔的適用性。

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自訂描述檔和使用案例{#custom-config}

[!DNL Asset Compute Service]支援多種使用案例，例如預設處理、處理Adobe特定格式（例如Photoshop檔案），以及實作自訂或組織特定處理。 過去需要的DAM更新資產工作流程自訂會自動處理，或是透過處理設定檔設定來處理。 如果這些處理選項無法滿足業務需求，Adobe建議開發並使用[!DNL Asset Compute Service]來擴充預設功能。 如需概觀，請參閱[瞭解擴充性，以及何時使用](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)。

>[!NOTE]
>
>Adobe建議僅在無法使用預設組態或標準設定檔來完成業務需求時，才使用自訂應用程式。

它可將影像、視訊、檔案和其他檔案格式轉換為不同的轉譯，包括縮圖、擷取的文字和中繼資料，以及封存。

開發人員可使用[!DNL Asset Compute Service]來建立符合支援使用案例的自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html)。 [[!DNL Experience Manager] 可以使用管理員設定的自訂設定檔，從使用者介面呼叫這些自訂應用程式。[!DNL Asset Compute Service] 支援以下調用外部服務的使用案例：

* 使用[!DNL Adobe Photoshop]的[ImageCutout API](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout)將結果儲存為轉譯。
* 呼叫協力廠商系統以更新資料，例如PIM系統。
* 使用[!DNL Photoshop] API，根據Photoshop範本產生各種轉譯。
* 使用[Adobe Lightroom API](https://github.com/AdobeDocs/lightroom-api-docs#supported-features)最佳化收錄的資產，並將其儲存為轉譯。

>[!NOTE]
>
>您無法使用自訂應用程式來編輯標準中繼資料。 您只能修改自訂中繼資料。

### 建立自訂描述檔{#create-custom-profile}

若要建立自訂描述檔，請遵循下列步驟：

1. 管理員可存取&#x200B;**[!UICONTROL 工具>資產>處理設定檔]**。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 按一下&#x200B;**[!UICONTROL Custom]**&#x200B;頁籤。 按一下&#x200B;**[!UICONTROL 添加新]**。 提供所要的轉譯檔案名稱。
1. 提供下列資訊。

   * 每個轉譯的檔案名稱及支援的副檔名。
   * [Firefly自訂應用程式的端點URL](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html)。應用程式必須與Experience Manager帳戶來自相同的組織。
   * 將服務參數添加到[，將額外資訊或參數傳遞到自定義應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend)。
   * 包含和排除的MIME類型，可將處理限制為少數特定的檔案格式。

   按一下&#x200B;**[!UICONTROL 「儲存」]**。

自訂應用程式是無頭[專案Firefly](https://github.com/AdobeDocs/project-firefly)應用程式。 如果自訂應用程式是使用處理設定檔來設定，就會取得所有提供的檔案。 應用程式必須篩選檔案。

>[!CAUTION]
>
>如果Firefly應用程式和[!DNL Experience Manager]帳戶不來自同一個組織，則整合無法運作。

### 自訂描述檔{#custom-profile-example}的範例

為了說明自訂描述檔的使用情形，我們考慮將一些自訂文字套用至促銷活動影像的使用案例。 您可以建立處理設定檔，以運用Photoshop API來編輯影像。

資產計算服務整合可讓Experience Manager使用[!UICONTROL 服務參數]欄位將這些參數傳遞至自訂應用程式。 然後自訂應用程式會呼叫Photoshop API，並將這些值傳遞至API。 例如，您可以傳遞字型名稱、文字顏色、文字粗細和文字大小，將自訂文字新增至促銷活動影像。

![custom-processing-profile](assets/custom-processing-profile.png)

*圖：使用 [!UICONTROL Service ] Parametersfield將新增資訊傳送至自訂應用程式內建的預先定義參數。在此範例中，當上傳促銷活動影像時，會以`Arial-BoldMT`字型的`Jumanji`文字更新影像。*

## 使用處理設定檔來處理資產{#use-profiles}

建立其他自訂處理設定檔並套用至特定資料夾，讓Experience Manager處理上傳至或更新至這些資料夾的資產。 預設的內建標準處理設定檔一律會執行，但在使用者介面上不可見。 如果您新增自訂的描述檔，則這兩個描述檔都會用來處理上傳的資產。

使用下列其中一種方法，將處理設定檔套用至資料夾：

* 管理員可以在&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理配置式]**&#x200B;中選擇處理配置式定義，並使用&#x200B;**[!UICONTROL 將配置式應用於資料夾]**&#x200B;操作。 它會開啟內容瀏覽器，讓您導覽至特定資料夾、選取資料夾並確認描述檔的應用程式。
* 使用者可以在「資產」使用者介面中選取資料夾、使用&#x200B;**[!UICONTROL 屬性]**&#x200B;動作來開啟資料夾屬性畫面、按一下「處理描述檔&#x200B;****」標籤，然後在快顯清單中，選取該資料夾的適當處理描述檔。 要保存更改，請按一下「保存並關閉」]**。**[!UICONTROL 
   ![從「資產屬性」標籤將處理設定檔套用至資料夾](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>只能將一個處理設定檔套用至資料夾。 若要產生更多轉譯，請新增更多轉譯定義至現有的處理設定檔。

將處理描述檔套用至資料夾後，會使用設定的其他處理描述檔來處理此資料夾或其子資料夾中上傳（或更新）的所有新資產。 此處理除了標準預設描述檔外，還有其他處理方式。

>[!NOTE]
>
>套用至資料夾的處理描述檔適用於整個樹狀結構，但可與套用至子資料夾的其他描述檔重疊。 當資產上傳至資料夾時，Experience Manager會檢查包含資料夾的屬性以取得處理設定檔。 如果未應用任何檔案，則會檢查層次結構中的父資料夾以查找要應用的處理配置檔案。

若要確認資產已處理，請在左側導軌的[!UICONTROL 轉譯]檢視中預覽產生的轉譯。 開啟資產預覽並開啟左側導軌以存取&#x200B;**[!UICONTROL 轉譯]**&#x200B;檢視。 處理設定檔中的特定轉譯（特定資產的類型與MIME類型包含規則相符）應可見且可存取。

![其他轉譯](assets/renditions-additional-renditions.png)

*圖：處理描述檔套用至父資料夾所產生的兩個其他轉譯範例。*

## 後處理工作流程{#post-processing-workflows}

若是需要額外處理無法使用處理設定檔的資產，則可新增其他後處理工作流程至設定。 這允許在使用資產微服務的可配置處理之上添加完全自定義的處理。

若已設定後處理工作流程，則會在微型服務處理完成後由[!DNL Experience Manager]自動執行。 您不需要手動新增工作流程啟動器來觸發它們。 範例包括：

* 處理資產的自訂工作流程步驟。
* 整合，將中繼資料或屬性新增至外部系統的資產，例如產品或流程資訊。
* 由外部服務完成的額外處理。

將後處理工作流程設定新增至Experience Manager，由下列步驟組成：

* 建立一或多個工作流程模型。 檔案將其提及為&#x200B;*後處理工作流程模型*，但這些是常規的Experience Manager工作流程模型。
* 將特定的工作流程步驟新增至這些模型。 這些步驟是根據工作流程模型組態對資產執行。
* 最後添加[!UICONTROL DAM更新資產工作流完成流程]步驟。 新增此步驟可確保Experience Manager知道處理何時結束，資產可標示為已處理，即&#x200B;*資產上會顯示新*。
* 為「自訂工作流程執行者服務」建立組態，允許依路徑（資料夾位置）或規則運算式來設定處理後工作流程模型的執行。

### 建立後處理工作流程模型{#create-post-processing-workflow-models}

後處理工作流模型是常規的[!DNL Experience Manager]工作流模型。 如果您需要針對不同儲存庫位置或資產類型進行不同的處理，請建立不同的模型。

應根據需求新增處理步驟。 您可以使用任何支援的步驟，以及任何自訂實作的工作流程步驟。

請確定每個後處理工作流程的最後一個步驟是`DAM Update Asset Workflow Completed Process`。 最後一個步驟有助於確保Experience Manager知道資產處理何時完成。

### 配置後處理工作流執行{#configure-post-processing-workflow-execution}

若要設定在資產微型服務處理完成後，系統中上傳或更新的資產所執行的後處理工作流程模型，必須設定自訂工作流程執行者服務。

自訂工作流程執行者服務(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服務，提供兩個設定選項：

* 依路徑(`postProcWorkflowsByPath`)的後處理工作流程：可以根據不同的儲存庫路徑列出多個工作流模型。 路徑和模型應以冒號分隔。 支援簡單儲存庫路徑，並應映射到`/var`路徑中的工作流模型。 例如：`/content/dam/my-brand:/var/workflow/models/my-workflow`。
* 依運算式(`postProcWorkflowsByExpression`)的後處理工作流程：可以根據不同的規則運算式列出多個工作流程模型。 運算式和模型應以冒號分隔。 規則運算式應直接指向「資產」節點，而非其中一個轉譯或檔案。 例如：`/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`。

>[!NOTE]
>
>「自訂工作流程執行者」的設定是OSGi服務的設定。 如需如何部署OSGi組態的詳細資訊，請參閱[部署至Experience Manager](/help/implementing/deploying/overview.md)。
>與[!DNL Experience Manager]的內部部署和受管服務部署不同，雲端服務部署不直接提供OSGi Web控制台。

如需後處理工作流程中可使用哪些標準工作流程步驟的詳細資訊，請參閱開發人員參考中後處理工作流程中的[工作流程步驟。](developer-reference-material-apis.md#post-processing-workflows-steps)

## 最佳做法和限制{#best-practices-limitations-tips}

* 設計工作流程時，請考慮您對所有類型轉譯的需求。 如果您未預見未來需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長期使用[!DNL Experience Manager]後，不需要的轉譯可能佔用大量儲存空間。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂[!DNL Experience Manager]以刪除特定轉譯，或刪除資產並再次上傳這些資產。
* 目前，支援僅限於產生轉譯。 不支援產生新資產。
* 目前，中繼資料擷取的檔案大小限制約為10 GB。 上傳超大型資產時，中繼資料擷取作業有時候會失敗。

>[!MORELIKETHIS]
>
>* [資產計算服務簡介](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html)。
>* [瞭解擴充性，以及何時使用](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)。
>* [如何建立自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html)。
>* [支援各種使用案例的MIME類型](/help/assets/file-format-support.md)。


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
