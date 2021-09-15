---
title: 在 [!DNL Assets]中管理 [!DNL Adobe Stock] 資產。
description: 從 [!DNL Adobe Experience Manager]內搜尋、擷取、授權及管理 [!DNL Adobe Stock] 資產。 將授權資產作為任何其他數位資產使用。
contentOwner: AG
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 3%

---

# 在[!DNL Adobe Experience Manager Assets]中使用[!DNL Adobe Stock]資產 {#use-adobe-stock-assets-in-aem-assets}

組織可將其[!DNL Adobe Stock]企業計畫與[!DNL Experience Manager Assets]整合，以確保授權資產可廣泛用於其創意和行銷專案，並具備[!DNL Experience Manager]的強大資產管理功能。

[!DNL Adobe Stock] 該服務為設計人員和企業提供數百萬張高質量、精心策劃、免版稅的照片、向量圖、插圖、視頻、模板和3D資產，供其所有創意項目使用。[!DNL Experience Manager] 使用者無需離開介面，即可快速尋 [!DNL Adobe Stock] 找、預覽和授 [!DNL Experience Manager]權儲存在中的 [!DNL Experience Manager] 資產。

## 整合[!DNL Experience Manager]和[!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

要在[!DNL Experience Manager]和[!DNL Adobe Stock]之間建立通信，請在[!DNL Experience Manager]中建立IMS配置和[!DNL Adobe Stock]配置。

>[!NOTE]
>
>只有組織的[!DNL Experience Manager]管理員和[!DNL Admin Console]管理員才能執行整合，因為整合需要管理員權限。

### 建立IMS設定 {#create-an-ims-configuration}

1. 在[!DNL Experience Manager]使用者介面中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**。 按一 **[!UICONTROL 下「建立]** 」，然後選 **[!UICONTROL 取「雲端解決方案]** > **[!UICONTROL Adobe Stock]**」。
1. 重複使用現有證書或選擇&#x200B;**[!UICONTROL 建立新證書]**。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。建立後，下載公開金鑰。 按一下&#x200B;**[!UICONTROL 下一步]**。[!UICONTROL Adobe IMS技術帳戶設定]畫面保持開啟，以便不久提供所需值。
1. 訪問[Adobe開發人員控制台](https://console.adobe.io)。 確認您的帳戶擁有需要整合之組織的管理員權限。
1. 按一下「**[!UICONTROL 建立新專案]**」，然後按一下「**[!UICONTROL 新增API]**」。 從可用的API清單中選取&#x200B;**[!UICONTROL Adobe Stock]**。 選擇[!UICONTROL OAUTH 2.0 Web]。
1. 提供&#x200B;**[!UICONTROL 預設重定向URI]**&#x200B;和&#x200B;**[!UICONTROL 重定向URI模式]**&#x200B;值。 按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。複製產生的ID和機密。
1. 在[!UICONTROL Adobe IMS技術帳戶設定]畫面中，提供標題為&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Authorization Server]**、**[!UICONTROL API金鑰]**、**[!UICONTROL Client Secret]**&#x200B;和&#x200B;**[!UICONTROL Payload]**&#x200B;的方塊中的值。 有關這些值的詳細資訊，請參閱[JWT驗證快速入門](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)。

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 在[!DNL Experience Manager]中建立[!DNL Adobe Stock]配置 {#create-adobe-stock-configuration-in-aem}

1. 在[!DNL Experience Manager]中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以建立設定，並將其與您現有的IMS設定建立關聯。 選擇`PROD`作為環境參數。
1. 在&#x200B;**[!UICONTROL 授權資產路徑]**&#x200B;欄位中，保留原樣的位置。 請勿變更要儲存[!DNL Adobe Stock]資產的位置。
1. 新增所有必要屬性以完成建立。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。
1. 新增[!DNL Experience Manager]使用者或群組，讓其授權資產。

>[!NOTE]
>
>如果有多個[!DNL Adobe Stock]配置，請在「用戶首選項」面板中選擇所需的配置。 要從Experience Manager首頁訪問面板，請按一下用戶表徵圖，然後按一下&#x200B;**[!UICONTROL 用戶首選項]** > **[!UICONTROL 庫存配置]**。

## 在[!DNL Experience Manager]中使用及管理[!DNL Adobe Stock]資產 {#usemanage}

使用此功能，組織使用者可以在[!DNL Experience Manager Assets]中使用[!DNL Adobe Stock]資產。 從[!DNL Experience Manager]使用者介面中，使用者可以搜尋[!DNL Adobe Stock]資產並授權所需資產。

在[!DNL Experience Manager]中授權[!DNL Adobe Stock]資產後，就可像一般資產一樣使用和管理該資產。 在[!DNL Experience Manager]中，使用者可以搜尋及預覽資產；複製並發佈資產；在[!DNL Brand Portal]上共用資產；透過[!DNL Experience Manager]案頭應用程式存取及使用資產；等等。

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### 尋找資產 {#find-assets}

您的[!DNL Experience Manager]使用者可以同時在[!DNL Experience Manager]和[!DNL Adobe Stock]中搜尋資產。 當搜索位置不限於[!DNL Adobe Stock]時，將顯示[!DNL Experience Manager]和[!DNL Adobe Stock]的搜索結果。

* 若要搜尋[!DNL Adobe Stock]資產，請按一下「**[!UICONTROL 導覽]** > **[!UICONTROL 資產]** > **[!UICONTROL 搜尋Adobe Stock]**」。

* 若要在[!DNL Adobe Stock]和[!DNL Experience Manager Assets]之間搜尋資產，請按一下搜尋![search](assets/do-not-localize/search_icon.png)。

或者，開始在搜尋列中輸入`Location: Adobe Stock`以選取[!DNL Adobe Stock]資產。 [!DNL Experience Manager] 針對所搜尋的資產提供進階篩選功能，讓使用者能使用篩選器（例如支援的資產類型、影像方向和授權狀態），快速將目標鎖定於所需的資產。

>[!NOTE]
>
>從[!DNL Adobe Stock]搜尋的資產只會顯示在[!DNL Experience Manager]中。 [!DNL Adobe Stock] 只有在使用者儲存資產或 [!DNL Experience Manager] 授權並儲存資產後，資 [產才](/help/assets/aem-assets-adobe-stock.md#saveassets) 會 [擷取並儲存在存放庫中](/help/assets/aem-assets-adobe-stock.md#licenseassets)。已儲存在[!DNL Experience Manager]中的資產會顯示並反白顯示，以方便參考和存取。 此外，會將[!DNL Stock]資產與一些其他中繼資料一起儲存，以將來源指示為[!DNL Stock]。

![在Experience Manager中搜尋篩選器，並在搜尋結果中強調顯示Adobe Stock資產](assets/aem-search-filters2.jpg)

*圖：在搜尋結果中 [!DNL Experience Manager] 和反白 [!DNL Adobe Stock] 顯示的資產搜尋篩選器。*

### 儲存並檢視所需資產 {#saveassets}

選取您要儲存在[!DNL Experience Manager]中的資產。 按一下頂端工具列中的[!UICONTROL 儲存] ，並提供資產的名稱和位置。 未授權的資產會以浮水印儲存在本機。

下次搜尋資產時，儲存的資產會以徽章強調顯示，以指出這些資產可在[!DNL Experience Manager Assets]中使用。

>[!NOTE]
>
>最近新增的資產會顯示「新」徽章，而非「授權」徽章。

### 授權資產 {#licenseassets}

使用者可使用其[!DNL Adobe Stock]企業計畫的配額來授權[!DNL Adobe Stock]資產。 當您授權資產時，資產會不含浮水印而儲存，且可供搜尋及使用於[!DNL Experience Manager Assets]中。

![對話方塊，以授權並儲存Adobe StockExperience Manager資產](assets/aem-stock_licenseandsave.jpg)

*圖：對話方塊，以在中授權 [!DNL Adobe Stock] 和儲存 [!DNL Experience Manager Assets]資產。*

### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取和預覽中繼資料，包括[!DNL Experience Manager]中儲存之資產的[!DNL Adobe Stock]中繼資料屬性，以及為資產新增&#x200B;**[!UICONTROL 授權參考]**。 不過，在[!DNL Experience Manager]和[!DNL Adobe Stock]網站之間未同步授權參考更新。

使用者可以查看授權和未授權資產的屬性。

![檢視及存取儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)

*圖：檢視及存取儲存資產的中繼資料和授權參考。*

## 已知限制 {#known-limitations}

* **未顯示編輯影像警告**:授權影像時，使用者無法檢查影像是否為「僅編輯使用」。為了防止可能的誤用，管理員可以關閉Admin Console對編輯資產的存取權。

* **顯示的許可證類型錯誤**:資產的中可能顯示錯誤的授 [!DNL Experience Manager] 權類型。用戶可以登錄[!DNL Adobe Stock]網站查看許可類型。

* **未同步參考欄位和中繼資料**:當用戶更新許可證參考欄位時，許可證參考資訊在中更新，但 [!DNL Experience Manager] 不在網站上 [!DNL Adobe Stock] 更新。同樣地，如果用戶更新[!DNL Adobe Stock]網站上的引用欄位，則在[!DNL Experience Manager]中不會同步更新。

>[!MORELIKETHIS]
>
>* [有關搭配使用Adobe Stock資產和Experience Manager資產的教學課程影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock企業計畫說明](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常見問題集](https://helpx.adobe.com/stock/faq.html)

