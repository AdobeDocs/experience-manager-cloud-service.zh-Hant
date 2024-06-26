---
title: 在Experience Manager中核准資產
description: 瞭解如何核准中的資產 [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# 核准中的資產 [!DNL Experience Manager]

品牌經理和行銷人員對品牌資產維持嚴格的控制。 該資產僅供經核准和最新版本的使用，以確保所有管道和應用程式的品牌一致性。

您可以在AEM Assets中核准資產，以簡化資產管理，確保處理資產的程式受到控制且有效率。

## 開始之前 {#pre-requisites}

您必須擁有AEM Assetsas a Cloud Service的存取權以及編輯 **[!UICONTROL 檢閱狀態]** 屬性來建立資產。

## 設定

在核准資產之前，您需要對管理員檢視中適用的中繼資料結構做一次性的更新。 您可以略過Assets檢視的此設定。 請依照下列步驟設定中繼資料結構：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構]**.
1. 選取適用的中繼資料結構，然後按一下 **[!UICONTROL 編輯]**. <br>此 **[!UICONTROL 中繼資料結構表單編輯器]** 開啟時使用 **[!UICONTROL 基本]** 索引標籤反白顯示。
1. 向下捲動並按一下 **[!UICONTROL 檢閱狀態]**.
1. 按一下 **[!UICONTROL 規則]** 標籤在右側面板。
1. 取消核取 **[!UICONTROL 停用編輯]** 並按一下 **[!UICONTROL 儲存]**.
如果您需要檢視 **[!UICONTROL 檢閱狀態]** 欄位已對應至，請導覽至 **[!UICONTROL 設定]** 標籤並檢視 `./jcr:content/metadata/dam:status` 中的值 **[!UICONTROL 對應至屬性]** 欄位。

>[!NOTE]
>
>如果您的資產或資料夾具有不同的預設結構描述，請務必在該特定結構描述中進行此更新。

## 核准資產 {#approve-assets}

您可以同時核准以下兩個中的資產： [!DNL Experience Manager] 和 [!DNL Experience Manager Assets]. 若要核准中的資產 [!DNL Experience Manager]，請遵循下列步驟：

1. 選取資產並按一下 **[!UICONTROL 屬性]** 在頂端窗格中。
1. 在 **[!UICONTROL 基本]** 標籤，向下捲動至 **[!UICONTROL 檢閱狀態]**.
1. 將稽核狀態變更為 **[!UICONTROL 已核准]**.
   ![影像](/help/assets/assets/approve-old-ui.png)
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同樣地，您可以使用核准資產 [新增Assets檢視](/help/assets/manage-organize-assets-view.md).

## 大量核准資產 {#bulk-approve-assets}

一次快速核准多個資產，簡化工作流程。 您可以大量核准資產，以加快核准程式，節省時間並提高生產力。
<br>請依照下列步驟，核准中的大量資產 [!DNL Experience Manager]：

1. 在作者環境中建立資料夾(https://author-pXXX-eYYY.adobeaemcloud.com)。 取代 _XXX_ 使用您的方案ID和 _YYYY_ Experience Manager的環境ID識別碼。
1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**.
1. 按一下 **[!UICONTROL 建立]** ，位於頁面的右上角。
1. 新增設定檔標題並按一下 **[!UICONTROL 建立]**. 已成功建立中繼資料設定檔。
1. 選取新建立的中繼資料設定檔，然後按一下 **[!UICONTROL 編輯 _(e)_]**. <br>此&#x200B;**[!UICONTROL 編輯中繼資料設定檔]**表單開啟&#x200B;**[!UICONTROL 基本]**索引標籤反白顯示。
1. 拖放 **[!UICONTROL 單行文字欄位]** 從 **[!UICONTROL 建置表單]** 區段至表單中的中繼資料區段。
1. 按一下新新增的欄位，然後在 **[!UICONTROL 設定]** 面板：
   1. 變更 **[!UICONTROL 欄位標籤]** 至 _已核准的Assets_.
   1. 更新 **[!UICONTROL 對應至屬性]** 至 _./jcr：content/metadata/dam：status_.
   1. 變更預設值為 _已核准_.

1. 按一下「**[!UICONTROL 儲存]**」。
1. 在 **[!UICONTROL 中繼資料設定檔]** 頁面上，選取新建立的中繼資料設定檔。
1. 按一下 **[!UICONTROL 套用中繼資料設定檔至資料夾]** 頂端動作列中的。
1. 選取您需要核准的資料夾，然後按一下 **[!UICONTROL 套用]**.
   <br> 系統會設定整個資料夾的許可權以供核准，且會自動核准上傳至此資料夾的任何資產。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>此方法會核准資料夾中新建立的資產。 針對資料夾中的現有資產，您需要手動選取並核准它們。 <br> 或者，您可以使用 **[!UICONTROL 重新處理]** 將中繼資料設定檔的變更套用至較舊資產的選項。

同樣地，若要在Assets檢視中大量核准資料夾內的資產：

1. 選取資產並按一下 **[!UICONTROL 大量中繼資料編輯]**.

1. 選取 **[!UICONTROL 已核准]** 在 **[!UICONTROL 狀態]** 中的可用欄位 [!UICONTROL 屬性] 區段。

1. 按一下「**[!UICONTROL 儲存]**」。

## 複製已核准資產的傳遞URL {#copy-delivery-url-approved-assets}

如果具備下列條件，則儲存庫中所有已核准資產的傳送URL都可供使用 [!UICONTROL 具有OpenAPI功能的Dynamic Media] 已在您的AEM as a Cloud Service執行個體上啟用。

若要複製存放庫中已核准資產的傳送URL：

1. 選取資產並按一下 **[!UICONTROL 詳細資料]**.

1. 按一下右窗格中的「轉譯」圖示。

1. 選取 **[!UICONTROL Dynamic Media與OpenAPI]** 可在 **[!UICONTROL 動態]** 區段。

1. 按一下 **[!UICONTROL 複製URL]** 以複製資產的傳遞URL。
   ![複製傳遞URL](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >在Assets檢視中，剛提供複製已核准資產之傳送URL的選項。

