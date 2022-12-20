---
title: 配置和使用資產微服務
description: 設定並使用雲端原生資產微服務以大規模處理資產。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 5545cd1739db41dbabf06cff916811123e7e09be
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 0%

---

# 使用資產微服務和處理設定檔 {#get-started-using-asset-microservices}

資產微服務提供使用雲端原生應用程式（也稱為背景工作）的資產可擴充且具彈性的處理功能。 Adobe管理服務，以最佳處理不同資產類型和處理選項。

資產微服務可讓您處理 [檔案類型廣泛](/help/assets/file-format-support.md) 比舊版可能涵蓋的更多現成格式 [!DNL Experience Manager]. 例如，現在可以擷取PSD和PSB格式的縮圖，但之前需要協力廠商解決方案，例如 [!DNL ImageMagick].

資產處理取決於 **[!UICONTROL 處理設定檔]**. Experience Manager提供基本預設設定，並讓管理員新增更具體的資產處理設定。 管理員建立、維護和修改後置處理工作流程的設定，包括可選自訂。 自訂工作流程可讓開發人員擴充預設產品。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的概觀](assets/asset-microservices-flow.png "資產處理的概觀")

>[!NOTE]
>
>此處所述的資產處理會取代 `DAM Update Asset` 舊版中存在的工作流模型 [!DNL Experience Manager]. 大部分標準轉譯產生和中繼資料相關步驟會由資產微服務處理取代，其餘步驟（若有）則可由後置處理工作流程設定取代。

## 了解資產處理選項 {#get-started}

[!DNL Experience Manager] 允許下列處理層級。

| 選項 | 說明 | 涵蓋的使用案例 |
|---|---|---|
| [預設設定](#default-config) | 可依原樣使用，且無法修改。 此配置提供了非常基本的格式副本生成功能。 | <ul> <li>使用的標準縮圖 [!DNL Assets] 使用者介面（48、140和319像素） </li> <li> 大型預覽（Web轉譯 — 1280像素） </li><li> 中繼資料和文字擷取。</li></ul> |
| [自訂設定](#standard-config) | 由管理員透過使用者介面進行設定。 透過擴充預設選項，為產生轉譯提供更多選項。 擴充現成可用的選項，以提供不同的格式和轉譯。 | <ul><li>FPO轉譯。 </li> <li>更改影像的檔案格式和解析度</li> <li> 有條件地應用於配置的檔案類型。 </li> </ul> |
| [自訂設定檔](#custom-config) | 由管理員透過使用者介面設定，透過自訂應用程式使用自訂程式碼，以呼叫 [asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). 支援雲端原生和可擴充方法中更複雜的需求。 | 請參閱 [允許的使用案例](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支援的檔案格式 {#supported-file-formats}

資產微服務支援多種檔案格式，以處理、產生轉譯或擷取中繼資料。 請參閱 [支援的檔案格式](file-format-support.md) 以取得MIME類型的完整清單，以及每種類型支援的功能。

## 預設設定 {#default-config}

有些預設值會預先設定，以確保Experience Manager中需要的預設轉譯可供使用。 預設設定也可確保中繼資料擷取和文字擷取作業可供使用。 使用者可以立即開始上傳或更新資產，且基本處理預設可供使用。

使用預設設定時，只會設定最基本的處理設定檔。 此類處理設定檔在使用者介面上不可見，且您無法加以修改。 系統一律會執行以處理上傳的資產。 此類預設處理設定檔可確保 [!DNL Experience Manager] 已完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準配置 {#standard-config}

[!DNL Experience Manager] 根據使用者需求，提供針對常用格式產生更特定轉譯的功能。 管理員可以建立其他 [!UICONTROL 處理設定檔] 以便建立此類轉譯。 然後，使用者將一或多個可用的設定檔指派給特定資料夾，以完成其他處理作業。 例如，額外的處理可產生網頁、行動裝置和平板電腦的轉譯。 以下影片說明如何建立和套用 [!UICONTROL 處理設定檔] 以及如何存取已建立的轉譯。

* **轉譯寬度和高度**:格式副本寬度和高度規範可提供生成的輸出影像的最大大小。 資產微服務會嘗試產生最大可能的轉譯，其寬度和高度分別不大於指定的寬度和高度。 長寬比會保留，與原始的相同。 空白值表示資產處理會假設原始影像的像素維度。

* **MIME類型包含規則**:處理具有特定MIME類型的資產時，系統會先根據轉譯規格的排除MIME類型值檢查MIME類型。 如果符合該清單，則不會為資產產生此特定轉譯（已封鎖清單）。 否則，會根據包含的MIME類型檢查MIME類型，如果該類型與清單匹配，則生成格式副本（允許的清單）。

* **特殊FPO轉譯**:將大型資產從 [!DNL Experience Manager] into [!DNL Adobe InDesign] 文檔，創意專家等了很長時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，用戶被阻止使用 [!DNL InDesign]. 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可暫時將小型轉譯放置在 [!DNL InDesign] 以開頭的檔案，稍後可以隨選以完整解析度的資產取代。 [!DNL Experience Manager] 提供僅用於版位(FPO)的轉譯。 這些FPO轉譯的檔案大小很小，但外觀比例相同。

處理設定檔可包含FPO（僅限For Placement）轉譯。 請參閱 [!DNL Adobe Asset Link] [檔案](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 以了解您是否需要為處理設定檔開啟此功能。 如需詳細資訊，請參閱 [Adobe資產連結完成檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html).

### 建立標準設定檔 {#create-standard-profile}

若要建立標準處理設定檔，請依照下列步驟操作：

1. 管理員存取 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**. 按一下&#x200B;**[!UICONTROL 建立]**。
1. 提供名稱，協助您在套用至資料夾時唯一識別設定檔。
1. 若要產生FPO轉譯，請在 **[!UICONTROL 影像]** 標籤，啟用 **[!UICONTROL 建立FPO轉譯]**. 輸入 **[!UICONTROL 品質]** 值介於1和100之間。
1. 若要產生其他轉譯，請按一下 **[!UICONTROL 新增]** 並提供下列資訊：

   * 每個格式副本的檔案名。
   * 每個轉譯的檔案格式(PNG、JPEG、GIF或WebP)。
   * 每個轉譯的寬度和高度（像素）。 如果未指定值，則使用原始影像的全像素大小。
   * 每個JPEG和WebP轉譯的品質百分比。
   * 包含和排除的MIME類型，以定義設定檔的適用性。

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自訂設定檔和使用案例 {#custom-config}

此 [!DNL Asset Compute Service] 支援多種使用案例，例如預設處理、處理Adobe特定格式(例如Photoshop檔案)，以及實作自訂或組織特定處理。 過去需要的DAM更新資產工作流程自訂會自動處理，或透過處理設定檔設定。 如果這些處理選項不能滿足業務需求，Adobe建議開發和使用 [!DNL Asset Compute Service] 以擴充預設功能。 如需概觀，請參閱 [了解擴充性，以及何時使用](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe建議僅在無法使用預設配置或標準配置檔案完成業務需求時使用自定義應用程式。

它可以將影像、視訊、檔案和其他檔案格式轉換為不同的轉譯，包括縮圖、擷取的文字和中繼資料，以及封存。

開發人員可使用 [!DNL Asset Compute Service] to [建立自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) 以了解支援的使用案例。 [!DNL Experience Manager] 可使用管理員設定的自訂設定檔，從使用者介面呼叫這些自訂應用程式。 [!DNL Asset Compute Service] 支援以下叫用外部服務的使用案例：

* 使用 [!DNL Adobe Photoshop]&#39;s [ImageCutout API](https://developer.adobe.com/photoshop/photoshop-api-docs/) 並將結果儲存為轉譯。
* 呼叫協力廠商系統以更新資料，例如PIM系統。
* 使用 [!DNL Photoshop] API以根據Photoshop範本產生各種轉譯。
* 使用 [Adobe Lightroom API](https://developer.adobe.com/photoshop/photoshop-api-docs/) 將擷取的資產最佳化，並將其儲存為轉譯。

>[!NOTE]
>
>您無法使用自訂應用程式編輯標準中繼資料。 您只能修改自訂中繼資料。

### 建立自訂設定檔 {#create-custom-profile}

若要建立自訂設定檔，請執行下列步驟：

1. 管理員存取 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**. 按一下&#x200B;**[!UICONTROL 建立]**。
1. 按一下 **[!UICONTROL 自訂]** 標籤。 按一下 **[!UICONTROL 新增]**. 提供所需的轉譯檔案名稱。
1. 提供下列資訊。

   * 每個轉譯的檔案名和支援的副檔名。
   * [App Builder自訂應用程式的端點URL](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). 應用程式必須來自與Experience Manager帳戶相同的組織。
   * 將服務參數添加到 [將額外資訊或參數傳遞至自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * 已包含和排除的MIME類型，以將處理限制為少數特定檔案格式。

   按一下「**[!UICONTROL 儲存]**」。

自定義應用程式無頭 [專案應用程式產生器](https://developer.adobe.com/app-builder/docs/overview/) 應用程式。 如果您的自訂應用程式是以處理設定檔設定，則會取得所有提供的檔案。 應用程式必須篩選檔案。

>[!CAUTION]
>
>如果App Builder應用程式和 [!DNL Experience Manager] 帳戶不來自同一個組織，整合無法運作。

### 自訂設定檔的範例 {#custom-profile-example}

為了說明自訂設定檔的使用方式，我們將考慮使用案例，將一些自訂文字套用至促銷活動影像。 您可以建立處理設定檔，利用Photoshop API來編輯影像。

asset compute服務整合可讓Experience Manager使用 [!UICONTROL 服務參數] 欄位。 接著，自訂應用程式會呼叫Photoshop API，並將這些值傳遞至API。 例如，您可以傳遞字型名稱、文字顏色、文字粗細和文字大小，將自訂文字新增至促銷活動影像。

<!-- TBD: Check screenshot against the interface. -->

![自訂處理設定檔](assets/custom-processing-profile.png)

*圖：使用 [!UICONTROL 服務參數] 欄位，將新增的資訊傳遞至自訂應用程式中預先定義的參陣列建。 在此範例中，上傳促銷活動影像時，影像會以 `Jumanji` 文字 `Arial-BoldMT` 字型。*

## 使用處理設定檔來處理資產 {#use-profiles}

建立其他自訂處理設定檔，並套用至特定資料夾，以便Experience Manager處理上傳至或更新在這些資料夾中的資產。 預設的內建標準處理設定檔一律會執行，但使用者介面上不會顯示。 如果您新增自訂設定檔，則兩個設定檔都用來處理上傳的資產。

使用下列其中一種方法，將處理設定檔套用至資料夾：

* 管理員可在 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**，以及使用 **[!UICONTROL 將配置檔案應用到資料夾]** 動作。 它會開啟內容瀏覽器，讓您導覽至特定資料夾、選取資料夾並確認設定檔的應用程式。
* 使用者可以在Assets使用者介面中選取資料夾，請使用 **[!UICONTROL 屬性]** 操作以開啟資料夾屬性螢幕，按一下 **[!UICONTROL 資產處理]** 標籤中 [!UICONTROL 處理設定檔] 清單中，為該資料夾選取適當的處理設定檔。 若要儲存變更，請按一下 **[!UICONTROL 儲存並關閉]**.
   ![從「資產屬性」標籤將處理設定檔套用至資料夾](assets/folder-properties-processing-profile.png)

* 使用者可以在「資產」使用者介面中選取資料夾或特定資產，以套用處理設定檔，然後選取 ![資產重新處理圖示](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL 重新處理資產]** 選項。

>[!TIP]
>
>只能將一個處理設定檔套用至資料夾。 若要產生更多轉譯，請新增更多轉譯定義至現有的處理設定檔。

將處理設定檔套用至資料夾後，此資料夾或其任何子資料夾中已上傳（或更新）的所有新資產都會使用設定的其他處理設定檔進行處理。 此處理方式除了標準預設設定檔之外。

>[!NOTE]
>
>套用至資料夾的處理設定檔適用於整個樹狀結構，但可能與套用至子資料夾的其他設定檔重疊。 當資產上傳至資料夾時，Experience Manager會檢查容納資料夾的屬性以取得處理設定檔。 如果未套用任何資料夾，則會檢查階層中的父資料夾以套用處理設定檔。

若要確認已處理資產，請在 [!UICONTROL 轉譯] 檢視。 開啟資產預覽並開啟左側邊欄以存取 **[!UICONTROL 轉譯]** 檢視。 處理設定檔中的特定轉譯（特定資產的類型與MIME類型包含規則相符）應可見且可供存取。

![其他轉譯](assets/renditions-additional-renditions.png)

*圖：處理設定檔套用至上層資料夾時產生的兩個額外轉譯範例。*

## 後置處理工作流程 {#post-processing-workflows}

若是使用處理設定檔無法達成的資產需要額外處理的情況，可將其他後續處理工作流程新增至設定。 後置處理可讓您在使用資產微服務的可設定處理之上新增完全自訂的處理。

後置處理工作流程，或 [自動啟動工作流程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html)，則會自動由執行 [!DNL Experience Manager] 微服務處理完成後。 不需要手動新增工作流程啟動器來觸發工作流程。 範例包括：

* 處理資產的自訂工作流程步驟。
* 整合功能，可從外部系統將中繼資料或屬性新增至資產，例如產品或程式資訊。
* 由外部服務完成的其他處理。

若要新增後續處理工作流程設定至 [!DNL Experience Manager]，請遵循下列步驟：

* 建立一或多個工作流模型。 這些自訂模型稱為 *後置處理工作流程模型* 。 那些是常規的 [!DNL Experience Manager] 工作流程模型。
* 將所需的工作流程步驟新增至這些模型。 檢閱預設工作流程的步驟，並將所有必要的預設步驟新增至自訂工作流程。 步驟會根據工作流程模型設定對資產執行。 例如，如果您希望智慧標籤在資產上傳時自動發生，請將步驟新增至自訂後置處理工作流程模型。
* 新增 [!UICONTROL DAM更新資產工作流程已完成程式] 最後一步。 新增此步驟可確保Experience Manager知道處理何時結束，且資產可標示為已處理，即 *新增* 會顯示在資產上。
* 為「自訂工作流程執行者服務」建立設定，可讓您透過路徑（資料夾位置）或規則運算式來設定處理後工作流程模型的執行。

如需可在後續處理工作流程中使用標準工作流程步驟的詳細資訊，請參閱 [後置處理工作流程中的工作流程步驟](developer-reference-material-apis.md#post-processing-workflows-steps) 在開發人員參考中。

### 建立後置處理工作流程模型 {#create-post-processing-workflow-models}

後置處理工作流程模型是固定的 [!DNL Experience Manager] 工作流程模型。 如果您需要針對不同存放庫位置或資產類型進行不同處理，請建立不同的模型。

視需要新增處理步驟。 您可以同時使用可用的支援步驟，以及任何自訂實作的工作流程步驟。

請確定每個後置處理工作流程的最後一個步驟是 `DAM Update Asset Workflow Completed Process`. 最後一個步驟有助於確保Experience Manager知道資產處理何時完成。

### 設定後置處理工作流程執行 {#configure-post-processing-workflow-execution}

資產微服務完成上傳資產的處理後，您可以定義後置處理工作流程以進一步處理資產。 若要使用工作流程模型來設定後續處理，您可以執行下列其中一項操作：

* [在資料夾屬性中套用工作流程模型](#apply-workflow-model-to-folder).
* [設定自訂工作流程執行者服務](#configure-custom-workflow-runner-service).

#### 將工作流模型應用於資料夾 {#apply-workflow-model-to-folder}

對於典型的後置處理使用案例，請考慮使用方法將工作流程套用至資料夾。 在資料夾中應用工作流模型 [!UICONTROL 屬性]，請遵循下列步驟：

1. 建立工作流模型。
1. 選取資料夾，按一下 **[!UICONTROL 屬性]** ，然後按一下 **[!UICONTROL 資產處理]** 標籤。
1. 在 **[!UICONTROL 自動啟動工作流程]**，選取所需的工作流程，提供工作流程的標題，然後儲存變更。

   ![將後處理工作流程套用至其屬性中的資料夾](assets/post-processing-profile-workflow-for-folders.png)

#### 設定自訂工作流程執行者服務 {#configure-custom-workflow-runner-service}

您可以為無法透過將工作流程套用至資料夾而輕鬆履行的進階設定，設定自訂工作流程執行者服務。 例如，使用規則運算式的工作流程。 Adobe CQ DAM自訂工作流程執行者(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服務。 它提供下列兩個設定選項：

* 依路徑的後置處理工作流程(`postProcWorkflowsByPath`):可以根據不同的存放庫路徑列出多個工作流程模型。 使用冒號分隔路徑和模型。 支援簡單的存放庫路徑。 將這些對應至 `/var` 路徑。 例如： `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* 依運算式的後置處理工作流程(`postProcWorkflowsByExpression`):可以根據不同的規則運算式列出多個工作流程模型。 運算式和模型應以冒號分隔。 規則運算式應直接指向「資產」節點，而非任何一個轉譯或檔案。 例如： `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

要了解如何部署OSGi配置，請參閱 [部署至 [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### 停用後處理工作流程執行

當不需要後置處理時，請在 __自動啟動工作流程__ 中。

##### 建立禁用的自動啟動工作流模型

1. 導覽至 __「工具」>「工作流」>「模型」__
1. 選擇 __建立>建立模型__ 形成頂端動作列
1. 提供新工作流模型的標題和名稱，例如：
   * 標題：禁用自動啟動工作流
   * 名稱：disable-auto-start-workflow
1. 選擇 __完成__ 建立工作流模型
1. __選擇__ 和 __編輯__ 新建立的工作流模型
1. 在「工作流模型」編輯器中，選擇 __步驟1__ 從模型定義中刪除
1. 開啟 __側面板__，然後選取 __步驟__
1. 拖曳 __DAM更新資產工作流程已完成__ 進入模型定義
1. 選取 __頁面資訊__ 按鈕(在 __側面板__ 切換)，然後選取 __開啟屬性__
1. 在 __基本__ 索引標籤，選取 __暫時性工作流程__
1. 選擇 __儲存並關閉__ 從頂端動作列
1. 選擇 __同步__ 在頂端動作列中
1. 關閉工作流模型編輯器

##### 應用禁用的自動啟動工作流模型

請依照 [將工作流模型應用到資料夾](#apply-workflow-model-to-folder) 並設定 __禁用自動啟動工作流__ 作為 __自動啟動工作流程__ 若為資料夾，不需要資產的後期處理。

## 最佳實務和限制 {#best-practices-limitations-tips}

* 設計工作流程時，請考量您對所有轉譯類型的需求。 如果您預計未來不需要轉譯，請從工作流程移除其建立步驟。 之後無法大量刪除轉譯。 長時間使用後，您可能會佔用大量儲存空間 [!DNL Experience Manager]. 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂 [!DNL Experience Manager] 刪除特定轉譯或刪除資產，然後再次上傳這些資產。
* 目前，支援僅限於產生轉譯。 不支援產生新資產。
* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳非常大型的資產時，有時中繼資料擷取作業會失敗。

>[!MORELIKETHIS]
>
>* [asset compute服務簡介](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [了解擴充性，以及其使用時機](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [如何建立自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html).
>* [各種使用案例支援的MIME類型](/help/assets/file-format-support.md).


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
