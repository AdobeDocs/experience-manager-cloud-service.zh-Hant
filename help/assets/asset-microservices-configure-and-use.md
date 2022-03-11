---
title: 配置和使用資產微服務
description: 配置和使用雲本地資產微服務以按規模處理資產。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 9645cf2ef95c41b8d319bb22eb4d69bd11525eca
workflow-type: tm+mt
source-wordcount: '2704'
ht-degree: 0%

---

# 使用資產微服務和處理配置檔案 {#get-started-using-asset-microservices}

資產微服務使用雲本機應用程式（也稱為工作程式）提供可擴展和彈性的資產處理。 Adobe管理服務，以便優化對不同資產類型和處理選項的處理。

資產微服務允許您處理 [各種檔案類型](/help/assets/file-format-support.md) 比以前版本的 [!DNL Experience Manager]。 例如，現在可以對PSD和PSB格式進行縮略圖提取，但以前需要的第三方解決方案，如 [!DNL ImageMagick]。

資產處理取決於中的配置 **[!UICONTROL 處理配置檔案]**。 Experience Manager提供基本預設設定，並讓管理員添加更具體的資產處理配置。 管理員建立、維護和修改後處理工作流的配置，包括可選的自定義。 自定義工作流使開發人員可以擴展預設產品。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高級視圖](assets/asset-microservices-flow.png "資產處理的高級視圖")

>[!NOTE]
>
>此處介紹的資產處理取代了 `DAM Update Asset` 早期版本的工作流模型 [!DNL Experience Manager]。 大多數標準格式副本生成和與元資料相關的步驟被資產微服務處理替換，而剩餘的步驟（如果有）可被後處理工作流配置替換。

## 瞭解資產處理選項 {#get-started}

[!DNL Experience Manager] 允許以下處理級別。

| 選項 | 說明 | 涵蓋的使用案例 |
|---|---|---|
| [預設設定](#default-config) | 它原樣可用，無法修改。 此配置提供了非常基本的格式副本生成功能。 | <ul> <li>標準縮略圖 [!DNL Assets] 用戶介面（48、140和319像素） </li> <li> 大預覽（Web格式副本 — 1280像素） </li><li> 元資料和文本提取。</li></ul> |
| [自定義配置](#standard-config) | 由管理員通過用戶介面配置。 通過擴展預設選項為生成格式副本提供更多選項。 擴展現成選項以提供不同的格式和格式副本。 | <ul><li>FPO格式副本。 </li> <li>更改影像的檔案格式和解析度</li> <li> 有條件地應用於已配置的檔案類型。 </li> </ul> |
| [自定義配置檔案](#custom-config) | 由管理員通過用戶介面配置以通過自定義應用程式使用自定義代碼來調用 [asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html)。 支援雲本地和可擴展方法中更複雜的要求。 | 請參閱 [允許的使用案例](#custom-config)。 |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支援的檔案格式 {#supported-file-formats}

Asset Microservices支援多種檔案格式以處理、生成格式副本或提取元資料。 請參閱 [支援的檔案格式](file-format-support.md) MIME類型的完整清單以及每種類型支援的功能。

## 預設設定 {#default-config}

已預配置某些預設設定，以確保Experience Manager中所需的預設格式副本可用。 預設配置還確保元資料提取和文本提取操作可用。 用戶可以立即開始上載或更新資產，並且預設情況下基本處理可用。

使用預設配置時，只配置最基本的處理配置檔案。 這種處理配置檔案在用戶介面上不可見，您無法修改它。 它始終執行以處理上載的資產。 這樣的預設處理配置檔案可確保滿足 [!DNL Experience Manager] 完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準配置 {#standard-config}

[!DNL Experience Manager] 根據用戶的需要，提供為通用格式生成更具體格式副本的功能。 管理員可以建立其他 [!UICONTROL 處理配置檔案] 以便建立此格式副本。 然後，用戶將一個或多個可用配置檔案分配給特定資料夾以完成附加處理。 例如，附加處理可以生成Web、Mobile和Tablet的格式副本。 以下視頻說明了如何建立和應用 [!UICONTROL 處理配置檔案] 以及如何訪問已建立的格式副本。

* **格式副本寬度和高度**:格式副本寬度和高度規範提供了所生成輸出影像的最大大小。 Asset Microservices嘗試生成最大可能的格式副本，其寬度和高度分別不大於指定的寬度和高度。 保留長寬比，即與原件相同。 空值表示資產處理假定原始影像的像素尺寸。

* **MIME類型包含規則**:處理具有特定MIME類型的資產時，首先根據格式副本規範的排除的MIME類型值檢查MIME類型。 如果與該清單匹配，則不會為資產（阻止的清單）生成此特定格式副本。 否則，將根據包含的MIME類型檢查MIME類型，如果它與清單匹配，則生成格式副本（允許清單）。

* **特殊FPO格式副本**:將大型資產 [!DNL Experience Manager] 入 [!DNL Adobe InDesign] 文檔，一個有創意的專業人士，等到他們 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html)。 同時，用戶被阻止使用 [!DNL InDesign]。 這會中斷創意流，並對用戶體驗造成負面影響。 Adobe允許臨時將小型格式副本放在 [!DNL InDesign] 文檔開始，稍後可以用全解析度資產按需替換。 [!DNL Experience Manager] 提供僅用於放置的格式副本(FPO)。 這些FPO格式副本的檔案大小較小，但長寬比相同。

處理配置檔案可以包括FPO（僅用於放置）格式副本。 請參閱 [!DNL Adobe Asset Link] [文檔](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 瞭解是否需要開啟處理配置檔案。 有關詳細資訊，請參見 [Adobe資產連結完成文檔](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

### 建立標準配置檔案 {#create-standard-profile}

要建立標準處理配置檔案，請執行以下步驟：

1. 管理員訪問 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理配置檔案]**。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 提供一個名稱，幫助您在應用到資料夾時唯一標識配置檔案。
1. 要生成FPO格式副本，請在 **[!UICONTROL 影像]** 頁籤，啟用 **[!UICONTROL 建立FPO格式副本]**。 輸入a **[!UICONTROL 質量]** 值介於1和100之間。
1. 要生成其他格式副本，請按一下 **[!UICONTROL 添加新]** 並提供以下資訊：

   * 每個格式副本的檔案名。
   * 每個格式副本的檔案格式(PNG、JPEG、GIF或WebP)。
   * 每個格式副本的寬度和高度（以像素為單位）。 如果未指定這些值，則使用原始影像的全像素大小。
   * 每個JPEG和WebP格式副本的質量百分比。
   * 包含和排除的MIME類型以定義配置檔案的適用性。

   ![處理配置檔案添加](assets/processing-profiles-image.png)

1. 按一下「**[!UICONTROL 儲存]**」。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自定義配置檔案和使用案例 {#custom-config}

的 [!DNL Asset Compute Service] 支援各種使用情形，如預設處理、處理特定於Adobe的格式(如Photoshop檔案)，以及實施自定義或特定於組織的處理。 過去需要的DAM更新資產工作流自定義，可以自動處理，也可以通過處理配置檔案配置進行處理。 如果這些處理選項不能滿足業務需求，Adobe建議開發和使用 [!DNL Asset Compute Service] 擴展預設功能。 有關概述，請參閱 [瞭解可擴充性以及何時使用](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)。

>[!NOTE]
>
>Adobe建議僅在無法使用預設配置或標準配置檔案完成業務需求時使用自定義應用程式。

它可以將影像、視頻、文檔和其他檔案格式轉換為不同的格式副本，包括縮略圖、提取的文本和元資料，以及存檔。

開發人員可以 [!DNL Asset Compute Service] 至 [建立自定義應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) 支援的使用案例。 [!DNL Experience Manager] 可以使用管理員配置的自定義配置檔案從用戶介面調用這些自定義應用程式。 [!DNL Asset Compute Service] 支援以下調用外部服務的使用情形：

* 使用 [!DNL Adobe Photoshop]`s [ImageCutout API](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) 並將結果另存為格式副本。
* 調用第三方系統以更新資料，例如PIM系統。
* 使用 [!DNL Photoshop] API，用於根據Photoshop模板生成各種格式副本。
* 使用 [Adobe LightroomAPI](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) 以優化所攝取的資產，並將其另存為格式副本。

>[!NOTE]
>
>無法使用自定義應用程式編輯標準元資料。 您只能修改自定義元資料。

### 建立自定義配置檔案 {#create-custom-profile}

要建立自定義配置檔案，請執行以下步驟：

1. 管理員訪問 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理配置檔案]**。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 按一下 **[!UICONTROL 自定義]** 頁籤。 按一下 **[!UICONTROL 添加新]**。 提供所需的格式副本檔案名。
1. 提供以下資訊。

   * 每個格式副本的檔案名和支援的檔案副檔名。
   * [Firefly自定義應用的端點URL](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html)。 應用必須與Experience Manager帳戶來自同一組織。
   * 將服務參數添加到 [將額外資訊或參數傳遞給自定義應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend)。
   * 包含和排除的MIME類型可將處理限制為少數特定的檔案格式。

   按一下「**[!UICONTROL 儲存]**」。

定制應用程式是無頭的 [螢火蟲計畫](https://github.com/AdobeDocs/project-firefly) 。 如果使用處理配置檔案設定了自定義應用程式，則會獲取所有提供的檔案。 應用程式必須篩選檔案。

>[!CAUTION]
>
>如果螢火蟲的應用和 [!DNL Experience Manager] 帳戶不來自同一組織，整合無效。

### 自定義配置檔案的示例 {#custom-profile-example}

要說明自定義配置檔案的用法，讓我們考慮使用案例將一些自定義文本應用於市場活動影像。 您可以建立利用PhotoshopAPI編輯映像的處理配置檔案。

asset compute服務整合允許Experience Manager使用 [!UICONTROL 服務參數] 的子菜單。 然後，自定義應用程式調用PhotoshopAPI並將這些值傳遞給API。 例如，您可以傳遞字型名稱、文本顏色、文本粗細和文本大小，以將自定義文本添加到市場活動影像。

<!-- TBD: Check screenshot against the interface. -->

![自定義處理配置檔案](assets/custom-processing-profile.png)

*圖：使用 [!UICONTROL 服務參數] 欄位，將添加的資訊傳遞給構建到自定義應用程式中的預定義參數。 在此示例中，當上載市場活動映像時，映像將更新為 `Jumanji` 文本 `Arial-BoldMT` 字型。*

## 使用處理配置檔案處理資產 {#use-profiles}

建立附加的自定義處理配置檔案並將其應用到特定資料夾，以便Experience Manager處理上載到這些資料夾或在這些資料夾中更新的資產。 預設的內置標準處理配置檔案始終執行，但在用戶介面上不可見。 如果添加自定義配置檔案，則兩個配置檔案都用於處理上載的資產。

使用以下方法之一將處理配置檔案應用於資料夾：

* 管理員可以在中選擇處理配置檔案定義 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理配置檔案]**，使用 **[!UICONTROL 將配置檔案應用到資料夾]** 操作。 它開啟一個內容瀏覽器，允許您導航到特定資料夾，選擇它們並確認配置檔案的應用程式。
* 用戶可以在「資產」用戶介面中選擇資料夾，使用 **[!UICONTROL 屬性]** 操作以開啟資料夾屬性螢幕，按一下 **[!UICONTROL 資產處理]** 的 [!UICONTROL 處理配置檔案] 清單中，選擇該資料夾的相應處理配置檔案。 要保存更改，請按一下 **[!UICONTROL 保存並關閉]**。
   ![將處理配置檔案應用到「資產屬性」頁籤中的資料夾](assets/folder-properties-processing-profile.png)

* 用戶可以在「資產」用戶介面中選擇資料夾或特定資產以應用處理配置檔案，然後選擇 ![資產重新處理表徵圖](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL 重新處理資產]** 的上界。

>[!TIP]
>
>只能將一個處理配置檔案應用於資料夾。 要生成更多格式副本，請將更多格式副本定義添加到現有處理配置檔案。

在將處理配置檔案應用到資料夾後，使用此資料夾或其任何子資料夾中上載（或更新）的所有新資產都使用配置的附加處理配置檔案進行處理。 此處理是標準預設配置檔案的補充。

>[!NOTE]
>
>應用於資料夾的處理配置檔案適用於整個樹，但可以使用應用於子資料夾的其他配置檔案進行過載。 將資產上載到資料夾時，Experience Manager會檢查包含資料夾的屬性以查找處理配置檔案。 如果未應用任何檔案，則會檢查層次結構中的父資料夾以應用處理配置檔案。

要驗證是否處理了資產，請在 [!UICONTROL 格式副本] 左欄。 開啟資產預覽並開啟左滑軌以訪問 **[!UICONTROL 格式副本]** 的子菜單。 處理配置檔案中的特定格式副本應可見且可訪問，該特定資產的類型與MIME類型包含規則匹配。

![附加格式副本](assets/renditions-additional-renditions.png)

*圖：由應用於父資料夾的處理配置檔案生成的兩個附加格式副本的示例。*

## 後處理工作流 {#post-processing-workflows}

對於需要額外處理無法使用處理配置檔案實現的資產的情況，可以將附加的後處理工作流添加到配置中。 後期處理允許您在使用資產微服務的可配置處理之上添加完全定製的處理。

後處理工作流（如果已配置）由自動執行 [!DNL Experience Manager] 在微服務處理完成後。 無需手動添加工作流啟動程式來觸發工作流。 示例包括：

* 處理資產的自定義工作流步驟。
* 將元資料或屬性添加到外部系統資產的整合，例如產品或流程資訊。
* 外部服務完成的附加處理。

將後處理工作流配置添加到 [!DNL Experience Manager]，請執行以下步驟：

* 建立一個或多個工作流模型。 這些定制模型稱為 *後處理工作流模型* 在文檔中。 這些是常規的 [!DNL Experience Manager] 工作流模型。
* 將所需的工作流步驟添加到這些模型。 查看預設工作流中的步驟，並將所有必需的預設步驟添加到自定義工作流。 基於工作流模型配置對資產執行這些步驟。 例如，如果希望在資產上載時自動執行智慧標籤，請將該步驟添加到自定義後處理工作流模型。
* 添加 [!UICONTROL DAM更新資產工作流已完成流程] 最後一步。 添加此步驟可確保Experience Manager知道處理何時結束以及資產可標籤為已處理，即 *新建* 的子菜單。
* 為自定義工作流運行程式服務建立配置，該配置允許通過路徑（資料夾位置）或規則運算式配置後處理工作流模型的執行。

有關在後處理工作流中可以使用哪些標準工作流步驟的詳細資訊，請參閱 [後處理工作流中的工作流步驟](developer-reference-material-apis.md#post-processing-workflows-steps) 的子菜單。

### 建立後處理工作流模型 {#create-post-processing-workflow-models}

後處理工作流模型是常規的 [!DNL Experience Manager] 工作流模型。 如果您需要針對不同的儲存庫位置或資產類型進行不同的處理，請建立不同的模型。

根據需要添加處理步驟。 您可以同時使用兩個步驟，即可用的支援步驟，以及任何自定義實施的工作流步驟。

確保每個後處理工作流的最後一步是 `DAM Update Asset Workflow Completed Process`。 最後一步有助於確保Experience Manager知道何時完成資產處理。

### 配置後處理工作流執行 {#configure-post-processing-workflow-execution}

在資產微服務完成上載資產的處理後，您可以定義後處理工作流以進一步處理資產。 要使用工作流模型配置後處理，可以執行以下操作之一：

* [在資料夾屬性中應用工作流模型](#apply-workflow-model-to-folder)。
* [配置自定義工作流運行程式服務](#configure-custom-workflow-runner-service)。

#### 將工作流模型應用於資料夾 {#apply-workflow-model-to-folder}

對於典型的後處理使用案例，請考慮使用方法將工作流應用到資料夾。 在資料夾中應用工作流模型 [!UICONTROL 屬性]，請執行以下步驟：

1. 建立工作流模型。
1. 選擇資料夾，按一下 **[!UICONTROL 屬性]** ，然後按一下 **[!UICONTROL 資產處理]** 頁籤。
1. 下 **[!UICONTROL 自動啟動工作流]**，選擇所需的工作流，提供工作流的標題，然後保存更改。

   ![將後處理工作流應用於其「屬性」中的資料夾](assets/post-processing-profile-workflow-for-folders.png)

#### 配置自定義工作流運行程式服務 {#configure-custom-workflow-runner-service}

您可以為無法通過將工作流應用到資料夾而輕鬆實現的高級配置配置自定義工作流運行程式服務。 例如，使用規則運算式的工作流。 Adobe CQDAM自定義工作流運行程式(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服務。 它提供了以下兩個配置選項：

* 按路徑(`postProcWorkflowsByPath`):可以根據不同的儲存庫路徑列出多個工作流模型。 使用冒號分隔路徑和模型。 支援簡單的儲存庫路徑。 將這些映射到 `/var` 路徑。 例如： `/content/dam/my-brand:/var/workflow/models/my-workflow`。
* 按表達式(`postProcWorkflowsByExpression`):可以根據不同的規則運算式列出多個工作流模型。 表達式和模型應用冒號分隔。 規則運算式應直接指向「資產」節點，而不是任何格式副本或檔案。 例如： `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`。

要瞭解如何部署OSGi配置，請參見 [部署 [!DNL Experience Manager]](/help/implementing/deploying/overview.md)。

## 最佳做法和限制 {#best-practices-limitations-tips}

* 在設計工作流時考慮您對所有類型的格式副本的需求。 如果您預計將來不需要格式副本，請從工作流中刪除其建立步驟。 之後無法批量刪除格式副本。 長期使用後，不希望的格式副本可能佔用大量儲存空間 [!DNL Experience Manager]。 對於單個資產，您可以從用戶介面手動刪除格式副本。 對於多個資產，您可以自定義 [!DNL Experience Manager] 刪除特定格式副本或刪除資產並重新上載這些資產。
* 目前，支援僅限於生成格式副本。 不支援生成新資產。
* 當前，元資料提取的檔案大小限制約為15 GB。 上載超大資產時，有時元資料提取操作會失敗。

>[!MORELIKETHIS]
>
>* [asset compute服務簡介](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html)。
>* [瞭解可擴充性以及何時使用](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)。
>* [如何建立自定義應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html)。
>* [支援用於各種使用情形的MIME類型](/help/assets/file-format-support.md)。


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
