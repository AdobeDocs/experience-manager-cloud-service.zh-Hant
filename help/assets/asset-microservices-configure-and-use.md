---
title: 設定並使用資產微服務進行資產處理
description: 瞭解如何設定和使用雲端原生資產微服務，以大規模處理資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304

---


# 開始使用資產微服務 {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

資產微服務使用雲端服務提供資產的可擴充且彈性化處理。 Adobe管理服務，以最佳化處理不同的資產類型和處理選項。

資產處理取決於處理設定檔 **[!UICONTROL 中的設定]**，此設定提供預設設定，並允許管理員新增更特定的資產處理設定。 管理員可以建立和維護後處理工作流程的設定，包括選擇性自訂。 自訂工作流程可讓您擴充性和完全自訂。

與舊版Experience Manager相比，Asset microservices [可讓您處理多種檔案類型](/help/assets/file-format-support.md) ，其中包含更多現成可用格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高階檢視資](assets/asset-microservices-flow.png "產處理的高階檢視")

>[!NOTE]
>
> 此處所述的資產處理會取代 `DAM Update Asset` 舊版Experience Manager中的工作流程模型。 大部分的標準轉譯產生和中繼資料相關步驟會由資產microservices處理取代，而剩下的步驟（如果有的話）則可由後處理工作流程設定取代。

## 開始處理資產 {#get-started}

資產微服務的資產處理已預先設定為預設設定，以確保系統所需的預設轉譯可供使用。 此外，還可確保可使用中繼資料擷取和文字擷取作業。 使用者可立即開始上傳或更新資產，而基本處理則預設為可用。

針對特定的轉譯產生或資產處理需求，AEM管理員可以建立其他處 [!UICONTROL 理設定檔]。 使用者可將一或多個可用的描述檔指派給特定的檔案夾，以完成其他處理。 例如，產生網頁、行動裝置和平板電腦專用的轉譯。 以下影片說明如何建立和套用「處 [!UICONTROL 理設定檔] 」，以及如何存取已建立的轉譯。

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

若要變更現有的設定檔，請參 [閱資產微型服務的設定](#configure-asset-microservices)。
若要建立符合您自訂需求的自訂處理設定檔，例如要與其他系統整合，請參 [閱後處理工作流程](#post-processing-workflows)。

## 資產微型服務的配置 {#configure-asset-microservices}

若要設定資產微型服務，管理員可使用「工具>資產>處 **[!UICONTROL 理設定檔」下方的設定使用者介面]**。

### 預設設定 {#default-config}

使用預設設定時，只會設定標準處理設定檔。 標準處理設定檔在使用者介面上不可見，您無法加以修改。 它一律會執行以處理上傳的資產。 標準處理設定檔可確保Experience Manager所需的所有基本處理都已完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

標準處理設定檔提供下列處理設定：

* Asset使用者介面使用的標準縮圖（48、140和319像素）
* 大型預覽（網頁轉譯- 1280 px）
* 中繼資料擷取
* 文字擷取

### 支援的檔案格式 {#supported-file-formats}

Asset microservices支援多種檔案格式，包括產生轉譯或擷取中繼資料的功能。 如需 [完整清單](file-format-support.md) ，請參閱支援的檔案格式。

### 新增其他處理設定檔 {#processing-profiles}

您可使用「建立」動作新增其他處 **[!UICONTROL 理設定]** 檔。

每個處理設定檔設定都包含轉譯清單。 您可以針對每個轉譯指定下列項目：

* 轉譯名稱。
* 支援的轉譯格式，例如JPEG、PNG或GIF。
* 轉譯寬度和高度（以像素為單位）。 如果未指定，則會使用原始影像的全像素大小。
* JPEG的轉譯品質（百分比）。
* 包含和排除的MIME類型，以定義描述檔的適用性。

![processing-profiles-adding](assets/processing-profiles-adding.png)

當您建立並儲存新的處理設定檔時，它會新增至已設定的處理設定檔清單。 您可以將這些處理設定檔套用至資料夾階層中的資料夾，讓這些設定檔對資產上傳和資產處理有效。

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) -->

#### 轉譯寬度和高度 {#rendition-width-height}

轉譯寬度和高度規格可提供所產生輸出影像的最大大小。 Asset microservice會嘗試產生最大的轉譯，其寬度和高度分別不會大於指定的寬度和高度。 外觀比例會保留，與原稿相同。

空值表示資產處理會假設原始影像的像素尺寸。

#### MIME類型包含規則 {#mime-type-inclusion-rules}

當處理具有特定MIME類型的資產時，會先根據轉譯規格的已排除MIME類型值檢查MIME類型。 如果符合該清單，則不會為資產產生此特定轉譯（「黑名單」）。

否則，會根據包含的MIME類型檢查MIME類型，如果與清單匹配，則會生成格式副本（「白名單」）。

#### 特殊FPO轉譯 {#special-fpo-rendition}

當將AEM中的大型資產放入Adobe InDesign檔案時，創意專業人員在放置資產後必須等 [待相當長時間](https://helpx.adobe.com/indesign/using/placing-graphics.html)。 同時，使用者也無法使用InDesign。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可讓InDesign檔案中暫時放置小型轉譯，以開始，稍後可以以隨選取代為完整解析度的資產。 Experience Manager提供僅用於放置(FPO)的轉譯。 這些FPO轉譯檔案大小較小，但外觀比例相同。

處理設定檔可包含FPO（僅限放置）轉譯。 請參閱Adobe Asset Link [檔案](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) ，瞭解您是否需要為處理設定檔開啟它。 如需詳細資訊，請參 [閱Adobe Asset Link完整檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

## 使用資產微服務處理資產 {#use-asset-microservices}

建立其他自訂處理設定檔並套用至特定資料夾，讓Experience Manager處理上傳至或更新至這些資料夾的資產。 預設的內建標準處理設定檔一律會執行，但在使用者介面上不可見。 如果您新增自訂的描述檔，則這兩個描述檔都會用來處理上傳的資產。

有兩種方式可讓處理設定檔套用至資料夾：

* 管理員可以在「工具」>「資產」>「處 **[!UICONTROL 理設定檔」中選取處理設定檔定義]**，然後使用「 **[!UICONTROL 將設定檔套用至資料夾」動作]** 。 它會開啟內容瀏覽器，讓您導覽至特定資料夾、選取資料夾並確認描述檔的應用程式。
* 使用者可以在「資產」使用者介面中選取資料夾、使用「屬性」動作來開啟資料夾屬性畫面、按一下「處理設定檔 ******** 」標籤，然後在下拉式清單中，為該資料夾選取正確的處理設定檔。「儲存並關閉」動作 **[!UICONTROL 時會儲存選項]** 。

>[!NOTE]
>
>只能將一個處理設定檔套用至特定資料夾。 如果您需要產生更多轉譯，可以新增更多轉譯定義至處理設定檔。

將處理描述檔套用至資料夾後，會使用設定的其他處理描述檔來處理此資料夾或其子資料夾中上傳（或更新）的所有新資產。 除了標準預設描述檔外，還有這項額外處理。 如果您將多個描述檔套用至資料夾，則會使用每個描述檔來處理已上傳或更新的資產。

>[!NOTE]
>
>當資產上傳至資料夾時，Experience Manager會檢查包含資料夾的屬性以取得處理設定檔。 如果未套用任何設定檔，則會在資料夾樹狀結構中上移，直到找到套用的處理設定檔，並將其用於資產。 這表示套用至資料夾的處理描述檔適用於整個樹狀結構，但可以套用至子資料夾的其他描述檔過度使用。

使用者可以開啟已完成處理的新上傳資產、開啟資產預覽，然後按一下左側邊欄的「轉譯」檢視，以檢查處理是否實際 **[!UICONTROL 發生]** 。 處理設定檔中的特定轉譯（特定資產的類型與MIME類型包含規則相符）應可見且可存取。

![additional-renditions](assets/renditions-additional-renditions.png)*圖： 處理描述檔套用至父資料夾所產生的兩個其他轉譯範例*

## 後處理工作流程 {#post-processing-workflows}

若是需要額外處理無法使用處理設定檔的資產，則可新增其他後處理工作流程至設定。 這允許在使用資產微服務的可配置處理之上添加完全自定義的處理。

若已設定後置處理工作流程，AEM會在微型服務處理完成後自動執行。 您不需要手動新增工作流程啟動器來觸發它們。

範例包括：

* 處理資產的自訂工作流程步驟，例如從專屬檔案格式產生轉譯的Java程式碼。
* 整合，將中繼資料或屬性新增至外部系統的資產，例如產品或流程資訊。
* 外部服務進行的額外處理

將後處理工作流程設定新增至Experience Manager，由下列步驟組成：

* 建立一或多個工作流程模型。 我們將它們稱為「後處理工作流程模型」，但它們是一般的AEM工作流程模型。
* 向這些模型添加特定的工作流步驟。 這些步驟將根據工作流程模型組態對資產執行。
* 此類模型的最後一步必須是步 `DAM Update Asset Workflow Completed Process` 驟。 這是必要項目，以確保AEM知道處理已結束，且資產可標示為已處理（「新」）
* 建立自訂工作流程執行者服務的設定，允許依路徑（資料夾位置）或規則運算式來設定後處理工作流程模型的執行

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
> OSGi Web主控台與AEM的內部部署和受管理服務部署不同，不直接在雲端服務部署中提供。

如需後處理工作流程中可使用哪些標準工作流程步驟的詳細資訊，請參閱開發 [人員參考中後處理工作流程中的工作流程](developer-reference-material-apis.md#post-processing-workflows-steps) 。
