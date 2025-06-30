---
title: 在Experience Manager中核准資產
description: 瞭解如何核准 [!DNL Experience Manager]中的資產。
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 7%

---

# 核准[!DNL Experience Manager]中的資產

品牌經理和行銷人員對品牌資產維持嚴格的控制。 唯有經核准且最新版本的資產才可供使用，以確保所有管道和應用程式間的品牌一致性。

您可以在AEM Assets中核准資產，以簡化資產管理，確保處理資產的程式受到控制且有效率。

## 開始之前 {#pre-requisites}

您必須擁有AEM Assets as a Cloud Service的存取權以及編輯資產&#x200B;**[!UICONTROL 檢閱狀態]**&#x200B;屬性的許可權。

## 設定

在核准資產之前，您需要對管理員檢視中適用的中繼資料結構做一次性的更新。 您可以略過Assets檢視的此設定。 請依照下列步驟設定中繼資料結構：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
1. 選取適用的中繼資料結構描述，然後按一下&#x200B;**[!UICONTROL 編輯]**。 <br>開啟&#x200B;**[!UICONTROL 中繼資料結構表單編輯器]**，並反白顯示&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤。
1. 向下捲動並按一下&#x200B;**[!UICONTROL 檢閱狀態]**。
1. 按一下右側面板上的&#x200B;**[!UICONTROL 規則]**&#x200B;標籤。
1. 取消勾選&#x200B;**[!UICONTROL 停用編輯]**。
如果您需要檢視**[!UICONTROL 檢閱狀態]**&#x200B;欄位對應到的屬性，請瀏覽至&#x200B;**[!UICONTROL 設定]**&#x200B;標籤，並檢視&#x200B;**[!UICONTROL 對應到屬性]**&#x200B;欄位中的`./jcr:content/metadata/dam:status`值。
1. 將&#x200B;**[!UICONTROL 下拉式清單]**&#x200B;欄位從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖放到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_核准目標_。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至&#x200B;_。/jcr：content/metadata/dam：activationTarget_。
   1. 以`contenthub`和`delivery`作為選項值新增選項。

   >[!NOTE]
   >
   >當您使用Assets檢視選取核准目標為Content Hub時，屬於相同組織的使用者可在Content Hub中使用資產。 當您選取核准目標為傳送時，資產可供所有使用者使用。

1. 按一下「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
>如果您的資產或資料夾具有不同的預設結構描述，請務必在該特定結構描述中進行此更新。

## 核准資產 {#approve-assets}

若要在[!DNL Experience Manager Admin view]中核准資產，請執行下列步驟：

1. 選取資產並按一下頂端窗格中的&#x200B;**[!UICONTROL 屬性]**。
1. 在「**[!UICONTROL 基本]**」索引標籤中，向下捲動至「**[!UICONTROL 審查狀態]**」。
1. 將審查狀態變更為「**[!UICONTROL 已核准]**」。
   ![影像](/help/assets/assets/approve-old-ui.png)
1. 按一下「**[!UICONTROL 儲存並關閉]**」。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同樣地，您可以使用[新的Assets檢視](/help/assets/manage-organize-assets-view.md)核准資產。

## 大量核准資產 {#bulk-approve-assets}

一次快速核准多個資產，簡化工作流程。 您可以大量核准資產，以加快核准程式，節省時間並提高生產力。
<br>請依照下列步驟在[!DNL Experience Manager Admin view]中核准大量資產：

1. 在作者環境中建立資料夾(https://author-pXXX-eYYY.adobeaemcloud.com)。 將&#x200B;_XXX_&#x200B;取代為您的方案ID，並將&#x200B;_YYYY_&#x200B;取代為Experience Manager中的環境ID。
1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**。
1. 按一下頁面右上方的&#x200B;**[!UICONTROL 「建立]**」。
1. 新增設定檔標題並按一下&#x200B;**[!UICONTROL 建立]**。 已成功建立中繼資料設定檔。
1. 選取新建立的中繼資料設定檔，然後按一下&#x200B;**[!UICONTROL 編輯&#x200B;_(e)_]**。 <br>會開啟&#x200B;**[!UICONTROL 編輯中繼資料設定檔]**表單，並反白顯示&#x200B;**[!UICONTROL 基本]**索引標籤。
1. 將&#x200B;**[!UICONTROL 單行文字欄位]**&#x200B;從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖放到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_已核准的Assets_。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至&#x200B;_。/jcr：content/metadata/dam：status_。
   1. 將預設值變更為&#x200B;_已核准_。

1. 將&#x200B;**[!UICONTROL 下拉式清單]**&#x200B;欄位從右側的&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖放到表單的中繼資料區段。
1. 按一下新新增的欄位，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;面板中執行下列更新：
   1. 將&#x200B;**[!UICONTROL 欄位標籤]**&#x200B;變更為&#x200B;_核准目標_。
   1. 將&#x200B;**[!UICONTROL 對應更新至屬性]**&#x200B;至&#x200B;_。/jcr：content/metadata/dam：activationTarget_。
   1. 以`contenthub`和`delivery`作為選項值新增選項。

   >[!NOTE]
   >
   >當您使用Assets檢視選取核准目標為Content Hub時，屬於相同組織的使用者可在Content Hub中使用資產。 當您選取核准目標為傳送時，資產可供所有使用者使用。
1. 按一下「**[!UICONTROL 儲存]**」。
1. 在&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面中，選取新建立的中繼資料設定檔。
1. 按一下頂端動作列中的&#x200B;**[!UICONTROL 套用中繼資料設定檔至資料夾]**。
1. 選取您需要核准的資料夾，然後按一下[套用]。****
   <br>整個資料夾的許可權已設定為待核准，且任何上傳至此資料夾的資產都會自動核准。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>此方法會核准資料夾中新建立的資產。 針對資料夾中的現有資產，您需要手動選取並核准它們。 <br>或者，您可以使用&#x200B;**[!UICONTROL 重新處理]**&#x200B;選項，將中繼資料設定檔的變更套用至較舊的資產。

同樣地，若要在Assets檢視中大量核准資料夾內的資產：

1. 選取資產，然後按一下「**[!UICONTROL 大量中繼資料編輯]**」。

1. 在右側面板「[!UICONTROL 屬性]」區段內提供的「**[!UICONTROL 狀態]**」欄位中，選取「**[!UICONTROL 已核准]**」。

   如果您將狀態選取為`Approved`，並且已為您的Experience Manager Assets啟用[具有OpenAPI功能的Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)或[Content Hub](/help/assets/product-overview.md)，或兩者皆已啟用，則您可以在&#x200B;**[!UICONTROL 核准目標]**&#x200B;欄位中檢視`Delivery`和`Content Hub`可用選項。

   * 選取&#x200B;**[!UICONTROL 傳送]**，讓具備OpenAPI功能的Dynamic Media與Content Hub都能使用資產。 如果您未啟用Content Hub，選取此選項會讓資產僅供具有OpenAPI功能的Dynamic Media使用。
   * 選取&#x200B;**[!UICONTROL Content Hub]**，讓資產可供Content Hub使用。

   ![核准狀態](/help/assets/assets/approval-status-delivery.png)

   如果您未使用預設的中繼資料表單，且無法檢視&#x200B;**[!UICONTROL 核准目標]**&#x200B;欄位，請[編輯您的中繼資料表單](/help/assets/metadata-assets-view.md#metadata-forms)，將&#x200B;**[!UICONTROL 的]**&#x200B;核准欄位從可用元件拖曳到中繼資料表單，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   >[!NOTE]
   >
   >如果您使用組織內的Assets檢視選取核准目標為`Content Hub`，則屬於相同組織的使用者可在Content Hub中使用資產。

1. 按一下「**[!UICONTROL 儲存]**」。

## 複製已核准資產的傳遞URL {#copy-delivery-url-approved-assets}

如果您在AEM as a Cloud Service執行個體上啟用了[!UICONTROL 具有OpenAPI功能的Dynamic Media]，則存放庫中所有已核准資產的傳送URL都可使用。

若要複製存放庫中已核准資產的傳送URL：

1. 選取資產並按一下&#x200B;**[!UICONTROL 詳細資料]**。

1. 按一下右窗格中可用的Dynamic Media圖示。

1. 選取&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;面板中可用的&#x200B;**[!UICONTROL Dynamic Media with OpenAPI]**。

1. 按一下&#x200B;**[!UICONTROL 複製URL]**以複製資產的傳遞URL。
   ![動態轉譯](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   >在Assets檢視中，剛提供複製已核准資產之傳送URL的選項。

如需Dynamic Media面板中顯示之其他轉譯的相關資訊，請參閱[檢視及下載Dynamic Media轉譯](/help/assets/renditions.md#view-download-dm-renditions)。
