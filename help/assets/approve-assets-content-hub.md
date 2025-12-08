---
title: 核准 Content Hub 的資產
description: 瞭解如何在Assets as a Cloud Service中核准資產，以便在Content Hub中使用。
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: aec2bd06ad498e92ce1e69ac587ee7fcd5106268
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 17%

---

# 核准 Content Hub 的資產 {#approve-assets-content-hub}

![核准Content Hub的資產](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

品牌經理和行銷人員對品牌資產維持嚴格的控制。 Content Hub內只能使用已核准且最新的資產版本，確保所有管道和應用程式的品牌一致性。

您可以使用AEM Assets as a Cloud Service核准資產，以簡化資產管理，確保處理資產的控制和有效率。

## 開始之前 {#pre-requisites}

開始之前，您應該先執行以下操作：

* 存取AEM Assets as a Cloud Service

* 寫入許可權可編輯資產中繼資料，以便能夠編輯資產&#x200B;**[!UICONTROL 資產屬性]**&#x200B;中可用的[狀態](/help/assets/manage-organize-assets-view.md##manage-asset-status)欄位。

## 核准 Content Hub 的資產{#approve-assets-for-content-hub}

在Assets as a Cloud Service中標示為`approved`的資產會自動在Content Hub中使用。

>[!NOTE]
>
>Assets as a Cloud Service和Content Hub必須使用相同的組織，資產才能在Content Hub中顯示。

若要使用AEM as a Cloud Service中的Assets檢視將資產狀態設為`approved`：

1. 選取該資產，然後按一下工具列中的「**[!UICONTROL 詳細資料]**」。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，從`approved`狀態&#x200B;**[!UICONTROL 下拉式清單中選取資產狀態為]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

如果您需要使用管理員檢視核准資產，請參閱[使用管理員檢視核准資產](/help/assets/approve-assets.md#approve-assets)。

## 使用Assets檢視大量核准Content Hub的資產 {#bulk-approve-assets-content-hub}

使用AEM Assets as a Cloud Service的Assets檢視大量核准資產。 所有資產，經大量核准後，即可在Content Hub中使用。

若要在Assets檢視中，大量核准資料夾內的資產：

1. 選取資產，然後按一下「**[!UICONTROL 大量中繼資料編輯]**」。

1. 在右側面板「[!UICONTROL 屬性]」區段內提供的「**[!UICONTROL 狀態]**」欄位中，選取「**[!UICONTROL 已核准]**」。

1. 按一下「**[!UICONTROL 儲存]**」。

## 設定核准目標 {#set-approval-target}

Assets檢視可讓您根據您在「資產詳細資料」頁面上的&#x200B;**核准目標**&#x200B;欄位中設定的值，使用OpenAPI功能、Content Hub或兩者將已核准的資產發佈到Dynamic Media。

若要設定核准目標：

1. 選取該資產，然後按一下工具列中的「**[!UICONTROL 詳細資料]**」。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 狀態]**&#x200B;下拉式清單中選取資產狀態。 可能的值包括「已核准」、「已拒絕」以及「無狀態」(預設)。

1. 如果您在步驟2中選取&#x200B;**已核准**，請選取核准目標。 可能的值包括「傳送」和「Content Hub」。

   * **傳送**&#x200B;是下拉式功能表中選取的預設選項，而且會透過OpenAPI[將資產發佈至](/help/assets/dynamic-media-open-apis-overview.md)Dynamic Media與[Content Hub](/help/assets/product-overview.md) (如果兩者都針對Experience Manager Assets啟用)。

   * 選取&#x200B;**Content Hub**&#x200B;會將資產發佈至Content Hub。 只有在為Experience Manager Assets啟用Content Hub時，它才會顯示為選項。

   * 如果您未從下拉式清單中選取選項，則為您的AEM as a Cloud Service環境啟用的預設選項會自動套用至資產。


   如需可用選項的詳細資訊，請參閱[已核准資產的預設核准目標和發佈目的地](#default-approval-target-options-publish-destinations)。

   ![核准狀態](/help/assets/assets/approval-status-delivery.png)

1. 指定其他資產屬性，然後按一下&#x200B;**[!UICONTROL 儲存]**。

其他需要注意的要點包括：

* 當您未使用預設的中繼資料表單且無法檢視&#x200B;**[!UICONTROL 核准目標]**&#x200B;欄位時，[編輯您的中繼資料表單](/help/assets/metadata-assets-view.md#metadata-forms)以將&#x200B;**[!UICONTROL 的]**&#x200B;核准欄位從可用元件拖曳到中繼資料表單，然後按一下&#x200B;**[!UICONTROL 儲存]**。

* 當您使用Assets檢視選取核准目標為`Content Hub`時，資產便可在Content Hub中提供給屬於相同組織的使用者使用。

### 已核准資產的預設核准目標和發佈目的地 {#default-approval-target-options-publish-destinations}

下表說明在您的AEM as a Cloud Service環境中使用OpenAPI和Content Hub啟用DM而顯示`Approval Target`下拉式清單和預設核准目標的先決條件：

| 動態媒體與OpenAPI | Content Hub | 是否要顯示核准目標下拉式清單？ | 已核准資產的預設核准目標 | 發佈目的地 |
| --- | --- | --- | --- |---|
| 已啟用 | 已啟用 | 是 | 傳遞 | Dynamic Media (含OpenAPI和Content Hub) |
| 未啟用 | 已啟用 | 是 | Content Hub | Content Hub |
| 已啟用 | 未啟用 | 是 | 傳遞 | 動態媒體與OpenAPI |
| 未啟用 | 未啟用 | 否 | N/A | N/A |

## 在管理員檢視中自動核准新擷取的資產 {#automate-approval-newly-ingested-assets}

從Assets檢視切換到「管理員」檢視後，您可以設定資料夾設定，好讓所有新增至資料夾的新資產都能自動獲得核准。

您可以透過下列方式，在管理員和Assets檢視之間切換：
![我的Workspace總覽](assets/assets-view.png)

請依照下列步驟，自動核准[!DNL Experience Manager Admin view]中新擷取的資產：

1. 在作者環境中建立資料夾(https://author-pXXX-eYYY.adobeaemcloud.com)。 將&#x200B;_XXX_&#x200B;取代為您的方案ID，並將&#x200B;_YYYY_&#x200B;取代為Experience Manager中的環境ID。
1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**。
1. 按一下頁面右上方的&#x200B;**[!UICONTROL 「建立]**」。
1. 新增設定檔標題並按一下&#x200B;**[!UICONTROL 建立]**。 已成功建立中繼資料設定檔。
1. 選取新建立的中繼資料設定檔，然後按一下&#x200B;**[!UICONTROL 編輯&#x200B;_(e)_]**。 <br>會開啟&#x200B;**[!UICONTROL 編輯中繼資料設定檔]**表單，並反白顯示&#x200B;**[!UICONTROL 基本]**索引標籤。
1. 將&#x200B;**[!UICONTROL 單行文字欄位]**&#x200B;從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖放到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_已核准的Assets_。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至_。/jcr:content/metadata/dam :status_。
   1. 將預設值變更為&#x200B;_已核准_。

1. 與步驟6類似，將&#x200B;**[!UICONTROL 單行文字欄位]**&#x200B;從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖曳到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_啟用目標_。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至_。/jcr:content/metadata/dam :activationTarget_。
   1. 將預設值變更為&#x200B;_contenthub_。

1. 按一下&#x200B;**[!UICONTROL 儲存]**。
1. 在&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面中，選取新建立的中繼資料設定檔。
1. 按一下頂端動作列中的&#x200B;**[!UICONTROL 套用中繼資料設定檔至資料夾]**。
1. 選取您需要核准的資料夾，然後按一下[套用]。****
   <br>整個資料夾的許可權已設定為待核准，且任何上傳至此資料夾的資產都會自動核准。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>此方法會核准資料夾中新建立的資產。 針對資料夾中的現有資產，您需要手動選取並核准它們。

## 管理使用Content Hub上傳的資產 {#manage-assets-uploaded-using-content-hub}

[有權新增資產的Content Hub使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)可以從本機檔案系統，或從OneDrive或Dropbox資料來源匯入資產，將[資產新增至Content Hub](/help/assets/upload-brand-approved-assets.md)。 不論本機檔案系統或OneDrive和Dropbox資料來源提供的檔案夾結構為何，所有資產都會顯示在Content Hub的頂層，以增強搜尋功能。

是否顯示使用Content Hub上傳的資產，取決於您是否已啟用[自動核准切換](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)：

* 如果啟用&#x200B;**[!UICONTROL 自動核准]**&#x200B;切換開關，您使用 Content Hub 上傳的資產則會自動顯示。

* 如果停用&#x200B;**[!UICONTROL 自動核准]**&#x200B;切換開關，您使用 Content Hub 上傳的資產就不會自動顯示。這些資產會顯示在您 Assets as a Cloud Service 環境的 `hydrated-assets` 資料夾中。導覽至該資料夾，並將資產狀態[大量編輯](#bulk-approve-assets-content-hub)為 `Approved`，使資產顯示於 Content Hub 中。

![Content Hub核准流程](/help/assets/assets/content-hub-approval.png)
